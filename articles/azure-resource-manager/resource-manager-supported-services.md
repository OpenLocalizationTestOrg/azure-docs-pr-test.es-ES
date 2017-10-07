---
title: aaaAzure proveedores de recursos y tipos de recursos | Documentos de Microsoft
description: Describe los proveedores de recursos de Hola que admiten el Administrador de recursos, sus esquemas y las versiones disponibles de API y regiones de Hola que pueden contener recursos de Hola.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="8743f-103">Tipos y proveedores de recursos</span><span class="sxs-lookup"><span data-stu-id="8743f-103">Resource providers and types</span></span>

<span data-ttu-id="8743f-104">Al implementar los recursos, con frecuencia necesitan tooretrieve información acerca de proveedores de recursos de Hola y tipos.</span><span class="sxs-lookup"><span data-stu-id="8743f-104">When deploying resources, you frequently need tooretrieve information about hello resource providers and types.</span></span> <span data-ttu-id="8743f-105">En este artículo, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="8743f-105">In this article, you learn to:</span></span>

* <span data-ttu-id="8743f-106">Ver todos los proveedores de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="8743f-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="8743f-107">Comprobar el estado de registro de un proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="8743f-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="8743f-108">Registrar un proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="8743f-108">Register a resource provider</span></span>
* <span data-ttu-id="8743f-109">Ver los tipos de recursos de un proveedor</span><span class="sxs-lookup"><span data-stu-id="8743f-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="8743f-110">Ver las ubicaciones válidas de un tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="8743f-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="8743f-111">Ver las versiones de API válidas de un tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="8743f-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="8743f-112">Puede realizar estos pasos a través del portal de hello, PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="8743f-112">You can perform these steps through hello portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="8743f-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8743f-113">PowerShell</span></span>

<span data-ttu-id="8743f-114">toosee todos los proveedores de recursos de Azure y el estado de registro de hello para su suscripción, usan:</span><span class="sxs-lookup"><span data-stu-id="8743f-114">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="8743f-115">Que devuelve resultados similares a:</span><span class="sxs-lookup"><span data-stu-id="8743f-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="8743f-116">Registrar un proveedor de recursos configura el toowork de suscripción con el proveedor de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-116">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="8743f-117">ámbito de Hello para el registro siempre es suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-117">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="8743f-118">De forma predeterminada, muchos proveedores de recursos se registran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8743f-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="8743f-119">Sin embargo, puede que necesite toomanually registrar algunos proveedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="8743f-119">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="8743f-120">tooregister un proveedor de recursos, debe tener Hola de permiso tooperform `/register/action` operación Hola proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="8743f-120">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="8743f-121">Esta operación se incluye en los roles de propietario y Hola colaborador.</span><span class="sxs-lookup"><span data-stu-id="8743f-121">This operation is included in hello Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="8743f-122">Que devuelve resultados similares a:</span><span class="sxs-lookup"><span data-stu-id="8743f-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="8743f-123">No se puede anular el registro de un proveedor de recursos si todavía dispone de tipos de recursos de ese proveedor de recursos en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="8743f-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="8743f-124">toosee información de un proveedor de recursos determinado, use:</span><span class="sxs-lookup"><span data-stu-id="8743f-124">toosee information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="8743f-125">Que devuelve resultados similares a:</span><span class="sxs-lookup"><span data-stu-id="8743f-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="8743f-126">tipos de recursos de hello toosee para un proveedor de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="8743f-126">toosee hello resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="8743f-127">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="8743f-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="8743f-128">versión de la API de Hello corresponde versión tooa de operaciones de API de REST que se publican en proveedor de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-128">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="8743f-129">Como un proveedor de recursos permite ofrecer nuevas características, lanza una nueva versión de hello API de REST.</span><span class="sxs-lookup"><span data-stu-id="8743f-129">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="8743f-130">versiones API tooget Hola disponibles para un tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="8743f-130">tooget hello available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="8743f-131">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="8743f-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="8743f-132">El Administrador de recursos se admite en todas las regiones, pero podrían no admitir recursos Hola que implementar en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="8743f-132">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="8743f-133">Además, puede haber limitaciones en la suscripción que impide utilizar algunas regiones que admiten recurso Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="8743f-134">usar ubicaciones de hello admite tooget para un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="8743f-134">tooget hello supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="8743f-135">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="8743f-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="8743f-136">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="8743f-136">Azure CLI</span></span>
<span data-ttu-id="8743f-137">toosee todos los proveedores de recursos de Azure y el estado de registro de hello para su suscripción, usan:</span><span class="sxs-lookup"><span data-stu-id="8743f-137">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="8743f-138">Que devuelve resultados similares a:</span><span class="sxs-lookup"><span data-stu-id="8743f-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="8743f-139">Registrar un proveedor de recursos configura el toowork de suscripción con el proveedor de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-139">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="8743f-140">ámbito de Hello para el registro siempre es suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-140">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="8743f-141">De forma predeterminada, muchos proveedores de recursos se registran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8743f-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="8743f-142">Sin embargo, puede que necesite toomanually registrar algunos proveedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="8743f-142">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="8743f-143">tooregister un proveedor de recursos, debe tener Hola de permiso tooperform `/register/action` operación Hola proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="8743f-143">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="8743f-144">Esta operación se incluye en los roles de propietario y Hola colaborador.</span><span class="sxs-lookup"><span data-stu-id="8743f-144">This operation is included in hello Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="8743f-145">Que devuelve un mensaje que indica que el registro está en curso.</span><span class="sxs-lookup"><span data-stu-id="8743f-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="8743f-146">No se puede anular el registro de un proveedor de recursos si todavía dispone de tipos de recursos de ese proveedor de recursos en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="8743f-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="8743f-147">toosee información de un proveedor de recursos determinado, use:</span><span class="sxs-lookup"><span data-stu-id="8743f-147">toosee information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="8743f-148">Que devuelve resultados similares a:</span><span class="sxs-lookup"><span data-stu-id="8743f-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="8743f-149">tipos de recursos de hello toosee para un proveedor de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="8743f-149">toosee hello resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="8743f-150">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="8743f-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="8743f-151">versión de la API de Hello corresponde versión tooa de operaciones de API de REST que se publican en proveedor de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-151">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="8743f-152">Como un proveedor de recursos permite ofrecer nuevas características, lanza una nueva versión de hello API de REST.</span><span class="sxs-lookup"><span data-stu-id="8743f-152">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="8743f-153">versiones API tooget Hola disponibles para un tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="8743f-153">tooget hello available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="8743f-154">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="8743f-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="8743f-155">El Administrador de recursos se admite en todas las regiones, pero podrían no admitir recursos Hola que implementar en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="8743f-155">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="8743f-156">Además, puede haber limitaciones en la suscripción que impide utilizar algunas regiones que admiten recurso Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="8743f-157">usar ubicaciones de hello admite tooget para un tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="8743f-157">tooget hello supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="8743f-158">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="8743f-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="8743f-159">Portal</span><span class="sxs-lookup"><span data-stu-id="8743f-159">Portal</span></span>

