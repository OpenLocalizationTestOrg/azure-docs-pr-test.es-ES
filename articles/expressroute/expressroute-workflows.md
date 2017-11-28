---
title: aaaWorkflows para configurar un circuito ExpressRoute | Documentos de Microsoft
description: "Esta página le guiará por los flujos de trabajo de Hola para configurar los emparejamientos y circuito de ExpressRoute"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="74bda-103">Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="74bda-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="74bda-104">Esta página le guiará por el aprovisionamiento del servicio de Hola y enrutamiento flujos de trabajo de configuración en un nivel superior.</span><span class="sxs-lookup"><span data-stu-id="74bda-104">This page walks you through hello service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="74bda-105">Hello siguiente ilustración y los pasos correspondientes muestran tareas de hello que debe seguir en orden toohave una ExpressRoute circuito aprovisionada-to-end.</span><span class="sxs-lookup"><span data-stu-id="74bda-105">hello following figure and corresponding steps show hello tasks you must follow in order toohave an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="74bda-106">Usar PowerShell tooconfigure un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="74bda-106">Use PowerShell tooconfigure an ExpressRoute circuit.</span></span> <span data-ttu-id="74bda-107">Siga las instrucciones de Hola Hola [circuitos ExpressRoute crear](expressroute-howto-circuit-classic.md) artículo para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="74bda-107">Follow hello instructions in hello [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="74bda-108">Conectividad de pedido de proveedor de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="74bda-108">Order connectivity from hello service provider.</span></span> <span data-ttu-id="74bda-109">Este proceso varía.</span><span class="sxs-lookup"><span data-stu-id="74bda-109">This process varies.</span></span> <span data-ttu-id="74bda-110">Póngase en contacto con el proveedor de conectividad para obtener más información acerca de cómo tooorder conectividad.</span><span class="sxs-lookup"><span data-stu-id="74bda-110">Contact your connectivity provider for more details about how tooorder connectivity.</span></span>
3. <span data-ttu-id="74bda-111">Asegúrese de que el circuito de Hola se haya aprovisionado correctamente comprobando el circuito de ExpressRoute de hello estado a través de PowerShell de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="74bda-111">Ensure that hello circuit has been provisioned successfully by verifying hello ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="74bda-112">Configure los dominios de enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="74bda-112">Configure routing domains.</span></span> <span data-ttu-id="74bda-113">Si el proveedor de conectividad administra el nivel 3, configurará el enrutamiento del circuito.</span><span class="sxs-lookup"><span data-stu-id="74bda-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="74bda-114">Si el proveedor de conectividad sólo ofrece servicios de nivel 2, debe configurar el enrutamiento por las directrices descritas en hello [requisitos de enrutamiento](expressroute-routing.md) y [configuración de enrutamiento](expressroute-howto-routing-classic.md) páginas.</span><span class="sxs-lookup"><span data-stu-id="74bda-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in hello [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="74bda-115">Habilitar el emparejamiento privado de Azure, debe habilitar este emparejamiento tooVMs tooconnect / servicios implementados en redes virtuales en la nube.</span><span class="sxs-lookup"><span data-stu-id="74bda-115">Enable Azure private peering - You must enable this peering tooconnect tooVMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="74bda-116">Habilitar pares públicos de Azure: debe habilitar pares públicos de Azure si desea tooconnect tooAzure servicios hospedados en direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="74bda-116">Enable Azure public peering - You must enable Azure public peering if you wish tooconnect tooAzure services hosted on public IP addresses.</span></span> <span data-ttu-id="74bda-117">Se trata de un tooaccess requisito recursos de Azure si ha elegido el enrutamiento de tooenable predeterminado para el nivel privado de Azure.</span><span class="sxs-lookup"><span data-stu-id="74bda-117">This is a requirement tooaccess Azure resources if you have chosen tooenable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="74bda-118">Habilitar el emparejamiento de Microsoft: debe habilitar este tooaccess Office 365 y Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="74bda-118">Enable Microsoft peering - You must enable this tooaccess Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="74bda-119">Debe asegurarse de que usa a un proxy independiente ni borde tooconnect tooMicrosoft de Hola uno que utilice para Hola Internet.</span><span class="sxs-lookup"><span data-stu-id="74bda-119">You must ensure that you use a separate proxy / edge tooconnect tooMicrosoft than hello one you use for hello Internet.</span></span> <span data-ttu-id="74bda-120">Uso de hello borde mismo de ExpressRoute y Hola Internet provocará enrutamiento asimétrico y causar interrupciones de la conectividad de la red.</span><span class="sxs-lookup"><span data-stu-id="74bda-120">Using hello same edge for both ExpressRoute and hello Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="74bda-121">Vinculación virtual redes circuitos tooExpressRoute: puede vincular circuito de ExpressRoute de tooyour de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="74bda-121">Linking virtual networks tooExpressRoute circuits - You can link virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="74bda-122">Siga las instrucciones [toolink redes virtuales](expressroute-howto-linkvnet-arm.md) tooyour circuito.</span><span class="sxs-lookup"><span data-stu-id="74bda-122">Follow instructions [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span></span> <span data-ttu-id="74bda-123">Estas redes virtuales pueden ser Hola misma suscripción de Azure como circuito de ExpressRoute de hello, o puede estar en una suscripción diferente.</span><span class="sxs-lookup"><span data-stu-id="74bda-123">These VNets can either be in hello same Azure subscription as hello ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="74bda-124">Estados de aprovisionamiento de circuitos de ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="74bda-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="74bda-125">Cada circuito ExpressRoute tiene dos estados:</span><span class="sxs-lookup"><span data-stu-id="74bda-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="74bda-126">Estado de aprovisionamiento de proveedor de servicio</span><span class="sxs-lookup"><span data-stu-id="74bda-126">Service provider provisioning state</span></span>
* <span data-ttu-id="74bda-127">Estado</span><span class="sxs-lookup"><span data-stu-id="74bda-127">Status</span></span>

<span data-ttu-id="74bda-128">Estado representa el estado de aprovisionamiento de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="74bda-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="74bda-129">Esta propiedad se establece tooEnabled cuando se crea un circuito Expressroute</span><span class="sxs-lookup"><span data-stu-id="74bda-129">This property is set tooEnabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="74bda-130">estado de aprovisionamiento del proveedor de conectividad de Hello representa el estado de hello en el lado del proveedor de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="74bda-130">hello connectivity provider provisioning state represents hello state on hello connectivity provider's side.</span></span> <span data-ttu-id="74bda-131">Puede ser *No aprovisionado*, *Aprovisionando* o *Aprovisionado*.</span><span class="sxs-lookup"><span data-stu-id="74bda-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="74bda-132">Hola circuito de ExpressRoute debe estar en estado aprovisionado para toobe pueda toouse lo.</span><span class="sxs-lookup"><span data-stu-id="74bda-132">hello ExpressRoute circuit must be in Provisioned state for you toobe able toouse it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="74bda-133">Posibles estados de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="74bda-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="74bda-134">Esta sección se enumeran los posibles estados de Hola por un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="74bda-134">This section lists out hello possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="74bda-135">**En tiempo de creación**</span><span class="sxs-lookup"><span data-stu-id="74bda-135">**At creation time**</span></span>

<span data-ttu-id="74bda-136">Verá circuito de ExpressRoute de Hola Hola después estado tan pronto como se ejecute el circuito de ExpressRoute de hello PowerShell cmdlet toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="74bda-136">You will see hello ExpressRoute circuit in hello following state as soon as you run hello PowerShell cmdlet toocreate hello ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="74bda-137">**Al proveedor de conectividad está en proceso de Hola de aprovisionamiento del circuito de Hola**</span><span class="sxs-lookup"><span data-stu-id="74bda-137">**When connectivity provider is in hello process of provisioning hello circuit**</span></span>

<span data-ttu-id="74bda-138">Verá circuito de ExpressRoute de Hola Hola después estado en cuanto se pase el proveedor de conectividad de toohello clave de servicio de Hola y que se ha iniciado el proceso de aprovisionamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="74bda-138">You will see hello ExpressRoute circuit in hello following state as soon as you pass hello service key toohello connectivity provider and they have started hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="74bda-139">**Cuando proveedor de conectividad ha completado el proceso de aprovisionamiento de Hola**</span><span class="sxs-lookup"><span data-stu-id="74bda-139">**When connectivity provider has completed hello provisioning process**</span></span>

<span data-ttu-id="74bda-140">Verá Hola circuito de ExpressRoute en hello después estado tan pronto como proveedor de conectividad de hello ha completado el proceso de aprovisionamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="74bda-140">You will see hello ExpressRoute circuit in hello following state as soon as hello connectivity provider has completed hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="74bda-141">Aprovisionado y habilitado es hello solo circuito de Hola de estado que puede estar en para toobe pueda toouse.</span><span class="sxs-lookup"><span data-stu-id="74bda-141">Provisioned and Enabled is hello only state hello circuit can be in for you toobe able toouse it.</span></span> <span data-ttu-id="74bda-142">Si usa un proveedor de nivel 2, puede configurar el enrutamiento para el circuito solo cuando se encuentre en este estado.</span><span class="sxs-lookup"><span data-stu-id="74bda-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="74bda-143">**Cuando el proveedor de conectividad desaprovisionamiento circuito Hola**</span><span class="sxs-lookup"><span data-stu-id="74bda-143">**When connectivity provider is deprovisioning hello circuit**</span></span>

<span data-ttu-id="74bda-144">Si se solicita el circuito de ExpressRoute de hello servicio proveedor toodeprovision hello, verá circuito Hola establece toohello después estado una vez completada la Hola proceso de desaprovisionamiento de proveedor de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="74bda-144">If you requested hello service provider toodeprovision hello ExpressRoute circuit, you will see hello circuit set toohello following state after hello service provider has completed hello deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="74bda-145">Puede elegir habilitar toore, si es necesario, o ejecutar los cmdlets de PowerShell circuito de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="74bda-145">You can choose toore-enable it if needed, or run PowerShell cmdlets toodelete hello circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="74bda-146">Si ejecuta Hola circuito de Hola de toodelete de PowerShell cmdlet hello ServiceProviderProvisioningState una vez aprovisionamiento o aprovisionado operación Hola se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="74bda-146">If you run hello PowerShell cmdlet toodelete hello circuit when hello ServiceProviderProvisioningState is Provisioning or Provisioned hello operation will fail.</span></span> <span data-ttu-id="74bda-147">Coopere con el circuito de ExpressRoute de conectividad proveedor toodeprovision hello en primer lugar y, a continuación, eliminar el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="74bda-147">Please work with your connectivity provider toodeprovision hello ExpressRoute circuit first and then delete hello circuit.</span></span> <span data-ttu-id="74bda-148">Microsoft seguirá circuito de hello toobill hasta que ejecute hello circuito de Hola de toodelete de cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="74bda-148">Microsoft will continue toobill hello circuit until you run hello PowerShell cmdlet toodelete hello circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="74bda-149">Estado de configuración de sesión de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="74bda-149">Routing session configuration state</span></span>
<span data-ttu-id="74bda-150">Hola estado de aprovisionamiento de BGP, sabrá si se ha habilitado la sesión BGP de hello en hello borde de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="74bda-150">hello BGP provisioning state lets you know if hello BGP session has been enabled on hello Microsoft edge.</span></span> <span data-ttu-id="74bda-151">Hello estado debe estar habilitado para toobe toouse capaz de hello emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="74bda-151">hello state must be enabled for you toobe able toouse hello peering.</span></span>

<span data-ttu-id="74bda-152">Es importante toocheck estado de sesión BGP de hello especialmente para el emparejamiento de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="74bda-152">It is important toocheck hello BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="74bda-153">En el estado de aprovisionamiento de suma toohello BGP, hay otro estado llamado *anunciados estado prefijos públicos*.</span><span class="sxs-lookup"><span data-stu-id="74bda-153">In addition toohello BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="74bda-154">Hola anunciados estado prefijos públicos debe estar en *configurado* state, tanto para hello BGP sesión toobe seguridad y para su enrutamiento toowork-to-end.</span><span class="sxs-lookup"><span data-stu-id="74bda-154">hello advertised public prefixes state must be in *configured* state, both for hello BGP session toobe up and for your routing toowork end-to-end.</span></span> 

<span data-ttu-id="74bda-155">Si Hola anuncia el estado de prefijo pública se establece tooa *validación necesitado* estado, no está habilitada la sesión BGP de hello, tal como se advierte de hello prefijos no coincidía con hello como número en cualquiera de los registros de enrutamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="74bda-155">If hello advertised public prefix state is set tooa *validation needed* state, hello BGP session is not enabled, as hello advertised prefixes did not match hello AS number in any of hello routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="74bda-156">Si Hola anunciados estado prefijos públicos se encuentra en *validación manual* estado, debe abrir una incidencia de soporte técnico con [soporte técnico de Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) y constituyen una prueba que pertenecen a las direcciones IP Hola anuncian a lo largo de con hello había asociado el número de sistema autónomo.</span><span class="sxs-lookup"><span data-stu-id="74bda-156">If hello advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own hello IP addresses advertised along with hello associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="74bda-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="74bda-157">Next steps</span></span>
* <span data-ttu-id="74bda-158">Configure su conexión ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="74bda-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="74bda-159">Creación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="74bda-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="74bda-160">Configuración del enrutamiento</span><span class="sxs-lookup"><span data-stu-id="74bda-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="74bda-161">Vincular un circuito de ExpressRoute de tooan de red virtual</span><span class="sxs-lookup"><span data-stu-id="74bda-161">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

