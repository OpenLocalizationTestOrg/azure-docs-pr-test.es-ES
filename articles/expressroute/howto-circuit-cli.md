---
title: "Creación y modificación de un circuito Azure ExpressRoute: CLI | Microsoft Docs"
description: "Este artículo describe cómo toocreate, aprovisionar, compruebe, actualizar, eliminar y cancelar el aprovisionamiento de un circuito de ExpressRoute con CLI."
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
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="bb7f7-103">Creación y modificación de un circuito ExpressRoute mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="bb7f7-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="bb7f7-104">Este artículo describe cómo toocreate un circuito de ExpressRoute de Azure mediante el uso de Hola interfaz de línea de comandos (CLI).</span><span class="sxs-lookup"><span data-stu-id="bb7f7-104">This article describes how toocreate an Azure ExpressRoute circuit by using hello Command Line Interface (CLI).</span></span> <span data-ttu-id="bb7f7-105">Este artículo también muestra cómo actualizar, estado de hello toocheck, o elimine y cancelar el aprovisionamiento de un circuito.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-105">This article also shows you how toocheck hello status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="bb7f7-106">Si desea toouse una toowork otro método con circuitos ExpressRoute, puede seleccionar artículo Hola de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-106">If you want toouse a different method toowork with ExpressRoute circuits, you can select hello article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb7f7-107">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bb7f7-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="bb7f7-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb7f7-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="bb7f7-109">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="bb7f7-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="bb7f7-110">Vídeo: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bb7f7-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="bb7f7-111">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="bb7f7-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="bb7f7-112">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="bb7f7-112">Before you begin</span></span>