<span data-ttu-id="8743f-160">Seleccione todos los proveedores de recursos de Azure y el estado de registro de hello para la suscripción de toosee **suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="8743f-160">toosee all resource providers in Azure, and hello registration status for your subscription, select **Subscriptions**.</span></span>

![selección de suscripciones](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="8743f-162">Elija Hola suscripción tooview.</span><span class="sxs-lookup"><span data-stu-id="8743f-162">Choose hello subscription tooview.</span></span>

![especificación de la suscripción](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="8743f-164">Seleccione **proveedores de recursos** y ver la lista de Hola de proveedores de recursos disponibles.</span><span class="sxs-lookup"><span data-stu-id="8743f-164">Select **Resource providers** and view hello list of available resource providers.</span></span>

![vista de los proveedores de recursos](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="8743f-166">Registrar un proveedor de recursos configura el toowork de suscripción con el proveedor de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-166">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="8743f-167">ámbito de Hello para el registro siempre es suscripción Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-167">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="8743f-168">De forma predeterminada, muchos proveedores de recursos se registran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8743f-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="8743f-169">Sin embargo, puede que necesite toomanually registrar algunos proveedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="8743f-169">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="8743f-170">tooregister un proveedor de recursos, debe tener Hola de permiso tooperform `/register/action` operación Hola proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="8743f-170">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="8743f-171">Esta operación se incluye en los roles de propietario y Hola colaborador.</span><span class="sxs-lookup"><span data-stu-id="8743f-171">This operation is included in hello Contributor and Owner roles.</span></span> <span data-ttu-id="8743f-172">Seleccione un proveedor de recursos, tooregister **registrar**.</span><span class="sxs-lookup"><span data-stu-id="8743f-172">tooregister a resource provider, select **Register**.</span></span>

![registro del proveedor de recursos](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="8743f-174">No se puede anular el registro de un proveedor de recursos si todavía dispone de tipos de recursos de ese proveedor de recursos en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="8743f-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="8743f-175">información de toosee para un proveedor de recursos determinado, seleccione **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="8743f-175">toosee information for a particular resource provider, select **More services**.</span></span>

![selección de más servicios](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="8743f-177">Busque **Resource Explorer** y selecciónelo en las opciones disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-177">Search for **Resource Explorer** and select it from hello available options.</span></span>

![selección de resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="8743f-179">Seleccione **Proveedores**.</span><span class="sxs-lookup"><span data-stu-id="8743f-179">Select **Providers**.</span></span>

![Selección de proveedores](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="8743f-181">Recursos y proveedor de recursos de hello Seleccione tipo que desea tooview.</span><span class="sxs-lookup"><span data-stu-id="8743f-181">Select hello resource provider and resource type that you want tooview.</span></span>

![Selección del tipo de recurso](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="8743f-183">El Administrador de recursos se admite en todas las regiones, pero podrían no admitir recursos Hola que implementar en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="8743f-183">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="8743f-184">Además, puede haber limitaciones en la suscripción que impide utilizar algunas regiones que admiten recurso Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> <span data-ttu-id="8743f-185">Explorador de recursos de Hello muestra ubicaciones válidas para el tipo de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-185">hello resource explorer displays valid locations for hello resource type.</span></span>

![Vista de las ubicaciones](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="8743f-187">versión de la API de Hello corresponde versión tooa de operaciones de API de REST que se publican en proveedor de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-187">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="8743f-188">Como un proveedor de recursos permite ofrecer nuevas características, lanza una nueva versión de hello API de REST.</span><span class="sxs-lookup"><span data-stu-id="8743f-188">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> <span data-ttu-id="8743f-189">Explorador de recursos de Hello muestra las versiones de API válidas para el tipo de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="8743f-189">hello resource explorer displays valid API versions for hello resource type.</span></span>

![Vista de las versiones de API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="8743f-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8743f-191">Next steps</span></span>
* <span data-ttu-id="8743f-192">toolearn acerca de cómo crear plantillas de administrador de recursos, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8743f-192">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8743f-193">toolearn sobre la implementación de recursos, consulte [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8743f-193">toolearn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="8743f-194">operaciones de hello tooview para un proveedor de recursos, consulte [API de REST de Azure](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="8743f-194">tooview hello operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

