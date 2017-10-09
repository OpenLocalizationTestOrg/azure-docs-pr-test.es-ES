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
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="bfb3b-103">Implementación de aplicaciones con plantillas de Azure Resource Manager para máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="bfb3b-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="bfb3b-104">Una vez que ha identificado todos los requisitos de infraestructura Azure y convertir en una plantilla de implementación, implementación de aplicaciones reales de hello debe toobe dirigido.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="bfb3b-105">Implementación de la aplicación hace referencia tooinstalling archivos binarios de aplicación real de hello en recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="bfb3b-106">Para el ejemplo de Hola a tienda de música, .net Core y NGINX, Supervisor necesitan toobe instalado y configurado en cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-106">For hello Music Store sample, .Net Core, NGINX, and Supervisor need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="bfb3b-107">Hola tienda de música binarios necesitan toobe instalado en la máquina virtual de Hola y Hola base de datos de almacén de música crean previamente.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="bfb3b-108">Este documento detalla cómo las extensiones de máquina Virtual pueden automatizar la aplicación implementación y configuración tooAzure máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="bfb3b-109">Se resaltan todas las dependencias y configuraciones únicas.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="bfb3b-110">Para la mejor experiencia de hello, implementar previamente una instancia de hello solución tooyour suscripción de Azure y trabajar junto con la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="bfb3b-111">plantilla de Hello completa puede encontrarse aquí: [implementación de la tienda de música en Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="bfb3b-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="bfb3b-112">Script de configuración</span><span class="sxs-lookup"><span data-stu-id="bfb3b-112">Configuration script</span></span>
<span data-ttu-id="bfb3b-113">Las extensiones de máquina virtual son programas especializados que se ejecuta en máquinas virtuales tooprovide automatización de las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="bfb3b-114">Hay extensiones disponibles para muchos fines específicos, como antivirus, configuración de registro y configuración de Docker.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="bfb3b-115">Una extensión de la secuencia de comandos personalizada puede ser usado toorun una secuencia de comandos en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-115">A custom script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="bfb3b-116">Con el ejemplo de Hola a tienda de música, se las máquinas de toohello secuencia de comandos personalizada extensión tooconfigure Hola Ubuntu virtuales e instalar aplicación de tienda de música de hello.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Ubuntu virtual machines and install hello Music Store application.</span></span> 

<span data-ttu-id="bfb3b-117">Antes de que detalla cómo se declaran las extensiones de máquina virtual en una plantilla de Azure Resource Manager, examine el script de Hola que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="bfb3b-118">Este script configura la máquina virtual de Ubuntu Hola Hola toohost aplicación de tienda de música.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-118">This script configures hello Ubuntu virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="bfb3b-119">Cuando se ejecuta, el script de Hola instala el software que necesite todos los, instalar la aplicación hello de la tienda de música desde control de código fuente y preparar la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

<span data-ttu-id="bfb3b-120">toolearn más información acerca de hospedaje de .net Core aplicación en Linux, consulte [entorno de producción de publicación tooa Linux](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="bfb3b-120">toolearn more about hosting a .Net Core application on Linux, see [Publish tooa Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="bfb3b-121">Este ejemplo es para fines de demostración.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-121">This sample is for demonstration purposes.</span></span>
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

## <a name="vm-script-extension"></a><span data-ttu-id="bfb3b-122">Extensión de script de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bfb3b-122">VM Script Extension</span></span>
<span data-ttu-id="bfb3b-123">Extensiones de máquina virtual se puede ejecutar en una máquina virtual en tiempo de compilación mediante la inclusión de recursos de extensión de hello en la plantilla de hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-123">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="bfb3b-124">extensión de Hola se puede agregar con el Asistente para agregar recursos de Visual Studio de hello, o mediante la inserción de un valor JSON válido en la plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-124">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="bfb3b-125">Hola recursos de extensión de Script está anidada dentro de hello recursos de máquina Virtual; Esto puede verse en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-125">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="bfb3b-126">Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [extensión de Script de máquina virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="bfb3b-126">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="bfb3b-127">Tenga en cuenta que en hello siguiente JSON que Hola script se almacena en GitHub.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-127">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="bfb3b-128">Este script también podría almacenarse en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="bfb3b-129">Además, las plantillas de Azure Resource Manager permiten tooconstructed de cadena de ejecución de script de Hola tal que los valores de parámetros de plantilla se pueden utilizar como parámetros para la ejecución del script.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-129">Also, Azure Resource Manager templates allow hello script execution string tooconstructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="bfb3b-130">En este caso se proporcionan datos al implementar plantillas de hello y, a continuación, se pueden utilizar estos valores cuando se ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfb3b-130">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="bfb3b-131">Para obtener más información sobre el uso de la extensión de script personalizado de hello, consulte [las extensiones de script personalizado con el Administrador de recursos plantillas](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bfb3b-131">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="bfb3b-132">siguiente paso</span><span class="sxs-lookup"><span data-stu-id="bfb3b-132">Next Step</span></span>
<hr>

[<span data-ttu-id="bfb3b-133">Más plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bfb3b-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

