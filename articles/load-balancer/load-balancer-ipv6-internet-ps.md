---
title: equilibrador de carga de aaaCreate un orientado a Internet de Azure con IPv6 - PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo el equilibrador con IPv6 mediante PowerShell para el Administrador de recursos de la carga de toocreate una conexión a Internet"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, Azure Load Balancer, pila doble, dirección ip pública, ipv6 nativo, móvil, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="8b3b0-104">Introducción a la creación de un equilibrador de carga orientado a Internet con IPv6 mediante el uso de PowerShell para Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8b3b0-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b3b0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b3b0-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="8b3b0-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="8b3b0-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="8b3b0-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="8b3b0-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="8b3b0-108">Azure Load Balancer es un equilibrador de carga de nivel 4 (TCP y UDP)</span><span class="sxs-lookup"><span data-stu-id="8b3b0-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="8b3b0-109">equilibrador de carga de Hello proporciona alta disponibilidad mediante la distribución de tráfico entrante entre instancias de servicio de estado de servicios en la nube o máquinas virtuales en un conjunto de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="8b3b0-110">Azure Load Balancer también pueden presentar prestar servicios en varios puertos, varias direcciones IP o ambos.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="8b3b0-111">Escenario de implementación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8b3b0-111">Example deployment scenario</span></span>

<span data-ttu-id="8b3b0-112">Hello siguiente diagrama ilustra Hola solución equilibrio de carga se implementa en este artículo.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-112">hello following diagram illustrates hello load balancing solution being deployed in this article.</span></span>

