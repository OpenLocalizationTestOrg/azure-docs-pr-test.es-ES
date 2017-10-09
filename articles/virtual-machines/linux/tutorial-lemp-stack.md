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
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="294b2-103">Instalación de un servidor web LEMP en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="294b2-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="294b2-104">Este artículo le guiará a través de cómo toodeploy una NGINX web server, MySQL y PHP (pila de hello LEMP) en una VM Ubuntu en Azure.</span><span class="sxs-lookup"><span data-stu-id="294b2-104">This article walks you through how toodeploy an NGINX web server, MySQL, and PHP (hello LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="294b2-105">pila de Hello LEMP es una alternativa toohello popular [pila LAMP](tutorial-lamp-stack.md), que también se puede instalar en Azure.</span><span class="sxs-lookup"><span data-stu-id="294b2-105">hello LEMP stack is an alternative toohello popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="294b2-106">servidor de toosee hello LEMP en acción, opcionalmente, puede instalar y configurar un sitio de WordPress.</span><span class="sxs-lookup"><span data-stu-id="294b2-106">toosee hello LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="294b2-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="294b2-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="294b2-108">Crear una VM de Ubuntu (Hola 'L' en la pila de hello LEMP)</span><span class="sxs-lookup"><span data-stu-id="294b2-108">Create an Ubuntu VM (hello 'L' in hello LEMP stack)</span></span>
> * <span data-ttu-id="294b2-109">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="294b2-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="294b2-110">Instalación de NGINX, MySQL y PHP</span><span class="sxs-lookup"><span data-stu-id="294b2-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="294b2-111">Comprobación de la instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="294b2-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="294b2-112">Instalar WordPress en servidor de hello LEMP</span><span class="sxs-lookup"><span data-stu-id="294b2-112">Install WordPress on hello LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="294b2-113">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="294b2-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="294b2-114">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="294b2-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="294b2-115">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="294b2-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="294b2-116">Instalación de NGINX, MySQL y PHP</span><span class="sxs-lookup"><span data-stu-id="294b2-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="294b2-117">Ejecute hello siguientes comando tooupdate Ubuntu paquete orígenes e instale NGINX, MySQL y PHP.</span><span class="sxs-lookup"><span data-stu-id="294b2-117">Run hello following command tooupdate Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="294b2-118">Son paquetes de saludo tooinstall solicitada y otras dependencias.</span><span class="sxs-lookup"><span data-stu-id="294b2-118">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="294b2-119">Cuando se le solicite, establecer una contraseña de root para MySQL y, a continuación, toocontinue [ENTRAR].</span><span class="sxs-lookup"><span data-stu-id="294b2-119">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="294b2-120">Siga Hola restantes mensajes.</span><span class="sxs-lookup"><span data-stu-id="294b2-120">Follow hello remaining prompts.</span></span> <span data-ttu-id="294b2-121">Este proceso instala Hola mínimo necesario PHP extensiones necesarias toouse PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="294b2-121">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Página de contraseña raíz de MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="294b2-123">Comprobación de la instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="294b2-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="294b2-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="294b2-124">NGINX</span></span>

<span data-ttu-id="294b2-125">Comprobar la versión de Hola de NGINX con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="294b2-125">Check hello version of NGINX with hello following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="294b2-126">Con NGINX instalada y el puerto 80 abra tooyour VM, servidor web de hello ahora puede tener acceso desde Hola internet.</span><span class="sxs-lookup"><span data-stu-id="294b2-126">With NGINX installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="294b2-127">página de bienvenida de tooview hello NGINX, abra un explorador web y escriba la dirección IP pública de Hola de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="294b2-127">tooview hello NGINX welcome page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="294b2-128">Usar dirección IP pública hello usa tooSSH toohello VM:</span><span class="sxs-lookup"><span data-stu-id="294b2-128">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Página predeterminada de NGINX][3]


### <a name="mysql"></a><span data-ttu-id="294b2-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="294b2-130">MySQL</span></span>

