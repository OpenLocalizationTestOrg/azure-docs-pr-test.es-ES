---
title: "Creación y modificación de un circuito ExpressRoute mediante Powershell y Azure clásico | Microsoft Docs"
description: "Este artículo le guiará por los pasos necesarios para crear y aprovisionar un circuito ExpressRoute. También se muestra cómo comprobar el estado, actualizar, o eliminar y desaprovisionar un circuito ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 3b12bbb21ebf6a0160227c4a281c420cf192d6f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="9ac61-104">Creación y modificación de un circuito ExpressRoute mediante PowerShell (clásica)</span><span class="sxs-lookup"><span data-stu-id="9ac61-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ac61-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9ac61-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="9ac61-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ac61-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="9ac61-107">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="9ac61-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="9ac61-108">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9ac61-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="9ac61-109">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="9ac61-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="9ac61-110">Este artículo le guiará por los pasos necesarios para crear un circuito ExpressRoute de Azure con los cmdlets de PowerShell y el modelo clásico de implementación.</span><span class="sxs-lookup"><span data-stu-id="9ac61-110">This article walks you through the steps to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the classic deployment model.</span></span> <span data-ttu-id="9ac61-111">En este artículo, también se muestra cómo comprobar el estado de un circuito ExpressRoute, así como el modo de actualizarlo o eliminarlo y desaprovisionarlo.</span><span class="sxs-lookup"><span data-stu-id="9ac61-111">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="9ac61-112">**Información acerca de los modelos de implementación de Azure**</span><span class="sxs-lookup"><span data-stu-id="9ac61-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="9ac61-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="9ac61-113">Before you begin</span></span>
### <a name="step-1-review-the-prerequisites-and-workflow-articles"></a><span data-ttu-id="9ac61-114">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="9ac61-114">Step 1.</span></span> <span data-ttu-id="9ac61-115">Revise los requisitos previos y los artículos de flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9ac61-115">Review the prerequisites and workflow articles</span></span>
<span data-ttu-id="9ac61-116">Asegúrese de haber revisado los [requisitos previos](expressroute-prerequisites.md) y los [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="9ac61-116">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-the-latest-versions-of-the-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="9ac61-117">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="9ac61-117">Step 2.</span></span> <span data-ttu-id="9ac61-118">Instale las versiones más recientes de los módulos de Azure PowerShell para Service Management (SM).</span><span class="sxs-lookup"><span data-stu-id="9ac61-118">Install the latest versions of the Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="9ac61-119">Para obtener instrucciones detalladas sobre cómo configurar el equipo para usar los módulos de Azure PowerShell, siga las indicaciones que aparecen en [Introducción a los cmdlets de PowerShell para Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9ac61-119">Follow the instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="9ac61-120">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="9ac61-120">Step 3.</span></span> <span data-ttu-id="9ac61-121">Inicie sesión en la cuenta de Azure y seleccione la suscripción.</span><span class="sxs-lookup"><span data-stu-id="9ac61-121">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="9ac61-122">Abra la consola de PowerShell con privilegios elevados y conéctela a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="9ac61-122">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="9ac61-123">Use el siguiente ejemplo para conectarse:</span><span class="sxs-lookup"><span data-stu-id="9ac61-123">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="9ac61-124">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="9ac61-124">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="9ac61-125">Si tiene varias suscripciones, seleccione la que quiera usar.</span><span class="sxs-lookup"><span data-stu-id="9ac61-125">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="9ac61-126">A continuación, use el cmdlet siguiente para agregar la suscripción de Azure a PowerShell para el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="9ac61-126">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="9ac61-127">Creación y aprovisionamiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-the-powershell-modules-for-expressroute"></a><span data-ttu-id="9ac61-128">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="9ac61-128">Step 1.</span></span> <span data-ttu-id="9ac61-129">Importación del módulo de PowerShell para ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-129">Import the PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="9ac61-130">Si aún no lo ha hecho, tiene que importar los módulos de Azure y ExpressRoute en la sesión de PowerShell para poder usar los cmdlets de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9ac61-130">If you have not already done so, you must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="9ac61-131">Importe los módulos de la ubicación donde estaban instaladas en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="9ac61-131">You import the modules from the location that they were installed to on your local computer.</span></span> <span data-ttu-id="9ac61-132">Según el método utilizado para instalar los módulos, la ubicación puede ser diferente a la que se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="9ac61-132">Depending on the method you used to install the modules, the location may be different than the following example shows.</span></span> <span data-ttu-id="9ac61-133">Si es necesario, modifique el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9ac61-133">Modify the example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="9ac61-134">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="9ac61-134">Step 2.</span></span> <span data-ttu-id="9ac61-135">Obtención de la lista de proveedores, ubicaciones y anchos de banda admitidos</span><span class="sxs-lookup"><span data-stu-id="9ac61-135">Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="9ac61-136">Para crear un circuito ExpressRoute, necesita la lista de proveedores de conectividad, ubicaciones y opciones de ancho de banda admitidas.</span><span class="sxs-lookup"><span data-stu-id="9ac61-136">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="9ac61-137">El cmdlet de PowerShell `Get-AzureDedicatedCircuitServiceProvider` devuelve esta información, que se usará en pasos posteriores:</span><span class="sxs-lookup"><span data-stu-id="9ac61-137">The PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="9ac61-138">Compruebe si aparece su proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="9ac61-138">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="9ac61-139">Tome nota de la siguiente información, porque la necesitará más adelante cuando cree un circuito:</span><span class="sxs-lookup"><span data-stu-id="9ac61-139">Make a note of the following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="9ac61-140">Nombre</span><span class="sxs-lookup"><span data-stu-id="9ac61-140">Name</span></span>
* <span data-ttu-id="9ac61-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="9ac61-141">PeeringLocations</span></span>
* <span data-ttu-id="9ac61-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="9ac61-142">BandwidthsOffered</span></span>

<span data-ttu-id="9ac61-143">Ahora está listo para crear un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9ac61-143">You're now ready to create an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="9ac61-144">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="9ac61-144">Step 3.</span></span> <span data-ttu-id="9ac61-145">Creación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="9ac61-146">En el ejemplo siguiente se muestra cómo crear un circuito ExpressRoute de 200 Mbps a través de Equinix en Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="9ac61-146">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="9ac61-147">Si usa otro proveedor y otra configuración, sustituya esa información al realizar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="9ac61-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ac61-148">El circuito ExpressRoute se facturará a partir del momento en que se emita una clave de servicio.</span><span class="sxs-lookup"><span data-stu-id="9ac61-148">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="9ac61-149">Asegúrese de realizar esta operación cuando el proveedor de conectividad esté listo para aprovisionar el circuito.</span><span class="sxs-lookup"><span data-stu-id="9ac61-149">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="9ac61-150">A continuación se muestra un ejemplo de solicitud para una nueva clave de servicio:</span><span class="sxs-lookup"><span data-stu-id="9ac61-150">The following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="9ac61-151">O bien, si desea crear un circuito ExpressRoute con el complemento Premium, use el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9ac61-151">Or, if you want to create an ExpressRoute circuit with the premium add-on, use the following example.</span></span> <span data-ttu-id="9ac61-152">Consulte la página [P+F de ExpressRoute](expressroute-faqs.md) para más información sobre el complemento Premium.</span><span class="sxs-lookup"><span data-stu-id="9ac61-152">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more details about the premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="9ac61-153">La respuesta contendrá la clave del servicio.</span><span class="sxs-lookup"><span data-stu-id="9ac61-153">The response will contain the service key.</span></span> <span data-ttu-id="9ac61-154">Puede obtener una descripción detallada de todos los parámetros ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9ac61-154">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-the-expressroute-circuits"></a><span data-ttu-id="9ac61-155">Paso 4</span><span class="sxs-lookup"><span data-stu-id="9ac61-155">Step 4.</span></span> <span data-ttu-id="9ac61-156">Lista de todos los circuitos ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-156">List all the ExpressRoute circuits</span></span>
<span data-ttu-id="9ac61-157">Para obtener una lista de todos los circuitos ExpressRoute que haya creado, ejecute el comando `Get-AzureDedicatedCircuit`:</span><span class="sxs-lookup"><span data-stu-id="9ac61-157">You can run the `Get-AzureDedicatedCircuit` command to get a list of all the ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="9ac61-158">La respuesta será similar al siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9ac61-158">The response will be something similar to the following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="9ac61-159">Esta información se puede recuperar en cualquier momento con el cmdlet `Get-AzureDedicatedCircuit` .</span><span class="sxs-lookup"><span data-stu-id="9ac61-159">You can retrieve this information at any time by using the `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="9ac61-160">Si se realiza la llamada sin parámetros, se obtendrá una lista de todos los circuitos.</span><span class="sxs-lookup"><span data-stu-id="9ac61-160">Making the call without any parameters lists all the circuits.</span></span> <span data-ttu-id="9ac61-161">La clave de servicio se mostrará en el campo *ServiceKey* .</span><span class="sxs-lookup"><span data-stu-id="9ac61-161">Your service key will be listed in the *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="9ac61-162">Puede obtener una descripción detallada de todos los parámetros ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9ac61-162">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="9ac61-163">Paso 5.</span><span class="sxs-lookup"><span data-stu-id="9ac61-163">Step 5.</span></span> <span data-ttu-id="9ac61-164">Envío de la clave de servicio al proveedor de conectividad para el aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="9ac61-164">Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="9ac61-165">*ServiceProviderProvisioningState* da información sobre el estado actual del aprovisionamiento en el lado del proveedor de servicios.</span><span class="sxs-lookup"><span data-stu-id="9ac61-165">*ServiceProviderProvisioningState* provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="9ac61-166">*Status* proporciona el estado relativo al lado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9ac61-166">*Status* provides the state on the Microsoft side.</span></span> <span data-ttu-id="9ac61-167">Para más información sobre los estados de aprovisionamiento del circuito, consulte el artículo [Flujos de trabajo de ExpressRoute para aprovisionamiento de circuitos y estados de circuitos de ExpressRoute](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="9ac61-167">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="9ac61-168">Cuando se crea un nuevo circuito ExpressRoute, dicho circuito estará en el siguiente estado:</span><span class="sxs-lookup"><span data-stu-id="9ac61-168">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="9ac61-169">El circuito pasará al estado siguiente cuando el proveedor de conectividad se encuentre en el proceso de habilitarlo:</span><span class="sxs-lookup"><span data-stu-id="9ac61-169">The circuit will go to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="9ac61-170">Un circuito ExpressRoute tiene que estar en el siguiente estado para poder usarlo:</span><span class="sxs-lookup"><span data-stu-id="9ac61-170">An ExpressRoute circuit must be in the following state for you to be able to use it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="9ac61-171">Paso 6.</span><span class="sxs-lookup"><span data-stu-id="9ac61-171">Step 6.</span></span> <span data-ttu-id="9ac61-172">Comprobación periódica del estado y la condición de la clave del circuito</span><span class="sxs-lookup"><span data-stu-id="9ac61-172">Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="9ac61-173">Esto le permitirá saber cuándo ha habilitado el circuito el proveedor.</span><span class="sxs-lookup"><span data-stu-id="9ac61-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="9ac61-174">Después de configurar el circuito, *ServiceProviderProvisioningState* aparece como *Provisioned*, tal como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9ac61-174">After the circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in the following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="9ac61-175">Paso 7.</span><span class="sxs-lookup"><span data-stu-id="9ac61-175">Step 7.</span></span> <span data-ttu-id="9ac61-176">Creación de la configuración de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="9ac61-176">Create your routing configuration</span></span>
<span data-ttu-id="9ac61-177">Consulte el artículo [Configuración de enrutamiento de circuitos ExpressRoute (crear y modificar emparejamientos de circuito)](expressroute-howto-routing-classic.md) para obtener instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="9ac61-177">Refer to the [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ac61-178">Estas instrucciones se aplican solo a los circuitos creados con proveedores de servicios que ofrecen servicios de conectividad de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="9ac61-178">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="9ac61-179">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="9ac61-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="9ac61-180">Paso 8.</span><span class="sxs-lookup"><span data-stu-id="9ac61-180">Step 8.</span></span> <span data-ttu-id="9ac61-181">Vinculación de una red virtual a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-181">Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="9ac61-182">A continuación, vincule una red virtual a su circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9ac61-182">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="9ac61-183">Consulte [Vinculación de una red virtual a un circuito ExpressRoute](expressroute-howto-linkvnet-classic.md) para obtener instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="9ac61-183">Refer to [Linking ExpressRoute circuits to virtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="9ac61-184">Si necesita crear una red virtual con el modelo de implementación clásica de ExpressRoute, consulte [Creación de una red virtual para ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="9ac61-184">If you need to create a virtual network using the classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="9ac61-185">Obtención del estado de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-185">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="9ac61-186">Esta información se puede recuperar en cualquier momento con el cmdlet `Get-AzureCircuit` .</span><span class="sxs-lookup"><span data-stu-id="9ac61-186">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="9ac61-187">Si se realiza la llamada sin parámetros, se obtendrá una lista de todos los circuitos.</span><span class="sxs-lookup"><span data-stu-id="9ac61-187">Making the call without any parameters lists all the circuits.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="9ac61-188">Puede obtener información sobre un circuito ExpressRoute específico, pasando la clave de servicio como un parámetro a la llamada.</span><span class="sxs-lookup"><span data-stu-id="9ac61-188">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="9ac61-189">Puede obtener una descripción detallada de todos los parámetros ejecutando el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9ac61-189">You can get detailed descriptions of all the parameters by running the following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="9ac61-190">Modificación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="9ac61-191">Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad.</span><span class="sxs-lookup"><span data-stu-id="9ac61-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="9ac61-192">Puede hacer lo siguiente sin experimentar tiempo de inactividad:</span><span class="sxs-lookup"><span data-stu-id="9ac61-192">You can do the following with no downtime:</span></span>

* <span data-ttu-id="9ac61-193">Habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9ac61-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="9ac61-194">Aumente el ancho de banda del circuito ExpressRoute, siempre que haya capacidad disponible en el puerto.</span><span class="sxs-lookup"><span data-stu-id="9ac61-194">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="9ac61-195">Tenga en cuenta que no se admite la degradación del ancho de banda de un circuito.</span><span class="sxs-lookup"><span data-stu-id="9ac61-195">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="9ac61-196">Cambio del plan de medición de datos limitados a datos ilimitados.</span><span class="sxs-lookup"><span data-stu-id="9ac61-196">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="9ac61-197">Tenga en cuenta que no es posible cambiar el plan de medición de datos ilimitados a datos limitados.</span><span class="sxs-lookup"><span data-stu-id="9ac61-197">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="9ac61-198">Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).</span><span class="sxs-lookup"><span data-stu-id="9ac61-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="9ac61-199">Consulte la página [P+F de ExpressRoute](expressroute-faqs.md) para más información sobre los límites y las limitaciones.</span><span class="sxs-lookup"><span data-stu-id="9ac61-199">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="9ac61-200">Para habilitar el complemento ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="9ac61-200">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="9ac61-201">Puede habilitar el complemento ExpressRoute Premium en el circuito existente mediante el siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9ac61-201">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="9ac61-202">El circuito tendrá ahora las características del complemento ExpressRoute Premium habilitadas.</span><span class="sxs-lookup"><span data-stu-id="9ac61-202">Your circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="9ac61-203">Tenga en cuenta que la facturación de la capacidad del complemento Premium comienza en cuanto el comando se ejecuta correctamente.</span><span class="sxs-lookup"><span data-stu-id="9ac61-203">Note that we will start billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="9ac61-204">Para deshabilitar el complemento ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="9ac61-204">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9ac61-205">Esta operación puede producir un error si usa recursos que son más grandes de lo que está permitido para el circuito estándar.</span><span class="sxs-lookup"><span data-stu-id="9ac61-205">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="9ac61-206">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="9ac61-206">Considerations</span></span>

* <span data-ttu-id="9ac61-207">Debe asegurarse de que el número de redes virtuales vinculadas al circuito es inferior a 10 antes de realizar la degradación de Premium a estándar.</span><span class="sxs-lookup"><span data-stu-id="9ac61-207">You must ensure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span></span> <span data-ttu-id="9ac61-208">Si no lo hace, se producirá un error en la solicitud de actualización y se le facturará con las tarifas Premium.</span><span class="sxs-lookup"><span data-stu-id="9ac61-208">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="9ac61-209">Tiene que desvincular todas las redes virtuales en otras regiones geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="9ac61-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="9ac61-210">Si no lo hace, se producirá un error en la solicitud de actualización y se le facturará con las tarifas Premium.</span><span class="sxs-lookup"><span data-stu-id="9ac61-210">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="9ac61-211">La tabla de enrutamiento tiene que tener menos de 4.000 rutas para el emparejamiento entre pares privados.</span><span class="sxs-lookup"><span data-stu-id="9ac61-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="9ac61-212">Si el tamaño de la tabla de ruta sobrepasa las 4.000 rutas, la sesión BGP se anulará y no se volverá a habilitar hasta que el número de prefijos anunciados esté por debajo de 4.000.</span><span class="sxs-lookup"><span data-stu-id="9ac61-212">If your route table size is greater than 4,000 routes, the BGP session will drop and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-the-premium-add-on"></a><span data-ttu-id="9ac61-213">Deshabilitamiento del complemento de premium</span><span class="sxs-lookup"><span data-stu-id="9ac61-213">Disable the premium add-on</span></span>
<span data-ttu-id="9ac61-214">Puede deshabilitar el complemento ExpressRoute Premium en el circuito existente mediante el siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9ac61-214">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="9ac61-215">Para actualizar el ancho de banda del circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-215">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="9ac61-216">Consulte la página [P+F de ExpressRoute](expressroute-faqs.md) para conocer las opciones de ancho de banda compatibles con su proveedor.</span><span class="sxs-lookup"><span data-stu-id="9ac61-216">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="9ac61-217">Puede elegir cualquier tamaño que sea mayor que el de su circuito existente siempre que lo permita el puerto físico (en el que se creó el circuito).</span><span class="sxs-lookup"><span data-stu-id="9ac61-217">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ac61-218">Si el puerto existente no tiene la capacidad adecuada, tendrá que volver a crear el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9ac61-218">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="9ac61-219">El circuito no se puede actualizar si no hay más capacidad disponible en la ubicación.</span><span class="sxs-lookup"><span data-stu-id="9ac61-219">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="9ac61-220">No podrá reducir el ancho de banda de un circuito ExpressRoute sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="9ac61-220">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="9ac61-221">Para degradar un ancho de banda, es necesario desaprovisionar el circuito ExpressRoute y luego volver a aprovisionar un nuevo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9ac61-221">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="9ac61-222">Cambio del tamaño de un circuito</span><span class="sxs-lookup"><span data-stu-id="9ac61-222">Resize a circuit</span></span>

<span data-ttu-id="9ac61-223">Después de decidir el tamaño que necesita, puede usar el comando siguiente para cambiar el tamaño del circuito:</span><span class="sxs-lookup"><span data-stu-id="9ac61-223">After you decide what size you need, you can use the following command to resize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="9ac61-224">El circuito habrá cambiado de tamaño en el lado de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9ac61-224">Your circuit will have been sized up on the Microsoft side.</span></span> <span data-ttu-id="9ac61-225">Debe ponerse en contacto con su proveedor de conectividad para actualizar las configuraciones de su parte para que coincidan con este cambio.</span><span class="sxs-lookup"><span data-stu-id="9ac61-225">You must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="9ac61-226">Tenga en cuenta que le facturará la opción de ancho de banda actualizada desde este momento.</span><span class="sxs-lookup"><span data-stu-id="9ac61-226">Note that we will start billing you for the updated bandwidth option from this point on.</span></span>

<span data-ttu-id="9ac61-227">Si ve el siguiente error al aumentar el ancho de banda de circuito, significa que no queda suficiente ancho de banda en el puerto físico donde se creó el circuito existente.</span><span class="sxs-lookup"><span data-stu-id="9ac61-227">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span></span> <span data-ttu-id="9ac61-228">Tendrá que eliminar el circuito y crear uno nuevo del tamaño que necesite.</span><span class="sxs-lookup"><span data-stu-id="9ac61-228">You have to delete this circuit and create a new circuit of the size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available to perform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="9ac61-229">Desaprovisionamiento y eliminación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="9ac61-230">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="9ac61-230">Considerations</span></span>

* <span data-ttu-id="9ac61-231">Para realizar esta operación correctamente, tiene que desvincular todas las redes virtuales del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9ac61-231">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span></span> <span data-ttu-id="9ac61-232">Si se produce un error en esta operación compruebe si tiene alguna red virtual vinculada al circuito.</span><span class="sxs-lookup"><span data-stu-id="9ac61-232">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span></span>
* <span data-ttu-id="9ac61-233">Si el estado de aprovisionamiento del proveedor de servicios del circuito ExpressRoute es **Aprovisionando** o **Aprovisionado**, debe colaborar con su proveedor de servicios para que desaprovisionen el circuito.</span><span class="sxs-lookup"><span data-stu-id="9ac61-233">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="9ac61-234">Se le continuará reservando recursos y facturándole por ello hasta que el proveedor de servicios complete el desaprovisionamiento del circuito y nos lo notifique.</span><span class="sxs-lookup"><span data-stu-id="9ac61-234">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="9ac61-235">Si el proveedor de servicios ha desaprovisionado el circuito (el estado de aprovisionamiento del proveedor de servicios está establecido en **No aprovisionado**), puede eliminar el circuito.</span><span class="sxs-lookup"><span data-stu-id="9ac61-235">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="9ac61-236">Esto detendrá la facturación del circuito.</span><span class="sxs-lookup"><span data-stu-id="9ac61-236">This will stop billing for the circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="9ac61-237">Eliminación de un circuito</span><span class="sxs-lookup"><span data-stu-id="9ac61-237">Delete a circuit</span></span>

<span data-ttu-id="9ac61-238">Puede eliminar el circuito ExpressRout con la ejecución del siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="9ac61-238">You can delete your ExpressRoute circuit by running the following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="9ac61-239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9ac61-239">Next steps</span></span>
<span data-ttu-id="9ac61-240">Después de crear el circuito, asegúrese de hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9ac61-240">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="9ac61-241">Crear y modificar el enrutamiento para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="9ac61-242">Vincular la red virtual a su circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9ac61-242">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