![Escenario del equilibrador de carga](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="8b3b0-114">En este escenario, creará hello Azure recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8b3b0-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="8b3b0-115">un equilibrador de carga orientado a Internet con una dirección IP pública IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="8b3b0-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="8b3b0-116">dos equilibrio reglas toomap Hola VIP toohello privados extremos públicos de carga</span><span class="sxs-lookup"><span data-stu-id="8b3b0-116">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>
* <span data-ttu-id="8b3b0-117">un conjunto de disponibilidad toothat contiene máquinas virtuales de hello dos</span><span class="sxs-lookup"><span data-stu-id="8b3b0-117">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="8b3b0-118">dos máquinas virtuales (VM)</span><span class="sxs-lookup"><span data-stu-id="8b3b0-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="8b3b0-119">una interfaz de red virtual para cada máquina virtual con las direcciones IPv4 e IPv6 asignadas</span><span class="sxs-lookup"><span data-stu-id="8b3b0-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a><span data-ttu-id="8b3b0-120">Implementar soluciones de hello mediante hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b3b0-120">Deploying hello solution using hello Azure PowerShell</span></span>

<span data-ttu-id="8b3b0-121">Hola pasos muestra cómo toocreate una conexión a Internet cargar equilibrador con el Administrador de recursos de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="8b3b0-122">Con el Administrador de recursos de Azure, cada recurso se haya creado y configurado de forma individual, a continuación, reunir toocreate un recurso.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-122">With Azure Resource Manager, each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="8b3b0-123">toodeploy un equilibrador de carga, se crea y configura Hola siguientes objetos:</span><span class="sxs-lookup"><span data-stu-id="8b3b0-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="8b3b0-124">Configuración de direcciones IP de front-end: contiene direcciones IP públicas para el tráfico de red entrante.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="8b3b0-125">Grupo de direcciones de back-end - contiene interfaces de red (NIC) de tráfico de red de tooreceive de máquinas virtuales de Hola Hola equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="8b3b0-126">Reglas de equilibrio de carga - contiene reglas de asignación de un puerto público en tooport de equilibrador de carga de hello en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="8b3b0-127">Reglas NAT de entrada: contiene las reglas de asignación de un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="8b3b0-128">Sondea: contiene toocheck disponibilidad de sondeos que se usan de mantenimiento de instancias de máquinas virtuales en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="8b3b0-129">Para más información, consulte [Compatibilidad de Azure Resource Manager con el equilibrador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8b3b0-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="8b3b0-130">Configurar PowerShell toouse el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="8b3b0-130">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="8b3b0-131">Asegúrese de que dispone de hello última versión de producción del módulo de Azure Resource Manager Hola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-131">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="8b3b0-132">Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="8b3b0-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="8b3b0-133">Escriba sus credenciales cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="8b3b0-134">Compruebe las suscripciones de hello para la cuenta de hello</span><span class="sxs-lookup"><span data-stu-id="8b3b0-134">Check hello subscriptions for hello account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="8b3b0-135">Elija qué su toouse de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-135">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="8b3b0-136">Creación de un grupo de recursos (omitir este paso si se utiliza un grupo de recursos existente)</span><span class="sxs-lookup"><span data-stu-id="8b3b0-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="8b3b0-137">Crear una red virtual y una dirección IP pública para el grupo de direcciones IP de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="8b3b0-137">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="8b3b0-138">Cree una red virtual con una subred</span><span class="sxs-lookup"><span data-stu-id="8b3b0-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="8b3b0-139">Crear recursos de (PIP) para el grupo de direcciones IP front-end de Hola de dirección IP pública de Azure.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-139">Create Azure Public IP address (PIP) resources for hello front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="8b3b0-140">equilibrador de carga de Hello usa la etiqueta de Hola de dominio de la dirección IP pública de hello como prefijo para su FQDN.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-140">hello load balancer uses hello domain label of hello public IP as prefix for its FQDN.</span></span> <span data-ttu-id="8b3b0-141">En este ejemplo, son nombres de dominio completos de hello *lbnrpipv4.westus.cloudapp.azure.com* y *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-141">In this example, hello FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="8b3b0-142">Creación de configuraciones de direcciones IP de front-end y un grupo de direcciones de back-end</span><span class="sxs-lookup"><span data-stu-id="8b3b0-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="8b3b0-143">Crear configuración de dirección front-end que utiliza direcciones IP públicas de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-143">Create front-end address configuration that uses hello Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="8b3b0-144">Cree grupos de direcciones de back-end</span><span class="sxs-lookup"><span data-stu-id="8b3b0-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="8b3b0-145">Crear reglas de equilibrador de carga, reglas NAT, un sondeo y un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="8b3b0-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="8b3b0-146">Este ejemplo crea Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="8b3b0-146">This example creates hello following items:</span></span>

* <span data-ttu-id="8b3b0-147">regla de NAT tootranslate todo el tráfico entrante en el puerto 443 tooport 4443</span><span class="sxs-lookup"><span data-stu-id="8b3b0-147">a NAT rule tootranslate all incoming traffic on port 443 tooport 4443</span></span>
* <span data-ttu-id="8b3b0-148">un toobalance de regla de equilibrador de carga todo el tráfico entrante en el puerto 80 tooport 80 en hello direcciones de grupo de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-148">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="8b3b0-149">una carga equilibrador regla tooallow RDP conexión toohello máquinas virtuales en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-149">a load balancer rule tooallow RDP connection toohello VMs on port 3389.</span></span>
* <span data-ttu-id="8b3b0-150">un estado de mantenimiento de sondeo regla toocheck hello en una página denominada *HealthProbe.aspx* o un servicio en el puerto 8080</span><span class="sxs-lookup"><span data-stu-id="8b3b0-150">a probe rule toocheck hello health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="8b3b0-151">un equilibrador de carga que usa todos estos objetos</span><span class="sxs-lookup"><span data-stu-id="8b3b0-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="8b3b0-152">Crear hello las reglas NAT.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-152">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="8b3b0-153">Cree un sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-153">Create a health probe.</span></span> <span data-ttu-id="8b3b0-154">Hay dos tooconfigure formas un sondeo:</span><span class="sxs-lookup"><span data-stu-id="8b3b0-154">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="8b3b0-155">Sondeo HTTP</span><span class="sxs-lookup"><span data-stu-id="8b3b0-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="8b3b0-156">o sondeo TCP</span><span class="sxs-lookup"><span data-stu-id="8b3b0-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="8b3b0-157">En este ejemplo, vamos hello toouse que sondeos de TCP.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-157">For this example, we are going toouse hello TCP probes.</span></span>

3. <span data-ttu-id="8b3b0-158">Cree una regla de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="8b3b0-159">Crear el equilibrador de carga de hello mediante objetos de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-159">Create hello load balancer using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a><span data-ttu-id="8b3b0-160">Crear NIC para hello máquinas virtuales de back-end</span><span class="sxs-lookup"><span data-stu-id="8b3b0-160">Create NICs for hello back-end VMs</span></span>

1. <span data-ttu-id="8b3b0-161">Obtener Hola red Virtual y subred de red Virtual, donde hello NIC necesita toobe creado.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-161">Get hello Virtual Network and Virtual Network Subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="8b3b0-162">Crear configuraciones de IP y NIC para las máquinas virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="8b3b0-162">Create IP configurations and NICs for hello VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a><span data-ttu-id="8b3b0-163">Crear máquinas virtuales y asignar Hola recién creado NIC</span><span class="sxs-lookup"><span data-stu-id="8b3b0-163">Create virtual machines and assign hello newly created NICs</span></span>

<span data-ttu-id="8b3b0-164">Para obtener más información sobre la creación de una máquina virtual, consulte [Creación de una máquina virtual de Windows con Resource Manager y Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8b3b0-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="8b3b0-165">Cree un conjunto de disponibilidad y una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="8b3b0-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="8b3b0-166">Cree cada máquina virtual y asigne Hola anterior creó NIC</span><span class="sxs-lookup"><span data-stu-id="8b3b0-166">Create each VM and assign hello previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a><span data-ttu-id="8b3b0-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8b3b0-167">Next steps</span></span>

[<span data-ttu-id="8b3b0-168">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="8b3b0-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="8b3b0-169">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="8b3b0-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8b3b0-170">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="8b3b0-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
