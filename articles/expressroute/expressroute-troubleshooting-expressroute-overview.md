---
title: "Comprobación de la conectividad: Guía de solución de problemas de Azure ExpressRoute | Microsoft Docs"
description: "Esta página proporciona instrucciones sobre la solución de problemas y validar la conectividad de tooend de final de un circuito de ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="25718-103">Comprobación de la conectividad de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="25718-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="25718-104">ExpressRoute, que amplía una red local en la nube de Microsoft hello por medio de una conexión privada que se realiza mediante un proveedor de conectividad, implica Hola siguientes a tres zonas de red distintas:</span><span class="sxs-lookup"><span data-stu-id="25718-104">ExpressRoute, which extends an on-premises network into hello Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves hello following three distinct network zones:</span></span>

-   <span data-ttu-id="25718-105">Red del cliente</span><span class="sxs-lookup"><span data-stu-id="25718-105">Customer Network</span></span>
-   <span data-ttu-id="25718-106">Red del proveedor</span><span class="sxs-lookup"><span data-stu-id="25718-106">Provider Network</span></span>
-   <span data-ttu-id="25718-107">Centro de datos de Microsoft</span><span class="sxs-lookup"><span data-stu-id="25718-107">Microsoft Datacenter</span></span>

<span data-ttu-id="25718-108">Hola de este documento sirve toohelp usuario tooidentify donde (o incluso si) existe un problema de conectividad y en qué zona, con lo que se tooseek de Ayuda de problema de equipo adecuada tooresolve Hola.</span><span class="sxs-lookup"><span data-stu-id="25718-108">hello purpose of this document is toohelp user tooidentify where (or even if) a connectivity issue exists and within which zone, thereby tooseek help from appropriate team tooresolve hello issue.</span></span> <span data-ttu-id="25718-109">Si soporte técnico de Microsoft es necesario tooresolve un problema, abra una incidencia de soporte técnico con [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="25718-109">If Microsoft support is needed tooresolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="25718-110">Este documento es toohelp previsto diagnosticar y corregir problemas sencillos.</span><span class="sxs-lookup"><span data-stu-id="25718-110">This document is intended toohelp diagnosing and fixing simple issues.</span></span> <span data-ttu-id="25718-111">No está previsto toobe un sustituto de soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25718-111">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="25718-112">Abra una incidencia de soporte técnico con [Microsoft Support] [ Support] si está toosolve no se puede problema de hello usando la orientación de hello proporcionado.</span><span class="sxs-lookup"><span data-stu-id="25718-112">Open a support ticket with [Microsoft Support][Support] if you are unable toosolve hello problem using hello guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="25718-113">Información general</span><span class="sxs-lookup"><span data-stu-id="25718-113">Overview</span></span>
<span data-ttu-id="25718-114">Hello siguiente diagrama muestra hello lógica a la conectividad de una red de tooMicrosoft de red de cliente mediante ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="25718-114">hello following diagram shows hello logical connectivity of a customer network tooMicrosoft network using ExpressRoute.</span></span>
<span data-ttu-id="25718-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="25718-115">[![1]][1]</span></span>

<span data-ttu-id="25718-116">Hola anterior diagrama, los números de hello indican puntos clave de red.</span><span class="sxs-lookup"><span data-stu-id="25718-116">In hello preceding diagram, hello numbers indicate key network points.</span></span> <span data-ttu-id="25718-117">puntos de la red de Hola se hace referencia a menudo a través de este artículo por su número asociado.</span><span class="sxs-lookup"><span data-stu-id="25718-117">hello network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="25718-118">Según la conectividad de ExpressRoute de hello modelo (ubicación compartida de Exchange en la nube, conexión Ethernet de punto a punto o (IPVPN) y a cualquier) Hola red puntos 3 y 4 pueden ser conmutadores (dispositivos de capa 2).</span><span class="sxs-lookup"><span data-stu-id="25718-118">Depending on hello ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) hello network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="25718-119">puntos clave Hola se muestra son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="25718-119">hello key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="25718-120">Dispositivo de proceso del cliente (por ejemplo, un servidor o equipo)</span><span class="sxs-lookup"><span data-stu-id="25718-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="25718-121">CE: enrutadores en el lado del cliente</span><span class="sxs-lookup"><span data-stu-id="25718-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="25718-122">PE (hacia los CE): enrutadores o conmutadores del lado del proveedor orientados hacia los enrutadores del lado del cliente.</span><span class="sxs-lookup"><span data-stu-id="25718-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="25718-123">Conoce tooas PE CEs en este documento.</span><span class="sxs-lookup"><span data-stu-id="25718-123">Referred tooas PE-CEs in this document.</span></span>
4.  <span data-ttu-id="25718-124">PE (hacia los MSEE): enrutadores o conmutadores del lado del proveedor orientados hacia los MSEE.</span><span class="sxs-lookup"><span data-stu-id="25718-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="25718-125">Conoce tooas PE MSEEs en este documento.</span><span class="sxs-lookup"><span data-stu-id="25718-125">Referred tooas PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="25718-126">MSEEs: enrutadores de Microsoft Enterprise Edge (MSEE) ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="25718-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="25718-127">Puerta de enlace de Virtual Network (VNet)</span><span class="sxs-lookup"><span data-stu-id="25718-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="25718-128">Dispositivo de red virtual de Azure Hola de proceso</span><span class="sxs-lookup"><span data-stu-id="25718-128">Compute device on hello Azure VNet</span></span>

