---
title: "aaaHow tooload equilibrar máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse hello Azure carga equilibrador toocreate una aplicación segura y de alta disponibilidad a través de tres máquinas virtuales de Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="40058-103">¿Cómo tooload equilibrar máquinas virtuales de Windows en Azure toocreate una aplicación de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="40058-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="40058-104">El equilibrio de carga proporciona un mayor nivel de disponibilidad al distribuir las solicitudes entrantes entre varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="40058-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="40058-105">En este tutorial, aprenderá acerca de los componentes diferentes Hola Hola Azure del equilibrador de carga que distribución el tráfico y proporcionan una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="40058-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="40058-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="40058-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="40058-107">Creación de un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="40058-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="40058-108">Creación del sondeo de estado de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="40058-109">Crear reglas de tráfico del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="40058-110">Usar la extensión de Script personalizado de hello toocreate un sitio IIS básico</span><span class="sxs-lookup"><span data-stu-id="40058-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="40058-111">Crear máquinas virtuales y adjuntar tooa equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="40058-112">Ver un equilibrador de carga en acción</span><span class="sxs-lookup"><span data-stu-id="40058-112">View a load balancer in action</span></span>
> * <span data-ttu-id="40058-113">Agregar y quitar las máquinas virtuales de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="40058-114">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="40058-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="40058-115">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="40058-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="40058-116">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="40058-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="40058-117">Información general sobre Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="40058-117">Azure load balancer overview</span></span>
<span data-ttu-id="40058-118">Un equilibrador de carga de Azure es un equilibrador de carga de nivel 4 (TCP, UDP) que proporciona una alta disponibilidad mediante la distribución del tráfico entrante entre máquinas virtuales con un estado correcto.</span><span class="sxs-lookup"><span data-stu-id="40058-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="40058-119">Un sondeo de estado de equilibrador de carga supervisa un puerto determinado en cada máquina virtual y sólo distribuye el tráfico tooan VM operativa.</span><span class="sxs-lookup"><span data-stu-id="40058-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="40058-120">Se define una configuración de IP de front-end que contiene una o varias direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="40058-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="40058-121">Esta configuración de IP de front-end permite que su toobe de aplicaciones y el equilibrador de carga puede tener acceso a través de Internet de Hola.</span><span class="sxs-lookup"><span data-stu-id="40058-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="40058-122">Máquinas virtuales se conectarán tooa equilibrador de carga con la tarjeta de interfaz de red virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="40058-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="40058-123">toodistribute tráfico toohello máquinas virtuales, un grupo de direcciones de back-end contiene direcciones IP de Hola Hola virtual (NIC) toohello conectados del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="40058-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="40058-124">flujo de hello toocontrol de tráfico, defina reglas de equilibrador de carga para determinados puertos y protocolos que se asignan tooyour las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="40058-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="40058-125">Creación del equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="40058-125">Create Azure load balancer</span></span>
<span data-ttu-id="40058-126">Esta sección detalla cómo puede crear y configurar cada componente Hola de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="40058-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="40058-127">Antes de poder crear el equilibrador de carga, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="40058-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="40058-128">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupLoadBalancer* en hello *EastUS* ubicación:</span><span class="sxs-lookup"><span data-stu-id="40058-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="40058-129">Crear una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="40058-129">Create a public IP address</span></span>
<span data-ttu-id="40058-130">tooaccess Hola de la aplicación en Internet, necesita una dirección IP pública para el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="40058-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="40058-131">Cree una dirección IP pública con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="40058-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="40058-132">Hello en el ejemplo siguiente se crea una dirección IP pública denominada *myPublicIP* en hello *myResourceGroupLoadBalancer* grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="40058-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="40058-133">Crear un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-133">Create a load balancer</span></span>
<span data-ttu-id="40058-134">Cree una dirección IP de front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="40058-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="40058-135">Hello en el ejemplo siguiente se crea una dirección IP de front-end denominada *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="40058-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="40058-136">Cree un grupo de direcciones de back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="40058-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="40058-137">Hello en el ejemplo siguiente se crea un grupo de direcciones de back-end denominado *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="40058-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="40058-138">A continuación, cree el equilibrador de carga de hello con [AzureRmLoadBalancer nuevo](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="40058-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="40058-139">Hello en el ejemplo siguiente se crea un equilibrador de carga con el nombre *myLoadBalancer* con hello *myPublicIP* dirección:</span><span class="sxs-lookup"><span data-stu-id="40058-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="40058-140">Creación de un sondeo de estado</span><span class="sxs-lookup"><span data-stu-id="40058-140">Create a health probe</span></span>
<span data-ttu-id="40058-141">tooallow Hola equilibrador toomonitor Hola estado de carga de la aplicación, utilice un sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="40058-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="40058-142">sondeo de estado de Hello dinámicamente agrega o quita las máquinas virtuales de rotación del equilibrador de carga de hello en función de sus comprobaciones de toohealth de respuesta.</span><span class="sxs-lookup"><span data-stu-id="40058-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="40058-143">De forma predeterminada, una máquina virtual se quita de la distribución de equilibrador de carga de hello después de dos errores consecutivos en intervalos de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="40058-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="40058-144">Cree un sondeo de estado en función de un protocolo o una página de comprobación de mantenimiento específica para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40058-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="40058-145">Hola siguiente ejemplo crea un sondeo TCP.</span><span class="sxs-lookup"><span data-stu-id="40058-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="40058-146">También se pueden crear sondeos HTTP personalizados para comprobaciones de estado más específicas.</span><span class="sxs-lookup"><span data-stu-id="40058-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="40058-147">Al utilizar un sondeo HTTP personalizado, debe crear página de comprobación de mantenimiento de hello, como *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="40058-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="40058-148">sondeo de Hello debe devolver un **HTTP 200 OK** respuesta para host Hola carga equilibrador tookeep Hola de rotación.</span><span class="sxs-lookup"><span data-stu-id="40058-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="40058-149">toocreate un sondeo de estado TCP, use [AzureRmLoadBalancerProbeConfig agregar](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="40058-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="40058-150">Hello en el ejemplo siguiente se crea un sondeo de estado denominado *myHealthProbe* que supervisa cada máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="40058-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="40058-151">Actualizar el equilibrador de carga de hello con [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="40058-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="40058-152">Creación de una regla de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-152">Create a load balancer rule</span></span>
<span data-ttu-id="40058-153">Una regla de equilibrador de carga es toodefine usado cómo tráfico es distribuida toohello máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="40058-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="40058-154">Definir configuración de IP front-end de hello para el tráfico entrante de Hola y Hola back-end grupo tooreceive Hola tráfico IP, junto con el origen de hello necesarios y el puerto de destino.</span><span class="sxs-lookup"><span data-stu-id="40058-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="40058-155">toomake seguro que solo las máquinas virtuales correcto reciban tráfico, también definir toouse de sondeo de estado de Hola.</span><span class="sxs-lookup"><span data-stu-id="40058-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="40058-156">Cree una regla del equilibrador de carga con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="40058-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="40058-157">Hello en el ejemplo siguiente se crea una regla de equilibrador de carga denominada *myLoadBalancerRule* y equilibra el tráfico en el puerto *80*:</span><span class="sxs-lookup"><span data-stu-id="40058-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

<span data-ttu-id="40058-158">Actualizar el equilibrador de carga de hello con [AzureRmLoadBalancer conjunto](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="40058-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="40058-159">Configuración de una red virtual</span><span class="sxs-lookup"><span data-stu-id="40058-159">Configure virtual network</span></span>
<span data-ttu-id="40058-160">Antes de implementar algunas máquinas virtuales y puede probar su equilibrador, crear Hola compatibilidad con recursos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="40058-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="40058-161">Para obtener más información sobre las redes virtuales, vea hello [administrar redes virtuales de Azure](tutorial-virtual-network.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="40058-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="40058-162">Crear recursos de red</span><span class="sxs-lookup"><span data-stu-id="40058-162">Create network resources</span></span>
<span data-ttu-id="40058-163">Cree una red virtual con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="40058-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="40058-164">Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* con *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="40058-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="40058-165">Cree una regla de grupo de seguridad de red con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) y después cree un grupo de seguridad de red con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="40058-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="40058-166">Agregar subred toohello grupo de seguridad de red de hello con [conjunto AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) y, a continuación, actualizar la red virtual de hello con [AzureRmVirtualNetwork conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="40058-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="40058-167">Hello en el ejemplo siguiente se crea una regla de grupo de seguridad de red denominada *myNetworkSecurityGroup* y lo aplica demasiado*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="40058-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="40058-168">Las NIC virtuales se crean con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="40058-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="40058-169">Hello en el ejemplo siguiente se crea tres NIC virtuales.</span><span class="sxs-lookup"><span data-stu-id="40058-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="40058-170">(Una NIC virtual para cada máquina virtual crea para la aplicación Hola siguiendo los pasos).</span><span class="sxs-lookup"><span data-stu-id="40058-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="40058-171">Puede crear NIC virtuales adicionales y las máquinas virtuales en cualquier momento y agregarlos toohello equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="40058-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a><span data-ttu-id="40058-172">Creación de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="40058-172">Create virtual machines</span></span>
<span data-ttu-id="40058-173">alta disponibilidad de Hola de tooimprove de la aplicación, coloque las máquinas virtuales en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="40058-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="40058-174">Cree un conjunto de disponibilidad con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="40058-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="40058-175">Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="40058-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="40058-176">Establecer un administrador username y password para máquinas virtuales de hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="40058-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="40058-177">Ahora puede crear máquinas virtuales de hello con [AzureRmVM nuevo](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="40058-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="40058-178">Hola siguiente ejemplo crea tres máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="40058-178">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

<span data-ttu-id="40058-179">Toma toocreate unos minutos y configurar todas las tres máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="40058-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="40058-180">Instalar IIS con la extensión de script personalizado</span><span class="sxs-lookup"><span data-stu-id="40058-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="40058-181">En un tutorial anterior en [cómo toocustomize una máquina virtual Windows](tutorial-automate-vm-deployment.md), ha aprendido cómo tooautomate personalización de máquina virtual con Hola extensión para ventanas de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="40058-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="40058-182">Puede usar hello mismo enfoque tooinstall y configure IIS en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="40058-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="40058-183">Use [AzureRmVMExtension conjunto](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Hola extensión de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="40058-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="40058-184">Hola se ejecuta la extensión `powershell Add-WindowsFeature Web-Server` tooinstall Hola actualizaciones hello servidor Web IIS y, a continuación, *Default.htm* página tooshow Hola hostname de hello VM:</span><span class="sxs-lookup"><span data-stu-id="40058-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a><span data-ttu-id="40058-185">Prueba del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-185">Test load balancer</span></span>
<span data-ttu-id="40058-186">Obtener dirección IP pública de Hola de un equilibrador de carga con [AzureRmPublicIPAddress Get](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="40058-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="40058-187">Hello en el ejemplo siguiente se obtiene la dirección IP de Hola para *myPublicIP* creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="40058-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="40058-188">A continuación, puede escribir la dirección IP pública hello en el Explorador de web tooa.</span><span class="sxs-lookup"><span data-stu-id="40058-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="40058-189">se muestra el sitio Web de Hello, incluyendo hostname Hola de hello VM ese equilibrador de carga de hello distribuye tooas de tráfico en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="40058-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Ejecución del sitio web de IIS](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="40058-191">equilibrador de carga de hello toosee distribuir el tráfico entre todas las tres VM que se ejecuta la aplicación, se puede forzar actualización el explorador web.</span><span class="sxs-lookup"><span data-stu-id="40058-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="40058-192">Agregar y quitar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="40058-192">Add and remove VMs</span></span>
<span data-ttu-id="40058-193">Puede que necesite tooperform mantenimiento en hello máquinas virtuales que ejecutan la aplicación, como la instalación de actualizaciones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="40058-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="40058-194">toodeal con un aumento del tráfico tooyour aplicación, puede que necesite tooadd máquinas virtuales adicionales.</span><span class="sxs-lookup"><span data-stu-id="40058-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="40058-195">Esta sección muestra cómo tooremove o agregar una máquina virtual desde el equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="40058-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="40058-196">Quitar una máquina virtual de equilibrador de carga de Hola</span><span class="sxs-lookup"><span data-stu-id="40058-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="40058-197">Obtener la tarjeta de interfaz de red de hello con [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), a continuación, el conjunto de hello *LoadBalancerBackendAddressPools* propiedad de Hola NIC virtual demasiado*$null*.</span><span class="sxs-lookup"><span data-stu-id="40058-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="40058-198">Por último, actualice NIC virtual. Hola:</span><span class="sxs-lookup"><span data-stu-id="40058-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="40058-199">equilibrador de carga de hello toosee distribuir el tráfico entre Hola otras dos máquinas virtuales que ejecutan la aplicación puede forzar actualización el explorador web.</span><span class="sxs-lookup"><span data-stu-id="40058-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="40058-200">Ahora puede realizar el mantenimiento en Hola de máquina virtual, como instalar actualizaciones del sistema operativo o realizar un reinicio de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="40058-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="40058-201">Agregar un equilibrador de carga de toohello VM</span><span class="sxs-lookup"><span data-stu-id="40058-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="40058-202">Después de realizar el mantenimiento de la máquina virtual, o si necesita capacidad de tooexpand, establezca hello *LoadBalancerBackendAddressPools* propiedad de hello virtual NIC toohello *BackendAddressPool* de [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="40058-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="40058-203">Obtener el equilibrador de carga de hello:</span><span class="sxs-lookup"><span data-stu-id="40058-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="40058-204">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="40058-204">Next steps</span></span>

<span data-ttu-id="40058-205">En este tutorial, ha creado un equilibrador de carga y adjunta tooit de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="40058-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="40058-206">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="40058-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="40058-207">Creación de un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="40058-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="40058-208">Creación del sondeo de estado de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="40058-209">Crear reglas de tráfico del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="40058-210">Usar la extensión de Script personalizado de hello toocreate un sitio IIS básico</span><span class="sxs-lookup"><span data-stu-id="40058-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="40058-211">Crear máquinas virtuales y adjuntar tooa equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="40058-212">Ver un equilibrador de carga en acción</span><span class="sxs-lookup"><span data-stu-id="40058-212">View a load balancer in action</span></span>
> * <span data-ttu-id="40058-213">Agregar y quitar las máquinas virtuales de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="40058-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="40058-214">Avanzar toohello siguiente tutorial toolearn cómo toomanage redes de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="40058-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="40058-215">Administración de máquinas y redes virtuales</span><span class="sxs-lookup"><span data-stu-id="40058-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
