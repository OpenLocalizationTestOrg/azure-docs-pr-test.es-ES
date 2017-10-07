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
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a><span data-ttu-id="983ee-103">Implementar pila LAMP con hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="983ee-103">Deploy LAMP stack with hello Azure CLI 1.0</span></span>
<span data-ttu-id="983ee-104">Este artículo le guiará a través de cómo toodeploy un Apache web server, MySQL y PHP (pila LAMP de Hola) en Azure.</span><span class="sxs-lookup"><span data-stu-id="983ee-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="983ee-105">Necesita una cuenta de Azure ([obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/)) hello y [CLI de Azure](../../cli-install-nodejs.md) decir [conectado tooyour cuenta de Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="983ee-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI](../../cli-install-nodejs.md) that is [connected tooyour Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="983ee-106">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="983ee-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="983ee-107">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="983ee-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="983ee-108">[Azure CLI 1.0] – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="983ee-108">[Azure CLI 1.0] – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="983ee-109">[Azure 2.0 CLI](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="983ee-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="983ee-110">Implementar LAMP en una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="983ee-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="983ee-111">Tutorial de implementación de LAMP en una nueva VM</span><span class="sxs-lookup"><span data-stu-id="983ee-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="983ee-112">Primero debe crear un [grupo de recursos](../../azure-resource-manager/resource-group-overview.md) que contendrá Hola nueva máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="983ee-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain hello new VM:</span></span>

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

<span data-ttu-id="983ee-113">toocreate Hola propia máquina virtual, puede usar una plantilla de Azure Resource Manager ya escrito [aquí en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="983ee-113">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="983ee-114">Debería obtener una respuesta en la que se pide introducir algunos datos más:</span><span class="sxs-lookup"><span data-stu-id="983ee-114">You should see a response prompting some more inputs:</span></span>

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

<span data-ttu-id="983ee-115">Ahora ha creado una máquina virtual Linux con la pila LAMP ya instalada.</span><span class="sxs-lookup"><span data-stu-id="983ee-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="983ee-116">Si lo desea, puede comprobar la instalación Hola saltar hacia abajo demasiado[comprobar luz correctamente instalada](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="983ee-116">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="983ee-117">Tutorial de implementación de LAMP en una VM existente</span><span class="sxs-lookup"><span data-stu-id="983ee-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="983ee-118">Si necesita ayuda para crear una VM de Linux, puede ir [toolearn aquí cómo toocreate una VM Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="983ee-118">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="983ee-119">A continuación, debe tooSSH en hello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="983ee-119">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="983ee-120">Si necesita ayuda para crear una clave SSH, puede ir [toolearn aquí cómo toocreate una clave SSH en Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="983ee-120">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="983ee-121">Si ya tiene una clave SSH, continúe y acceda mediante SSH desde la línea de comandos a la VM Linux con `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="983ee-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="983ee-122">Ahora que está trabajando en la VM de Linux, podemos guiaremos por la instalación pila LAMP de hello en distribuciones de Debian.</span><span class="sxs-lookup"><span data-stu-id="983ee-122">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="983ee-123">comandos de Hello exacta podrían ser diferente en otras distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="983ee-123">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="983ee-124">Instalación en Debian y Ubuntu</span><span class="sxs-lookup"><span data-stu-id="983ee-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="983ee-125">Necesita Hola siguiendo los paquetes instalados: `apache2`, `mysql-server`, `php5`, y `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="983ee-125">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="983ee-126">Puede instalarlos directamente o mediante Tasksel.</span><span class="sxs-lookup"><span data-stu-id="983ee-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="983ee-127">A continuación, se muestran las instrucciones para ambas opciones.</span><span class="sxs-lookup"><span data-stu-id="983ee-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="983ee-128">Antes de instalar toodownload es necesario y, a continuación, actualizar las listas de paquete.</span><span class="sxs-lookup"><span data-stu-id="983ee-128">Before installing you need toodownload and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="983ee-129">Paquetes individuales</span><span class="sxs-lookup"><span data-stu-id="983ee-129">Individual packages</span></span>
<span data-ttu-id="983ee-130">Uso de apt-get:</span><span class="sxs-lookup"><span data-stu-id="983ee-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="983ee-131">Uso de tasksel</span><span class="sxs-lookup"><span data-stu-id="983ee-131">Using tasksel</span></span>
<span data-ttu-id="983ee-132">Como alternativa, puede descargar Tasksel, una herramienta de Debian y Ubuntu que instala varios paquetes relacionados como una tarea coordinada en el sistema.</span><span class="sxs-lookup"><span data-stu-id="983ee-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="983ee-133">Después de ejecutar cualquiera de las opciones anteriores hello, que se van a ser solicitada tooinstall estos paquetes y varias otras dependencias.</span><span class="sxs-lookup"><span data-stu-id="983ee-133">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="983ee-134">Presione 's' y, a continuación, 'ENTRAR' toocontinue y siga los otro tooset solicita una contraseña administrativa para MySQL.</span><span class="sxs-lookup"><span data-stu-id="983ee-134">Press 'y' and then 'Enter' toocontinue, and follow any other prompts tooset an administrative password for MySQL.</span></span> <span data-ttu-id="983ee-135">Esto instala Hola mínimo necesario PHP extensiones necesarias toouse PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="983ee-135">This installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="983ee-136">Ejecute hello después comando toosee otras extensiones PHP que están disponibles como paquetes:</span><span class="sxs-lookup"><span data-stu-id="983ee-136">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="983ee-137">Creación de documento info.php</span><span class="sxs-lookup"><span data-stu-id="983ee-137">Create info.php document</span></span>
<span data-ttu-id="983ee-138">Ahora debería ser capaz de toocheck qué versión de Apache, MySQL y PHP tiene a través de la línea de comandos de hello escribiendo `apache2 -v`, `mysql -v`, o `php -v`.</span><span class="sxs-lookup"><span data-stu-id="983ee-138">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="983ee-139">Si la diferencia como tootest más, puede crear un rápido tooview de página de información PHP en un explorador.</span><span class="sxs-lookup"><span data-stu-id="983ee-139">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="983ee-140">Cree un archivo con el editor de texto Nano ejecutando este comando:</span><span class="sxs-lookup"><span data-stu-id="983ee-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="983ee-141">En el editor de texto de GNU Nano hello, agregar Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="983ee-141">Within hello GNU Nano text editor, add hello following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="983ee-142">Después, guarde y cierre el editor de texto hello.</span><span class="sxs-lookup"><span data-stu-id="983ee-142">Then save and exit hello text editor.</span></span>

<span data-ttu-id="983ee-143">Reinicie Apache con este comando para que todas las nuevas instalaciones surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="983ee-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="983ee-144">Comprobación de que LAMP se ha instalado correctamente</span><span class="sxs-lookup"><span data-stu-id="983ee-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="983ee-145">Ahora puede comprobar la página de información de hello PHP que creó, abra un explorador y vaya toohttp://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="983ee-145">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="983ee-146">Debería ser una imagen toothis similar.</span><span class="sxs-lookup"><span data-stu-id="983ee-146">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="983ee-147">Puede comprobar la instalación de Apache viendo Hola Apache2 Ubuntu Default Page yendo tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="983ee-147">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="983ee-148">Debe ver algo parecido a esta imagen.</span><span class="sxs-lookup"><span data-stu-id="983ee-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="983ee-149">Enhorabuena. Ya ha instalado una pila LAMP en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="983ee-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="983ee-150">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="983ee-150">Next steps</span></span>
<span data-ttu-id="983ee-151">Desproteger Hola Ubuntu documentación en pila LAMP de hello:</span><span class="sxs-lookup"><span data-stu-id="983ee-151">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="983ee-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="983ee-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png