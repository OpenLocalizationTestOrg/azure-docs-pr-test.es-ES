---
title: funciones de plantilla de administrador de recursos de aaaAzure - recursos | Documentos de Microsoft
description: Describe hello toouse de funciones en un tooretrieve de valores de la plantilla de Azure Resource Manager acerca de los recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="88cdc-103">Funciones de recursos para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="88cdc-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="88cdc-104">Administrador de recursos proporciona Hola siguientes funciones para obtener valores de recurso:</span><span class="sxs-lookup"><span data-stu-id="88cdc-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="88cdc-105">listKeys y list{Value}</span><span class="sxs-lookup"><span data-stu-id="88cdc-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="88cdc-106">providers</span><span class="sxs-lookup"><span data-stu-id="88cdc-106">providers</span></span>](#providers)
* [<span data-ttu-id="88cdc-107">reference</span><span class="sxs-lookup"><span data-stu-id="88cdc-107">reference</span></span>](#reference)
* [<span data-ttu-id="88cdc-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="88cdc-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="88cdc-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="88cdc-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="88cdc-110">suscripción</span><span class="sxs-lookup"><span data-stu-id="88cdc-110">subscription</span></span>](#subscription)

<span data-ttu-id="88cdc-111">tooget valores de parámetros, variables o la implementación actual de hello, consulte [funciones con valores de implementación](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="88cdc-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="88cdc-112">listKeys y list{Value}</span><span class="sxs-lookup"><span data-stu-id="88cdc-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="88cdc-113">Devuelve Hola valores para cualquier tipo de recurso que admite la operación de lista Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="88cdc-114">el uso más común de Hello es `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="88cdc-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="88cdc-115">parameters</span><span class="sxs-lookup"><span data-stu-id="88cdc-115">Parameters</span></span>

| <span data-ttu-id="88cdc-116">Parámetro</span><span class="sxs-lookup"><span data-stu-id="88cdc-116">Parameter</span></span> | <span data-ttu-id="88cdc-117">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="88cdc-117">Required</span></span> | <span data-ttu-id="88cdc-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="88cdc-118">Type</span></span> | <span data-ttu-id="88cdc-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="88cdc-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="88cdc-120">resourceName o resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="88cdc-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="88cdc-121">Sí</span><span class="sxs-lookup"><span data-stu-id="88cdc-121">Yes</span></span> |<span data-ttu-id="88cdc-122">cadena</span><span class="sxs-lookup"><span data-stu-id="88cdc-122">string</span></span> |<span data-ttu-id="88cdc-123">Identificador único para el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="88cdc-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="88cdc-124">apiVersion</span></span> |<span data-ttu-id="88cdc-125">Sí</span><span class="sxs-lookup"><span data-stu-id="88cdc-125">Yes</span></span> |<span data-ttu-id="88cdc-126">cadena</span><span class="sxs-lookup"><span data-stu-id="88cdc-126">string</span></span> |<span data-ttu-id="88cdc-127">Versión de API de estado en tiempo de ejecución de un recurso.</span><span class="sxs-lookup"><span data-stu-id="88cdc-127">API version of resource runtime state.</span></span> <span data-ttu-id="88cdc-128">Por lo general, en formato de hello, **aaaa-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="88cdc-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="88cdc-129">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="88cdc-129">Return value</span></span>

<span data-ttu-id="88cdc-130">Hola devuelve tiene un objeto de listKeys Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="88cdc-130">hello returned object from listKeys has hello following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="88cdc-131">Otras funciones List tienen diferentes formatos de retorno.</span><span class="sxs-lookup"><span data-stu-id="88cdc-131">Other list functions have different return formats.</span></span> <span data-ttu-id="88cdc-132">formato de hello toosee de una función, inclúyala en hello salidas sección tal y como se muestra en la plantilla de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="88cdc-133">Comentarios</span><span class="sxs-lookup"><span data-stu-id="88cdc-133">Remarks</span></span>

<span data-ttu-id="88cdc-134">Cualquier operación que comienza por **list** se puede usar como función en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="88cdc-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="88cdc-135">Hello las operaciones disponibles incluyen no solo listKeys, pero también las operaciones como `list`, `listAdminKeys`, y `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="88cdc-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="88cdc-136">Sin embargo, no puede usar **lista** las operaciones que requieren valores de hello cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="88cdc-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="88cdc-137">Por ejemplo, hello [lista cuenta SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operación requiere parámetros de cuerpo de solicitud, como *signedExpiry*, por lo que no puede usar dentro de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="88cdc-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="88cdc-138">toodetermine qué tipos de recursos tienen una operación de lista, deberá Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="88cdc-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="88cdc-139">Hola de vista [operaciones de API de REST](/rest/api/) para un proveedor de recursos y buscar la lista de operaciones.</span><span class="sxs-lookup"><span data-stu-id="88cdc-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="88cdc-140">Por ejemplo, las cuentas de almacenamiento tienen hello [listKeys operación](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="88cdc-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="88cdc-141">Hola de uso [AzureRmProviderOperation Get](/powershell/module/azurerm.resources/get-azurermprovideroperation) cmdlet de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88cdc-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="88cdc-142">Hello en el ejemplo siguiente se obtiene todas las operaciones de lista para las cuentas de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="88cdc-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="88cdc-143">Usar hello siguiente toofilter Hola sólo la lista de operaciones de comando de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="88cdc-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="88cdc-144">Especificar recursos de hello mediante cualquier hello [función resourceId](#resourceid), formato de Hola o `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="88cdc-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="88cdc-145">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="88cdc-145">Example</span></span>

<span data-ttu-id="88cdc-146">Hello en el ejemplo siguiente se muestra cómo los claves principal y secundaria de hello tooreturn de una cuenta de almacenamiento de Hola genera sección.</span><span class="sxs-lookup"><span data-stu-id="88cdc-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="88cdc-147">providers</span><span class="sxs-lookup"><span data-stu-id="88cdc-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="88cdc-148">Devuelve información acerca de un proveedor de recursos y sus tipos de recursos admitidos.</span><span class="sxs-lookup"><span data-stu-id="88cdc-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="88cdc-149">Si no proporciona un tipo de recurso, función hello devuelve todos los tipos de hello admitida Hola proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="88cdc-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="88cdc-150">parameters</span><span class="sxs-lookup"><span data-stu-id="88cdc-150">Parameters</span></span>

| <span data-ttu-id="88cdc-151">Parámetro</span><span class="sxs-lookup"><span data-stu-id="88cdc-151">Parameter</span></span> | <span data-ttu-id="88cdc-152">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="88cdc-152">Required</span></span> | <span data-ttu-id="88cdc-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="88cdc-153">Type</span></span> | <span data-ttu-id="88cdc-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="88cdc-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="88cdc-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="88cdc-155">providerNamespace</span></span> |<span data-ttu-id="88cdc-156">Sí</span><span class="sxs-lookup"><span data-stu-id="88cdc-156">Yes</span></span> |<span data-ttu-id="88cdc-157">cadena</span><span class="sxs-lookup"><span data-stu-id="88cdc-157">string</span></span> |<span data-ttu-id="88cdc-158">Namespace del proveedor de Hola</span><span class="sxs-lookup"><span data-stu-id="88cdc-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="88cdc-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="88cdc-159">resourceType</span></span> |<span data-ttu-id="88cdc-160">No</span><span class="sxs-lookup"><span data-stu-id="88cdc-160">No</span></span> |<span data-ttu-id="88cdc-161">cadena</span><span class="sxs-lookup"><span data-stu-id="88cdc-161">string</span></span> |<span data-ttu-id="88cdc-162">tipo de Hola de recurso dentro de hello especifica espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="88cdc-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="88cdc-163">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="88cdc-163">Return value</span></span>

<span data-ttu-id="88cdc-164">Cada tipo admitido se devuelve en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="88cdc-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="88cdc-165">Matriz de clasificación de hello devuelto no se garantiza que los valores.</span><span class="sxs-lookup"><span data-stu-id="88cdc-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="88cdc-166">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="88cdc-166">Example</span></span>

<span data-ttu-id="88cdc-167">Hola de ejemplo siguiente muestra cómo toouse Hola función de proveedor:</span><span class="sxs-lookup"><span data-stu-id="88cdc-167">hello following example shows how toouse hello provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="88cdc-168">Hello en el ejemplo anterior se devuelve un objeto de hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="88cdc-168">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="88cdc-169">reference</span><span class="sxs-lookup"><span data-stu-id="88cdc-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="88cdc-170">Devuelve un objeto que representa el estado de tiempo de ejecución de un recurso.</span><span class="sxs-lookup"><span data-stu-id="88cdc-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="88cdc-171">parameters</span><span class="sxs-lookup"><span data-stu-id="88cdc-171">Parameters</span></span>

| <span data-ttu-id="88cdc-172">Parámetro</span><span class="sxs-lookup"><span data-stu-id="88cdc-172">Parameter</span></span> | <span data-ttu-id="88cdc-173">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="88cdc-173">Required</span></span> | <span data-ttu-id="88cdc-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="88cdc-174">Type</span></span> | <span data-ttu-id="88cdc-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="88cdc-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="88cdc-176">resourceName o resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="88cdc-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="88cdc-177">Sí</span><span class="sxs-lookup"><span data-stu-id="88cdc-177">Yes</span></span> |<span data-ttu-id="88cdc-178">string</span><span class="sxs-lookup"><span data-stu-id="88cdc-178">string</span></span> |<span data-ttu-id="88cdc-179">Nombre o identificador único de un recurso.</span><span class="sxs-lookup"><span data-stu-id="88cdc-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="88cdc-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="88cdc-180">apiVersion</span></span> |<span data-ttu-id="88cdc-181">No</span><span class="sxs-lookup"><span data-stu-id="88cdc-181">No</span></span> |<span data-ttu-id="88cdc-182">cadena</span><span class="sxs-lookup"><span data-stu-id="88cdc-182">string</span></span> |<span data-ttu-id="88cdc-183">Versión de API de hello recurso específico.</span><span class="sxs-lookup"><span data-stu-id="88cdc-183">API version of hello specified resource.</span></span> <span data-ttu-id="88cdc-184">Incluya este parámetro cuando no se ha aprovisionado el recurso de hello dentro de la misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="88cdc-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="88cdc-185">Por lo general, en formato de hello, **aaaa-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="88cdc-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="88cdc-186">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="88cdc-186">Return value</span></span>

<span data-ttu-id="88cdc-187">Cada tipo de recurso devuelve propiedades distintas para cada función de la referencia de hello.</span><span class="sxs-lookup"><span data-stu-id="88cdc-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="88cdc-188">función Hello no devuelve un solo formato predefinido.</span><span class="sxs-lookup"><span data-stu-id="88cdc-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="88cdc-189">toosee Hola propiedades para un tipo de recurso, que devuelven objetos Hola Hola genera sección tal y como se muestra en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="88cdc-190">Comentarios</span><span class="sxs-lookup"><span data-stu-id="88cdc-190">Remarks</span></span>

<span data-ttu-id="88cdc-191">función de la referencia de Hello deriva su valor desde un estado en tiempo de ejecución y, por tanto, no se puede usar en la sección de variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="88cdc-192">Se puede utilizar en la sección de salidas de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="88cdc-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="88cdc-193">Mediante la función de la referencia de hello, se declara implícitamente que un recurso depende otro recurso si se aprovisionan recursos Hola al que hace referencia dentro de la misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="88cdc-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="88cdc-194">No es necesario propiedad dependsOn de tooalso use Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="88cdc-195">Hello función no se ha evalúa hasta hello recursos que se hace referencia han completado la implementación.</span><span class="sxs-lookup"><span data-stu-id="88cdc-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="88cdc-196">nombres de propiedad de hello toosee y valores para un tipo de recurso, cree una plantilla que devuelve el objeto de hello en la sección de salidas de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="88cdc-197">Si tiene un recurso existente de ese tipo, la plantilla devuelve objeto Hola sin necesidad de implementar los nuevos recursos.</span><span class="sxs-lookup"><span data-stu-id="88cdc-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="88cdc-198">Normalmente, se utiliza hello **referencia** función tooreturn un valor determinado de un objeto, como el URI del extremo de blob de Hola o el nombre de dominio completo.</span><span class="sxs-lookup"><span data-stu-id="88cdc-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="88cdc-199">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="88cdc-199">Example</span></span>

<span data-ttu-id="88cdc-200">toodeploy y referencia de recurso de Hola Hola misma plantilla, use:</span><span class="sxs-lookup"><span data-stu-id="88cdc-200">toodeploy and reference hello resource in hello same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="88cdc-201">Hello en el ejemplo anterior se devuelve un objeto de hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="88cdc-201">hello preceding example returns an object in hello following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="88cdc-202">Hello en el ejemplo siguiente se hace referencia a una cuenta de almacenamiento que no está implementada en esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="88cdc-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="88cdc-203">Hello cuenta de almacenamiento ya existe dentro de hello mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="88cdc-203">hello storage account already exists within hello same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="88cdc-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="88cdc-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="88cdc-205">Devuelve un objeto que representa el grupo de recursos actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="88cdc-206">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="88cdc-206">Return value</span></span>

<span data-ttu-id="88cdc-207">Hola devuelve el objeto se encuentra en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="88cdc-207">hello returned object is in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="88cdc-208">Comentarios</span><span class="sxs-lookup"><span data-stu-id="88cdc-208">Remarks</span></span>

<span data-ttu-id="88cdc-209">Un uso común de la función de grupo de recursos de hello es toocreate recursos Hola misma ubicación que el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="88cdc-210">Hello en el ejemplo siguiente se usa Hola recursos grupo tooassign Hola ubicación de un sitio web.</span><span class="sxs-lookup"><span data-stu-id="88cdc-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="88cdc-211">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="88cdc-211">Example</span></span>

<span data-ttu-id="88cdc-212">Hello plantilla siguiente devuelve las propiedades de Hola Hola del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="88cdc-212">hello following template returns hello properties of hello resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="88cdc-213">Hello en el ejemplo anterior se devuelve un objeto de hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="88cdc-213">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="88cdc-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="88cdc-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="88cdc-215">Devuelve Hola identificador único de un recurso.</span><span class="sxs-lookup"><span data-stu-id="88cdc-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="88cdc-216">Use esta función cuando el nombre del recurso de hello es ambiguo o no se ha aprovisionado en hello misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="88cdc-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="88cdc-217">parameters</span><span class="sxs-lookup"><span data-stu-id="88cdc-217">Parameters</span></span>

| <span data-ttu-id="88cdc-218">Parámetro</span><span class="sxs-lookup"><span data-stu-id="88cdc-218">Parameter</span></span> | <span data-ttu-id="88cdc-219">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="88cdc-219">Required</span></span> | <span data-ttu-id="88cdc-220">Tipo</span><span class="sxs-lookup"><span data-stu-id="88cdc-220">Type</span></span> | <span data-ttu-id="88cdc-221">Descripción</span><span class="sxs-lookup"><span data-stu-id="88cdc-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="88cdc-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="88cdc-222">subscriptionId</span></span> |<span data-ttu-id="88cdc-223">No</span><span class="sxs-lookup"><span data-stu-id="88cdc-223">No</span></span> |<span data-ttu-id="88cdc-224">Cadena (en formato de GUID)</span><span class="sxs-lookup"><span data-stu-id="88cdc-224">string (In GUID format)</span></span> |<span data-ttu-id="88cdc-225">Valor predeterminado es la suscripción actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-225">Default value is hello current subscription.</span></span> <span data-ttu-id="88cdc-226">Especifique este valor cuando necesite tooretrieve un recurso en otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="88cdc-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="88cdc-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="88cdc-227">resourceGroupName</span></span> |<span data-ttu-id="88cdc-228">No</span><span class="sxs-lookup"><span data-stu-id="88cdc-228">No</span></span> |<span data-ttu-id="88cdc-229">cadena</span><span class="sxs-lookup"><span data-stu-id="88cdc-229">string</span></span> |<span data-ttu-id="88cdc-230">El valor predeterminado es el grupo de recursos actual.</span><span class="sxs-lookup"><span data-stu-id="88cdc-230">Default value is current resource group.</span></span> <span data-ttu-id="88cdc-231">Especifique este valor cuando necesite tooretrieve un recurso en otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="88cdc-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="88cdc-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="88cdc-232">resourceType</span></span> |<span data-ttu-id="88cdc-233">Sí</span><span class="sxs-lookup"><span data-stu-id="88cdc-233">Yes</span></span> |<span data-ttu-id="88cdc-234">string</span><span class="sxs-lookup"><span data-stu-id="88cdc-234">string</span></span> |<span data-ttu-id="88cdc-235">Tipo de recurso, incluido el espacio de nombres del proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="88cdc-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="88cdc-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="88cdc-236">resourceName1</span></span> |<span data-ttu-id="88cdc-237">Sí</span><span class="sxs-lookup"><span data-stu-id="88cdc-237">Yes</span></span> |<span data-ttu-id="88cdc-238">cadena</span><span class="sxs-lookup"><span data-stu-id="88cdc-238">string</span></span> |<span data-ttu-id="88cdc-239">Nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="88cdc-239">Name of resource.</span></span> |
| <span data-ttu-id="88cdc-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="88cdc-240">resourceName2</span></span> |<span data-ttu-id="88cdc-241">No</span><span class="sxs-lookup"><span data-stu-id="88cdc-241">No</span></span> |<span data-ttu-id="88cdc-242">string</span><span class="sxs-lookup"><span data-stu-id="88cdc-242">string</span></span> |<span data-ttu-id="88cdc-243">Siguiente segmento de nombre de recurso si el recurso está anidado.</span><span class="sxs-lookup"><span data-stu-id="88cdc-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="88cdc-244">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="88cdc-244">Return value</span></span>

<span data-ttu-id="88cdc-245">identificador de Hola se devuelve en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="88cdc-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="88cdc-246">Comentarios</span><span class="sxs-lookup"><span data-stu-id="88cdc-246">Remarks</span></span>

<span data-ttu-id="88cdc-247">Hello valores de parámetro especificados dependen de si el recurso de hello está en hello mismo grupo de recursos y la suscripción como la implementación actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="88cdc-248">recursos de hello tooget el Id. de una cuenta de almacenamiento en hello mismo suscripción y el grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="88cdc-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="88cdc-249">Id. de recurso de hello tooget para una cuenta de almacenamiento en Hola misma suscripción, pero un grupo de recursos diferente, utilice:</span><span class="sxs-lookup"><span data-stu-id="88cdc-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="88cdc-250">Id. de recurso de hello tooget para una cuenta de almacenamiento en una suscripción diferente y el grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="88cdc-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="88cdc-251">Id. de recurso de hello tooget para una base de datos en otro grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="88cdc-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="88cdc-252">A menudo, necesita toouse esta función si usa una cuenta de almacenamiento o red virtual en un grupo de recursos alternativos.</span><span class="sxs-lookup"><span data-stu-id="88cdc-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="88cdc-253">Hello en el ejemplo siguiente se muestra cómo fácilmente se puede utilizar un recurso de un grupo de recursos externos:</span><span class="sxs-lookup"><span data-stu-id="88cdc-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="88cdc-254">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="88cdc-254">Example</span></span>

<span data-ttu-id="88cdc-255">Hello en el ejemplo siguiente se devuelve Hola Id. de recurso para una cuenta de almacenamiento en grupo de recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="88cdc-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="88cdc-256">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="88cdc-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="88cdc-257">Nombre</span><span class="sxs-lookup"><span data-stu-id="88cdc-257">Name</span></span> | <span data-ttu-id="88cdc-258">Tipo</span><span class="sxs-lookup"><span data-stu-id="88cdc-258">Type</span></span> | <span data-ttu-id="88cdc-259">Valor</span><span class="sxs-lookup"><span data-stu-id="88cdc-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="88cdc-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="88cdc-260">sameRGOutput</span></span> | <span data-ttu-id="88cdc-261">String</span><span class="sxs-lookup"><span data-stu-id="88cdc-261">String</span></span> | <span data-ttu-id="88cdc-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="88cdc-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="88cdc-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="88cdc-263">differentRGOutput</span></span> | <span data-ttu-id="88cdc-264">String</span><span class="sxs-lookup"><span data-stu-id="88cdc-264">String</span></span> | <span data-ttu-id="88cdc-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="88cdc-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="88cdc-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="88cdc-266">differentSubOutput</span></span> | <span data-ttu-id="88cdc-267">String</span><span class="sxs-lookup"><span data-stu-id="88cdc-267">String</span></span> | <span data-ttu-id="88cdc-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="88cdc-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="88cdc-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="88cdc-269">nestedResourceOutput</span></span> | <span data-ttu-id="88cdc-270">String</span><span class="sxs-lookup"><span data-stu-id="88cdc-270">String</span></span> | <span data-ttu-id="88cdc-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="88cdc-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="88cdc-272">suscripción</span><span class="sxs-lookup"><span data-stu-id="88cdc-272">subscription</span></span>
`subscription()`

<span data-ttu-id="88cdc-273">Devuelve detalles acerca de la suscripción de hello para la implementación actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="88cdc-274">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="88cdc-274">Return value</span></span>

<span data-ttu-id="88cdc-275">función Hello devuelve Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="88cdc-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="88cdc-276">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="88cdc-276">Example</span></span>

<span data-ttu-id="88cdc-277">Hello en el ejemplo siguiente se muestra hello suscripción función llamado en la sección de salidas de Hola.</span><span class="sxs-lookup"><span data-stu-id="88cdc-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="88cdc-278">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="88cdc-278">Next steps</span></span>
* <span data-ttu-id="88cdc-279">Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="88cdc-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="88cdc-280">toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="88cdc-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="88cdc-281">tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="88cdc-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="88cdc-282">toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="88cdc-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

