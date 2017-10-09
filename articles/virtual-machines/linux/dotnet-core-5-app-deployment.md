---
title: "Implementación de aplicación con extensiones de máquina Virtual aaaAutomating | Documentos de Microsoft"
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>Implementación de aplicaciones con plantillas de Azure Resource Manager para máquinas virtuales Linux

Una vez que ha identificado todos los requisitos de infraestructura Azure y convertir en una plantilla de implementación, implementación de aplicaciones reales de hello debe toobe dirigido. Implementación de la aplicación hace referencia tooinstalling archivos binarios de aplicación real de hello en recursos de Azure. Para el ejemplo de Hola a tienda de música, .net Core y NGINX, Supervisor necesitan toobe instalado y configurado en cada máquina virtual. Hola tienda de música binarios necesitan toobe instalado en la máquina virtual de Hola y Hola base de datos de almacén de música crean previamente.

Este documento detalla cómo las extensiones de máquina Virtual pueden automatizar la aplicación implementación y configuración tooAzure máquinas virtuales. Se resaltan todas las dependencias y configuraciones únicas. Para la mejor experiencia de hello, implementar previamente una instancia de hello solución tooyour suscripción de Azure y trabajar junto con la plantilla de hello Azure Resource Manager. plantilla de Hello completa puede encontrarse aquí: [implementación de la tienda de música en Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="configuration-script"></a>Script de configuración
Las extensiones de máquina virtual son programas especializados que se ejecuta en máquinas virtuales tooprovide automatización de las configuraciones. Hay extensiones disponibles para muchos fines específicos, como antivirus, configuración de registro y configuración de Docker. Una extensión de la secuencia de comandos personalizada puede ser usado toorun una secuencia de comandos en una máquina virtual. Con el ejemplo de Hola a tienda de música, se las máquinas de toohello secuencia de comandos personalizada extensión tooconfigure Hola Ubuntu virtuales e instalar aplicación de tienda de música de hello. 

Antes de que detalla cómo se declaran las extensiones de máquina virtual en una plantilla de Azure Resource Manager, examine el script de Hola que se ejecuta. Este script configura la máquina virtual de Ubuntu Hola Hola toohost aplicación de tienda de música. Cuando se ejecuta, el script de Hola instala el software que necesite todos los, instalar la aplicación hello de la tienda de música desde control de código fuente y preparar la base de datos de Hola. 

toolearn más información acerca de hospedaje de .net Core aplicación en Linux, consulte [entorno de producción de publicación tooa Linux](https://docs.asp.net/en/latest/publishing/linuxproduction.html).

> Este ejemplo es para fines de demostración.
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a>Extensión de script de máquina virtual
Extensiones de máquina virtual se puede ejecutar en una máquina virtual en tiempo de compilación mediante la inclusión de recursos de extensión de hello en la plantilla de hello Azure Resource Manager. extensión de Hola se puede agregar con el Asistente para agregar recursos de Visual Studio de hello, o mediante la inserción de un valor JSON válido en la plantilla de Hola. Hola recursos de extensión de Script está anidada dentro de hello recursos de máquina Virtual; Esto puede verse en el siguiente ejemplo de Hola.

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [extensión de Script de máquina virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359). 

Tenga en cuenta que en hello siguiente JSON que Hola script se almacena en GitHub. Este script también podría almacenarse en Azure Blob Storage. Además, las plantillas de Azure Resource Manager permiten tooconstructed de cadena de ejecución de script de Hola tal que los valores de parámetros de plantilla se pueden utilizar como parámetros para la ejecución del script. En este caso se proporcionan datos al implementar plantillas de hello y, a continuación, se pueden utilizar estos valores cuando se ejecute el script de Hola.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Para obtener más información sobre el uso de la extensión de script personalizado de hello, consulte [las extensiones de script personalizado con el Administrador de recursos plantillas](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="next-step"></a>siguiente paso
<hr>

[Más plantillas de Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

