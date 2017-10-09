---
title: "aaaAzure redes virtuales y máquinas virtuales de Windows | Documentos de Microsoft"
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
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="46bf9-103">Administración de máquinas virtuales Windows y redes virtuales de Azure con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="46bf9-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="46bf9-104">Las máquinas virtuales de Azure utilizan las redes de Azure para la comunicación de red interna y externa.</span><span class="sxs-lookup"><span data-stu-id="46bf9-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="46bf9-105">En este tutorial, creará varias máquinas virtuales (VM) en una red virtual y configurará la conectividad de red entre ellas.</span><span class="sxs-lookup"><span data-stu-id="46bf9-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="46bf9-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="46bf9-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="46bf9-107">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="46bf9-107">Create a virtual network</span></span>
> * <span data-ttu-id="46bf9-108">Crear subredes de redes virtuales</span><span class="sxs-lookup"><span data-stu-id="46bf9-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="46bf9-109">Controlar el tráfico de red con grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="46bf9-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="46bf9-110">Ver reglas de tráfico en acción</span><span class="sxs-lookup"><span data-stu-id="46bf9-110">View traffic rules in action</span></span>

<span data-ttu-id="46bf9-111">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="46bf9-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="46bf9-112">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="46bf9-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="46bf9-113">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="46bf9-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="46bf9-114">Creación de una red virtual</span><span class="sxs-lookup"><span data-stu-id="46bf9-114">Create VNet</span></span>

<span data-ttu-id="46bf9-115">Una red virtual es una representación de su propia red en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="46bf9-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="46bf9-116">Una red virtual es un aislamiento lógico de hello nube de Azure dedicada tooyour suscripción.</span><span class="sxs-lookup"><span data-stu-id="46bf9-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="46bf9-117">Dentro de una red virtual, buscar subredes, las reglas para las conexiones desde toohello subredes de hello las máquinas virtuales y subredes de toothose de conectividad.</span><span class="sxs-lookup"><span data-stu-id="46bf9-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="46bf9-118">Para poder crear otros recursos de Azure, necesita toocreate un grupo de recursos con [AzureRmResourceGroup nuevo](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="46bf9-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="46bf9-119">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myRGNetwork* en hello *EastUS* ubicación:</span><span class="sxs-lookup"><span data-stu-id="46bf9-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="46bf9-120">Una subred es un recurso secundario de una red virtual que le ayudará a definir segmentos de espacios de direcciones dentro de un bloque CIDR mediante prefijos de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="46bf9-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="46bf9-121">Pueden agregarse NIC toosubnets y tooVMs conectados, proporcionar conectividad para diversas cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="46bf9-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="46bf9-122">Cree una subred con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="46bf9-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="46bf9-123">Crear una red virtual denominada *myVNet* con *myFrontendSubnet* con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="46bf9-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="46bf9-124">Creación de una máquina virtual de "front-end"</span><span class="sxs-lookup"><span data-stu-id="46bf9-124">Create front-end VM</span></span>

<span data-ttu-id="46bf9-125">Para la toocommunicate de una máquina virtual en una red virtual, se necesita una interfaz de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="46bf9-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="46bf9-126">Hola *myFrontendVM* se obtiene acceso desde Hola internet, por lo que también necesita una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="46bf9-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="46bf9-127">Cree una dirección IP pública con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="46bf9-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="46bf9-128">Cree una NIC con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="46bf9-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="46bf9-129">Establecer el nombre de usuario de Hola y la contraseña necesarios para la cuenta de administrador de hello en hello VM con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="46bf9-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="46bf9-130">Crear máquinas virtuales de hello con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [AzureRmVMOperatingSystem conjunto](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [conjunto AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [AzureRmVMNetworkInterface agregar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), y [nueva AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="46bf9-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

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

## <a name="install-web-server"></a><span data-ttu-id="46bf9-131">Instalación del servidor web</span><span class="sxs-lookup"><span data-stu-id="46bf9-131">Install web server</span></span>

<span data-ttu-id="46bf9-132">Puede instalar IIS en *myFrontendVM* usando una sesión del Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="46bf9-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="46bf9-133">Necesitará tooget Hola pública dirección IP de hello tooaccess VM se.</span><span class="sxs-lookup"><span data-stu-id="46bf9-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="46bf9-134">Puede obtener la dirección IP pública de Hola de *myFrontendVM* con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="46bf9-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="46bf9-135">Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIPAddress* creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="46bf9-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="46bf9-136">Tome nota de esta dirección IP para poder usarla en pasos futuros.</span><span class="sxs-lookup"><span data-stu-id="46bf9-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="46bf9-137">Siguiente Hola de uso del comando toocreate una sesión de escritorio remoto con *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="46bf9-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="46bf9-138">Reemplace  *<publicIPAddress>*  con la dirección de Hola que haya grabado previamente.</span><span class="sxs-lookup"><span data-stu-id="46bf9-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="46bf9-139">Cuando se le solicite, escriba credenciales de hello utilizadas cuando creó Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="46bf9-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="46bf9-140">Ahora que ha iniciado sesión demasiado*myFrontendVM*, puede utilizar una sola línea de PowerShell tooinstall IIS y permitir el tráfico de web de tooallow de regla de hello firewall local.</span><span class="sxs-lookup"><span data-stu-id="46bf9-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="46bf9-141">Abra un símbolo del sistema de PowerShell y ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="46bf9-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="46bf9-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) extensión de script personalizado de hello toorun que instala el servidor Web IIS de hello:</span><span class="sxs-lookup"><span data-stu-id="46bf9-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="46bf9-143">Ahora puede usar Hola IP dirección toobrowse toohello VM toosee Hola IIS sitio público.</span><span class="sxs-lookup"><span data-stu-id="46bf9-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![Sitio predeterminado de IIS](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="46bf9-145">Administración del tráfico interno</span><span class="sxs-lookup"><span data-stu-id="46bf9-145">Manage internal traffic</span></span>

