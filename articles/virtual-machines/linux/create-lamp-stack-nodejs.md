---
title: "aaaDeploy LAMP en una máquina virtual de Linux con hello 1.0 de CLI de Azure | Documentos de Microsoft"
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
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a>Implementar pila LAMP con hello Azure CLI 1.0
Este artículo le guiará a través de cómo toodeploy un Apache web server, MySQL y PHP (pila LAMP de Hola) en Azure. Necesita una cuenta de Azure ([obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/)) hello y [CLI de Azure](../../cli-install-nodejs.md) decir [conectado tooyour cuenta de Azure](../../xplat-cli-connect.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure CLI 1.0] – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* Implementar LAMP en una máquina virtual existente

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Tutorial de implementación de LAMP en una nueva VM
Primero debe crear un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md) que contendrá Hola nueva máquina virtual:

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

toocreate Hola propia máquina virtual, puede usar una plantilla de Azure Resource Manager ya escrito [aquí en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

Debería obtener una respuesta en la que se pide introducir algunos datos más:

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

Ahora ha creado una máquina virtual Linux con la pila LAMP ya instalada. Si lo desea, puede comprobar la instalación Hola saltar hacia abajo demasiado[comprobar luz correctamente instalada](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Tutorial de implementación de LAMP en una VM existente
Si necesita ayuda para crear una VM de Linux, puede ir [toolearn aquí cómo toocreate una VM Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). A continuación, debe tooSSH en hello VM de Linux. Si necesita ayuda para crear una clave SSH, puede ir [toolearn aquí cómo toocreate una clave SSH en Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Si ya tiene una clave SSH, continúe y acceda mediante SSH desde la línea de comandos a la VM Linux con `ssh exampleUsername@exampleDNS`.

Ahora que está trabajando en la VM de Linux, podemos guiaremos por la instalación pila LAMP de hello en distribuciones de Debian. comandos de Hello exacta podrían ser diferente en otras distribuciones de Linux.

#### <a name="installing-on-debianubuntu"></a>Instalación en Debian y Ubuntu
Necesita Hola siguiendo los paquetes instalados: `apache2`, `mysql-server`, `php5`, y `php5-mysql`. Puede instalarlos directamente o mediante Tasksel. A continuación, se muestran las instrucciones para ambas opciones.
Antes de instalar toodownload es necesario y, a continuación, actualizar las listas de paquete.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Paquetes individuales
Uso de apt-get:

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Uso de tasksel
Como alternativa, puede descargar Tasksel, una herramienta de Debian y Ubuntu que instala varios paquetes relacionados como una tarea coordinada en el sistema.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

Después de ejecutar cualquiera de las opciones anteriores hello, que se van a ser solicitada tooinstall estos paquetes y varias otras dependencias. Presione 's' y, a continuación, 'ENTRAR' toocontinue y siga los otro tooset solicita una contraseña administrativa para MySQL. Esto instala Hola mínimo necesario PHP extensiones necesarias toouse PHP con MySQL. 

![][1]

Ejecute hello después comando toosee otras extensiones PHP que están disponibles como paquetes:

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>Creación de documento info.php
Ahora debería ser capaz de toocheck qué versión de Apache, MySQL y PHP tiene a través de la línea de comandos de hello escribiendo `apache2 -v`, `mysql -v`, o `php -v`.

Si la diferencia como tootest más, puede crear un rápido tooview de página de información PHP en un explorador. Cree un archivo con el editor de texto Nano ejecutando este comando:

    user@ubuntu$ sudo nano /var/www/html/info.php

En el editor de texto de GNU Nano hello, agregar Hola siguientes líneas:

    <?php
    phpinfo();
    ?>

Después, guarde y cierre el editor de texto hello.

Reinicie Apache con este comando para que todas las nuevas instalaciones surtan efecto.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Comprobación de que LAMP se ha instalado correctamente
Ahora puede comprobar la página de información de hello PHP que creó, abra un explorador y vaya toohttp://youruniqueDNS/info.php. Debería ser una imagen toothis similar.

![][2]

Puede comprobar la instalación de Apache viendo Hola Apache2 Ubuntu Default Page yendo tooyou http://youruniqueDNS/. Debe ver algo parecido a esta imagen.

![][3]

Enhorabuena. Ya ha instalado una pila LAMP en la máquina virtual de Azure.

## <a name="next-steps"></a>Pasos siguientes
Desproteger Hola Ubuntu documentación en pila LAMP de hello:

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png