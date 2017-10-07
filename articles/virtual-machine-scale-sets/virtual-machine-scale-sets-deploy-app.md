---
title: "establece aaaDeploy una aplicación en la escala de máquinas virtuales"
description: "Utilizar extensiones toodepoy una aplicación en conjuntos de escalas de máquina Virtual de Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="9caa4-103">Implementación de la aplicación en conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9caa4-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="9caa4-104">Este artículo describen distintas formas de cómo establece el software tooinstall de escala de tiempo del Hola Hola se aprovisionó.</span><span class="sxs-lookup"><span data-stu-id="9caa4-104">This article describes different ways of how tooinstall software at hello time hello scale set is provisioned.</span></span>

<span data-ttu-id="9caa4-105">Puede que desee hello tooreview [Introducción al diseño de conjunto escala](virtual-machine-scale-sets-design-overview.md) artículo, que se describe algunos de los límites de hello impuestos por conjuntos de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9caa4-105">You may want tooreview hello [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of hello limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="9caa4-106">Captura y reutilización de una imagen</span><span class="sxs-lookup"><span data-stu-id="9caa4-106">Capture and reuse an image</span></span>

<span data-ttu-id="9caa4-107">Puede usar una máquina virtual que en Azure tooprepare una imagen base para la escala estableciste.</span><span class="sxs-lookup"><span data-stu-id="9caa4-107">You can use a virtual machine you have in Azure tooprepare a base-image for your scale set.</span></span> <span data-ttu-id="9caa4-108">Este proceso crea un disco administrado en su cuenta de almacenamiento, que puede hacer referencia como imagen base hello para el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="9caa4-108">This process creates a managed disk in your storage account, which you can reference as hello base image for your scale set.</span></span> 

<span data-ttu-id="9caa4-109">Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9caa4-109">Do hello following steps:</span></span>

1. <span data-ttu-id="9caa4-110">Cree una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9caa4-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="9caa4-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="9caa4-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="9caa4-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="9caa4-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="9caa4-113">Remoto en Hola máquina virtual y personalizar gusto de tooyour de sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="9caa4-113">Remote into hello virtual machine and customize hello system tooyour liking.</span></span>

   <span data-ttu-id="9caa4-114">Si quiere, puede instalar la aplicación ahora.</span><span class="sxs-lookup"><span data-stu-id="9caa4-114">If you want, you can install your application now.</span></span> <span data-ttu-id="9caa4-115">Sin embargo, saber que al instalar la aplicación ahora, puede realizar actualización de la aplicación más complicada porque puede que necesite tooremove primero.</span><span class="sxs-lookup"><span data-stu-id="9caa4-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need tooremove it first.</span></span> <span data-ttu-id="9caa4-116">En su lugar, puede usar este paso tooinstall todos los requisitos previos que necesita la aplicación, como una característica específica de sistema operativo o en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="9caa4-116">Instead, you can use this step tooinstall any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="9caa4-117">Siga Hola "capturar una máquina" tutorial para cualquiera [Linux] [ linux-vm-capture] o [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="9caa4-117">Follow hello "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="9caa4-118">Crear un [conjunto de escala de máquinas virtuales] [ vmss-create] con hello imagen URI se capturó en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="9caa4-118">Create a [Virtual Machine Scale Set][vmss-create] with hello image URI you captured in hello previous step.</span></span>

