---
title: "Implementación de LEMP en una máquina virtual Linux en Azure | Microsoft Docs"
description: "Tutorial: Instalación de la pila LEMP en una máquina virtual Linux en Azure"
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
ms.openlocfilehash: 653af144eb12cacf955f96a5442efd73add38e88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="01f8a-103">Instalación de un servidor web LEMP en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="01f8a-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="01f8a-104">En este artículo se ofrecen instrucciones paso a paso para implementar un servidor web NGINX, MySQL y PHP (la pila LEMP) en una máquina virtual de Ubuntu en Azure.</span><span class="sxs-lookup"><span data-stu-id="01f8a-104">This article walks you through how to deploy an NGINX web server, MySQL, and PHP (the LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="01f8a-105">La pila LEMP es una alternativa a la popular [pila LAMP](tutorial-lamp-stack.md), que también se puede instalar en Azure.</span><span class="sxs-lookup"><span data-stu-id="01f8a-105">The LEMP stack is an alternative to the popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="01f8a-106">Para ver el servidor LEMP en acción, si lo desea, puede instalar y configurar un sitio de WordPress.</span><span class="sxs-lookup"><span data-stu-id="01f8a-106">To see the LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="01f8a-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="01f8a-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="01f8a-108">Creación de una máquina virtual de Ubuntu (la "L" de la pila LEMP)</span><span class="sxs-lookup"><span data-stu-id="01f8a-108">Create an Ubuntu VM (the 'L' in the LEMP stack)</span></span>
> * <span data-ttu-id="01f8a-109">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="01f8a-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="01f8a-110">Instalación de NGINX, MySQL y PHP</span><span class="sxs-lookup"><span data-stu-id="01f8a-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="01f8a-111">Comprobación de la instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="01f8a-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="01f8a-112">Instalación de WordPress en el servidor LEMP</span><span class="sxs-lookup"><span data-stu-id="01f8a-112">Install WordPress on the LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="01f8a-113">Si decide instalar y usar la CLI localmente, para este tutorial es preciso que ejecute la CLI de Azure versión 2.0.4 o posterior.</span><span class="sxs-lookup"><span data-stu-id="01f8a-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="01f8a-114">Ejecute `az --version` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="01f8a-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="01f8a-115">Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="01f8a-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="01f8a-116">Instalación de NGINX, MySQL y PHP</span><span class="sxs-lookup"><span data-stu-id="01f8a-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="01f8a-117">Ejecute el siguiente comando para actualizar los orígenes de paquetes de Ubuntu e instalar NGINX, MySQL y PHP.</span><span class="sxs-lookup"><span data-stu-id="01f8a-117">Run the following command to update Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="01f8a-118">Se le pide que instale los paquetes y otras dependencias.</span><span class="sxs-lookup"><span data-stu-id="01f8a-118">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="01f8a-119">Cuando se le solicite, establezca una contraseña raíz para MySQL y, a continuación, presione [Entrar] para continuar.</span><span class="sxs-lookup"><span data-stu-id="01f8a-119">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="01f8a-120">Siga el resto de instrucciones.</span><span class="sxs-lookup"><span data-stu-id="01f8a-120">Follow the remaining prompts.</span></span> <span data-ttu-id="01f8a-121">Este proceso instala las extensiones PHP mínimas necesarias para utilizar PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="01f8a-121">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![Página de contraseña raíz de MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="01f8a-123">Comprobación de la instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="01f8a-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="01f8a-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="01f8a-124">NGINX</span></span>

<span data-ttu-id="01f8a-125">Compruebe la versión de NGINX con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="01f8a-125">Check the version of NGINX with the following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="01f8a-126">Con NGINX instalado y el puerto 80 abierto para la máquina virtual, se puede acceder ahora al servidor web desde Internet.</span><span class="sxs-lookup"><span data-stu-id="01f8a-126">With NGINX installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="01f8a-127">Para ver la página de bienvenida de NGINX, abra un explorador web y escriba la dirección IP pública de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01f8a-127">To view the NGINX welcome page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="01f8a-128">Use la dirección IP pública utilizada para SSH en la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="01f8a-128">Use the public IP address you used to SSH to the VM:</span></span>

![Página predeterminada de NGINX][3]


### <a name="mysql"></a><span data-ttu-id="01f8a-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="01f8a-130">MySQL</span></span>

