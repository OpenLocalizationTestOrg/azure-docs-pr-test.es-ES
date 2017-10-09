---
title: "Configuración de filtros de ruta para el emparejamiento de Microsoft en Azure ExpressRoute | Microsoft Docs"
description: "Este artículo describe cómo se filtra tooconfigure ruta para Peering Microsoft mediante PowerShell"
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="31242-103">Configuración de filtros de ruta para el emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="31242-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="31242-104">Filtros de ruta son un tooconsume de manera un subconjunto de servicios admitidos a través de emparejamiento de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="31242-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="31242-105">Hola pasos de este artículo le ayudarán a configura y administra filtros de ruta para los circuitos ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31242-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="31242-106">Servicios de Dynamics 365 y servicios de Office 365 como Exchange Online, SharePoint Online y Skype empresarial, son accesibles a través de emparejamiento de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="31242-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="31242-107">Cuando se configura el emparejamiento de Microsoft en un circuito ExpressRoute, todos los servicios de toothese relacionados de prefijos se anuncian a través de sesiones BGP de Hola que se establecen.</span><span class="sxs-lookup"><span data-stu-id="31242-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="31242-108">Un valor de la Comunidad BGP es tooevery adjunto prefijo tooidentify Hola servicio se ofrece a través de prefijo de Hola.</span><span class="sxs-lookup"><span data-stu-id="31242-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="31242-109">Para obtener una lista de valores de comunidad BGP de Hola y servicios de Hola que se asignan, vea [Comunidades BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="31242-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="31242-110">Si necesita conectividad tooall servicios, un gran número de prefijos se anuncia a través de BGP.</span><span class="sxs-lookup"><span data-stu-id="31242-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="31242-111">Esto aumenta significativamente el tamaño de Hola Hola de tablas de rutas mantenido por enrutadores dentro de la red.</span><span class="sxs-lookup"><span data-stu-id="31242-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="31242-112">Si tiene previsto tooconsume solo un subconjunto de servicios ofrece a través de emparejamiento de Microsoft, puede reducir el tamaño de Hola de las tablas de enrutamiento de dos maneras.</span><span class="sxs-lookup"><span data-stu-id="31242-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="31242-113">Puede:</span><span class="sxs-lookup"><span data-stu-id="31242-113">You can:</span></span>

