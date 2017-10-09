---
title: "Configuración de conexiones de ExpressRoute y VPN de sitio a sitio coexistentes: modelo de implementación clásica: Azure | Microsoft Docs"
description: "Este artículo le guiará a través de configuración de una conexión VPN de sitio a sitio que puede coexistir para el modelo de implementación clásica de Hola y ExpressRoute."
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
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="f85de-103">Configuración de conexiones de ExpressRoute y de sitio a sitio coexistentes (modelo de implementación clásica)</span><span class="sxs-lookup"><span data-stu-id="f85de-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f85de-104">PowerShell: administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="f85de-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="f85de-105">PowerShell: clásico</span><span class="sxs-lookup"><span data-stu-id="f85de-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="f85de-106">Tener capacidad de hello tooconfigure VPN de sitio a sitio y ExpressRoute tiene varias ventajas.</span><span class="sxs-lookup"><span data-stu-id="f85de-106">Having hello ability tooconfigure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="f85de-107">Puede configurar VPN de sitio a sitio como una ruta de acceso seguro de conmutación por error para ExressRoute o usar VPN de sitio a sitio tooconnect toosites que no están conectados a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f85de-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="f85de-108">Trataremos Hola pasos tooconfigure ambos escenarios en este artículo.</span><span class="sxs-lookup"><span data-stu-id="f85de-108">We will cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="f85de-109">En este artículo se aplica a modelos de implementación clásica de toohello.</span><span class="sxs-lookup"><span data-stu-id="f85de-109">This article applies toohello classic deployment model.</span></span> <span data-ttu-id="f85de-110">Esta configuración no está disponible en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-110">This configuration is not available in hello portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="f85de-111">**Información sobre los modelos de implementación de Azure**</span><span class="sxs-lookup"><span data-stu-id="f85de-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="f85de-112">Circuitos ExpressRoute deben configurarse previamente antes de seguir estas instrucciones Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-112">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="f85de-113">Asegúrese de que ha seguido las guías de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-classic.md) y [configurar el enrutamiento de](expressroute-howto-routing-classic.md) antes de seguir estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-113">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow hello steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="f85de-114">Límites y limitaciones</span><span class="sxs-lookup"><span data-stu-id="f85de-114">Limits and limitations</span></span>
* <span data-ttu-id="f85de-115">**No se admite el enrutamiento transitorio.**</span><span class="sxs-lookup"><span data-stu-id="f85de-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="f85de-116">No se puede realizar un enrutamiento (a través de Azure) entre una red local conectada a través de una VPN sitio a sitio y una red local conectada a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f85de-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="f85de-117">**No se admite el punto a sitio.**</span><span class="sxs-lookup"><span data-stu-id="f85de-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="f85de-118">No se puede habilitar point-to-site VPN conexiones toohello misma red virtual que está conectado tooExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f85de-118">You can't enable point-to-site VPN connections toohello same VNet that is connected tooExpressRoute.</span></span> <span data-ttu-id="f85de-119">Point-to-site VPN y ExpressRoute no pueden coexistir para hello misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="f85de-119">Point-to-site VPN and ExpressRoute cannot coexist for hello same VNet.</span></span>
* <span data-ttu-id="f85de-120">**No se puede habilitar la tunelización forzada en la puerta de enlace VPN de sitio a sitio de Hola.**</span><span class="sxs-lookup"><span data-stu-id="f85de-120">**Forced tunneling cannot be enabled on hello Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="f85de-121">Solo puede "forzar" todo vinculado a Internet tráfico tooyour back-local de red a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f85de-121">You can only "force" all Internet-bound traffic back tooyour on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="f85de-122">**No se admite la puerta de enlace de la SKU de nivel Básico.**</span><span class="sxs-lookup"><span data-stu-id="f85de-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="f85de-123">Debe usar una puerta de enlace básico SKU que no sea para ambos hello [puerta de enlace ExpressRoute](expressroute-about-virtual-network-gateways.md) hello y [puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="f85de-123">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="f85de-124">**Solo se admite la VPN Gateway basada en rutas.**</span><span class="sxs-lookup"><span data-stu-id="f85de-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="f85de-125">Debe usar una [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) basada en rutas.</span><span class="sxs-lookup"><span data-stu-id="f85de-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="f85de-126">**Se debe configurar una ruta estática para VPN Gateway.**</span><span class="sxs-lookup"><span data-stu-id="f85de-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="f85de-127">Si la red local está conectado tooboth ExpressRoute y un sitio a sitio VPN, debe tener una ruta estática configurada en su toohello de conexión de red local tooroute Hola sitio a sitio VPN Internet pública.</span><span class="sxs-lookup"><span data-stu-id="f85de-127">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="f85de-128">**Primero debe configurarse la puerta de enlace de ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="f85de-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="f85de-129">Debe crear puerta de enlace de ExpressRoute de hello primero antes de agregar la puerta de enlace VPN de sitio a sitio de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-129">You must create hello ExpressRoute gateway first before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="f85de-130">Diseños de configuración</span><span class="sxs-lookup"><span data-stu-id="f85de-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="f85de-131">Configuración de una VPN de sitio a sitio como una ruta de acceso de conmutación por error para ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f85de-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="f85de-132">Puede configurar una conexión VPN de sitio a sitio como una copia de seguridad para ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f85de-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="f85de-133">Esto aplica solo toovirtual redes vinculado toohello Azure ruta privada de intercambio de tráfico.</span><span class="sxs-lookup"><span data-stu-id="f85de-133">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="f85de-134">No hay ninguna solución de conmutación por error basada en VPN para servicios accesibles a través de emparejamientos de Microsoft y públicos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f85de-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="f85de-135">Hola circuito de ExpressRoute no distingue vínculo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-135">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="f85de-136">Datos fluirá a través de la ruta de acceso VPN de sitio a sitio Hola solo si se produce un error en hello circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f85de-136">Data will flow through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="f85de-137">Mientras se prefiere circuito de ExpressRoute a través de VPN de sitio a sitio cuando ambas rutas se Hola igual, Azure utilizará ruta de hello más larga prefijo coincidencia toochoose Hola hacia el destino del paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="f85de-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Coexistencia](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="f85de-139">Configurar una toosites de tooconnect VPN de sitio a sitio no está conectado a través de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f85de-139">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="f85de-140">Puede configurar la red donde algunos sitios conectan directamente tooAzure a través de VPN de sitio a sitio y algunos de los sitios a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f85de-140">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coexistencia](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="f85de-142">No se puede configurar una red virtual como un enrutador de tránsito.</span><span class="sxs-lookup"><span data-stu-id="f85de-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="f85de-143">Seleccionar Hola pasos toouse</span><span class="sxs-lookup"><span data-stu-id="f85de-143">Selecting hello steps toouse</span></span>
<span data-ttu-id="f85de-144">Hay dos conjuntos diferentes de toochoose de procedimientos de en las conexiones de tooconfigure de orden que pueden coexistir.</span><span class="sxs-lookup"><span data-stu-id="f85de-144">There are two different sets of procedures toochoose from in order tooconfigure connections that can coexist.</span></span> <span data-ttu-id="f85de-145">procedimiento de configuración de Hola que seleccione dependerá de si tiene una red virtual existente que desea tooconnect a, o desea toocreate una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="f85de-145">hello configuration procedure that you select will depend on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="f85de-146">No tiene una red virtual y necesita toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="f85de-146">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="f85de-147">Si ya no tiene una red virtual, este procedimiento le guiará a través de la creación de una nueva red virtual mediante el modelo de implementación clásica de Hola y para crear nuevas conexiones de VPN de sitio a sitio y de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f85de-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using hello classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="f85de-148">tooconfigure, siga los pasos en la sección del artículo Hola Hola [toocreate una nueva red virtual y las conexiones coexistentes](#new).</span><span class="sxs-lookup"><span data-stu-id="f85de-148">tooconfigure, follow hello steps in hello article section [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="f85de-149">Ya tengo una red virtual con el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="f85de-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="f85de-150">Puede que ya tenga una red virtual con una conexión VPN de sitio a sitio o una conexión ExpressRoute existentes.</span><span class="sxs-lookup"><span data-stu-id="f85de-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="f85de-151">Hola sección artículo [tooconfigure coexsiting conexiones para una red virtual existente ya](#add) le guiará a través de la eliminación de puerta de enlace de hello y, a continuación, crear nuevas conexiones de ExpressRoute y VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="f85de-151">hello article section [tooconfigure coexsiting connections for an already existing VNet](#add) will walk you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="f85de-152">Tenga en cuenta que al crear nuevas conexiones de hello, pasos de hello deben realizarse en un orden muy específico.</span><span class="sxs-lookup"><span data-stu-id="f85de-152">Note that when creating hello new connections, hello steps must be completed in a very specific order.</span></span> <span data-ttu-id="f85de-153">No utilice instrucciones de hello en otro artículos toocreate sus conexiones y las puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="f85de-153">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="f85de-154">En este procedimiento, creación de conexiones que pueden coexistir necesitarán toodelete la puerta de enlace y, a continuación, configurar nuevas puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="f85de-154">In this procedure, creating connections that can coexist will require you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="f85de-155">Esto significa que tendrá tiempo de inactividad para las conexiones entre entornos al eliminar y volver a crear la puerta de enlace y las conexiones, pero no tendrá que toomigrate cualquiera de su máquinas virtuales o servicios tooa nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="f85de-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="f85de-156">Las máquinas virtuales y servicios se seguirán toocommunicate capaz de salida a través del equilibrador de carga de hello al configurar la puerta de enlace si están toodo configurado así.</span><span class="sxs-lookup"><span data-stu-id="f85de-156">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="f85de-157"><a name="new"></a>toocreate una nueva red virtual y las conexiones coexistentes</span><span class="sxs-lookup"><span data-stu-id="f85de-157"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="f85de-158">Este procedimiento le guiará en la creación de una red virtual y conexiones de sitio a sitio y ExpressRoute que coexistirán.</span><span class="sxs-lookup"><span data-stu-id="f85de-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="f85de-159">Necesitará la versión más reciente de hello tooinstall de hello cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="f85de-159">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="f85de-160">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-160">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="f85de-161">Tenga en cuenta que los cmdlets de Hola que va a utilizar para esta configuración puede ser ligeramente diferentes de lo que es posible que esté familiarizado con.</span><span class="sxs-lookup"><span data-stu-id="f85de-161">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="f85de-162">Cmdlets de hello toouse seguro especificar en estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="f85de-162">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="f85de-163">Cree un esquema para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="f85de-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="f85de-164">Para obtener más información acerca del esquema de configuración de hello, consulte [esquema de configuración de red Virtual de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="f85de-164">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="f85de-165">Cuando se crea el esquema, asegúrese de que utilizar Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="f85de-165">When you create your schema, make sure you use hello following values:</span></span>
   
   * <span data-ttu-id="f85de-166">subred de puerta de enlace de Hello para la red virtual de hello debe ser /27 o un prefijo más corto (por ejemplo, /26 o /25).</span><span class="sxs-lookup"><span data-stu-id="f85de-166">hello gateway subnet for hello virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="f85de-167">tipo de conexión de puerta de enlace de Hola "dedicado".</span><span class="sxs-lookup"><span data-stu-id="f85de-167">hello gateway connection type is "Dedicated".</span></span>
     
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
3. <span data-ttu-id="f85de-168">Después de crear y configurar el archivo de esquema xml, cargar archivo hello.</span><span class="sxs-lookup"><span data-stu-id="f85de-168">After creating and configuring your xml schema file, upload hello file.</span></span> <span data-ttu-id="f85de-169">Esto creará la red virtual.</span><span class="sxs-lookup"><span data-stu-id="f85de-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="f85de-170">Usar hello siguiente cmdlet tooupload el archivo, reemplazando el valor de Hola por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="f85de-170">Use hello following cmdlet tooupload your file, replacing hello value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="f85de-171"><a name="gw"></a>Cree una puerta de enlace de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f85de-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="f85de-172">Ser seguro toospecify Hola GatewaySKU como *estándar*, *HighPerformance*, o *UltraPerformance* y Hola el GatewayType como *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="f85de-172">Be sure toospecify hello GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="f85de-173">Usar hello según muestra, sustituyendo los valores de hello para su propio.</span><span class="sxs-lookup"><span data-stu-id="f85de-173">Use hello following sample, substituting hello values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="f85de-174">Vínculo de circuito de ExpressRoute de toohello de puerta de enlace de ExpressRoute de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-174">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="f85de-175">Una vez completado este paso, se establece la conexión de hello entre la red local y Azure, a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f85de-175">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="f85de-176"><a name="vpngw"></a>A continuación, cree la puerta de enlace de la VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="f85de-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="f85de-177">Hello GatewaySKU debe ser *estándar*, *HighPerformance*, o *UltraPerformance* y hello el GatewayType debe ser *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="f85de-177">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="f85de-178">configuración de puerta de enlace de red virtual de hello tooretrieve, incluidos los Id. de puerta de enlace de Hola y Hola IP pública, usa hello `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f85de-178">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
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
7. <span data-ttu-id="f85de-179">Cree una entidad de puerta de enlace de VPN de sitio local.</span><span class="sxs-lookup"><span data-stu-id="f85de-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="f85de-180">Este comando no configura la puerta de enlace de VPN local.</span><span class="sxs-lookup"><span data-stu-id="f85de-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="f85de-181">En su lugar, permite a tooprovide la configuración de puerta de enlace local hello, como la dirección IP pública de Hola y Hola local espacio de direcciones, por lo que hello puerta de enlace VPN de Azure puede conectarse tooit.</span><span class="sxs-lookup"><span data-stu-id="f85de-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="f85de-182">sitio local Hola Hola VPN de sitio a sitio no está definido en hello netcfg.</span><span class="sxs-lookup"><span data-stu-id="f85de-182">hello local site for hello Site-to-Site VPN is not defined in hello netcfg.</span></span> <span data-ttu-id="f85de-183">En su lugar, debe usar estos parámetros de cmdlet toospecify Hola sitio local.</span><span class="sxs-lookup"><span data-stu-id="f85de-183">Instead, you must use this cmdlet toospecify hello local site parameters.</span></span> <span data-ttu-id="f85de-184">No se puede definir mediante el portal o archivo de netcfg Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-184">You cannot define it using either portal, or hello netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="f85de-185">Usar hello según muestra, reemplazar valores de hello por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="f85de-185">Use hello following sample, replacing hello values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="f85de-186">Si la red local tiene varias rutas, puede pasar todas ellas en una matriz.</span><span class="sxs-lookup"><span data-stu-id="f85de-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="f85de-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="f85de-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="f85de-188">configuración de puerta de enlace de red virtual de hello tooretrieve, incluidos los Id. de puerta de enlace de Hola y Hola IP pública, usa hello `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f85de-188">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="f85de-189">Vea el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-189">See hello following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="f85de-190">Configurar la VPN dispositivo tooconnect toohello nueva puerta de enlace local.</span><span class="sxs-lookup"><span data-stu-id="f85de-190">Configure your local VPN device tooconnect toohello new gateway.</span></span> <span data-ttu-id="f85de-191">Utilice la información de Hola que recuperó en el paso 6 al configurar el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="f85de-191">Use hello information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="f85de-192">Para obtener más información sobre la configuración del dispositivo VPN, vea [Configuración de dispositivos VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="f85de-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="f85de-193">Vínculo Hola VPN de sitio a sitio puerta de enlace en Azure toohello puerta de enlace local.</span><span class="sxs-lookup"><span data-stu-id="f85de-193">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>
   
    <span data-ttu-id="f85de-194">En este ejemplo, connectedEntityId es el Id. de puerta de enlace local de hello, que puede encontrar mediante la ejecución de `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="f85de-194">In this example, connectedEntityId is hello local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="f85de-195">También puede encontrar virtualNetworkGatewayId mediante hello `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f85de-195">You can find virtualNetworkGatewayId by using hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="f85de-196">Después de este paso, se establece la conexión de hello entre la red local y Azure a través de hello conexión VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="f85de-196">After this step, hello connection between your local network and Azure via hello Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="f85de-197"><a name="add"></a>tooconfigure coexsiting conexiones para una red virtual existente</span><span class="sxs-lookup"><span data-stu-id="f85de-197"><a name="add"></a>tooconfigure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="f85de-198">Si tiene una red virtual existente, compruebe el tamaño de subred de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-198">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="f85de-199">Si está en la subred de puerta de enlace de hello /28 o /29, primero debe eliminar la puerta de enlace de red virtual de Hola y aumentar el tamaño de subred de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-199">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="f85de-200">Hello pasos de esta sección le mostrará cómo toodo que.</span><span class="sxs-lookup"><span data-stu-id="f85de-200">hello steps in this section will show you how toodo that.</span></span>

<span data-ttu-id="f85de-201">Si está de subred de puerta de enlace de hello /27 o superior y red virtual de hello está conectado a través de ExpressRoute, puede omitir estos pasos hello y continuar demasiado["Paso 6: crear una puerta de enlace VPN de sitio a sitio"](#vpngw) en la sección anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-201">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="f85de-202">Cuando se elimina la puerta de enlace existente hello, sus instalaciones locales perderá red virtual de hello conexión tooyour mientras se trabaja con esta configuración.</span><span class="sxs-lookup"><span data-stu-id="f85de-202">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="f85de-203">Necesitará la versión más reciente de hello tooinstall de hello cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f85de-203">You'll need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="f85de-204">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información acerca de cómo instalar los cmdlets de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-204">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="f85de-205">Tenga en cuenta que los cmdlets de Hola que va a utilizar para esta configuración puede ser ligeramente diferentes de lo que es posible que esté familiarizado con.</span><span class="sxs-lookup"><span data-stu-id="f85de-205">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="f85de-206">Cmdlets de hello toouse seguro especificar en estas instrucciones.</span><span class="sxs-lookup"><span data-stu-id="f85de-206">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="f85de-207">Eliminar Hola VPN de sitio a sitio o ExpressRoute puerta de enlace existente.</span><span class="sxs-lookup"><span data-stu-id="f85de-207">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="f85de-208">Usar hello siguiente cmdlet, reemplazando los valores de hello con sus propios.</span><span class="sxs-lookup"><span data-stu-id="f85de-208">Use hello following cmdlet, replacing hello values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="f85de-209">Exportar el esquema de la red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-209">Export hello virtual network schema.</span></span> <span data-ttu-id="f85de-210">Usar hello siguiente cmdlet de PowerShell, reemplazar valores de hello por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="f85de-210">Use hello following PowerShell cmdlet, replacing hello values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="f85de-211">Editar el esquema de archivo de configuración de red de Hola para que la subred de puerta de enlace de hello es /27 o un prefijo más corto (por ejemplo, /26 o /25).</span><span class="sxs-lookup"><span data-stu-id="f85de-211">Edit hello network configuration file schema so that hello gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="f85de-212">Vea el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f85de-212">See hello following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f85de-213">Si no tiene suficientes direcciones IP que se mantienen en el tamaño de subred de puerta de enlace de red virtual tooincrease hello, deberá tooadd más espacio de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="f85de-213">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span> <span data-ttu-id="f85de-214">Para obtener más información acerca del esquema de configuración de hello, consulte [esquema de configuración de red Virtual de Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="f85de-214">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="f85de-215">Si la puerta de enlace anterior era una VPN de sitio a sitio, también debe cambiar el tipo de conexión de hello demasiado**dedicado**.</span><span class="sxs-lookup"><span data-stu-id="f85de-215">If your previous gateway was a Site-to-Site VPN, you must also change hello connection type too**Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="f85de-216">Ya tiene una red virtual sin puertas de enlace.</span><span class="sxs-lookup"><span data-stu-id="f85de-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="f85de-217">toocreate nuevas puertas de enlace y completar las conexiones, puede continuar con la [paso 4: crear una puerta de enlace de ExpressRoute](#gw), que se encuentra en hello anterior conjunto de pasos.</span><span class="sxs-lookup"><span data-stu-id="f85de-217">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f85de-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f85de-218">Next steps</span></span>
<span data-ttu-id="f85de-219">Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="f85de-219">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

