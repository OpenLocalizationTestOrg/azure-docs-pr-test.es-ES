---
title: "aaaCreate VM desde una imagen de máquina virtual administrada de Azure | Documentos de Microsoft"
description: "Crear una máquina virtual de Windows desde una imagen de máquina virtual administrada generalizada con PowerShell de Azure, en el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="97b09-103">Creación de una máquina virtual a partir de una imagen administrada</span><span class="sxs-lookup"><span data-stu-id="97b09-103">Create a VM from a managed image</span></span>

<span data-ttu-id="97b09-104">Puede crear varias VM a partir de una imagen de VM administrada en Azure.</span><span class="sxs-lookup"><span data-stu-id="97b09-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="97b09-105">Una imagen de máquina virtual administrada contiene Hola información necesarios toocreate una máquina virtual, incluidos los discos de sistema operativo y datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="97b09-106">Hola discos duros virtuales que constituyen la imagen de hello, incluidos los discos de hello OS y los discos de datos, se almacenan como discos administrados.</span><span class="sxs-lookup"><span data-stu-id="97b09-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="97b09-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="97b09-107">Prerequisites</span></span>

<span data-ttu-id="97b09-108">Necesita toohave ya [crea una imagen de máquina virtual administrada](capture-image-resource.md) Hola a toouse para crear nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="97b09-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="97b09-109">Asegúrese de que tiene las últimas versiones de Hola de hello AzureRM.Compute y AzureRM.Network módulos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97b09-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="97b09-110">Abra un símbolo del sistema de PowerShell como administrador y ejecute hello después tooinstall comando ellos.</span><span class="sxs-lookup"><span data-stu-id="97b09-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="97b09-111">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="97b09-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="97b09-112">Recopilar información acerca de la imagen de Hola</span><span class="sxs-lookup"><span data-stu-id="97b09-112">Collect information about hello image</span></span>

