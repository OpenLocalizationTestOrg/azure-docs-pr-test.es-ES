---
title: "Hola a aaaCreate y administrar máquinas virtuales de Windows con el módulo de PowerShell de Azure | Documentos de Microsoft"
description: "Tutorial: crear y administrar máquinas virtuales de Windows con Hola módulo Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a><span data-ttu-id="9ecf8-103">Crear y administrar máquinas virtuales de Windows con Hola módulo Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ecf8-103">Create and Manage Windows VMs with hello Azure PowerShell module</span></span>

<span data-ttu-id="9ecf8-104">Las máquinas virtuales de Azure proporcionan un entorno informático completamente configurable y flexible.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="9ecf8-105">En este tutorial se tratan elementos básicos de la implementación de máquinas virtuales de Azure, como la selección de su tamaño, la selección de una imagen de máquina virtual y la implementación de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="9ecf8-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="9ecf8-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ecf8-107">Crear y conectar tooa VM</span><span class="sxs-lookup"><span data-stu-id="9ecf8-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="9ecf8-108">Seleccionar y usar imágenes de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9ecf8-108">Select and use VM images</span></span>
> * <span data-ttu-id="9ecf8-109">Ver y usar tamaños de una máquina virtual específicos</span><span class="sxs-lookup"><span data-stu-id="9ecf8-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="9ecf8-110">Cambiar el tamaño de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-110">Resize a VM</span></span>
> * <span data-ttu-id="9ecf8-111">Ver y entender el estado de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9ecf8-111">View and understand VM state</span></span>

<span data-ttu-id="9ecf8-112">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-112">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="9ecf8-113">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-113">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="9ecf8-114">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="9ecf8-114">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="9ecf8-115">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9ecf8-115">Create resource group</span></span>

