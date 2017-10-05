---
title: "Implementación de una aplicación en conjuntos de escalado de máquinas virtuales"
description: "Use extensiones para implementar una aplicación en conjuntos de escalado de máquinas virtuales de Azure."
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
ms.openlocfilehash: fa7d9d3bef4cb326844ede76171e8c566e87116b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="bd92d-103">Implementación de la aplicación en conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="bd92d-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="bd92d-104">En este artículo se describen diferentes formas de instalar software en el momento de aprovisionar el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="bd92d-104">This article describes different ways of how to install software at the time the scale set is provisioned.</span></span>

<span data-ttu-id="bd92d-105">Es recomendable revisar el artículo sobre [introducción al diseño de conjuntos de escalado](virtual-machine-scale-sets-design-overview.md), en el que se describen algunos de los límites impuestos por los conjuntos de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bd92d-105">You may want to review the [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of the limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="bd92d-106">Captura y reutilización de una imagen</span><span class="sxs-lookup"><span data-stu-id="bd92d-106">Capture and reuse an image</span></span>

<span data-ttu-id="bd92d-107">Puede usar una máquina virtual que tenga en Azure para preparar una imagen base para el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="bd92d-107">You can use a virtual machine you have in Azure to prepare a base-image for your scale set.</span></span> <span data-ttu-id="bd92d-108">Mediante este proceso se crea un disco administrado en la cuenta de almacenamiento, al que puede hacerse referencia como imagen base para el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="bd92d-108">This process creates a managed disk in your storage account, which you can reference as the base image for your scale set.</span></span> 

<span data-ttu-id="bd92d-109">Siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="bd92d-109">Do the following steps:</span></span>

1. <span data-ttu-id="bd92d-110">Cree una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd92d-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="bd92d-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="bd92d-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="bd92d-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="bd92d-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="bd92d-113">Acceda de forma remota a la máquina virtual y personalice el sistema a su gusto.</span><span class="sxs-lookup"><span data-stu-id="bd92d-113">Remote into the virtual machine and customize the system to your liking.</span></span>

   <span data-ttu-id="bd92d-114">Si quiere, puede instalar la aplicación ahora.</span><span class="sxs-lookup"><span data-stu-id="bd92d-114">If you want, you can install your application now.</span></span> <span data-ttu-id="bd92d-115">Sin embargo, sepa que si instala la aplicación ahora, puede hacer que resulte más complicada de actualizar, ya que puede tener que eliminarla primero.</span><span class="sxs-lookup"><span data-stu-id="bd92d-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need to remove it first.</span></span> <span data-ttu-id="bd92d-116">En su lugar, puede seguir este paso para instalar cualquier requisito previo que la aplicación pudiera tener, como un entorno en tiempo de ejecución específico o una función de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="bd92d-116">Instead, you can use this step to install any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="bd92d-117">Siga el tutorial de captura de máquinas para [Linux][linux-vm-capture] o [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="bd92d-117">Follow the "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="bd92d-118">Cree un [conjunto de escalado de máquinas virtuales][vmss-create] con el URI de la imagen que capturó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="bd92d-118">Create a [Virtual Machine Scale Set][vmss-create] with the image URI you captured in the previous step.</span></span>

