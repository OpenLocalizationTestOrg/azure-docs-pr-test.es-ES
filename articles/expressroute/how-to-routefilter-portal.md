---
title: "Configuración de filtros de ruta para el emparejamiento de Microsoft de Azure ExpressRoute: Portal | Microsoft Docs"
description: "Este artículo describe cómo tooconfigure filtros de ruta para el uso de Microsoft Peering Hola portal de Azure"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="55184-103">Configuración de filtros de ruta para el emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="55184-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="55184-104">Filtros de ruta son un tooconsume de manera un subconjunto de servicios admitidos a través de emparejamiento de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="55184-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="55184-105">Hola pasos de este artículo le ayudarán a configura y administra filtros de ruta para los circuitos ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="55184-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="55184-106">Servicios de Dynamics 365 y servicios de Office 365 como Exchange Online, SharePoint Online y Skype empresarial, son accesibles a través de emparejamiento de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="55184-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="55184-107">Cuando se configura el emparejamiento de Microsoft en un circuito ExpressRoute, todos los servicios de toothese relacionados de prefijos se anuncian a través de sesiones BGP de Hola que se establecen.</span><span class="sxs-lookup"><span data-stu-id="55184-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="55184-108">Un valor de la Comunidad BGP es tooevery adjunto prefijo tooidentify Hola servicio se ofrece a través de prefijo de Hola.</span><span class="sxs-lookup"><span data-stu-id="55184-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="55184-109">Para obtener una lista de valores de comunidad BGP de Hola y servicios de Hola que se asignan, vea [Comunidades BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="55184-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="55184-110">Si necesita conectividad tooall servicios, un gran número de prefijos se anuncia a través de BGP.</span><span class="sxs-lookup"><span data-stu-id="55184-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="55184-111">Esto aumenta significativamente el tamaño de Hola Hola de tablas de rutas mantenido por enrutadores dentro de la red.</span><span class="sxs-lookup"><span data-stu-id="55184-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="55184-112">Si tiene previsto tooconsume solo un subconjunto de servicios ofrece a través de emparejamiento de Microsoft, puede reducir el tamaño de Hola de las tablas de enrutamiento de dos maneras.</span><span class="sxs-lookup"><span data-stu-id="55184-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="55184-113">Puede:</span><span class="sxs-lookup"><span data-stu-id="55184-113">You can:</span></span>

- <span data-ttu-id="55184-114">Filtrar los prefijos no deseados mediante la aplicación de filtros de ruta en las comunidades de BGP.</span><span class="sxs-lookup"><span data-stu-id="55184-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="55184-115">Este es un procedimiento de red estándar y se usa normalmente en muchas redes.</span><span class="sxs-lookup"><span data-stu-id="55184-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="55184-116">Definir filtros de ruta y aplicarlas tooyour circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="55184-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="55184-117">Un filtro de ruta es un recurso nuevo que permite seleccionar una lista de hello de servicios planee tooconsume a través de emparejamiento de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="55184-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="55184-118">Enrutadores de ExpressRoute solo envían lista Hola de prefijos que pertenecen a los servicios de toohello identificados en el filtro de ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="55184-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="55184-119"><a name="about"></a>Acerca de los filtros de ruta</span><span class="sxs-lookup"><span data-stu-id="55184-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="55184-120">Cuando se configura el emparejamiento de Microsoft en el circuito de ExpressRoute, enrutadores de borde de Microsoft hello establecen un par de sesiones de BGP con enrutadores de borde de hello (usted o el proveedor de conectividad).</span><span class="sxs-lookup"><span data-stu-id="55184-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="55184-121">No hay rutas son redes de tooyour anunciado.</span><span class="sxs-lookup"><span data-stu-id="55184-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="55184-122">red de tooyour de anuncios de ruta tooenable, debe asociar un filtro de ruta.</span><span class="sxs-lookup"><span data-stu-id="55184-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="55184-123">Un filtro de rutas permite identificar servicios que desee tooconsume a través de emparejamiento de Microsoft el circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="55184-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="55184-124">Es básicamente una lista blanca de todos los valores de comunidad de hello BGP.</span><span class="sxs-lookup"><span data-stu-id="55184-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="55184-125">Una vez que un recurso de filtro de ruta se define y adjunta tooan circuito ExpressRoute, todos los prefijos que se asignan valores de comunidad BGP toohello son redes de tooyour anunciado.</span><span class="sxs-lookup"><span data-stu-id="55184-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="55184-126">toobe tooattach capaz de filtros de ruta con servicios de Office 365 en ellos, debe tener autorización tooconsume Office 365 services a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="55184-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="55184-127">Si no está autorizado tooconsume Office 365 services a través de ExpressRoute, filtros de ruta de hello operación tooattach produce un error.</span><span class="sxs-lookup"><span data-stu-id="55184-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="55184-128">Para obtener más información sobre el proceso de autorización de hello, consulte [ExpressRoute de Azure para Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="55184-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="55184-129">Servicios de conectividad tooDynamics 365 no requiere una autorización previa.</span><span class="sxs-lookup"><span data-stu-id="55184-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55184-130">Emparejamiento de Microsoft de circuitos ExpressRoute que estaban configurados anterior tooAugust 1, 2017 tendrá todos los prefijos de servicio implementados a través de emparejamiento de Microsoft, incluso si no se definen los filtros de ruta.</span><span class="sxs-lookup"><span data-stu-id="55184-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="55184-131">Emparejamiento de Microsoft de circuitos ExpressRoute configurados en o después del 1 de agosto de 2017 no tendrá todos los prefijos anunciados hasta que se conecte un filtro de ruta toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="55184-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="55184-132"><a name="workflow"></a>Flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="55184-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="55184-133">toobe puede toosuccessfully conecte tooservices a través de emparejamiento de Microsoft, debe completar los siguientes pasos de configuración de Hola:</span><span class="sxs-lookup"><span data-stu-id="55184-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="55184-134">Debe tener un circuito ExpressRoute activo que tenga el emparejamiento de Microsoft aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="55184-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="55184-135">Puede usar Hola siguiendo las instrucciones tooaccomplish estas tareas:</span><span class="sxs-lookup"><span data-stu-id="55184-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="55184-136">[Crear un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="55184-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="55184-137">Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="55184-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="55184-138">[Crear el emparejamiento de Microsoft](expressroute-howto-routing-portal-resource-manager.md) si administra directamente la sesión BGP de Hola.</span><span class="sxs-lookup"><span data-stu-id="55184-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="55184-139">O bien, pida a su proveedor de conectividad que aprovisione el emparejamiento de Microsoft para su circuito.</span><span class="sxs-lookup"><span data-stu-id="55184-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="55184-140">Debe crear y configurar un filtro de ruta.</span><span class="sxs-lookup"><span data-stu-id="55184-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="55184-141">Identificar servicios Hola con tooconsume a través de emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="55184-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="55184-142">Identificar Hola lista de valores de la Comunidad BGP asociados con los servicios de Hola</span><span class="sxs-lookup"><span data-stu-id="55184-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="55184-143">Crear una lista regla tooallow Hola prefijo coincidente hello valores de la Comunidad BGP</span><span class="sxs-lookup"><span data-stu-id="55184-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="55184-144">Debe asociar el circuito de ExpressRoute de toohello de filtro de ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="55184-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="55184-145">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="55184-145">Before you begin</span></span>

<span data-ttu-id="55184-146">Antes de comenzar, asegúrese de que cumplir Hola siguiendo criterios:</span><span class="sxs-lookup"><span data-stu-id="55184-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="55184-147">Hola de revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="55184-147">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="55184-148">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="55184-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="55184-149">Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="55184-149">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="55184-150">Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="55184-150">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="55184-151">Debe tener un emparejamiento de Microsoft activo.</span><span class="sxs-lookup"><span data-stu-id="55184-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="55184-152">Siga las instrucciones que encontrará en [Creación y modificación de la configuración de emparejamiento](expressroute-howto-routing-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="55184-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="55184-153"><a name="prefixes"></a>Paso 1.</span><span class="sxs-lookup"><span data-stu-id="55184-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="55184-154">Obtención de una lista de prefijos y valores de la comunidad de BGP</span><span class="sxs-lookup"><span data-stu-id="55184-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="55184-155">1. Obtención de una lista de valores de la comunidad de BGP</span><span class="sxs-lookup"><span data-stu-id="55184-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="55184-156">Valores de la Comunidad BGP asociados con los servicios accesibles a través de emparejamiento de Microsoft está disponible en hello [requisitos de enrutamiento de ExpressRoute](expressroute-routing.md) página.</span><span class="sxs-lookup"><span data-stu-id="55184-156">BGP community values associated with services accessible through Microsoft peering is available in hello [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="55184-157">2. Realice una lista de valores de hello que desea toouse</span><span class="sxs-lookup"><span data-stu-id="55184-157">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="55184-158">Realice una lista de valores de la Comunidad BGP que desea toouse de filtro de ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="55184-158">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="55184-159">Por ejemplo, hello valor de la Comunidad BGP para servicios de Dynamics 365 es 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="55184-159">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="55184-160"><a name="filter"></a>Paso 2.</span><span class="sxs-lookup"><span data-stu-id="55184-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="55184-161">Creación de un filtro de ruta y una regla de filtro</span><span class="sxs-lookup"><span data-stu-id="55184-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="55184-162">Un filtro de ruta puede tener una única regla y Hola regla debe ser de tipo 'Allow'.</span><span class="sxs-lookup"><span data-stu-id="55184-162">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="55184-163">Esta regla puede tener una lista de valores de la comunidad de BGP asociados a ella.</span><span class="sxs-lookup"><span data-stu-id="55184-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="55184-164">1. Creación de un filtro de ruta</span><span class="sxs-lookup"><span data-stu-id="55184-164">1. Create a route filter</span></span>
<span data-ttu-id="55184-165">Puede crear un filtro de ruta seleccionando Hola opción toocreate un nuevo recurso.</span><span class="sxs-lookup"><span data-stu-id="55184-165">You can create a route filter by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="55184-166">Haga clic en **New** > **red** > **RouteFilter**, tal y como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="55184-166">Click **New** > **Networking** > **RouteFilter**, as shown in hello following image:</span></span>

![Creación de un filtro de ruta](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="55184-168">Debe colocar el filtro de ruta de hello en un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="55184-168">You must place hello route filter in a resource group.</span></span> 

![Creación de un filtro de ruta](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="55184-170">2. Creación de una regla de filtro</span><span class="sxs-lookup"><span data-stu-id="55184-170">2. Create a filter rule</span></span>

<span data-ttu-id="55184-171">Puede agregar y reglas de actualización seleccionando Hola administración ficha de regla para el filtro de ruta.</span><span class="sxs-lookup"><span data-stu-id="55184-171">You can add and update rules by selecting hello manage rule tab for your route filter.</span></span>

![Creación de un filtro de ruta](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="55184-173">Puede seleccionar Hola servicios que desee tooconnect toofrom Hola lista desplegable y guardar la regla de hello cuando haya finalizado.</span><span class="sxs-lookup"><span data-stu-id="55184-173">You can select hello services you want tooconnect toofrom hello drop down list and save hello rule when done.</span></span>

![Creación de un filtro de ruta](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="55184-175"><a name="attach"></a>Paso 3.</span><span class="sxs-lookup"><span data-stu-id="55184-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="55184-176">Adjuntar el circuito de ExpressRoute de tooan de filtro de ruta de Hola</span><span class="sxs-lookup"><span data-stu-id="55184-176">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="55184-177">Puede adjuntar el circuito de hello route filtro tooa seleccionando el botón de "Agregar circuito" hello y circuito de ExpressRoute de Hola de lista desplegable Hola.</span><span class="sxs-lookup"><span data-stu-id="55184-177">You can attach hello route filter tooa circuit by selecting hello "add Circuit" button and selecting hello ExpressRoute circuit from hello drop down list.</span></span>

![Creación de un filtro de ruta](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="55184-179"><a name="getproperties"></a>propiedades de hello tooget de un filtro de ruta</span><span class="sxs-lookup"><span data-stu-id="55184-179"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="55184-180">Puede ver propiedades de un filtro de ruta cuando se abre el recurso de hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="55184-180">You can view properties of a route filter when you open hello resource in hello portal.</span></span>

![Creación de un filtro de ruta](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="55184-182"><a name="updateproperties"></a>propiedades de hello tooupdate de un filtro de ruta</span><span class="sxs-lookup"><span data-stu-id="55184-182"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="55184-183">Puede actualizar lista Hola de BGP Comunidad valores tooa adjunto circuito seleccionando el botón Hola "Administrar regla".</span><span class="sxs-lookup"><span data-stu-id="55184-183">You can update hello list of BGP community values attached tooa circuit by selecting hello "Manage rule" button.</span></span>


![Creación de un filtro de ruta](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Creación de un filtro de ruta](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="55184-186"><a name="detach"></a>toodetach un filtro de ruta de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="55184-186"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="55184-187">toodetach un circuito de filtro de ruta de hello, haga clic con el botón secundario en el circuito de Hola y haga clic en "desvincular".</span><span class="sxs-lookup"><span data-stu-id="55184-187">toodetach a circuit from hello route filter, right click on hello circuit and click on "disassociate".</span></span>

![Creación de un filtro de ruta](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="55184-189"><a name="delete"></a>toodelete un filtro de ruta</span><span class="sxs-lookup"><span data-stu-id="55184-189"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="55184-190">Puede eliminar un filtro de ruta seleccionando el botón de eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="55184-190">You can delete a route filter by selecting hello delete button.</span></span> 

![Creación de un filtro de ruta](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="55184-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="55184-192">Next steps</span></span>

<span data-ttu-id="55184-193">Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="55184-193">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
