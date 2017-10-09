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
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a><span data-ttu-id="ed99c-103">Implementar una aplicación de luz usando Hola CustomScript extensión de Azure para Linux</span><span class="sxs-lookup"><span data-stu-id="ed99c-103">Deploy a LAMP app using hello Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="ed99c-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ed99c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ed99c-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="ed99c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ed99c-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed99c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ed99c-107">Para obtener información acerca de cómo implementar una pila LAMP utilizando el modelo de administrador de recursos de hello, consulte [aquí](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed99c-107">For information about deploying a LAMP stack using hello Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ed99c-108">Hola CustomScript extensión de Microsoft Azure para Linux proporciona una manera toocustomize sus máquinas virtuales (VM) mediante la ejecución de código arbitrario escrito en cualquier lenguaje de scripting admitido Hola VM (por ejemplo, Python e intensiva de errores).</span><span class="sxs-lookup"><span data-stu-id="ed99c-108">hello Microsoft Azure CustomScript Extension for Linux provides a way toocustomize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by hello VM (for example, Python, and Bash).</span></span> <span data-ttu-id="ed99c-109">Esto proporciona una forma muy flexible tooautomate máquinas de toomultiple de implementación de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ed99c-109">This provides a very flexible way tooautomate application deployment toomultiple machines.</span></span>

<span data-ttu-id="ed99c-110">Puede implementar la CustomScript extensión Hola utilizando Hola portal de Azure, Windows PowerShell o hello Azure interfaz de línea de comandos (CLI de Azure).</span><span class="sxs-lookup"><span data-stu-id="ed99c-110">You can deploy hello CustomScript Extension using hello Azure portal, Windows PowerShell, or hello Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="ed99c-111">En este artículo que vamos a usar hello Azure CLI toodeploy una tooan de aplicación LAMP Ubuntu VM simple creado utilizando el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed99c-111">In this article we'll use hello Azure CLI toodeploy a simple LAMP application tooan Ubuntu VM created using hello classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed99c-112">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ed99c-112">Prerequisites</span></span>
<span data-ttu-id="ed99c-113">Para este ejemplo, cree primero dos máquinas virtuales de Azure con Ubuntu 14.04 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="ed99c-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="ed99c-114">Hello las máquinas virtuales se denominan *script vm* y *luz virtual*.</span><span class="sxs-lookup"><span data-stu-id="ed99c-114">hello VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="ed99c-115">Utilice nombres únicos al crear máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="ed99c-115">Use unique names when you create hello VMs.</span></span> <span data-ttu-id="ed99c-116">Uno toorun usa comandos de CLI de Hola y aplicación de luz de hello toodeploy usado.</span><span class="sxs-lookup"><span data-stu-id="ed99c-116">One is used toorun hello CLI commands and one is used toodeploy hello LAMP app.</span></span>

<span data-ttu-id="ed99c-117">También necesitará una cuenta de almacenamiento de Azure y una clave tooaccess TI (que puede obtener de hello portal de Azure).</span><span class="sxs-lookup"><span data-stu-id="ed99c-117">You also need an Azure Storage account and a key tooaccess it (you can get this from hello Azure portal).</span></span>

