---
title: "Implementación de LAMP en una máquina virtual Linux en Azure | Microsoft Docs"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: ad69876bfbeba5f948a81e5c48c659fdf2265ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="14bcd-103">Implementación de la pila LAMP en Azure</span><span class="sxs-lookup"><span data-stu-id="14bcd-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="14bcd-104">En este artículo se ofrecen instrucciones paso a paso sobre cómo implementar un servidor web Apache, MySQL y PHP (la pila LAMP) en Azure.</span><span class="sxs-lookup"><span data-stu-id="14bcd-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="14bcd-105">Necesita una cuenta de Azure ([obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/)) y la [CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="14bcd-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="14bcd-106">También puede llevar a cabo estos pasos con la [CLI de Azure 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="14bcd-106">You can also perform these steps with the [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="14bcd-107">Resumen rápido de comandos</span><span class="sxs-lookup"><span data-stu-id="14bcd-107">Quick command summary</span></span>

1. <span data-ttu-id="14bcd-108">Guarde y edite el [archivo azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) según sus preferencias en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="14bcd-108">Save and edit the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your preference on your local machine.</span></span>
2. <span data-ttu-id="14bcd-109">Ejecute los dos comandos siguientes para crear un grupo de recursos y luego implemente la plantilla:</span><span class="sxs-lookup"><span data-stu-id="14bcd-109">Run the following two commands to create a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="14bcd-110">Implementar LAMP en una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="14bcd-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="14bcd-111">El siguiente comando actualiza paquetes y luego instala Apache, MySQL y PHP:</span><span class="sxs-lookup"><span data-stu-id="14bcd-111">The following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="14bcd-112">Tutorial de implementación de LAMP en una nueva VM</span><span class="sxs-lookup"><span data-stu-id="14bcd-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="14bcd-113">Cree un grupo de recursos con [az group create](/cli/azure/group#create) para que contenga la nueva VM:</span><span class="sxs-lookup"><span data-stu-id="14bcd-113">Create a resource group with [az group create](/cli/azure/group#create) to contain the new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="14bcd-114">Para crear la máquina virtual, puede usar una de las plantillas de Azure Resource Manager que se encuentran [en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="14bcd-114">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="14bcd-115">Guarde el [archivo azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="14bcd-115">Save the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your local machine.</span></span>
3. <span data-ttu-id="14bcd-116">Edite el archivo **azuredeploy.parameters.json** según estime oportuno.</span><span class="sxs-lookup"><span data-stu-id="14bcd-116">Edit the **azuredeploy.parameters.json** file to your preferred inputs.</span></span>
4. <span data-ttu-id="14bcd-117">Implemente la plantilla con [az group deployment create] remitiéndose al archivo json descargado:</span><span class="sxs-lookup"><span data-stu-id="14bcd-117">Deploy the template with [az group deployment create] referencing the downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="14bcd-118">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="14bcd-118">The output is similar to the following example:</span></span>

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="14bcd-119">Ahora ha creado una máquina virtual Linux con la pila LAMP ya instalada.</span><span class="sxs-lookup"><span data-stu-id="14bcd-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="14bcd-120">Si lo desea, puede comprobar la instalación pasando directamente a la sección [Comprobación de que LAMP se ha instalado correctamente](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="14bcd-120">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="14bcd-121">Tutorial de implementación de LAMP en una VM existente</span><span class="sxs-lookup"><span data-stu-id="14bcd-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="14bcd-122">Si necesita ayuda con el proceso de creación de una VM Linux, puede visitar [esta página para aprender a hacerlo](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="14bcd-122">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="14bcd-123">A continuación, necesita acceder mediante SSH a la VM Linux.</span><span class="sxs-lookup"><span data-stu-id="14bcd-123">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="14bcd-124">Si necesita ayuda con el proceso de creación de una clave SSH, puede visitar [esta página para aprender a hacerlo en Linux o Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="14bcd-124">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="14bcd-125">Si ya tiene una clave SSH, continúe y acceda mediante SSH desde la línea de comandos a la VM Linux con `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="14bcd-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="14bcd-126">Ahora que ya puede entrar en la VM Linux para trabajar, le enseñaremos a instalar paso a paso la pila LAMP en distribuciones basadas en Debian.</span><span class="sxs-lookup"><span data-stu-id="14bcd-126">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="14bcd-127">Los comandos exactos podrían ser diferentes en otras distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="14bcd-127">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="14bcd-128">Instalación en Debian y Ubuntu</span><span class="sxs-lookup"><span data-stu-id="14bcd-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="14bcd-129">Necesitará tener instalados los siguientes paquetes: `apache2`, `mysql-server`, `php5` y `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="14bcd-129">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="14bcd-130">Puede instalarlos directamente o mediante Tasksel.</span><span class="sxs-lookup"><span data-stu-id="14bcd-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="14bcd-131">Antes de instalarlos, debe descargar y actualizar las listas de paquetes.</span><span class="sxs-lookup"><span data-stu-id="14bcd-131">Before installing you need to download and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="14bcd-132">Paquetes individuales</span><span class="sxs-lookup"><span data-stu-id="14bcd-132">Individual packages</span></span>
<span data-ttu-id="14bcd-133">Uso de apt-get:</span><span class="sxs-lookup"><span data-stu-id="14bcd-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="14bcd-134">Uso de tasksel</span><span class="sxs-lookup"><span data-stu-id="14bcd-134">Using tasksel</span></span>
<span data-ttu-id="14bcd-135">Como alternativa, puede descargar Tasksel, una herramienta de Debian y Ubuntu que instala varios paquetes relacionados como una tarea coordinada en el sistema.</span><span class="sxs-lookup"><span data-stu-id="14bcd-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="14bcd-136">Tras ejecutar una de las opciones anteriores, se le pedirá que instale estos paquetes y una serie de dependencias.</span><span class="sxs-lookup"><span data-stu-id="14bcd-136">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="14bcd-137">Para establecer un contraseña administrativa para MySQL, presione 'y' seguido de 'Intro' para continuar y siga cualquier otra instrucción que aparezca.</span><span class="sxs-lookup"><span data-stu-id="14bcd-137">To set an administrative password for MySQL, press 'y' and then 'Enter' to continue, and follow any other prompts.</span></span> <span data-ttu-id="14bcd-138">Este proceso instala las extensiones PHP mínimas necesarias para utilizar PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="14bcd-138">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="14bcd-139">Ejecute el siguiente comando para ver otras extensiones PHP disponibles como paquetes:</span><span class="sxs-lookup"><span data-stu-id="14bcd-139">Run the following command to see other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="14bcd-140">Creación de documento info.php</span><span class="sxs-lookup"><span data-stu-id="14bcd-140">Create info.php document</span></span>
<span data-ttu-id="14bcd-141">Ahora podrá comprobar qué versión de Apache, MySQL y PHP tiene a través de la línea de comandos. Para ello, escriba `apache2 -v`, `mysql -v` o `php -v`.</span><span class="sxs-lookup"><span data-stu-id="14bcd-141">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="14bcd-142">Si desea realizar más pruebas, puede crear una página PHP de información rápida para verla en un explorador.</span><span class="sxs-lookup"><span data-stu-id="14bcd-142">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="14bcd-143">Cree un archivo con el editor de texto Nano ejecutando este comando:</span><span class="sxs-lookup"><span data-stu-id="14bcd-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="14bcd-144">En el editor de texto GNU Nano, agregue las siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="14bcd-144">Within the GNU Nano text editor, add the following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="14bcd-145">Después, guarde y salga del editor de texto.</span><span class="sxs-lookup"><span data-stu-id="14bcd-145">Then save and exit the text editor.</span></span>

<span data-ttu-id="14bcd-146">Reinicie Apache con este comando para que todas las nuevas instalaciones surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="14bcd-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="14bcd-147">Comprobación de que LAMP se ha instalado correctamente</span><span class="sxs-lookup"><span data-stu-id="14bcd-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="14bcd-148">Ahora puede comprobar la página de información PHP que creó abriendo un explorador y yendo a http://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="14bcd-148">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="14bcd-149">Debe tener un aspecto similar a esta imagen.</span><span class="sxs-lookup"><span data-stu-id="14bcd-149">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="14bcd-150">Puede comprobar la instalación de Apache visitando la página predeterminada de Apache2 en Ubuntu (http://suDNSúnica/info.php).</span><span class="sxs-lookup"><span data-stu-id="14bcd-150">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="14bcd-151">La salida es similar a la del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="14bcd-151">The output is similar to the following example:</span></span>

![][3]

<span data-ttu-id="14bcd-152">Enhorabuena. Ya ha instalado una pila LAMP en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="14bcd-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="14bcd-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="14bcd-153">Next steps</span></span>
<span data-ttu-id="14bcd-154">Consulte la documentación de Ubuntu relacionada con la pila LAMP:</span><span class="sxs-lookup"><span data-stu-id="14bcd-154">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="14bcd-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="14bcd-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
