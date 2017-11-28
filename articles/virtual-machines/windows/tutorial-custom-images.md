---
title: "Creación de imágenes de máquina virtual personalizadas con Azure PowerShell | Microsoft Docs"
description: "Tutorial: creación de una imagen de máquina virtual personalizada mediante Azure PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 96be2872a902a7d7063bf1dff7b4ca209a5b67c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="8f2df-103">Creación de una imagen personalizada de una máquina virtual de Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f2df-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="8f2df-104">Las imágenes personalizadas son como las imágenes de Marketplace, pero las puede crear usted mismo.</span><span class="sxs-lookup"><span data-stu-id="8f2df-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="8f2df-105">Las imágenes personalizadas pueden usarse para configuraciones de arranque como la carga previa de aplicaciones, configuraciones de aplicaciones y otras configuraciones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="8f2df-105">Custom images can be used to bootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="8f2df-106">En este tutorial, creará su propia imagen personalizada de una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f2df-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="8f2df-107">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="8f2df-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f2df-108">Ejecutar Sysprep y generalizar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="8f2df-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="8f2df-109">Crear una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="8f2df-109">Create a custom image</span></span>
> * <span data-ttu-id="8f2df-110">Crear una imagen personalizada a partir de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8f2df-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="8f2df-111">Enumerar todas las imágenes en su suscripción</span><span class="sxs-lookup"><span data-stu-id="8f2df-111">List all the images in your subscription</span></span>
> * <span data-ttu-id="8f2df-112">Eliminar una imagen</span><span class="sxs-lookup"><span data-stu-id="8f2df-112">Delete an image</span></span>