<span data-ttu-id="25718-129">Si se utilizan los modelos de conectividad de colocación de Exchange para la nube o una conexión Ethernet de punto a punto de hello, enrutador perimetral de cliente hello (2) ¿establecer BGP emparejamiento con MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="25718-129">If hello Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, hello customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="25718-130">Los puntos de red 3 y 4 todavía existirán, pero serán transparentes de forma parecida a los dispositivos de capa 2.</span><span class="sxs-lookup"><span data-stu-id="25718-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="25718-131">Si se usa el modelo de conectividad de Hola y a cualquier (IPVPN), Hola PEs (MSEE con conexión a) (4) podría establecer BGP emparejamiento con MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="25718-131">If hello Any-to-any (IPVPN) connectivity model is used, hello PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="25718-132">Las rutas, a continuación, podrían propagar toohello atrás de red de cliente a través de la red del proveedor de servicio de hello IPVPN.</span><span class="sxs-lookup"><span data-stu-id="25718-132">Routes would then propagate back toohello customer network via hello IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="25718-133">Para lograr la alta disponibilidad de ExpressRoute, Microsoft requiere un par redundante de sesiones BGP entre los MSEE (5) y los PE-MSEE (4).</span><span class="sxs-lookup"><span data-stu-id="25718-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="25718-134">También se recomienda establecer un par redundante de rutas de red entre la red del cliente y los PE-CE.</span><span class="sxs-lookup"><span data-stu-id="25718-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="25718-135">Sin embargo, en el modelo de conexión y a cualquier (IPVPN), un único dispositivo CE (2) pueden tooone conectado o más PEs (3).</span><span class="sxs-lookup"><span data-stu-id="25718-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected tooone or more PEs (3).</span></span>
>
>

