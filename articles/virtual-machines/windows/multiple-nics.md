---
title: "aaaCreate y administrar máquinas virtuales de Windows en Azure que usan varios NIC | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y administrar una máquina virtual de Windows que tenga varias NIC a adjunto tooit mediante plantillas de Azure PowerShell o administrador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="93b77-103">Crear y administrar una máquina virtual con Windows que tiene varias NIC</span><span class="sxs-lookup"><span data-stu-id="93b77-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="93b77-104">Máquinas virtuales (VM) en Azure puede tener varios toothem de tarjetas (NIC) adjuntadas de interfaz de red virtual.</span><span class="sxs-lookup"><span data-stu-id="93b77-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="93b77-105">Un escenario común es toohave subredes diferentes para la conectividad de front-end y back-end o una red dedicada tooa supervisión o una solución de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="93b77-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="93b77-106">Este artículo detalla cómo toocreate una máquina virtual con varias NIC había conectado tooit.</span><span class="sxs-lookup"><span data-stu-id="93b77-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="93b77-107">También aprenderá cómo NIC tooadd o quitar de una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="93b77-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="93b77-108">Diferentes [tamaños de máquina virtual](sizes.md) admiten un número distinto de NIC, así que ajuste el tamaño de su máquina virtual teniendo esto en cuenta.</span><span class="sxs-lookup"><span data-stu-id="93b77-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="93b77-109">Para obtener información detallada, incluyendo cómo toocreate varios NIC dentro de sus propios scripts de PowerShell, consulte [implementar máquinas virtuales de varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="93b77-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93b77-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="93b77-110">Prerequisites</span></span>
<span data-ttu-id="93b77-111">Asegúrese de que dispone de hello [versión más reciente de Azure PowerShell instalado y configurado](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="93b77-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="93b77-112">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="93b77-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="93b77-113">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="93b77-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="93b77-114">Creación de una máquina virtual con varias NIC</span><span class="sxs-lookup"><span data-stu-id="93b77-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="93b77-115">En primer lugar, cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="93b77-115">First, create a resource group.</span></span> <span data-ttu-id="93b77-116">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *EastUs* ubicación:</span><span class="sxs-lookup"><span data-stu-id="93b77-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="93b77-117">Creación de redes virtuales y subredes</span><span class="sxs-lookup"><span data-stu-id="93b77-117">Create virtual network and subnets</span></span>
<span data-ttu-id="93b77-118">Un escenario común es para una red virtual toohave dos o más subredes.</span><span class="sxs-lookup"><span data-stu-id="93b77-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="93b77-119">Puede ser una subred para el tráfico de front-end, Hola otro para el tráfico de back-end.</span><span class="sxs-lookup"><span data-stu-id="93b77-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="93b77-120">tooconnect tooboth subredes, a continuación, usa varios NIC en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="93b77-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="93b77-121">Defina dos subredes de red virtual con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="93b77-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="93b77-122">Hello en el ejemplo siguiente se define subredes Hola de *mySubnetFrontEnd* y *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="93b77-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="93b77-123">Cree la red virtual y las subredes con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="93b77-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="93b77-124">Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="93b77-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="93b77-125">Creación de varias NIC</span><span class="sxs-lookup"><span data-stu-id="93b77-125">Create multiple NICs</span></span>
<span data-ttu-id="93b77-126">Cree dos NIC con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="93b77-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="93b77-127">Adjuntar una subred de front-end de toohello NIC y una subred de back-end de toohello NIC.</span><span class="sxs-lookup"><span data-stu-id="93b77-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="93b77-128">Hello en el ejemplo siguiente se crea con el nombre de NIC *myNic1* y *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="93b77-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

<span data-ttu-id="93b77-129">Normalmente se crea también un [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) o [equilibrador de carga](../../load-balancer/load-balancer-overview.md) toohelp administrar y distribuir el tráfico entre las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="93b77-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="93b77-130">Hola [más VM de varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) artículo le guía en la creación de un grupo de seguridad de red y la asignación de NIC.</span><span class="sxs-lookup"><span data-stu-id="93b77-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="93b77-131">Crear la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="93b77-131">Create hello virtual machine</span></span>
<span data-ttu-id="93b77-132">Iniciar toobuild la configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="93b77-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="93b77-133">El tamaño de cada máquina virtual tiene un límite para el número total de Hola de NIC que se puede agregar tooa VM.</span><span class="sxs-lookup"><span data-stu-id="93b77-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="93b77-134">Para más información, vea [Tamaños de las máquinas virtuales con Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="93b77-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="93b77-135">Establecer el toohello de las credenciales de la máquina virtual `$cred` variable como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="93b77-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="93b77-136">Defina la máquina virtual con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="93b77-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="93b77-137">Hello en el ejemplo siguiente se define una máquina virtual denominada *myVM* y utiliza un tamaño de memoria virtual que es compatible con más de dos NIC (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="93b77-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="93b77-138">Crear el resto de saludo de la configuración de máquina virtual con [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) y [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="93b77-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="93b77-139">Hola de ejemplo siguiente crea una máquina virtual de Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="93b77-139">hello following example creates a Windows Server 2016 VM:</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. <span data-ttu-id="93b77-140">Adjuntar Hola dos NIC que creó anteriormente con [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="93b77-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="93b77-141">Por último, cree la máquina virtual con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="93b77-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="93b77-142">Agregar un tooan NIC existente de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="93b77-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="93b77-143">Agregar tooadd una tooan NIC virtual existente de la máquina virtual, se cancela la asignación de hello VM, Hola NIC virtual e inicie Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="93b77-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="93b77-144">Cancela la asignación de Hola VM con [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="93b77-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="93b77-145">Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM* en *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="93b77-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="93b77-146">Obtener la configuración existente de Hola de hello VM con [AzureRmVm Get](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="93b77-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="93b77-147">Hello en el ejemplo siguiente se obtiene información de máquina virtual denominada hello *myVM* en *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="93b77-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="93b77-148">Hello en el ejemplo siguiente se crea una NIC virtual con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) denominado *myNic3* que está conectada demasiado*mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="93b77-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="93b77-149">Hola NIC virtual es, a continuación, adjunta toohello máquina virtual denominada *myVM* en *myResourceGroup* con [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="93b77-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="93b77-150">NIC virtuales principales</span><span class="sxs-lookup"><span data-stu-id="93b77-150">Primary virtual NICs</span></span>
    <span data-ttu-id="93b77-151">Uno de hello NIC en una VM de varias NIC debe toobe principal.</span><span class="sxs-lookup"><span data-stu-id="93b77-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="93b77-152">Si uno de Hola NIC virtuales existentes en hello VM ya está establecida como principal, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="93b77-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="93b77-153">Hello en el ejemplo siguiente se supone que dos NIC virtuales ahora están presentes en una máquina virtual y desea tooadd Hola primera NIC (`[0]`) como Hola principal:</span><span class="sxs-lookup"><span data-stu-id="93b77-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="93b77-154">Iniciar Hola VM con [AzureRmVm inicio](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="93b77-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="93b77-155">Eliminación de una NIC de una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="93b77-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="93b77-156">tooremove una NIC virtual de una máquina virtual existente, se cancela la asignación de hello VM, quite Hola NIC virtual y, a continuación, inicio Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="93b77-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="93b77-157">Cancela la asignación de Hola VM con [AzureRmVM Stop](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="93b77-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="93b77-158">Hello en el ejemplo siguiente se desasigna Hola máquina virtual denominada *myVM* en *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="93b77-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="93b77-159">Obtener la configuración existente de Hola de hello VM con [AzureRmVm Get](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="93b77-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="93b77-160">Hello en el ejemplo siguiente se obtiene información de máquina virtual denominada hello *myVM* en *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="93b77-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="93b77-161">Obtener información acerca de hello NIC quitar con [AzureRmNetworkInterface Get](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="93b77-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="93b77-162">Hello en el ejemplo siguiente se obtiene información sobre *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="93b77-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="93b77-163">Quitar Hola NIC con [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) y actualice Hola VM con [AzureRmVm actualización](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="93b77-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="93b77-164">Quita de Hello en el ejemplo siguiente se *myNic3* obtenida por `$nicId` Hola anterior paso:</span><span class="sxs-lookup"><span data-stu-id="93b77-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="93b77-165">Iniciar Hola VM con [AzureRmVm inicio](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="93b77-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="93b77-166">Crear varias NIC con plantillas</span><span class="sxs-lookup"><span data-stu-id="93b77-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="93b77-167">Plantillas de administrador de recursos de Azure proporcionan una manera toocreate varias instancias de un recurso durante la implementación, como la creación de varias NIC.</span><span class="sxs-lookup"><span data-stu-id="93b77-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="93b77-168">Plantillas de administrador de recursos utilizan declarativa toodefine de archivos JSON en su entorno.</span><span class="sxs-lookup"><span data-stu-id="93b77-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="93b77-169">Para más información, vea [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93b77-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="93b77-170">Puede usar *copia* número de hello toospecify de toocreate de instancias:</span><span class="sxs-lookup"><span data-stu-id="93b77-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="93b77-171">Para más información, vea [Creación de varias instancias mediante *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="93b77-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="93b77-172">También puede usar `copyIndex()` tooappend un nombre de recurso tooa número.</span><span class="sxs-lookup"><span data-stu-id="93b77-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="93b77-173">Después, puede crear *myNic1*, *MyNic2* y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="93b77-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="93b77-174">Hello código siguiente muestra un ejemplo de anexar el valor de índice de hello:</span><span class="sxs-lookup"><span data-stu-id="93b77-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="93b77-175">Puede leer un ejemplo completo de [cómo crear varias NIC mediante plantillas de Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="93b77-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93b77-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="93b77-176">Next steps</span></span>
<span data-ttu-id="93b77-177">Revisión [tamaños de máquina virtual de Windows](sizes.md) al que está tratando de toocreate una máquina virtual que tiene varios NIC.</span><span class="sxs-lookup"><span data-stu-id="93b77-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="93b77-178">Pagar el número máximo de toohello de atención de NIC que admite cada tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="93b77-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 