<span data-ttu-id="294b2-131">Comprobar la versión de Hola de MySQL con el siguiente comando de hello (tenga en cuenta mayúsculas hello `V` parámetro):</span><span class="sxs-lookup"><span data-stu-id="294b2-131">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="294b2-132">Se recomienda ejecutar Hola después de la instalación de secuencia de comandos toohelp Hola segura de MySQL:</span><span class="sxs-lookup"><span data-stu-id="294b2-132">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="294b2-133">Escriba la contraseña de la raíz de MySQL y configurar opciones de seguridad de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="294b2-133">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="294b2-134">Si desea toocreate una base de datos MySQL, agregar usuarios o cambiar la configuración, tooMySQL de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="294b2-134">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="294b2-135">Cuando haya finalizado, salir del símbolo del sistema de hello mysql escribiendo `\q`.</span><span class="sxs-lookup"><span data-stu-id="294b2-135">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="294b2-136">PHP</span><span class="sxs-lookup"><span data-stu-id="294b2-136">PHP</span></span>

<span data-ttu-id="294b2-137">Hola de comprobación de versión de PHP con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="294b2-137">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="294b2-138">Configurar Hola de toouse NGINX Administrador de procesos de FastCGI de PHP (PHP-FPM).</span><span class="sxs-lookup"><span data-stu-id="294b2-138">Configure NGINX toouse hello PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="294b2-139">Ejecute hello después comandos tooback servidor NGINX original de hello bloquear el archivo de configuración y, a continuación, editar el archivo original de hello en un editor de su elección:</span><span class="sxs-lookup"><span data-stu-id="294b2-139">Run hello following commands tooback up hello original NGINX server block config file and then edit hello original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="294b2-140">En el editor de hello, reemplace el contenido de Hola de `/etc/nginx/sites-available/default` con siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="294b2-140">In hello editor, replace hello contents of `/etc/nginx/sites-available/default` with hello following.</span></span> <span data-ttu-id="294b2-141">Vea los comentarios de Hola para ver una explicación de la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="294b2-141">See hello comments for explanation of hello settings.</span></span> <span data-ttu-id="294b2-142">Sustituya la dirección IP pública de saludo de la máquina virtual para *yourPublicIPAddress*y dejar Hola restantes de la configuración.</span><span class="sxs-lookup"><span data-stu-id="294b2-142">Substitute hello public IP address of your VM for *yourPublicIPAddress*, and leave hello remaining settings.</span></span> <span data-ttu-id="294b2-143">A continuación, guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="294b2-143">Then save hello file.</span></span>

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

<span data-ttu-id="294b2-144">Compruebe la configuración de hello NGINX errores de sintaxis:</span><span class="sxs-lookup"><span data-stu-id="294b2-144">Check hello NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="294b2-145">Si la sintaxis de hello es correcta, reinicie NGINX con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="294b2-145">If hello syntax is correct, restart NGINX with hello following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="294b2-146">Si desea más tootest, cree un rápido tooview de página de información PHP en un explorador.</span><span class="sxs-lookup"><span data-stu-id="294b2-146">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="294b2-147">Hola siguiente comando crea la página de información de hello PHP:</span><span class="sxs-lookup"><span data-stu-id="294b2-147">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="294b2-148">Ahora puede comprobar la página de información de hello PHP que ha creado.</span><span class="sxs-lookup"><span data-stu-id="294b2-148">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="294b2-149">Abra un explorador y vaya demasiado`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="294b2-149">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="294b2-150">Sustituya la dirección IP pública de saludo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="294b2-150">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="294b2-151">Debería ser una imagen toothis similar.</span><span class="sxs-lookup"><span data-stu-id="294b2-151">It should look similar toothis image.</span></span>

![Página de información de PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="294b2-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="294b2-153">Next steps</span></span>

<span data-ttu-id="294b2-154">En este tutorial, implementó un servidor LEMP en Azure.</span><span class="sxs-lookup"><span data-stu-id="294b2-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="294b2-155">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="294b2-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="294b2-156">Creación de una máquina virtual de Ubuntu</span><span class="sxs-lookup"><span data-stu-id="294b2-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="294b2-157">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="294b2-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="294b2-158">Instalación de NGINX, MySQL y PHP</span><span class="sxs-lookup"><span data-stu-id="294b2-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="294b2-159">Comprobación de la instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="294b2-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="294b2-160">Instalar WordPress en pila de hello LEMP</span><span class="sxs-lookup"><span data-stu-id="294b2-160">Install WordPress on hello LEMP stack</span></span>

<span data-ttu-id="294b2-161">Avanzar toohello siguiente tutorial toolearn cómo toosecure los servidores web con certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="294b2-161">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="294b2-162">Protección de un servidor web con SSL</span><span class="sxs-lookup"><span data-stu-id="294b2-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
