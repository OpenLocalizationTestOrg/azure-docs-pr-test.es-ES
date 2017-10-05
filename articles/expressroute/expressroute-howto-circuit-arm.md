---
title: "Creación y modificación de un circuito ExpressRoute mediante Powershell y Azure Resource Manager | Microsoft Docs"
description: "Este artículo describe cómo crear, aprovisionar, comprobar, actualizar, eliminar y desaprovisionar un circuito ExpressRoute."
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
ms.openlocfilehash: 8bfae39d84aaac3b9527084df9dcfbd51f591dfe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="883a9-103">Creación y modificación de un circuito ExpressRoute mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="883a9-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="883a9-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="883a9-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="883a9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="883a9-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="883a9-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="883a9-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="883a9-107">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="883a9-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="883a9-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="883a9-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="883a9-109">En este artículo se describe cómo crear un circuito Azure ExpressRoute mediante los cmdlets de PowerShell y el modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="883a9-109">This article describes how to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="883a9-110">En este artículo, también se muestra cómo comprobar el estado del circuito, así como el modo de actualizarlo o eliminarlo y desaprovisionarlo.</span><span class="sxs-lookup"><span data-stu-id="883a9-110">This article also shows you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="883a9-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="883a9-111">Before you begin</span></span>
* <span data-ttu-id="883a9-112">Instale la versión más reciente de los cmdlets de PowerShell de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="883a9-112">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="883a9-113">Para obtener más información, consulte la [Overview of Azure PowerShell](/powershell/azure/overview) (Introducción a Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="883a9-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="883a9-114">Revise los [Requisitos previos y lista de comprobación de ExpressRoute](expressroute-prerequisites.md) y los [Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="883a9-114">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="883a9-115">Creación y aprovisionamiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="883a9-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="883a9-116">1. Iniciar sesión en la cuenta de Azure y seleccione la suscripción</span><span class="sxs-lookup"><span data-stu-id="883a9-116">1. Sign in to your Azure account and select your subscription</span></span>
<span data-ttu-id="883a9-117">Para empezar la configuración, inicie sesión en la cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="883a9-117">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="883a9-118">Use los siguientes ejemplos para conectarse:</span><span class="sxs-lookup"><span data-stu-id="883a9-118">Use the following examples to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="883a9-119">Compruebe las suscripciones para la cuenta:</span><span class="sxs-lookup"><span data-stu-id="883a9-119">Check the subscriptions for the account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="883a9-120">Seleccione la suscripción para la que desea crear un circuito ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="883a9-120">Select the subscription that you want to create an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="883a9-121">2. Obtención de la lista de proveedores, ubicaciones y anchos de banda admitidos</span><span class="sxs-lookup"><span data-stu-id="883a9-121">2. Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="883a9-122">Para crear un circuito ExpressRoute, necesita la lista de proveedores de conectividad, ubicaciones y opciones de ancho de banda admitidas.</span><span class="sxs-lookup"><span data-stu-id="883a9-122">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="883a9-123">El cmdlet de PowerShell **Get-AzureRmExpressRouteServiceProvider** devuelve esta información, que se usará en pasos posteriores:</span><span class="sxs-lookup"><span data-stu-id="883a9-123">The PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="883a9-124">Compruebe si aparece su proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="883a9-124">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="883a9-125">Tome nota de la siguiente información.</span><span class="sxs-lookup"><span data-stu-id="883a9-125">Make a note of the following information.</span></span> <span data-ttu-id="883a9-126">La necesitará más adelante cuando cree un circuito.</span><span class="sxs-lookup"><span data-stu-id="883a9-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="883a9-127">Nombre</span><span class="sxs-lookup"><span data-stu-id="883a9-127">Name</span></span>
* <span data-ttu-id="883a9-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="883a9-128">PeeringLocations</span></span>
* <span data-ttu-id="883a9-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="883a9-129">BandwidthsOffered</span></span>

<span data-ttu-id="883a9-130">Ahora está listo para crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="883a9-130">You're now ready to create an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="883a9-131">3. Creación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="883a9-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="883a9-132">Si todavía no tiene un grupo de recursos, debe crear uno antes de crear ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="883a9-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="883a9-133">Para ello, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="883a9-133">You can do so by running the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="883a9-134">En el ejemplo siguiente se muestra cómo crear un circuito ExpressRoute de 200 Mbps a través de Equinix en Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="883a9-134">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="883a9-135">Si usa otro proveedor y otra configuración, sustituya esa información al realizar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="883a9-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="883a9-136">A continuación se muestra un ejemplo de solicitud para una nueva clave de servicio:</span><span class="sxs-lookup"><span data-stu-id="883a9-136">The following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="883a9-137">Asegúrese de que especifica el nivel y la familia correctos de SKU.</span><span class="sxs-lookup"><span data-stu-id="883a9-137">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="883a9-138">El nivel de SKU determina si está habilitado un complemento estándar o premium de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="883a9-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="883a9-139">Puede especificar *Estándar* para obtener la SKU estándar o *Premium* si quiere el complemento Premium.</span><span class="sxs-lookup"><span data-stu-id="883a9-139">You can specify *Standard* to get the standard SKU or *Premium* for the premium add-on.</span></span>
* <span data-ttu-id="883a9-140">La familia de SKU determina el tipo de facturación.</span><span class="sxs-lookup"><span data-stu-id="883a9-140">SKU family determines the billing type.</span></span> <span data-ttu-id="883a9-141">Puede seleccionar *Metereddata* para el plan de datos limitado y *Unlimiteddata* para el plan de datos ilimitado.</span><span class="sxs-lookup"><span data-stu-id="883a9-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="883a9-142">Puede cambiar el tipo de facturación de *Metereddata* a *Unlimiteddata*, pero no se puede cambiar el tipo de *Unlimiteddata* a *Metereddata*.</span><span class="sxs-lookup"><span data-stu-id="883a9-142">You can change the billing type from *Metereddata* to *Unlimiteddata*, but you can't change the type from *Unlimiteddata* to *Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="883a9-143">El circuito ExpressRoute se facturará a partir del momento en que se emita una clave de servicio.</span><span class="sxs-lookup"><span data-stu-id="883a9-143">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="883a9-144">Asegúrese de realizar esta operación cuando el proveedor de conectividad esté listo para aprovisionar el circuito.</span><span class="sxs-lookup"><span data-stu-id="883a9-144">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="883a9-145">La respuesta contiene la clave del servicio.</span><span class="sxs-lookup"><span data-stu-id="883a9-145">The response contains the service key.</span></span> <span data-ttu-id="883a9-146">Puede obtener una descripción detallada de todos los parámetros ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="883a9-146">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="883a9-147">4. Lista de todos los circuitos ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="883a9-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="883a9-148">Para obtener una lista de todos los circuitos ExpressRoute que haya creado, ejecute el comando **Get-AzureRmExpressRouteCircuit**:</span><span class="sxs-lookup"><span data-stu-id="883a9-148">To get a list of all the ExpressRoute circuits that you created, run the **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="883a9-149">La respuesta será similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="883a9-149">The response will look similar to the following example:</span></span>

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

<span data-ttu-id="883a9-150">Esta información se puede recuperar en cualquier momento con el cmdlet `Get-AzureRmExpressRouteCircuit` .</span><span class="sxs-lookup"><span data-stu-id="883a9-150">You can retrieve this information at any time by using the `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="883a9-151">Si se realiza la llamada sin parámetros, se obtendrá una lista de todos los circuitos.</span><span class="sxs-lookup"><span data-stu-id="883a9-151">Making the call with no parameters lists all the circuits.</span></span> <span data-ttu-id="883a9-152">La clave de servicio se mostrará en el campo *ServiceKey* :</span><span class="sxs-lookup"><span data-stu-id="883a9-152">Your service key will be listed in the *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="883a9-153">La respuesta será similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="883a9-153">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="883a9-154">Puede obtener una descripción detallada de todos los parámetros ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="883a9-154">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="883a9-155">5. Envío de la clave de servicio al proveedor de conectividad para el aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="883a9-155">5. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="883a9-156">*ServiceProviderProvisioningState* da información sobre el estado actual del aprovisionamiento en el lado del proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="883a9-156">*ServiceProviderProvisioningState* provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="883a9-157">"Status" proporciona el estado relativo al lado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="883a9-157">Status provides the state on the Microsoft side.</span></span> <span data-ttu-id="883a9-158">Para más información sobre los estados de aprovisionamiento del circuito, consulte el artículo [Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="883a9-158">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="883a9-159">Cuando se crea un nuevo circuito ExpressRoute, dicho circuito estará en el siguiente estado:</span><span class="sxs-lookup"><span data-stu-id="883a9-159">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="883a9-160">El circuito cambiará al estado siguiente cuando el proveedor de conectividad se encuentre en el proceso de habilitarlo:</span><span class="sxs-lookup"><span data-stu-id="883a9-160">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="883a9-161">Para poder usar un circuito ExpressRoute, dicho circuito tiene que estar en el siguiente estado.</span><span class="sxs-lookup"><span data-stu-id="883a9-161">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="883a9-162">6. Comprobación periódica del estado y la condición de la clave del circuito</span><span class="sxs-lookup"><span data-stu-id="883a9-162">6. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="883a9-163">La comprobación del estado y la condición de la clave de circuito le informa cuando el proveedor ha habilitado el circuito.</span><span class="sxs-lookup"><span data-stu-id="883a9-163">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="883a9-164">Después de configurar el circuito, *ServiceProviderProvisioningState* aparece como *Provisioned*, tal como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="883a9-164">After the circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in the following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="883a9-165">La respuesta será similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="883a9-165">The response will look similar to the following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="883a9-166">7. Creación de la configuración de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="883a9-166">7. Create your routing configuration</span></span>
<span data-ttu-id="883a9-167">Consulte [Creación y modificación del enrutamiento de un circuito ExpressRoute mediante PowerShell](expressroute-howto-routing-arm.md) para ver las instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="883a9-167">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="883a9-168">Estas instrucciones se aplican solo a los circuitos creados con proveedores de servicios que ofrecen servicios de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="883a9-168">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="883a9-169">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="883a9-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="883a9-170">8. Vinculación de una red virtual a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="883a9-170">8. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="883a9-171">A continuación, vincule una red virtual a su circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="883a9-171">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="883a9-172">Consulte el artículo [Vinculación de redes virtuales a circuitos ExpressRoute](expressroute-howto-linkvnet-arm.md) al trabajar con el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="883a9-172">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="883a9-173">Obtención del estado de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="883a9-173">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="883a9-174">Esta información se puede recuperar en cualquier momento con el cmdlet **Get-AzureRmExpressRouteCircuit**.</span><span class="sxs-lookup"><span data-stu-id="883a9-174">You can retrieve this information at any time by using the **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="883a9-175">Si se realiza la llamada sin parámetros, se obtendrá una lista de todos los circuitos.</span><span class="sxs-lookup"><span data-stu-id="883a9-175">Making the call with no parameters lists all the circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="883a9-176">La respuesta será similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="883a9-176">The response will be similar to the following example:</span></span>

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


<span data-ttu-id="883a9-177">Se puede obtener información sobre un circuito ExpressRoute específico si se pasa el nombre del grupo de recursos y el nombre del circuito como parámetro a la llamada:</span><span class="sxs-lookup"><span data-stu-id="883a9-177">You can get information on a specific ExpressRoute circuit by passing the resource group name and circuit name as a parameter to the call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="883a9-178">La respuesta será similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="883a9-178">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="883a9-179">Puede obtener una descripción detallada de todos los parámetros ejecutando el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="883a9-179">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="883a9-180"><a name="modify"></a>Modificación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="883a9-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="883a9-181">Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad.</span><span class="sxs-lookup"><span data-stu-id="883a9-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="883a9-182">Puede hacer lo siguiente sin experimentar tiempo de inactividad:</span><span class="sxs-lookup"><span data-stu-id="883a9-182">You can do the following with no downtime:</span></span>

* <span data-ttu-id="883a9-183">Habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="883a9-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="883a9-184">Aumente el ancho de banda del circuito ExpressRoute, siempre que haya capacidad disponible en el puerto.</span><span class="sxs-lookup"><span data-stu-id="883a9-184">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="883a9-185">No se admite la degradación del ancho de banda de un circuito.</span><span class="sxs-lookup"><span data-stu-id="883a9-185">Downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="883a9-186">Cambio del plan de medición de datos limitados a datos ilimitados.</span><span class="sxs-lookup"><span data-stu-id="883a9-186">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="883a9-187">No se admite cambiar el plan de medición de datos ilimitados a datos limitados.</span><span class="sxs-lookup"><span data-stu-id="883a9-187">Changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="883a9-188">Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).</span><span class="sxs-lookup"><span data-stu-id="883a9-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="883a9-189">Consulte la página [P+F de ExpressRoute](expressroute-faqs.md)para más información sobre los límites y las limitaciones.</span><span class="sxs-lookup"><span data-stu-id="883a9-189">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="883a9-190">Para habilitar el complemento ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="883a9-190">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="883a9-191">Puede habilitar el complemento ExpressRoute Premium para el circuito existente mediante el siguiente fragmento de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="883a9-191">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="883a9-192">El circuito tendrá ahora las características del complemento ExpressRoute Premium habilitadas.</span><span class="sxs-lookup"><span data-stu-id="883a9-192">The circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="883a9-193">La facturación de la capacidad del complemento Premium comienza en cuanto el comando se ejecuta correctamente.</span><span class="sxs-lookup"><span data-stu-id="883a9-193">We will begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="883a9-194">Para deshabilitar el complemento ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="883a9-194">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="883a9-195">Esta operación puede producir un error si usa recursos que son más grandes de lo que está permitido para el circuito estándar.</span><span class="sxs-lookup"><span data-stu-id="883a9-195">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

<span data-ttu-id="883a9-196">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="883a9-196">Note the following:</span></span>

* <span data-ttu-id="883a9-197">Debe asegurarse de que el número de redes virtuales vinculadas al circuito es inferior a 10 antes de realizar la degradación de Premium a Estándar.</span><span class="sxs-lookup"><span data-stu-id="883a9-197">Before you downgrade from premium to standard, you must ensure that the number of virtual networks that are linked to the circuit is less than 10.</span></span> <span data-ttu-id="883a9-198">Si no lo hace, se producirá un error en la solicitud de actualización y se le facturará con las tarifas de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="883a9-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="883a9-199">Tiene que desvincular todas las redes virtuales en otras regiones geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="883a9-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="883a9-200">Si no lo hace, se producirá un error en la solicitud de actualización y se le facturará con las tarifas de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="883a9-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="883a9-201">La tabla de enrutamiento tiene que tener menos de 4.000 rutas para el emparejamiento entre pares privados.</span><span class="sxs-lookup"><span data-stu-id="883a9-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="883a9-202">Si el tamaño de la tabla de ruta sobrepasa las 4.000 rutas, la sesión BGP se anulará y no se volverá a habilitar hasta que el número de prefijos anunciados esté por debajo de 4.000.</span><span class="sxs-lookup"><span data-stu-id="883a9-202">If your route table size is greater than 4,000 routes, the BGP session drops and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="883a9-203">Puede deshabilitar el complemento ExpressRoute Premium en el circuito existente mediante el siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="883a9-203">You can disable the ExpressRoute premium add-on for the existing circuit by using the following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="883a9-204">Para actualizar el ancho de banda del circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="883a9-204">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="883a9-205">Consulte la página [P+F de ExpressRoute](expressroute-faqs.md)para conocer las opciones de ancho de banda compatibles con su proveedor.</span><span class="sxs-lookup"><span data-stu-id="883a9-205">For supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="883a9-206">Puede elegir cualquier tamaño mayor que el tamaño de su circuito existente.</span><span class="sxs-lookup"><span data-stu-id="883a9-206">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="883a9-207">Si el puerto existente no tiene la capacidad adecuada, tendrá que volver a crear el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="883a9-207">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="883a9-208">El circuito no se puede actualizar si no hay más capacidad disponible en la ubicación.</span><span class="sxs-lookup"><span data-stu-id="883a9-208">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="883a9-209">No podrá reducir el ancho de banda de un circuito ExpressRoute sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="883a9-209">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="883a9-210">Para degradar un ancho de banda, es necesario desaprovisionar el circuito ExpressRoute y luego volver a aprovisionar un nuevo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="883a9-210">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="883a9-211">Cuando haya decidido el tamaño que necesita, use el comando siguiente para cambiar el tamaño del circuito:</span><span class="sxs-lookup"><span data-stu-id="883a9-211">After you decide what size you need, use the following command to resize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="883a9-212">El circuito se cambiará de tamaño en el lado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="883a9-212">Your circuit will be sized up on the Microsoft side.</span></span> <span data-ttu-id="883a9-213">Así pues, debe ponerse en contacto con su proveedor de conectividad para actualizar las configuraciones de su parte para que coincidan con este cambio.</span><span class="sxs-lookup"><span data-stu-id="883a9-213">Then you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="883a9-214">Después de realizar esta notificación, se le empezará a facturar por la opción de ancho de banda actualizada.</span><span class="sxs-lookup"><span data-stu-id="883a9-214">After you make this notification, we will begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="883a9-215">Para pasar la SKU de limitada a ilimitada</span><span class="sxs-lookup"><span data-stu-id="883a9-215">To move the SKU from metered to unlimited</span></span>
<span data-ttu-id="883a9-216">Puede cambiar la SKU de un circuito ExpressRoute mediante el siguiente fragmento de código de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="883a9-216">You can change the SKU of an ExpressRoute circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="883a9-217">Para controlar el acceso a los entornos de implementación clásica y del Resource Manager</span><span class="sxs-lookup"><span data-stu-id="883a9-217">To control access to the classic and Resource Manager environments</span></span>
<span data-ttu-id="883a9-218">Revise las instrucciones que se ofrecen en [Transición de los circuitos ExpressRoute desde el modelo de implementación clásica al modelo de implementación de Resource Manager](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="883a9-218">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="883a9-219">Desaprovisionamiento y eliminación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="883a9-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="883a9-220">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="883a9-220">Note the following:</span></span>

* <span data-ttu-id="883a9-221">Tiene que desvincular todas las redes virtuales del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="883a9-221">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="883a9-222">Si se produce un error en esta operación, compruebe si hay alguna red virtual vinculada al circuito.</span><span class="sxs-lookup"><span data-stu-id="883a9-222">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="883a9-223">Si el estado de aprovisionamiento del proveedor de servicios del circuito ExpressRoute es **Aprovisionando** o **Aprovisionado**, debe colaborar con su proveedor de servicios para que desaprovisionen el circuito.</span><span class="sxs-lookup"><span data-stu-id="883a9-223">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="883a9-224">Se le continuará reservando recursos y facturándole por ello hasta que el proveedor de servicios complete el desaprovisionamiento del circuito y nos lo notifique.</span><span class="sxs-lookup"><span data-stu-id="883a9-224">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="883a9-225">Si el proveedor de servicios ha desaprovisionado el circuito (el estado de aprovisionamiento del proveedor de servicios está establecido en **No aprovisionado**), puede eliminar el circuito.</span><span class="sxs-lookup"><span data-stu-id="883a9-225">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="883a9-226">Esto detendrá la facturación del circuito.</span><span class="sxs-lookup"><span data-stu-id="883a9-226">This will stop billing for the circuit</span></span>

<span data-ttu-id="883a9-227">Puede eliminar el circuito ExpressRout con la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="883a9-227">You can delete your ExpressRoute circuit by running the following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="883a9-228">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="883a9-228">Next steps</span></span>

<span data-ttu-id="883a9-229">Después de crear el circuito, asegúrese de hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="883a9-229">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="883a9-230">Crear y modificar el enrutamiento para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="883a9-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="883a9-231">Vincular la red virtual a su circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="883a9-231">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
