---
title: "Configuración de conexiones de ExpressRoute y VPN de sitio a sitio coexistentes: modelo de implementación clásica: Azure | Microsoft Docs"
description: "Este artículo le guiará en la configuración de conexiones ExpressRoute y VPN de sitio a sitio que puedan coexistir en el modelo de implementación clásica."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 09d1649f0ca0cf4ca464d95b29461cad3fe51788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="8fda9-103">Configuración de conexiones de ExpressRoute y de sitio a sitio coexistentes (modelo de implementación clásica)</span><span class="sxs-lookup"><span data-stu-id="8fda9-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8fda9-104">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="8fda9-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="8fda9-105">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="8fda9-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="8fda9-106">Tener la posibilidad de configurar VPN de sitio a sitio y ExpressRoute tiene varias ventajas.</span><span class="sxs-lookup"><span data-stu-id="8fda9-106">Having the ability to configure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="8fda9-107">Puede configurar una VPN de sitio a sitio como una ruta de acceso seguro de conmutación por error para ExressRoute, o bien usar VPN de sitio a sitio para conectarse a sitios que no están conectados mediante ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="8fda9-108">En este artículo trataremos los pasos para configurar ambos escenarios.</span><span class="sxs-lookup"><span data-stu-id="8fda9-108">We will cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="8fda9-109">Este artículo se aplica al modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="8fda9-109">This article applies to the classic deployment model.</span></span> <span data-ttu-id="8fda9-110">Esta configuración no está disponible en el portal.</span><span class="sxs-lookup"><span data-stu-id="8fda9-110">This configuration is not available in the portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="8fda9-111">**Información acerca de los modelos de implementación de Azure**</span><span class="sxs-lookup"><span data-stu-id="8fda9-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="8fda9-112">Los circuitos ExpressRoute deben configurarse previamente antes de seguir las instrucciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="8fda9-112">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="8fda9-113">Asegúrese de que ha seguido las instrucciones para [crear un circuito ExpressRoute](expressroute-howto-circuit-classic.md) y [configurar el enrutamiento](expressroute-howto-routing-classic.md) antes de seguir los pasos que se indican a continuación.</span><span class="sxs-lookup"><span data-stu-id="8fda9-113">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow the steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="8fda9-114">Límites y limitaciones</span><span class="sxs-lookup"><span data-stu-id="8fda9-114">Limits and limitations</span></span>
* <span data-ttu-id="8fda9-115">**No se admite el enrutamiento transitorio.**</span><span class="sxs-lookup"><span data-stu-id="8fda9-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="8fda9-116">No se puede realizar un enrutamiento (a través de Azure) entre una red local conectada a través de una VPN sitio a sitio y una red local conectada a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="8fda9-117">**No se admite el punto a sitio.**</span><span class="sxs-lookup"><span data-stu-id="8fda9-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="8fda9-118">No se pueden habilitar conexiones VPN de punto a sitio a la misma red virtual que esté conectada a ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-118">You can't enable point-to-site VPN connections to the same VNet that is connected to ExpressRoute.</span></span> <span data-ttu-id="8fda9-119">VPN de punto a sitio y ExpressRoute no pueden coexistir en la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="8fda9-119">Point-to-site VPN and ExpressRoute cannot coexist for the same VNet.</span></span>
* <span data-ttu-id="8fda9-120">**En VPN Gateway de sitio a sitio no se puede habilitar la tunelización forzada.**</span><span class="sxs-lookup"><span data-stu-id="8fda9-120">**Forced tunneling cannot be enabled on the Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="8fda9-121">Solo se puede "forzar" que todo el tráfico vinculado a Internet vuelva a la red local a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-121">You can only "force" all Internet-bound traffic back to your on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="8fda9-122">**No se admite la puerta de enlace de la SKU de nivel Básico.**</span><span class="sxs-lookup"><span data-stu-id="8fda9-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="8fda9-123">Debe utilizar una puerta de enlace de la SKU que no sea de nivel Básico tanto para la [puerta de enlace de ExpressRoute](expressroute-about-virtual-network-gateways.md) como para la [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="8fda9-123">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="8fda9-124">**Solo se admite la VPN Gateway basada en rutas.**</span><span class="sxs-lookup"><span data-stu-id="8fda9-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="8fda9-125">Debe usar una [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) basada en rutas.</span><span class="sxs-lookup"><span data-stu-id="8fda9-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="8fda9-126">**Se debe configurar una ruta estática para VPN Gateway.**</span><span class="sxs-lookup"><span data-stu-id="8fda9-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="8fda9-127">Si la red local está conectada tanto a ExpressRoute como a una VPN de sitio a sitio, debe tener configurada una ruta estática en la red local para enrutar la conexión VPN de sitio a sitio a la red pública de Internet.</span><span class="sxs-lookup"><span data-stu-id="8fda9-127">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="8fda9-128">**Primero debe configurarse la puerta de enlace de ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="8fda9-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="8fda9-129">La puerta de enlace de ExpressRoute se debe crear antes de agregar la puerta de enlace de la VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="8fda9-129">You must create the ExpressRoute gateway first before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="8fda9-130">Diseños de configuración</span><span class="sxs-lookup"><span data-stu-id="8fda9-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="8fda9-131">Configuración de una VPN de sitio a sitio como una ruta de acceso de conmutación por error para ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8fda9-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="8fda9-132">Puede configurar una conexión VPN de sitio a sitio como una copia de seguridad para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="8fda9-133">Esto se aplica únicamente a las redes virtuales vinculadas a la ruta de acceso de emparejamiento privada de Azure.</span><span class="sxs-lookup"><span data-stu-id="8fda9-133">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="8fda9-134">No hay ninguna solución de conmutación por error basada en VPN para servicios accesibles a través de emparejamientos de Microsoft y públicos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8fda9-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="8fda9-135">El circuito ExpressRoute siempre es el vínculo principal.</span><span class="sxs-lookup"><span data-stu-id="8fda9-135">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="8fda9-136">Los datos fluirán a través de la ruta de acceso de VPN de sitio a sitio solo si se produce un error en el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-136">Data will flow through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="8fda9-137">Si bien se prefiere el circuito ExpressRoute a la VPN de sitio a sitio cuando ambas rutas son las mismas, Azure utilizará la coincidencia de prefijo más larga para elegir la ruta hacia el destino del paquete.</span><span class="sxs-lookup"><span data-stu-id="8fda9-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![Coexistencia](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="8fda9-139">Configuración de una VPN de sitio a sitio para conectarse a sitios no conectados mediante ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8fda9-139">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="8fda9-140">Puede configurar la red para sitios que se conectan directamente a Azure mediante una VPN de sitio a sitio y otros que se conectan a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-140">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexistencia](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="8fda9-142">No se puede configurar una red virtual como un enrutador de tránsito.</span><span class="sxs-lookup"><span data-stu-id="8fda9-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="8fda9-143">Selección de los pasos a seguir</span><span class="sxs-lookup"><span data-stu-id="8fda9-143">Selecting the steps to use</span></span>
<span data-ttu-id="8fda9-144">Hay dos conjuntos diferentes de los procedimientos entre los que elegir para configurar las conexiones que pueden coexistir.</span><span class="sxs-lookup"><span data-stu-id="8fda9-144">There are two different sets of procedures to choose from in order to configure connections that can coexist.</span></span> <span data-ttu-id="8fda9-145">El procedimiento de configuración que seleccione dependerá de si ya tiene una red virtual existente a la que quiere conectarse o si desea crear una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="8fda9-145">The configuration procedure that you select will depend on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="8fda9-146">No tengo una red virtual y necesito crear una.</span><span class="sxs-lookup"><span data-stu-id="8fda9-146">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="8fda9-147">Si aún no tiene una red virtual, este procedimiento le guiará en la creación de una nueva red virtual mediante el modelo de implementación clásica y la creación de nuevas conexiones VPN de sitio a sitio y ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using the classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="8fda9-148">Para configurarla, siga los pasos que se describen en la sección del artículo [Creación de una nueva red virtual y conexiones coexistentes](#new).</span><span class="sxs-lookup"><span data-stu-id="8fda9-148">To configure, follow the steps in the article section [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="8fda9-149">Ya tengo una red virtual con el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="8fda9-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="8fda9-150">Puede que ya tenga una red virtual con una conexión VPN de sitio a sitio o una conexión ExpressRoute existentes.</span><span class="sxs-lookup"><span data-stu-id="8fda9-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="8fda9-151">La sección [Configuración de conexiones coexistentes para una red virtual ya existente](#add) le guiará en la eliminación de la puerta de enlace y la creación de nuevas conexiones VPN de sitio a sitio y ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-151">The article section [To configure coexsiting connections for an already existing VNet](#add) will walk you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="8fda9-152">Tenga en cuenta que al crear las nuevas conexiones, se deben completar los pasos en un orden muy específico.</span><span class="sxs-lookup"><span data-stu-id="8fda9-152">Note that when creating the new connections, the steps must be completed in a very specific order.</span></span> <span data-ttu-id="8fda9-153">No utilice las instrucciones que aparecen en otros artículos para crear puertas de enlace y conexiones.</span><span class="sxs-lookup"><span data-stu-id="8fda9-153">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="8fda9-154">En este procedimiento, para crear conexiones que puedan coexistir, tendrá que eliminar la puerta de enlace y luego configurar nuevas puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="8fda9-154">In this procedure, creating connections that can coexist will require you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="8fda9-155">Esto significa que tendrá tiempo de inactividad para las conexiones entre entornos mientras elimina y vuelve a crear la puerta de enlace y las conexiones, pero no necesitará migrar las máquinas virtuales o servicios a una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="8fda9-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="8fda9-156">Las máquinas virtuales y los servicios podrán seguir comunicándose con el exterior a través del equilibrador de carga mientras configura la puerta de enlace si están configurados para ello.</span><span class="sxs-lookup"><span data-stu-id="8fda9-156">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="8fda9-157"><a name="new"></a>Creación de una nueva red virtual y conexiones coexistentes</span><span class="sxs-lookup"><span data-stu-id="8fda9-157"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="8fda9-158">Este procedimiento le guiará en la creación de una red virtual y conexiones de sitio a sitio y ExpressRoute que coexistirán.</span><span class="sxs-lookup"><span data-stu-id="8fda9-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="8fda9-159">Deberá instalar la versión más reciente de los cmdlets de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8fda9-159">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8fda9-160">Consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) para más información sobre cómo instalar los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8fda9-160">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="8fda9-161">Tenga en cuenta que los cmdlets que se van a utilizar en esta configuración pueden ser ligeramente diferentes de aquellos con los que podría estar familiarizado.</span><span class="sxs-lookup"><span data-stu-id="8fda9-161">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="8fda9-162">Asegúrese de usar los cmdlets especificados en estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="8fda9-162">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="8fda9-163">Cree un esquema para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="8fda9-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="8fda9-164">Para más información sobre el esquema de configuración, consulte [Esquema de configuración de la red virtual de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fda9-164">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="8fda9-165">Al crear el esquema, asegúrese de que usa los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="8fda9-165">When you create your schema, make sure you use the following values:</span></span>
   
   * <span data-ttu-id="8fda9-166">La subred de puerta de enlace para la red virtual debe ser /27 o un prefijo más corto (como /26 o /25).</span><span class="sxs-lookup"><span data-stu-id="8fda9-166">The gateway subnet for the virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="8fda9-167">El tipo de conexión de puerta de enlace es "Dedicado".</span><span class="sxs-lookup"><span data-stu-id="8fda9-167">The gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="8fda9-168">Después de crear y configurar el archivo de esquema xml, cargue el archivo.</span><span class="sxs-lookup"><span data-stu-id="8fda9-168">After creating and configuring your xml schema file, upload the file.</span></span> <span data-ttu-id="8fda9-169">Esto creará la red virtual.</span><span class="sxs-lookup"><span data-stu-id="8fda9-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="8fda9-170">Use el cmdlet siguiente para cargar el archivo, reemplazando el valor por el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="8fda9-170">Use the following cmdlet to upload your file, replacing the value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="8fda9-171"><a name="gw"></a>Cree una puerta de enlace de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="8fda9-172">Asegúrese de especificar GatewaySKU como *Standard*, *HighPerformance* o *UltraPerformance* y GatewayType como *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="8fda9-172">Be sure to specify the GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="8fda9-173">Use el ejemplo siguiente y sustituya los valores por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="8fda9-173">Use the following sample, substituting the values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="8fda9-174">Vincule la puerta de enlace de ExpressRoute al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-174">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="8fda9-175">Una vez completado este paso, se ha establecido la conexión entre su red local y Azure a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8fda9-175">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="8fda9-176"><a name="vpngw"></a>A continuación, cree la puerta de enlace de la VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="8fda9-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="8fda9-177">Los valores de GatewaySKU deben ser *Standard*, *HighPerformance* o *UltraPerformance* y GatewayType debe ser *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="8fda9-177">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="8fda9-178">Para recuperar la configuración de la puerta de enlace de red virtual, lo que incluye el identificador de puerta de enlace y la dirección IP pública, use el cmdlet `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="8fda9-178">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for the following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="8fda9-179">Cree una entidad de puerta de enlace de VPN de sitio local.</span><span class="sxs-lookup"><span data-stu-id="8fda9-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="8fda9-180">Este comando no configura la puerta de enlace de VPN local.</span><span class="sxs-lookup"><span data-stu-id="8fda9-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="8fda9-181">En su lugar, permite proporcionar la configuración de puerta de enlace local, como la dirección IP pública y el espacio de direcciones local, para que la puerta de enlace de VPN de Azure pueda conectarse a ella.</span><span class="sxs-lookup"><span data-stu-id="8fda9-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8fda9-182">El sitio local de la VPN de sitio a sitio no está definido en netcfg.</span><span class="sxs-lookup"><span data-stu-id="8fda9-182">The local site for the Site-to-Site VPN is not defined in the netcfg.</span></span> <span data-ttu-id="8fda9-183">En su lugar, es preciso usar este cmdlet para especificar los parámetros del sitio local.</span><span class="sxs-lookup"><span data-stu-id="8fda9-183">Instead, you must use this cmdlet to specify the local site parameters.</span></span> <span data-ttu-id="8fda9-184">No puede definirlos ni con el portal ni con el archivo netcfg.</span><span class="sxs-lookup"><span data-stu-id="8fda9-184">You cannot define it using either portal, or the netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="8fda9-185">Use el ejemplo siguiente y reemplace los valores por los suyos propios:</span><span class="sxs-lookup"><span data-stu-id="8fda9-185">Use the following sample, replacing the values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="8fda9-186">Si la red local tiene varias rutas, puede pasar todas ellas en una matriz.</span><span class="sxs-lookup"><span data-stu-id="8fda9-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="8fda9-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="8fda9-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="8fda9-188">Para recuperar la configuración de la puerta de enlace de red virtual, lo que incluye el identificador de puerta de enlace y la dirección IP pública, use el cmdlet `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="8fda9-188">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="8fda9-189">Consulte el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="8fda9-189">See the following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="8fda9-190">Configure el dispositivo VPN local para que se conecte a la nueva puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8fda9-190">Configure your local VPN device to connect to the new gateway.</span></span> <span data-ttu-id="8fda9-191">Al configurar el dispositivo VPN, use la información que recuperó en el paso 6.</span><span class="sxs-lookup"><span data-stu-id="8fda9-191">Use the information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="8fda9-192">Para obtener más información acerca de la configuración del dispositivo VPN, consulte [Configuración de dispositivos VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="8fda9-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="8fda9-193">Vincule la puerta de enlace de VPN sitio a sitio en Azure a la puerta de enlace local.</span><span class="sxs-lookup"><span data-stu-id="8fda9-193">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>
   
    <span data-ttu-id="8fda9-194">En este ejemplo, connectedEntityId es el identificador de puerta de enlace local. Para encontrarlo, es preciso ejecutar `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="8fda9-194">In this example, connectedEntityId is the local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="8fda9-195">Para encontrar virtualNetworkGatewayId, use el cmdlet `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="8fda9-195">You can find virtualNetworkGatewayId by using the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="8fda9-196">Después de este paso, se establece la conexión entre la red local y Azure a través de la conexión VPN sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="8fda9-196">After this step, the connection between your local network and Azure via the Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="8fda9-197"><a name="add"></a>Para configurar conexiones coexistentes para una red virtual ya existente</span><span class="sxs-lookup"><span data-stu-id="8fda9-197"><a name="add"></a>To configure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="8fda9-198">Si ya tiene una red virtual, compruebe el tamaño de la subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8fda9-198">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="8fda9-199">Si la subred de puerta de enlace es /28 o /29, primero debe eliminar la puerta de enlace de red virtual y aumentar el tamaño de la subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8fda9-199">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="8fda9-200">Los pasos de esta sección le mostrarán cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="8fda9-200">The steps in this section will show you how to do that.</span></span>

<span data-ttu-id="8fda9-201">Si la puerta de enlace es /27 o mayor y la red virtual está conectada a través de ExpressRoute, puede omitir los pasos siguientes y continuar con ["Paso 6: Creación una puerta de enlace VPN de sitio a sitio"](#vpngw) en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="8fda9-201">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="8fda9-202">Cuando elimine la puerta de enlace existente, las instalaciones locales perderán la conexión con la red virtual mientras trabaja en esta configuración.</span><span class="sxs-lookup"><span data-stu-id="8fda9-202">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="8fda9-203">Necesitará instalar la versión más reciente de los cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8fda9-203">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="8fda9-204">Consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview) para más información sobre cómo instalar los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8fda9-204">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="8fda9-205">Tenga en cuenta que los cmdlets que se van a utilizar en esta configuración pueden ser ligeramente diferentes de aquellos con los que podría estar familiarizado.</span><span class="sxs-lookup"><span data-stu-id="8fda9-205">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="8fda9-206">Asegúrese de usar los cmdlets especificados en estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="8fda9-206">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="8fda9-207">Elimine la puerta de enlace de la VPN de ExpressRoute o de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="8fda9-207">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="8fda9-208">Use el siguiente cmdlet, reemplazando los valores por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="8fda9-208">Use the following cmdlet, replacing the values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="8fda9-209">Exporte el esquema de red virtual.</span><span class="sxs-lookup"><span data-stu-id="8fda9-209">Export the virtual network schema.</span></span> <span data-ttu-id="8fda9-210">Use el siguiente cmdlet de PowerShell, reemplazando los valores por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="8fda9-210">Use the following PowerShell cmdlet, replacing the values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="8fda9-211">Edite el esquema del archivo de configuración de red para que la subred de puerta de enlace sea /27 o un prefijo más corto (como /26 o /25).</span><span class="sxs-lookup"><span data-stu-id="8fda9-211">Edit the network configuration file schema so that the gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="8fda9-212">Consulte el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="8fda9-212">See the following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="8fda9-213">Si no quedan suficientes direcciones IP en la red virtual para aumentar el tamaño de la subred de puerta de enlace, debe agregar más espacio de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="8fda9-213">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span> <span data-ttu-id="8fda9-214">Para más información sobre el esquema de configuración, consulte [Esquema de configuración de la red virtual de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="8fda9-214">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="8fda9-215">Si la puerta de enlace anterior era una VPN de sitio a sitio, debe cambiar también el tipo de conexión a **Dedicado**.</span><span class="sxs-lookup"><span data-stu-id="8fda9-215">If your previous gateway was a Site-to-Site VPN, you must also change the connection type to **Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="8fda9-216">Ya tiene una red virtual sin puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="8fda9-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="8fda9-217">Para crear puertas de enlace y completar las conexiones, puede continuar con el [paso 4 para crear una puerta de enlace de ExpressRoute](#gw), del conjunto de pasos anterior.</span><span class="sxs-lookup"><span data-stu-id="8fda9-217">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fda9-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8fda9-218">Next steps</span></span>
<span data-ttu-id="8fda9-219">Para más información sobre ExpressRoute, consulte [P+F de ExpressRoute](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="8fda9-219">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

