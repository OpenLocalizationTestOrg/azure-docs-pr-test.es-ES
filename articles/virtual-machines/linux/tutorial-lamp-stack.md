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
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="cedcb-103">Instalación de un servidor web LAMP en una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="cedcb-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="cedcb-104">Este artículo le guiará a través de cómo toodeploy un Apache web server, MySQL y PHP (pila LAMP de Hola) en una VM Ubuntu en Azure.</span><span class="sxs-lookup"><span data-stu-id="cedcb-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="cedcb-105">Si prefiere que el servidor web de hello NGINX, vea hello [pila LEMP](tutorial-lemp-stack.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="cedcb-105">If you prefer hello NGINX web server, see hello [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="cedcb-106">servidor de luz de hello toosee en acción, opcionalmente, puede instalar y configurar un sitio de WordPress.</span><span class="sxs-lookup"><span data-stu-id="cedcb-106">toosee hello LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="cedcb-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="cedcb-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cedcb-108">Crear una VM de Ubuntu (Hola 'L' en la pila de luz de hello)</span><span class="sxs-lookup"><span data-stu-id="cedcb-108">Create an Ubuntu VM (hello 'L' in hello LAMP stack)</span></span>
> * <span data-ttu-id="cedcb-109">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="cedcb-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="cedcb-110">Instalación de Apache, MySQL y PHP</span><span class="sxs-lookup"><span data-stu-id="cedcb-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="cedcb-111">Comprobación de la instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="cedcb-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="cedcb-112">Instalar WordPress en servidor de luz de Hola</span><span class="sxs-lookup"><span data-stu-id="cedcb-112">Install WordPress on hello LAMP server</span></span>


<span data-ttu-id="cedcb-113">Para obtener más información sobre la pila LAMP de hello, incluidas las recomendaciones para un entorno de producción, vea hello [Ubuntu documentación](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="cedcb-113">For more on hello LAMP stack, including recommendations for a production environment, see hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cedcb-114">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="cedcb-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cedcb-115">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="cedcb-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cedcb-116">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cedcb-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="cedcb-117">Instalación de Apache, MySQL y PHP</span><span class="sxs-lookup"><span data-stu-id="cedcb-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="cedcb-118">Ejecute hello siguientes comando tooupdate Ubuntu paquete orígenes e instale Apache, MySQL y PHP.</span><span class="sxs-lookup"><span data-stu-id="cedcb-118">Run hello following command tooupdate Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="cedcb-119">Tenga en cuenta la intercalación de hello (^) al final de hello del comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="cedcb-119">Note hello caret (^) at hello end of hello command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="cedcb-120">Son paquetes de saludo tooinstall solicitada y otras dependencias.</span><span class="sxs-lookup"><span data-stu-id="cedcb-120">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="cedcb-121">Cuando se le solicite, establecer una contraseña de root para MySQL y, a continuación, toocontinue [ENTRAR].</span><span class="sxs-lookup"><span data-stu-id="cedcb-121">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="cedcb-122">Siga Hola restantes mensajes.</span><span class="sxs-lookup"><span data-stu-id="cedcb-122">Follow hello remaining prompts.</span></span> <span data-ttu-id="cedcb-123">Este proceso instala Hola mínimo necesario PHP extensiones necesarias toouse PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="cedcb-123">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Página de contraseña raíz de MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="cedcb-125">Comprobación de la instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="cedcb-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="cedcb-126">Apache</span><span class="sxs-lookup"><span data-stu-id="cedcb-126">Apache</span></span>

<span data-ttu-id="cedcb-127">Comprobar la versión de Hola de Apache con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cedcb-127">Check hello version of Apache with hello following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="cedcb-128">Con Apache instalada y el puerto 80 abra tooyour VM, servidor web de hello ahora puede tener acceso desde Hola internet.</span><span class="sxs-lookup"><span data-stu-id="cedcb-128">With Apache installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="cedcb-129">Hola tooview Apache2 Ubuntu Default Page, abra un explorador web y escriba la dirección IP pública de Hola de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cedcb-129">tooview hello Apache2 Ubuntu Default Page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="cedcb-130">Usar dirección IP pública hello usa tooSSH toohello VM:</span><span class="sxs-lookup"><span data-stu-id="cedcb-130">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Página predeterminada de Apache][3]


### <a name="mysql"></a><span data-ttu-id="cedcb-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="cedcb-132">MySQL</span></span>

<span data-ttu-id="cedcb-133">Comprobar la versión de Hola de MySQL con el siguiente comando de hello (tenga en cuenta mayúsculas hello `V` parámetro):</span><span class="sxs-lookup"><span data-stu-id="cedcb-133">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="cedcb-134">Se recomienda ejecutar Hola después de la instalación de secuencia de comandos toohelp Hola segura de MySQL:</span><span class="sxs-lookup"><span data-stu-id="cedcb-134">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="cedcb-135">Escriba la contraseña de la raíz de MySQL y configurar opciones de seguridad de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="cedcb-135">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="cedcb-136">Si desea toocreate una base de datos MySQL, agregar usuarios o cambiar la configuración, tooMySQL de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="cedcb-136">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="cedcb-137">Cuando haya finalizado, salir del símbolo del sistema de hello mysql escribiendo `\q`.</span><span class="sxs-lookup"><span data-stu-id="cedcb-137">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="cedcb-138">PHP</span><span class="sxs-lookup"><span data-stu-id="cedcb-138">PHP</span></span>

<span data-ttu-id="cedcb-139">Hola de comprobación de versión de PHP con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cedcb-139">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="cedcb-140">Si desea más tootest, cree un rápido tooview de página de información PHP en un explorador.</span><span class="sxs-lookup"><span data-stu-id="cedcb-140">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="cedcb-141">Hola siguiente comando crea la página de información de hello PHP:</span><span class="sxs-lookup"><span data-stu-id="cedcb-141">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="cedcb-142">Ahora puede comprobar la página de información de hello PHP que ha creado.</span><span class="sxs-lookup"><span data-stu-id="cedcb-142">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="cedcb-143">Abra un explorador y vaya demasiado`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="cedcb-143">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="cedcb-144">Sustituya la dirección IP pública de saludo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cedcb-144">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="cedcb-145">Debería ser una imagen toothis similar.</span><span class="sxs-lookup"><span data-stu-id="cedcb-145">It should look similar toothis image.</span></span>

![Página de información de PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="cedcb-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cedcb-147">Next steps</span></span>

<span data-ttu-id="cedcb-148">En este tutorial, implementó un servidor LAMP en Azure.</span><span class="sxs-lookup"><span data-stu-id="cedcb-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="cedcb-149">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="cedcb-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cedcb-150">Creación de una máquina virtual de Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cedcb-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="cedcb-151">Apertura del puerto 80 para el tráfico web</span><span class="sxs-lookup"><span data-stu-id="cedcb-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="cedcb-152">Instalación de Apache, MySQL y PHP</span><span class="sxs-lookup"><span data-stu-id="cedcb-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="cedcb-153">Comprobación de la instalación y configuración</span><span class="sxs-lookup"><span data-stu-id="cedcb-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="cedcb-154">Instalar WordPress en servidor de luz de Hola</span><span class="sxs-lookup"><span data-stu-id="cedcb-154">Install WordPress on hello LAMP server</span></span>

<span data-ttu-id="cedcb-155">Avanzar toohello siguiente tutorial toolearn cómo toosecure los servidores web con certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="cedcb-155">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cedcb-156">Protección de un servidor web con SSL</span><span class="sxs-lookup"><span data-stu-id="cedcb-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png