<span data-ttu-id="97b09-113">En primer lugar se necesita toogather información básica acerca de la imagen de Hola y cree una variable para la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="97b09-114">Este ejemplo utiliza una imagen de máquina virtual administrada con el nombre **myImage** decir Hola en **myResourceGroup** grupo de recursos de hello **oeste Ee.uu. Central** ubicación.</span><span class="sxs-lookup"><span data-stu-id="97b09-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="97b09-115">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="97b09-115">Create a virtual network</span></span>
<span data-ttu-id="97b09-116">Crear red virtual de Hola y de las subredes de hello [red virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97b09-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="97b09-117">Crear una subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-117">Create hello subnet.</span></span> <span data-ttu-id="97b09-118">Este ejemplo crea una subred denominada **mySubnet** con prefijo de dirección de hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="97b09-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="97b09-119">Crear red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-119">Create hello virtual network.</span></span> <span data-ttu-id="97b09-120">Este ejemplo crea una red virtual denominada **myVnet** con prefijo de dirección de hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="97b09-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="97b09-121">Creación de una dirección IP y una interfaz de red</span><span class="sxs-lookup"><span data-stu-id="97b09-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="97b09-122">tooenable la comunicación con la máquina virtual de hello en la red virtual de hello, necesita un [dirección IP pública](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) y una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="97b09-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="97b09-123">Cree una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="97b09-123">Create a public IP address.</span></span> <span data-ttu-id="97b09-124">Este ejemplo crea una dirección IP pública denominada "**myPip**".</span><span class="sxs-lookup"><span data-stu-id="97b09-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="97b09-125">Crear NIC de Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-125">Create hello NIC.</span></span> <span data-ttu-id="97b09-126">Este ejemplo crea una NIC denominada "**myNic**".</span><span class="sxs-lookup"><span data-stu-id="97b09-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="97b09-127">Crear grupo de seguridad de red de hello y una regla de RDP</span><span class="sxs-lookup"><span data-stu-id="97b09-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="97b09-128">toobe puede toolog en tooyour VM mediante RDP, deberá toohave una regla de seguridad de red (NSG) que permite el acceso RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="97b09-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="97b09-129">Este ejemplo crea un NSG denominado"**myNsg**" que contiene una regla llamada "**myRdpRule**" que permita el tráfico RDP en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="97b09-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="97b09-130">Para obtener más información acerca de los NSG, consulte [abrir puertos tooa VM en Azure con PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97b09-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="97b09-131">Cree una variable para la red virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="97b09-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="97b09-132">Cree una variable para la red virtual de hello completado.</span><span class="sxs-lookup"><span data-stu-id="97b09-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="97b09-133">Obtener las credenciales de Hola Hola VM</span><span class="sxs-lookup"><span data-stu-id="97b09-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="97b09-134">Hello siguiente cmdlet abrirá una ventana donde se incluirá un nuevo toouse de nombre y la contraseña de usuario como cuenta de administrador local de Hola de tengan acceso remoto a Hola VM.</span><span class="sxs-lookup"><span data-stu-id="97b09-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="97b09-135">Las variables establecidas para hello VM name, nombre de equipo y Hola tamaño de hello VM</span><span class="sxs-lookup"><span data-stu-id="97b09-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="97b09-136">Cree variables para el nombre de la máquina virtual de Hola y el nombre de equipo.</span><span class="sxs-lookup"><span data-stu-id="97b09-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="97b09-137">Este ejemplo establece el nombre de la máquina virtual de hello como **myVM** y el nombre de equipo de hello como **MiPC**.</span><span class="sxs-lookup"><span data-stu-id="97b09-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="97b09-138">Establecer tamaño de Hola de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="97b09-139">Este ejemplo crea la VM con el tamaño **Standard_DS1_v2**.</span><span class="sxs-lookup"><span data-stu-id="97b09-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="97b09-140">Vea hello [tamaños de máquina virtual](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentación para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="97b09-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="97b09-141">Agregar nombre de máquina virtual de Hola y de configuración de máquina virtual de tamaño toohello.</span><span class="sxs-lookup"><span data-stu-id="97b09-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="97b09-142">Imagen de máquina virtual de hello conjunto como imagen de origen para hello nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="97b09-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="97b09-143">Establecer la imagen de origen de hello con el Id. de Hola de imagen de VM de hello administrado.</span><span class="sxs-lookup"><span data-stu-id="97b09-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="97b09-144">Establecer la configuración del sistema operativo hello y agregue NIC de Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="97b09-145">Escriba el tipo de almacenamiento de hello (PremiumLRS o StandardLRS) y el tamaño de Hola de disco del sistema operativo Hola.</span><span class="sxs-lookup"><span data-stu-id="97b09-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="97b09-146">Este ejemplo establece el tipo de cuenta de hello demasiado**PremiumLRS**, Hola demasiado de tamaño de disco**128 GB** y disco, almacenamiento en caché demasiado**ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="97b09-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="97b09-147">Crear hello VM</span><span class="sxs-lookup"><span data-stu-id="97b09-147">Create hello VM</span></span>

<span data-ttu-id="97b09-148">Crear nueva máquina virtual con configuración de Hola que hemos creado y almacenado en Hola de Hola **$vm** variable.</span><span class="sxs-lookup"><span data-stu-id="97b09-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="97b09-149">Compruebe que se creó la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="97b09-149">Verify that hello VM was created</span></span>
<span data-ttu-id="97b09-150">Cuando haya finalizado, debería ver Hola recién creado VM hello [portal de Azure](https://portal.azure.com) en **examinar** > **máquinas virtuales**, o mediante Hola siguiente Comandos de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="97b09-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="97b09-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97b09-151">Next steps</span></span>
<span data-ttu-id="97b09-152">toomanage la nueva máquina virtual con PowerShell de Azure, consulte [crear y administrar máquinas virtuales de Windows con el módulo de PowerShell de Azure de hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97b09-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