<span data-ttu-id="25718-136">toovalidate un circuito de ExpressRoute, Hola pasos se tratan (con el punto de red de hello indicado por el número de asociados de hello):</span><span class="sxs-lookup"><span data-stu-id="25718-136">toovalidate an ExpressRoute circuit, hello following steps are covered (with hello network point indicated by hello associated number):</span></span>
1. [<span data-ttu-id="25718-137">Validación del aprovisionamiento y el estado del circuito (5)</span><span class="sxs-lookup"><span data-stu-id="25718-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="25718-138">Validación de que hay al menos un emparejamiento de ExpressRoute configurado (5)</span><span class="sxs-lookup"><span data-stu-id="25718-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="25718-139">Validar a ARP entre el proveedor de servicios de Microsoft y hello (vínculo entre 4 y 5)</span><span class="sxs-lookup"><span data-stu-id="25718-139">Validate ARP between Microsoft and hello service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="25718-140">Validar BGP y las rutas de hello MSEE (BGP entre too5 4 y 5 too6 si está conectada a una red virtual)</span><span class="sxs-lookup"><span data-stu-id="25718-140">Validate BGP and routes on hello MSEE (BGP between 4 too5, and 5 too6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="25718-141">Hola de comprobación de las estadísticas de tráfico (tráfico que pasa a través de 5)</span><span class="sxs-lookup"><span data-stu-id="25718-141">Check hello Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="25718-142">Más validaciones y comprobaciones se agregarán en hello futuras, consulte esta página mensualmente!</span><span class="sxs-lookup"><span data-stu-id="25718-142">More validations and checks will be added in hello future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="25718-143">Validación del aprovisionamiento y el estado del circuito</span><span class="sxs-lookup"><span data-stu-id="25718-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="25718-144">Independientemente del modelo de conectividad a hello, tiene un circuito ExpressRoute toobe creado y, por tanto, un servicio en la clave generada para el aprovisionamiento del circuito.</span><span class="sxs-lookup"><span data-stu-id="25718-144">Regardless of hello connectivity model, an ExpressRoute circuit has toobe created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="25718-145">El aprovisionamiento de un circuito ExpressRoute establece conexiones redundantes de capa 2 entre los PE-MSEE (4) y los MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="25718-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="25718-146">Para obtener más información acerca de cómo toocreate, modificar, aprovisionar y comprobar un circuito ExpressRoute, consulte el artículo de hello [crear y modificar un circuito ExpressRoute][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="25718-146">For more information on how toocreate, modify, provision, and verify an ExpressRoute circuit, see hello article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="25718-147">Una clave de servicio identifica de forma única un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="25718-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="25718-148">Esta clave es necesaria para la mayoría de los comandos de powershell de hello mencionados en este documento.</span><span class="sxs-lookup"><span data-stu-id="25718-148">This key is required for most of hello powershell commands mentioned in this document.</span></span> <span data-ttu-id="25718-149">Además, si necesita asistencia de Microsoft o de un tootroubleshoot de socio comercial de ExpressRoute un problema de ExpressRoute, proporcionar servicio hello tooreadily clave identificar circuito Hola.</span><span class="sxs-lookup"><span data-stu-id="25718-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner tootroubleshoot an ExpressRoute issue, provide hello service key tooreadily identify hello circuit.</span></span>
>
>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="25718-150">Comprobación a través de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="25718-150">Verification via hello Azure portal</span></span>
<span data-ttu-id="25718-151">Hola portal de Azure, se puede comprobar el estado Hola de un circuito ExpressRoute seleccionando ![2][2] en hello menú de barra de lado izquierda y, a continuación, seleccionando Hola circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="25718-151">In hello Azure portal, hello status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="25718-152">Al seleccionar una ExpressRoute circuito aparecen en "Todos los recursos" abre una hoja de circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="25718-152">Selecting an ExpressRoute circuit listed under "All resources" opens hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="25718-153">Hola ![3][3] sección de hoja de hello, hello ExpressRoute essentials aparecen como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="25718-153">In hello ![3][3] section of hello blade, hello ExpressRoute essentials are listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="25718-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="25718-154">![4][4]</span></span>    

<span data-ttu-id="25718-155">Hola Essentials de ExpressRoute, *Circuit estado* indica el estado de saludo del circuito de hello en hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25718-155">In hello ExpressRoute Essentials, *Circuit status* indicates hello status of hello circuit on hello Microsoft side.</span></span> <span data-ttu-id="25718-156">*Estado del proveedor* indica si se ha circuito hello *aprovisionado/no aprovisionado* en lado de proveedor de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="25718-156">*Provider status* indicates if hello circuit has been *Provisioned/Not provisioned* on hello service-provider side.</span></span> 

<span data-ttu-id="25718-157">Para toobe de circuito ExpressRoute operativa, Hola *Circuit estado* debe ser *habilitado* hello y *estado del proveedor* debe ser *aprovisionado*.</span><span class="sxs-lookup"><span data-stu-id="25718-157">For an ExpressRoute circuit toobe operational, hello *Circuit status* must be *Enabled* and hello *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="25718-158">Si hello *Circuit estado* no es habilitado, póngase en contacto con [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="25718-158">If hello *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="25718-159">Si hello *estado del proveedor* no es aprovisionado, póngase en contacto con su proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="25718-159">If hello *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="25718-160">Comprobación a través de PowerShell</span><span class="sxs-lookup"><span data-stu-id="25718-160">Verification via PowerShell</span></span>
<span data-ttu-id="25718-161">toolist Hola a todos los circuitos ExpressRoute en un grupo de recursos, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25718-161">toolist all hello ExpressRoute circuits in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="25718-162">Puede obtener el nombre del grupo de recursos a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="25718-162">You can get your resource group name through hello Azure portal.</span></span> <span data-ttu-id="25718-163">Vea Hola subsección anterior de este documento y tenga en cuenta que ese nombre de grupo de recursos de Hola se muestra en la captura de pantalla de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="25718-163">See hello previous subsection of this document and note that hello resource group name is listed in hello example screen shot.</span></span>
>
>

<span data-ttu-id="25718-164">tooselect un circuito de ExpressRoute determinado en un grupo de recursos, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25718-164">tooselect a particular ExpressRoute circuit in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="25718-165">Una respuesta de ejemplo es:</span><span class="sxs-lookup"><span data-stu-id="25718-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="25718-166">tooconfirm si un circuito ExpressRoute está operativo, preste toohello especial atención siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="25718-166">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="25718-167">Si hello *CircuitProvisioningState* no es habilitado, póngase en contacto con [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="25718-167">If hello *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="25718-168">Si hello *ServiceProviderProvisioningState* no es aprovisionado, póngase en contacto con su proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="25718-168">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="25718-169">Comprobación a través de PowerShell (Clásico)</span><span class="sxs-lookup"><span data-stu-id="25718-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="25718-170">toolist Hola a todos los circuitos ExpressRoute en una suscripción, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25718-170">toolist all hello ExpressRoute circuits under a subscription, use hello following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="25718-171">tooselect un circuito de ExpressRoute determinado, use Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25718-171">tooselect a particular ExpressRoute circuit, use hello following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="25718-172">Una respuesta de ejemplo es:</span><span class="sxs-lookup"><span data-stu-id="25718-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="25718-173">tooconfirm si está operativo, un circuito ExpressRoute pagar toohello especial atención siguientes campos: ServiceProviderProvisioningState: estado de aprovisionamiento: habilitado</span><span class="sxs-lookup"><span data-stu-id="25718-173">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="25718-174">Si hello *estado* no es habilitado, póngase en contacto con [Microsoft Support][Support].</span><span class="sxs-lookup"><span data-stu-id="25718-174">If hello *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="25718-175">Si hello *ServiceProviderProvisioningState* no es aprovisionado, póngase en contacto con su proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="25718-175">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="25718-176">Validación de la configuración de emparejamiento</span><span class="sxs-lookup"><span data-stu-id="25718-176">Validate Peering Configuration</span></span>
<span data-ttu-id="25718-177">Después de que el proveedor de servicios de hello tiene completado Hola aprovisionamiento del circuito de ExpressRoute de hello, se pueden crear una configuración de enrutamiento en hello circuito de ExpressRoute entre MSEE-PR (4) y MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="25718-177">After hello service provider has completed hello provisioning hello ExpressRoute circuit, a routing configuration can be created over hello ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="25718-178">Cada circuito de ExpressRoute puede tener uno, dos o tres contextos de enrutamiento habilitados: el emparejamiento privado Azure (tráfico tooprivate redes virtuales en Azure), el emparejamiento público Azure (direcciones IP de tráfico toopublic en Azure) y (tráfico tooOffice 365 de emparejamiento de Microsoft y Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="25718-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic tooprivate virtual networks in Azure), Azure public peering (traffic toopublic IP addresses in Azure), and Microsoft peering (traffic tooOffice 365 and Dynamics 365).</span></span> <span data-ttu-id="25718-179">Para obtener más información acerca de cómo toocreate y modificar la configuración de enrutamiento, consulte el artículo de hello [crear y modificar el enrutamiento de un circuito de ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="25718-179">For more information on how toocreate and modify routing configuration, see hello article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="25718-180">Comprobación a través de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="25718-180">Verification via hello Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="25718-181">Hay un problema conocido en hello portal de Azure donde están los emparejamientos de ExpressRoute *no* muestran en el portal de hello si configurado por el proveedor de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="25718-181">There is a known bug in hello Azure portal wherein ExpressRoute peerings are *NOT* shown in hello portal if configured by hello service provider.</span></span> <span data-ttu-id="25718-182">Adición de emparejamientos de ExpressRoute a través del portal de Hola o PowerShell *sobrescribe la configuración del proveedor de servicio de hello*.</span><span class="sxs-lookup"><span data-stu-id="25718-182">Adding ExpressRoute peerings via hello portal or PowerShell *overwrites hello service provider settings*.</span></span> <span data-ttu-id="25718-183">Esta acción interrumpe Hola enrutamiento en el circuito de ExpressRoute de Hola y requiere soporte de Hola Hola proveedor toorestore Hola de opciones de servicios y restablecer la distribución normal.</span><span class="sxs-lookup"><span data-stu-id="25718-183">This action breaks hello routing on hello ExpressRoute circuit and requires hello support of hello service provider toorestore hello settings and reestablish normal routing.</span></span> <span data-ttu-id="25718-184">Modificar solo hello ExpressRoute emparejamientos si que dicho proveedor de servicios de hello proporciona servicios de nivel 2 solo!</span><span class="sxs-lookup"><span data-stu-id="25718-184">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="25718-185">Si capa 3 se proporciona por hello emparejamientos de hello y proveedor de servicio están en blanco en el portal de hello, PowerShell puede ser usado toosee Hola servicio proveedor configurado configuración.</span><span class="sxs-lookup"><span data-stu-id="25718-185">If layer 3 is provided by hello service provider and hello peerings are blank in hello portal, PowerShell can be used toosee hello service provider configured settings.</span></span>
>
>

<span data-ttu-id="25718-186">Hola portal de Azure, se puede comprobar el estado de un circuito ExpressRoute seleccionando ![2][2] en hello menú de barra de lado izquierda y, a continuación, seleccionando Hola circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="25718-186">In hello Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="25718-187">Al seleccionar una ExpressRoute circuito aparecen en "Todos los recursos" abriría hoja de circuito de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="25718-187">Selecting an ExpressRoute circuit listed under "All resources" would open hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="25718-188">Hola ![3][3] sección de hoja de hello, hello ExpressRoute essentials aparecerá como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="25718-188">In hello ![3][3] section of hello blade, hello ExpressRoute essentials would be listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="25718-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="25718-189">![5][5]</span></span>

<span data-ttu-id="25718-190">En el anterior ejemplo de Hola, como se indicó Azure privada emparejamiento enrutamiento se ha habilitado el contexto, mientras que Azure pública y contextos de enrutamiento de emparejamiento de Microsoft no están habilitadas.</span><span class="sxs-lookup"><span data-stu-id="25718-190">In hello preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="25718-191">Un contexto de emparejamiento se habilitó correctamente también tendría subredes de punto a punto principal y secundaria (requerido para BGP) Hola enumerados.</span><span class="sxs-lookup"><span data-stu-id="25718-191">A successfully enabled peering context would also have hello primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="25718-192">subredes de Hello /30 se usan para dirección IP de la interfaz de Hola de hello MSEEs y MSEEs PE.</span><span class="sxs-lookup"><span data-stu-id="25718-192">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="25718-193">Si no está habilitado un emparejamiento, compruebe si coincide con subredes principal y secundaria de hello asignadas configuración hello en MSEEs PE.</span><span class="sxs-lookup"><span data-stu-id="25718-193">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on PE-MSEEs.</span></span> <span data-ttu-id="25718-194">Si no es así, toochange Hola configuración en los enrutadores MSEE, consulte demasiado[crear y modificar el enrutamiento de un circuito de ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="25718-194">If not, toochange hello configuration on MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="25718-195">Comprobación a través de PowerShell</span><span class="sxs-lookup"><span data-stu-id="25718-195">Verification via PowerShell</span></span>
<span data-ttu-id="25718-196">tooget hello Azure privada emparejamiento detalles de configuración, utilice Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="25718-196">tooget hello Azure private peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="25718-197">Una respuesta de ejemplo para un emparejamiento privado configurado correctamente es:</span><span class="sxs-lookup"><span data-stu-id="25718-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="25718-198">Un contexto de emparejamiento se habilitó correctamente tendría prefijos de dirección principal y secundaria de hello enumerados.</span><span class="sxs-lookup"><span data-stu-id="25718-198">A successfully enabled peering context would have hello primary and secondary address prefixes listed.</span></span> <span data-ttu-id="25718-199">subredes de Hello /30 se usan para dirección IP de la interfaz de Hola de hello MSEEs y MSEEs PE.</span><span class="sxs-lookup"><span data-stu-id="25718-199">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="25718-200">tooget hello Azure pública emparejamiento detalles de configuración, utilice Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="25718-200">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="25718-201">tooget Hola emparejamiento configuración detalles de Microsoft, use Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="25718-201">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="25718-202">Si no se configura un emparejamiento, aparecerá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="25718-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="25718-203">Una respuesta de ejemplo, cuando Hola indique emparejamiento (públicos de Azure emparejamiento en este ejemplo) no está configurada en el circuito de hello:</span><span class="sxs-lookup"><span data-stu-id="25718-203">A sample response, when hello stated peering (Azure Public peering in this example) is not configured within hello circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="25718-204">Si no está habilitado un emparejamiento, comprobar si Hola principal y secundaria subredes asignadas coincidencia Hola configuración en hello vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="25718-204">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="25718-205">También compruebe si hello corregir *VlanId*, *AzureASN*, y *PeerASN* se utilizan en MSEEs y si estos valores se asigna toohello aquellas que se usan en hello vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="25718-205">Also check if hello correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="25718-206">Si se elige el hash MD5, una clave compartida Hola debe coincidir en MSEE y PE MSEE par.</span><span class="sxs-lookup"><span data-stu-id="25718-206">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="25718-207">la configuración de hello toochange en los enrutadores MSEE hello, demasiado, consulte [crear y modificar el enrutamiento por un circuito ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="25718-207">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="25718-208">Comprobación a través de PowerShell (Clásico)</span><span class="sxs-lookup"><span data-stu-id="25718-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="25718-209">Hola tooget Azure privada emparejamiento detalles de configuración, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25718-209">tooget hello Azure private peering configuration details, use hello following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="25718-210">Una respuesta de ejemplo de un emparejamiento privado configurado correctamente es:</span><span class="sxs-lookup"><span data-stu-id="25718-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="25718-211">Se ha habilitado correctamente, un contexto emparejamiento tendría subredes del mismo nivel principal y secundaria de hello enumerados.</span><span class="sxs-lookup"><span data-stu-id="25718-211">A successfully, enabled peering context would have hello primary and secondary peer subnets listed.</span></span> <span data-ttu-id="25718-212">subredes de Hello /30 se usan para dirección IP de la interfaz de Hola de hello MSEEs y MSEEs PE.</span><span class="sxs-lookup"><span data-stu-id="25718-212">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="25718-213">tooget hello Azure pública emparejamiento detalles de configuración, utilice Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="25718-213">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="25718-214">tooget Hola emparejamiento configuración detalles de Microsoft, use Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="25718-214">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="25718-215">Si emparejamientos de capa 3 se establecieron por el proveedor de servicios de hello, establecer Hola emparejamientos de ExpressRoute a través del portal de Hola o PowerShell sobrescribe la configuración del proveedor de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="25718-215">If layer 3 peerings were set by hello service provider, setting hello ExpressRoute peerings via hello portal or PowerShell overwrites hello service provider settings.</span></span> <span data-ttu-id="25718-216">Restablecer la configuración de emparejamiento de lado de proveedor de hello requiere soporte de Hola Hola del proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="25718-216">Resetting hello provider side peering settings requires hello support of hello service provider.</span></span> <span data-ttu-id="25718-217">Modificar solo hello ExpressRoute emparejamientos si que dicho proveedor de servicios de hello proporciona servicios de nivel 2 solo!</span><span class="sxs-lookup"><span data-stu-id="25718-217">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="25718-218">Si no está habilitado un emparejamiento, comprobar si configuración Hola del mismo nivel principal y secundaria subredes asignadas coincidencia hello en hello vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="25718-218">If a peering is not enabled, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="25718-219">También compruebe si hello corregir *VlanId*, *AzureAsn*, y *PeerAsn* se utilizan en MSEEs y si estos valores se asigna toohello aquellas que se usan en hello vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="25718-219">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="25718-220">la configuración de hello toochange en los enrutadores MSEE hello, demasiado, consulte [crear y modificar el enrutamiento por un circuito ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="25718-220">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a><span data-ttu-id="25718-221">Validar a ARP entre el proveedor de servicios de Microsoft y Hola</span><span class="sxs-lookup"><span data-stu-id="25718-221">Validate ARP between Microsoft and hello service provider</span></span>
<span data-ttu-id="25718-222">Esta sección utiliza comandos de PowerShell (clásico).</span><span class="sxs-lookup"><span data-stu-id="25718-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="25718-223">Si ha estado utilizando los comandos del Administrador de recursos de Azure PowerShell, asegúrese de que dispone de acceso de administrador o Coadministrador toohello suscripción a través de [portal de Azure clásico][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="25718-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="25718-224">Para solucionar problemas con el Administrador de recursos de Azure comandos, consulte toohello [tablas de ARP obtener en el modelo de implementación del Administrador de recursos de hello] [ ARP] documento.</span><span class="sxs-lookup"><span data-stu-id="25718-224">For troubleshooting using Azure Resource Manager commands please refer toohello [Getting ARP tables in hello Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="25718-225">se puede utilizar tooget ARP, Hola portal de Azure y comandos de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="25718-225">tooget ARP, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="25718-226">Si se producen errores con los comandos de PowerShell del Administrador de recursos de Azure de hello, comandos de PowerShell clásicos deben funcionar como PowerShell clásico comandos también funcionan con circuitos ExpressRoute de administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="25718-226">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="25718-227">tooget Hola tabla ARP del enrutador MSEE principal de hello para el nivel privado de hello, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25718-227">tooget hello ARP table from hello primary MSEE router for hello private peering, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="25718-228">Una respuesta de ejemplo de comando de hello, en caso de éxito hello:</span><span class="sxs-lookup"><span data-stu-id="25718-228">An example response for hello command, in hello successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="25718-229">De forma similar, puede comprobar la tabla ARP de hello MSEE Hola Hola *principal*/*secundaria* ruta de acceso, para *privada* /  *Pública*/*Microsoft* emparejamientos.</span><span class="sxs-lookup"><span data-stu-id="25718-229">Similarly, you can check hello ARP table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="25718-230">Hello el ejemplo siguiente se muestra hello respuesta del comando de Hola para un emparejamiento no existe.</span><span class="sxs-lookup"><span data-stu-id="25718-230">hello following example shows hello response of hello command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="25718-231">Si no dispone de hello tabla ARP direcciones IP de interfaces de hello asignan direcciones tooMAC, Hola revisión siguiente información:</span><span class="sxs-lookup"><span data-stu-id="25718-231">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
>1. <span data-ttu-id="25718-232">Si Hola primera asignará dirección IP de subred de hello /30 para hello vínculo entre Hola PR MSEE y MSEE se utiliza en la interfaz de Hola de MSEE de int</span><span class="sxs-lookup"><span data-stu-id="25718-232">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="25718-233">Azure usa siempre la dirección IP de la segunda Hola para MSEEs.</span><span class="sxs-lookup"><span data-stu-id="25718-233">Azure always uses hello second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="25718-234">Compruebe si Hola cliente (C-Tag) y las etiquetas VLAN de servicio (S-Tag) coinciden con ambos en par MSEE PR y MSEE.</span><span class="sxs-lookup"><span data-stu-id="25718-234">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a><span data-ttu-id="25718-235">Validar BGP y las rutas de hello MSEE</span><span class="sxs-lookup"><span data-stu-id="25718-235">Validate BGP and routes on hello MSEE</span></span>
<span data-ttu-id="25718-236">Esta sección utiliza comandos de PowerShell (clásico).</span><span class="sxs-lookup"><span data-stu-id="25718-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="25718-237">Si ha estado utilizando los comandos del Administrador de recursos de Azure PowerShell, asegúrese de que dispone de acceso de administrador o Coadministrador toohello suscripción a través de [portal de Azure clásico][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="25718-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="25718-238">tooget información sobre BGP, ambos Hola portal de Azure y comandos de PowerShell del Administrador de recursos de Azure se pueden usar.</span><span class="sxs-lookup"><span data-stu-id="25718-238">tooget BGP information, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="25718-239">Si se producen errores con los comandos de PowerShell del Administrador de recursos de Azure de hello, comandos de PowerShell clásicos deben funcionar como PowerShell clásico comandos también funcionan con circuitos ExpressRoute de administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="25718-239">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="25718-240">tooget Hola tabla de enrutamiento (vecino BGP) resumen para un determinado contexto de enrutamiento, usar hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25718-240">tooget hello routing table (BGP neighbor) summary for a particular routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="25718-241">Ejemplo de respuesta:</span><span class="sxs-lookup"><span data-stu-id="25718-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="25718-242">Tal y como se muestra en el anterior ejemplo de Hola, comando hello es útil toodetermine de cuánto tiempo se ha establecido el contexto de enrutamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="25718-242">As shown in hello preceding example, hello command is useful toodetermine for how long hello routing context has been established.</span></span> <span data-ttu-id="25718-243">También indica el número de prefijos de rutas que anuncia Hola emparejamiento enrutador.</span><span class="sxs-lookup"><span data-stu-id="25718-243">It also indicates number of route prefixes advertised by hello peering router.</span></span>

>[!NOTE]
><span data-ttu-id="25718-244">Si el estado de hello en activo o inactivo, comprobar si configuración Hola del mismo nivel principal y secundaria subredes asignadas coincidencia hello en hello vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="25718-244">If hello state is in Active or Idle, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="25718-245">También compruebe si hello corregir *VlanId*, *AzureAsn*, y *PeerAsn* se utilizan en MSEEs y si estos valores se asigna toohello aquellas que se usan en hello vinculado MSEE PE.</span><span class="sxs-lookup"><span data-stu-id="25718-245">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="25718-246">Si se elige el hash MD5, una clave compartida Hola debe coincidir en MSEE y PE MSEE par.</span><span class="sxs-lookup"><span data-stu-id="25718-246">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="25718-247">la configuración de hello toochange en los enrutadores MSEE hello, demasiado, consulte[crear y modificar el enrutamiento de un circuito de ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="25718-247">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="25718-248">Si algunos destinos no son accesibles a través de un emparejamiento determinado, compruebe la tabla de rutas de Hola de MSEEs Hola que pertenecen a ese contexto concreto emparejamiento toohello.</span><span class="sxs-lookup"><span data-stu-id="25718-248">If certain destinations are not reachable over a particular peering, check hello route table of hello MSEEs belonging toohello particular peering context.</span></span> <span data-ttu-id="25718-249">Si un prefijo coincidente (podría ser NATed IP) se encuentra en la tabla de enrutamiento de hello, a continuación, compruebe si hay firewalls/NSG/ACL en la ruta de acceso de Hola y permitir el tráfico de Hola.</span><span class="sxs-lookup"><span data-stu-id="25718-249">If a matching prefix (could be NATed IP) is present in hello routing table, then check if there are firewalls/NSG/ACLs on hello path and if they permit hello traffic.</span></span>
>
>

<span data-ttu-id="25718-250">tooget Hola completa tabla de enrutamiento de MSEE hello *principal* ruta de acceso de hello determinado *privada* contexto de enrutamiento, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25718-250">tooget hello full routing table from MSEE on hello *Primary* path for hello particular *Private* routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="25718-251">Es un resultado correcto de ejemplo de comando de hello:</span><span class="sxs-lookup"><span data-stu-id="25718-251">An example successful outcome for hello command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="25718-252">De forma similar, puede comprobar la tabla de enrutamiento de Hola de hello MSEE Hola *principal*/*secundaria* ruta de acceso, para *privada* / *Pública*/*Microsoft* un contexto de emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="25718-252">Similarly, you can check hello routing table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="25718-253">Hello el ejemplo siguiente se muestra hello respuesta del comando de Hola para un emparejamiento no existe:</span><span class="sxs-lookup"><span data-stu-id="25718-253">hello following example shows hello response of hello command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a><span data-ttu-id="25718-254">Hola de comprobación de las estadísticas de tráfico</span><span class="sxs-lookup"><span data-stu-id="25718-254">Check hello Traffic Statistics</span></span>
<span data-ttu-id="25718-255">Hola tooget combina estadísticas de tráfico de la ruta de acceso principal y secundaria: bytes de entrada y salida, de un contexto de intercambio de tráfico, Hola de uso siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25718-255">tooget hello combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="25718-256">Es un resultado de ejemplo de Hola comando:</span><span class="sxs-lookup"><span data-stu-id="25718-256">A sample output of hello command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="25718-257">Es un resultado de ejemplo de comando de Hola para un emparejamiento inexistente:</span><span class="sxs-lookup"><span data-stu-id="25718-257">A sample output of hello command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="25718-258">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25718-258">Next Steps</span></span>
<span data-ttu-id="25718-259">Para obtener más información o ayuda, visite Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="25718-259">For more information or help, check out hello following links:</span></span>

- <span data-ttu-id="25718-260">[Ayuda y soporte técnico de Microsoft][Support]</span><span class="sxs-lookup"><span data-stu-id="25718-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="25718-261">[Creación y modificación de un circuito ExpressRoute][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="25718-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="25718-262">[Creación y modificación del enrutamiento de un circuito ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="25718-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity" (Conectividad lógica de Expressroute)
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Icono All resources"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Icono Overview"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Captura de pantalla de ejemplo de Essentials de ExpressRoute"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Captura de pantalla de ejemplo de Essentials de ExpressRoute"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