<span data-ttu-id="9ecf8-116">Crear un grupo de recursos con hello [AzureRmResourceGroup New](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-116">Create a resource group with hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="9ecf8-117">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="9ecf8-118">Se debe crear un grupo de recursos antes de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="9ecf8-119">En este ejemplo, un grupo de recursos denominado *myResourceGroupVM* se crea en hello *EastUS* región.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-119">In this example, a resource group named *myResourceGroupVM* is created in hello *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="9ecf8-120">grupo de recursos de Hola se especifica al crear o modificar una máquina virtual, que puede ser vista a lo largo de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="9ecf8-121">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="9ecf8-121">Create virtual machine</span></span>

<span data-ttu-id="9ecf8-122">Una máquina virtual debe estar conectado tooa red virtual.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-122">A virtual machine must be connected tooa virtual network.</span></span> <span data-ttu-id="9ecf8-123">Comunicarse con la máquina virtual de hello mediante una dirección IP pública a través de una tarjeta de interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-123">You communicate with hello virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="9ecf8-124">Creación de una red virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-124">Create virtual network</span></span>

<span data-ttu-id="9ecf8-125">Cree una subred con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="9ecf8-126">Cree una red virtual con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="9ecf8-127">Creación de una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="9ecf8-127">Create public IP address</span></span>

<span data-ttu-id="9ecf8-128">Cree una dirección IP pública con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="9ecf8-129">Creación de una tarjeta de interfaz de red</span><span class="sxs-lookup"><span data-stu-id="9ecf8-129">Create network interface card</span></span>

<span data-ttu-id="9ecf8-130">Cree una tarjeta de interfaz de red con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="9ecf8-131">Creación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="9ecf8-131">Create network security group</span></span>

<span data-ttu-id="9ecf8-132">Un [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) de Azure controla el tráfico entrante y saliente para una o varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="9ecf8-133">Las reglas del grupo de seguridad de red permiten o deniegan el tráfico de red en un puerto específico o en un intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="9ecf8-134">Estas reglas también pueden incluir un prefijo de dirección de origen para que solo el tráfico que se origine en un origen predefinido pueda comunicarse con una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="9ecf8-135">tooaccess servidor Web IIS de Hola que va a instalar, debe agregar una regla de NSG de entrada.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-135">tooaccess hello IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="9ecf8-136">usar toocreate una regla de entrada NSG, [AzureRmNetworkSecurityRuleConfig agregar](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="9ecf8-136">toocreate an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="9ecf8-137">Hello en el ejemplo siguiente se crea una regla NSG denominada *myNSGRule* que abre el puerto *3389* para la máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="9ecf8-137">hello following example creates an NSG rule named *myNSGRule* that opens port *3389* for hello virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

<span data-ttu-id="9ecf8-138">Crear hello NSG mediante *myNSGRule* con [AzureRmNetworkSecurityGroup New](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-138">Create hello NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="9ecf8-139">Agregar subred de hello NSG toohello en red virtual de hello con [AzureRmVirtualNetworkSubnetConfig conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-139">Add hello NSG toohello subnet in hello virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="9ecf8-140">Red virtual de Hola de actualización con [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-140">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="9ecf8-141">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="9ecf8-141">Create virtual machine</span></span>

<span data-ttu-id="9ecf8-142">Al crear una máquina virtual, están disponibles varias opciones, como la imagen de sistema operativo, tamaño de disco y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="9ecf8-143">En este ejemplo, se crea una máquina virtual con el nombre de *myVM* versión más reciente en ejecución Hola del centro de datos de Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-143">In this example, a virtual machine is created with a name of *myVM* running hello latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="9ecf8-144">Establecer nombre de usuario de Hola y la contraseña necesarios para la cuenta de administrador de hello en hello la máquina virtual con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-144">Set hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="9ecf8-145">Crear la configuración inicial de hello para la máquina virtual de hello con [AzureRmVMConfig New](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-145">Create hello initial configuration for hello virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="9ecf8-146">Agregar configuración de máquina virtual de hello sistema operativo información toohello con [AzureRmVMOperatingSystem conjunto](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-146">Add hello operating system information toohello virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="9ecf8-147">Agregar configuración de máquina virtual de hello imagen información toohello con [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-147">Add hello image information toohello virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="9ecf8-148">Agregar configuración de máquina virtual de toohello configuración disco de sistema operativo Hola con [AzureRmVMOSDisk conjunto](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-148">Add hello operating system disk settings toohello virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="9ecf8-149">Tarjeta de interfaz de red de Hola de complemento que creó anteriormente toohello configuración de máquina virtual con [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-149">Add hello network interface card that you previously created toohello virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="9ecf8-150">Crear la máquina virtual Hola con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="9ecf8-150">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a><span data-ttu-id="9ecf8-151">Conectar tooVM</span><span class="sxs-lookup"><span data-stu-id="9ecf8-151">Connect tooVM</span></span>

<span data-ttu-id="9ecf8-152">Una vez finalizada la implementación de hello, cree una conexión a escritorio remota con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-152">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="9ecf8-153">Ejecute hello después comandos tooreturn Hola dirección IP pública de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-153">Run hello following commands tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="9ecf8-154">Tome nota de esta dirección IP para que pueda conectarse tooit con la conectividad de web tootest de explorador en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-154">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="9ecf8-155">Siguiente Hola de uso del comando toocreate una sesión de escritorio remoto con la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-155">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="9ecf8-156">Reemplace la dirección IP de hello con hello *publicIPAddress* de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-156">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="9ecf8-157">Cuando se le solicite, escriba credenciales de hello usadas al crear la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-157">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="9ecf8-158">Descripción de las imágenes de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-158">Understand VM images</span></span>

<span data-ttu-id="9ecf8-159">Hello Azure marketplace incluye muchas imágenes de máquina virtual que pueden ser usado toocreate una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-159">hello Azure marketplace includes many virtual machine images that can be used toocreate a new virtual machine.</span></span> <span data-ttu-id="9ecf8-160">En los pasos anteriores de hello, se crea una máquina virtual mediante la imagen de Windows Server 2016-Datacenter Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-160">In hello previous steps, a virtual machine was created using hello Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="9ecf8-161">En este paso, módulo de PowerShell de hello es marketplace de hello toosearch usado otras imágenes de Windows, puede también como base para nuevas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-161">In this step, hello PowerShell module is used toosearch hello marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="9ecf8-162">Este proceso consiste en Buscar publicador de hello, oferta y nombre de la imagen de hello (Sku).</span><span class="sxs-lookup"><span data-stu-id="9ecf8-162">This process consists of finding hello publisher, offer, and hello image name (Sku).</span></span> 

<span data-ttu-id="9ecf8-163">Hola de uso [Get AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) comando tooreturn una lista de publicadores de imagen.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-163">Use hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command tooreturn a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="9ecf8-164">Hola de uso [AzureRmVMImageOffer Get](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn una lista de ofertas de imagen.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-164">Use hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn a list of image offers.</span></span> <span data-ttu-id="9ecf8-165">Con este comando, Hola devuelve la lista se filtra en el publicador especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-165">With this command, hello returned list is filtered on hello specified publisher.</span></span> 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

<span data-ttu-id="9ecf8-166">Hola [Get AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) comando, a continuación, filtrará en tooreturn de nombre de publicador y oferta de hello una lista de nombres de imagen.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-166">hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on hello publisher and offer name tooreturn a list of image names.</span></span>

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

<span data-ttu-id="9ecf8-167">Esta información puede ser toodeploy usa una máquina virtual con una imagen específica.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-167">This information can be used toodeploy a VM with a specific image.</span></span> <span data-ttu-id="9ecf8-168">Este ejemplo establece el nombre de la imagen de hello en objeto de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-168">This example sets hello image name on hello VM object.</span></span> <span data-ttu-id="9ecf8-169">En este tutorial para los pasos de implementación completa, consulte toohello en los ejemplos anteriores.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-169">Refer toohello previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="9ecf8-170">Comprensión de los tamaños de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-170">Understand VM sizes</span></span>

<span data-ttu-id="9ecf8-171">Un tamaño de máquina virtual determina la cantidad de Hola de recursos de proceso, como CPU y GPU, memoria que se realizan la máquina virtual de toohello disponible.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-171">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="9ecf8-172">Máquinas virtuales deben toobe creado con un tamaño adecuado para hello esperar que la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-172">Virtual machines need toobe created with a size appropriate for hello expect work load.</span></span> <span data-ttu-id="9ecf8-173">Si aumenta la carga de trabajo, se puede cambiar el tamaño de una máquina virtual existente.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="9ecf8-174">Tamaños de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-174">VM Sizes</span></span>

<span data-ttu-id="9ecf8-175">Hello en la tabla siguiente clasifica tamaños en casos de uso.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-175">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="9ecf8-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="9ecf8-176">Type</span></span>                     | <span data-ttu-id="9ecf8-177">Tamaños</span><span class="sxs-lookup"><span data-stu-id="9ecf8-177">Sizes</span></span>           |    <span data-ttu-id="9ecf8-178">Descripción</span><span class="sxs-lookup"><span data-stu-id="9ecf8-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9ecf8-179">Uso general</span><span class="sxs-lookup"><span data-stu-id="9ecf8-179">General purpose</span></span>         |<span data-ttu-id="9ecf8-180">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="9ecf8-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="9ecf8-181">Uso equilibrado de CPU y memoria.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="9ecf8-182">Ideal para desarrollo / pruebas y las soluciones de aplicaciones y datos de toomedium pequeños.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-182">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| <span data-ttu-id="9ecf8-183">Proceso optimizado</span><span class="sxs-lookup"><span data-stu-id="9ecf8-183">Compute optimized</span></span>      | <span data-ttu-id="9ecf8-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="9ecf8-184">Fs, F</span></span>             | <span data-ttu-id="9ecf8-185">Uso elevado de la CPU respecto a la memoria.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-185">High CPU-to-memory.</span></span> <span data-ttu-id="9ecf8-186">Adecuado para aplicaciones, dispositivos de red y procesos por lotes de tráfico medio.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="9ecf8-187">Memoria optimizada</span><span class="sxs-lookup"><span data-stu-id="9ecf8-187">Memory optimized</span></span>       | <span data-ttu-id="9ecf8-188">GS, G, DSv2, DS, Dv2 y D</span><span class="sxs-lookup"><span data-stu-id="9ecf8-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="9ecf8-189">Uso elevado de memoria respecto al núcleo.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-189">High memory-to-core.</span></span> <span data-ttu-id="9ecf8-190">Muy bien para bases de datos relacionales, las cachés de toolarge intermedio y análisis en memoria.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-190">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="9ecf8-191">Almacenamiento optimizado</span><span class="sxs-lookup"><span data-stu-id="9ecf8-191">Storage optimized</span></span>       | <span data-ttu-id="9ecf8-192">LS</span><span class="sxs-lookup"><span data-stu-id="9ecf8-192">Ls</span></span>                | <span data-ttu-id="9ecf8-193">Alto rendimiento de disco y E/S.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-193">High disk throughput and IO.</span></span> <span data-ttu-id="9ecf8-194">Perfecto para bases de datos SQL y NoSQL y macrodatos.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="9ecf8-195">GPU</span><span class="sxs-lookup"><span data-stu-id="9ecf8-195">GPU</span></span>           | <span data-ttu-id="9ecf8-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="9ecf8-196">NV, NC</span></span>            | <span data-ttu-id="9ecf8-197">Máquinas virtuales especializadas específicas para actividades intensas de representación de gráficos y edición de vídeo.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="9ecf8-198">Alto rendimiento</span><span class="sxs-lookup"><span data-stu-id="9ecf8-198">High performance</span></span> | <span data-ttu-id="9ecf8-199">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="9ecf8-199">H, A8-11</span></span>          | <span data-ttu-id="9ecf8-200">Nuestras máquinas virtuales con CPU más eficaces e interfaces de red de alto rendimiento (RDMA) opcionales.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="9ecf8-201">Búsqueda de los tamaños de máquina virtual disponibles</span><span class="sxs-lookup"><span data-stu-id="9ecf8-201">Find available VM sizes</span></span>

<span data-ttu-id="9ecf8-202">toosee una lista de la máquina virtual los tamaños disponibles en una región determinada, use hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) comando.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-202">toosee a list of VM sizes available in a particular region, use hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="9ecf8-203">Cambiar el tamaño de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-203">Resize a VM</span></span>

<span data-ttu-id="9ecf8-204">Una vez implementada una máquina virtual, puede tooincrease cuyo tamaño ha cambiado o reducir la asignación de recursos.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-204">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="9ecf8-205">Antes de cambiar el tamaño de una máquina virtual, compruebe si hello tamaño deseado está disponible en el clúster VM actual Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-205">Before resizing a VM, check if hello desired size is available on hello current VM cluster.</span></span> <span data-ttu-id="9ecf8-206">Hola [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) comando devuelve una lista de tamaños.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-206">hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="9ecf8-207">Si Hola deseado tamaño está disponible, hello VM puede cambiarse desde un estado encendido, sin embargo, se reinicia durante la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-207">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="9ecf8-208">Si Hola tamaño deseado no está en el clúster actual hello, Hola VM necesidades puede producirse toobe cancela la asignación antes de hello cambiar el tamaño de operación.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-208">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="9ecf8-209">Tenga en cuenta que cuando Hola máquina virtual está encendida nuevo, se quitan todos los datos en disco temporal de Hola y la dirección IP pública Hola cambia a menos que se está usando una dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-209">Note, when hello VM is powered back on, any data on hello temp disk are removed, and hello public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="9ecf8-210">Estados de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-210">VM power states</span></span>

<span data-ttu-id="9ecf8-211">Una máquina virtual de Azure puede tener uno de muchos estados de energía.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="9ecf8-212">Este estado representa estado actual de Hola de hello VM desde la perspectiva de Hola de hipervisor de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-212">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="9ecf8-213">Estados de energía</span><span class="sxs-lookup"><span data-stu-id="9ecf8-213">Power states</span></span>

| <span data-ttu-id="9ecf8-214">Estado de energía</span><span class="sxs-lookup"><span data-stu-id="9ecf8-214">Power State</span></span> | <span data-ttu-id="9ecf8-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="9ecf8-215">Description</span></span>
|----|----|
| <span data-ttu-id="9ecf8-216">Iniciando</span><span class="sxs-lookup"><span data-stu-id="9ecf8-216">Starting</span></span> | <span data-ttu-id="9ecf8-217">Indica que se está iniciando la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-217">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="9ecf8-218">En ejecución</span><span class="sxs-lookup"><span data-stu-id="9ecf8-218">Running</span></span> | <span data-ttu-id="9ecf8-219">Indica que la máquina virtual Hola se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-219">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="9ecf8-220">Deteniéndose</span><span class="sxs-lookup"><span data-stu-id="9ecf8-220">Stopping</span></span> | <span data-ttu-id="9ecf8-221">Indica que la máquina virtual Hola se está deteniendo.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-221">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="9ecf8-222">Stopped</span><span class="sxs-lookup"><span data-stu-id="9ecf8-222">Stopped</span></span> | <span data-ttu-id="9ecf8-223">Indica que la máquina virtual Hola se ha detenido.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-223">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="9ecf8-224">Tenga en cuenta que máquinas virtuales en estado de hello detenido sigue acumulando cargos de proceso.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-224">Note that virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="9ecf8-225">Desasignando</span><span class="sxs-lookup"><span data-stu-id="9ecf8-225">Deallocating</span></span> | <span data-ttu-id="9ecf8-226">Indica que la máquina virtual Hola se está desasignando.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-226">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="9ecf8-227">Desasignado</span><span class="sxs-lookup"><span data-stu-id="9ecf8-227">Deallocated</span></span> | <span data-ttu-id="9ecf8-228">Indica que la máquina virtual Hola se quita completamente del hipervisor de hello pero sigue estando disponible en el plano de control de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-228">Indicates that hello virtual machine is completely removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="9ecf8-229">Máquinas virtuales en estado desasignado hello no acumulando cargos de proceso.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-229">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="9ecf8-230">Indica que el estado de energía de Hola de máquina virtual de hello es desconocido.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-230">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="9ecf8-231">Búsqueda del estado de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-231">Find power state</span></span>

<span data-ttu-id="9ecf8-232">estado de hello tooretrieve de una máquina virtual concreta, use hello [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) comando.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-232">tooretrieve hello state of a particular VM, use hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="9ecf8-233">Ser seguro toospecify un nombre válido para una máquina virtual y el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-233">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="9ecf8-234">Salida:</span><span class="sxs-lookup"><span data-stu-id="9ecf8-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="9ecf8-235">Tareas de administración</span><span class="sxs-lookup"><span data-stu-id="9ecf8-235">Management tasks</span></span>

<span data-ttu-id="9ecf8-236">Durante el ciclo de vida de Hola de una máquina virtual, puede desear toorun tareas de administración, como iniciar, detener o eliminar una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-236">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="9ecf8-237">Además, puede que desee toocreate tooautomate repetitivas o complejas tareas de secuencias de comandos.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-237">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="9ecf8-238">Uso de PowerShell de Azure, muchas tareas comunes de administración pueden realizarse desde la línea de comandos de Hola o en scripts.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-238">Using Azure PowerShell, many common management tasks can be run from hello command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="9ecf8-239">Detener una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-239">Stop virtual machine</span></span>

<span data-ttu-id="9ecf8-240">Detenga y desasigne una máquina virtual con [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="9ecf8-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="9ecf8-241">Si desea tookeep Hola virtual machine en un estado de aprovisionamiento, use el parámetro de - StayProvisioned de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-241">If you want tookeep hello virtual machine in a provisioned state, use hello -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="9ecf8-242">Iniciar una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="9ecf8-243">Eliminación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9ecf8-243">Delete resource group</span></span>

<span data-ttu-id="9ecf8-244">Al eliminar un grupo de recursos se eliminan también todos los recursos contenidos en el mismo.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="9ecf8-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9ecf8-245">Next steps</span></span>

<span data-ttu-id="9ecf8-246">En este tutorial, ha aprendido conceptos básicos sobre la creación y administración de máquinas virtuales. Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9ecf8-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9ecf8-247">Crear y conectar tooa VM</span><span class="sxs-lookup"><span data-stu-id="9ecf8-247">Create and connect tooa VM</span></span>
> * <span data-ttu-id="9ecf8-248">Seleccionar y usar imágenes de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9ecf8-248">Select and use VM images</span></span>
> * <span data-ttu-id="9ecf8-249">Ver y usar tamaños de una máquina virtual específicos</span><span class="sxs-lookup"><span data-stu-id="9ecf8-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="9ecf8-250">Cambiar el tamaño de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9ecf8-250">Resize a VM</span></span>
> * <span data-ttu-id="9ecf8-251">Ver y entender el estado de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9ecf8-251">View and understand VM state</span></span>

<span data-ttu-id="9ecf8-252">Avanzar toohello toolearn de tutorial siguiente acerca de los discos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9ecf8-252">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="9ecf8-253">Creación y administración de discos de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="9ecf8-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
