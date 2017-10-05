---
title: "Creación de un equilibrador de carga con conexión a Internet de Azure con IPv6: PowerShell | Microsoft Docs"
description: Aprenda a crear un equilibrador de carga orientado a Internet con IPv6 mediante el uso de PowerShell para Resource Manager
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
ms.openlocfilehash: 9d3cd37d3f2912301904b0a35f6fbc978d173079
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="be2c5-104">Introducción a la creación de un equilibrador de carga orientado a Internet con IPv6 mediante el uso de PowerShell para Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be2c5-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="be2c5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be2c5-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="be2c5-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="be2c5-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="be2c5-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="be2c5-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="be2c5-108">Azure Load Balancer es un equilibrador de carga de nivel 4 (TCP y UDP)</span><span class="sxs-lookup"><span data-stu-id="be2c5-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="be2c5-109">que distribuye proporcionando una alta disponibilidad el tráfico entrante entre las instancias de servicio correctas de los servicios en la nube o las máquinas virtuales de un conjunto de carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="be2c5-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="be2c5-110">Azure Load Balancer también pueden presentar prestar servicios en varios puertos, varias direcciones IP o ambos.</span><span class="sxs-lookup"><span data-stu-id="be2c5-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="be2c5-111">Escenario de implementación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="be2c5-111">Example deployment scenario</span></span>

<span data-ttu-id="be2c5-112">En el siguiente diagrama se ilustra la solución de equilibrio de carga que se implementa en este artículo.</span><span class="sxs-lookup"><span data-stu-id="be2c5-112">The following diagram illustrates the load balancing solution being deployed in this article.</span></span>

