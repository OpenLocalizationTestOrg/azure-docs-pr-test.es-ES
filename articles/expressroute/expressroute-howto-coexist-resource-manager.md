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
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a><span data-ttu-id="04906-103">Configuración de conexiones coexistentes de ExpressRoute de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="04906-103">Configure ExpressRoute and Site-to-Site coexisting connections</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="04906-104">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="04906-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="04906-105">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="04906-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="04906-106">La configuración de las conexiones coexistentes VPN de sitio a sitio y ExpressRoute tiene varias ventajas.</span><span class="sxs-lookup"><span data-stu-id="04906-106">Configuring Site-to-Site VPN and ExpressRoute coexisting connections has several advantages.</span></span> <span data-ttu-id="04906-107">Puede configurar una VPN de sitio a sitio como una ruta de acceso seguro de conmutación por error para ExressRoute o usar VPN de sitio a sitio tooconnect toosites que no están conectados a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04906-107">You can configure a Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="04906-108">Trataremos Hola pasos tooconfigure ambos escenarios en este artículo.</span><span class="sxs-lookup"><span data-stu-id="04906-108">We cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="04906-109">En este artículo se aplica el modelo de implementación del Administrador de recursos de toohello y usa PowerShell.</span><span class="sxs-lookup"><span data-stu-id="04906-109">This article applies toohello Resource Manager deployment model and uses PowerShell.</span></span> <span data-ttu-id="04906-110">Esta configuración no está disponible en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="04906-110">This configuration is not available in hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04906-111">Circuitos ExpressRoute deben configurarse previamente antes de seguir estas instrucciones Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-111">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="04906-112">Asegúrese de que ha seguido las guías de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y [configurar el enrutamiento de](expressroute-howto-routing-arm.md) antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="04906-112">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [configure routing](expressroute-howto-routing-arm.md) before you proceed.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="04906-113">Límites y limitaciones</span><span class="sxs-lookup"><span data-stu-id="04906-113">Limits and limitations</span></span>
* <span data-ttu-id="04906-114">**No se admite el enrutamiento transitorio.**</span><span class="sxs-lookup"><span data-stu-id="04906-114">**Transit routing is not supported.**</span></span> <span data-ttu-id="04906-115">No se puede realizar un enrutamiento (a través de Azure) entre una red local conectada a través de una VPN sitio a sitio y una red local conectada a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04906-115">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="04906-116">**No se admite la puerta de enlace de la SKU de nivel Básico.**</span><span class="sxs-lookup"><span data-stu-id="04906-116">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="04906-117">Debe usar una puerta de enlace básico SKU que no sea para ambos hello [puerta de enlace ExpressRoute](expressroute-about-virtual-network-gateways.md) hello y [puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="04906-117">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="04906-118">**Solo se admite la VPN Gateway basada en rutas.**</span><span class="sxs-lookup"><span data-stu-id="04906-118">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="04906-119">Debe usar una [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) basada en rutas.</span><span class="sxs-lookup"><span data-stu-id="04906-119">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="04906-120">**Se debe configurar una ruta estática para VPN Gateway.**</span><span class="sxs-lookup"><span data-stu-id="04906-120">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="04906-121">Si la red local está conectado tooboth ExpressRoute y un sitio a sitio VPN, debe tener una ruta estática configurada en su toohello de conexión de red local tooroute Hola sitio a sitio VPN Internet pública.</span><span class="sxs-lookup"><span data-stu-id="04906-121">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="04906-122">**Puerta de enlace de ExpressRoute debe configurarse en primer lugar y vinculado tooa circuito.**</span><span class="sxs-lookup"><span data-stu-id="04906-122">**ExpressRoute gateway must be configured first and linked tooa circuit.**</span></span> <span data-ttu-id="04906-123">Debe crear la puerta de enlace de ExpressRoute de hello en primer lugar y vincularla tooa circuito antes de agregar la puerta de enlace VPN de sitio a sitio Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-123">You must create hello ExpressRoute gateway first and link it tooa circuit before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="04906-124">Diseños de configuración</span><span class="sxs-lookup"><span data-stu-id="04906-124">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="04906-125">Configuración de una VPN de sitio a sitio como una ruta de acceso de conmutación por error para ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="04906-125">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="04906-126">Puede configurar una conexión VPN de sitio a sitio como una copia de seguridad para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04906-126">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="04906-127">Esto aplica solo toovirtual redes vinculado toohello Azure ruta privada de intercambio de tráfico.</span><span class="sxs-lookup"><span data-stu-id="04906-127">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="04906-128">No hay ninguna solución de conmutación por error basada en VPN para servicios accesibles a través de emparejamientos de Microsoft y públicos de Azure.</span><span class="sxs-lookup"><span data-stu-id="04906-128">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="04906-129">Hola circuito de ExpressRoute no distingue vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-129">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="04906-130">Los datos fluyen a través de la ruta de acceso VPN de sitio a sitio Hola solo si se produce un error en hello circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04906-130">Data flows through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span>

