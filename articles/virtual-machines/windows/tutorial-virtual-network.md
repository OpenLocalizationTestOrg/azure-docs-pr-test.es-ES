---
title: "Máquinas virtuales Windows y redes virtuales de Azure | Microsoft Docs"
description: "Tutorial: Administración de máquinas virtuales Windows y redes virtuales de Azure con Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: c71c07f8ecd123a7e27848ba5043d46e315fcf03
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="01901-103">Administración de máquinas virtuales Windows y redes virtuales de Azure con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="01901-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="01901-104">Las máquinas virtuales de Azure utilizan las redes de Azure para la comunicación de red interna y externa.</span><span class="sxs-lookup"><span data-stu-id="01901-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="01901-105">En este tutorial, creará varias máquinas virtuales (VM) en una red virtual y configurará la conectividad de red entre ellas.</span><span class="sxs-lookup"><span data-stu-id="01901-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="01901-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="01901-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="01901-107">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="01901-107">Create a virtual network</span></span>
> * <span data-ttu-id="01901-108">Crear subredes de redes virtuales</span><span class="sxs-lookup"><span data-stu-id="01901-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="01901-109">Controlar el tráfico de red con grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="01901-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="01901-110">Ver reglas de tráfico en acción</span><span class="sxs-lookup"><span data-stu-id="01901-110">View traffic rules in action</span></span>