![Escenario del equilibrador de carga](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="be2c5-114">En este escenario creará los siguientes recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="be2c5-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="be2c5-115">un equilibrador de carga orientado a Internet con una dirección IP pública IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="be2c5-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="be2c5-116">dos reglas de equilibrio de carga para asignar las VIP públicas a los puntos de conexión privados</span><span class="sxs-lookup"><span data-stu-id="be2c5-116">two load balancing rules to map the public VIPs to the private endpoints</span></span>
* <span data-ttu-id="be2c5-117">un conjunto de disponibilidad con las dos máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="be2c5-117">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="be2c5-118">dos máquinas virtuales (VM)</span><span class="sxs-lookup"><span data-stu-id="be2c5-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="be2c5-119">una interfaz de red virtual para cada máquina virtual con las direcciones IPv4 e IPv6 asignadas</span><span class="sxs-lookup"><span data-stu-id="be2c5-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-the-solution-using-the-azure-powershell"></a><span data-ttu-id="be2c5-120">Implementación de la solución mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="be2c5-120">Deploying the solution using the Azure PowerShell</span></span>

<span data-ttu-id="be2c5-121">Los pasos siguientes muestran cómo crear un equilibrador de carga orientado a Internet mediante Azure Resource Manager con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be2c5-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="be2c5-122">Con Azure Resource Manager, cada recurso se crea y configura individualmente y, a continuación, se colocan juntos para crear un recurso.</span><span class="sxs-lookup"><span data-stu-id="be2c5-122">With Azure Resource Manager, each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="be2c5-123">Para implementar un equilibrador de carga, debe crear y configurar los siguientes objetos:</span><span class="sxs-lookup"><span data-stu-id="be2c5-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="be2c5-124">Configuración de direcciones IP de front-end: contiene direcciones IP públicas para el tráfico de red entrante.</span><span class="sxs-lookup"><span data-stu-id="be2c5-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="be2c5-125">Grupo de direcciones de back-end: contiene interfaces de red (NIC) para que las máquinas virtuales reciban tráfico de red del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="be2c5-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="be2c5-126">Reglas de equilibrio de carga: contiene reglas que asignan un puerto público en el equilibrador de carga al del grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="be2c5-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="be2c5-127">Reglas NAT de entrada: contiene reglas que asignan un puerto público en el equilibrador de carga a un puerto para una máquina virtual específica en el grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="be2c5-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="be2c5-128">Sondeos: contiene los sondeos de estado que se usan para comprobar la disponibilidad de las instancias de las máquinas virtuales del grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="be2c5-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="be2c5-129">Para más información, consulte [Compatibilidad de Azure Resource Manager con el equilibrador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="be2c5-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="be2c5-130">Configuración de PowerShell para usar Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be2c5-130">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="be2c5-131">Asegúrese de que tiene la última versión de producción del módulo Azure Resource Manager para PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be2c5-131">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="be2c5-132">Inicio de sesión en Azure</span><span class="sxs-lookup"><span data-stu-id="be2c5-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="be2c5-133">Escriba sus credenciales cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="be2c5-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="be2c5-134">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="be2c5-134">Check the subscriptions for the account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="be2c5-135">Elección de la suscripción de Azure que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="be2c5-135">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="be2c5-136">Creación de un grupo de recursos (omitir este paso si se utiliza un grupo de recursos existente)</span><span class="sxs-lookup"><span data-stu-id="be2c5-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="be2c5-137">Creación de una red virtual y una dirección IP pública para el grupo de direcciones IP front-end</span><span class="sxs-lookup"><span data-stu-id="be2c5-137">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="be2c5-138">Cree una red virtual con una subred</span><span class="sxs-lookup"><span data-stu-id="be2c5-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="be2c5-139">Cree recursos de dirección IP pública (PIP) de Azure para el grupo de direcciones IP de front-end</span><span class="sxs-lookup"><span data-stu-id="be2c5-139">Create Azure Public IP address (PIP) resources for the front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="be2c5-140">El equilibrador de carga usa la etiqueta de dominio de la dirección IP pública como prefijo para su FQDN.</span><span class="sxs-lookup"><span data-stu-id="be2c5-140">The load balancer uses the domain label of the public IP as prefix for its FQDN.</span></span> <span data-ttu-id="be2c5-141">En este ejemplo, los FQDN son *lbnrpipv4.westus.cloudapp.azure.com* y *lbnrpipv6.westus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="be2c5-141">In this example, the FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="be2c5-142">Creación de configuraciones de direcciones IP de front-end y un grupo de direcciones de back-end</span><span class="sxs-lookup"><span data-stu-id="be2c5-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="be2c5-143">Cree la configuración de direcciones de front-end que usa las direcciones IP públicas que ha creado</span><span class="sxs-lookup"><span data-stu-id="be2c5-143">Create front-end address configuration that uses the Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="be2c5-144">Cree grupos de direcciones de back-end</span><span class="sxs-lookup"><span data-stu-id="be2c5-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="be2c5-145">Crear reglas de equilibrador de carga, reglas NAT, un sondeo y un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="be2c5-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="be2c5-146">En este ejemplo se crean los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="be2c5-146">This example creates the following items:</span></span>

* <span data-ttu-id="be2c5-147">una regla NAT para trasladar todo el tráfico entrante del puerto 443 al puerto 4443</span><span class="sxs-lookup"><span data-stu-id="be2c5-147">a NAT rule to translate all incoming traffic on port 443 to port 4443</span></span>
* <span data-ttu-id="be2c5-148">Una regla de equilibrador de carga para equilibrar todo el tráfico entrante del puerto 80 al puerto 80 en las direcciones del grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="be2c5-148">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="be2c5-149">Una regla de equilibrador de carga para permitir la conexión RDP a las máquinas virtuales en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="be2c5-149">a load balancer rule to allow RDP connection to the VMs on port 3389.</span></span>
* <span data-ttu-id="be2c5-150">una regla de sondeo para comprobar el estado de mantenimiento en una página llamada *HealthProbe.aspx* o un servicio en el puerto 8080</span><span class="sxs-lookup"><span data-stu-id="be2c5-150">a probe rule to check the health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="be2c5-151">un equilibrador de carga que usa todos estos objetos</span><span class="sxs-lookup"><span data-stu-id="be2c5-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="be2c5-152">Cree las reglas NAT.</span><span class="sxs-lookup"><span data-stu-id="be2c5-152">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="be2c5-153">Cree un sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="be2c5-153">Create a health probe.</span></span> <span data-ttu-id="be2c5-154">Hay dos formas de configurar un sondeo:</span><span class="sxs-lookup"><span data-stu-id="be2c5-154">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="be2c5-155">Sondeo HTTP</span><span class="sxs-lookup"><span data-stu-id="be2c5-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="be2c5-156">o sondeo TCP</span><span class="sxs-lookup"><span data-stu-id="be2c5-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="be2c5-157">En este ejemplo, vamos a usar los sondeos TCP.</span><span class="sxs-lookup"><span data-stu-id="be2c5-157">For this example, we are going to use the TCP probes.</span></span>

3. <span data-ttu-id="be2c5-158">Cree una regla de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="be2c5-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="be2c5-159">Cree el equilibrador de carga mediante los objetos creados anteriormente</span><span class="sxs-lookup"><span data-stu-id="be2c5-159">Create the load balancer using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-the-back-end-vms"></a><span data-ttu-id="be2c5-160">Creación de tarjetas NIC para las máquinas virtuales de back-end</span><span class="sxs-lookup"><span data-stu-id="be2c5-160">Create NICs for the back-end VMs</span></span>

1. <span data-ttu-id="be2c5-161">Obtenga la red virtual y la subred de red virtual, donde deben crearse las NIC.</span><span class="sxs-lookup"><span data-stu-id="be2c5-161">Get the Virtual Network and Virtual Network Subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="be2c5-162">Cree configuraciones de direcciones IP y tarjetas NIC para las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="be2c5-162">Create IP configurations and NICs for the VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-the-newly-created-nics"></a><span data-ttu-id="be2c5-163">Creación de máquinas virtuales y asignación de las tarjetas NIC recién creadas</span><span class="sxs-lookup"><span data-stu-id="be2c5-163">Create virtual machines and assign the newly created NICs</span></span>

<span data-ttu-id="be2c5-164">Para obtener más información sobre la creación de una máquina virtual, consulte [Creación de una máquina virtual de Windows con Resource Manager y Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="be2c5-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="be2c5-165">Cree un conjunto de disponibilidad y una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="be2c5-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="be2c5-166">Cree cada máquina virtual y asigne las tarjetas NIC creadas con anterioridad</span><span class="sxs-lookup"><span data-stu-id="be2c5-166">Create each VM and assign the previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type the username and password of the local administrator account."

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

## <a name="next-steps"></a><span data-ttu-id="be2c5-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be2c5-167">Next steps</span></span>

[<span data-ttu-id="be2c5-168">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="be2c5-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="be2c5-169">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="be2c5-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="be2c5-170">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="be2c5-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