<span data-ttu-id="01f8a-131">Compruebe la versión de MySQL con el siguiente comando (tenga en cuenta el parámetro `V` en mayúsculas):</span><span class="sxs-lookup"><span data-stu-id="01f8a-131">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="01f8a-132">Se recomienda ejecutar el script siguiente para ayudar a proteger la instalación de MySQL:</span><span class="sxs-lookup"><span data-stu-id="01f8a-132">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="01f8a-133">Escriba la contraseña raíz de MySQL y configure la seguridad para su entorno.</span><span class="sxs-lookup"><span data-stu-id="01f8a-133">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="01f8a-134">Si desea crear una base de datos MySQL, agregar usuarios o cambiar la configuración, inicie sesión en MySQL:</span><span class="sxs-lookup"><span data-stu-id="01f8a-134">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="01f8a-135">Cuando haya terminado, escriba `\q` para salir del símbolo del sistema de mysql.</span><span class="sxs-lookup"><span data-stu-id="01f8a-135">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="01f8a-136">PHP</span><span class="sxs-lookup"><span data-stu-id="01f8a-136">PHP</span></span>

<span data-ttu-id="01f8a-137">Compruebe la versión de PHP con el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="01f8a-137">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="01f8a-138">Configure NGINX para usar el Administrador de procesos FastCGI para PHP (PHP-FPM).</span><span class="sxs-lookup"><span data-stu-id="01f8a-138">Configure NGINX to use the PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="01f8a-139">Ejecute los siguientes comandos para realizar la copia de seguridad del archivo de configuración del bloque de servidor NGINX original y, a continuación, edite el archivo original en el editor que prefiera:</span><span class="sxs-lookup"><span data-stu-id="01f8a-139">Run the following commands to back up the original NGINX server block config file and then edit the original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="01f8a-140">En el editor, reemplace el contenido de `/etc/nginx/sites-available/default` por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="01f8a-140">In the editor, replace the contents of `/etc/nginx/sites-available/default` with the following.</span></span> <span data-ttu-id="01f8a-141">Vea los comentarios para obtener una explicación de la configuración.</span><span class="sxs-lookup"><span data-stu-id="01f8a-141">See the comments for explanation of the settings.</span></span> <span data-ttu-id="01f8a-142">Sustituya la dirección IP pública de la máquina virtual para *yourPublicIPAddress* y deje el resto de opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="01f8a-142">Substitute the public IP address of your VM for *yourPublicIPAddress*, and leave the remaining settings.</span></span> <span data-ttu-id="01f8a-143">A continuación, guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="01f8a-143">Then save the file.</span></span>

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

<span data-ttu-id="01f8a-144">Compruebe la configuración de NGINX para ver si hay errores de sintaxis:</span><span class="sxs-lookup"><span data-stu-id="01f8a-144">Check the NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="01f8a-145">Si la sintaxis es correcta, reinicie NGINX con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="01f8a-145">If the syntax is correct, restart NGINX with the following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="01f8a-146">Si desea realizar más pruebas, cree una página PHP de información rápida para verla en un explorador.</span><span class="sxs-lookup"><span data-stu-id="01f8a-146">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="01f8a-147">El siguiente comando crea la página de información de PHP:</span><span class="sxs-lookup"><span data-stu-id="01f8a-147">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="01f8a-148">Ahora puede comprobar la página de información de PHP que creó.</span><span class="sxs-lookup"><span data-stu-id="01f8a-148">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="01f8a-149">Abra un explorador y vaya a `http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="01f8a-149">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="01f8a-150">Sustituya la dirección por la dirección IP pública de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01f8a-150">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="01f8a-151">Debe tener un aspecto similar a esta imagen.</span><span class="sxs-lookup"><span data-stu-id="01f8a-151">It should look similar to this image.</span></span>

![Página de información de PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="01f8a-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01f8a-153">Next steps</span></span>

<span data-ttu-id="01f8a-154">En este tutorial, implementó un servidor LEMP en Azure.</span><span class="sxs-lookup"><span data-stu-id="01f8a-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="01f8a-155">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="01f8a-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="01f8a-156">Creación de una máquina virtual de Ubuntu</span><span class="sxs-lookup"><span data-stu-id="01f8a-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="01f8a-157">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="01f8a-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="01f8a-158">Instalación de NGINX, MySQL y PHP</span><span class="sxs-lookup"><span data-stu-id="01f8a-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="01f8a-159">Comprobación de la instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="01f8a-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="01f8a-160">Instalación de WordPress en la pila LEMP</span><span class="sxs-lookup"><span data-stu-id="01f8a-160">Install WordPress on the LEMP stack</span></span>

<span data-ttu-id="01f8a-161">Pase al siguiente tutorial para aprender a proteger servidores web con certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="01f8a-161">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01f8a-162">Protección de un servidor web con SSL</span><span class="sxs-lookup"><span data-stu-id="01f8a-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