<span data-ttu-id="01901-111">Para realizar este tutorial es necesaria la versión 3.6 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="01901-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="01901-112">Ejecute ` Get-Module -ListAvailable AzureRM` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="01901-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="01901-113">Si necesita actualizarla, consulte [Instalación del módulo de Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="01901-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="01901-114">Creación de una red virtual</span><span class="sxs-lookup"><span data-stu-id="01901-114">Create VNet</span></span>

<span data-ttu-id="01901-115">Una red virtual es una representación de su propia red en la nube.</span><span class="sxs-lookup"><span data-stu-id="01901-115">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="01901-116">Una red virtual es un aislamiento lógico de la nube de Azure dedicada a su suscripción.</span><span class="sxs-lookup"><span data-stu-id="01901-116">A VNet is a logical isolation of the Azure cloud dedicated to your subscription.</span></span> <span data-ttu-id="01901-117">Dentro de una red virtual, hay subredes, reglas para la conectividad a esas subredes y conexiones desde las máquinas virtuales a las subredes.</span><span class="sxs-lookup"><span data-stu-id="01901-117">Within a VNet, you find subnets, rules for connectivity to those subnets, and connections from the VMs to the subnets.</span></span>

<span data-ttu-id="01901-118">Para poder crear otros recursos de Azure, tiene que crear un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="01901-118">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="01901-119">En el ejemplo siguiente, se crea un grupo de recursos denominado *myRGNetwork* en la ubicación *EastUS*:</span><span class="sxs-lookup"><span data-stu-id="01901-119">The following example creates a resource group named *myRGNetwork* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="01901-120">Una subred es un recurso secundario de una red virtual que le ayudará a definir segmentos de espacios de direcciones dentro de un bloque CIDR mediante prefijos de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="01901-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="01901-121">Las NIC pueden agregarse a subredes y conectarse a máquinas virtuales, lo cual le proporciona conectividad a varias cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="01901-121">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="01901-122">Cree una subred con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="01901-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="01901-123">Crear una red virtual denominada *myVNet* con *myFrontendSubnet* con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="01901-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="01901-124">Creación de una máquina virtual de "front-end"</span><span class="sxs-lookup"><span data-stu-id="01901-124">Create front-end VM</span></span>

<span data-ttu-id="01901-125">Una máquina virtual debe tener un interfaz de red virtual (NIC) para comunicarse en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="01901-125">For a VM to communicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="01901-126">A *myFrontendVM* se obtiene acceso desde Internet, por lo que también se necesita una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="01901-126">The *myFrontendVM* is accessed from the internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="01901-127">Cree una dirección IP pública con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="01901-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="01901-128">Cree una NIC con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="01901-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="01901-129">Establezca el nombre de usuario y la contraseña que se necesitan para la cuenta de administrador en la máquina virtual con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="01901-129">Set the username and password needed for the administrator account on the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="01901-130">Cree las máquinas virtuales con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) y [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="01901-130">Create the VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="01901-131">Instalación del servidor web</span><span class="sxs-lookup"><span data-stu-id="01901-131">Install web server</span></span>

<span data-ttu-id="01901-132">Puede instalar IIS en *myFrontendVM* usando una sesión del Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="01901-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="01901-133">Debe obtener la dirección IP pública de la máquina virtual para acceder a ella.</span><span class="sxs-lookup"><span data-stu-id="01901-133">You need to get the public IP address of the VM to access it.</span></span>

<span data-ttu-id="01901-134">Puede conseguir la dirección IP pública de *myFrontendVM* con [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="01901-134">You can get the public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="01901-135">En el ejemplo siguiente se obtiene la dirección IP de *myPublicIPAddress* que se ha creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="01901-135">The following example obtains the IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="01901-136">Tome nota de esta dirección IP para poder usarla en pasos futuros.</span><span class="sxs-lookup"><span data-stu-id="01901-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="01901-137">Utilice el comando siguiente para crear una sesión del Escritorio remoto con *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="01901-137">Use the following command to create a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="01901-138">Reemplace *<publicIPAddress>* por la dirección que haya registrado previamente.</span><span class="sxs-lookup"><span data-stu-id="01901-138">Replace *<publicIPAddress>* with the address that you previously recorded.</span></span> <span data-ttu-id="01901-139">Cuando se le solicite, escriba las credenciales usadas al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01901-139">When prompted, enter the credentials used when you created the VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="01901-140">Ahora que ha iniciado sesión en *myFrontendVM*, puede usar una sola línea de PowerShell para instalar IIS y habilitar la regla de firewall local para permitir el tráfico web.</span><span class="sxs-lookup"><span data-stu-id="01901-140">Now that you have logged in to *myFrontendVM*, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="01901-141">Abra una ventana de PowerShell y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="01901-141">Open a PowerShell prompt and run the following command:</span></span>

<span data-ttu-id="01901-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) para ejecutar la extensión de script personalizado que instala el servidor web de IIS:</span><span class="sxs-lookup"><span data-stu-id="01901-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) to run the custom script extension that installs the IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="01901-143">Ahora puede usar la dirección IP pública para ir a la máquina virtual con el fin de ver el sitio de IIS.</span><span class="sxs-lookup"><span data-stu-id="01901-143">Now you can use the public IP address to browse to the VM to see the IIS site.</span></span>

![Sitio predeterminado de IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="01901-145">Administración del tráfico interno</span><span class="sxs-lookup"><span data-stu-id="01901-145">Manage internal traffic</span></span>

<span data-ttu-id="01901-146">Un grupo de seguridad de red (NSG) contiene una lista de reglas de seguridad que permiten o deniegan el tráfico de red a recursos conectados a una red virtual.</span><span class="sxs-lookup"><span data-stu-id="01901-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to a VNet.</span></span> <span data-ttu-id="01901-147">Los NSG se pueden asociar a las subredes o a NIC individuales conectados a máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="01901-147">NSGs can be associated to subnets or individual NICs attached to VMs.</span></span> <span data-ttu-id="01901-148">La apertura o el cierre del acceso a las máquinas virtuales a través de puertos se realiza mediante las reglas de NSG.</span><span class="sxs-lookup"><span data-stu-id="01901-148">Opening or closing access to VMs through ports is done using NSG rules.</span></span> <span data-ttu-id="01901-149">Al crear *myFrontendVM*, el puerto de entrada 3389 se abrió automáticamente para la conectividad RDP.</span><span class="sxs-lookup"><span data-stu-id="01901-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="01901-150">La comunicación interna de las máquinas virtuales puede configurarse con un NSG.</span><span class="sxs-lookup"><span data-stu-id="01901-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="01901-151">En esta sección, aprenderá a crear una subred adicional en la red y asignar un NSG a ella para permitir una conexión de *myFrontendVM* a *myBackendVM* en el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="01901-151">In this section, you learn how to create an additional subnet in the network and assign an NSG to it to allow a connection from *myFrontendVM* to *myBackendVM* on port 1433.</span></span> <span data-ttu-id="01901-152">Después, la subred se asigna a la máquina virtual cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="01901-152">The subnet is then assigned to the VM when it is created.</span></span>

<span data-ttu-id="01901-153">Puede limitar el tráfico interno a *myBackendVM* solo desde *myFrontendVM* creando un NSG para la subred de "back-end".</span><span class="sxs-lookup"><span data-stu-id="01901-153">You can limit internal traffic to *myBackendVM* from only *myFrontendVM* by creating an NSG for the back-end subnet.</span></span> <span data-ttu-id="01901-154">En el ejemplo siguiente se crea una regla NSG denominada *myBackendNSGRule* con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="01901-154">The following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="01901-155">Agregue un nuevo grupo de seguridad de red denominado *myBackendNSG* con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="01901-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="01901-156">Adición de una subred de "back-end"</span><span class="sxs-lookup"><span data-stu-id="01901-156">Add back-end subnet</span></span>

<span data-ttu-id="01901-157">Adición de *myBackEndSubnet* a *myVNet* con [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="01901-157">Add *myBackEndSubnet* to *myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="01901-158">Creación de la máquina virtual de "back-end"</span><span class="sxs-lookup"><span data-stu-id="01901-158">Create back-end VM</span></span>

<span data-ttu-id="01901-159">La manera más fácil de crear la máquina virtual de "back-end "es utilizando una imagen de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="01901-159">The easiest way to create the back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="01901-160">Con este tutorial solo se crea la máquina virtual con el servidor de base de datos, pero no se proporciona información del acceso a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="01901-160">This tutorial only creates the VM with the database server, but doesn't provide information about accessing the database.</span></span>

<span data-ttu-id="01901-161">Creación de *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="01901-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="01901-162">Establezca el nombre de usuario y la contraseña que se necesitan para la cuenta de administrador en la máquina virtual con Get-Credential:</span><span class="sxs-lookup"><span data-stu-id="01901-162">Set the username and password needed for the administrator account on the VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="01901-163">Creación de *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="01901-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="01901-164">La imagen que se utiliza tiene instalado SQL Server, pero no se usa en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="01901-164">The image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="01901-165">Se incluye para mostrar cómo se pueden configurar una máquina virtual para controlar el tráfico de web y otra para controlar la administración de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="01901-165">It is included to show you how you can configure a VM to handle web traffic and a VM to handle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01901-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01901-166">Next steps</span></span>

<span data-ttu-id="01901-167">En este tutorial, ha creado y protegido redes de Azure cuando están relacionadas con máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="01901-167">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="01901-168">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="01901-168">Create a virtual network</span></span>
> * <span data-ttu-id="01901-169">Crear subredes de redes virtuales</span><span class="sxs-lookup"><span data-stu-id="01901-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="01901-170">Controlar el tráfico de red con grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="01901-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="01901-171">Ver reglas de tráfico en acción</span><span class="sxs-lookup"><span data-stu-id="01901-171">View traffic rules in action</span></span>

<span data-ttu-id="01901-172">Prosiga con el siguiente tutorial para aprender a supervisar la protección de datos en máquinas virtuales mediante Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="01901-172">Advance to the next tutorial to learn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="01901-173">.</span><span class="sxs-lookup"><span data-stu-id="01901-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01901-174">Copia de seguridad de máquinas virtuales Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="01901-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
