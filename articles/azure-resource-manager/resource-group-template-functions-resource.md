---
title: 'Funciones de la plantilla de Azure Resource Manager: recursos | Microsoft Docs'
description: Describe las funciones para usar en una plantilla de Azure Resource Manager para recuperar valores sobre recursos.
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
ms.openlocfilehash: 494ade55f21c19d9c68d5cc52756528401d9bb77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="8ffc3-103">Funciones de recursos para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8ffc3-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="8ffc3-104">El Administrador de recursos ofrece las siguientes funciones para obtener valores de recursos:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-104">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="8ffc3-105">listKeys y list{Value}</span><span class="sxs-lookup"><span data-stu-id="8ffc3-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="8ffc3-106">providers</span><span class="sxs-lookup"><span data-stu-id="8ffc3-106">providers</span></span>](#providers)
* [<span data-ttu-id="8ffc3-107">reference</span><span class="sxs-lookup"><span data-stu-id="8ffc3-107">reference</span></span>](#reference)
* [<span data-ttu-id="8ffc3-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="8ffc3-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="8ffc3-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="8ffc3-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="8ffc3-110">suscripción</span><span class="sxs-lookup"><span data-stu-id="8ffc3-110">subscription</span></span>](#subscription)

<span data-ttu-id="8ffc3-111">Para obtener valores de parámetro, variables o la implementación actual, consulte [Funciones con valores de implementación](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="8ffc3-111">To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="8ffc3-112">listKeys y list{Value}</span><span class="sxs-lookup"><span data-stu-id="8ffc3-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="8ffc3-113">Devuelve los valores para cualquier tipo de recurso que admite la operación list.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-113">Returns the values for any resource type that supports the list operation.</span></span> <span data-ttu-id="8ffc3-114">El uso más común es `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-114">The most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="8ffc3-115">parameters</span><span class="sxs-lookup"><span data-stu-id="8ffc3-115">Parameters</span></span>

| <span data-ttu-id="8ffc3-116">Parámetro</span><span class="sxs-lookup"><span data-stu-id="8ffc3-116">Parameter</span></span> | <span data-ttu-id="8ffc3-117">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8ffc3-117">Required</span></span> | <span data-ttu-id="8ffc3-118">Tipo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-118">Type</span></span> | <span data-ttu-id="8ffc3-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="8ffc3-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8ffc3-120">resourceName o resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="8ffc3-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="8ffc3-121">Sí</span><span class="sxs-lookup"><span data-stu-id="8ffc3-121">Yes</span></span> |<span data-ttu-id="8ffc3-122">string</span><span class="sxs-lookup"><span data-stu-id="8ffc3-122">string</span></span> |<span data-ttu-id="8ffc3-123">Identificador único para el recurso.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-123">Unique identifier for the resource.</span></span> |
| <span data-ttu-id="8ffc3-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8ffc3-124">apiVersion</span></span> |<span data-ttu-id="8ffc3-125">Sí</span><span class="sxs-lookup"><span data-stu-id="8ffc3-125">Yes</span></span> |<span data-ttu-id="8ffc3-126">cadena</span><span class="sxs-lookup"><span data-stu-id="8ffc3-126">string</span></span> |<span data-ttu-id="8ffc3-127">Versión de API de estado en tiempo de ejecución de un recurso.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-127">API version of resource runtime state.</span></span> <span data-ttu-id="8ffc3-128">Por lo general, en el formato, **aaaa-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-128">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="8ffc3-129">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="8ffc3-129">Return value</span></span>

<span data-ttu-id="8ffc3-130">El objeto devuelto desde listKeys tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-130">The returned object from listKeys has the following format:</span></span>

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

<span data-ttu-id="8ffc3-131">Otras funciones List tienen diferentes formatos de retorno.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-131">Other list functions have different return formats.</span></span> <span data-ttu-id="8ffc3-132">Para ver el formato de una función, inclúyalo en la sección de resultados tal y como se muestra en la plantilla de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-132">To see the format of a function, include it in the outputs section as shown in the example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="8ffc3-133">Comentarios</span><span class="sxs-lookup"><span data-stu-id="8ffc3-133">Remarks</span></span>

<span data-ttu-id="8ffc3-134">Cualquier operación que comienza por **list** se puede usar como función en la plantilla.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="8ffc3-135">Entre las operaciones disponibles se incluyen no solo listKeys, sino también operaciones como `list`, `listAdminKeys` y `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-135">The available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="8ffc3-136">Sin embargo, no puede usar operaciones **list** que requieren valores en el cuerpo de solicitud.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-136">However, you cannot use **list** operations that require values in the request body.</span></span> <span data-ttu-id="8ffc3-137">Por ejemplo, la operación [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) requiere parámetros de cuerpo de solicitud como *signedExpiry*, por lo que no puede usarla dentro de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-137">For example, the [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="8ffc3-138">Para determinar qué tipos de recursos tienen una operación de lista, dispone de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-138">To determine which resource types have a list operation, you have the following options:</span></span>

* <span data-ttu-id="8ffc3-139">Vea las [operaciones de API de REST](/rest/api/) para un proveedor de recursos y busque operaciones List.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-139">View the [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="8ffc3-140">Por ejemplo, las cuentas de almacenamiento tienen una [operación listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="8ffc3-140">For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="8ffc3-141">Utilice el cmdlet de PowerShell [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation).</span><span class="sxs-lookup"><span data-stu-id="8ffc3-141">Use the [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="8ffc3-142">En el ejemplo siguiente se obtienen todas las operaciones List para cuentas de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-142">The following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="8ffc3-143">Use el siguiente comando de la CLI de Azure para filtrar solo las operaciones de la lista:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-143">Use the following Azure CLI command to filter only the list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="8ffc3-144">Especifique el recurso utilizando la [función resourceId](#resourceid) o el formato `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-144">Specify the resource by using either the [resourceId function](#resourceid), or the format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="8ffc3-145">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-145">Example</span></span>

<span data-ttu-id="8ffc3-146">En el ejemplo siguiente se muestra cómo se devuelven las claves principal y secundaria de una cuenta de almacenamiento en la sección de salidas.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-146">The following example shows how to return the primary and secondary keys from a storage account in the outputs section.</span></span>

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

## <a name="providers"></a><span data-ttu-id="8ffc3-147">providers</span><span class="sxs-lookup"><span data-stu-id="8ffc3-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="8ffc3-148">Devuelve información acerca de un proveedor de recursos y sus tipos de recursos admitidos.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="8ffc3-149">Si no proporciona un tipo de recurso, la función devuelve todos los tipos admitidos para el proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-149">If you do not provide a resource type, the function returns all the supported types for the resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="8ffc3-150">parameters</span><span class="sxs-lookup"><span data-stu-id="8ffc3-150">Parameters</span></span>

| <span data-ttu-id="8ffc3-151">Parámetro</span><span class="sxs-lookup"><span data-stu-id="8ffc3-151">Parameter</span></span> | <span data-ttu-id="8ffc3-152">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8ffc3-152">Required</span></span> | <span data-ttu-id="8ffc3-153">Tipo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-153">Type</span></span> | <span data-ttu-id="8ffc3-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="8ffc3-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8ffc3-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="8ffc3-155">providerNamespace</span></span> |<span data-ttu-id="8ffc3-156">Sí</span><span class="sxs-lookup"><span data-stu-id="8ffc3-156">Yes</span></span> |<span data-ttu-id="8ffc3-157">string</span><span class="sxs-lookup"><span data-stu-id="8ffc3-157">string</span></span> |<span data-ttu-id="8ffc3-158">Espacio de nombres del proveedor</span><span class="sxs-lookup"><span data-stu-id="8ffc3-158">Namespace of the provider</span></span> |
| <span data-ttu-id="8ffc3-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="8ffc3-159">resourceType</span></span> |<span data-ttu-id="8ffc3-160">No</span><span class="sxs-lookup"><span data-stu-id="8ffc3-160">No</span></span> |<span data-ttu-id="8ffc3-161">cadena</span><span class="sxs-lookup"><span data-stu-id="8ffc3-161">string</span></span> |<span data-ttu-id="8ffc3-162">El tipo de recurso en el espacio de nombres especificado.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-162">The type of resource within the specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="8ffc3-163">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="8ffc3-163">Return value</span></span>

<span data-ttu-id="8ffc3-164">Se devuelve cada tipo admitido en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-164">Each supported type is returned in the following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="8ffc3-165">No se garantiza el orden de matriz de los valores devueltos.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-165">Array ordering of the returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="8ffc3-166">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-166">Example</span></span>

<span data-ttu-id="8ffc3-167">En el ejemplo siguiente se muestra cómo utilizar la función de proveedor:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-167">The following example shows how to use the provider function:</span></span>

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

<span data-ttu-id="8ffc3-168">El ejemplo anterior devuelve un objeto en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-168">The preceding example returns an object in the following format:</span></span>

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

## <a name="reference"></a><span data-ttu-id="8ffc3-169">reference</span><span class="sxs-lookup"><span data-stu-id="8ffc3-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="8ffc3-170">Devuelve un objeto que representa el estado de tiempo de ejecución de un recurso.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="8ffc3-171">parameters</span><span class="sxs-lookup"><span data-stu-id="8ffc3-171">Parameters</span></span>

| <span data-ttu-id="8ffc3-172">Parámetro</span><span class="sxs-lookup"><span data-stu-id="8ffc3-172">Parameter</span></span> | <span data-ttu-id="8ffc3-173">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8ffc3-173">Required</span></span> | <span data-ttu-id="8ffc3-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-174">Type</span></span> | <span data-ttu-id="8ffc3-175">Descripción</span><span class="sxs-lookup"><span data-stu-id="8ffc3-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8ffc3-176">resourceName o resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="8ffc3-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="8ffc3-177">Sí</span><span class="sxs-lookup"><span data-stu-id="8ffc3-177">Yes</span></span> |<span data-ttu-id="8ffc3-178">string</span><span class="sxs-lookup"><span data-stu-id="8ffc3-178">string</span></span> |<span data-ttu-id="8ffc3-179">Nombre o identificador único de un recurso.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="8ffc3-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8ffc3-180">apiVersion</span></span> |<span data-ttu-id="8ffc3-181">No</span><span class="sxs-lookup"><span data-stu-id="8ffc3-181">No</span></span> |<span data-ttu-id="8ffc3-182">string</span><span class="sxs-lookup"><span data-stu-id="8ffc3-182">string</span></span> |<span data-ttu-id="8ffc3-183">Versión de la API del recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-183">API version of the specified resource.</span></span> <span data-ttu-id="8ffc3-184">Incluya este parámetro cuando el recurso no esté aprovisionado en la misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-184">Include this parameter when the resource is not provisioned within same template.</span></span> <span data-ttu-id="8ffc3-185">Por lo general, en el formato, **aaaa-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-185">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="8ffc3-186">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="8ffc3-186">Return value</span></span>

<span data-ttu-id="8ffc3-187">Cada tipo de recurso devuelve propiedades diferentes para la función de referencia.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-187">Every resource type returns different properties for the reference function.</span></span> <span data-ttu-id="8ffc3-188">La función no devuelve un solo formato predefinido.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-188">The function does not return a single, predefined format.</span></span> <span data-ttu-id="8ffc3-189">Para ver las propiedades de un tipo de recurso, devuelva el objeto en la sección de resultados tal como se muestra en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-189">To see the properties for a resource type, return the object in the outputs section as shown in the example.</span></span>

### <a name="remarks"></a><span data-ttu-id="8ffc3-190">Comentarios</span><span class="sxs-lookup"><span data-stu-id="8ffc3-190">Remarks</span></span>

<span data-ttu-id="8ffc3-191">La función reference deriva su valor desde un estado de tiempo de ejecución y, por tanto, no se puede utilizar en la sección de variables.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-191">The reference function derives its value from a runtime state, and therefore cannot be used in the variables section.</span></span> <span data-ttu-id="8ffc3-192">Se puede utilizar en la sección de salidas de una plantilla.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="8ffc3-193">Mediante el uso de la función de referencia, se declara implícitamente que un recurso depende de otro recurso si el recurso al que se hace referencia se aprovisiona en la misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-193">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template.</span></span> <span data-ttu-id="8ffc3-194">No tiene que usar también la propiedad dependsOn.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-194">You do not need to also use the dependsOn property.</span></span> <span data-ttu-id="8ffc3-195">La función no se evalúa hasta que el recurso al que se hace referencia complete la implementación.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-195">The function is not evaluated until the referenced resource has completed deployment.</span></span>

<span data-ttu-id="8ffc3-196">Para ver los nombres y los valores de propiedad de un tipo de recurso, cree una plantilla que devuelva el objeto en la sección de salidas.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-196">To see the property names and values for a resource type, create a template that returns the object in the outputs section.</span></span> <span data-ttu-id="8ffc3-197">Si tiene un recurso existente de ese tipo, la plantilla devuelve el objeto sin necesidad de implementar los nuevos recursos.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-197">If you have an existing resource of that type, your template returns the object without deploying any new resources.</span></span> 

<span data-ttu-id="8ffc3-198">Normalmente, se usa la función de **referencia** para devolver un valor determinado de un objeto, como el identificador URI del punto de conexión de blob o el nombre de dominio completo.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-198">Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.</span></span>

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

### <a name="example"></a><span data-ttu-id="8ffc3-199">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-199">Example</span></span>

<span data-ttu-id="8ffc3-200">Para implementar y hacer referencia al recurso en la misma plantilla, use:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-200">To deploy and reference the resource in the same template, use:</span></span>

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

<span data-ttu-id="8ffc3-201">El ejemplo anterior devuelve un objeto en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-201">The preceding example returns an object in the following format:</span></span>

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

<span data-ttu-id="8ffc3-202">En el ejemplo siguiente se hace referencia a una cuenta de almacenamiento que no se implementa en esta plantilla.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-202">The following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="8ffc3-203">La cuenta de almacenamiento ya existe dentro del mismo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-203">The storage account already exists within the same resource group.</span></span>

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

## <a name="resourcegroup"></a><span data-ttu-id="8ffc3-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="8ffc3-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="8ffc3-205">Devuelve un objeto que representa el grupo de recursos actual.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-205">Returns an object that represents the current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="8ffc3-206">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="8ffc3-206">Return value</span></span>

<span data-ttu-id="8ffc3-207">El objeto devuelto está en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-207">The returned object is in the following format:</span></span>

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

### <a name="remarks"></a><span data-ttu-id="8ffc3-208">Comentarios</span><span class="sxs-lookup"><span data-stu-id="8ffc3-208">Remarks</span></span>

<span data-ttu-id="8ffc3-209">Un uso común de la función resourceGroup es crear recursos en la misma ubicación que el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-209">A common use of the resourceGroup function is to create resources in the same location as the resource group.</span></span> <span data-ttu-id="8ffc3-210">En el ejemplo siguiente se utiliza la ubicación del grupo de recursos para asignar la ubicación de un sitio web.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-210">The following example uses the resource group location to assign the location for a web site.</span></span>

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

### <a name="example"></a><span data-ttu-id="8ffc3-211">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-211">Example</span></span>

<span data-ttu-id="8ffc3-212">La plantilla siguiente devuelve las propiedades del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-212">The following template returns the properties of the resource group.</span></span>

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

<span data-ttu-id="8ffc3-213">El ejemplo anterior devuelve un objeto en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-213">The preceding example returns an object in the following format:</span></span>

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

## <a name="resourceid"></a><span data-ttu-id="8ffc3-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="8ffc3-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="8ffc3-215">Devuelve el identificador único de un recurso.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-215">Returns the unique identifier of a resource.</span></span> <span data-ttu-id="8ffc3-216">Utilice esta función cuando el nombre del recurso sea ambiguo o no esté aprovisionado dentro de la misma plantilla.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-216">You use this function when the resource name is ambiguous or not provisioned within the same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="8ffc3-217">parameters</span><span class="sxs-lookup"><span data-stu-id="8ffc3-217">Parameters</span></span>

| <span data-ttu-id="8ffc3-218">Parámetro</span><span class="sxs-lookup"><span data-stu-id="8ffc3-218">Parameter</span></span> | <span data-ttu-id="8ffc3-219">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="8ffc3-219">Required</span></span> | <span data-ttu-id="8ffc3-220">Tipo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-220">Type</span></span> | <span data-ttu-id="8ffc3-221">Descripción</span><span class="sxs-lookup"><span data-stu-id="8ffc3-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="8ffc3-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="8ffc3-222">subscriptionId</span></span> |<span data-ttu-id="8ffc3-223">No</span><span class="sxs-lookup"><span data-stu-id="8ffc3-223">No</span></span> |<span data-ttu-id="8ffc3-224">Cadena (en formato de GUID)</span><span class="sxs-lookup"><span data-stu-id="8ffc3-224">string (In GUID format)</span></span> |<span data-ttu-id="8ffc3-225">El valor predeterminado es la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-225">Default value is the current subscription.</span></span> <span data-ttu-id="8ffc3-226">Especifique este valor cuando necesite recuperar un recurso en otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-226">Specify this value when you need to retrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="8ffc3-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="8ffc3-227">resourceGroupName</span></span> |<span data-ttu-id="8ffc3-228">No</span><span class="sxs-lookup"><span data-stu-id="8ffc3-228">No</span></span> |<span data-ttu-id="8ffc3-229">cadena</span><span class="sxs-lookup"><span data-stu-id="8ffc3-229">string</span></span> |<span data-ttu-id="8ffc3-230">El valor predeterminado es el grupo de recursos actual.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-230">Default value is current resource group.</span></span> <span data-ttu-id="8ffc3-231">Especifique este valor cuando necesite recuperar un recurso en otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-231">Specify this value when you need to retrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="8ffc3-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="8ffc3-232">resourceType</span></span> |<span data-ttu-id="8ffc3-233">Sí</span><span class="sxs-lookup"><span data-stu-id="8ffc3-233">Yes</span></span> |<span data-ttu-id="8ffc3-234">string</span><span class="sxs-lookup"><span data-stu-id="8ffc3-234">string</span></span> |<span data-ttu-id="8ffc3-235">Tipo de recurso, incluido el espacio de nombres del proveedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="8ffc3-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="8ffc3-236">resourceName1</span></span> |<span data-ttu-id="8ffc3-237">Sí</span><span class="sxs-lookup"><span data-stu-id="8ffc3-237">Yes</span></span> |<span data-ttu-id="8ffc3-238">cadena</span><span class="sxs-lookup"><span data-stu-id="8ffc3-238">string</span></span> |<span data-ttu-id="8ffc3-239">Nombre del recurso.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-239">Name of resource.</span></span> |
| <span data-ttu-id="8ffc3-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="8ffc3-240">resourceName2</span></span> |<span data-ttu-id="8ffc3-241">No</span><span class="sxs-lookup"><span data-stu-id="8ffc3-241">No</span></span> |<span data-ttu-id="8ffc3-242">string</span><span class="sxs-lookup"><span data-stu-id="8ffc3-242">string</span></span> |<span data-ttu-id="8ffc3-243">Siguiente segmento de nombre de recurso si el recurso está anidado.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="8ffc3-244">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="8ffc3-244">Return value</span></span>

<span data-ttu-id="8ffc3-245">El identificador se devuelve con el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-245">The identifier is returned in the following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="8ffc3-246">Comentarios</span><span class="sxs-lookup"><span data-stu-id="8ffc3-246">Remarks</span></span>

<span data-ttu-id="8ffc3-247">Los valores de parámetro que especifique dependen de si el recurso está en el mismo grupo de recursos y la misma suscripción que la implementación actual.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-247">The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment.</span></span>

<span data-ttu-id="8ffc3-248">Para obtener el identificador de recurso para una cuenta de almacenamiento de la misma suscripción y el mismo grupo de recursos, use:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-248">To get the resource ID for a storage account in the same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="8ffc3-249">Para obtener el identificador de recurso para una cuenta de almacenamiento de la misma suscripción, pero un grupo de recursos diferente, use:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-249">To get the resource ID for a storage account in the same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="8ffc3-250">Para obtener el identificador de recurso para una cuenta de almacenamiento de una suscripción y un grupo de recursos diferente, use:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-250">To get the resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="8ffc3-251">Para obtener el identificador de recurso para una base de datos de un grupo de recursos diferente, use:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-251">To get the resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="8ffc3-252">A menudo, necesitará utilizar esta función cuando se usa una cuenta de almacenamiento o red virtual en un grupo de recursos alternativo.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-252">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="8ffc3-253">En el ejemplo siguiente se muestra cómo un recurso de un grupo de recursos externos se puede utilizar fácilmente:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-253">The following example shows how a resource from an external resource group can easily be used:</span></span>

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

### <a name="example"></a><span data-ttu-id="8ffc3-254">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-254">Example</span></span>

<span data-ttu-id="8ffc3-255">En el ejemplo siguiente se devuelve el identificador de recurso de la cuenta de almacenamiento en el grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-255">The following example returns the resource ID for a storage account in the resource group:</span></span>

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

<span data-ttu-id="8ffc3-256">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-256">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="8ffc3-257">Nombre</span><span class="sxs-lookup"><span data-stu-id="8ffc3-257">Name</span></span> | <span data-ttu-id="8ffc3-258">Tipo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-258">Type</span></span> | <span data-ttu-id="8ffc3-259">Valor</span><span class="sxs-lookup"><span data-stu-id="8ffc3-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="8ffc3-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="8ffc3-260">sameRGOutput</span></span> | <span data-ttu-id="8ffc3-261">String</span><span class="sxs-lookup"><span data-stu-id="8ffc3-261">String</span></span> | <span data-ttu-id="8ffc3-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="8ffc3-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="8ffc3-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="8ffc3-263">differentRGOutput</span></span> | <span data-ttu-id="8ffc3-264">String</span><span class="sxs-lookup"><span data-stu-id="8ffc3-264">String</span></span> | <span data-ttu-id="8ffc3-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="8ffc3-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="8ffc3-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="8ffc3-266">differentSubOutput</span></span> | <span data-ttu-id="8ffc3-267">String</span><span class="sxs-lookup"><span data-stu-id="8ffc3-267">String</span></span> | <span data-ttu-id="8ffc3-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="8ffc3-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="8ffc3-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="8ffc3-269">nestedResourceOutput</span></span> | <span data-ttu-id="8ffc3-270">String</span><span class="sxs-lookup"><span data-stu-id="8ffc3-270">String</span></span> | <span data-ttu-id="8ffc3-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="8ffc3-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="8ffc3-272">suscripción</span><span class="sxs-lookup"><span data-stu-id="8ffc3-272">subscription</span></span>
`subscription()`

<span data-ttu-id="8ffc3-273">Devuelve detalles sobre la suscripción para la implementación actual.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-273">Returns details about the subscription for the current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="8ffc3-274">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="8ffc3-274">Return value</span></span>

<span data-ttu-id="8ffc3-275">La función devuelve el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="8ffc3-275">The function returns the following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="8ffc3-276">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8ffc3-276">Example</span></span>

<span data-ttu-id="8ffc3-277">En el ejemplo siguiente se muestra la función de suscripción a la que se llama en la sección de salidas.</span><span class="sxs-lookup"><span data-stu-id="8ffc3-277">The following example shows the subscription function called in the outputs section.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="8ffc3-278">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8ffc3-278">Next steps</span></span>
* <span data-ttu-id="8ffc3-279">Para obtener una descripción de las secciones de una plantilla de Azure Resource Manager, vea [Creación de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8ffc3-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8ffc3-280">Para combinar varias plantillas, vea [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8ffc3-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="8ffc3-281">Para iterar una cantidad de veces específica al crear un tipo de recurso, vea [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8ffc3-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="8ffc3-282">Para saber cómo implementar la plantilla que creó, consulte [Implementación de una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8ffc3-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