<span data-ttu-id="9caa4-119">Para obtener más información sobre los discos, consulte [Información general de Managed Disks](../virtual-machines/windows/managed-disks-overview.md) y [Uso de datos de discos conectados](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="9caa4-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-hello-scale-set-is-provisioned"></a><span data-ttu-id="9caa4-120">Instalar cuando se aprovisiona el conjunto de escalas de Hola</span><span class="sxs-lookup"><span data-stu-id="9caa4-120">Install when hello scale set is provisioned</span></span>

<span data-ttu-id="9caa4-121">Las extensiones de máquina virtual se pueden aplicar tooa conjunto de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9caa4-121">Virtual machine extensions can be applied tooa virtual machine scale set.</span></span> <span data-ttu-id="9caa4-122">Con una extensión de máquina virtual, puede personalizar máquinas virtuales de hello en una escala establecida como un grupo entero.</span><span class="sxs-lookup"><span data-stu-id="9caa4-122">With a virtual machine extension, you can customize hello virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="9caa4-123">Para obtener más información sobre extensiones, consulte [Extensiones de máquinas virtuales](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9caa4-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="9caa4-124">Hay tres extensiones principales que puede usar en función de si el sistema operativo está basado en Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="9caa4-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="9caa4-125">Windows</span><span class="sxs-lookup"><span data-stu-id="9caa4-125">Windows</span></span>

<span data-ttu-id="9caa4-126">Para un sistema operativo basado en Windows, use cualquier hello **Script personalizado v1.8** Hola o extensiones **PowerShell DSC** extensión.</span><span class="sxs-lookup"><span data-stu-id="9caa4-126">For a Windows-based operating system, use either hello **Custom Script v1.8** extension, or hello **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="9caa4-127">Script personalizado</span><span class="sxs-lookup"><span data-stu-id="9caa4-127">Custom Script</span></span>

<span data-ttu-id="9caa4-128">Hola extensión de Script personalizado ejecuta un script en cada instancia de máquina virtual en el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="9caa4-128">hello Custom Script extension runs a script on each virtual machine instance in hello scale set.</span></span> <span data-ttu-id="9caa4-129">Un archivo de configuración o una variable indica qué archivos son la máquina virtual de toohello descargado y, a continuación, se ejecuta el comando.</span><span class="sxs-lookup"><span data-stu-id="9caa4-129">A config file or variable indicates which files are downloaded toohello virtual machine, and then what command runs.</span></span> <span data-ttu-id="9caa4-130">Por ejemplo se pudieron utilizar esta toorun un instalador, una secuencia de comandos, un archivo por lotes, cualquier archivo ejecutable.</span><span class="sxs-lookup"><span data-stu-id="9caa4-130">You could use this toorun an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="9caa4-131">PowerShell utiliza una tabla hash para los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="9caa4-131">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="9caa4-132">Este ejemplo configura toorun de extensión de script personalizado de hello un script de PowerShell que se instala IIS.</span><span class="sxs-lookup"><span data-stu-id="9caa4-132">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="9caa4-133">Hola de uso `-ProtectedSetting` cambie para cualquier configuración que puede contener información confidencial.</span><span class="sxs-lookup"><span data-stu-id="9caa4-133">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="9caa4-134">CLI de Azure utiliza un archivo json para valores de hello.</span><span class="sxs-lookup"><span data-stu-id="9caa4-134">Azure CLI uses a json file for hello settings.</span></span> <span data-ttu-id="9caa4-135">Este ejemplo configura toorun de extensión de script personalizado de hello un script de PowerShell que se instala IIS.</span><span class="sxs-lookup"><span data-stu-id="9caa4-135">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span> <span data-ttu-id="9caa4-136">Guardar Hola siguiente archivo de json como _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="9caa4-136">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="9caa4-137">A continuación, ejecute este comando de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9caa4-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="9caa4-138">Hola de uso `--protected-settings` cambie para cualquier configuración que puede contener información confidencial.</span><span class="sxs-lookup"><span data-stu-id="9caa4-138">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="9caa4-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="9caa4-139">PowerShell DSC</span></span>

<span data-ttu-id="9caa4-140">Puede usar instancias de vm de conjunto de escala de DSC de PowerShell toocustomize Hola.</span><span class="sxs-lookup"><span data-stu-id="9caa4-140">You can use PowerShell DSC toocustomize hello scale set vm instances.</span></span> <span data-ttu-id="9caa4-141">Hola **DSC** extensión publicada por **Microsoft.Powershell** implementa y ejecuta la configuración de DSC de hello proporcionado en cada instancia de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9caa4-141">hello **DSC** extension published by **Microsoft.Powershell** deploys and runs hello provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="9caa4-142">Un archivo de configuración o una variable indica extensión Hola donde *.zip* es el paquete y que _función de script_ toorun de combinación.</span><span class="sxs-lookup"><span data-stu-id="9caa4-142">A config file or variable tells hello extension where *.zip* package is, and which _script-function_ combination toorun.</span></span>

<span data-ttu-id="9caa4-143">PowerShell utiliza una tabla hash para los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="9caa4-143">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="9caa4-144">En este ejemplo se implementa un paquete DSC que instala IIS.</span><span class="sxs-lookup"><span data-stu-id="9caa4-144">This example deploys a DSC package that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="9caa4-145">Hola de uso `-ProtectedSetting` cambie para cualquier configuración que puede contener información confidencial.</span><span class="sxs-lookup"><span data-stu-id="9caa4-145">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="9caa4-146">CLI de Azure usa json para la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="9caa4-146">Azure CLI uses a json for hello settings.</span></span> <span data-ttu-id="9caa4-147">En este ejemplo se implementa un paquete DSC que instala IIS.</span><span class="sxs-lookup"><span data-stu-id="9caa4-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="9caa4-148">Guardar Hola siguiente archivo de json como _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="9caa4-148">Save hello following json file as _settings.json_.</span></span>

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

<span data-ttu-id="9caa4-149">A continuación, ejecute este comando de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9caa4-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="9caa4-150">Hola de uso `--protected-settings` cambie para cualquier configuración que puede contener información confidencial.</span><span class="sxs-lookup"><span data-stu-id="9caa4-150">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="9caa4-151">Linux</span><span class="sxs-lookup"><span data-stu-id="9caa4-151">Linux</span></span>

<span data-ttu-id="9caa4-152">Linux puede usar cualquier hello **v2.0 de Script personalizado** extensión o use **init de la nube** durante la creación.</span><span class="sxs-lookup"><span data-stu-id="9caa4-152">Linux can use either hello **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="9caa4-153">Secuencia de comandos personalizada es una extensión simple que descarga las instancias de máquina virtual de toohello de archivos y se ejecuta un comando.</span><span class="sxs-lookup"><span data-stu-id="9caa4-153">Custom script is a simple extension that downloads files toohello virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="9caa4-154">Script personalizado</span><span class="sxs-lookup"><span data-stu-id="9caa4-154">Custom Script</span></span>

<span data-ttu-id="9caa4-155">Guardar Hola siguiente archivo de json como _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="9caa4-155">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="9caa4-156">Utilice hello Azure CLI tooadd esta tooan de extensión existente de conjunto de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9caa4-156">Use hello Azure CLI tooadd this extension tooan existing virtual machine scale set.</span></span> <span data-ttu-id="9caa4-157">Cada máquina virtual en la escala de hello establecen automáticamente se ejecuta Hola extensión.</span><span class="sxs-lookup"><span data-stu-id="9caa4-157">Each virtual machine in hello scale set automatically runs hello extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="9caa4-158">Hola de uso `--protected-settings` cambie para cualquier configuración que puede contener información confidencial.</span><span class="sxs-lookup"><span data-stu-id="9caa4-158">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="9caa4-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="9caa4-159">Cloud-Init</span></span>

<span data-ttu-id="9caa4-160">En la nube Init se utiliza cuando se crea el conjunto de escalas de Hola.</span><span class="sxs-lookup"><span data-stu-id="9caa4-160">Cloud-Init is used when hello scale set is created.</span></span> <span data-ttu-id="9caa4-161">En primer lugar, cree un archivo local denominado _init.txt nube_ y agregue su tooit de configuración.</span><span class="sxs-lookup"><span data-stu-id="9caa4-161">First, create a local file named _cloud-init.txt_ and add your configuration tooit.</span></span> <span data-ttu-id="9caa4-162">Por ejemplo, consulte [este gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt).</span><span class="sxs-lookup"><span data-stu-id="9caa4-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="9caa4-163">Establece Hola uso toocreate una escala de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="9caa4-163">Use hello Azure CLI toocreate a scale set.</span></span> <span data-ttu-id="9caa4-164">Hola `--custom-data` campo acepta el nombre de archivo de Hola de una secuencia de comandos init de la nube.</span><span class="sxs-lookup"><span data-stu-id="9caa4-164">hello `--custom-data` field accepts hello file name of a cloud-init script.</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="9caa4-165">Instrucciones de administración de actualizaciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="9caa4-165">How do I manage application updates?</span></span>

<span data-ttu-id="9caa4-166">Si ha implementado la aplicación a través de una extensión, modifique la definición de extensión de Hola de alguna manera.</span><span class="sxs-lookup"><span data-stu-id="9caa4-166">If you deployed your application through an extension, alter hello extension definition in some way.</span></span> <span data-ttu-id="9caa4-167">Este cambio hace que las instancias de máquina virtual de hello extensión toobe volver a implementar tooall.</span><span class="sxs-lookup"><span data-stu-id="9caa4-167">This change causes hello extension toobe redeployed tooall virtual machine instances.</span></span> <span data-ttu-id="9caa4-168">Algo **debe** cambiarse acerca de la extensión de hello, como cambiar el nombre de un archivo que se hace referencia, en caso contrario, Azure hace que no vería que Hola extensión ha cambiado.</span><span class="sxs-lookup"><span data-stu-id="9caa4-168">Something **must** be changed about hello extension, such as renaming a referenced file, otherwise, Azure does not see that hello extension has changed.</span></span>

<span data-ttu-id="9caa4-169">Si incrustadas aplicación hello en su propia imagen de sistema operativo, use una canalización de implementación automatizada de actualizaciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9caa4-169">If you baked hello application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="9caa4-170">Diseñar su toofacilitate arquitectura rápido de intercambio de una escala de ensayada se ha establecido en producción.</span><span class="sxs-lookup"><span data-stu-id="9caa4-170">Design your architecture toofacilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="9caa4-171">Un buen ejemplo de este enfoque es hello [trabajo de controlador de Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="9caa4-171">A good example of this approach is hello [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="9caa4-172">[Compresor](https://www.packer.io/) y [Terraform](https://www.terraform.io/) soporte técnico de Azure Resource Manager, por lo que también puede definir las imágenes "como código" y compilarlos en Azure, a continuación, use Hola VHD en el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="9caa4-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use hello VHD in your scale set.</span></span> <span data-ttu-id="9caa4-173">Sin embargo, hacerlo así sería problemático para las imágenes de marketplace, donde los scripts de extensiones o los personalizados se vuelven más importantes ya que no manipula directamente los bits de marketplace.</span><span class="sxs-lookup"><span data-stu-id="9caa4-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="9caa4-174">¿Qué pasa cuando un conjunto de escalado escala horizontalmente?</span><span class="sxs-lookup"><span data-stu-id="9caa4-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="9caa4-175">Al agregar uno o más el conjunto de escala de máquinas virtuales tooa, se instala automáticamente la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9caa4-175">When you add one or more virtual machines tooa scale set, hello application is automatically installed.</span></span> <span data-ttu-id="9caa4-176">Para el ejemplo se si establece la escala de hello tiene extensiones definidas, en una nueva máquina virtual ejecute cada vez que se crea.</span><span class="sxs-lookup"><span data-stu-id="9caa4-176">For example if hello scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="9caa4-177">Si el conjunto de escalas de Hola se basa en una imagen personalizada, cualquier nueva máquina virtual es una copia de la imagen personalizada del origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="9caa4-177">If hello scale set is based on a custom image, any new virtual machine is a copy of hello source custom image.</span></span> <span data-ttu-id="9caa4-178">Si las máquinas virtuales conjunto Hola escala son hosts de contenedor, tendrá contenedores de Hola de tooload de código de inicio en una extensión de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="9caa4-178">If hello scale set virtual machines are container hosts, then you might have startup code tooload hello containers in a Custom Script Extension.</span></span> <span data-ttu-id="9caa4-179">O bien podría haber una extensión que instalara un agente que se registre con un orquestador de clúster, como Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="9caa4-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="9caa4-180">¿Cómo aplicar una actualización de sistema operativo a través de dominios de actualización?</span><span class="sxs-lookup"><span data-stu-id="9caa4-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="9caa4-181">Imagine que desea tooupdate la imagen del SO manteniendo escalas de máquina virtual de hello establecer ejecutando.</span><span class="sxs-lookup"><span data-stu-id="9caa4-181">Suppose you want tooupdate your OS image while keeping hello virtual machine scale set running.</span></span> <span data-ttu-id="9caa4-182">Hello Azure CLI y PowerShell pueden actualizar las imágenes de máquina virtual de hello, una máquina virtual a la vez.</span><span class="sxs-lookup"><span data-stu-id="9caa4-182">PowerShell and hello Azure CLI can update hello virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="9caa4-183">Hola [actualizar un conjunto de escala de máquinas virtuales](./virtual-machine-scale-sets-upgrade-scale-set.md) artículo también proporciona información adicional sobre qué opciones están disponible tooperform actualizar un sistema operativo a través de un conjunto de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9caa4-183">hello [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available tooperform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9caa4-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9caa4-184">Next steps</span></span>

* [<span data-ttu-id="9caa4-185">Usar PowerShell toomanage el conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="9caa4-185">Use PowerShell toomanage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* <span data-ttu-id="9caa4-186">[Creación de una plantilla de conjunto de escalado](virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="9caa4-186">[Create a scale set template.](virtual-machine-scale-sets-mvss-start.md)</span></span>


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

