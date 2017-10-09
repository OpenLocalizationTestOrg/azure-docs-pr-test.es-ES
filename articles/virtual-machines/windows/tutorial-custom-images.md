---
title: "imágenes de máquina virtual personalizadas aaaCreate con hello Azure PowerShell | Documentos de Microsoft"
description: "Tutorial: crear una imagen de máquina virtual personalizada con hello Azure PowerShell."
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
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="ca98f-103">Creación de una imagen personalizada de una máquina virtual de Azure mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca98f-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="ca98f-104">Las imágenes personalizadas son como las imágenes de Marketplace, pero las puede crear usted mismo.</span><span class="sxs-lookup"><span data-stu-id="ca98f-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="ca98f-105">Imágenes personalizadas pueden ser configuraciones toobootstrap usado como carga previa de aplicaciones, configuraciones de aplicaciones y otras configuraciones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="ca98f-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="ca98f-106">En este tutorial, creará su propia imagen personalizada de una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="ca98f-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="ca98f-107">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="ca98f-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ca98f-108">Ejecutar Sysprep y generalizar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ca98f-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="ca98f-109">Crear una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="ca98f-109">Create a custom image</span></span>
> * <span data-ttu-id="ca98f-110">Crear una imagen personalizada a partir de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ca98f-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="ca98f-111">Una lista de todas las imágenes de hello en su suscripción</span><span class="sxs-lookup"><span data-stu-id="ca98f-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="ca98f-112">Eliminar una imagen</span><span class="sxs-lookup"><span data-stu-id="ca98f-112">Delete an image</span></span>

<span data-ttu-id="ca98f-113">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="ca98f-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="ca98f-114">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca98f-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="ca98f-115">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ca98f-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ca98f-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="ca98f-116">Before you begin</span></span>

<span data-ttu-id="ca98f-117">Hola los pasos siguientes detalla cómo tootake una máquina virtual existente y a su vez en un personalizado reutilizable de la imagen que pueden usar toocreate nuevas instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ca98f-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="ca98f-118">ejemplo de Hola a toocomplete en este tutorial, debe tener una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="ca98f-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="ca98f-119">Si es necesario, este [script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) puede crear una.</span><span class="sxs-lookup"><span data-stu-id="ca98f-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="ca98f-120">Cuando reemplace trabajar a través de tutorial de hello, grupo de recursos de Hola y VM nombres cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="ca98f-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="ca98f-121">Preparación de la VM</span><span class="sxs-lookup"><span data-stu-id="ca98f-121">Prepare VM</span></span>

