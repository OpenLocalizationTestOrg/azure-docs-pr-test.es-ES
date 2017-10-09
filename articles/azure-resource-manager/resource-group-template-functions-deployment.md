---
title: funciones de plantilla de administrador de recursos de aaaAzure - deployment | Documentos de Microsoft
description: "Describe hello toouse de funciones en una información de la implementación de la plantilla tooretrieve Azure Resource Manager."
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
ms.date: 06/13/2017
ms.author: tomfitz
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="3d8d5-103">Funciones de implementación para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3d8d5-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="3d8d5-104">Administrador de recursos proporciona siguiente hello las funciones para obtener los valores de las secciones de plantilla de Hola y los valores relacionados toohello implementación:</span><span class="sxs-lookup"><span data-stu-id="3d8d5-104">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="3d8d5-105">deployment</span><span class="sxs-lookup"><span data-stu-id="3d8d5-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="3d8d5-106">parameters</span><span class="sxs-lookup"><span data-stu-id="3d8d5-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="3d8d5-107">variables</span><span class="sxs-lookup"><span data-stu-id="3d8d5-107">variables</span></span>](#variables)

<span data-ttu-id="3d8d5-108">valores de tooget de recursos, grupos de recursos o suscripciones, vea [las funciones de recursos](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="3d8d5-108">tooget values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="3d8d5-109">deployment</span><span class="sxs-lookup"><span data-stu-id="3d8d5-109">deployment</span></span>
`deployment()`

<span data-ttu-id="3d8d5-110">Devuelve información acerca de la operación de implementación actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-110">Returns information about hello current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="3d8d5-111">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="3d8d5-111">Return value</span></span>

<span data-ttu-id="3d8d5-112">Esta función devuelve el objeto de Hola que se pasa durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-112">This function returns hello object that is passed during deployment.</span></span> <span data-ttu-id="3d8d5-113">propiedades de Hola Hola devolvió objeto varían en función de si hello implementación objeto se pasa como un vínculo o como un objeto en línea.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-113">hello properties in hello returned object differ based on whether hello deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="3d8d5-114">Cuando se pasa el objeto de implementación de hello en línea, como cuando se usa hello **- TemplateFile** parámetro en el archivo local de Azure PowerShell toopoint tooa, Hola devuelve objeto tiene Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="3d8d5-114">When hello deployment object is passed in-line, such as when using hello **-TemplateFile** parameter in Azure PowerShell toopoint tooa local file, hello returned object has hello following format:</span></span>

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

<span data-ttu-id="3d8d5-115">Cuando se pasa el objeto de Hola como un vínculo, como al usar Hola **TemplateUri -** parámetro toopoint tooa remoto del objeto, se devuelve el objeto de Hola Hola siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="3d8d5-115">When hello object is passed as a link, such as when using hello **-TemplateUri** parameter toopoint tooa remote object, hello object is returned in hello following format:</span></span> 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a><span data-ttu-id="3d8d5-116">Comentarios</span><span class="sxs-lookup"><span data-stu-id="3d8d5-116">Remarks</span></span>

<span data-ttu-id="3d8d5-117">Puede usar deployment() toolink tooanother plantilla basado en el URI de la plantilla principal de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-117">You can use deployment() toolink tooanother template based on hello URI of hello parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="3d8d5-118">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3d8d5-118">Example</span></span>

<span data-ttu-id="3d8d5-119">Hello en el ejemplo siguiente se devuelve el objeto de implementación de hello:</span><span class="sxs-lookup"><span data-stu-id="3d8d5-119">hello following example returns hello deployment object:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="3d8d5-120">Hello en el ejemplo anterior se devuelve Hola después de objeto:</span><span class="sxs-lookup"><span data-stu-id="3d8d5-120">hello preceding example returns hello following object:</span></span>

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a><span data-ttu-id="3d8d5-121">parameters</span><span class="sxs-lookup"><span data-stu-id="3d8d5-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="3d8d5-122">Devuelve un valor de parámetro.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-122">Returns a parameter value.</span></span> <span data-ttu-id="3d8d5-123">nombre de parámetro especificado de Hello debe definirse en la sección de parámetros de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-123">hello specified parameter name must be defined in hello parameters section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="3d8d5-124">parameters</span><span class="sxs-lookup"><span data-stu-id="3d8d5-124">Parameters</span></span>

| <span data-ttu-id="3d8d5-125">Parámetro</span><span class="sxs-lookup"><span data-stu-id="3d8d5-125">Parameter</span></span> | <span data-ttu-id="3d8d5-126">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="3d8d5-126">Required</span></span> | <span data-ttu-id="3d8d5-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d8d5-127">Type</span></span> | <span data-ttu-id="3d8d5-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="3d8d5-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3d8d5-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="3d8d5-129">parameterName</span></span> |<span data-ttu-id="3d8d5-130">Sí</span><span class="sxs-lookup"><span data-stu-id="3d8d5-130">Yes</span></span> |<span data-ttu-id="3d8d5-131">cadena</span><span class="sxs-lookup"><span data-stu-id="3d8d5-131">string</span></span> |<span data-ttu-id="3d8d5-132">nombre de Hola de hello parámetro tooreturn.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-132">hello name of hello parameter tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3d8d5-133">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="3d8d5-133">Return value</span></span>

<span data-ttu-id="3d8d5-134">valor de Hola de hello parámetro especifica.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-134">hello value of hello specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="3d8d5-135">Comentarios</span><span class="sxs-lookup"><span data-stu-id="3d8d5-135">Remarks</span></span>

<span data-ttu-id="3d8d5-136">Por lo general, utilice valores de parámetros tooset recursos.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-136">Typically, you use parameters tooset resource values.</span></span> <span data-ttu-id="3d8d5-137">Hello en el ejemplo siguiente se establece Hola nombre del valor de parámetro de sitio web toohello pasado durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-137">hello following example sets hello name of web site toohello parameter value passed in during deployment.</span></span>

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="3d8d5-138">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3d8d5-138">Example</span></span>

<span data-ttu-id="3d8d5-139">Hello en el ejemplo siguiente se muestra un uso simplificado de función de parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-139">hello following example shows a simplified use of hello parameters function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="3d8d5-140">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="3d8d5-140">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="3d8d5-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="3d8d5-141">Name</span></span> | <span data-ttu-id="3d8d5-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d8d5-142">Type</span></span> | <span data-ttu-id="3d8d5-143">Valor</span><span class="sxs-lookup"><span data-stu-id="3d8d5-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3d8d5-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="3d8d5-144">stringOutput</span></span> | <span data-ttu-id="3d8d5-145">String</span><span class="sxs-lookup"><span data-stu-id="3d8d5-145">String</span></span> | <span data-ttu-id="3d8d5-146">opción 1</span><span class="sxs-lookup"><span data-stu-id="3d8d5-146">option 1</span></span> |
| <span data-ttu-id="3d8d5-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="3d8d5-147">intOutput</span></span> | <span data-ttu-id="3d8d5-148">int</span><span class="sxs-lookup"><span data-stu-id="3d8d5-148">Int</span></span> | <span data-ttu-id="3d8d5-149">1</span><span class="sxs-lookup"><span data-stu-id="3d8d5-149">1</span></span> |
| <span data-ttu-id="3d8d5-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="3d8d5-150">objectOutput</span></span> | <span data-ttu-id="3d8d5-151">Objeto</span><span class="sxs-lookup"><span data-stu-id="3d8d5-151">Object</span></span> | <span data-ttu-id="3d8d5-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="3d8d5-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="3d8d5-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="3d8d5-153">arrayOutput</span></span> | <span data-ttu-id="3d8d5-154">Matriz</span><span class="sxs-lookup"><span data-stu-id="3d8d5-154">Array</span></span> | <span data-ttu-id="3d8d5-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="3d8d5-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="3d8d5-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="3d8d5-156">crossOutput</span></span> | <span data-ttu-id="3d8d5-157">String</span><span class="sxs-lookup"><span data-stu-id="3d8d5-157">String</span></span> | <span data-ttu-id="3d8d5-158">opción 1</span><span class="sxs-lookup"><span data-stu-id="3d8d5-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="3d8d5-159">variables</span><span class="sxs-lookup"><span data-stu-id="3d8d5-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="3d8d5-160">Devuelve Hola valor de variable.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-160">Returns hello value of variable.</span></span> <span data-ttu-id="3d8d5-161">nombre de variable especificado Hola debe definirse en la sección de variables de Hola de plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-161">hello specified variable name must be defined in hello variables section of hello template.</span></span>

### <a name="parameters"></a><span data-ttu-id="3d8d5-162">parameters</span><span class="sxs-lookup"><span data-stu-id="3d8d5-162">Parameters</span></span>

| <span data-ttu-id="3d8d5-163">Parámetro</span><span class="sxs-lookup"><span data-stu-id="3d8d5-163">Parameter</span></span> | <span data-ttu-id="3d8d5-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="3d8d5-164">Required</span></span> | <span data-ttu-id="3d8d5-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d8d5-165">Type</span></span> | <span data-ttu-id="3d8d5-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="3d8d5-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3d8d5-167">variableName</span><span class="sxs-lookup"><span data-stu-id="3d8d5-167">variableName</span></span> |<span data-ttu-id="3d8d5-168">Sí</span><span class="sxs-lookup"><span data-stu-id="3d8d5-168">Yes</span></span> |<span data-ttu-id="3d8d5-169">String</span><span class="sxs-lookup"><span data-stu-id="3d8d5-169">String</span></span> |<span data-ttu-id="3d8d5-170">nombre de Hola de hello variable tooreturn.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-170">hello name of hello variable tooreturn.</span></span> |

### <a name="return-value"></a><span data-ttu-id="3d8d5-171">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="3d8d5-171">Return value</span></span>

<span data-ttu-id="3d8d5-172">valor de Hola de variable especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-172">hello value of hello specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="3d8d5-173">Comentarios</span><span class="sxs-lookup"><span data-stu-id="3d8d5-173">Remarks</span></span>

<span data-ttu-id="3d8d5-174">Normalmente, se usa variables toosimplify la plantilla mediante la creación de una sola vez valores complejos.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-174">Typically, you use variables toosimplify your template by constructing complex values only once.</span></span> <span data-ttu-id="3d8d5-175">Hello en el ejemplo siguiente se crea un nombre único para una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-175">hello following example constructs a unique name for a storage account.</span></span>

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a><span data-ttu-id="3d8d5-176">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3d8d5-176">Example</span></span>

<span data-ttu-id="3d8d5-177">plantilla de ejemplo de Hola devuelve distintos valores de variable.</span><span class="sxs-lookup"><span data-stu-id="3d8d5-177">hello example template returns different variable values.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="3d8d5-178">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="3d8d5-178">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="3d8d5-179">Nombre</span><span class="sxs-lookup"><span data-stu-id="3d8d5-179">Name</span></span> | <span data-ttu-id="3d8d5-180">Tipo</span><span class="sxs-lookup"><span data-stu-id="3d8d5-180">Type</span></span> | <span data-ttu-id="3d8d5-181">Valor</span><span class="sxs-lookup"><span data-stu-id="3d8d5-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="3d8d5-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="3d8d5-182">exampleOutput1</span></span> | <span data-ttu-id="3d8d5-183">String</span><span class="sxs-lookup"><span data-stu-id="3d8d5-183">String</span></span> | <span data-ttu-id="3d8d5-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="3d8d5-184">myVariable</span></span> |
| <span data-ttu-id="3d8d5-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="3d8d5-185">exampleOutput2</span></span> | <span data-ttu-id="3d8d5-186">Matriz</span><span class="sxs-lookup"><span data-stu-id="3d8d5-186">Array</span></span> | <span data-ttu-id="3d8d5-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="3d8d5-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="3d8d5-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="3d8d5-188">exampleOutput3</span></span> | <span data-ttu-id="3d8d5-189">String</span><span class="sxs-lookup"><span data-stu-id="3d8d5-189">String</span></span> | <span data-ttu-id="3d8d5-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="3d8d5-190">myVariable</span></span> |
| <span data-ttu-id="3d8d5-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="3d8d5-191">exampleOutput4</span></span> |  <span data-ttu-id="3d8d5-192">Objeto</span><span class="sxs-lookup"><span data-stu-id="3d8d5-192">Object</span></span> | <span data-ttu-id="3d8d5-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="3d8d5-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3d8d5-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3d8d5-194">Next steps</span></span>
* <span data-ttu-id="3d8d5-195">Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3d8d5-195">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3d8d5-196">toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3d8d5-196">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="3d8d5-197">tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3d8d5-197">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="3d8d5-198">toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3d8d5-198">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

