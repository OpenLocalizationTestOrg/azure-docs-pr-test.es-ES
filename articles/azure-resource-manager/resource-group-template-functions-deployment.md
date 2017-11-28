---
title: "Funciones de la plantilla de Azure Resource Manager: implementación | Microsoft Docs"
description: "Describe las funciones para usar en una plantilla de Azure Resource Manager para recuperar información de implementación."
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
ms.openlocfilehash: d7e6bcd669d40cb19de44b646505856ecd8f51a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="ff94c-103">Funciones de implementación para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ff94c-103">Deployment functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="ff94c-104">El Administrador de recursos ofrece las siguientes funciones para obtener valores de las secciones de la plantilla y valores relacionados con la implementación:</span><span class="sxs-lookup"><span data-stu-id="ff94c-104">Resource Manager provides the following functions for getting values from sections of the template and values related to the deployment:</span></span>

* [<span data-ttu-id="ff94c-105">deployment</span><span class="sxs-lookup"><span data-stu-id="ff94c-105">deployment</span></span>](#deployment)
* [<span data-ttu-id="ff94c-106">parameters</span><span class="sxs-lookup"><span data-stu-id="ff94c-106">parameters</span></span>](#parameters)
* [<span data-ttu-id="ff94c-107">variables</span><span class="sxs-lookup"><span data-stu-id="ff94c-107">variables</span></span>](#variables)

<span data-ttu-id="ff94c-108">Para obtener valores de recursos, grupos de recursos o suscripciones, consulte [Funciones de recursos](resource-group-template-functions-resource.md).</span><span class="sxs-lookup"><span data-stu-id="ff94c-108">To get values from resources, resource groups, or subscriptions, see [Resource functions](resource-group-template-functions-resource.md).</span></span>

<a id="deployment" />

## <a name="deployment"></a><span data-ttu-id="ff94c-109">deployment</span><span class="sxs-lookup"><span data-stu-id="ff94c-109">deployment</span></span>
`deployment()`

<span data-ttu-id="ff94c-110">Devuelve información sobre la operación de implementación actual.</span><span class="sxs-lookup"><span data-stu-id="ff94c-110">Returns information about the current deployment operation.</span></span>

### <a name="return-value"></a><span data-ttu-id="ff94c-111">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ff94c-111">Return value</span></span>

<span data-ttu-id="ff94c-112">Esta función devuelve el objeto pasado durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="ff94c-112">This function returns the object that is passed during deployment.</span></span> <span data-ttu-id="ff94c-113">Las propiedades del objeto devuelto varían en función de si el objeto de implementación se ha pasado como un vínculo o como un objeto en línea.</span><span class="sxs-lookup"><span data-stu-id="ff94c-113">The properties in the returned object differ based on whether the deployment object is passed as a link or as an in-line object.</span></span> <span data-ttu-id="ff94c-114">Cuando se pasa el objeto de implementación en línea, como cuando se usa el parámetro **-TemplateFile** en Azure PowerShell para orientarlo a un archivo local, el objeto devuelto tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="ff94c-114">When the deployment object is passed in-line, such as when using the **-TemplateFile** parameter in Azure PowerShell to point to a local file, the returned object has the following format:</span></span>

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

<span data-ttu-id="ff94c-115">Cuando el objeto se pasa como un vínculo, como cuando se usa el parámetro **-TemplateUri** para orientarlo a un objeto remoto, se devuelve el objeto en el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="ff94c-115">When the object is passed as a link, such as when using the **-TemplateUri** parameter to point to a remote object, the object is returned in the following format:</span></span> 

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

### <a name="remarks"></a><span data-ttu-id="ff94c-116">Comentarios</span><span class="sxs-lookup"><span data-stu-id="ff94c-116">Remarks</span></span>

<span data-ttu-id="ff94c-117">Puede usar deployment() para establecer un vínculo con otra plantilla basada en el identificador URI de la plantilla primaria.</span><span class="sxs-lookup"><span data-stu-id="ff94c-117">You can use deployment() to link to another template based on the URI of the parent template.</span></span>

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a><span data-ttu-id="ff94c-118">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ff94c-118">Example</span></span>

<span data-ttu-id="ff94c-119">El ejemplo siguiente devuelve el objeto de implementación:</span><span class="sxs-lookup"><span data-stu-id="ff94c-119">The following example returns the deployment object:</span></span>

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

<span data-ttu-id="ff94c-120">El ejemplo anterior devuelve el objeto siguiente:</span><span class="sxs-lookup"><span data-stu-id="ff94c-120">The preceding example returns the following object:</span></span>

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

## <a name="parameters"></a><span data-ttu-id="ff94c-121">parameters</span><span class="sxs-lookup"><span data-stu-id="ff94c-121">parameters</span></span>
`parameters(parameterName)`

<span data-ttu-id="ff94c-122">Devuelve un valor de parámetro.</span><span class="sxs-lookup"><span data-stu-id="ff94c-122">Returns a parameter value.</span></span> <span data-ttu-id="ff94c-123">El nombre del parámetro especificado debe definirse en la sección de parámetros de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ff94c-123">The specified parameter name must be defined in the parameters section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff94c-124">parameters</span><span class="sxs-lookup"><span data-stu-id="ff94c-124">Parameters</span></span>

| <span data-ttu-id="ff94c-125">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ff94c-125">Parameter</span></span> | <span data-ttu-id="ff94c-126">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ff94c-126">Required</span></span> | <span data-ttu-id="ff94c-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="ff94c-127">Type</span></span> | <span data-ttu-id="ff94c-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="ff94c-128">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ff94c-129">parameterName</span><span class="sxs-lookup"><span data-stu-id="ff94c-129">parameterName</span></span> |<span data-ttu-id="ff94c-130">Sí</span><span class="sxs-lookup"><span data-stu-id="ff94c-130">Yes</span></span> |<span data-ttu-id="ff94c-131">cadena</span><span class="sxs-lookup"><span data-stu-id="ff94c-131">string</span></span> |<span data-ttu-id="ff94c-132">El nombre del parámetro que se va a devolver.</span><span class="sxs-lookup"><span data-stu-id="ff94c-132">The name of the parameter to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ff94c-133">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ff94c-133">Return value</span></span>

<span data-ttu-id="ff94c-134">Valor del parámetro especificado.</span><span class="sxs-lookup"><span data-stu-id="ff94c-134">The value of the specified parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="ff94c-135">Comentarios</span><span class="sxs-lookup"><span data-stu-id="ff94c-135">Remarks</span></span>

<span data-ttu-id="ff94c-136">Por lo general, se usan parámetros para establecer los valores de recurso.</span><span class="sxs-lookup"><span data-stu-id="ff94c-136">Typically, you use parameters to set resource values.</span></span> <span data-ttu-id="ff94c-137">En el ejemplo siguiente se establece el nombre del sitio web en el valor del parámetro pasado durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="ff94c-137">The following example sets the name of web site to the parameter value passed in during deployment.</span></span>

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

### <a name="example"></a><span data-ttu-id="ff94c-138">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ff94c-138">Example</span></span>

<span data-ttu-id="ff94c-139">En el ejemplo siguiente se muestra un uso simplificado de la función de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="ff94c-139">The following example shows a simplified use of the parameters function.</span></span>

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

<span data-ttu-id="ff94c-140">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="ff94c-140">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="ff94c-141">Nombre</span><span class="sxs-lookup"><span data-stu-id="ff94c-141">Name</span></span> | <span data-ttu-id="ff94c-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="ff94c-142">Type</span></span> | <span data-ttu-id="ff94c-143">Valor</span><span class="sxs-lookup"><span data-stu-id="ff94c-143">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ff94c-144">stringOutput</span><span class="sxs-lookup"><span data-stu-id="ff94c-144">stringOutput</span></span> | <span data-ttu-id="ff94c-145">String</span><span class="sxs-lookup"><span data-stu-id="ff94c-145">String</span></span> | <span data-ttu-id="ff94c-146">opción 1</span><span class="sxs-lookup"><span data-stu-id="ff94c-146">option 1</span></span> |
| <span data-ttu-id="ff94c-147">intOutput</span><span class="sxs-lookup"><span data-stu-id="ff94c-147">intOutput</span></span> | <span data-ttu-id="ff94c-148">int</span><span class="sxs-lookup"><span data-stu-id="ff94c-148">Int</span></span> | <span data-ttu-id="ff94c-149">1</span><span class="sxs-lookup"><span data-stu-id="ff94c-149">1</span></span> |
| <span data-ttu-id="ff94c-150">objectOutput</span><span class="sxs-lookup"><span data-stu-id="ff94c-150">objectOutput</span></span> | <span data-ttu-id="ff94c-151">Objeto</span><span class="sxs-lookup"><span data-stu-id="ff94c-151">Object</span></span> | <span data-ttu-id="ff94c-152">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="ff94c-152">{"one": "a", "two": "b"}</span></span> |
| <span data-ttu-id="ff94c-153">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="ff94c-153">arrayOutput</span></span> | <span data-ttu-id="ff94c-154">Matriz</span><span class="sxs-lookup"><span data-stu-id="ff94c-154">Array</span></span> | <span data-ttu-id="ff94c-155">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="ff94c-155">[1, 2, 3]</span></span> |
| <span data-ttu-id="ff94c-156">crossOutput</span><span class="sxs-lookup"><span data-stu-id="ff94c-156">crossOutput</span></span> | <span data-ttu-id="ff94c-157">String</span><span class="sxs-lookup"><span data-stu-id="ff94c-157">String</span></span> | <span data-ttu-id="ff94c-158">opción 1</span><span class="sxs-lookup"><span data-stu-id="ff94c-158">option 1</span></span> |

<a id="variables" />

## <a name="variables"></a><span data-ttu-id="ff94c-159">variables</span><span class="sxs-lookup"><span data-stu-id="ff94c-159">variables</span></span>
`variables(variableName)`

<span data-ttu-id="ff94c-160">Devuelve el valor de variable.</span><span class="sxs-lookup"><span data-stu-id="ff94c-160">Returns the value of variable.</span></span> <span data-ttu-id="ff94c-161">El nombre de la variable especificada debe definirse en la sección de variables de la plantilla.</span><span class="sxs-lookup"><span data-stu-id="ff94c-161">The specified variable name must be defined in the variables section of the template.</span></span>

### <a name="parameters"></a><span data-ttu-id="ff94c-162">parameters</span><span class="sxs-lookup"><span data-stu-id="ff94c-162">Parameters</span></span>

| <span data-ttu-id="ff94c-163">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ff94c-163">Parameter</span></span> | <span data-ttu-id="ff94c-164">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ff94c-164">Required</span></span> | <span data-ttu-id="ff94c-165">Tipo</span><span class="sxs-lookup"><span data-stu-id="ff94c-165">Type</span></span> | <span data-ttu-id="ff94c-166">Descripción</span><span class="sxs-lookup"><span data-stu-id="ff94c-166">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ff94c-167">variableName</span><span class="sxs-lookup"><span data-stu-id="ff94c-167">variableName</span></span> |<span data-ttu-id="ff94c-168">Sí</span><span class="sxs-lookup"><span data-stu-id="ff94c-168">Yes</span></span> |<span data-ttu-id="ff94c-169">string</span><span class="sxs-lookup"><span data-stu-id="ff94c-169">String</span></span> |<span data-ttu-id="ff94c-170">El nombre de la variable que se va a devolver.</span><span class="sxs-lookup"><span data-stu-id="ff94c-170">The name of the variable to return.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ff94c-171">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ff94c-171">Return value</span></span>

<span data-ttu-id="ff94c-172">Valor de la variable especificada.</span><span class="sxs-lookup"><span data-stu-id="ff94c-172">The value of the specified variable.</span></span>

### <a name="remarks"></a><span data-ttu-id="ff94c-173">Comentarios</span><span class="sxs-lookup"><span data-stu-id="ff94c-173">Remarks</span></span>

<span data-ttu-id="ff94c-174">Por lo general, para simplificar la plantilla se usan variables para crear valores complejos de una sola vez.</span><span class="sxs-lookup"><span data-stu-id="ff94c-174">Typically, you use variables to simplify your template by constructing complex values only once.</span></span> <span data-ttu-id="ff94c-175">En el ejemplo siguiente se crea un nombre único para una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ff94c-175">The following example constructs a unique name for a storage account.</span></span>

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

### <a name="example"></a><span data-ttu-id="ff94c-176">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ff94c-176">Example</span></span>

<span data-ttu-id="ff94c-177">La plantilla de ejemplo devuelve distintos valores de variable.</span><span class="sxs-lookup"><span data-stu-id="ff94c-177">The example template returns different variable values.</span></span>

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

<span data-ttu-id="ff94c-178">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="ff94c-178">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="ff94c-179">Nombre</span><span class="sxs-lookup"><span data-stu-id="ff94c-179">Name</span></span> | <span data-ttu-id="ff94c-180">Tipo</span><span class="sxs-lookup"><span data-stu-id="ff94c-180">Type</span></span> | <span data-ttu-id="ff94c-181">Valor</span><span class="sxs-lookup"><span data-stu-id="ff94c-181">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ff94c-182">exampleOutput1</span><span class="sxs-lookup"><span data-stu-id="ff94c-182">exampleOutput1</span></span> | <span data-ttu-id="ff94c-183">String</span><span class="sxs-lookup"><span data-stu-id="ff94c-183">String</span></span> | <span data-ttu-id="ff94c-184">myVariable</span><span class="sxs-lookup"><span data-stu-id="ff94c-184">myVariable</span></span> |
| <span data-ttu-id="ff94c-185">exampleOutput2</span><span class="sxs-lookup"><span data-stu-id="ff94c-185">exampleOutput2</span></span> | <span data-ttu-id="ff94c-186">Matriz</span><span class="sxs-lookup"><span data-stu-id="ff94c-186">Array</span></span> | <span data-ttu-id="ff94c-187">[1, 2, 3, 4]</span><span class="sxs-lookup"><span data-stu-id="ff94c-187">[1, 2, 3, 4]</span></span> |
| <span data-ttu-id="ff94c-188">exampleOutput3</span><span class="sxs-lookup"><span data-stu-id="ff94c-188">exampleOutput3</span></span> | <span data-ttu-id="ff94c-189">String</span><span class="sxs-lookup"><span data-stu-id="ff94c-189">String</span></span> | <span data-ttu-id="ff94c-190">myVariable</span><span class="sxs-lookup"><span data-stu-id="ff94c-190">myVariable</span></span> |
| <span data-ttu-id="ff94c-191">exampleOutput4</span><span class="sxs-lookup"><span data-stu-id="ff94c-191">exampleOutput4</span></span> |  <span data-ttu-id="ff94c-192">Objeto</span><span class="sxs-lookup"><span data-stu-id="ff94c-192">Object</span></span> | <span data-ttu-id="ff94c-193">{"property1": "value1", "property2": "value2"}</span><span class="sxs-lookup"><span data-stu-id="ff94c-193">{"property1": "value1", "property2": "value2"}</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff94c-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ff94c-194">Next steps</span></span>
* <span data-ttu-id="ff94c-195">Para obtener una descripción de las secciones de una plantilla de Azure Resource Manager, vea [Creación de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ff94c-195">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="ff94c-196">Para combinar varias plantillas, vea [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ff94c-196">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="ff94c-197">Para iterar una cantidad de veces específica al crear un tipo de recurso, vea [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="ff94c-197">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="ff94c-198">Para saber cómo implementar la plantilla que creó, consulte [Implementación de una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ff94c-198">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

