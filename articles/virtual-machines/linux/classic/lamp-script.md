---
title: "aaaUse Hola CustomScript extensión en una VM Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo las toouse hello CustomScript extensión toodeploy aplicaciones en máquinas de virtuales de Linux en Azure creadas utilizando el modelo de implementación clásica de Hola."
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a>Implementar una aplicación de luz usando Hola CustomScript extensión de Azure para Linux
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Para obtener información acerca de cómo implementar una pila LAMP utilizando el modelo de administrador de recursos de hello, consulte [aquí](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hola CustomScript extensión de Microsoft Azure para Linux proporciona una manera toocustomize sus máquinas virtuales (VM) mediante la ejecución de código arbitrario escrito en cualquier lenguaje de scripting admitido Hola VM (por ejemplo, Python e intensiva de errores). Esto proporciona una forma muy flexible tooautomate máquinas de toomultiple de implementación de aplicación.

Puede implementar la CustomScript extensión Hola utilizando Hola portal de Azure, Windows PowerShell o hello Azure interfaz de línea de comandos (CLI de Azure).

En este artículo que vamos a usar hello Azure CLI toodeploy una tooan de aplicación LAMP Ubuntu VM simple creado utilizando el modelo de implementación clásica de Hola.

## <a name="prerequisites"></a>Requisitos previos
Para este ejemplo, cree primero dos máquinas virtuales de Azure con Ubuntu 14.04 o una versión posterior. Hello las máquinas virtuales se denominan *script vm* y *luz virtual*. Utilice nombres únicos al crear máquinas virtuales de Hola. Uno toorun usa comandos de CLI de Hola y aplicación de luz de hello toodeploy usado.

También necesitará una cuenta de almacenamiento de Azure y una clave tooaccess TI (que puede obtener de hello portal de Azure).

Si necesita ayuda para crear máquinas virtuales de Linux en Azure, consulte demasiado[crear una máquina Virtual ejecuta Linux](createportal.md).

comandos de instalación de Hello asume Ubuntu, pero puede adaptar la instalación de Hola para cualquier admite la distribución de Linux.

Hello máquina virtual de vm de la secuencia de comandos debe toohave instalado CLI de Azure, con un tooAzure de conexión del trabajo. Para obtener ayuda con esto, consulte demasiado[instalar y configurar la interfaz de línea de comandos de Azure hello](../../../cli-install-nodejs.md).

## <a name="upload-a-script"></a>Cargar un script
Comenzaremos usar Hola CustomScript extensión toorun una secuencia de comandos en una pila de luz de máquina virtual tooinstall Hola remota y crear una página PHP. En el script de Hola de orden tooaccess desde cualquier lugar nosotros cargaremos como un blob de Azure.

### <a name="script-overview"></a>Información general del script
ejemplo de script de Hola instala un tooUbuntu de pila LAMP (incluyendo la configuración de una instalación silenciosa de MySQL), escribe un simple archivo PHP e inicia Apache.

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a>Cargar script
Guardar script de Hola como un archivo de texto, por ejemplo *install_lamp.sh*y, a continuación, cargarlo tooAzure almacenamiento. Puede hacerlo fácilmente con la CLI de Azure. Hello en el ejemplo siguiente se carga Hola archivo tooa almacenamiento contenedor denominado "scripts". Si no existe el contenedor de hello, necesitará toocreate primero.

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

Crear un archivo JSON que describe cómo toodownload Hola script desde el almacenamiento de Azure. Guardar como *public_config.json* (reemplazando "mystorage" con el nombre de saludo de la cuenta de almacenamiento):

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a>Implementar la extensión de Hola
Ahora puede usar Hola siguiente comando toodeploy Hola CustomScript extensión de Linux toohello remoto VM con Hola CLI de Azure.

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

comando anterior Hola descarga y ejecuta hello *install_lamp.sh* secuencia de comandos de hello VM llama *lamp-vm*.

Puesto que la aplicación hello incluye un servidor web, recuerde tooopen HTTP el puerto de escucha en hello VM remoto con el comando siguiente Hola.

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>Supervisión y solución de problemas
Puede comprobar en grado ejecuciones de secuencia de comandos personalizada hello examinando el archivo de registro de hello Hola VM remoto. SSH demasiado*lamp-vm* y archivo de registro de hello final con el comando siguiente Hola.

    cd /var/log/azure/customscript
    tail -f handler.log

Después de ejecutar la CustomScript extensión hello, puede examinar la página PHP toohello que ha creado para obtener información. Hola PHP página de ejemplo de Hola en este artículo es *http://lamp-vm.cloudapp.net/phpinfo.php*.

## <a name="additional-resources"></a>Recursos adicionales
Puede usar Hola mismo toodeploy pasos básicos aplicaciones más complejas. En este ejemplo se guardó el script de instalación de Hola como un blob público en el almacenamiento de Azure. Una opción más segura sería el script de instalación de hello toostore como un blob seguro con un [firma de acceso seguro](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).

Recursos adicionales de CLI de Azure, Linux y Hola CustomScript extensión se enumeran a continuación.

[Automatización de las tareas de personalización de VM de Linux con la extensión CustomScript](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Extensiones de Linux de Azure (GitHub)](https://github.com/Azure/azure-linux-extensions)