* <span data-ttu-id="bb7f7-113">Antes de comenzar, instalar la versión más reciente de Hola de comandos de CLI de hello (2.0 o posteriores).</span><span class="sxs-lookup"><span data-stu-id="bb7f7-113">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="bb7f7-114">Para obtener información acerca de cómo instalar los comandos de CLI de hello, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli) y [empezar a trabajar con Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bb7f7-114">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="bb7f7-115">Hola de revisión [requisitos previos](expressroute-prerequisites.md) y [flujos de trabajo](expressroute-workflows.md) antes de comenzar la configuración.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-115">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="bb7f7-116">Creación y aprovisionamiento de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bb7f7-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="bb7f7-117">1. Inicie sesión en tooyour cuenta de Azure y seleccione su suscripción</span><span class="sxs-lookup"><span data-stu-id="bb7f7-117">1. Sign in tooyour Azure account and select your subscription</span></span>

<span data-ttu-id="bb7f7-118">toobegin la configuración, el inicio de sesión tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-118">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="bb7f7-119">Usar hello después toohelp ejemplos que conectarse:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-119">Use hello following examples toohelp you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="bb7f7-120">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-120">Check hello subscriptions for hello account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="bb7f7-121">Seleccione la suscripción de hello para el que desea toocreate un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-121">Select hello subscription for which you want toocreate an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="bb7f7-122">2. Obtener lista de Hola de proveedores compatibles, las ubicaciones y anchos de banda</span><span class="sxs-lookup"><span data-stu-id="bb7f7-122">2. Get hello list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="bb7f7-123">Antes de crear un circuito ExpressRoute, necesita Hola lista de proveedores admitidos conectividad, ubicaciones y opciones de ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-123">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="bb7f7-124">Hola CLI comando 'az red express route lista de proveedores de servicios' devuelve esta información, que usará en pasos posteriores:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-124">hello CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="bb7f7-125">respuesta de Hello es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-125">hello response is similar toohello following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="bb7f7-126">Compruebe Hola respuesta toosee si aparece el proveedor de conectividad.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-126">Check hello response toosee if your connectivity provider is listed.</span></span> <span data-ttu-id="bb7f7-127">Tome nota de hello después de obtener información, que tendrá cuando se crea un circuito:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-127">Make a note of hello following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="bb7f7-128">Nombre</span><span class="sxs-lookup"><span data-stu-id="bb7f7-128">Name</span></span>
* <span data-ttu-id="bb7f7-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="bb7f7-129">PeeringLocations</span></span>
* <span data-ttu-id="bb7f7-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="bb7f7-130">BandwidthsOffered</span></span>

<span data-ttu-id="bb7f7-131">Ahora está listo toocreate un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-131">You're now ready toocreate an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="bb7f7-132">3. Creación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bb7f7-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb7f7-133">El circuito de ExpressRoute se factura desde el momento de Hola que se emite una clave de servicio.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-133">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="bb7f7-134">Realizar esta operación cuando proveedor de conectividad de hello circuito de hello tooprovision listo.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-134">Perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="bb7f7-135">Si todavía no tiene un grupo de recursos, debe crear uno antes de crear ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="bb7f7-136">Puede crear un grupo de recursos mediante la ejecución de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-136">You can create a resource group by running hello following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="bb7f7-137">Hola de ejemplo siguiente muestra cómo el circuito toocreate una ExpressRoute de 200 Mbps a través de Equinix en Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-137">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="bb7f7-138">Si usa otro proveedor y otra configuración, sustituya esa información al realizar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="bb7f7-139">Asegúrese de que se especifique nivel correcto de la SKU de Hola y familia de SKU:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-139">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="bb7f7-140">El nivel de SKU determina si está habilitado un complemento estándar o premium de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="bb7f7-141">Puede especificar 'Estándar' hello tooget SKU estándar o 'Premium' para el complemento de hello premium.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-141">You can specify 'Standard' tooget hello standard SKU or 'Premium' for hello premium add-on.</span></span>
* <span data-ttu-id="bb7f7-142">Familia de SKU determina el tipo de facturación de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-142">SKU family determines hello billing type.</span></span> <span data-ttu-id="bb7f7-143">Puede seleccionar "Metereddata" para el plan de datos limitado y "Unlimiteddata" para el plan de datos ilimitado.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="bb7f7-144">Puede cambiar el tipo de facturación de Hola de ' Metereddata 'too'Unlimiteddata', pero no puede cambiar tipo hello de 'Unlimiteddata' too'Metereddata'.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-144">You can change hello billing type from 'Metereddata' too'Unlimiteddata', but you can't change hello type from 'Unlimiteddata' too'Metereddata'.</span></span>


<span data-ttu-id="bb7f7-145">El circuito de ExpressRoute se factura desde el momento de Hola que se emite una clave de servicio.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-145">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="bb7f7-146">Hola siguiente ejemplo es una solicitud de una nueva clave de servicio:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-146">hello following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="bb7f7-147">respuesta de Hello contiene la clave de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-147">hello response contains hello service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="bb7f7-148">4. Lista de todos los circuitos ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bb7f7-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="bb7f7-149">tooget una lista de todos los circuitos ExpressRoute de Hola que ha creado, ejecute 'hello az red express route mostrar' (comando).</span><span class="sxs-lookup"><span data-stu-id="bb7f7-149">tooget a list of all hello ExpressRoute circuits that you created, run hello 'az network express-route list' command.</span></span> <span data-ttu-id="bb7f7-150">Puede recuperar esta información en cualquier momento con este comando.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="bb7f7-151">toolist todos los circuitos, realizar Hola llamada sin parámetros.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-151">toolist all circuits, make hello call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="bb7f7-152">La clave del servicio aparece en hello *ServiceKey* campo de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-152">Your service key is listed in hello *ServiceKey* field of hello response.</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="bb7f7-153">Puede obtener una descripción detallada de todos los parámetros de hello ejecutando el comando hello mediante hello '-h' parámetro.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-153">You can get detailed descriptions of all hello parameters by running hello command using hello '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="bb7f7-154">5. Enviar el proveedor de conectividad de tooyour clave de servicio de hello para el aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="bb7f7-154">5. Send hello service key tooyour connectivity provider for provisioning</span></span>

<span data-ttu-id="bb7f7-155">'ServiceProviderProvisioningState' proporciona información sobre el estado actual de Hola de aprovisionamiento en el lado del proveedor de servicios de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-155">'ServiceProviderProvisioningState' provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="bb7f7-156">estado de Hello proporciona estado hello en hello side de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-156">hello status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="bb7f7-157">Para obtener más información, vea hello [artículo de flujos de trabajo](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="bb7f7-157">For more information, see hello [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="bb7f7-158">Cuando se crea un nuevo circuito de ExpressRoute, circuito hello es Hola siguiente estado:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-158">When you create a new ExpressRoute circuit, hello circuit is in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="bb7f7-159">Hola circuito cambios toohello siguiente estado cuando el proveedor de conectividad de hello está en proceso de Hola de habilitarla para:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-159">hello circuit changes toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="bb7f7-160">Para toobe pueda toouse un circuito ExpressRoute, debe estar en hello siguiente estado:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-160">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="bb7f7-161">6. Comprobar periódicamente el estado de Hola y el estado de Hola de clave de circuito de Hola</span><span class="sxs-lookup"><span data-stu-id="bb7f7-161">6. Periodically check hello status and hello state of hello circuit key</span></span>

<span data-ttu-id="bb7f7-162">Comprobación de estado de Hola y el estado de Hola de clave de circuito de hello le permite saber si el proveedor ha habilitado el circuito.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-162">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="bb7f7-163">Una vez configurado el circuito de hello, 'ServiceProviderProvisioningState' aparece como "Aprovisionado", como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-163">After hello circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in hello following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="bb7f7-164">respuesta de Hello es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-164">hello response is similar toohello following example:</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="bb7f7-165">7. Creación de la configuración de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="bb7f7-165">7. Create your routing configuration</span></span>

<span data-ttu-id="bb7f7-166">Para obtener instrucciones detalladas, consulte hello [circuito de ExpressRoute de configuración de enrutamiento](howto-routing-cli.md) artículo toocreate y modificar los emparejamientos de circuito.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-166">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](howto-routing-cli.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb7f7-167">Estas instrucciones aplican solo toocircuits que se crean con proveedores de servicios que ofrecen servicios de conectividad de 2 niveles.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-167">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="bb7f7-168">Si usa un proveedor de servicios que ofrece servicios administrados de nivel 3 (normalmente VPN IP, como MPLS), el mismo proveedor de conectividad configura y administra el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="bb7f7-169">8. Vincular un circuito de ExpressRoute de tooan de red virtual</span><span class="sxs-lookup"><span data-stu-id="bb7f7-169">8. Link a virtual network tooan ExpressRoute circuit</span></span>

<span data-ttu-id="bb7f7-170">A continuación, vincular un circuito de ExpressRoute de tooyour de red virtual.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-170">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="bb7f7-171">Hola de uso [vinculación virtual redes tooExpressRoute circuitos](howto-linkvnet-cli.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-171">Use hello [Linking virtual networks tooExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="bb7f7-172"><a name="modify"></a>Modificación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bb7f7-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="bb7f7-173">Puede modificar determinadas propiedades de un circuito ExpressRoute sin afectar a la conectividad.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="bb7f7-174">Puede realizar Hola después cambios sin tiempo de inactividad:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-174">You can make hello following changes with no downtime:</span></span>

* <span data-ttu-id="bb7f7-175">Puede habilitar o deshabilitar el complemento ExpressRoute Premium en su circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="bb7f7-176">Puede aumentar el ancho de banda de Hola del circuito de ExpressRoute siempre hay capacidad disponible en el puerto de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-176">You can increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="bb7f7-177">Sin embargo, no se admite la degradación de ancho de banda de Hola de un circuito.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-177">However, downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="bb7f7-178">Puede cambiar el plan de disponibilidad de Hola de tooUnlimited datos limitados de datos.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-178">You can change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="bb7f7-179">Sin embargo, cambiar Hola plan desde tooMetered ilimitados datos que no se admiten datos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-179">However, changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="bb7f7-180">Puede habilitar y deshabilitar *Allow Classic Operations*(Permitir operaciones clásicas).</span><span class="sxs-lookup"><span data-stu-id="bb7f7-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="bb7f7-181">Para obtener más información sobre los límites y limitaciones, vea hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="bb7f7-181">For more information on limits and limitations, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="bb7f7-182">complemento de tooenable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="bb7f7-182">tooenable hello ExpressRoute premium add-on</span></span>

<span data-ttu-id="bb7f7-183">Puede habilitar complemento de hello ExpressRoute premium para el circuito existente mediante Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-183">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="bb7f7-184">circuito de Hello tiene ahora hello ExpressRoute complemento las características premium habilitadas.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-184">hello circuit now has hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="bb7f7-185">Empezaremos facturación para la capacidad de complemento de hello premium tan pronto como comando de Hola se ha ejecutado correctamente.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-185">We begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="bb7f7-186">complemento de toodisable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="bb7f7-186">toodisable hello ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb7f7-187">Esta operación puede producir un error si usa recursos que son mayores que lo que está permitido para el circuito de hello estándar.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-187">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="bb7f7-188">Antes de deshabilitar el complemento de hello ExpressRoute premium, comprender Hola siguiendo criterios:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-188">Before disabling hello ExpressRoute premium add-on, understand hello following criteria:</span></span>

* <span data-ttu-id="bb7f7-189">Antes de degradar de toostandard premium, debe asegurarse de que dispone de menos de 10 redes virtuales vinculadas toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-189">Before you downgrade from premium toostandard, you must make sure that you have fewer than 10 virtual networks linked toohello circuit.</span></span> <span data-ttu-id="bb7f7-190">Si tiene más de diez, se produce una solicitud de actualización y se le factura con las tarifas de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="bb7f7-191">Tiene que desvincular todas las redes virtuales en otras regiones geopolíticas.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="bb7f7-192">Si no lo hace, se produce un error en la solicitud de actualización y se le factura con las tarifas de nivel Premium.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="bb7f7-193">La tabla de enrutamiento tiene que tener menos de 4.000 rutas para el emparejamiento entre pares privados.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="bb7f7-194">Si el tamaño de la tabla de ruta es mayor que 4000 rutas, quita la sesión BGP Hola.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-194">If your route table size is greater than 4,000 routes, hello BGP session drops.</span></span> <span data-ttu-id="bb7f7-195">No volver a habilitar la sesión de Hello hasta que el número de Hola de los prefijos anunciados es inferior a 4.000.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-195">hello session won't be reenabled until hello number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="bb7f7-196">Puede deshabilitar el complemento de premium de ExpressRoute de hello para el circuito de hello existente utilizando el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-196">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="bb7f7-197">ancho de banda de circuito de ExpressRoute de tooupdate Hola</span><span class="sxs-lookup"><span data-stu-id="bb7f7-197">tooupdate hello ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="bb7f7-198">Para hello admitida opciones de ancho de banda para el proveedor, consulte hello [preguntas más frecuentes de ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="bb7f7-198">For hello supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="bb7f7-199">Puede elegir cualquier tamaño mayor que el tamaño de Hola de su circuito existente.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-199">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb7f7-200">Si no hay capacidad inadecuada en el puerto existente de hello, habrá circuito de ExpressRoute de toorecreate Hola.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-200">If there is inadequate capacity on hello existing port, you may have toorecreate hello ExpressRoute circuit.</span></span> <span data-ttu-id="bb7f7-201">No puede actualizar el circuito de hello si no hay ninguna capacidad adicional disponible en esa ubicación.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-201">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="bb7f7-202">No se puede reducir el ancho de banda de Hola de un circuito de ExpressRoute sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-202">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="bb7f7-203">Degradar de ancho de banda requiere toodeprovision Hola circuito ExpressRoute y, a continuación, vuelva a aprovisionar un nuevo circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-203">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="bb7f7-204">Una vez decidido el tamaño de Hola que sea necesario, utilice Hola después comando tooresize el circuito:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-204">After you decide hello size you need, use hello following command tooresize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="bb7f7-205">El circuito tiene un tamaño lado de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-205">Your circuit is sized up on hello Microsoft side.</span></span> <span data-ttu-id="bb7f7-206">A continuación, debe ponerse en contacto con las configuraciones de tooupdate de proveedor de conectividad en su lado toomatch este cambio.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-206">Next, you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="bb7f7-207">Después de realizar esta notificación, empezaremos facturación para la opción de ancho de banda de hello actualizado.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-207">After you make this notification, we begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="bb7f7-208">Hola toomove SKU de uso medido toounlimited</span><span class="sxs-lookup"><span data-stu-id="bb7f7-208">toomove hello SKU from metered toounlimited</span></span>

<span data-ttu-id="bb7f7-209">Puede cambiar Hola SKU de un circuito ExpressRoute mediante el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-209">You can change hello SKU of an ExpressRoute circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="bb7f7-210">clásico de toocontrol acceso toohello y entornos de administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="bb7f7-210">toocontrol access toohello classic and Resource Manager environments</span></span>

<span data-ttu-id="bb7f7-211">Revisar las instrucciones de Hola de [circuitos ExpressRoute mover de modelo de implementación de administrador de recursos de hello toohello clásico](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="bb7f7-211">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="bb7f7-212">Desaprovisionamiento y eliminación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bb7f7-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="bb7f7-213">toodeprovision y eliminar un circuito ExpressRoute, asegúrese de comprender Hola siguiendo criterios:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-213">toodeprovision and delete an ExpressRoute circuit, make sure you understand hello following criteria:</span></span>

* <span data-ttu-id="bb7f7-214">Debe desvincular todas las redes virtuales de hello circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-214">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="bb7f7-215">Si se produce un error en esta operación, compruebe toosee si las redes virtuales están vinculados toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-215">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="bb7f7-216">Si es el proveedor de servicios del circuito de ExpressRoute de hello estado de aprovisionamiento **Provisioning** o **aprovisionado**, debe trabajar con el circuito de Hola de toodeprovision de proveedor de servicio en uno de su lados.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-216">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="bb7f7-217">Hemos continuar tooreserve recursos y facturar hasta que el proveedor de servicios de hello finaliza desaprovisionamiento circuito de Hola y notifica a nosotros.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-217">We continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="bb7f7-218">Puede eliminar el circuito de hello si el proveedor de servicios de Hola se canceló el aprovisionamiento de circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-218">You can delete hello circuit if hello service provider has deprovisioned hello circuit.</span></span> <span data-ttu-id="bb7f7-219">Cuando se desaprovisiona un circuito, estado de aprovisionamiento de proveedor de servicios de Hola se establece demasiado**no aprovisionado**.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-219">When a circuit is deprovisioned, hello service provider provisioning state is set too**Not provisioned**.</span></span> <span data-ttu-id="bb7f7-220">Esto deja de facturación para el circuito de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb7f7-220">This stops billing for hello circuit.</span></span>

<span data-ttu-id="bb7f7-221">Puede eliminar el circuito de ExpressRoute ejecutando Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-221">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="bb7f7-222">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb7f7-222">Next steps</span></span>

<span data-ttu-id="bb7f7-223">Después de crear el circuito, asegúrese de que hello las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="bb7f7-223">After you create your circuit, make sure that you do hello following tasks:</span></span>

* [<span data-ttu-id="bb7f7-224">Crear y modificar el enrutamiento para el circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="bb7f7-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="bb7f7-225">Vincular el circuito de ExpressRoute de tooyour de red virtual</span><span class="sxs-lookup"><span data-stu-id="bb7f7-225">Link your virtual network tooyour ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)
