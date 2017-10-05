---
title: "Implementación de LAMP en una máquina virtual Linux con la CLI de Azure 1.0 | Microsoft Docs"
description: Aprender a instalar la pila LAMP en una VM Linux en Azure
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
ms.openlocfilehash: feba2fb20d1831e92358ff5d1b4c9589d63d28dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-with-the-azure-cli-10"></a>Implementar la pila LAMP con la CLI de Azure 1.0
En este artículo se ofrecen instrucciones paso a paso sobre cómo implementar un servidor web Apache, MySQL y PHP (la pila LAMP) en Azure. Necesita una cuenta de Azure ([consiga una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/)) y la [CLI de Azure](../../cli-install-nodejs.md) que esté [conectada a su cuenta de Azure](../../xplat-cli-connect.md).

## <a name="cli-versions-to-complete-the-task"></a>Versiones de la CLI para completar la tarea
Puede completar la tarea mediante una de las siguientes versiones de la CLI:

- [CLI de Azure 1.0]: CLI para los modelos de implementación clásico y de Resource Manager (este artículo)
- [CLI de Azure 2.0 ](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): CLI de última generación para el modelo de implementación de administración de recursos

```
# One command to create a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* Implementar LAMP en una máquina virtual existente

```
# Two commands: one updates packages, the other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Tutorial de implementación de LAMP en una nueva VM
Para empezar, cree un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md) que contendrá la nueva VM:

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

Para crear la máquina virtual, puede usar una de las plantillas de Azure Resource Manager que se encuentran [en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

Debería obtener una respuesta en la que se pide introducir algunos datos más:

    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment to complete
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

Ahora ha creado una máquina virtual Linux con la pila LAMP ya instalada. Si lo desea, puede comprobar la instalación pasando directamente a la sección [Comprobación de que LAMP se ha instalado correctamente](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Tutorial de implementación de LAMP en una VM existente
Si necesita ayuda con el proceso de creación de una VM Linux, puede visitar [esta página para aprender a hacerlo](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). A continuación, necesita acceder mediante SSH a la VM Linux. Si necesita ayuda con el proceso de creación de una clave SSH, puede visitar [esta página para aprender a hacerlo en Linux o Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Si ya tiene una clave SSH, continúe y acceda mediante SSH desde la línea de comandos a la VM Linux con `ssh exampleUsername@exampleDNS`.

Ahora que ya puede entrar en la VM Linux para trabajar, le enseñaremos a instalar paso a paso la pila LAMP en distribuciones basadas en Debian. Los comandos exactos podrían ser diferentes en otras distribuciones de Linux.

#### <a name="installing-on-debianubuntu"></a>Instalación en Debian y Ubuntu
Necesitará tener instalados los siguientes paquetes: `apache2`, `mysql-server`, `php5` y `php5-mysql`. Puede instalarlos directamente o mediante Tasksel. A continuación, se muestran las instrucciones para ambas opciones.
Antes de instalarlos, debe descargar y actualizar las listas de paquetes.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Paquetes individuales
Uso de apt-get:

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Uso de tasksel
Como alternativa, puede descargar Tasksel, una herramienta de Debian y Ubuntu que instala varios paquetes relacionados como una tarea coordinada en el sistema.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

Tras ejecutar una de las opciones anteriores, se le pedirá que instale estos paquetes y una serie de dependencias. Pulse 'y' seguido por 'Enter' para continuar, y siga cualquier otra instrucción que aparezca para establecer un contraseña administrativa para MySQL. Este proceso instalará las extensiones PHP mínimas necesarias para utilizar PHP con MySQL. 

![][1]

Ejecute el siguiente comando para ver otras extensiones PHP disponibles como paquetes:

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>Creación de documento info.php
Ahora podrá comprobar qué versión de Apache, MySQL y PHP tiene a través de la línea de comandos. Para ello, escriba `apache2 -v`, `mysql -v` o `php -v`.

Si desea realizar más pruebas, puede crear una página PHP de información rápida para verla en un explorador. Cree un archivo con el editor de texto Nano ejecutando este comando:

    user@ubuntu$ sudo nano /var/www/html/info.php

En el editor de texto GNU Nano, agregue las siguientes líneas:

    <?php
    phpinfo();
    ?>

Después, guarde y salga del editor de texto.

Reinicie Apache con este comando para que todas las nuevas instalaciones surtan efecto.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Comprobación de que LAMP se ha instalado correctamente
Ahora puede comprobar la página de información PHP que creó abriendo un explorador y yendo a http://youruniqueDNS/info.php. Debe tener un aspecto similar a esta imagen.

![][2]

Puede comprobar la instalación de Apache visitando la página predeterminada de Apache2 en Ubuntu (http://suDNSúnica/info.php). Debe ver algo parecido a esta imagen.

![][3]

Enhorabuena. Ya ha instalado una pila LAMP en la máquina virtual de Azure.

## <a name="next-steps"></a>Pasos siguientes
Consulte la documentación de Ubuntu relacionada con la pila LAMP:

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png