<span data-ttu-id="bd92d-119">Para obtener más información sobre los discos, consulte [Información general de Managed Disks](../virtual-machines/windows/managed-disks-overview.md) y [Uso de datos de discos conectados](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="bd92d-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-the-scale-set-is-provisioned"></a><span data-ttu-id="bd92d-120">Instalación cuando el conjunto de escalado está aprovisionado</span><span class="sxs-lookup"><span data-stu-id="bd92d-120">Install when the scale set is provisioned</span></span>

<span data-ttu-id="bd92d-121">Es posible aplicar extensiones de máquina virtual al conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bd92d-121">Virtual machine extensions can be applied to a virtual machine scale set.</span></span> <span data-ttu-id="bd92d-122">Con una extensión de máquina virtual, puede personalizar las máquinas virtuales de un conjunto de escalado como grupo completo.</span><span class="sxs-lookup"><span data-stu-id="bd92d-122">With a virtual machine extension, you can customize the virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="bd92d-123">Para obtener más información sobre extensiones, consulte [Extensiones de máquinas virtuales](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd92d-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="bd92d-124">Hay tres extensiones principales que puede usar en función de si el sistema operativo está basado en Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="bd92d-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="bd92d-125">Windows</span><span class="sxs-lookup"><span data-stu-id="bd92d-125">Windows</span></span>

<span data-ttu-id="bd92d-126">En los sistemas operativos basados en Windows, use la extensión **Custom Script v1.8**, o bien la extensión **PowerShell DSC**.</span><span class="sxs-lookup"><span data-stu-id="bd92d-126">For a Windows-based operating system, use either the **Custom Script v1.8** extension, or the **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="bd92d-127">Script personalizado</span><span class="sxs-lookup"><span data-stu-id="bd92d-127">Custom Script</span></span>

<span data-ttu-id="bd92d-128">La extensión Custom Script se ejecuta como script en cada instancia de máquina virtual del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="bd92d-128">The Custom Script extension runs a script on each virtual machine instance in the scale set.</span></span> <span data-ttu-id="bd92d-129">Un archivo de configuración o una variable indican qué archivos se descargan en la máquina virtual y, seguidamente, qué comando se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="bd92d-129">A config file or variable indicates which files are downloaded to the virtual machine, and then what command runs.</span></span> <span data-ttu-id="bd92d-130">Podría usarlo para ejecutar, por ejemplo, un instalador, un script, un archivo por lotes o cualquier archivo ejecutable.</span><span class="sxs-lookup"><span data-stu-id="bd92d-130">You could use this to run an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="bd92d-131">PowerShell usa una tabla hash para la configuración.</span><span class="sxs-lookup"><span data-stu-id="bd92d-131">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="bd92d-132">En este ejemplo se configura la extensión de script personalizado para ejecutar un script de PowerShell que instale IIS.</span><span class="sxs-lookup"><span data-stu-id="bd92d-132">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="bd92d-133">Use el conmutador `-ProtectedSetting` para cualquier valor de configuración que pudiera contener información confidencial.</span><span class="sxs-lookup"><span data-stu-id="bd92d-133">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="bd92d-134">La CLI de Azure usa un archivo json para la configuración.</span><span class="sxs-lookup"><span data-stu-id="bd92d-134">Azure CLI uses a json file for the settings.</span></span> <span data-ttu-id="bd92d-135">En este ejemplo se configura la extensión de script personalizado para ejecutar un script de PowerShell que instale IIS.</span><span class="sxs-lookup"><span data-stu-id="bd92d-135">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span> <span data-ttu-id="bd92d-136">Guarde el siguiente archivo json como _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="bd92d-136">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="bd92d-137">A continuación, ejecute este comando de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd92d-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="bd92d-138">Use el conmutador `--protected-settings` para cualquier valor de configuración que pudiera contener información confidencial.</span><span class="sxs-lookup"><span data-stu-id="bd92d-138">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="bd92d-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="bd92d-139">PowerShell DSC</span></span>

<span data-ttu-id="bd92d-140">Puede usar PowerShell DSC para personalizar las instancias de vm del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="bd92d-140">You can use PowerShell DSC to customize the scale set vm instances.</span></span> <span data-ttu-id="bd92d-141">La extensión **DSC** publicada por **Microsoft.Powershell** implementa la configuración de DSC proporcionada y la ejecuta en todas las instancias de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bd92d-141">The **DSC** extension published by **Microsoft.Powershell** deploys and runs the provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="bd92d-142">Un archivo de configuración o una variable indica a la extensión dónde se encuentra el paquete *.zip* y qué combinación de _script-función_ ejecutar.</span><span class="sxs-lookup"><span data-stu-id="bd92d-142">A config file or variable tells the extension where *.zip* package is, and which _script-function_ combination to run.</span></span>

<span data-ttu-id="bd92d-143">PowerShell usa una tabla hash para la configuración.</span><span class="sxs-lookup"><span data-stu-id="bd92d-143">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="bd92d-144">En este ejemplo se implementa un paquete DSC que instala IIS.</span><span class="sxs-lookup"><span data-stu-id="bd92d-144">This example deploys a DSC package that installs IIS.</span></span>

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

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="bd92d-145">Use el conmutador `-ProtectedSetting` para cualquier valor de configuración que pudiera contener información confidencial.</span><span class="sxs-lookup"><span data-stu-id="bd92d-145">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="bd92d-146">La CLI de Azure usa un archivo json para la configuración.</span><span class="sxs-lookup"><span data-stu-id="bd92d-146">Azure CLI uses a json for the settings.</span></span> <span data-ttu-id="bd92d-147">En este ejemplo se implementa un paquete DSC que instala IIS.</span><span class="sxs-lookup"><span data-stu-id="bd92d-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="bd92d-148">Guarde el siguiente archivo json como _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="bd92d-148">Save the following json file as _settings.json_.</span></span>

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

<span data-ttu-id="bd92d-149">A continuación, ejecute este comando de CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="bd92d-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="bd92d-150">Use el conmutador `--protected-settings` para cualquier valor de configuración que pudiera contener información confidencial.</span><span class="sxs-lookup"><span data-stu-id="bd92d-150">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="bd92d-151">Linux</span><span class="sxs-lookup"><span data-stu-id="bd92d-151">Linux</span></span>

<span data-ttu-id="bd92d-152">En Linux pueden usarse la extensión **Custom Script v2.0** o **cloud-init** durante la creación.</span><span class="sxs-lookup"><span data-stu-id="bd92d-152">Linux can use either the **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="bd92d-153">Custom Script es una extensión sencilla que descarga archivos a las instancias de máquinas virtuales y ejecuta un comando.</span><span class="sxs-lookup"><span data-stu-id="bd92d-153">Custom script is a simple extension that downloads files to the virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="bd92d-154">Script personalizado</span><span class="sxs-lookup"><span data-stu-id="bd92d-154">Custom Script</span></span>

<span data-ttu-id="bd92d-155">Guarde el siguiente archivo json como _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="bd92d-155">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="bd92d-156">Use la CLI de Azure para agregar esta extensión a un conjunto de escalado de máquinas virtuales existente.</span><span class="sxs-lookup"><span data-stu-id="bd92d-156">Use the Azure CLI to add this extension to an existing virtual machine scale set.</span></span> <span data-ttu-id="bd92d-157">Cada máquina virtual del conjunto de escalado ejecuta la extensión de forma automática.</span><span class="sxs-lookup"><span data-stu-id="bd92d-157">Each virtual machine in the scale set automatically runs the extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="bd92d-158">Use el conmutador `--protected-settings` para cualquier valor de configuración que pudiera contener información confidencial.</span><span class="sxs-lookup"><span data-stu-id="bd92d-158">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="bd92d-159">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="bd92d-159">Cloud-Init</span></span>

<span data-ttu-id="bd92d-160">Cloud-Init se usa al crear el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="bd92d-160">Cloud-Init is used when the scale set is created.</span></span> <span data-ttu-id="bd92d-161">En primera lugar, cree un archivo local llamado _cloud-init.txt_ y agréguele su configuración.</span><span class="sxs-lookup"><span data-stu-id="bd92d-161">First, create a local file named _cloud-init.txt_ and add your configuration to it.</span></span> <span data-ttu-id="bd92d-162">Por ejemplo, consulte [este gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt).</span><span class="sxs-lookup"><span data-stu-id="bd92d-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="bd92d-163">Use la CLI de Azure para crear un conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="bd92d-163">Use the Azure CLI to create a scale set.</span></span> <span data-ttu-id="bd92d-164">El campo `--custom-data` acepta el nombre de archivo de un script de cloud-init.</span><span class="sxs-lookup"><span data-stu-id="bd92d-164">The `--custom-data` field accepts the file name of a cloud-init script.</span></span>

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

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="bd92d-165">Instrucciones de administración de actualizaciones de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="bd92d-165">How do I manage application updates?</span></span>

<span data-ttu-id="bd92d-166">Si implementó la aplicación por medio de una extensión, altere la definición de la extensión de algún modo.</span><span class="sxs-lookup"><span data-stu-id="bd92d-166">If you deployed your application through an extension, alter the extension definition in some way.</span></span> <span data-ttu-id="bd92d-167">Este cambio hace que la extensión vuelva a implementarse en todas las instancias de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bd92d-167">This change causes the extension to be redeployed to all virtual machine instances.</span></span> <span data-ttu-id="bd92d-168">**Es necesario** cambiar algún elemento de la extensión, por ejemplo, el nombre de un archivo al que se hace referencia, o Azure no detectará el cambio de la extensión.</span><span class="sxs-lookup"><span data-stu-id="bd92d-168">Something **must** be changed about the extension, such as renaming a referenced file, otherwise, Azure does not see that the extension has changed.</span></span>

<span data-ttu-id="bd92d-169">Si incorporó la aplicación a su propia imagen de sistema operativo, use una canalización de implementación automatizada para las actualizaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="bd92d-169">If you baked the application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="bd92d-170">Diseñe la arquitectura para facilitar introducir un conjunto de escalado de ensayo en producción con rapidez.</span><span class="sxs-lookup"><span data-stu-id="bd92d-170">Design your architecture to facilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="bd92d-171">Un buen ejemplo de este enfoque es el [trabajo de controlador Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="bd92d-171">A good example of this approach is the [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="bd92d-172">[Packer](https://www.packer.io/) y [Terraform](https://www.terraform.io/) también son compatibles con Azure Resource Manager, por lo que también puede definir sus imágenes "como código" y compilarlas en Azure, para, a continuación, usar el disco duro virtual en el conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="bd92d-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use the VHD in your scale set.</span></span> <span data-ttu-id="bd92d-173">Sin embargo, hacerlo así sería problemático para las imágenes de marketplace, donde los scripts de extensiones o los personalizados se vuelven más importantes ya que no manipula directamente los bits de marketplace.</span><span class="sxs-lookup"><span data-stu-id="bd92d-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="bd92d-174">¿Qué pasa cuando un conjunto de escalado escala horizontalmente?</span><span class="sxs-lookup"><span data-stu-id="bd92d-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="bd92d-175">Al agregar una o varias máquinas virtuales a un conjunto de escalado, la aplicación se instala automáticamente.</span><span class="sxs-lookup"><span data-stu-id="bd92d-175">When you add one or more virtual machines to a scale set, the application is automatically installed.</span></span> <span data-ttu-id="bd92d-176">Por ejemplo, si el conjunto de escalado tiene extensiones definidas, estas se ejecutan en una máquina virtual nueva cada vez que se crea el conjunto.</span><span class="sxs-lookup"><span data-stu-id="bd92d-176">For example if the scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="bd92d-177">Si el conjunto de escalado se basa en una imagen personalizada, cualquier máquina virtual nueva es una copia de la imagen personalizada de origen.</span><span class="sxs-lookup"><span data-stu-id="bd92d-177">If the scale set is based on a custom image, any new virtual machine is a copy of the source custom image.</span></span> <span data-ttu-id="bd92d-178">Si las máquinas virtuales del conjunto de escalado son hosts de contenedor, podría hacer que hubiera código de inicio que cargara los contenedores en una extensión Custom Script.</span><span class="sxs-lookup"><span data-stu-id="bd92d-178">If the scale set virtual machines are container hosts, then you might have startup code to load the containers in a Custom Script Extension.</span></span> <span data-ttu-id="bd92d-179">O bien podría haber una extensión que instalara un agente que se registre con un orquestador de clúster, como Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="bd92d-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="bd92d-180">¿Cómo aplicar una actualización de sistema operativo a través de dominios de actualización?</span><span class="sxs-lookup"><span data-stu-id="bd92d-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="bd92d-181">Suponga que quiere actualizar la imagen de sistema operativo al tiempo que mantiene el conjunto de escalado de máquinas virtuales en ejecución.</span><span class="sxs-lookup"><span data-stu-id="bd92d-181">Suppose you want to update your OS image while keeping the virtual machine scale set running.</span></span> <span data-ttu-id="bd92d-182">PowerShell y la CLI de Azure pueden actualizar las imágenes de las máquinas virtuales, una máquina virtual cada vez.</span><span class="sxs-lookup"><span data-stu-id="bd92d-182">PowerShell and the Azure CLI can update the virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="bd92d-183">En el artículo [Actualización de un conjunto de escalado de máquinas virtuales](./virtual-machine-scale-sets-upgrade-scale-set.md) también se proporciona más información sobre qué opciones hay disponibles para realizar actualizaciones del sistema operativo en un conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="bd92d-183">The [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available to perform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd92d-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd92d-184">Next steps</span></span>

* <span data-ttu-id="bd92d-185">[Uso de PowerShell para administrar un conjunto de escalado](virtual-machine-scale-sets-windows-manage.md).</span><span class="sxs-lookup"><span data-stu-id="bd92d-185">[Use PowerShell to manage your scale set.](virtual-machine-scale-sets-windows-manage.md)</span></span>
* <span data-ttu-id="bd92d-186">[Creación de una plantilla de conjunto de escalado](virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="bd92d-186">[Create a scale set template.](virtual-machine-scale-sets-mvss-start.md)</span></span>


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