<span data-ttu-id="46bf9-146">Un grupo de seguridad de red (NSG) contiene una lista de reglas de seguridad que permiten o deniegan tooa de tooresources conectado de tráfico de red red virtual.</span><span class="sxs-lookup"><span data-stu-id="46bf9-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="46bf9-147">Los NSG pueden ser toosubnets asociado o NIC individuales adjunta tooVMs.</span><span class="sxs-lookup"><span data-stu-id="46bf9-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="46bf9-148">Abrir o cerrar tooVMs de acceso a través de puertos se realiza utilizando las reglas NSG.</span><span class="sxs-lookup"><span data-stu-id="46bf9-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="46bf9-149">Al crear *myFrontendVM*, el puerto de entrada 3389 se abrió automáticamente para la conectividad RDP.</span><span class="sxs-lookup"><span data-stu-id="46bf9-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="46bf9-150">La comunicación interna de las máquinas virtuales puede configurarse con un NSG.</span><span class="sxs-lookup"><span data-stu-id="46bf9-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="46bf9-151">En esta sección, aprenderá cómo toocreate una subred adicional en Hola de red y asignar una tooallow de tooit NSG una conexión de *myFrontendVM* demasiado*myBackendVM* en el puerto 1433.</span><span class="sxs-lookup"><span data-stu-id="46bf9-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="46bf9-152">subred de Hello, a continuación, se asigna toohello VM cuando se crea.</span><span class="sxs-lookup"><span data-stu-id="46bf9-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="46bf9-153">Puede limitar el tráfico interno demasiado*myBackendVM* de sólo *myFrontendVM* mediante la creación de un NSG de subred de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="46bf9-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="46bf9-154">Hello en el ejemplo siguiente se crea una regla NSG denominada *myBackendNSGRule* con [AzureRmNetworkSecurityRuleConfig New](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="46bf9-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

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

<span data-ttu-id="46bf9-155">Agregue un nuevo grupo de seguridad de red denominado *myBackendNSG* con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="46bf9-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="46bf9-156">Adición de una subred de "back-end"</span><span class="sxs-lookup"><span data-stu-id="46bf9-156">Add back-end subnet</span></span>

<span data-ttu-id="46bf9-157">Agregar *myBackEndSubnet* demasiado*myVNet* con [AzureRmVirtualNetworkSubnetConfig agregar](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="46bf9-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

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

## <a name="create-back-end-vm"></a><span data-ttu-id="46bf9-158">Creación de la máquina virtual de "back-end"</span><span class="sxs-lookup"><span data-stu-id="46bf9-158">Create back-end VM</span></span>

<span data-ttu-id="46bf9-159">Hola Hola de manera más fácil toocreate que VM back-end es mediante una imagen de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="46bf9-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="46bf9-160">Este tutorial sólo crea Hola VM con el servidor de base de datos de hello, pero no proporciona información acerca del acceso a la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="46bf9-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="46bf9-161">Creación de *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="46bf9-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="46bf9-162">Establecer el nombre de usuario de Hola y la contraseña necesarios para la cuenta de administrador de hello en hello VM con Get-Credential:</span><span class="sxs-lookup"><span data-stu-id="46bf9-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="46bf9-163">Creación de *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="46bf9-163">Create *myBackendVM*:</span></span>

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

<span data-ttu-id="46bf9-164">imagen de Hola que se utiliza tiene instalado SQL Server, pero no se utiliza en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="46bf9-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="46bf9-165">Es tooshow incluye también cómo puede configurar el tráfico de web toohandle de una máquina virtual y una administración de base de datos de toohandle de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="46bf9-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46bf9-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46bf9-166">Next steps</span></span>

<span data-ttu-id="46bf9-167">En este tutorial, ha creado y protege las redes de Azure como máquinas toovirtual relacionados.</span><span class="sxs-lookup"><span data-stu-id="46bf9-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="46bf9-168">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="46bf9-168">Create a virtual network</span></span>
> * <span data-ttu-id="46bf9-169">Crear subredes de redes virtuales</span><span class="sxs-lookup"><span data-stu-id="46bf9-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="46bf9-170">Controlar el tráfico de red con grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="46bf9-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="46bf9-171">Ver reglas de tráfico en acción</span><span class="sxs-lookup"><span data-stu-id="46bf9-171">View traffic rules in action</span></span>

<span data-ttu-id="46bf9-172">Avanzar toohello toolearn de tutorial siguiente acerca de la supervisión para asegurar datos en máquinas virtuales mediante copia de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="46bf9-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="46bf9-173">.</span><span class="sxs-lookup"><span data-stu-id="46bf9-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="46bf9-174">Copia de seguridad de máquinas virtuales Windows en Azure</span><span class="sxs-lookup"><span data-stu-id="46bf9-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
