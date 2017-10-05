---
title: "Crear y administrar máquinas virtuales con Windows en Azure que usan varias NIC | Microsoft Docs"
description: "Obtenga información sobre cómo crear y administrar una máquina virtual con Windows que tenga varias tarjetas de interfaz de red (NIC) conectadas a ella mediante Azure PowerShell o las plantillas de Resource Manager."
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
ms.openlocfilehash: 3bd99a67dae41de3533d7f6e244eb7ee3ecc4049
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="65725-103">Crear y administrar una máquina virtual con Windows que tiene varias NIC</span><span class="sxs-lookup"><span data-stu-id="65725-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="65725-104">En Azure, las máquinas virtuales (VM) pueden tener varias tarjetas de interfaz de red virtual (NIC) conectadas a ellas.</span><span class="sxs-lookup"><span data-stu-id="65725-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached to them.</span></span> <span data-ttu-id="65725-105">Un escenario común es tener distintas subredes para la conectividad front-end y back-end o una red dedicada a una solución de supervisión o copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="65725-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="65725-106">En este artículo se describe cómo crear una máquina virtual con varias NIC conectadas.</span><span class="sxs-lookup"><span data-stu-id="65725-106">This article details how to create a VM that has multiple NICs attached to it.</span></span> <span data-ttu-id="65725-107">También obtendrá información sobre cómo agregar o quitar NIC de una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="65725-107">You also learn how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="65725-108">Diferentes [tamaños de máquina virtual](sizes.md) admiten un número distinto de NIC, así que ajuste el tamaño de su máquina virtual teniendo esto en cuenta.</span><span class="sxs-lookup"><span data-stu-id="65725-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="65725-109">Para obtener más detalles, incluido cómo crear varias NIC dentro de sus propios scripts de PowerShell, vea la [implementación de máquinas virtuales con varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="65725-109">For detailed information, including how to create multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65725-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="65725-110">Prerequisites</span></span>
<span data-ttu-id="65725-111">Asegúrese de que tiene la [versión de Azure PowerShell más reciente instalada y configurada](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65725-111">Make sure that you have the [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="65725-112">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="65725-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="65725-113">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="65725-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="65725-114">Creación de una máquina virtual con varias NIC</span><span class="sxs-lookup"><span data-stu-id="65725-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="65725-115">En primer lugar, cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="65725-115">First, create a resource group.</span></span> <span data-ttu-id="65725-116">En el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *EastUs*:</span><span class="sxs-lookup"><span data-stu-id="65725-116">The following example creates a resource group named *myResourceGroup* in the *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="65725-117">Creación de redes virtuales y subredes</span><span class="sxs-lookup"><span data-stu-id="65725-117">Create virtual network and subnets</span></span>
<span data-ttu-id="65725-118">Un escenario común es que una red virtual tenga dos o más subredes.</span><span class="sxs-lookup"><span data-stu-id="65725-118">A common scenario is for a virtual network to have two or more subnets.</span></span> <span data-ttu-id="65725-119">Una subred puede ser para el tráfico de front-end y la otra para el tráfico de back-end.</span><span class="sxs-lookup"><span data-stu-id="65725-119">One subnet may be for front-end traffic, the other for back-end traffic.</span></span> <span data-ttu-id="65725-120">Para conectarse a las dos subredes, se usan varias NIC en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65725-120">To connect to both subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="65725-121">Defina dos subredes de red virtual con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="65725-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="65725-122">En el ejemplo siguiente se definen dos subredes para *mySubnetFrontEnd* y *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="65725-122">The following example defines the subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="65725-123">Cree la red virtual y las subredes con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="65725-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="65725-124">En el ejemplo siguiente se crea una red virtual denominada *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="65725-124">The following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="65725-125">Creación de varias NIC</span><span class="sxs-lookup"><span data-stu-id="65725-125">Create multiple NICs</span></span>
<span data-ttu-id="65725-126">Cree dos NIC con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="65725-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="65725-127">Conecte una NIC a la subred de front-end y la otra a la subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="65725-127">Attach one NIC to the front-end subnet and one NIC to the back-end subnet.</span></span> <span data-ttu-id="65725-128">En el ejemplo siguiente se crean las NIC denominadas *myNic1* y *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="65725-128">The following example creates NICs named *myNic1* and *myNic2*:</span></span>

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

<span data-ttu-id="65725-129">Normalmente también se crea un [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) o un [equilibrador de carga](../../load-balancer/load-balancer-overview.md) que ayuden a administrar y distribuir el tráfico entre las distintas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="65725-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="65725-130">En el [artículo más detallado sobre máquinas virtuales con varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) se proporcionan los pasos para crear un grupo de seguridad de red y asignar NIC.</span><span class="sxs-lookup"><span data-stu-id="65725-130">The [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-the-virtual-machine"></a><span data-ttu-id="65725-131">Creación de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="65725-131">Create the virtual machine</span></span>
<span data-ttu-id="65725-132">Comience ahora a compilar la configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65725-132">Now start to build your VM configuration.</span></span> <span data-ttu-id="65725-133">El tamaño de cada máquina virtual tiene un límite en cuanto al número total de NIC que se pueden agregar a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65725-133">Each VM size has a limit for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="65725-134">Para más información, vea [Tamaños de las máquinas virtuales con Windows](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="65725-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="65725-135">Establezca las credenciales de la máquina virtual en la variable `$cred` como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="65725-135">Set your VM credentials to the `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="65725-136">Defina la máquina virtual con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="65725-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="65725-137">En el ejemplo siguiente se define una máquina virtual denominada *myVM* y se usa un tamaño de máquina virtual que admite hasta dos NIC (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="65725-137">The following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="65725-138">Cree el resto de la configuración de máquinas virtuales con [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) y [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="65725-138">Create the rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="65725-139">En el ejemplo siguiente se crea una máquina virtual con Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="65725-139">The following example creates a Windows Server 2016 VM:</span></span>

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

4. <span data-ttu-id="65725-140">Conecte las dos NIC que creó anteriormente con [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="65725-140">Attach the two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="65725-141">Por último, cree la máquina virtual con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="65725-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-to-an-existing-vm"></a><span data-ttu-id="65725-142">Adición de una NIC a una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="65725-142">Add a NIC to an existing VM</span></span>
<span data-ttu-id="65725-143">Para agregar una NIC virtual a una máquina virtual existente, se desasigna la máquina virtual, se agrega la NIC virtual y, después, se inicia la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65725-143">To add a virtual NIC to an existing VM, you deallocate the VM, add the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="65725-144">Desasigne la máquina virtual con [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="65725-144">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="65725-145">En el ejemplo siguiente se desasigna la máquina virtual denominada *myVM* en *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="65725-145">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="65725-146">Obtenga la configuración existente de la máquina virtual con [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="65725-146">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="65725-147">En el ejemplo siguiente se obtiene información de la máquina virtual denominada *myVM* en *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="65725-147">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="65725-148">En el ejemplo siguiente se crea una NIC virtual con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) denominada *myNic3* que está conectada a *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="65725-148">The following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached to *mySubnetBackEnd*.</span></span> <span data-ttu-id="65725-149">Después, la NIC virtual se conecta a la máquina virtual denominada *myVM* en *myResourceGroup* con [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="65725-149">The virtual NIC is then attached to the VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for the back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get the ID of the new virtual NIC and add to VM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="65725-150">NIC virtuales principales</span><span class="sxs-lookup"><span data-stu-id="65725-150">Primary virtual NICs</span></span>
    <span data-ttu-id="65725-151">En una máquina virtual de varias NIC una de las NIC debe ser la principal.</span><span class="sxs-lookup"><span data-stu-id="65725-151">One of the NICs on a multi-NIC VM needs to be primary.</span></span> <span data-ttu-id="65725-152">Si una de las NIC virtuales existentes en la máquina virtual ya se ha establecido como principal, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="65725-152">If one of the existing virtual NICs on the VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="65725-153">En el siguiente ejemplo se da por supuesto que hay dos NIC virtuales en una máquina virtual y que se va a agregar la primera NIC (`[0]`) como la principal:</span><span class="sxs-lookup"><span data-stu-id="65725-153">The following example assumes that two virtual NICs are now present on a VM and you wish to add the first NIC (`[0]`) as the primary:</span></span>
        
    ```powershell
    # List existing NICs on the VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 to be primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update the VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="65725-154">Inicie la máquina virtual con [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="65725-154">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="65725-155">Eliminación de una NIC de una máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="65725-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="65725-156">Para quitar una NIC virtual de una máquina virtual existente, se desasigna la máquina virtual, se quita la NIC virtual y, después, se inicia la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65725-156">To remove a virtual NIC from an existing VM, you deallocate the VM, remove the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="65725-157">Desasigne la máquina virtual con [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="65725-157">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="65725-158">En el ejemplo siguiente se desasigna la máquina virtual denominada *myVM* en *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="65725-158">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="65725-159">Obtenga la configuración existente de la máquina virtual con [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="65725-159">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="65725-160">En el ejemplo siguiente se obtiene información de la máquina virtual denominada *myVM* en *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="65725-160">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="65725-161">Obtenga información sobre la eliminación de NIC con [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="65725-161">Get information about the NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="65725-162">En el ejemplo siguiente se obtiene información sobre *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="65725-162">The following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on the VM if you need to determine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="65725-163">Quite la NIC con [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) y, después, actualice la máquina virtual con [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="65725-163">Remove the NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update the VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="65725-164">En el ejemplo siguiente se quita *myNic3* obtenida por `$nicId` en el paso anterior:</span><span class="sxs-lookup"><span data-stu-id="65725-164">The following example removes *myNic3* as obtained by `$nicId` in the preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="65725-165">Inicie la máquina virtual con [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="65725-165">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="65725-166">Crear varias NIC con plantillas</span><span class="sxs-lookup"><span data-stu-id="65725-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="65725-167">Las plantillas de Azure Resource Manager ofrecen una manera de crear varias instancias de un recurso durante la implementación; por ejemplo, se pueden crear varias NIC.</span><span class="sxs-lookup"><span data-stu-id="65725-167">Azure Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="65725-168">Las plantillas de Resource Manager usan archivos JSON declarativos para definir el entorno.</span><span class="sxs-lookup"><span data-stu-id="65725-168">Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="65725-169">Para más información, vea [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="65725-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="65725-170">Puede usar *copy* para especificar el número de instancias que se crearán:</span><span class="sxs-lookup"><span data-stu-id="65725-170">You can use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="65725-171">Para más información, vea [Creación de varias instancias mediante *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="65725-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="65725-172">También puede usar `copyIndex()` para anexar un número a un nombre de recurso.</span><span class="sxs-lookup"><span data-stu-id="65725-172">You can also use `copyIndex()` to append a number to a resource name.</span></span> <span data-ttu-id="65725-173">Después, puede crear *myNic1*, *MyNic2* y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="65725-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="65725-174">En el código siguiente se muestra un ejemplo de cómo anexar el valor de índice:</span><span class="sxs-lookup"><span data-stu-id="65725-174">The following code shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="65725-175">Puede leer un ejemplo completo de [cómo crear varias NIC mediante plantillas de Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="65725-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="65725-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="65725-176">Next steps</span></span>
<span data-ttu-id="65725-177">Revise [Tamaños de máquina virtual con Windows](sizes.md) cuando esté intentando crear una máquina virtual que tiene varias NIC.</span><span class="sxs-lookup"><span data-stu-id="65725-177">Review [Windows VM sizes](sizes.md) when you're trying to create a VM that has multiple NICs.</span></span> <span data-ttu-id="65725-178">Preste atención al número máximo de NIC que admite cada tamaño de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="65725-178">Pay attention to the maximum number of NICs that each VM size supports.</span></span> 