<span data-ttu-id="ed99c-118">Si necesita ayuda para crear máquinas virtuales de Linux en Azure, consulte demasiado[crear una máquina Virtual ejecuta Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="ed99c-118">If you need help creating Linux VMs on Azure refer too[Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="ed99c-119">comandos de instalación de Hello asume Ubuntu, pero puede adaptar la instalación de Hola para cualquier admite la distribución de Linux.</span><span class="sxs-lookup"><span data-stu-id="ed99c-119">hello install commands assume Ubuntu, but you can adapt hello installation for any supported Linux distro.</span></span>

<span data-ttu-id="ed99c-120">Hello máquina virtual de vm de la secuencia de comandos debe toohave instalado CLI de Azure, con un tooAzure de conexión del trabajo.</span><span class="sxs-lookup"><span data-stu-id="ed99c-120">hello script-vm VM needs toohave Azure CLI installed, with a working connection tooAzure.</span></span> <span data-ttu-id="ed99c-121">Para obtener ayuda con esto, consulte demasiado[instalar y configurar la interfaz de línea de comandos de Azure hello](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ed99c-121">For help with this refer too[Install and Configure hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="ed99c-122">Cargar un script</span><span class="sxs-lookup"><span data-stu-id="ed99c-122">Upload a script</span></span>
<span data-ttu-id="ed99c-123">Comenzaremos usar Hola CustomScript extensión toorun una secuencia de comandos en una pila de luz de máquina virtual tooinstall Hola remota y crear una página PHP.</span><span class="sxs-lookup"><span data-stu-id="ed99c-123">We'll use hello CustomScript Extension toorun a script on a remote VM tooinstall hello LAMP stack and create a PHP page.</span></span> <span data-ttu-id="ed99c-124">En el script de Hola de orden tooaccess desde cualquier lugar nosotros cargaremos como un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed99c-124">In order tooaccess hello script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="ed99c-125">Información general del script</span><span class="sxs-lookup"><span data-stu-id="ed99c-125">Script overview</span></span>
<span data-ttu-id="ed99c-126">ejemplo de script de Hola instala un tooUbuntu de pila LAMP (incluyendo la configuración de una instalación silenciosa de MySQL), escribe un simple archivo PHP e inicia Apache.</span><span class="sxs-lookup"><span data-stu-id="ed99c-126">hello script example installs a LAMP stack tooUbuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

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

### <a name="upload-script"></a><span data-ttu-id="ed99c-127">Cargar script</span><span class="sxs-lookup"><span data-stu-id="ed99c-127">Upload script</span></span>
<span data-ttu-id="ed99c-128">Guardar script de Hola como un archivo de texto, por ejemplo *install_lamp.sh*y, a continuación, cargarlo tooAzure almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ed99c-128">Save hello script as a text file, for example *install_lamp.sh*, and then upload it tooAzure Storage.</span></span> <span data-ttu-id="ed99c-129">Puede hacerlo fácilmente con la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed99c-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="ed99c-130">Hello en el ejemplo siguiente se carga Hola archivo tooa almacenamiento contenedor denominado "scripts".</span><span class="sxs-lookup"><span data-stu-id="ed99c-130">hello following example uploads hello file tooa storage container named "scripts".</span></span> <span data-ttu-id="ed99c-131">Si no existe el contenedor de hello, necesitará toocreate primero.</span><span class="sxs-lookup"><span data-stu-id="ed99c-131">If hello container doesn't exist you'll need toocreate it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="ed99c-132">Crear un archivo JSON que describe cómo toodownload Hola script desde el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed99c-132">Also create a JSON file that describes how toodownload hello script from Azure Storage.</span></span> <span data-ttu-id="ed99c-133">Guardar como *public_config.json* (reemplazando "mystorage" con el nombre de saludo de la cuenta de almacenamiento):</span><span class="sxs-lookup"><span data-stu-id="ed99c-133">Save this as *public_config.json* (replacing "mystorage" with hello name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a><span data-ttu-id="ed99c-134">Implementar la extensión de Hola</span><span class="sxs-lookup"><span data-stu-id="ed99c-134">Deploy hello extension</span></span>
<span data-ttu-id="ed99c-135">Ahora puede usar Hola siguiente comando toodeploy Hola CustomScript extensión de Linux toohello remoto VM con Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed99c-135">Now you can use hello next command toodeploy hello Linux CustomScript Extension toohello remote VM using hello Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="ed99c-136">comando anterior Hola descarga y ejecuta hello *install_lamp.sh* secuencia de comandos de hello VM llama *lamp-vm*.</span><span class="sxs-lookup"><span data-stu-id="ed99c-136">hello previous command downloads and runs hello *install_lamp.sh* script on hello VM called *lamp-vm*.</span></span>

<span data-ttu-id="ed99c-137">Puesto que la aplicación hello incluye un servidor web, recuerde tooopen HTTP el puerto de escucha en hello VM remoto con el comando siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="ed99c-137">Since hello app includes a web server, remember tooopen an HTTP listening port on hello remote VM with hello next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="ed99c-138">Supervisión y solución de problemas</span><span class="sxs-lookup"><span data-stu-id="ed99c-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="ed99c-139">Puede comprobar en grado ejecuciones de secuencia de comandos personalizada hello examinando el archivo de registro de hello Hola VM remoto.</span><span class="sxs-lookup"><span data-stu-id="ed99c-139">You can check on how well hello custom script runs by looking at hello log file on hello remote VM.</span></span> <span data-ttu-id="ed99c-140">SSH demasiado*lamp-vm* y archivo de registro de hello final con el comando siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="ed99c-140">SSH too*lamp-vm* and tail hello log file with hello next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="ed99c-141">Después de ejecutar la CustomScript extensión hello, puede examinar la página PHP toohello que ha creado para obtener información.</span><span class="sxs-lookup"><span data-stu-id="ed99c-141">After you run hello CustomScript Extension, you can browse toohello PHP page you created for information.</span></span> <span data-ttu-id="ed99c-142">Hola PHP página de ejemplo de Hola en este artículo es *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="ed99c-142">hello PHP page for hello example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed99c-143">Recursos adicionales</span><span class="sxs-lookup"><span data-stu-id="ed99c-143">Additional resources</span></span>
<span data-ttu-id="ed99c-144">Puede usar Hola mismo toodeploy pasos básicos aplicaciones más complejas.</span><span class="sxs-lookup"><span data-stu-id="ed99c-144">You can use hello same basic steps toodeploy more complex apps.</span></span> <span data-ttu-id="ed99c-145">En este ejemplo se guardó el script de instalación de Hola como un blob público en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ed99c-145">In this example hello install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="ed99c-146">Una opción más segura sería el script de instalación de hello toostore como un blob seguro con un [firma de acceso seguro](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="ed99c-146">A more secure option would be toostore hello install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="ed99c-147">Recursos adicionales de CLI de Azure, Linux y Hola CustomScript extensión se enumeran a continuación.</span><span class="sxs-lookup"><span data-stu-id="ed99c-147">Additional resources for Azure CLI, Linux and hello CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="ed99c-148">Automatización de las tareas de personalización de VM de Linux con la extensión CustomScript</span><span class="sxs-lookup"><span data-stu-id="ed99c-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="ed99c-149">Extensiones de Linux de Azure (GitHub)</span><span class="sxs-lookup"><span data-stu-id="ed99c-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)