- <span data-ttu-id="31242-114">Filtrar los prefijos no deseados mediante la aplicación de filtros de ruta en las comunidades de BGP.</span><span class="sxs-lookup"><span data-stu-id="31242-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="31242-115">Este es un procedimiento de red estándar y se usa normalmente en muchas redes.</span><span class="sxs-lookup"><span data-stu-id="31242-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="31242-116">Definir filtros de ruta y aplicarlas tooyour circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31242-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="31242-117">Un filtro de ruta es un recurso nuevo que permite seleccionar una lista de hello de servicios planee tooconsume a través de emparejamiento de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="31242-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="31242-118">Enrutadores de ExpressRoute solo envían lista Hola de prefijos que pertenecen a los servicios de toohello identificados en el filtro de ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="31242-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="31242-119"><a name="about"></a>Acerca de los filtros de ruta</span><span class="sxs-lookup"><span data-stu-id="31242-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="31242-120">Cuando se configura el emparejamiento de Microsoft en el circuito de ExpressRoute, enrutadores de borde de Microsoft hello establecen un par de sesiones de BGP con enrutadores de borde de hello (usted o el proveedor de conectividad).</span><span class="sxs-lookup"><span data-stu-id="31242-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="31242-121">No hay rutas son redes de tooyour anunciado.</span><span class="sxs-lookup"><span data-stu-id="31242-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="31242-122">red de tooyour de anuncios de ruta tooenable, debe asociar un filtro de ruta.</span><span class="sxs-lookup"><span data-stu-id="31242-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="31242-123">Un filtro de rutas permite identificar servicios que desee tooconsume a través de emparejamiento de Microsoft el circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31242-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="31242-124">Es básicamente una lista blanca de todos los valores de comunidad de hello BGP.</span><span class="sxs-lookup"><span data-stu-id="31242-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="31242-125">Una vez que un recurso de filtro de ruta se define y adjunta tooan circuito ExpressRoute, todos los prefijos que se asignan valores de comunidad BGP toohello son redes de tooyour anunciado.</span><span class="sxs-lookup"><span data-stu-id="31242-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="31242-126">toobe tooattach capaz de filtros de ruta con servicios de Office 365 en ellos, debe tener autorización tooconsume Office 365 services a través de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="31242-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="31242-127">Si no está autorizado tooconsume Office 365 services a través de ExpressRoute, filtros de ruta de hello operación tooattach produce un error.</span><span class="sxs-lookup"><span data-stu-id="31242-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="31242-128">Para obtener más información sobre el proceso de autorización de hello, consulte [ExpressRoute de Azure para Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="31242-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="31242-129">Servicios de conectividad tooDynamics 365 no requiere una autorización previa.</span><span class="sxs-lookup"><span data-stu-id="31242-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31242-130">Emparejamiento de Microsoft de circuitos ExpressRoute que estaban configurados anterior tooAugust 1, 2017 tendrá todos los prefijos de servicio implementados a través de emparejamiento de Microsoft, incluso si no se definen los filtros de ruta.</span><span class="sxs-lookup"><span data-stu-id="31242-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="31242-131">Emparejamiento de Microsoft de circuitos ExpressRoute configurados en o después del 1 de agosto de 2017 no tendrá todos los prefijos anunciados hasta que se conecte un filtro de ruta toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="31242-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="31242-132"><a name="workflow"></a>Flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="31242-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="31242-133">toobe puede toosuccessfully conecte tooservices a través de emparejamiento de Microsoft, debe completar los siguientes pasos de configuración de Hola:</span><span class="sxs-lookup"><span data-stu-id="31242-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="31242-134">Debe tener un circuito ExpressRoute activo que tenga el emparejamiento de Microsoft aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="31242-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="31242-135">Puede usar Hola siguiendo las instrucciones tooaccomplish estas tareas:</span><span class="sxs-lookup"><span data-stu-id="31242-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="31242-136">[Crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="31242-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="31242-137">Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="31242-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="31242-138">[Crear el emparejamiento de Microsoft](expressroute-circuit-peerings.md) si administra directamente la sesión BGP de Hola.</span><span class="sxs-lookup"><span data-stu-id="31242-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="31242-139">O bien, pida a su proveedor de conectividad que aprovisione el emparejamiento de Microsoft para su circuito.</span><span class="sxs-lookup"><span data-stu-id="31242-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="31242-140">Debe crear y configurar un filtro de ruta.</span><span class="sxs-lookup"><span data-stu-id="31242-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="31242-141">Identificar servicios Hola con tooconsume a través de emparejamiento de Microsoft</span><span class="sxs-lookup"><span data-stu-id="31242-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="31242-142">Identificar Hola lista de valores de la Comunidad BGP asociados con los servicios de Hola</span><span class="sxs-lookup"><span data-stu-id="31242-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="31242-143">Crear una lista regla tooallow Hola prefijo coincidente hello valores de la Comunidad BGP</span><span class="sxs-lookup"><span data-stu-id="31242-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="31242-144">Debe asociar el circuito de ExpressRoute de toohello de filtro de ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="31242-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="31242-145">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="31242-145">Before you begin</span></span>

<span data-ttu-id="31242-146">Antes de comenzar, asegúrese de que cumplir Hola siguiendo criterios:</span><span class="sxs-lookup"><span data-stu-id="31242-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="31242-147">Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="31242-147">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="31242-148">Para más información, consulte [Install and Configure Azure PowerShell](/powershell/azure/install-azurerm-ps) (Instalación y configuración de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="31242-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="31242-149">Descargar Hola última versión de la Galería de PowerShell de hello, en lugar de usar Hola instalador.</span><span class="sxs-lookup"><span data-stu-id="31242-149">Download hello latest version from hello PowerShell Gallery, rather than using hello Installer.</span></span> <span data-ttu-id="31242-150">Hola instalador actualmente no es compatible con los cmdlets de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="31242-150">hello Installer currently does not support hello required cmdlets.</span></span>
  > 

 - <span data-ttu-id="31242-151">Hola de revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="31242-151">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="31242-152">Tiene que tener un circuito ExpressRoute activo.</span><span class="sxs-lookup"><span data-stu-id="31242-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="31242-153">Siga las instrucciones de hello demasiado[crear un circuito ExpressRoute](expressroute-howto-circuit-arm.md) y tener circuito de hello habilitada por el proveedor de conectividad antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="31242-153">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="31242-154">Hola circuito de ExpressRoute debe estar en un estado habilitado y aprovisionado.</span><span class="sxs-lookup"><span data-stu-id="31242-154">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="31242-155">Debe tener un emparejamiento de Microsoft activo.</span><span class="sxs-lookup"><span data-stu-id="31242-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="31242-156">Siga las instrucciones que encontrará en [Creación y modificación de la configuración de emparejamiento](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="31242-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="31242-157">Inicie sesión en tooyour cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="31242-157">Log in tooyour Azure account</span></span>

<span data-ttu-id="31242-158">Antes de comenzar esta configuración, primero debe iniciar sesión en tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="31242-158">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="31242-159">Hola cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="31242-159">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="31242-160">Después de iniciar sesión, descarga la configuración de la cuenta para que estén disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31242-160">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="31242-161">Abra la consola de PowerShell con privilegios elevados y conectar con cuenta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="31242-161">Open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="31242-162">Usar hello después toohelp de ejemplo que se conecta:</span><span class="sxs-lookup"><span data-stu-id="31242-162">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="31242-163">Si tiene varias suscripciones de Azure, compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="31242-163">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="31242-164">Especifique que desea toouse de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="31242-164">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="31242-165"><a name="prefixes"></a>Paso 1.</span><span class="sxs-lookup"><span data-stu-id="31242-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="31242-166">Obtención de una lista de prefijos y valores de la comunidad de BGP</span><span class="sxs-lookup"><span data-stu-id="31242-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="31242-167">1. Obtención de una lista de valores de la comunidad de BGP</span><span class="sxs-lookup"><span data-stu-id="31242-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="31242-168">Usar hello cmdlet tooget Hola lista de valores de la Comunidad BGP asociados con los servicios accesibles a través de emparejamiento de Microsoft siguiente y Hola lista de prefijos asociados a ellos:</span><span class="sxs-lookup"><span data-stu-id="31242-168">Use hello following cmdlet tooget hello list of BGP community values associated with services accessible through Microsoft peering, and hello list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="31242-169">2. Realice una lista de valores de hello que desea toouse</span><span class="sxs-lookup"><span data-stu-id="31242-169">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="31242-170">Realice una lista de valores de la Comunidad BGP que desea toouse de filtro de ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="31242-170">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="31242-171">Por ejemplo, hello valor de la Comunidad BGP para servicios de Dynamics 365 es 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="31242-171">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="31242-172"><a name="filter"></a>Paso 2.</span><span class="sxs-lookup"><span data-stu-id="31242-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="31242-173">Creación de un filtro de ruta y una regla de filtro</span><span class="sxs-lookup"><span data-stu-id="31242-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="31242-174">Un filtro de ruta puede tener una única regla y Hola regla debe ser de tipo 'Allow'.</span><span class="sxs-lookup"><span data-stu-id="31242-174">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="31242-175">Esta regla puede tener una lista de valores de la comunidad de BGP asociados a ella.</span><span class="sxs-lookup"><span data-stu-id="31242-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="31242-176">1. Creación de un filtro de ruta</span><span class="sxs-lookup"><span data-stu-id="31242-176">1. Create a route filter</span></span>

<span data-ttu-id="31242-177">Primero, cree el filtro de ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="31242-177">First, create hello route filter.</span></span> <span data-ttu-id="31242-178">comando de Hello 'New-AzureRmRouteFilter' solo crea un recurso de filtro de ruta.</span><span class="sxs-lookup"><span data-stu-id="31242-178">hello command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="31242-179">Después de crear el recurso de hello, debe crear una regla y adjuntarlo toohello objeto de filtro de ruta.</span><span class="sxs-lookup"><span data-stu-id="31242-179">After you create hello resource, you must then create a rule and attach it toohello route filter object.</span></span> <span data-ttu-id="31242-180">Ejecute hello después comando toocreate un recurso de filtro de ruta:</span><span class="sxs-lookup"><span data-stu-id="31242-180">Run hello following command toocreate a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="31242-181">2. Creación de una regla de filtro</span><span class="sxs-lookup"><span data-stu-id="31242-181">2. Create a filter rule</span></span>

<span data-ttu-id="31242-182">Puede especificar un conjunto de Comunidades BGP como una lista separada por comas, como se muestra en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="31242-182">You can specify a set of BGP communities as a comma-separated list, as shown in hello example.</span></span> <span data-ttu-id="31242-183">Ejecutar una nueva regla de hello después toocreate de comando:</span><span class="sxs-lookup"><span data-stu-id="31242-183">Run hello following command toocreate a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a><span data-ttu-id="31242-184">3. Agregar filtro de ruta de hello regla toohello</span><span class="sxs-lookup"><span data-stu-id="31242-184">3. Add hello rule toohello route filter</span></span>

<span data-ttu-id="31242-185">Siguiente ejecución Hola comando tooadd Hola regla toohello ruta filtro:</span><span class="sxs-lookup"><span data-stu-id="31242-185">Run hello following command tooadd hello filter rule toohello route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="31242-186"><a name="attach"></a>Paso 3.</span><span class="sxs-lookup"><span data-stu-id="31242-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="31242-187">Adjuntar el circuito de ExpressRoute de tooan de filtro de ruta de Hola</span><span class="sxs-lookup"><span data-stu-id="31242-187">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="31242-188">Ejecute hello después comando tooattach Hola ruta filtro toohello circuito de ExpressRoute, suponiendo que tenga el emparejamiento único de Microsoft:</span><span class="sxs-lookup"><span data-stu-id="31242-188">Run hello following command tooattach hello route filter toohello ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="31242-189"><a name="getproperties"></a>propiedades de hello tooget de un filtro de ruta</span><span class="sxs-lookup"><span data-stu-id="31242-189"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="31242-190">propiedades de hello tooget de un filtro de ruta, utilice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="31242-190">tooget hello properties of a route filter, use hello following steps:</span></span>

1. <span data-ttu-id="31242-191">Ejecute hello después de recurso de filtro de ruta de comando tooget hello:</span><span class="sxs-lookup"><span data-stu-id="31242-191">Run hello following command tooget hello route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="31242-192">Obtener las reglas de filtro de ruta de hello para el recurso de filtro de ruta de hello ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="31242-192">Get hello route filter rules for hello route-filter resource by running hello following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="31242-193"><a name="updateproperties"></a>propiedades de hello tooupdate de un filtro de ruta</span><span class="sxs-lookup"><span data-stu-id="31242-193"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="31242-194">Si ya está asociado el filtro de ruta de hello tooa circuito, lista de actualizaciones toohello BGP Comunidad automáticamente propaga los cambios de anuncio de prefijo adecuado a través de sesiones BGP Hola establecida.</span><span class="sxs-lookup"><span data-stu-id="31242-194">If hello route filter is already attached tooa circuit, updates toohello BGP community list automatically propagates appropriate prefix advertisement changes through hello established BGP sessions.</span></span> <span data-ttu-id="31242-195">Puede actualizar la lista de comunidad BGP de Hola de su filtro de ruta utilizando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="31242-195">You can update hello BGP community list of your route filter using hello following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="31242-196"><a name="detach"></a>toodetach un filtro de ruta de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="31242-196"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="31242-197">Una vez que un filtro de ruta se separa de hello circuito ExpressRoute, prefijos no se difundan a través de la sesión BGP Hola.</span><span class="sxs-lookup"><span data-stu-id="31242-197">Once a route filter is detached from hello ExpressRoute circuit, no prefixes are advertised through hello BGP session.</span></span> <span data-ttu-id="31242-198">Puede separar un filtro de ruta de un circuito de ExpressRoute con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="31242-198">You can detach a route filter from an ExpressRoute circuit using hello following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="31242-199"><a name="delete"></a>toodelete un filtro de ruta</span><span class="sxs-lookup"><span data-stu-id="31242-199"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="31242-200">Solo puede eliminar un filtro de ruta si no está había conectado tooany circuito.</span><span class="sxs-lookup"><span data-stu-id="31242-200">You can only delete a route filter if it is not attached tooany circuit.</span></span> <span data-ttu-id="31242-201">Asegúrese de que ese filtro de ruta de hello no está adjunta tooany circuito antes de intentar toodelete.</span><span class="sxs-lookup"><span data-stu-id="31242-201">Ensure that hello route filter is not attached tooany circuit before attempting toodelete it.</span></span> <span data-ttu-id="31242-202">Puede eliminar un filtro de ruta mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="31242-202">You can delete a route filter using hello following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="31242-203">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="31242-203">Next steps</span></span>

<span data-ttu-id="31242-204">Para obtener más información sobre ExpressRoute, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="31242-204">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
