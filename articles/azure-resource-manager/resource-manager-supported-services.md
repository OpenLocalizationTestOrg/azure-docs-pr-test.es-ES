---
title: Tipos de recursos y proveedores de recursos de Azure | Microsoft Docs
description: Describe los proveedores de recursos que admiten el Administrador de recursos, sus esquemas y las versiones disponibles de API y las regiones que pueden hospedar los recursos.
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
ms.openlocfilehash: 6a9128f45d4199404019cee594842d59c7f1aaf3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="b495f-103">Tipos y proveedores de recursos</span><span class="sxs-lookup"><span data-stu-id="b495f-103">Resource providers and types</span></span>

<span data-ttu-id="b495f-104">Al implementar los recursos, con frecuencia necesitará recuperar información sobre los tipos y proveedores de recursos.</span><span class="sxs-lookup"><span data-stu-id="b495f-104">When deploying resources, you frequently need to retrieve information about the resource providers and types.</span></span> <span data-ttu-id="b495f-105">En este artículo, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="b495f-105">In this article, you learn to:</span></span>

* <span data-ttu-id="b495f-106">Ver todos los proveedores de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="b495f-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="b495f-107">Comprobar el estado de registro de un proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="b495f-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="b495f-108">Registrar un proveedor de recursos</span><span class="sxs-lookup"><span data-stu-id="b495f-108">Register a resource provider</span></span>
* <span data-ttu-id="b495f-109">Ver los tipos de recursos de un proveedor</span><span class="sxs-lookup"><span data-stu-id="b495f-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="b495f-110">Ver las ubicaciones válidas de un tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="b495f-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="b495f-111">Ver las versiones de API válidas de un tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="b495f-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="b495f-112">También puede llevar a cabo estos pasos a través del portal, PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="b495f-112">You can perform these steps through the portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="b495f-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b495f-113">PowerShell</span></span>

<span data-ttu-id="b495f-114">Para ver todos los proveedores de recursos de Azure y el estado de registro de su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="b495f-114">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="b495f-115">Que devuelve resultados similares a:</span><span class="sxs-lookup"><span data-stu-id="b495f-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="b495f-116">Al registrar un proveedor de recursos se configura la suscripción para que funcione con este.</span><span class="sxs-lookup"><span data-stu-id="b495f-116">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="b495f-117">El ámbito de registro es siempre la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b495f-117">The scope for registration is always the subscription.</span></span> <span data-ttu-id="b495f-118">De forma predeterminada, muchos proveedores de recursos se registran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b495f-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="b495f-119">Pero es posible que tenga que registrar manualmente algunos.</span><span class="sxs-lookup"><span data-stu-id="b495f-119">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="b495f-120">Para registrar un proveedor de recursos, debe tener permiso para realizar la operación `/register/action` para este.</span><span class="sxs-lookup"><span data-stu-id="b495f-120">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="b495f-121">Esta operación está incluida en los roles Colaborador y Propietario.</span><span class="sxs-lookup"><span data-stu-id="b495f-121">This operation is included in the Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="b495f-122">Que devuelve resultados similares a:</span><span class="sxs-lookup"><span data-stu-id="b495f-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="b495f-123">No se puede anular el registro de un proveedor de recursos si todavía dispone de tipos de recursos de ese proveedor de recursos en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b495f-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="b495f-124">Para ver información de un proveedor de recursos concreto, use:</span><span class="sxs-lookup"><span data-stu-id="b495f-124">To see information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="b495f-125">Que devuelve resultados similares a:</span><span class="sxs-lookup"><span data-stu-id="b495f-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="b495f-126">Para ver los tipos de recursos de un proveedor, use:</span><span class="sxs-lookup"><span data-stu-id="b495f-126">To see the resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="b495f-127">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="b495f-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="b495f-128">La versión de API se corresponde a una versión de operaciones de API de REST que se publican por el proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="b495f-128">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="b495f-129">Conforme un proveedor de recursos habilite nuevas características, publicará una nueva versión de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="b495f-129">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="b495f-130">Para obtener las versiones de API de un tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="b495f-130">To get the available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="b495f-131">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="b495f-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="b495f-132">El Administrador de recursos se admite en todas las regiones, pero puede que los recursos que implementa no se admitan en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="b495f-132">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="b495f-133">Además, puede haber limitaciones en su suscripción que le impidan utilizar algunas regiones que admiten el recurso.</span><span class="sxs-lookup"><span data-stu-id="b495f-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="b495f-134">Para obtener las ubicaciones compatibles con un tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="b495f-134">To get the supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="b495f-135">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="b495f-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="b495f-136">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b495f-136">Azure CLI</span></span>
<span data-ttu-id="b495f-137">Para ver todos los proveedores de recursos de Azure y el estado de registro de su suscripción, use:</span><span class="sxs-lookup"><span data-stu-id="b495f-137">To see all resource providers in Azure, and the registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="b495f-138">Que devuelve resultados similares a:</span><span class="sxs-lookup"><span data-stu-id="b495f-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="b495f-139">Al registrar un proveedor de recursos se configura la suscripción para que funcione con este.</span><span class="sxs-lookup"><span data-stu-id="b495f-139">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="b495f-140">El ámbito de registro es siempre la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b495f-140">The scope for registration is always the subscription.</span></span> <span data-ttu-id="b495f-141">De forma predeterminada, muchos proveedores de recursos se registran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b495f-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="b495f-142">Pero es posible que tenga que registrar manualmente algunos.</span><span class="sxs-lookup"><span data-stu-id="b495f-142">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="b495f-143">Para registrar un proveedor de recursos, debe tener permiso para realizar la operación `/register/action` para este.</span><span class="sxs-lookup"><span data-stu-id="b495f-143">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="b495f-144">Esta operación está incluida en los roles Colaborador y Propietario.</span><span class="sxs-lookup"><span data-stu-id="b495f-144">This operation is included in the Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="b495f-145">Que devuelve un mensaje que indica que el registro está en curso.</span><span class="sxs-lookup"><span data-stu-id="b495f-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="b495f-146">No se puede anular el registro de un proveedor de recursos si todavía dispone de tipos de recursos de ese proveedor de recursos en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b495f-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="b495f-147">Para ver información de un proveedor de recursos concreto, use:</span><span class="sxs-lookup"><span data-stu-id="b495f-147">To see information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="b495f-148">Que devuelve resultados similares a:</span><span class="sxs-lookup"><span data-stu-id="b495f-148">Which returns results similar to:</span></span>

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

