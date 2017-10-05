---
title: "Cómo equilibrar la carga de máquinas virtuales de Windows en Azure | Microsoft Docs"
description: "Obtenga información sobre cómo usar Azure Load Balancer para crear una aplicación con alta disponibilidad y segura en tres máquinas virtuales de Windows"
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
ms.openlocfilehash: 6738d88d5a0430abaf3855dbf97a618e4c83617f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-windows-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="557a6-103">Cómo equilibrar la carga de máquinas virtuales de Windows en Azure para crear una aplicación de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="557a6-103">How to load balance Windows virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="557a6-104">El equilibrio de carga proporciona un mayor nivel de disponibilidad al distribuir las solicitudes entrantes entre varias máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="557a6-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="557a6-105">En este tutorial, aprenderá sobre los distintos componentes de Azure Load Balancer que distribuyen el tráfico y proporcionan una alta disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="557a6-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="557a6-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="557a6-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="557a6-107">Creación de un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="557a6-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="557a6-108">Creación del sondeo de estado de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="557a6-109">Crear reglas de tráfico del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="557a6-110">Usar la extensión de script personalizada para crear un sitio IIS básico</span><span class="sxs-lookup"><span data-stu-id="557a6-110">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="557a6-111">Crear máquinas virtuales y conectarlas a un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="557a6-112">Ver un equilibrador de carga en acción</span><span class="sxs-lookup"><span data-stu-id="557a6-112">View a load balancer in action</span></span>
> * <span data-ttu-id="557a6-113">Agregar y quitar las máquinas virtuales de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="557a6-114">Para realizar este tutorial es necesaria la versión 3.6 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="557a6-114">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="557a6-115">Ejecute ` Get-Module -ListAvailable AzureRM` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="557a6-115">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="557a6-116">Si necesita actualizarla, consulte [Instalación del módulo de Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="557a6-116">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="557a6-117">Información general sobre Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="557a6-117">Azure load balancer overview</span></span>
<span data-ttu-id="557a6-118">Un equilibrador de carga de Azure es un equilibrador de carga de nivel 4 (TCP, UDP) que proporciona una alta disponibilidad mediante la distribución del tráfico entrante entre máquinas virtuales con un estado correcto.</span><span class="sxs-lookup"><span data-stu-id="557a6-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="557a6-119">Un sondeo de estado de equilibrador de carga supervisa un puerto determinado en cada máquina virtual y solo distribuye tráfico a una máquina virtual operativa.</span><span class="sxs-lookup"><span data-stu-id="557a6-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="557a6-120">Se define una configuración de IP de front-end que contiene una o varias direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="557a6-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="557a6-121">Esta configuración de IP de front-end permite que el equilibrador de carga y las aplicaciones sean accesibles a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="557a6-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="557a6-122">Las máquinas virtuales se conectarán a un equilibrador de carga mediante su tarjeta de interfaz de red (NIC) virtual.</span><span class="sxs-lookup"><span data-stu-id="557a6-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="557a6-123">Para distribuir el tráfico a las máquinas virtuales, un grupo de direcciones de back-end contiene las direcciones IP de las tarjetas de interfaz de red (NIC) virtual conectadas al equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="557a6-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="557a6-124">Para controlar el flujo de tráfico, se definen reglas de equilibrador de carga para determinados puertos y protocolos que se asignan a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="557a6-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="557a6-125">Crear un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="557a6-125">Create Azure load balancer</span></span>
<span data-ttu-id="557a6-126">En esta sección se detalla cómo se puede crear y configurar cada componente del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="557a6-126">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="557a6-127">Antes de poder crear el equilibrador de carga, cree un grupo de recursos con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="557a6-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="557a6-128">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroupLoadBalancer* en la ubicación *EastUS*:</span><span class="sxs-lookup"><span data-stu-id="557a6-128">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="557a6-129">Crear una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="557a6-129">Create a public IP address</span></span>
<span data-ttu-id="557a6-130">Para obtener acceso a la aplicación en Internet, necesita una dirección IP pública para el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="557a6-130">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="557a6-131">Cree una dirección IP pública con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="557a6-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="557a6-132">En el ejemplo siguiente se crea una dirección IP pública denominada *myPublicIP* en el grupo de recursos *myResourceGroupLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="557a6-132">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="557a6-133">Crear un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-133">Create a load balancer</span></span>
<span data-ttu-id="557a6-134">Cree una dirección IP de front-end con [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="557a6-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="557a6-135">En el ejemplo siguiente se crea una dirección IP de front-end denominada *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="557a6-135">The following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="557a6-136">Cree un grupo de direcciones de back-end con [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="557a6-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="557a6-137">En el siguiente ejemplo se crea un grupo de direcciones de back-end denominado *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="557a6-137">The following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="557a6-138">Ahora, cree el equilibrador de carga con [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="557a6-138">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="557a6-139">En el ejemplo siguiente se crea un equilibrador de carga denominado *myLoadBalancer* utilizando la dirección *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="557a6-139">The following example creates a load balancer named *myLoadBalancer* using the *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="557a6-140">Creación de un sondeo de estado</span><span class="sxs-lookup"><span data-stu-id="557a6-140">Create a health probe</span></span>
<span data-ttu-id="557a6-141">Para permitir que el equilibrador de carga supervise el estado de la aplicación, utilice un sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="557a6-141">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="557a6-142">El sondeo de estado agrega o quita de forma dinámica las máquinas virtuales de la rotación del equilibrador de carga en base a su respuesta a las comprobaciones de estado.</span><span class="sxs-lookup"><span data-stu-id="557a6-142">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="557a6-143">De forma predeterminada, una máquina virtual se quita de la distribución del equilibrador de carga después de dos errores consecutivos en un intervalo de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="557a6-143">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="557a6-144">Cree un sondeo de estado en función de un protocolo o una página de comprobación de mantenimiento específica para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="557a6-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="557a6-145">En el ejemplo siguiente se crea un sondeo de TCP.</span><span class="sxs-lookup"><span data-stu-id="557a6-145">The following example creates a TCP probe.</span></span> <span data-ttu-id="557a6-146">También se pueden crear sondeos HTTP personalizados para comprobaciones de estado más específicas.</span><span class="sxs-lookup"><span data-stu-id="557a6-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="557a6-147">Al usar un sondeo HTTP personalizado, debe crear la página de comprobación de estado, por ejemplo *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="557a6-147">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="557a6-148">El sondeo debe devolver una respuesta **HTTP 200 OK** para que el equilibrador de carga mantenga el host en rotación.</span><span class="sxs-lookup"><span data-stu-id="557a6-148">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="557a6-149">Para crear un sondeo de estado TCP, se usa [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="557a6-149">To create a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="557a6-150">En el ejemplo siguiente se crea un sondeo de estado denominado *myHealthProbe* que supervisa cada máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="557a6-150">The following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="557a6-151">Actualice el equilibrador de carga con [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="557a6-151">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="557a6-152">Creación de una regla de equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-152">Create a load balancer rule</span></span>
<span data-ttu-id="557a6-153">Las reglas de equilibrador de carga se utilizan para definir cómo se distribuye el tráfico a las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="557a6-153">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="557a6-154">Se define la configuración de IP front-end para el tráfico entrante y el grupo IP de back-end para recibir el tráfico, junto con el puerto de origen y destino requeridos.</span><span class="sxs-lookup"><span data-stu-id="557a6-154">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="557a6-155">Para asegurarse de que solo las máquinas virtuales correctas reciban tráfico, también hay que definir el sondeo de estado que se va usar.</span><span class="sxs-lookup"><span data-stu-id="557a6-155">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="557a6-156">Cree una regla del equilibrador de carga con [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="557a6-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="557a6-157">En el ejemplo siguiente se crea una regla del equilibrador de carga denominada *myLoadBalancerRule* y se equilibra el tráfico en el puerto *80*:</span><span class="sxs-lookup"><span data-stu-id="557a6-157">The following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

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

<span data-ttu-id="557a6-158">Actualice el equilibrador de carga con [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="557a6-158">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="557a6-159">Configurar la red virtual</span><span class="sxs-lookup"><span data-stu-id="557a6-159">Configure virtual network</span></span>
<span data-ttu-id="557a6-160">Antes de implementar algunas máquinas virtuales y poder probar el equilibrador, cree los recursos de red virtual auxiliares.</span><span class="sxs-lookup"><span data-stu-id="557a6-160">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="557a6-161">Para más información sobre las redes virtuales, consulte el tutorial [Administración de Azure Virtual Networks](tutorial-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="557a6-161">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="557a6-162">Crear recursos de red</span><span class="sxs-lookup"><span data-stu-id="557a6-162">Create network resources</span></span>
<span data-ttu-id="557a6-163">Cree una red virtual con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="557a6-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="557a6-164">En el ejemplo siguiente se crea una red virtual denominada con una subred llamada *myVnet* con *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="557a6-164">The following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create the virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="557a6-165">Cree una regla de grupo de seguridad de red con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) y después cree un grupo de seguridad de red con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="557a6-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="557a6-166">Agregue el grupo de seguridad de red a la subred con [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) y, después, actualice la red virtual con [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="557a6-166">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="557a6-167">En el ejemplo siguiente, se crea una regla de grupo de seguridad de red denominada *myNetworkSecurityGroup* y se aplica a *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="557a6-167">The following example creates a network security group rule named *myNetworkSecurityGroup* and applies it to *mySubnet*:</span></span>

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

# Create the network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply the network security group to a subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update the virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="557a6-168">Las NIC virtuales se crean con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="557a6-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="557a6-169">En el ejemplo siguiente se crean tres NIC.</span><span class="sxs-lookup"><span data-stu-id="557a6-169">The following example creates three virtual NICs.</span></span> <span data-ttu-id="557a6-170">(Una NIC virtual para cada máquina virtual que cree para la aplicación en los pasos siguientes).</span><span class="sxs-lookup"><span data-stu-id="557a6-170">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="557a6-171">Puede crear NIC virtuales y máquinas virtuales adicionales en cualquier momento y agregarlas al equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="557a6-171">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="557a6-172">Crear máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="557a6-172">Create virtual machines</span></span>
<span data-ttu-id="557a6-173">Para mejorar la alta disponibilidad de la aplicación, coloque las máquinas virtuales en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="557a6-173">To improve the high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="557a6-174">Cree un conjunto de disponibilidad con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="557a6-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="557a6-175">En el ejemplo siguiente se crea un conjunto de disponibilidad denominado *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="557a6-175">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="557a6-176">Establezca un nombre de usuario de administrador y una contraseña para las máquinas virtuales con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="557a6-176">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="557a6-177">Ahora puede crear las máquinas virtuales con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="557a6-177">Now you can create the VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="557a6-178">En el ejemplo siguiente se crean tres máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="557a6-178">The following example creates three VMs:</span></span>

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

<span data-ttu-id="557a6-179">Se tarda unos minutos en crear y configurar las tres máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="557a6-179">It takes a few minutes to create and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="557a6-180">Instalar IIS con la extensión de script personalizado</span><span class="sxs-lookup"><span data-stu-id="557a6-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="557a6-181">En un tutorial anterior sobre [Cómo personalizar una máquina virtual de Windows](tutorial-automate-vm-deployment.md), aprendió a automatizar la personalización de máquinas virtuales con la extensión de script personalizado para Windows.</span><span class="sxs-lookup"><span data-stu-id="557a6-181">In a previous tutorial on [How to customize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with the Custom Script Extension for Windows.</span></span> <span data-ttu-id="557a6-182">Puede usar el mismo enfoque para instalar y configurar IIS en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="557a6-182">You can use the same approach to install and configure IIS on your VMs.</span></span>

<span data-ttu-id="557a6-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) para instalar la extensión de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="557a6-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="557a6-184">La extensión ejecuta `powershell Add-WindowsFeature Web-Server` para instalar el servidor web de IIS y después actualiza la página *Default.htm* para mostrar el nombre de host de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="557a6-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

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

## <a name="test-load-balancer"></a><span data-ttu-id="557a6-185">Prueba del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-185">Test load balancer</span></span>
<span data-ttu-id="557a6-186">Obtenga la dirección IP pública del equilibrador de carga con [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="557a6-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="557a6-187">En el ejemplo siguiente se obtiene la dirección IP de *myPublicIP* que se ha creado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="557a6-187">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="557a6-188">A continuación, puede escribir la dirección IP pública en un explorador web.</span><span class="sxs-lookup"><span data-stu-id="557a6-188">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="557a6-189">Se muestra el sitio web, incluido el nombre de host de la máquina virtual a la que el equilibrador de carga distribuye el tráfico como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="557a6-189">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![Ejecución del sitio web de IIS](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="557a6-191">Para ver cómo el equilibrador de carga distribuye el tráfico entre las tres máquinas virtuales que ejecutan la aplicación, puede realizar una actualización forzada del explorador web.</span><span class="sxs-lookup"><span data-stu-id="557a6-191">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="557a6-192">Agregar y quitar máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="557a6-192">Add and remove VMs</span></span>
<span data-ttu-id="557a6-193">Puede que tenga que realizar labores de mantenimiento de las máquinas virtuales que ejecutan la aplicación, como la instalación de actualizaciones del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="557a6-193">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="557a6-194">Para gestionar un aumento de tráfico a la aplicación, tiene que agregar más máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="557a6-194">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="557a6-195">Esta sección le muestra cómo quitar o agregar una máquina virtual desde el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="557a6-195">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="557a6-196">Eliminación de una máquina virtual del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-196">Remove a VM from the load balancer</span></span>
<span data-ttu-id="557a6-197">Obtenga la tarjeta de interfaz de red con [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface) y después establezca la propiedad *LoadBalancerBackendAddressPools* de la NIC virtual en *$null*.</span><span class="sxs-lookup"><span data-stu-id="557a6-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set the *LoadBalancerBackendAddressPools* property of the virtual NIC to *$null*.</span></span> <span data-ttu-id="557a6-198">Por último, actualice la NIC virtual:</span><span class="sxs-lookup"><span data-stu-id="557a6-198">Finally, update the virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="557a6-199">Para ver cómo el equilibrador de carga distribuye el tráfico entre las dos máquinas virtuales que quedan ejecutando la aplicación, puede realizar una actualización forzada del explorador web.</span><span class="sxs-lookup"><span data-stu-id="557a6-199">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="557a6-200">Ahora puede realizar tareas de mantenimiento en la máquina virtual, como instalar actualizaciones del sistema operativo o realizar un reinicio de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="557a6-200">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="557a6-201">Incorporación de una máquina virtual al equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-201">Add a VM to the load balancer</span></span>
<span data-ttu-id="557a6-202">Después de realizar el mantenimiento de la máquina virtual, o si necesita expandir la capacidad, establezca la propiedad *LoadBalancerBackendAddressPools* de la NIC virtual en el elemento *BackendAddressPool* de [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="557a6-202">After performing VM maintenance, or if you need to expand capacity, set the *LoadBalancerBackendAddressPools* property of the virtual NIC to the *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="557a6-203">Obtención del equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="557a6-203">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="557a6-204">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="557a6-204">Next steps</span></span>

<span data-ttu-id="557a6-205">En este tutorial, ha creado un equilibrador de carga y conectó máquinas virtuales a él.</span><span class="sxs-lookup"><span data-stu-id="557a6-205">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="557a6-206">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="557a6-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="557a6-207">Creación de un equilibrador de carga de Azure</span><span class="sxs-lookup"><span data-stu-id="557a6-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="557a6-208">Creación del sondeo de estado de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="557a6-209">Crear reglas de tráfico del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="557a6-210">Usar la extensión de script personalizada para crear un sitio IIS básico</span><span class="sxs-lookup"><span data-stu-id="557a6-210">Use the Custom Script Extension to create a basic IIS site</span></span>
> * <span data-ttu-id="557a6-211">Crear máquinas virtuales y conectarlas a un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-211">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="557a6-212">Ver un equilibrador de carga en acción</span><span class="sxs-lookup"><span data-stu-id="557a6-212">View a load balancer in action</span></span>
> * <span data-ttu-id="557a6-213">Agregar y quitar las máquinas virtuales de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="557a6-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="557a6-214">Avance al siguiente tutorial para aprender a administrar redes de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="557a6-214">Advance to the next tutorial to learn how to manage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="557a6-215">Administración de máquinas y redes virtuales</span><span class="sxs-lookup"><span data-stu-id="557a6-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
