---
title: "Configuración de conexiones de ExpressRoute y VPN de sitio a sitio coexistentes: Resource Manager: Azure | Microsoft Docs"
description: "Este artículo le guiará en la configuración de conexiones ExpressRoute y VPN de sitio a sitio que puedan coexistir en el modelo de implementación de Resource Manager."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: b29147a37f9a90fc80e16b350ac9b91daac1d7f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="57b2c-103">Configuración de conexiones coexistentes de ExpressRoute de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="57b2c-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57b2c-104">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="57b2c-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="57b2c-105">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="57b2c-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="57b2c-106">La configuración de las conexiones coexistentes VPN de sitio a sitio y ExpressRoute tiene varias ventajas.</span><span class="sxs-lookup"><span data-stu-id="57b2c-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="57b2c-107">Puede configurar una VPN de sitio a sitio como una ruta de acceso seguro de conmutación por error para ExressRoute, o bien usar unas VPN de sitio a sitio para conectarse a sitios que no están conectados mediante ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="57b2c-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="57b2c-108">En este artículo se tratan los pasos para configurar ambos escenarios.</span><span class="sxs-lookup"><span data-stu-id="57b2c-108">We cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="57b2c-109">Este artículo se aplica al modelo de implementación de Resource Manager y utiliza PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57b2c-109">This article applies to the Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="57b2c-110">Esta configuración no está disponible en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="57b2c-110">This configuration is not available in the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="57b2c-111">Los circuitos ExpressRoute deben configurarse previamente antes de seguir las instrucciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="57b2c-111">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="57b2c-112">Asegúrese de que ha seguido las instrucciones para [crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y [configurar el enrutamiento](expressroute-howto-routing-arm.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="57b2c-112">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="57b2c-113">Límites y limitaciones</span><span class="sxs-lookup"><span data-stu-id="57b2c-113">Limits and limitations</span></span>
* <span data-ttu-id="57b2c-114">**No se admite el enrutamiento transitorio.**</span><span class="sxs-lookup"><span data-stu-id="57b2c-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="57b2c-115">No se puede realizar un enrutamiento (a través de Azure) entre una red local conectada a través de una VPN sitio a sitio y una red local conectada a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="57b2c-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="57b2c-116">**No se admite la puerta de enlace de la SKU de nivel Básico.**</span><span class="sxs-lookup"><span data-stu-id="57b2c-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="57b2c-117">Debe utilizar una puerta de enlace de la SKU que no sea de nivel Básico tanto para la [puerta de enlace de ExpressRoute](expressroute-about-virtual-network-gateways.md) como para la [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="57b2c-117">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="57b2c-118">**Solo se admite la VPN Gateway basada en rutas.**</span><span class="sxs-lookup"><span data-stu-id="57b2c-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="57b2c-119">Debe usar una [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) basada en rutas.</span><span class="sxs-lookup"><span data-stu-id="57b2c-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="57b2c-120">**Se debe configurar una ruta estática para VPN Gateway.**</span><span class="sxs-lookup"><span data-stu-id="57b2c-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="57b2c-121">Si la red local está conectada tanto a ExpressRoute como a una VPN de sitio a sitio, debe tener configurada una ruta estática en la red local para enrutar la conexión VPN de sitio a sitio a la red pública de Internet.</span><span class="sxs-lookup"><span data-stu-id="57b2c-121">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="57b2c-122">**Primero es preciso configurar la puerta de enlace de ExpressRoute y vincularla a un circuito.**</span><span class="sxs-lookup"><span data-stu-id="57b2c-122">**ExpressRoute gateway must be configured first and linked to a circuit.**</span></span> <span data-ttu-id="57b2c-123">Debe crear la puerta de enlace de ExpressRoute y vincularla a un circuito antes de agregar la puerta de enlace de VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="57b2c-123">You must create the ExpressRoute gateway first and link it to a circuit before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="57b2c-124">Diseños de configuración</span><span class="sxs-lookup"><span data-stu-id="57b2c-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="57b2c-125">Configuración de una VPN de sitio a sitio como una ruta de acceso de conmutación por error para ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="57b2c-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="57b2c-126">Puede configurar una conexión VPN de sitio a sitio como una copia de seguridad para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="57b2c-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="57b2c-127">Esto se aplica únicamente a las redes virtuales vinculadas a la ruta de acceso de emparejamiento privada de Azure.</span><span class="sxs-lookup"><span data-stu-id="57b2c-127">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="57b2c-128">No hay ninguna solución de conmutación por error basada en VPN para servicios accesibles a través de emparejamientos de Microsoft y públicos de Azure.</span><span class="sxs-lookup"><span data-stu-id="57b2c-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="57b2c-129">El circuito ExpressRoute siempre es el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="57b2c-129">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="57b2c-130">Los datos fluyen a través de la ruta de acceso de la VPN de sitio a sitio solo si se produce un error en el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="57b2c-130">Data flows through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="57b2c-131">Si bien se prefiere el circuito ExpressRoute a la VPN de sitio a sitio cuando ambas rutas son las mismas, Azure utilizará la coincidencia de prefijo más larga para elegir la ruta hacia el destino del paquete.</span><span class="sxs-lookup"><span data-stu-id="57b2c-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![Coexistencia](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="57b2c-133">Configuración de una VPN de sitio a sitio para conectarse a sitios no conectados mediante ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="57b2c-133">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="57b2c-134">Puede configurar la red para sitios que se conectan directamente a Azure mediante una VPN de sitio a sitio y otros que se conectan a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="57b2c-134">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexistencia](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="57b2c-136">No se puede configurar una red virtual como un enrutador de tránsito.</span><span class="sxs-lookup"><span data-stu-id="57b2c-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="57b2c-137">Selección de los pasos a seguir</span><span class="sxs-lookup"><span data-stu-id="57b2c-137">Selecting the steps to use</span></span>
<span data-ttu-id="57b2c-138">Hay dos conjuntos diferentes de procedimientos que puede elegir.</span><span class="sxs-lookup"><span data-stu-id="57b2c-138">There are two different sets of procedures to choose from.</span></span> <span data-ttu-id="57b2c-139">El procedimiento de configuración que seleccione depende de si ya tiene una red virtual existente a la que quiere conectarse o si desea crear una nueva.</span><span class="sxs-lookup"><span data-stu-id="57b2c-139">The configuration procedure that you select depends on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="57b2c-140">No tengo una red virtual y necesito crear una.</span><span class="sxs-lookup"><span data-stu-id="57b2c-140">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="57b2c-141">Si aún no tiene una red virtual, este procedimiento le guía en la creación de una nueva red virtual mediante el modelo de implementación de Resource Manager y la creación de nuevas conexiones VPN de sitio a sitio y ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="57b2c-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="57b2c-142">Para configurar una red virtual, siga los pasos que se describen en [Creación de una nueva red virtual y conexiones coexistentes](#new).</span><span class="sxs-lookup"><span data-stu-id="57b2c-142">To configure a virtual network, follow the steps in [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="57b2c-143">Ya tengo una red virtual del modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="57b2c-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="57b2c-144">Puede que ya tenga una red virtual con una conexión VPN de sitio a sitio o una conexión ExpressRoute existentes.</span><span class="sxs-lookup"><span data-stu-id="57b2c-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="57b2c-145">La sección [Configuración de conexiones coexistentes para una red virtual existente](#add) le guía en la eliminación de la puerta de enlace y la creación de nuevas conexiones VPN de sitio a sitio y ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="57b2c-145">The [To configure coexisting connections for an already existing VNet](#add) section walks you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="57b2c-146">Al crear las nuevas conexiones, se deben completar los pasos en un orden específico.</span><span class="sxs-lookup"><span data-stu-id="57b2c-146">When creating the new connections, the steps must be completed in a specific order.</span></span> <span data-ttu-id="57b2c-147">No utilice las instrucciones que aparecen en otros artículos para crear puertas de enlace y conexiones.</span><span class="sxs-lookup"><span data-stu-id="57b2c-147">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="57b2c-148">En este procedimiento, para crear conexiones que puedan coexistir, tiene que eliminar la puerta de enlace y luego configurar nuevas puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="57b2c-148">In this procedure, creating connections that can coexist requires you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="57b2c-149">Tendrá tiempo de inactividad para las conexiones entre entornos mientras elimina y vuelve a crear la puerta de enlace y las conexiones, pero no necesitará migrar las máquinas virtuales o servicios a una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="57b2c-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="57b2c-150">Las máquinas virtuales y los servicios podrán seguir comunicándose con el exterior a través del equilibrador de carga mientras configura la puerta de enlace si están configurados para ello.</span><span class="sxs-lookup"><span data-stu-id="57b2c-150">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="57b2c-151"><a name="new"></a>Creación de una nueva red virtual y conexiones coexistentes</span><span class="sxs-lookup"><span data-stu-id="57b2c-151"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="57b2c-152">Este procedimiento le guía en la creación de una red virtual y conexiones de sitio a sitio y ExpressRoute que coexisten.</span><span class="sxs-lookup"><span data-stu-id="57b2c-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="57b2c-153">Instale la versión más reciente de los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57b2c-153">Install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="57b2c-154">Para obtener información acerca de cómo instalar los cmdlets, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="57b2c-154">For information about installing the cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="57b2c-155">Los cmdlets que se usan en esta configuración pueden ser ligeramente diferentes de aquellos con los que podría estar familiarizado.</span><span class="sxs-lookup"><span data-stu-id="57b2c-155">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="57b2c-156">Asegúrese de usar los cmdlets especificados en estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="57b2c-156">Be sure to use the cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="57b2c-157">Inicie sesión en su cuenta y configure el entorno.</span><span class="sxs-lookup"><span data-stu-id="57b2c-157">Log in to your account and set up the environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="57b2c-158">Cree una red virtual, incluida la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="57b2c-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="57b2c-159">Para más información sobre la configuración de la red virtual, consulte [Creación de una red virtual usando PowerShell](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="57b2c-159">For more information about the virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="57b2c-160">La subred de puerta de enlace debe ser /27 o un prefijo más corto (por ejemplo, /26 o /25).</span><span class="sxs-lookup"><span data-stu-id="57b2c-160">The Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="57b2c-161">Cree una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="57b2c-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="57b2c-162">Agregue subredes.</span><span class="sxs-lookup"><span data-stu-id="57b2c-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="57b2c-163">Guarde la configuración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="57b2c-163">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="57b2c-164"><a name="gw"></a>Cree una puerta de enlace de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="57b2c-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="57b2c-165">Para más información sobre la configuración de la puerta de enlace de ExpressRoute, consulte [Adición de una puerta de enlace de VPN a una red virtual de Resource Manager para una configuración de ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="57b2c-165">For more information about the ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="57b2c-166">El valor de GatewaySKU debe ser *Standard*, *HighPerformance* o *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="57b2c-166">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="57b2c-167">Vincule la puerta de enlace de ExpressRoute al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="57b2c-167">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="57b2c-168">Una vez completado este paso, se ha establecido la conexión entre su red local y Azure a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="57b2c-168">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="57b2c-169">Para más información sobre la operación de vinculación, consulte [Vinculación de redes virtuales a circuitos ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="57b2c-169">For more information about the link operation, see [Link VNets to ExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="57b2c-170"><a name="vpngw"></a>A continuación, cree la puerta de enlace de la VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="57b2c-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="57b2c-171">Para más información sobre la configuración de VPN Gateway, consulte [Creación de una red virtual con una conexión de sitio a sitio mediante PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="57b2c-171">For more information about the VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="57b2c-172">El valor de GatewaySKU debe ser *Standard*, *HighPerformance* o *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="57b2c-172">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="57b2c-173">El valor de VpnType debe ser *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="57b2c-173">The VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="57b2c-174">Azure VPN Gateway admite el protocolo de enrutamiento de BGP.</span><span class="sxs-lookup"><span data-stu-id="57b2c-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="57b2c-175">Para especificar el ASN (número AS) de la red virtual, agregue el modificador - Asn al siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="57b2c-175">You can specify ASN (AS Number) for that Virtual Network by adding the -Asn switch in the following command.</span></span> <span data-ttu-id="57b2c-176">Si no se especifica ese parámetro, el valor predeterminado del número AS será 65515.</span><span class="sxs-lookup"><span data-stu-id="57b2c-176">Not specifying that parameter will default to AS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="57b2c-177">Puede buscar el IP de emparejamiento BGP y el número de AS que Azure usa para VPN Gateway en $azureVpn.BgpSettings.BgpPeeringAddress y $azureVpn.BgpSettings.Asn de BGP.</span><span class="sxs-lookup"><span data-stu-id="57b2c-177">You can find the BGP peering IP and the AS number that Azure uses for the VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="57b2c-178">Para más información, consulte [Configuración de BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) para Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="57b2c-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="57b2c-179">Cree una entidad de puerta de enlace de VPN de sitio local.</span><span class="sxs-lookup"><span data-stu-id="57b2c-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="57b2c-180">Este comando no configura la puerta de enlace de VPN local.</span><span class="sxs-lookup"><span data-stu-id="57b2c-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="57b2c-181">En su lugar, permite proporcionar la configuración de puerta de enlace local, como la dirección IP pública y el espacio de direcciones local, para que la puerta de enlace de VPN de Azure pueda conectarse a ella.</span><span class="sxs-lookup"><span data-stu-id="57b2c-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
    <span data-ttu-id="57b2c-182">Si el dispositivo VPN local solo admite enrutamiento estático, las rutas estáticas se pueden configurar como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="57b2c-182">If your local VPN device only supports static routing, you can configure the static routes in the following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="57b2c-183">Si el dispositivo VPN local admite el BGP y desea habilitar el enrutamiento dinámico, es preciso que conozca la IP de emparejamiento BGP y el número de AS que usa el dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="57b2c-183">If your local VPN device supports the BGP and you want to enable dynamic routing, you need to know the BGP peering IP and the AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for the BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="57b2c-184">Configure el dispositivo VPN local para que se conecte a la nueva puerta de enlace de VPN de Azure.</span><span class="sxs-lookup"><span data-stu-id="57b2c-184">Configure your local VPN device to connect to the new Azure VPN gateway.</span></span> <span data-ttu-id="57b2c-185">Para obtener más información sobre la configuración del dispositivo VPN, vea [Configuración de dispositivos VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="57b2c-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="57b2c-186">Vincule la puerta de enlace de VPN sitio a sitio en Azure a la puerta de enlace local.</span><span class="sxs-lookup"><span data-stu-id="57b2c-186">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="57b2c-187"><a name="add"></a>Para configurar conexiones coexistentes para una red virtual ya existente</span><span class="sxs-lookup"><span data-stu-id="57b2c-187"><a name="add"></a>To configure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="57b2c-188">Si ya tiene una red virtual, compruebe el tamaño de la subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="57b2c-188">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="57b2c-189">Si la subred de puerta de enlace es /28 o /29, primero debe eliminar la puerta de enlace de red virtual y aumentar el tamaño de la subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="57b2c-189">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="57b2c-190">Los pasos de esta sección le muestran cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="57b2c-190">The steps in this section show you how to do that.</span></span>

<span data-ttu-id="57b2c-191">Si la puerta de enlace es /27 o mayor y la red virtual está conectada a través de ExpressRoute, puede omitir los pasos siguientes y continuar con ["Paso 6: Creación una puerta de enlace VPN de sitio a sitio"](#vpngw) en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="57b2c-191">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="57b2c-192">Cuando elimine la puerta de enlace existente, las instalaciones locales perderán la conexión a la red virtual mientras trabaja en esta configuración.</span><span class="sxs-lookup"><span data-stu-id="57b2c-192">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="57b2c-193">Deberá instalar la versión más reciente de los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57b2c-193">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="57b2c-194">Para más información sobre cómo instalar los cmdlets, consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="57b2c-194">For more information about installing cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="57b2c-195">Los cmdlets que se usan en esta configuración pueden ser ligeramente diferentes de aquellos con los que podría estar familiarizado.</span><span class="sxs-lookup"><span data-stu-id="57b2c-195">The cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="57b2c-196">Asegúrese de usar los cmdlets especificados en estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="57b2c-196">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="57b2c-197">Elimine la puerta de enlace de la VPN de ExpressRoute o de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="57b2c-197">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="57b2c-198">Elimine la subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="57b2c-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="57b2c-199">Agregue una subred de puerta de enlace que sea /27 o superior.</span><span class="sxs-lookup"><span data-stu-id="57b2c-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="57b2c-200">Si no tiene suficientes direcciones IP en la red virtual para aumentar el tamaño de la subred de puerta de enlace, debe agregar más espacio de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="57b2c-200">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="57b2c-201">Guarde la configuración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="57b2c-201">Save the VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="57b2c-202">Ya tiene una red virtual sin puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="57b2c-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="57b2c-203">Para crear puertas de enlace y completar las conexiones, puede continuar con el [paso 4 para crear una puerta de enlace de ExpressRoute](#gw), del conjunto de pasos anterior.</span><span class="sxs-lookup"><span data-stu-id="57b2c-203">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="to-add-point-to-site-configuration-to-the-vpn-gateway"></a><span data-ttu-id="57b2c-204">Incorporación de la configuración de punto a sitio a la puerta de enlace de VPN</span><span class="sxs-lookup"><span data-stu-id="57b2c-204">To add point-to-site configuration to the VPN gateway</span></span>
<span data-ttu-id="57b2c-205">Para agregar una configuración de punto a sitio a la puerta de enlace de VPN en una configuración de coexistencia, puede seguir los pasos que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="57b2c-205">You can follow the steps below to add Point-to-Site configuration to your VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="57b2c-206">Agregue el grupo de direcciones de clientes de VPN.</span><span class="sxs-lookup"><span data-stu-id="57b2c-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="57b2c-207">En Azure, cargue el certificado raíz de VPN de la puerta de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="57b2c-207">Upload the VPN root certificate to Azure for your VPN gateway.</span></span> <span data-ttu-id="57b2c-208">En este ejemplo, se supone que el certificado raíz se almacena en el equipo local donde se ejecutan los siguientes cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="57b2c-208">In this example, it's assumed that the root certificate is stored in the local machine where the following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="57b2c-209">Para más información sobre la VPN de punto a sitio, consulte [Configuración de una conexión punto a sitio a una red virtual mediante PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="57b2c-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="57b2c-210">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57b2c-210">Next steps</span></span>
<span data-ttu-id="57b2c-211">Para obtener más información acerca de ExpressRoute, consulte [P+F de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="57b2c-211">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
