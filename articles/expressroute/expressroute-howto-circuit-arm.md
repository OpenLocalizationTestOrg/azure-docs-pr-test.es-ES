---
title: "Creación y modificación de un circuito ExpressRoute mediante Powershell y Azure Resource Manager | Microsoft Docs"
description: "Este artículo describe cómo toocreate, aprovisionar, compruebe, actualizar, eliminar y cancelar el aprovisionamiento de un circuito de ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="48932-103">Creación y modificación de un circuito ExpressRoute mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="48932-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="48932-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="48932-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="48932-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48932-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="48932-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="48932-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="48932-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="48932-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="48932-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="48932-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="48932-109">Este artículo describe cómo el circuito toocreate una ExpressRoute de Azure utilizando el modelo de implementación de Azure Resource Manager de hello y cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="48932-109">This article describes how toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="48932-110">Este artículo también muestra cómo actualizarlo, estado de hello toocheck del circuito de hello, o eliminar y Cancelar.</span><span class="sxs-lookup"><span data-stu-id="48932-110">This article also shows you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="48932-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="48932-111">Before you begin</span></span>
* <span data-ttu-id="48932-112">Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="48932-112">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="48932-113">Para obtener más información, consulte la [Overview of Azure PowerShell](/powershell/azure/overview) (Introducción a Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="48932-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="48932-114">Hola de revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="48932-114">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="48932-115">Creación y aprovisionamiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="48932-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="48932-116">1. Inicie sesión en tooyour cuenta de Azure y seleccione su suscripción</span><span class="sxs-lookup"><span data-stu-id="48932-116">1. Sign in tooyour Azure account and select your subscription</span></span>
<span data-ttu-id="48932-117">toobegin la configuración, el inicio de sesión tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="48932-117">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="48932-118">Usar hello después toohelp ejemplos que conectarse:</span><span class="sxs-lookup"><span data-stu-id="48932-118">Use hello following examples toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="48932-119">Compruebe las suscripciones de hello para la cuenta de hello:</span><span class="sxs-lookup"><span data-stu-id="48932-119">Check hello subscriptions for hello account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="48932-120">Seleccione la suscripción de Hola que desea toocreate una ExpressRoute de circuito para:</span><span class="sxs-lookup"><span data-stu-id="48932-120">Select hello subscription that you want toocreate an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="48932-121">2. Obtener lista de Hola de proveedores compatibles, las ubicaciones y anchos de banda</span><span class="sxs-lookup"><span data-stu-id="48932-121">2. Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="48932-122">Antes de crear un circuito ExpressRoute, necesita Hola lista de proveedores admitidos conectividad, ubicaciones y opciones de ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="48932-122">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="48932-123">Hola cmdlet de PowerShell **AzureRmExpressRouteServiceProvider Get** devuelve esta información, que usará en pasos posteriores:</span><span class="sxs-lookup"><span data-stu-id="48932-123">hello PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="48932-124">Compruebe toosee si aparece el proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="48932-124">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="48932-125">Tome nota de hello siguiente información.</span><span class="sxs-lookup"><span data-stu-id="48932-125">Make a note of hello following information.</span></span> <span data-ttu-id="48932-126">La necesitará más adelante cuando cree un circuito.</span><span class="sxs-lookup"><span data-stu-id="48932-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="48932-127">Nombre</span><span class="sxs-lookup"><span data-stu-id="48932-127">Name</span></span>
* <span data-ttu-id="48932-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="48932-128">PeeringLocations</span></span>
* <span data-ttu-id="48932-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="48932-129">BandwidthsOffered</span></span>

<span data-ttu-id="48932-130">Ahora está listo toocreate un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="48932-130">You're now ready toocreate an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="48932-131">3. Creación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="48932-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="48932-132">Si todavía no tiene un grupo de recursos, debe crear uno antes de crear ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="48932-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="48932-133">Puede hacerlo ejecutando el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="48932-133">You can do so by running hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="48932-134">Hola de ejemplo siguiente muestra cómo el circuito toocreate una ExpressRoute de 200 Mbps a través de Equinix en Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="48932-134">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="48932-135">Si usa otro proveedor y otra configuración, sustituya esa información al realizar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="48932-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="48932-136">Hola te mostramos una solicitud de ejemplo para una nueva clave de servicio:</span><span class="sxs-lookup"><span data-stu-id="48932-136">hello following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="48932-137">Asegúrese de que se especifique nivel correcto de la SKU de Hola y familia de SKU:</span><span class="sxs-lookup"><span data-stu-id="48932-137">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="48932-138">El nivel de SKU determina si está habilitado un complemento estándar o premium de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="48932-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="48932-139">Puede especificar *estándar* tooget Hola SKU estándar o *Premium* para el complemento de hello premium.</span><span class="sxs-lookup"><span data-stu-id="48932-139">You can specify *Standard* tooget hello standard SKU or *Premium* for hello premium add-on.</span></span>
* <span data-ttu-id="48932-140">Familia de SKU determina el tipo de facturación de Hola.</span><span class="sxs-lookup"><span data-stu-id="48932-140">SKU family determines hello billing type.</span></span> <span data-ttu-id="48932-141">Puede seleccionar *Metereddata* para el plan de datos limitado y *Unlimiteddata* para el plan de datos ilimitado.</span><span class="sxs-lookup"><span data-stu-id="48932-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="48932-142">Se puede cambiar el tipo de facturación de Hola de *Metereddata* demasiado*Unlimiteddata*, pero no se puede cambiar tipo hello de *Unlimiteddata* demasiado*Metereddata* .</span><span class="sxs-lookup"><span data-stu-id="48932-142">You can change hello billing type from *Metereddata* too*Unlimiteddata*, but you can't change hello type from *Unlimiteddata* too*Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48932-143">El circuito de ExpressRoute se cobrará desde el momento de Hola que se emite una clave de servicio.</span><span class="sxs-lookup"><span data-stu-id="48932-143">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="48932-144">Asegúrese de que lleva a cabo esta operación cuando proveedor de conectividad de hello circuito de hello tooprovision listo.</span><span class="sxs-lookup"><span data-stu-id="48932-144">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="48932-145">respuesta de Hello contiene la clave de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="48932-145">hello response contains hello service key.</span></span> <span data-ttu-id="48932-146">Puede obtener una descripción detallada de todos los parámetros de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="48932-146">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="48932-147">4. Lista de todos los circuitos ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="48932-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="48932-148">tooget Hola de una lista de todos los circuitos ExpressRoute que ha creado, ejecute hello **Get AzureRmExpressRouteCircuit** comando:</span><span class="sxs-lookup"><span data-stu-id="48932-148">tooget a list of all hello ExpressRoute circuits that you created, run hello **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="48932-149">respuesta de Hello tendrá un aspecto similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="48932-149">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

<span data-ttu-id="48932-150">Puede recuperar esta información en cualquier momento mediante hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="48932-150">You can retrieve this information at any time by using hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="48932-151">Realizar Hola llamada sin parámetros, enumera todos los circuitos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48932-151">Making hello call with no parameters lists all hello circuits.</span></span> <span data-ttu-id="48932-152">La clave del servicio se enumerarán en hello *ServiceKey* campo:</span><span class="sxs-lookup"><span data-stu-id="48932-152">Your service key will be listed in hello *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="48932-153">respuesta de Hello tendrá un aspecto similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="48932-153">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="48932-154">Puede obtener una descripción detallada de todos los parámetros de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="48932-154">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="48932-155">5. Enviar el proveedor de conectividad de tooyour clave de servicio de hello para el aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="48932-155">5. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="48932-156">*ServiceProviderProvisioningState* proporciona información sobre el estado actual de Hola de aprovisionamiento en el lado del proveedor de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="48932-156">*ServiceProviderProvisioningState* provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="48932-157">Estado proporciona el estado de Hola en hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="48932-157">Status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="48932-158">Para obtener más información acerca de los Estados de aprovisionamiento del circuito, vea hello [flujos de trabajo](expressroute-workflows.md#expressroute-circuit-provisioning-states) artículo.</span><span class="sxs-lookup"><span data-stu-id="48932-158">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="48932-159">Cuando se crea un nuevo circuito de ExpressRoute, circuito Hola estará en hello siguiente estado:</span><span class="sxs-lookup"><span data-stu-id="48932-159">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="48932-160">circuito Hola cambiará toohello siguiente estado cuando el proveedor de conectividad de hello está en proceso de Hola de habilitarla para:</span><span class="sxs-lookup"><span data-stu-id="48932-160">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="48932-161">Para toobe pueda toouse un circuito ExpressRoute, debe estar en hello siguiente estado:</span><span class="sxs-lookup"><span data-stu-id="48932-161">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="48932-162">6. Comprobar periódicamente el estado de Hola y el estado de Hola de clave de circuito de Hola</span><span class="sxs-lookup"><span data-stu-id="48932-162">6. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="48932-163">Comprobación de estado de Hola y el estado de Hola de clave de circuito de hello le permite saber si el proveedor ha habilitado el circuito.</span><span class="sxs-lookup"><span data-stu-id="48932-163">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="48932-164">Una vez configurado el circuito de hello, *ServiceProviderProvisioningState* aparece como *aprovisionado*, tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="48932-164">After hello circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in hello following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="48932-165">respuesta de Hello tendrá un aspecto similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="48932-165">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                       }
    ServiceKey                       : **************************************
    Peerings                         : []

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="48932-166">7. Creación de la configuración de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="48932-166">7. Create your routing configuration</span></span>
<span data-ttu-id="48932-167">Para obtener instrucciones detalladas, consulte hello [circuito de ExpressRoute de configuración de enrutamiento](expressroute-howto-routing-arm.md) artículo toocreate y modificar los emparejamientos de circuito.</span><span class="sxs-lookup"><span data-stu-id="48932-167">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48932-168">Estas instrucciones aplican solo toocircuits que se crean con proveedores de servicios que ofrecen servicios de conectividad de 2 niveles.</span><span class="sxs-lookup"><span data-stu-id="48932-168">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="48932-169">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="48932-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="48932-170">8. Vincular un circuito de ExpressRoute de tooan de red virtual</span><span class="sxs-lookup"><span data-stu-id="48932-170">8. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="48932-171">A continuación, vincular un circuito de ExpressRoute de tooyour de red virtual.</span><span class="sxs-lookup"><span data-stu-id="48932-171">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="48932-172">Hola de uso [vinculación virtual redes tooExpressRoute circuitos](expressroute-howto-linkvnet-arm.md) artículo cuando se trabaja con el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48932-172">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="48932-173">Obtener el estado de saludo de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="48932-173">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="48932-174">Puede recuperar esta información en cualquier momento mediante hello **AzureRmExpressRouteCircuit Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="48932-174">You can retrieve this information at any time by using hello **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="48932-175">Realizar Hola llamada sin parámetros, enumera todos los circuitos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48932-175">Making hello call with no parameters lists all hello circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="48932-176">respuesta de Hello será similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="48932-176">hello response will be similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                            "ServiceProviderName": "Equinix",
                                            "PeeringLocation": "Silicon Valley",
                                            "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="48932-177">Puede obtener información sobre un circuito de ExpressRoute concreto pasando el nombre del grupo de recursos de Hola y el nombre de circuito como una llamada a toohello de parámetro:</span><span class="sxs-lookup"><span data-stu-id="48932-177">You can get information on a specific ExpressRoute circuit by passing hello resource group name and circuit name as a parameter toohello call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="48932-178">respuesta de Hello tendrá un aspecto similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="48932-178">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                            "Tier": "Standard",
                                            "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="48932-179">Puede obtener una descripción detallada de todos los parámetros de hello ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="48932-179">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="48932-180"><a name="modify"></a>Modificación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="48932-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="48932-181">Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad.</span><span class="sxs-lookup"><span data-stu-id="48932-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="48932-182">Puede hacer Hola sigue sin tiempo de inactividad:</span><span class="sxs-lookup"><span data-stu-id="48932-182">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="48932-183">Habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="48932-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="48932-184">Ancho de banda de Hola de aumento de su circuito de ExpressRoute proporciona hay capacidad disponible en el puerto de Hola.</span><span class="sxs-lookup"><span data-stu-id="48932-184">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="48932-185">No se admite la degradación de ancho de banda de Hola de un circuito.</span><span class="sxs-lookup"><span data-stu-id="48932-185">Downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="48932-186">Cambiar Hola plan desde tooUnlimited datos limitados de datos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="48932-186">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="48932-187">Cambiar Hola plan desde tooMetered ilimitados datos que no se admiten datos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="48932-187">Changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="48932-188">Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).</span><span class="sxs-lookup"><span data-stu-id="48932-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="48932-189">Para obtener más información sobre los límites y limitaciones, consulte toohello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="48932-189">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="48932-190">complemento de tooenable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="48932-190">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="48932-191">Puede habilitar complemento de hello ExpressRoute premium para el circuito existente mediante Hola siguiente fragmento de código de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="48932-191">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="48932-192">circuito Hola tendrán ahora hello ExpressRoute complemento las características premium habilitadas.</span><span class="sxs-lookup"><span data-stu-id="48932-192">hello circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="48932-193">Comenzaremos facturación para la capacidad de complemento de hello premium tan pronto como comando de Hola se ha ejecutado correctamente.</span><span class="sxs-lookup"><span data-stu-id="48932-193">We will begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="48932-194">complemento de toodisable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="48932-194">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="48932-195">Esta operación puede producir un error si usa recursos que son mayores que lo que está permitido para el circuito de hello estándar.</span><span class="sxs-lookup"><span data-stu-id="48932-195">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="48932-196">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="48932-196">Note hello following:</span></span>

