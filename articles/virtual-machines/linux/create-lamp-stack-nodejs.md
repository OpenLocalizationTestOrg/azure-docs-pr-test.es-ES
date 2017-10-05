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
# <a name="deploy-lamp-stack-with-the-azure-cli-10"></a><span data-ttu-id="904a0-103">Implementar la pila LAMP con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="904a0-103">Deploy LAMP stack with the Azure CLI 1.0</span></span>
<span data-ttu-id="904a0-104">En este artículo se ofrecen instrucciones paso a paso sobre cómo implementar un servidor web Apache, MySQL y PHP (la pila LAMP) en Azure.</span><span class="sxs-lookup"><span data-stu-id="904a0-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="904a0-105">Necesita una cuenta de Azure ([consiga una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/)) y la [CLI de Azure](../../cli-install-nodejs.md) que esté [conectada a su cuenta de Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="904a0-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI](../../cli-install-nodejs.md) that is [connected to your Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="904a0-106">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="904a0-106">CLI versions to complete the task</span></span>
<span data-ttu-id="904a0-107">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="904a0-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="904a0-108">[CLI de Azure 1.0]: CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="904a0-108">[Azure CLI 1.0] – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="904a0-109">[CLI de Azure 2.0 ](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): CLI de última generación para el modelo de implementación de administración de recursos</span><span class="sxs-lookup"><span data-stu-id="904a0-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

```
# One command to create a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="904a0-110">Implementar LAMP en una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="904a0-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, the other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="904a0-111">Tutorial de implementación de LAMP en una nueva VM</span><span class="sxs-lookup"><span data-stu-id="904a0-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="904a0-112">Para empezar, cree un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md) que contendrá la nueva VM:</span><span class="sxs-lookup"><span data-stu-id="904a0-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain the new VM:</span></span>

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

<span data-ttu-id="904a0-113">Para crear la máquina virtual, puede usar una de las plantillas de Azure Resource Manager que se encuentran [en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="904a0-113">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="904a0-114">Debería obtener una respuesta en la que se pide introducir algunos datos más:</span><span class="sxs-lookup"><span data-stu-id="904a0-114">You should see a response prompting some more inputs:</span></span>

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

<span data-ttu-id="904a0-115">Ahora ha creado una máquina virtual Linux con la pila LAMP ya instalada.</span><span class="sxs-lookup"><span data-stu-id="904a0-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="904a0-116">Si lo desea, puede comprobar la instalación pasando directamente a la sección [Comprobación de que LAMP se ha instalado correctamente](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="904a0-116">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="904a0-117">Tutorial de implementación de LAMP en una VM existente</span><span class="sxs-lookup"><span data-stu-id="904a0-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="904a0-118">Si necesita ayuda con el proceso de creación de una VM Linux, puede visitar [esta página para aprender a hacerlo](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="904a0-118">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="904a0-119">A continuación, necesita acceder mediante SSH a la VM Linux.</span><span class="sxs-lookup"><span data-stu-id="904a0-119">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="904a0-120">Si necesita ayuda con el proceso de creación de una clave SSH, puede visitar [esta página para aprender a hacerlo en Linux o Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="904a0-120">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="904a0-121">Si ya tiene una clave SSH, continúe y acceda mediante SSH desde la línea de comandos a la VM Linux con `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="904a0-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="904a0-122">Ahora que ya puede entrar en la VM Linux para trabajar, le enseñaremos a instalar paso a paso la pila LAMP en distribuciones basadas en Debian.</span><span class="sxs-lookup"><span data-stu-id="904a0-122">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="904a0-123">Los comandos exactos podrían ser diferentes en otras distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="904a0-123">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="904a0-124">Instalación en Debian y Ubuntu</span><span class="sxs-lookup"><span data-stu-id="904a0-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="904a0-125">Necesitará tener instalados los siguientes paquetes: `apache2`, `mysql-server`, `php5` y `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="904a0-125">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="904a0-126">Puede instalarlos directamente o mediante Tasksel.</span><span class="sxs-lookup"><span data-stu-id="904a0-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="904a0-127">A continuación, se muestran las instrucciones para ambas opciones.</span><span class="sxs-lookup"><span data-stu-id="904a0-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="904a0-128">Antes de instalarlos, debe descargar y actualizar las listas de paquetes.</span><span class="sxs-lookup"><span data-stu-id="904a0-128">Before installing you need to download and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="904a0-129">Paquetes individuales</span><span class="sxs-lookup"><span data-stu-id="904a0-129">Individual packages</span></span>
<span data-ttu-id="904a0-130">Uso de apt-get:</span><span class="sxs-lookup"><span data-stu-id="904a0-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="904a0-131">Uso de tasksel</span><span class="sxs-lookup"><span data-stu-id="904a0-131">Using tasksel</span></span>
<span data-ttu-id="904a0-132">Como alternativa, puede descargar Tasksel, una herramienta de Debian y Ubuntu que instala varios paquetes relacionados como una tarea coordinada en el sistema.</span><span class="sxs-lookup"><span data-stu-id="904a0-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="904a0-133">Tras ejecutar una de las opciones anteriores, se le pedirá que instale estos paquetes y una serie de dependencias.</span><span class="sxs-lookup"><span data-stu-id="904a0-133">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="904a0-134">Pulse 'y' seguido por 'Enter' para continuar, y siga cualquier otra instrucción que aparezca para establecer un contraseña administrativa para MySQL.</span><span class="sxs-lookup"><span data-stu-id="904a0-134">Press 'y' and then 'Enter' to continue, and follow any other prompts to set an administrative password for MySQL.</span></span> <span data-ttu-id="904a0-135">Este proceso instalará las extensiones PHP mínimas necesarias para utilizar PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="904a0-135">This installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="904a0-136">Ejecute el siguiente comando para ver otras extensiones PHP disponibles como paquetes:</span><span class="sxs-lookup"><span data-stu-id="904a0-136">Run the following command to see other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="904a0-137">Creación de documento info.php</span><span class="sxs-lookup"><span data-stu-id="904a0-137">Create info.php document</span></span>
<span data-ttu-id="904a0-138">Ahora podrá comprobar qué versión de Apache, MySQL y PHP tiene a través de la línea de comandos. Para ello, escriba `apache2 -v`, `mysql -v` o `php -v`.</span><span class="sxs-lookup"><span data-stu-id="904a0-138">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="904a0-139">Si desea realizar más pruebas, puede crear una página PHP de información rápida para verla en un explorador.</span><span class="sxs-lookup"><span data-stu-id="904a0-139">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="904a0-140">Cree un archivo con el editor de texto Nano ejecutando este comando:</span><span class="sxs-lookup"><span data-stu-id="904a0-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="904a0-141">En el editor de texto GNU Nano, agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="904a0-141">Within the GNU Nano text editor, add the following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="904a0-142">Después, guarde y salga del editor de texto.</span><span class="sxs-lookup"><span data-stu-id="904a0-142">Then save and exit the text editor.</span></span>

<span data-ttu-id="904a0-143">Reinicie Apache con este comando para que todas las nuevas instalaciones surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="904a0-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="904a0-144">Comprobación de que LAMP se ha instalado correctamente</span><span class="sxs-lookup"><span data-stu-id="904a0-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="904a0-145">Ahora puede comprobar la página de información PHP que creó abriendo un explorador y yendo a http://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="904a0-145">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="904a0-146">Debe tener un aspecto similar a esta imagen.</span><span class="sxs-lookup"><span data-stu-id="904a0-146">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="904a0-147">Puede comprobar la instalación de Apache visitando la página predeterminada de Apache2 en Ubuntu (http://suDNSúnica/info.php).</span><span class="sxs-lookup"><span data-stu-id="904a0-147">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="904a0-148">Debe ver algo parecido a esta imagen.</span><span class="sxs-lookup"><span data-stu-id="904a0-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="904a0-149">Enhorabuena. Ya ha instalado una pila LAMP en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="904a0-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="904a0-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="904a0-150">Next steps</span></span>
<span data-ttu-id="904a0-151">Consulte la documentación de Ubuntu relacionada con la pila LAMP:</span><span class="sxs-lookup"><span data-stu-id="904a0-151">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="904a0-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="904a0-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png