<span data-ttu-id="b495f-149">Para ver los tipos de recursos de un proveedor, use:</span><span class="sxs-lookup"><span data-stu-id="b495f-149">To see the resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="b495f-150">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="b495f-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="b495f-151">La versión de API se corresponde a una versión de operaciones de API de REST que se publican por el proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="b495f-151">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="b495f-152">Conforme un proveedor de recursos habilite nuevas características, publicará una nueva versión de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="b495f-152">As a resource provider enables new features, it releases a new version of the REST API.</span></span> 

<span data-ttu-id="b495f-153">Para obtener las versiones de API de un tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="b495f-153">To get the available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="b495f-154">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="b495f-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="b495f-155">El Administrador de recursos se admite en todas las regiones, pero puede que los recursos que implementa no se admitan en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="b495f-155">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="b495f-156">Además, puede haber limitaciones en su suscripción que le impidan utilizar algunas regiones que admiten el recurso.</span><span class="sxs-lookup"><span data-stu-id="b495f-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> 

<span data-ttu-id="b495f-157">Para obtener las ubicaciones compatibles con un tipo de recurso, use:</span><span class="sxs-lookup"><span data-stu-id="b495f-157">To get the supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="b495f-158">Que devuelve:</span><span class="sxs-lookup"><span data-stu-id="b495f-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="b495f-159">Portal</span><span class="sxs-lookup"><span data-stu-id="b495f-159">Portal</span></span>

<span data-ttu-id="b495f-160">Para ver todos los proveedores de recursos de Azure y el estado de registro de su suscripción, seleccione **Suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="b495f-160">To see all resource providers in Azure, and the registration status for your subscription, select **Subscriptions**.</span></span>

