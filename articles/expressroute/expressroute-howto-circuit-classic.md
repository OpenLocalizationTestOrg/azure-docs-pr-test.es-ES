---
title: "Creación y modificación de un circuito ExpressRoute mediante Powershell y Azure clásico | Microsoft Docs"
description: "En este artículo le guiará por los pasos de Hola para crear y aprovisionar un circuito ExpressRoute. Este artículo también muestra cómo actualizar, estado de hello toocheck, o eliminar y desaprovisionar el circuito."
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
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="306d2-104">Creación y modificación de un circuito ExpressRoute mediante PowerShell (clásica)</span><span class="sxs-lookup"><span data-stu-id="306d2-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="306d2-105">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="306d2-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="306d2-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="306d2-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="306d2-107">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="306d2-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="306d2-108">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="306d2-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="306d2-109">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="306d2-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="306d2-110">Este artículo le guiará a través de hello pasos toocreate un circuito ExpressRoute de Azure utilizando el modelo de implementación clásica de hello y cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="306d2-110">This article walks you through hello steps toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello classic deployment model.</span></span> <span data-ttu-id="306d2-111">Este artículo también muestra cómo actualizar, toocheck estado de hello, o eliminar y cancelar el aprovisionamiento de un circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="306d2-111">This article also shows you how toocheck hello status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="306d2-112">**Información sobre los modelos de implementación de Azure**</span><span class="sxs-lookup"><span data-stu-id="306d2-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="306d2-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="306d2-113">Before you begin</span></span>
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a><span data-ttu-id="306d2-114">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="306d2-114">Step 1.</span></span> <span data-ttu-id="306d2-115">Revisar los requisitos previos de Hola y artículos de flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="306d2-115">Review hello prerequisites and workflow articles</span></span>
<span data-ttu-id="306d2-116">Asegúrese de que ha revisado hello [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="306d2-116">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="306d2-117">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="306d2-117">Step 2.</span></span> <span data-ttu-id="306d2-118">Instalar versiones más recientes de Hola de módulos de administración de servicio de Azure (SM) PowerShell Hola</span><span class="sxs-lookup"><span data-stu-id="306d2-118">Install hello latest versions of hello Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="306d2-119">Siga las instrucciones de hello en [Introducción a cmdlets de PowerShell de Azure](/powershell/azure/overview) para obtener instrucciones paso a paso acerca de cómo tooconfigure los módulos de PowerShell de Azure de equipo toouse Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-119">Follow hello instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="306d2-120">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="306d2-120">Step 3.</span></span> <span data-ttu-id="306d2-121">Inicie sesión en tooyour cuenta de Azure y seleccione una suscripción</span><span class="sxs-lookup"><span data-stu-id="306d2-121">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="306d2-122">Abra la consola de PowerShell con derechos elevados y conectar con tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="306d2-122">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="306d2-123">Usar hello después toohelp de ejemplo que se conecta:</span><span class="sxs-lookup"><span data-stu-id="306d2-123">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="306d2-124">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="306d2-124">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="306d2-125">Si tiene más de una suscripción, seleccione Hola suscripción que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="306d2-125">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="306d2-126">A continuación, usar hello siguiente cmdlet tooadd su tooPowerShell de suscripción de Azure para el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-126">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="306d2-127">Creación y aprovisionamiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="306d2-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a><span data-ttu-id="306d2-128">Paso 1.</span><span class="sxs-lookup"><span data-stu-id="306d2-128">Step 1.</span></span> <span data-ttu-id="306d2-129">Importar módulos de PowerShell de Hola para ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="306d2-129">Import hello PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="306d2-130">Si no lo ha hecho ya, debe importar los módulos de Azure y ExpressRoute de hello en la sesión de PowerShell de hello en toostart orden mediante cmdlets de ExpressRoute Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-130">If you have not already done so, you must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="306d2-131">Importar módulos de Hola de hello ubicación que se encontraban instalado tooon el equipo local.</span><span class="sxs-lookup"><span data-stu-id="306d2-131">You import hello modules from hello location that they were installed tooon your local computer.</span></span> <span data-ttu-id="306d2-132">Según el método hello usa módulos de hello tooinstall, ubicación de hello puede ser diferente de hello siguiente ejemplo se muestra.</span><span class="sxs-lookup"><span data-stu-id="306d2-132">Depending on hello method you used tooinstall hello modules, hello location may be different than hello following example shows.</span></span> <span data-ttu-id="306d2-133">Modificar el ejemplo de Hola si es necesario.</span><span class="sxs-lookup"><span data-stu-id="306d2-133">Modify hello example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="306d2-134">Paso 2:</span><span class="sxs-lookup"><span data-stu-id="306d2-134">Step 2.</span></span> <span data-ttu-id="306d2-135">Obtener lista de Hola de proveedores compatibles, las ubicaciones y anchos de banda</span><span class="sxs-lookup"><span data-stu-id="306d2-135">Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="306d2-136">Antes de crear un circuito ExpressRoute, necesita Hola lista de proveedores admitidos conectividad, ubicaciones y opciones de ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="306d2-136">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="306d2-137">Hola cmdlet de PowerShell `Get-AzureDedicatedCircuitServiceProvider` devuelve esta información, que usará en pasos posteriores:</span><span class="sxs-lookup"><span data-stu-id="306d2-137">hello PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="306d2-138">Compruebe toosee si aparece el proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="306d2-138">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="306d2-139">Tome nota de hello siguiente información porque lo necesitará más adelante cuando se crea un circuito:</span><span class="sxs-lookup"><span data-stu-id="306d2-139">Make a note of hello following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="306d2-140">Nombre</span><span class="sxs-lookup"><span data-stu-id="306d2-140">Name</span></span>
* <span data-ttu-id="306d2-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="306d2-141">PeeringLocations</span></span>
* <span data-ttu-id="306d2-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="306d2-142">BandwidthsOffered</span></span>

<span data-ttu-id="306d2-143">Ahora está listo toocreate un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="306d2-143">You're now ready toocreate an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="306d2-144">Paso 3:</span><span class="sxs-lookup"><span data-stu-id="306d2-144">Step 3.</span></span> <span data-ttu-id="306d2-145">Creación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="306d2-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="306d2-146">Hola de ejemplo siguiente muestra cómo el circuito toocreate una ExpressRoute de 200 Mbps a través de Equinix en Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="306d2-146">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="306d2-147">Si usa otro proveedor y otra configuración, sustituya esa información al realizar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="306d2-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="306d2-148">El circuito de ExpressRoute se cobrará desde el momento de Hola que se emite una clave de servicio.</span><span class="sxs-lookup"><span data-stu-id="306d2-148">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="306d2-149">Asegúrese de que lleva a cabo esta operación cuando proveedor de conectividad de hello circuito de hello tooprovision listo.</span><span class="sxs-lookup"><span data-stu-id="306d2-149">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="306d2-150">Hola te mostramos una solicitud de ejemplo para una nueva clave de servicio:</span><span class="sxs-lookup"><span data-stu-id="306d2-150">hello following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="306d2-151">O bien, si desea que toocreate un circuito de ExpressRoute con el complemento de hello premium, use Hola siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="306d2-151">Or, if you want toocreate an ExpressRoute circuit with hello premium add-on, use hello following example.</span></span> <span data-ttu-id="306d2-152">Consulte toohello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) para obtener más información sobre el complemento de hello premium.</span><span class="sxs-lookup"><span data-stu-id="306d2-152">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more details about hello premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="306d2-153">respuesta de Hello contendrá la clave de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-153">hello response will contain hello service key.</span></span> <span data-ttu-id="306d2-154">Puede obtener una descripción detallada de todos los parámetros de hello ejecutando Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="306d2-154">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a><span data-ttu-id="306d2-155">Paso 4</span><span class="sxs-lookup"><span data-stu-id="306d2-155">Step 4.</span></span> <span data-ttu-id="306d2-156">Lista de todos los circuitos ExpressRoute de Hola</span><span class="sxs-lookup"><span data-stu-id="306d2-156">List all hello ExpressRoute circuits</span></span>
<span data-ttu-id="306d2-157">Puede ejecutar hello `Get-AzureDedicatedCircuit` comando Hola de tooget una lista de todos los circuitos ExpressRoute que ha creado:</span><span class="sxs-lookup"><span data-stu-id="306d2-157">You can run hello `Get-AzureDedicatedCircuit` command tooget a list of all hello ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="306d2-158">respuesta de Hello será algo similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="306d2-158">hello response will be something similar toohello following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="306d2-159">Puede recuperar esta información en cualquier momento mediante hello `Get-AzureDedicatedCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="306d2-159">You can retrieve this information at any time by using hello `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="306d2-160">Realizar Hola llamada sin ningún parámetro, enumera todos los circuitos de Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-160">Making hello call without any parameters lists all hello circuits.</span></span> <span data-ttu-id="306d2-161">La clave del servicio se enumerarán en hello *ServiceKey* campo.</span><span class="sxs-lookup"><span data-stu-id="306d2-161">Your service key will be listed in hello *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="306d2-162">Puede obtener una descripción detallada de todos los parámetros de hello ejecutando Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="306d2-162">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="306d2-163">Paso 5.</span><span class="sxs-lookup"><span data-stu-id="306d2-163">Step 5.</span></span> <span data-ttu-id="306d2-164">Enviar el proveedor de conectividad de tooyour clave de servicio de hello para el aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="306d2-164">Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="306d2-165">*ServiceProviderProvisioningState* proporciona información sobre el estado actual de Hola de aprovisionamiento en el lado del proveedor de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-165">*ServiceProviderProvisioningState* provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="306d2-166">*Estado* proporciona el estado de hello en hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="306d2-166">*Status* provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="306d2-167">Para obtener más información acerca de los Estados de aprovisionamiento del circuito, vea hello [flujos de trabajo](expressroute-workflows.md#expressroute-circuit-provisioning-states) artículo.</span><span class="sxs-lookup"><span data-stu-id="306d2-167">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="306d2-168">Cuando se crea un nuevo circuito de ExpressRoute, circuito Hola estará en hello siguiente estado:</span><span class="sxs-lookup"><span data-stu-id="306d2-168">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="306d2-169">circuito Hola irá toohello siguiente estado cuando el proveedor de conectividad de hello está en proceso de Hola de habilitarla para:</span><span class="sxs-lookup"><span data-stu-id="306d2-169">hello circuit will go toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="306d2-170">Un circuito ExpressRoute debe estar en hello después de estado para toobe pueda toouse lo:</span><span class="sxs-lookup"><span data-stu-id="306d2-170">An ExpressRoute circuit must be in hello following state for you toobe able toouse it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="306d2-171">Paso 6.</span><span class="sxs-lookup"><span data-stu-id="306d2-171">Step 6.</span></span> <span data-ttu-id="306d2-172">Comprobar periódicamente el estado de Hola y el estado de Hola de clave de circuito de Hola</span><span class="sxs-lookup"><span data-stu-id="306d2-172">Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="306d2-173">Esto le permitirá saber cuándo ha habilitado el circuito el proveedor.</span><span class="sxs-lookup"><span data-stu-id="306d2-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="306d2-174">Una vez configurado el circuito de hello, *ServiceProviderProvisioningState* se mostrará como *aprovisionado* tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="306d2-174">After hello circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in hello following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="306d2-175">Paso 7.</span><span class="sxs-lookup"><span data-stu-id="306d2-175">Step 7.</span></span> <span data-ttu-id="306d2-176">Creación de la configuración de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="306d2-176">Create your routing configuration</span></span>
<span data-ttu-id="306d2-177">Consulte toohello [circuito de ExpressRoute de configuración de enrutamiento (crear y modificar los emparejamientos de circuito)](expressroute-howto-routing-classic.md) artículo para obtener instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="306d2-177">Refer toohello [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="306d2-178">Estas instrucciones aplican solo toocircuits que se crean con proveedores de servicios que ofrecen servicios de conectividad de 2 niveles.</span><span class="sxs-lookup"><span data-stu-id="306d2-178">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="306d2-179">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configurará y administrará el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="306d2-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="306d2-180">Paso 8.</span><span class="sxs-lookup"><span data-stu-id="306d2-180">Step 8.</span></span> <span data-ttu-id="306d2-181">Vincular un circuito de ExpressRoute de tooan de red virtual</span><span class="sxs-lookup"><span data-stu-id="306d2-181">Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="306d2-182">A continuación, vincular un circuito de ExpressRoute de tooyour de red virtual.</span><span class="sxs-lookup"><span data-stu-id="306d2-182">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="306d2-183">Consulte demasiado[ExpressRoute vinculación circuitos toovirtual redes](expressroute-howto-linkvnet-classic.md) para obtener instrucciones paso a paso.</span><span class="sxs-lookup"><span data-stu-id="306d2-183">Refer too[Linking ExpressRoute circuits toovirtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="306d2-184">Si necesita una red virtual con el modelo de implementación clásica de Hola para ExpressRoute toocreate, consulte [crear una red virtual para ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="306d2-184">If you need toocreate a virtual network using hello classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="306d2-185">Obtener el estado de saludo de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="306d2-185">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="306d2-186">Puede recuperar esta información en cualquier momento mediante hello `Get-AzureCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="306d2-186">You can retrieve this information at any time by using hello `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="306d2-187">Realizar Hola llamada sin ningún parámetro, enumera todos los circuitos de Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-187">Making hello call without any parameters lists all hello circuits.</span></span>

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

<span data-ttu-id="306d2-188">Puede obtener información sobre un circuito de ExpressRoute concreto pasando la clave de servicio de hello como una llamada a toohello de parámetro.</span><span class="sxs-lookup"><span data-stu-id="306d2-188">You can get information on a specific ExpressRoute circuit by passing hello service key as a parameter toohello call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="306d2-189">Puede obtener una descripción detallada de todos los parámetros de hello ejecutando el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="306d2-189">You can get detailed descriptions of all hello parameters by running hello following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="306d2-190">Modificación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="306d2-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="306d2-191">Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad.</span><span class="sxs-lookup"><span data-stu-id="306d2-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="306d2-192">Puede hacer Hola sigue sin tiempo de inactividad:</span><span class="sxs-lookup"><span data-stu-id="306d2-192">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="306d2-193">Habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="306d2-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="306d2-194">Ancho de banda de Hola de aumento de su circuito de ExpressRoute proporciona hay capacidad disponible en el puerto de Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-194">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="306d2-195">Tenga en cuenta que no se admite la degradación de ancho de banda de Hola de un circuito.</span><span class="sxs-lookup"><span data-stu-id="306d2-195">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="306d2-196">Cambiar Hola plan desde tooUnlimited datos limitados de datos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="306d2-196">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="306d2-197">Tenga en cuenta ese plan de disponibilidad de hello cambiante de tooMetered datos ilimitados que datos no se admiten.</span><span class="sxs-lookup"><span data-stu-id="306d2-197">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="306d2-198">Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).</span><span class="sxs-lookup"><span data-stu-id="306d2-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="306d2-199">Consulte toohello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) para obtener más información sobre los límites y limitaciones.</span><span class="sxs-lookup"><span data-stu-id="306d2-199">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="306d2-200">complemento de tooenable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="306d2-200">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="306d2-201">Puede habilitar complemento de hello ExpressRoute premium para el circuito existente mediante Hola siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="306d2-201">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="306d2-202">El circuito tendrán ahora hello ExpressRoute complemento las características premium habilitadas.</span><span class="sxs-lookup"><span data-stu-id="306d2-202">Your circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="306d2-203">Tenga en cuenta que se iniciará de facturación para la capacidad de complemento de hello premium tan pronto como comando de Hola se ha ejecutado correctamente.</span><span class="sxs-lookup"><span data-stu-id="306d2-203">Note that we will start billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="306d2-204">complemento de toodisable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="306d2-204">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="306d2-205">Esta operación puede producir un error si usa recursos que son mayores que lo que está permitido para el circuito de hello estándar.</span><span class="sxs-lookup"><span data-stu-id="306d2-205">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="306d2-206">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="306d2-206">Considerations</span></span>

* <span data-ttu-id="306d2-207">Debe asegurarse de que el número de Hola de redes virtuales vinculadas toohello circuito es menor que 10 antes de cambiar de premium toostandard.</span><span class="sxs-lookup"><span data-stu-id="306d2-207">You must ensure that hello number of virtual networks linked toohello circuit is less than 10 before you downgrade from premium toostandard.</span></span> <span data-ttu-id="306d2-208">Si no lo hace, se producirá un error en la solicitud de actualización y le tarifas de facturación Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-208">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="306d2-209">Tiene que desvincular todas las redes virtuales en otras regiones geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="306d2-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="306d2-210">Si no lo hace, se producirá un error en la solicitud de actualización y le tarifas de facturación Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-210">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="306d2-211">La tabla de enrutamiento tiene que tener menos de 4.000 rutas para el emparejamiento entre pares privados.</span><span class="sxs-lookup"><span data-stu-id="306d2-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="306d2-212">Si el tamaño de la tabla de ruta es mayor que 4000 rutas, sesión BGP Hola se quitará y no volver a habilitar hasta que el número de Hola de los prefijos anunciados esté por debajo de 4.000.</span><span class="sxs-lookup"><span data-stu-id="306d2-212">If your route table size is greater than 4,000 routes, hello BGP session will drop and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-hello-premium-add-on"></a><span data-ttu-id="306d2-213">Deshabilitar complemento de hello premium</span><span class="sxs-lookup"><span data-stu-id="306d2-213">Disable hello premium add-on</span></span>
<span data-ttu-id="306d2-214">Puede deshabilitar complemento de hello ExpressRoute premium para el circuito existente mediante el uso de hello siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="306d2-214">You can disable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="306d2-215">ancho de banda de circuito de ExpressRoute de tooupdate Hola</span><span class="sxs-lookup"><span data-stu-id="306d2-215">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="306d2-216">Comprobar hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md) para admite opciones de ancho de banda para el proveedor.</span><span class="sxs-lookup"><span data-stu-id="306d2-216">Check hello [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="306d2-217">Puede elegir cualquier tamaño que es mayor que el tamaño de Hola de su circuito existente como Hola puerto físico (en el que se creó el circuito) permite.</span><span class="sxs-lookup"><span data-stu-id="306d2-217">You can pick any size that is greater than hello size of your existing circuit as long as hello physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="306d2-218">Puede tener circuito de ExpressRoute de hello toorecreate si hay capacidad inadecuada en el puerto existente Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-218">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="306d2-219">No puede actualizar el circuito de hello si no hay ninguna capacidad adicional disponible en esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="306d2-219">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="306d2-220">No se puede reducir el ancho de banda de Hola de un circuito de ExpressRoute sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="306d2-220">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="306d2-221">Degradar de ancho de banda requiere circuito de ExpressRoute de toodeprovision hello y, a continuación, vuelva a aprovisionar un nuevo circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="306d2-221">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="306d2-222">Cambio del tamaño de un circuito</span><span class="sxs-lookup"><span data-stu-id="306d2-222">Resize a circuit</span></span>

<span data-ttu-id="306d2-223">Después de decidir qué tamaño que sea necesario, puede usar Hola después comando tooresize el circuito:</span><span class="sxs-lookup"><span data-stu-id="306d2-223">After you decide what size you need, you can use hello following command tooresize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="306d2-224">El circuito ha habrá tamaño en lado de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-224">Your circuit will have been sized up on hello Microsoft side.</span></span> <span data-ttu-id="306d2-225">Debe ponerse en contacto con las configuraciones de tooupdate de proveedor de conectividad en su lado toomatch este cambio.</span><span class="sxs-lookup"><span data-stu-id="306d2-225">You must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="306d2-226">Tenga en cuenta que se iniciará factura para hello actualiza la opción de ancho de banda desde este punto en.</span><span class="sxs-lookup"><span data-stu-id="306d2-226">Note that we will start billing you for hello updated bandwidth option from this point on.</span></span>

<span data-ttu-id="306d2-227">Si ve Hola tras error al aumentar el ancho de banda de circuito de hello, significa que no hay queda no hay suficiente ancho de banda en el puerto físico Hola donde se crea el circuito existente.</span><span class="sxs-lookup"><span data-stu-id="306d2-227">If you see hello following error when increasing hello circuit bandwidth, it means there is no sufficient bandwidth left on hello physical port where your existing circuit is created.</span></span> <span data-ttu-id="306d2-228">Toodelete este circuito y cree un nuevo circuito de tamaño Hola que sea necesario.</span><span class="sxs-lookup"><span data-stu-id="306d2-228">You have toodelete this circuit and create a new circuit of hello size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="306d2-229">Desaprovisionamiento y eliminación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="306d2-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="306d2-230">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="306d2-230">Considerations</span></span>

* <span data-ttu-id="306d2-231">Debe desvincular todas las redes virtuales de hello circuito de ExpressRoute para esta operación toosucceed.</span><span class="sxs-lookup"><span data-stu-id="306d2-231">You must unlink all virtual networks from hello ExpressRoute circuit for this operation toosucceed.</span></span> <span data-ttu-id="306d2-232">Comprobar toosee si dispone de las redes virtuales que están vinculados toohello circuito si se produce un error en esta operación.</span><span class="sxs-lookup"><span data-stu-id="306d2-232">Check toosee if you have any virtual networks that are linked toohello circuit if this operation fails.</span></span>
* <span data-ttu-id="306d2-233">Si es el proveedor de servicios del circuito de ExpressRoute de hello estado de aprovisionamiento **Provisioning** o **aprovisionado** debe trabajar con el circuito de Hola de toodeprovision de proveedor de servicio en uno de su lados.</span><span class="sxs-lookup"><span data-stu-id="306d2-233">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="306d2-234">Se continuará tooreserve recursos y facturar hasta que el proveedor de servicios de hello finaliza desaprovisionamiento circuito de Hola y notifica a nosotros.</span><span class="sxs-lookup"><span data-stu-id="306d2-234">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="306d2-235">Si el proveedor de servicios de Hola se canceló el aprovisionamiento de circuito de hello (proveedor de servicios de hello estado de aprovisionamiento se establece demasiado**no aprovisionado**), a continuación, puede eliminar el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-235">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="306d2-236">Esto detendrá la facturación para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="306d2-236">This will stop billing for hello circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="306d2-237">Eliminación de un circuito</span><span class="sxs-lookup"><span data-stu-id="306d2-237">Delete a circuit</span></span>

<span data-ttu-id="306d2-238">Puede eliminar el circuito de ExpressRoute ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="306d2-238">You can delete your ExpressRoute circuit by running hello following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="306d2-239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="306d2-239">Next steps</span></span>
<span data-ttu-id="306d2-240">Después de crear el circuito, asegúrese de que Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="306d2-240">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="306d2-241">Crear y modificar el enrutamiento para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="306d2-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="306d2-242">Vincular el circuito de ExpressRoute de tooyour de red virtual</span><span class="sxs-lookup"><span data-stu-id="306d2-242">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

