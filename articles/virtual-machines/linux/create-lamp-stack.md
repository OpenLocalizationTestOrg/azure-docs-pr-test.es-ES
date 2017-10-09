---
title: "aaaDeploy LAMP en una máquina virtual de Linux en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall Hola LAMP la pila en una VM de Linux en Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a>Implementación de la pila LAMP en Azure
Este artículo le guiará a través de cómo toodeploy un Apache web server, MySQL y PHP (pila LAMP de Hola) en Azure. Necesita una cuenta de Azure ([obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/)) hello y [CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2). También puede realizar estos pasos con hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-command-summary"></a>Resumen rápido de comandos

1. Guardar y editar hello [azuredeploy.parameters.json archivo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preferencia en el equipo local.
2. Ejecute hello siguiendo dos toocreate de comandos de un grupo de recursos y, a continuación, implementar la plantilla:

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>Implementar LAMP en una máquina virtual existente
siguiente Hola comandos paquetes de actualizaciones y, a continuación, instala Apache, MySQL y PHP:

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Tutorial de implementación de LAMP en una nueva VM

1. Crear un grupo de recursos con [crear grupo az](/cli/azure/group#create) toocontain Hola nueva máquina virtual:

```azurecli
az group create -l westus -n myResourceGroup
```
toocreate Hola propia máquina virtual, puede usar una plantilla de Azure Resource Manager ya escrito [aquí en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

2. Guardar hello [azuredeploy.parameters.json archivo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour de equipo local.
3. Editar hello **azuredeploy.parameters.json** tooyour de archivo preferido entradas.
4. Implementar la plantilla de hello con [Crear implementación de grupo az] hace referencia a Hola Descargar archivo json:

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

Hola de salida es similar toohello siguiente ejemplo:

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

Ahora ha creado una máquina virtual Linux con la pila LAMP ya instalada. Si lo desea, puede comprobar la instalación Hola saltar hacia abajo demasiado[comprobar luz correctamente instalada](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Tutorial de implementación de LAMP en una VM existente
Si necesita ayuda para crear una VM de Linux, puede ir [toolearn aquí cómo toocreate una VM Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli). A continuación, debe tooSSH en hello VM de Linux. Si necesita ayuda para crear una clave SSH, puede ir [toolearn aquí cómo toocreate una clave SSH en Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Si ya tiene una clave SSH, continúe y acceda mediante SSH desde la línea de comandos a la VM Linux con `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.

Ahora que está trabajando en la VM de Linux, podemos guiaremos por la instalación pila LAMP de hello en distribuciones de Debian. comandos de Hello exacta podrían ser diferente en otras distribuciones de Linux.

#### <a name="installing-on-debianubuntu"></a>Instalación en Debian y Ubuntu
Necesita Hola siguiendo los paquetes instalados: `apache2`, `mysql-server`, `php5`, y `php5-mysql`. Puede instalarlos directamente o mediante Tasksel.
Antes de instalar toodownload es necesario y, a continuación, actualizar las listas de paquete.

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a>Paquetes individuales
Uso de apt-get:

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a>Uso de tasksel
Como alternativa, puede descargar Tasksel, una herramienta de Debian y Ubuntu que instala varios paquetes relacionados como una tarea coordinada en el sistema.

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

Después de ejecutar cualquiera de las opciones anteriores hello, que se van a ser solicitada tooinstall estos paquetes y varias otras dependencias. tooset una contraseña administrativa para MySQL, presione 's' y, a continuación, 'ENTRAR' toocontinue y siga las indicaciones de otros. Este proceso instala Hola mínimo necesario PHP extensiones necesarias toouse PHP con MySQL. 

![][1]

Ejecute hello después comando toosee otras extensiones PHP que están disponibles como paquetes:

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>Creación de documento info.php
Ahora debería ser capaz de toocheck qué versión de Apache, MySQL y PHP tiene a través de la línea de comandos de hello escribiendo `apache2 -v`, `mysql -v`, o `php -v`.

Si la diferencia como tootest más, puede crear un rápido tooview de página de información PHP en un explorador. Cree un archivo con el editor de texto Nano ejecutando este comando:

```bash
sudo nano /var/www/html/info.php
```

En el editor de texto de GNU Nano hello, agregar Hola siguientes líneas:

```php
<?php
phpinfo();
?>
```

Después, guarde y cierre el editor de texto hello.

Reinicie Apache con este comando para que todas las nuevas instalaciones surtan efecto.

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>Comprobación de que LAMP se ha instalado correctamente
Ahora puede comprobar la página de información de hello PHP que creó, abra un explorador y vaya toohttp://youruniqueDNS/info.php. Debería ser una imagen toothis similar.

![][2]

Puede comprobar la instalación de Apache viendo Hola Apache2 Ubuntu Default Page yendo tooyou http://youruniqueDNS/. Hola de salida es similar toohello siguiente ejemplo:

![][3]

Enhorabuena. Ya ha instalado una pila LAMP en la máquina virtual de Azure.

## <a name="next-steps"></a>Pasos siguientes
Desproteger Hola Ubuntu documentación en pila LAMP de hello:

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
