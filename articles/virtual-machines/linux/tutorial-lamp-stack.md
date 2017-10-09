---
title: "aaaDeploy LAMP en una máquina virtual de Linux en Azure | Documentos de Microsoft"
description: 'Tutorial: instalar pila de luz de hello en una VM de Linux en Azure'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a>Instalación de un servidor web LAMP en una máquina virtual de Azure
Este artículo le guiará a través de cómo toodeploy un Apache web server, MySQL y PHP (pila LAMP de Hola) en una VM Ubuntu en Azure. Si prefiere que el servidor web de hello NGINX, vea hello [pila LEMP](tutorial-lemp-stack.md) tutorial. servidor de luz de hello toosee en acción, opcionalmente, puede instalar y configurar un sitio de WordPress. En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una VM de Ubuntu (Hola 'L' en la pila de luz de hello)
> * Apertura del puerto 80 para el tráfico web
> * Instalación de Apache, MySQL y PHP
> * Comprobación de la instalación y configuración
> * Instalar WordPress en servidor de luz de Hola


Para obtener más información sobre la pila LAMP de hello, incluidas las recomendaciones para un entorno de producción, vea hello [Ubuntu documentación](https://help.ubuntu.com/community/ApacheMySQLPHP).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a>Instalación de Apache, MySQL y PHP

Ejecute hello siguientes comando tooupdate Ubuntu paquete orígenes e instale Apache, MySQL y PHP. Tenga en cuenta la intercalación de hello (^) al final de hello del comando de Hola.


```bash
sudo apt update && sudo apt install lamp-server^
```



Son paquetes de saludo tooinstall solicitada y otras dependencias. Cuando se le solicite, establecer una contraseña de root para MySQL y, a continuación, toocontinue [ENTRAR]. Siga Hola restantes mensajes. Este proceso instala Hola mínimo necesario PHP extensiones necesarias toouse PHP con MySQL. 

![Página de contraseña raíz de MySQL][1]

## <a name="verify-installation-and-configuration"></a>Comprobación de la instalación y configuración


### <a name="apache"></a>Apache

Comprobar la versión de Hola de Apache con hello siguiente comando:
```bash
apache2 -v
```

Con Apache instalada y el puerto 80 abra tooyour VM, servidor web de hello ahora puede tener acceso desde Hola internet. Hola tooview Apache2 Ubuntu Default Page, abra un explorador web y escriba la dirección IP pública de Hola de hello máquina virtual. Usar dirección IP pública hello usa tooSSH toohello VM:

![Página predeterminada de Apache][3]


### <a name="mysql"></a>MySQL

Comprobar la versión de Hola de MySQL con el siguiente comando de hello (tenga en cuenta mayúsculas hello `V` parámetro):

```bash
msql -V
```

Se recomienda ejecutar Hola después de la instalación de secuencia de comandos toohelp Hola segura de MySQL:

```bash
mysql_secure_installation
```

Escriba la contraseña de la raíz de MySQL y configurar opciones de seguridad de Hola para su entorno.

Si desea toocreate una base de datos MySQL, agregar usuarios o cambiar la configuración, tooMySQL de inicio de sesión:

```bash
mysql -u root -p
```

Cuando haya finalizado, salir del símbolo del sistema de hello mysql escribiendo `\q`.

### <a name="php"></a>PHP

Hola de comprobación de versión de PHP con hello siguiente comando:

```bash
php -v
```

Si desea más tootest, cree un rápido tooview de página de información PHP en un explorador. Hola siguiente comando crea la página de información de hello PHP:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

Ahora puede comprobar la página de información de hello PHP que ha creado. Abra un explorador y vaya demasiado`http://yourPublicIPAddress/info.php`. Sustituya la dirección IP pública de saludo de la máquina virtual. Debería ser una imagen toothis similar.

![Página de información de PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a>Pasos siguientes

En este tutorial, implementó un servidor LAMP en Azure. Ha aprendido a:

> [!div class="checklist"]
> * Creación de una máquina virtual de Ubuntu
> * Apertura del puerto 80 para el tráfico web
> * Instalación de Apache, MySQL y PHP
> * Comprobación de la instalación y configuración
> * Instalar WordPress en servidor de luz de Hola

Avanzar toohello siguiente tutorial toolearn cómo toosecure los servidores web con certificados SSL.

> [!div class="nextstepaction"]
> [Protección de un servidor web con SSL](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png