<span data-ttu-id="ca98f-122">toocreate una imagen de una máquina virtual, deberá tooprepare Hola VM por hello generalizar VM desasignar y, a continuación, marcar origen Hola VM tal y como se ha generalizado en Azure.</span><span class="sxs-lookup"><span data-stu-id="ca98f-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="ca98f-123">Generalizar Hola VM de Windows con Sysprep</span><span class="sxs-lookup"><span data-stu-id="ca98f-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="ca98f-124">Sysprep quita toda la información de cuenta personal, entre otras cosas y prepara Hola máquina toobe utilizado como una imagen.</span><span class="sxs-lookup"><span data-stu-id="ca98f-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="ca98f-125">Para obtener más información acerca de Sysprep, consulte [cómo tooUse Sysprep: Introducción](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca98f-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="ca98f-126">Conectar la máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="ca98f-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="ca98f-127">Abra la ventana de símbolo del sistema de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="ca98f-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="ca98f-128">Cambie el directorio de hello demasiado*%windir%\system32\sysprep*y, a continuación, ejecute *sysprep.exe*.</span><span class="sxs-lookup"><span data-stu-id="ca98f-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="ca98f-129">Hola **herramienta de preparación del sistema** cuadro de diálogo, seleccione *sistema Out-of-Box experiencia inmediata (OOBE)*y asegúrese de que ese hello *generalizar* casilla está activada.</span><span class="sxs-lookup"><span data-stu-id="ca98f-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="ca98f-130">En **Opciones de apagado**, seleccione *Apagar* y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ca98f-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="ca98f-131">Cuando Sysprep finalice, se apaga máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca98f-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="ca98f-132">**No se reinician Hola VM**.</span><span class="sxs-lookup"><span data-stu-id="ca98f-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="ca98f-133">Cancelar la asignación y marcar Hola VM como generalizado</span><span class="sxs-lookup"><span data-stu-id="ca98f-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="ca98f-134">toocreate una imagen, Hola VM debe toobe cancela la asignación y está marcado como generalizada en Azure.</span><span class="sxs-lookup"><span data-stu-id="ca98f-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="ca98f-135">Hola desasignada VM con [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="ca98f-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="ca98f-136">Establecer el estado de saludo de la máquina virtual de hello demasiado`-Generalized` con [AzureRmVm conjunto](/powershell/module/azurerm.compute/set-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="ca98f-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="ca98f-137">Crear imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="ca98f-137">Create hello image</span></span>

<span data-ttu-id="ca98f-138">Ahora puede crear una imagen de máquina virtual de hello mediante [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) y [AzureRmImage nuevo](/powershell/module/azurerm.compute/new-azurermimage).</span><span class="sxs-lookup"><span data-stu-id="ca98f-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="ca98f-139">Hello en el ejemplo siguiente se crea una imagen denominada *myImage* desde una máquina virtual denominada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="ca98f-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="ca98f-140">Obtenga la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca98f-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="ca98f-141">Crear configuración de la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca98f-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="ca98f-142">Crear imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca98f-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="ca98f-143">Crear máquinas virtuales de la imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="ca98f-143">Create VMs from hello image</span></span>

<span data-ttu-id="ca98f-144">Ahora que tiene una imagen, puede crear una o varias nuevas máquinas virtuales de la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca98f-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="ca98f-145">Crear una máquina virtual a partir de una imagen personalizada es muy similar toocreating una máquina virtual mediante una imagen de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ca98f-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="ca98f-146">Cuando se usa una imagen de Marketplace, tener tooinformation acerca de la imagen de hello, proveedor de imágenes, oferta, SKU y versión.</span><span class="sxs-lookup"><span data-stu-id="ca98f-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="ca98f-147">Con una imagen personalizada, debe tooprovide Hola identificador de recurso de imagen personalizado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ca98f-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="ca98f-148">En la siguiente secuencia de comandos de hello, creamos una variable *$image* toostore información sobre el uso de la imagen personalizada de hello [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) y, a continuación, usamos [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)y especifique el identificador de hello mediante hello *$image* variable que acabamos de crear.</span><span class="sxs-lookup"><span data-stu-id="ca98f-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="ca98f-149">script de Hola crea una máquina virtual denominada *myVMfromImage* desde la imagen personalizada en un nuevo grupo de recursos denominado *myResourceGroupFromImage* en hello *oeste de Estados Unidos* ubicación.</span><span class="sxs-lookup"><span data-stu-id="ca98f-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

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

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="ca98f-150">Administración de imágenes</span><span class="sxs-lookup"><span data-stu-id="ca98f-150">Image management</span></span> 

<span data-ttu-id="ca98f-151">Estos son algunos ejemplos de tareas de imágenes comunes de administración y cómo toocomplete mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca98f-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="ca98f-152">Enumere todas las imágenes por nombre.</span><span class="sxs-lookup"><span data-stu-id="ca98f-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="ca98f-153">Elimine una imagen.</span><span class="sxs-lookup"><span data-stu-id="ca98f-153">Delete an image.</span></span> <span data-ttu-id="ca98f-154">Este ejemplo elimina Hola imagen denominada *myOldImage* de hello *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="ca98f-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ca98f-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca98f-155">Next steps</span></span>

<span data-ttu-id="ca98f-156">En este tutorial, ha creado una imagen de máquina virtual personalizada.</span><span class="sxs-lookup"><span data-stu-id="ca98f-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="ca98f-157">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="ca98f-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ca98f-158">Ejecutar Sysprep y generalizar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="ca98f-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="ca98f-159">Crear una imagen personalizada</span><span class="sxs-lookup"><span data-stu-id="ca98f-159">Create a custom image</span></span>
> * <span data-ttu-id="ca98f-160">Crear una imagen personalizada a partir de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ca98f-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="ca98f-161">Una lista de todas las imágenes de hello en su suscripción</span><span class="sxs-lookup"><span data-stu-id="ca98f-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="ca98f-162">Eliminar una imagen</span><span class="sxs-lookup"><span data-stu-id="ca98f-162">Delete an image</span></span>

<span data-ttu-id="ca98f-163">Avanzar toohello toolearn de tutorial siguiente sobre máquinas virtuales de la alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="ca98f-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ca98f-164">Creación de máquinas virtuales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="ca98f-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