<span data-ttu-id="8f2df-113">Para realizar este tutorial es necesaria la versión 3.6 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="8f2df-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="8f2df-114">Ejecute ` Get-Module -ListAvailable AzureRM` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="8f2df-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="8f2df-115">Si necesita actualizarla, consulte [Instalación del módulo de Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8f2df-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8f2df-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="8f2df-116">Before you begin</span></span>

<span data-ttu-id="8f2df-117">Los siguientes pasos explican cómo tomar una máquina virtual existente y convertirla en una imagen personalizada reutilizable que puede usar para crear nuevas instancias de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8f2df-117">The steps below detail how to take an existing VM and turn it into a re-usable custom image that you can use to create new VM instances.</span></span>

<span data-ttu-id="8f2df-118">Para completar el ejemplo de este tutorial, debe tener una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f2df-118">To complete the example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="8f2df-119">Si es necesario, este [script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) puede crear una.</span><span class="sxs-lookup"><span data-stu-id="8f2df-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="8f2df-120">Al trabajar en el tutorial, reemplace los nombres de grupo de recursos y máquina virtual cuando proceda.</span><span class="sxs-lookup"><span data-stu-id="8f2df-120">When working through the tutorial, replace the resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="8f2df-121">Preparación de la VM</span><span class="sxs-lookup"><span data-stu-id="8f2df-121">Prepare VM</span></span>

<span data-ttu-id="8f2df-122">Para crear una imagen de una máquina virtual, debe preparar la VM generalizando la VM y desasignando y marcando después la VM de origen como generalizada en Azure.</span><span class="sxs-lookup"><span data-stu-id="8f2df-122">To create an image of a virtual machine, you need to prepare the VM by generalizing the VM, deallocating, and then marking the source VM as generalized in Azure.</span></span>

### <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="8f2df-123">Generalización de VM con Windows mediante Sysprep</span><span class="sxs-lookup"><span data-stu-id="8f2df-123">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="8f2df-124">Entre otras características, Sysprep elimina toda la información personal de la cuenta y prepara, entre otras cosas, la máquina para usarse como imagen.</span><span class="sxs-lookup"><span data-stu-id="8f2df-124">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="8f2df-125">Para obtener más información sobre Sysprep, vea [Uso de Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f2df-125">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="8f2df-126">Conexión a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f2df-126">Connect to the virtual machine.</span></span>
2. <span data-ttu-id="8f2df-127">Abra una ventana del símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="8f2df-127">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="8f2df-128">Cambie el directorio a *%windir%\system32\sysprep* y, después, ejecute *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="8f2df-128">Change the directory to *%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="8f2df-129">En **Herramienta de preparación del sistema**, seleccione *Iniciar la Configuración rápida (OOBE)* y asegúrese de que la casilla *Generalizar* está activada.</span><span class="sxs-lookup"><span data-stu-id="8f2df-129">In the **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that the *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="8f2df-130">En **Opciones de apagado**, seleccione *Apagar* y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8f2df-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="8f2df-131">Cuando Sysprep finaliza, apaga la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f2df-131">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="8f2df-132">**No reinicie la VM**.</span><span class="sxs-lookup"><span data-stu-id="8f2df-132">**Do not restart the VM**.</span></span>

### <a name="deallocate-and-mark-the-vm-as-generalized"></a><span data-ttu-id="8f2df-133">Desasignación y marcado de la VM como generalizada</span><span class="sxs-lookup"><span data-stu-id="8f2df-133">Deallocate and mark the VM as generalized</span></span>

<span data-ttu-id="8f2df-134">Para crear una imagen, la VM debe desasignarse y estar marcada como generalizada en Azure.</span><span class="sxs-lookup"><span data-stu-id="8f2df-134">To create an image, the VM needs to be deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="8f2df-135">Cancele la asignación de la VM con [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="8f2df-135">Deallocated the VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="8f2df-136">Establezca el estado de la máquina virtual en `-Generalized` mediante [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="8f2df-136">Set the status of the virtual machine to `-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-the-image"></a><span data-ttu-id="8f2df-137">Crear la imagen</span><span class="sxs-lookup"><span data-stu-id="8f2df-137">Create the image</span></span>

<span data-ttu-id="8f2df-138">Ahora puede crear una imagen de la VM mediante [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) y [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="8f2df-138">Now you can create an image of the VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="8f2df-139">En el ejemplo siguiente se crea una imagen denominada *myImage* a partir de la VM llamada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="8f2df-139">The following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="8f2df-140">Obtenga la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8f2df-140">Get the virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="8f2df-141">Cree la configuración de la imagen.</span><span class="sxs-lookup"><span data-stu-id="8f2df-141">Create the image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="8f2df-142">Cree la imagen.</span><span class="sxs-lookup"><span data-stu-id="8f2df-142">Create the image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-the-image"></a><span data-ttu-id="8f2df-143">Creación de VM a partir de la imagen</span><span class="sxs-lookup"><span data-stu-id="8f2df-143">Create VMs from the image</span></span>

<span data-ttu-id="8f2df-144">Ahora que tiene una imagen, puede crear una o varias VM desde la imagen.</span><span class="sxs-lookup"><span data-stu-id="8f2df-144">Now that you have an image, you can create one or more new VMs from the image.</span></span> <span data-ttu-id="8f2df-145">La creación de una VM a partir de una imagen personalizada es muy similar a la creación de una VM mediante una imagen de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8f2df-145">Creating a VM from a custom image is very similar to creating a VM using a Marketplace image.</span></span> <span data-ttu-id="8f2df-146">Cuando se use una imagen de Marketplace, tendrá que obtener información sobre la imagen, el proveedor de imágenes, la oferta, la SKU y la versión.</span><span class="sxs-lookup"><span data-stu-id="8f2df-146">When you use a Marketplace image, you have to information about the image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="8f2df-147">Con una imagen personalizada, solo debe proporcionar el identificador del recurso de imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="8f2df-147">With a custom image, you just need to provide the ID of the custom image resource.</span></span> 

<span data-ttu-id="8f2df-148">En el siguiente script, se creará una variable *$image* para almacenar información sobre la imagen personalizada mediante [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) y, a continuación, usaremos [conjunto AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) y especificaremos el identificador con la variable *$image* que acabamos de crear.</span><span class="sxs-lookup"><span data-stu-id="8f2df-148">In the following script, we create a variable *$image* to store information about the custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify the ID using the *$image* variable we just created.</span></span> 

<span data-ttu-id="8f2df-149">El script crea una VM denominada *myVMfromImage* a partir de nuestra imagen personalizada en un nuevo grupo de recursos denominado *myResourceGroupFromImage* en la ubicación del *oeste de EE. UU.*</span><span class="sxs-lookup"><span data-stu-id="8f2df-149">The script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in the *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable to store information about the image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want to create the VM from and image and provide the image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="8f2df-150">Administración de imágenes</span><span class="sxs-lookup"><span data-stu-id="8f2df-150">Image management</span></span> 

<span data-ttu-id="8f2df-151">Estos son algunos ejemplos de tareas comunes de administración de imágenes y cómo realizarlas mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f2df-151">Here are some examples of common management image tasks and how to complete them using PowerShell.</span></span>

<span data-ttu-id="8f2df-152">Enumere todas las imágenes por nombre.</span><span class="sxs-lookup"><span data-stu-id="8f2df-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="8f2df-153">Elimine una imagen.</span><span class="sxs-lookup"><span data-stu-id="8f2df-153">Delete an image.</span></span> <span data-ttu-id="8f2df-154">Este ejemplo elimina la imagen con el nombre *myOldImage* de *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="8f2df-154">This example deletes the image named *myOldImage* from the *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8f2df-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8f2df-155">Next steps</span></span>

<span data-ttu-id="8f2df-156">En este tutorial, ha creado una imagen de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="8f2df-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="8f2df-157">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="8f2df-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f2df-158">Ejecutar Sysprep y generalizar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="8f2df-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="8f2df-159">Crear una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="8f2df-159">Create a custom image</span></span>
> * <span data-ttu-id="8f2df-160">Crear una imagen personalizada a partir de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8f2df-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="8f2df-161">Enumerar todas las imágenes en su suscripción</span><span class="sxs-lookup"><span data-stu-id="8f2df-161">List all the images in your subscription</span></span>
> * <span data-ttu-id="8f2df-162">Eliminar una imagen</span><span class="sxs-lookup"><span data-stu-id="8f2df-162">Delete an image</span></span>

<span data-ttu-id="8f2df-163">Avance al siguiente tutorial para obtener información sobre máquinas virtuales de alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="8f2df-163">Advance to the next tutorial to learn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8f2df-164">Creación de máquinas virtuales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="8f2df-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



