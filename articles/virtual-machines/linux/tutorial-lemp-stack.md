---
title: "aaaDeploy LEMP en una máquina virtual de Linux en Azure | Documentos de Microsoft"
description: "Tutorial: pila LEMP Hola de instalación en una VM de Linux en Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Instalación de un servidor web LEMP en una máquina virtual de Azure
Este artículo le guiará a través de cómo toodeploy una NGINX web server, MySQL y PHP (pila de hello LEMP) en una VM Ubuntu en Azure. pila de Hello LEMP es una alternativa toohello popular [pila LAMP](tutorial-lamp-stack.md), que también se puede instalar en Azure. servidor de toosee hello LEMP en acción, opcionalmente, puede instalar y configurar un sitio de WordPress. En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una VM de Ubuntu (Hola 'L' en la pila de hello LEMP)
> * Apertura del puerto 80 para el tráfico web
> * Instalación de NGINX, MySQL y PHP
> * Comprobación de la instalación y configuración
> * Instalar WordPress en servidor de hello LEMP


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>Instalación de NGINX, MySQL y PHP

Ejecute hello siguientes comando tooupdate Ubuntu paquete orígenes e instale NGINX, MySQL y PHP. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

Son paquetes de saludo tooinstall solicitada y otras dependencias. Cuando se le solicite, establecer una contraseña de root para MySQL y, a continuación, toocontinue [ENTRAR]. Siga Hola restantes mensajes. Este proceso instala Hola mínimo necesario PHP extensiones necesarias toouse PHP con MySQL. 

![Página de contraseña raíz de MySQL][1]

## <a name="verify-installation-and-configuration"></a>Comprobación de la instalación y configuración


### <a name="nginx"></a>NGINX

Comprobar la versión de Hola de NGINX con hello siguiente comando:
```bash
nginx -v
```

Con NGINX instalada y el puerto 80 abra tooyour VM, servidor web de hello ahora puede tener acceso desde Hola internet. página de bienvenida de tooview hello NGINX, abra un explorador web y escriba la dirección IP pública de Hola de hello máquina virtual. Usar dirección IP pública hello usa tooSSH toohello VM:

![Página predeterminada de NGINX][3]


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

Configurar Hola de toouse NGINX Administrador de procesos de FastCGI de PHP (PHP-FPM). Ejecute hello después comandos tooback servidor NGINX original de hello bloquear el archivo de configuración y, a continuación, editar el archivo original de hello en un editor de su elección:

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

En el editor de hello, reemplace el contenido de Hola de `/etc/nginx/sites-available/default` con siguiente Hola. Vea los comentarios de Hola para ver una explicación de la configuración de Hola. Sustituya la dirección IP pública de saludo de la máquina virtual para *yourPublicIPAddress*y dejar Hola restantes de la configuración. A continuación, guarde el archivo hello.

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

Compruebe la configuración de hello NGINX errores de sintaxis:

```bash
sudo nginx -t
```

Si la sintaxis de hello es correcta, reinicie NGINX con hello siguiente comando:

```bash
sudo service nginx restart
```

Si desea más tootest, cree un rápido tooview de página de información PHP en un explorador. Hola siguiente comando crea la página de información de hello PHP:

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



Ahora puede comprobar la página de información de hello PHP que ha creado. Abra un explorador y vaya demasiado`http://yourPublicIPAddress/info.php`. Sustituya la dirección IP pública de saludo de la máquina virtual. Debería ser una imagen toothis similar.

![Página de información de PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, implementó un servidor LEMP en Azure. Ha aprendido a:

> [!div class="checklist"]
> * Creación de una máquina virtual de Ubuntu
> * Apertura del puerto 80 para el tráfico web
> * Instalación de NGINX, MySQL y PHP
> * Comprobación de la instalación y configuración
> * Instalar WordPress en pila de hello LEMP

Avanzar toohello siguiente tutorial toolearn cómo toosecure los servidores web con certificados SSL.

> [!div class="nextstepaction"]
> [Protección de un servidor web con SSL](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