* <span data-ttu-id="48932-197">Antes de degradar de toostandard premium, debe asegurarse de ese número de Hola de redes virtuales que están vinculadas toohello circuito es menor que 10.</span><span class="sxs-lookup"><span data-stu-id="48932-197">Before you downgrade from premium toostandard, you must ensure that hello number of virtual networks that are linked toohello circuit is less than 10.</span></span> <span data-ttu-id="48932-198">Si no lo hace, se producirá un error en la solicitud de actualización y se le facturará con las tarifas de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="48932-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="48932-199">Tiene que desvincular todas las redes virtuales en otras regiones geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="48932-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="48932-200">Si no lo hace, se producirá un error en la solicitud de actualización y se le facturará con las tarifas de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="48932-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="48932-201">La tabla de enrutamiento tiene que tener menos de 4.000 rutas para el emparejamiento entre pares privados.</span><span class="sxs-lookup"><span data-stu-id="48932-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="48932-202">Si el tamaño de la tabla de ruta es mayor que 4000 rutas, sesión BGP de hello quita y no volver a habilitar hasta que el número de Hola de los prefijos anunciados esté por debajo de 4.000.</span><span class="sxs-lookup"><span data-stu-id="48932-202">If your route table size is greater than 4,000 routes, hello BGP session drops and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="48932-203">Puede deshabilitar el complemento de hello ExpressRoute premium para el circuito existente hello mediante Hola siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="48932-203">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="48932-204">ancho de banda de circuito de ExpressRoute de tooupdate Hola</span><span class="sxs-lookup"><span data-stu-id="48932-204">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="48932-205">Para ver opciones de ancho de banda admitido para el proveedor, compruebe hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="48932-205">For supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="48932-206">Puede elegir cualquier tamaño mayor que el tamaño de Hola de su circuito existente.</span><span class="sxs-lookup"><span data-stu-id="48932-206">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48932-207">Puede tener circuito de ExpressRoute de hello toorecreate si hay capacidad inadecuada en el puerto existente Hola.</span><span class="sxs-lookup"><span data-stu-id="48932-207">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="48932-208">No puede actualizar el circuito de hello si no hay ninguna capacidad adicional disponible en esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="48932-208">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="48932-209">No se puede reducir el ancho de banda de Hola de un circuito de ExpressRoute sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="48932-209">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="48932-210">Degradar de ancho de banda requiere circuito de ExpressRoute de toodeprovision hello y, a continuación, vuelva a aprovisionar un nuevo circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="48932-210">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="48932-211">Después de decidir qué tamaño que sea necesario, utilice Hola después comando tooresize el circuito:</span><span class="sxs-lookup"><span data-stu-id="48932-211">After you decide what size you need, use hello following command tooresize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="48932-212">El circuito se dimensionarán en lado de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="48932-212">Your circuit will be sized up on hello Microsoft side.</span></span> <span data-ttu-id="48932-213">A continuación, debe ponerse en contacto con las configuraciones de tooupdate de proveedor de conectividad en su lado toomatch este cambio.</span><span class="sxs-lookup"><span data-stu-id="48932-213">Then you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="48932-214">Después de realizar esta notificación, empezaremos a facturación para la opción de ancho de banda de hello actualizado.</span><span class="sxs-lookup"><span data-stu-id="48932-214">After you make this notification, we will begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="48932-215">Hola toomove SKU de uso medido toounlimited</span><span class="sxs-lookup"><span data-stu-id="48932-215">toomove hello SKU from metered toounlimited</span></span>
<span data-ttu-id="48932-216">Puede cambiar Hola SKU de un circuito ExpressRoute mediante Hola siguiente fragmento de código de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="48932-216">You can change hello SKU of an ExpressRoute circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="48932-217">clásico de toocontrol acceso toohello y entornos de administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="48932-217">toocontrol access toohello classic and Resource Manager environments</span></span>
<span data-ttu-id="48932-218">Revisar las instrucciones de Hola de [circuitos ExpressRoute mover de modelo de implementación de administrador de recursos de hello toohello clásico](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="48932-218">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="48932-219">Desaprovisionamiento y eliminación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="48932-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="48932-220">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="48932-220">Note hello following:</span></span>

* <span data-ttu-id="48932-221">Debe desvincular todas las redes virtuales de hello circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="48932-221">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="48932-222">Si se produce un error en esta operación, compruebe toosee si las redes virtuales están vinculados toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="48932-222">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="48932-223">Si es el proveedor de servicios del circuito de ExpressRoute de hello estado de aprovisionamiento **Provisioning** o **aprovisionado** debe trabajar con el circuito de Hola de toodeprovision de proveedor de servicio en uno de su lados.</span><span class="sxs-lookup"><span data-stu-id="48932-223">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="48932-224">Se continuará tooreserve recursos y facturar hasta que el proveedor de servicios de hello finaliza desaprovisionamiento circuito de Hola y notifica a nosotros.</span><span class="sxs-lookup"><span data-stu-id="48932-224">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="48932-225">Si el proveedor de servicios de Hola se canceló el aprovisionamiento de circuito de hello (proveedor de servicios de hello estado de aprovisionamiento se establece demasiado**no aprovisionado**), a continuación, puede eliminar el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="48932-225">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="48932-226">Se detendrá la facturación para el circuito de Hola</span><span class="sxs-lookup"><span data-stu-id="48932-226">This will stop billing for hello circuit</span></span>

<span data-ttu-id="48932-227">Puede eliminar el circuito de ExpressRoute ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="48932-227">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="48932-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="48932-228">Next steps</span></span>

<span data-ttu-id="48932-229">Después de crear el circuito, asegúrese de que Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="48932-229">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="48932-230">Crear y modificar el enrutamiento para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="48932-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="48932-231">Vincular el circuito de ExpressRoute de tooyour de red virtual</span><span class="sxs-lookup"><span data-stu-id="48932-231">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
