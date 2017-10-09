---
title: "aaaDeploy LAMP en una máquina virtual de Linux en Azure | Documentos de Microsoft"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="7262b-103">Implementación de la pila LAMP en Azure</span><span class="sxs-lookup"><span data-stu-id="7262b-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="7262b-104">Este artículo le guiará a través de cómo toodeploy un Apache web server, MySQL y PHP (pila LAMP de Hola) en Azure.</span><span class="sxs-lookup"><span data-stu-id="7262b-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="7262b-105">Necesita una cuenta de Azure ([obtener una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/)) hello y [CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="7262b-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="7262b-106">También puede realizar estos pasos con hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7262b-106">You can also perform these steps with hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="7262b-107">Resumen rápido de comandos</span><span class="sxs-lookup"><span data-stu-id="7262b-107">Quick command summary</span></span>

1. <span data-ttu-id="7262b-108">Guardar y editar hello [azuredeploy.parameters.json archivo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preferencia en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="7262b-108">Save and edit hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preference on your local machine.</span></span>
2. <span data-ttu-id="7262b-109">Ejecute hello siguiendo dos toocreate de comandos de un grupo de recursos y, a continuación, implementar la plantilla:</span><span class="sxs-lookup"><span data-stu-id="7262b-109">Run hello following two commands toocreate a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="7262b-110">Implementar LAMP en una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="7262b-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="7262b-111">siguiente Hola comandos paquetes de actualizaciones y, a continuación, instala Apache, MySQL y PHP:</span><span class="sxs-lookup"><span data-stu-id="7262b-111">hello following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="7262b-112">Tutorial de implementación de LAMP en una nueva VM</span><span class="sxs-lookup"><span data-stu-id="7262b-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="7262b-113">Crear un grupo de recursos con [crear grupo az](/cli/azure/group#create) toocontain Hola nueva máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="7262b-113">Create a resource group with [az group create](/cli/azure/group#create) toocontain hello new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="7262b-114">toocreate Hola propia máquina virtual, puede usar una plantilla de Azure Resource Manager ya escrito [aquí en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="7262b-114">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="7262b-115">Guardar hello [azuredeploy.parameters.json archivo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour de equipo local.</span><span class="sxs-lookup"><span data-stu-id="7262b-115">Save hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour local machine.</span></span>
3. <span data-ttu-id="7262b-116">Editar hello **azuredeploy.parameters.json** tooyour de archivo preferido entradas.</span><span class="sxs-lookup"><span data-stu-id="7262b-116">Edit hello **azuredeploy.parameters.json** file tooyour preferred inputs.</span></span>
4. <span data-ttu-id="7262b-117">Implementar la plantilla de hello con [Crear implementación de grupo az] hace referencia a Hola Descargar archivo json:</span><span class="sxs-lookup"><span data-stu-id="7262b-117">Deploy hello template with [az group deployment create] referencing hello downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="7262b-118">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7262b-118">hello output is similar toohello following example:</span></span>

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

<span data-ttu-id="7262b-119">Ahora ha creado una máquina virtual Linux con la pila LAMP ya instalada.</span><span class="sxs-lookup"><span data-stu-id="7262b-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="7262b-120">Si lo desea, puede comprobar la instalación Hola saltar hacia abajo demasiado[comprobar luz correctamente instalada](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="7262b-120">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="7262b-121">Tutorial de implementación de LAMP en una VM existente</span><span class="sxs-lookup"><span data-stu-id="7262b-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="7262b-122">Si necesita ayuda para crear una VM de Linux, puede ir [toolearn aquí cómo toocreate una VM Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="7262b-122">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="7262b-123">A continuación, debe tooSSH en hello VM de Linux.</span><span class="sxs-lookup"><span data-stu-id="7262b-123">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="7262b-124">Si necesita ayuda para crear una clave SSH, puede ir [toolearn aquí cómo toocreate una clave SSH en Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7262b-124">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="7262b-125">Si ya tiene una clave SSH, continúe y acceda mediante SSH desde la línea de comandos a la VM Linux con `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="7262b-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="7262b-126">Ahora que está trabajando en la VM de Linux, podemos guiaremos por la instalación pila LAMP de hello en distribuciones de Debian.</span><span class="sxs-lookup"><span data-stu-id="7262b-126">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="7262b-127">comandos de Hello exacta podrían ser diferente en otras distribuciones de Linux.</span><span class="sxs-lookup"><span data-stu-id="7262b-127">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="7262b-128">Instalación en Debian y Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7262b-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="7262b-129">Necesita Hola siguiendo los paquetes instalados: `apache2`, `mysql-server`, `php5`, y `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="7262b-129">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="7262b-130">Puede instalarlos directamente o mediante Tasksel.</span><span class="sxs-lookup"><span data-stu-id="7262b-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="7262b-131">Antes de instalar toodownload es necesario y, a continuación, actualizar las listas de paquete.</span><span class="sxs-lookup"><span data-stu-id="7262b-131">Before installing you need toodownload and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="7262b-132">Paquetes individuales</span><span class="sxs-lookup"><span data-stu-id="7262b-132">Individual packages</span></span>
<span data-ttu-id="7262b-133">Uso de apt-get:</span><span class="sxs-lookup"><span data-stu-id="7262b-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="7262b-134">Uso de tasksel</span><span class="sxs-lookup"><span data-stu-id="7262b-134">Using tasksel</span></span>
<span data-ttu-id="7262b-135">Como alternativa, puede descargar Tasksel, una herramienta de Debian y Ubuntu que instala varios paquetes relacionados como una tarea coordinada en el sistema.</span><span class="sxs-lookup"><span data-stu-id="7262b-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="7262b-136">Después de ejecutar cualquiera de las opciones anteriores hello, que se van a ser solicitada tooinstall estos paquetes y varias otras dependencias.</span><span class="sxs-lookup"><span data-stu-id="7262b-136">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="7262b-137">tooset una contraseña administrativa para MySQL, presione 's' y, a continuación, 'ENTRAR' toocontinue y siga las indicaciones de otros.</span><span class="sxs-lookup"><span data-stu-id="7262b-137">tooset an administrative password for MySQL, press 'y' and then 'Enter' toocontinue, and follow any other prompts.</span></span> <span data-ttu-id="7262b-138">Este proceso instala Hola mínimo necesario PHP extensiones necesarias toouse PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="7262b-138">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="7262b-139">Ejecute hello después comando toosee otras extensiones PHP que están disponibles como paquetes:</span><span class="sxs-lookup"><span data-stu-id="7262b-139">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="7262b-140">Creación de documento info.php</span><span class="sxs-lookup"><span data-stu-id="7262b-140">Create info.php document</span></span>
<span data-ttu-id="7262b-141">Ahora debería ser capaz de toocheck qué versión de Apache, MySQL y PHP tiene a través de la línea de comandos de hello escribiendo `apache2 -v`, `mysql -v`, o `php -v`.</span><span class="sxs-lookup"><span data-stu-id="7262b-141">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="7262b-142">Si la diferencia como tootest más, puede crear un rápido tooview de página de información PHP en un explorador.</span><span class="sxs-lookup"><span data-stu-id="7262b-142">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="7262b-143">Cree un archivo con el editor de texto Nano ejecutando este comando:</span><span class="sxs-lookup"><span data-stu-id="7262b-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="7262b-144">En el editor de texto de GNU Nano hello, agregar Hola siguientes líneas:</span><span class="sxs-lookup"><span data-stu-id="7262b-144">Within hello GNU Nano text editor, add hello following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="7262b-145">Después, guarde y cierre el editor de texto hello.</span><span class="sxs-lookup"><span data-stu-id="7262b-145">Then save and exit hello text editor.</span></span>

<span data-ttu-id="7262b-146">Reinicie Apache con este comando para que todas las nuevas instalaciones surtan efecto.</span><span class="sxs-lookup"><span data-stu-id="7262b-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="7262b-147">Comprobación de que LAMP se ha instalado correctamente</span><span class="sxs-lookup"><span data-stu-id="7262b-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="7262b-148">Ahora puede comprobar la página de información de hello PHP que creó, abra un explorador y vaya toohttp://youruniqueDNS/info.php.</span><span class="sxs-lookup"><span data-stu-id="7262b-148">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="7262b-149">Debería ser una imagen toothis similar.</span><span class="sxs-lookup"><span data-stu-id="7262b-149">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="7262b-150">Puede comprobar la instalación de Apache viendo Hola Apache2 Ubuntu Default Page yendo tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="7262b-150">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="7262b-151">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7262b-151">hello output is similar toohello following example:</span></span>

![][3]

<span data-ttu-id="7262b-152">Enhorabuena. Ya ha instalado una pila LAMP en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="7262b-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="7262b-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7262b-153">Next steps</span></span>
<span data-ttu-id="7262b-154">Desproteger Hola Ubuntu documentación en pila LAMP de hello:</span><span class="sxs-lookup"><span data-stu-id="7262b-154">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="7262b-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="7262b-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