![selección de suscripciones](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="b495f-162">Elija la suscripción que quiera ver.</span><span class="sxs-lookup"><span data-stu-id="b495f-162">Choose the subscription to view.</span></span>

![especificación de la suscripción](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="b495f-164">Seleccione **Proveedores de recursos** y consulte la lista de proveedores de recursos disponibles.</span><span class="sxs-lookup"><span data-stu-id="b495f-164">Select **Resource providers** and view the list of available resource providers.</span></span>

![vista de los proveedores de recursos](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="b495f-166">Al registrar un proveedor de recursos se configura la suscripción para que funcione con este.</span><span class="sxs-lookup"><span data-stu-id="b495f-166">Registering a resource provider configures your subscription to work with the resource provider.</span></span> <span data-ttu-id="b495f-167">El ámbito de registro es siempre la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b495f-167">The scope for registration is always the subscription.</span></span> <span data-ttu-id="b495f-168">De forma predeterminada, muchos proveedores de recursos se registran automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b495f-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="b495f-169">Pero es posible que tenga que registrar manualmente algunos.</span><span class="sxs-lookup"><span data-stu-id="b495f-169">However, you may need to manually register some resource providers.</span></span> <span data-ttu-id="b495f-170">Para registrar un proveedor de recursos, debe tener permiso para realizar la operación `/register/action` para este.</span><span class="sxs-lookup"><span data-stu-id="b495f-170">To register a resource provider, you must have permission to perform the `/register/action` operation for the resource provider.</span></span> <span data-ttu-id="b495f-171">Esta operación está incluida en los roles Colaborador y Propietario.</span><span class="sxs-lookup"><span data-stu-id="b495f-171">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="b495f-172">Para registrar un proveedor de recursos, seleccione **Registro**.</span><span class="sxs-lookup"><span data-stu-id="b495f-172">To register a resource provider, select **Register**.</span></span>

![registro del proveedor de recursos](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="b495f-174">No se puede anular el registro de un proveedor de recursos si todavía dispone de tipos de recursos de ese proveedor de recursos en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="b495f-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="b495f-175">Para ver información de un proveedor de recursos concreto, seleccione **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="b495f-175">To see information for a particular resource provider, select **More services**.</span></span>

![selección de más servicios](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="b495f-177">Busque **Resource Explorer** y selecciónelo entre las opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="b495f-177">Search for **Resource Explorer** and select it from the available options.</span></span>

![selección de resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="b495f-179">Seleccione **Proveedores**.</span><span class="sxs-lookup"><span data-stu-id="b495f-179">Select **Providers**.</span></span>

![Selección de proveedores](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="b495f-181">Seleccione el proveedor de recursos y el tipo de recurso que desea ver.</span><span class="sxs-lookup"><span data-stu-id="b495f-181">Select the resource provider and resource type that you want to view.</span></span>

![Selección del tipo de recurso](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="b495f-183">El Administrador de recursos se admite en todas las regiones, pero puede que los recursos que implementa no se admitan en todas las regiones.</span><span class="sxs-lookup"><span data-stu-id="b495f-183">Resource Manager is supported in all regions, but the resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="b495f-184">Además, puede haber limitaciones en su suscripción que le impidan utilizar algunas regiones que admiten el recurso.</span><span class="sxs-lookup"><span data-stu-id="b495f-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support the resource.</span></span> <span data-ttu-id="b495f-185">El explorador de recursos muestra las ubicaciones válidas para el tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="b495f-185">The resource explorer displays valid locations for the resource type.</span></span>

![Vista de las ubicaciones](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="b495f-187">La versión de API se corresponde a una versión de operaciones de API de REST que se publican por el proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="b495f-187">The API version corresponds to a version of REST API operations that are released by the resource provider.</span></span> <span data-ttu-id="b495f-188">Conforme un proveedor de recursos habilite nuevas características, publicará una nueva versión de la API de REST.</span><span class="sxs-lookup"><span data-stu-id="b495f-188">As a resource provider enables new features, it releases a new version of the REST API.</span></span> <span data-ttu-id="b495f-189">El explorador de recursos muestra las versiones de API válidas para el tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="b495f-189">The resource explorer displays valid API versions for the resource type.</span></span>

![Vista de las versiones de API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="b495f-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b495f-191">Next steps</span></span>
* <span data-ttu-id="b495f-192">Para obtener más información sobre la creación de plantillas del Administrador de recursos, consulte [Creación de plantillas del Administrador de recursos de Azure](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b495f-192">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="b495f-193">Para obtener más información sobre la implementación de recursos, consulte [Implementación de una aplicación con la plantilla del Administrador de recursos de Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b495f-193">To learn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="b495f-194">Para ver las operaciones de un proveedor de recursos, consulte [API de REST de Azure](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="b495f-194">To view the operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