> [!NOTE]
> <span data-ttu-id="04906-131">Mientras se prefiere circuito de ExpressRoute a través de VPN de sitio a sitio cuando ambas rutas se Hola igual, Azure utilizará ruta de hello más larga prefijo coincidencia toochoose Hola hacia el destino del paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="04906-131">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Coexistencia](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="04906-133">Configurar una toosites de tooconnect VPN de sitio a sitio no está conectado a través de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="04906-133">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="04906-134">Puede configurar la red donde algunos sitios conectan directamente tooAzure a través de VPN de sitio a sitio y algunos de los sitios a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04906-134">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexistencia](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="04906-136">No se puede configurar una red virtual como un enrutador de tránsito.</span><span class="sxs-lookup"><span data-stu-id="04906-136">You cannot configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="04906-137">Seleccionar Hola pasos toouse</span><span class="sxs-lookup"><span data-stu-id="04906-137">Selecting hello steps toouse</span></span>
<span data-ttu-id="04906-138">Hay dos conjuntos diferentes de los procedimientos toochoose de.</span><span class="sxs-lookup"><span data-stu-id="04906-138">There are two different sets of procedures toochoose from.</span></span> <span data-ttu-id="04906-139">procedimiento de configuración de Hola que seleccione depende de si tiene una red virtual existente que desea tooconnect a, o desea toocreate una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="04906-139">hello configuration procedure that you select depends on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="04906-140">No tiene una red virtual y necesita toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="04906-140">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="04906-141">Si aún no tiene una red virtual, este procedimiento le guía en la creación de una nueva red virtual mediante el modelo de implementación de Resource Manager y la creación de nuevas conexiones VPN de sitio a sitio y ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04906-141">If you don’t already have a virtual network, this procedure walks you through creating a new virtual network using Resource Manager deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="04906-142">tooconfigure una red virtual, siga los pasos de hello en [toocreate una nueva red virtual y las conexiones coexistentes](#new).</span><span class="sxs-lookup"><span data-stu-id="04906-142">tooconfigure a virtual network, follow hello steps in [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="04906-143">Ya tengo una red virtual del modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="04906-143">I already have a Resource Manager deployment model VNet.</span></span>
  
    <span data-ttu-id="04906-144">Puede que ya tenga una red virtual con una conexión VPN de sitio a sitio o una conexión ExpressRoute existentes.</span><span class="sxs-lookup"><span data-stu-id="04906-144">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="04906-145">Hola [tooconfigure coexistentes conexiones para una red virtual existente ya](#add) sección le guía a través de la eliminación de puerta de enlace de hello y, a continuación, crear nuevas conexiones de VPN de sitio a sitio y de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04906-145">hello [tooconfigure coexisting connections for an already existing VNet](#add) section walks you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="04906-146">Al crear nuevas conexiones de hello, pasos de hello deben realizarse en un orden específico.</span><span class="sxs-lookup"><span data-stu-id="04906-146">When creating hello new connections, hello steps must be completed in a specific order.</span></span> <span data-ttu-id="04906-147">No utilice instrucciones de hello en otro artículos toocreate sus conexiones y las puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="04906-147">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="04906-148">En este procedimiento, crear conexiones que pueden coexistir requiere toodelete la puerta de enlace y, a continuación, configure nuevas puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="04906-148">In this procedure, creating connections that can coexist requires you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="04906-149">Tendrá tiempo de inactividad para las conexiones entre entornos al eliminar y volver a crear la puerta de enlace y las conexiones, pero no tendrá que toomigrate cualquiera de su máquinas virtuales o servicios tooa nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="04906-149">You will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="04906-150">Las máquinas virtuales y servicios se seguirán toocommunicate capaz de salida a través del equilibrador de carga de hello al configurar la puerta de enlace si están toodo configurado así.</span><span class="sxs-lookup"><span data-stu-id="04906-150">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="04906-151"><a name="new"></a>toocreate una nueva red virtual y las conexiones coexistentes</span><span class="sxs-lookup"><span data-stu-id="04906-151"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="04906-152">Este procedimiento le guía en la creación de una red virtual y conexiones de sitio a sitio y ExpressRoute que coexisten.</span><span class="sxs-lookup"><span data-stu-id="04906-152">This procedure walks you through creating a VNet and Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="04906-153">Instalar versión más reciente de Hola de hello cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="04906-153">Install hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="04906-154">Para obtener información acerca de cómo instalar los cmdlets de hello, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="04906-154">For information about installing hello cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="04906-155">cmdlets de Hola que se usan para esta configuración puede ser ligeramente diferente de lo que es posible que esté familiarizado con.</span><span class="sxs-lookup"><span data-stu-id="04906-155">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="04906-156">Cmdlets de hello toouse seguro especificar en estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="04906-156">Be sure toouse hello cmdlets specified in these instructions.</span></span>
2. <span data-ttu-id="04906-157">Inicie sesión en tooyour cuenta y configurar el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-157">Log in tooyour account and set up hello environment.</span></span>

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. <span data-ttu-id="04906-158">Cree una red virtual, incluida la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="04906-158">Create a virtual network including Gateway Subnet.</span></span> <span data-ttu-id="04906-159">Para obtener más información acerca de la configuración de red virtual de hello, consulte [configuración de red Virtual de Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="04906-159">For more information about hello virtual network configuration, see [Azure Virtual Network configuration](../virtual-network/virtual-networks-create-vnet-arm-ps.md).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="04906-160">Hola subred de puerta de enlace debe ser /27 o un prefijo más corto (por ejemplo, /26 o /25).</span><span class="sxs-lookup"><span data-stu-id="04906-160">hello Gateway Subnet must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   > 
   > 
   
    <span data-ttu-id="04906-161">Cree una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="04906-161">Create a new VNet.</span></span>

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    <span data-ttu-id="04906-162">Agregue subredes.</span><span class="sxs-lookup"><span data-stu-id="04906-162">Add subnets.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="04906-163">Guardar configuración de redes virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-163">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="04906-164"><a name="gw"></a>Cree una puerta de enlace de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04906-164"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="04906-165">Para obtener más información acerca de la configuración de puerta de enlace de ExpressRoute de hello, consulte [configuración de puerta de enlace de ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="04906-165">For more information about hello ExpressRoute gateway configuration, see [ExpressRoute gateway configuration](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="04906-166">Hello GatewaySKU debe ser *estándar*, *HighPerformance*, o *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="04906-166">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. <span data-ttu-id="04906-167">Vínculo de circuito de ExpressRoute de toohello de puerta de enlace de ExpressRoute de Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-167">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="04906-168">Una vez completado este paso, se establece la conexión de hello entre la red local y Azure, a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="04906-168">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span> <span data-ttu-id="04906-169">Para obtener más información acerca de la operación de enlace de hello, consulte [tooExpressRoute de redes virtuales de vínculo](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="04906-169">For more information about hello link operation, see [Link VNets tooExpressRoute](expressroute-howto-linkvnet-arm.md).</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <span data-ttu-id="04906-170"><a name="vpngw"></a>A continuación, cree la puerta de enlace de la VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="04906-170"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="04906-171">Para obtener más información acerca de la configuración de puerta de enlace VPN de hello, consulte [configurar una red virtual con una conexión de sitio a sitio](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="04906-171">For more information about hello VPN gateway configuration, see [Configure a VNet with a Site-to-Site connection](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md).</span></span> <span data-ttu-id="04906-172">Hello GatewaySKU debe ser *estándar*, *HighPerformance*, o *UltraPerformance*.</span><span class="sxs-lookup"><span data-stu-id="04906-172">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance*.</span></span> <span data-ttu-id="04906-173">debe Hello VpnType *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="04906-173">hello VpnType must *RouteBased*.</span></span>

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    <span data-ttu-id="04906-174">Azure VPN Gateway admite el protocolo de enrutamiento de BGP.</span><span class="sxs-lookup"><span data-stu-id="04906-174">Azure VPN gateway supports BGP routing protocol.</span></span> <span data-ttu-id="04906-175">Puede especificar ASN (número de AS) para esa red Virtual mediante la adición de conmutador de Asn - Hola Hola siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="04906-175">You can specify ASN (AS Number) for that Virtual Network by adding hello -Asn switch in hello following command.</span></span> <span data-ttu-id="04906-176">No se especifica ese parámetro se 65515 número tooAS de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="04906-176">Not specifying that parameter will default tooAS number 65515.</span></span>

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    <span data-ttu-id="04906-177">Puede encontrar Hola emparejamiento IP BGP y Hola como número que utiliza Azure para puerta de enlace VPN de hello en $azureVpn.BgpSettings.BgpPeeringAddress y $azureVpn.BgpSettings.Asn.</span><span class="sxs-lookup"><span data-stu-id="04906-177">You can find hello BGP peering IP and hello AS number that Azure uses for hello VPN gateway in $azureVpn.BgpSettings.BgpPeeringAddress and $azureVpn.BgpSettings.Asn.</span></span> <span data-ttu-id="04906-178">Para más información, consulte [Configuración de BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) para Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="04906-178">For more information, see [Configure BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) for Azure VPN gateway.</span></span>
7. <span data-ttu-id="04906-179">Cree una entidad de puerta de enlace de VPN de sitio local.</span><span class="sxs-lookup"><span data-stu-id="04906-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="04906-180">Este comando no configura la puerta de enlace de VPN local.</span><span class="sxs-lookup"><span data-stu-id="04906-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="04906-181">En su lugar, permite a tooprovide la configuración de puerta de enlace local hello, como la dirección IP pública de Hola y Hola local espacio de direcciones, por lo que hello puerta de enlace VPN de Azure puede conectarse tooit.</span><span class="sxs-lookup"><span data-stu-id="04906-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
    <span data-ttu-id="04906-182">Si su dispositivo VPN local solo admite enrutamiento estático, puede configurar rutas estáticas Hola Hola siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="04906-182">If your local VPN device only supports static routing, you can configure hello static routes in hello following way:</span></span>

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    <span data-ttu-id="04906-183">Si su dispositivo VPN local admite Hola BGP y desea tooenable de enrutamiento dinámico, debe tooknow Hola BGP emparejamiento hello como número de que la VPN local y la IP de dispositivo usa.</span><span class="sxs-lookup"><span data-stu-id="04906-183">If your local VPN device supports hello BGP and you want tooenable dynamic routing, you need tooknow hello BGP peering IP and hello AS number that your local VPN device uses.</span></span>

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. <span data-ttu-id="04906-184">Configure su local VPN dispositivo tooconnect toohello nueva puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="04906-184">Configure your local VPN device tooconnect toohello new Azure VPN gateway.</span></span> <span data-ttu-id="04906-185">Para obtener más información sobre la configuración del dispositivo VPN, vea [Configuración de dispositivos VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="04906-185">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
9. <span data-ttu-id="04906-186">Vínculo Hola VPN de sitio a sitio puerta de enlace en Azure toohello puerta de enlace local.</span><span class="sxs-lookup"><span data-stu-id="04906-186">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <span data-ttu-id="04906-187"><a name="add"></a>tooconfigure coexistentes conexiones para una red virtual existente</span><span class="sxs-lookup"><span data-stu-id="04906-187"><a name="add"></a>tooconfigure coexisting connections for an already existing VNet</span></span>
<span data-ttu-id="04906-188">Si tiene una red virtual existente, compruebe el tamaño de subred de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-188">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="04906-189">Si está en la subred de puerta de enlace de hello /28 o /29, primero debe eliminar la puerta de enlace de red virtual de Hola y aumentar el tamaño de subred de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-189">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="04906-190">Hello pasos de esta sección muestran cómo toodo que.</span><span class="sxs-lookup"><span data-stu-id="04906-190">hello steps in this section show you how toodo that.</span></span>

<span data-ttu-id="04906-191">Si está de subred de puerta de enlace de hello /27 o superior y red virtual de hello está conectado a través de ExpressRoute, puede omitir estos pasos hello y continuar demasiado["Paso 6: crear una puerta de enlace VPN de sitio a sitio"](#vpngw) en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-191">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span> 

> [!NOTE]
> <span data-ttu-id="04906-192">Cuando se elimina la puerta de enlace existente hello, sus instalaciones locales perderá red virtual de hello conexión tooyour mientras se trabaja con esta configuración.</span><span class="sxs-lookup"><span data-stu-id="04906-192">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span> 
> 
> 

1. <span data-ttu-id="04906-193">Necesitará la versión más reciente de hello tooinstall de hello cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="04906-193">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="04906-194">Para obtener más información acerca de cómo instalar los cmdlets, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="04906-194">For more information about installing cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="04906-195">cmdlets de Hola que se usan para esta configuración puede ser ligeramente diferente de lo que es posible que esté familiarizado con.</span><span class="sxs-lookup"><span data-stu-id="04906-195">hello cmdlets that you use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="04906-196">Cmdlets de hello toouse seguro especificar en estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="04906-196">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="04906-197">Eliminar Hola VPN de sitio a sitio o ExpressRoute puerta de enlace existente.</span><span class="sxs-lookup"><span data-stu-id="04906-197">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span>

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. <span data-ttu-id="04906-198">Elimine la subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="04906-198">Delete Gateway Subnet.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. <span data-ttu-id="04906-199">Agregue una subred de puerta de enlace que sea /27 o superior.</span><span class="sxs-lookup"><span data-stu-id="04906-199">Add a Gateway Subnet that is /27 or larger.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="04906-200">Si no tiene suficientes direcciones IP que se mantienen en el tamaño de subred de puerta de enlace de red virtual tooincrease hello, deberá tooadd más espacio de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="04906-200">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span>
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    <span data-ttu-id="04906-201">Guardar configuración de redes virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-201">Save hello VNet configuration.</span></span>

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="04906-202">Ya tiene una red virtual sin puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="04906-202">At this point, you have a VNet with no gateways.</span></span> <span data-ttu-id="04906-203">toocreate nuevas puertas de enlace y completar las conexiones, puede continuar con la [paso 4: crear una puerta de enlace de ExpressRoute](#gw), que se encuentra en hello anterior conjunto de pasos.</span><span class="sxs-lookup"><span data-stu-id="04906-203">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a><span data-ttu-id="04906-204">puerta de enlace VPN de tooadd point-to-site configuration toohello</span><span class="sxs-lookup"><span data-stu-id="04906-204">tooadd point-to-site configuration toohello VPN gateway</span></span>
<span data-ttu-id="04906-205">Puede seguir pasos de Hola por debajo de la puerta de enlace VPN de tooyour de tooadd Point-to-Site configuración en una configuración de coexistencia.</span><span class="sxs-lookup"><span data-stu-id="04906-205">You can follow hello steps below tooadd Point-to-Site configuration tooyour VPN gateway in a co-existence setup.</span></span>

1. <span data-ttu-id="04906-206">Agregue el grupo de direcciones de clientes de VPN.</span><span class="sxs-lookup"><span data-stu-id="04906-206">Add VPN Client address pool.</span></span>

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. <span data-ttu-id="04906-207">Cargar certificado de raíz de hello VPN tooAzure para la puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="04906-207">Upload hello VPN root certificate tooAzure for your VPN gateway.</span></span> <span data-ttu-id="04906-208">En este ejemplo, se supone que ese certificado de raíz de Hola se almacena en el equipo local Hola donde se ejecuta los siguientes cmdlets de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="04906-208">In this example, it's assumed that hello root certificate is stored in hello local machine where hello following PowerShell cmdlets are run.</span></span>

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

<span data-ttu-id="04906-209">Para más información sobre la VPN de punto a sitio, consulte [Configuración de una conexión punto a sitio a una red virtual mediante PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="04906-209">For more information on Point-to-Site VPN, see [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04906-210">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04906-210">Next steps</span></span>
<span data-ttu-id="04906-211">Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="04906-211">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
