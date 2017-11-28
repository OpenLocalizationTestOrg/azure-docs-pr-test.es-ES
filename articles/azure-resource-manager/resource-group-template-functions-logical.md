---
title: "Funciones lógicas de la plantilla de Azure Resource Manager | Microsoft Docs"
description: "Describe las funciones que se pueden usar en una plantilla de Azure Resource Manager para determinar valores lógicos."
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
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: 313601ad99cdc12c4b50f5469959d37a9fa70d35
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="0844e-103">Funciones lógicas para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0844e-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="0844e-104">Resource Manager proporciona varias funciones para realizar comparaciones en las plantillas.</span><span class="sxs-lookup"><span data-stu-id="0844e-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="0844e-105">and</span><span class="sxs-lookup"><span data-stu-id="0844e-105">and</span></span>](#and)
* [<span data-ttu-id="0844e-106">bool</span><span class="sxs-lookup"><span data-stu-id="0844e-106">bool</span></span>](#bool)
* [<span data-ttu-id="0844e-107">if</span><span class="sxs-lookup"><span data-stu-id="0844e-107">if</span></span>](#if)
* [<span data-ttu-id="0844e-108">not</span><span class="sxs-lookup"><span data-stu-id="0844e-108">not</span></span>](#not)
* [<span data-ttu-id="0844e-109">or</span><span class="sxs-lookup"><span data-stu-id="0844e-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="0844e-110">y</span><span class="sxs-lookup"><span data-stu-id="0844e-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="0844e-111">Comprueba si los dos valores de parámetro son verdaderos.</span><span class="sxs-lookup"><span data-stu-id="0844e-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="0844e-112">parameters</span><span class="sxs-lookup"><span data-stu-id="0844e-112">Parameters</span></span>

| <span data-ttu-id="0844e-113">Parámetro</span><span class="sxs-lookup"><span data-stu-id="0844e-113">Parameter</span></span> | <span data-ttu-id="0844e-114">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0844e-114">Required</span></span> | <span data-ttu-id="0844e-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-115">Type</span></span> | <span data-ttu-id="0844e-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="0844e-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0844e-117">arg1</span><span class="sxs-lookup"><span data-stu-id="0844e-117">arg1</span></span> |<span data-ttu-id="0844e-118">Sí</span><span class="sxs-lookup"><span data-stu-id="0844e-118">Yes</span></span> |<span data-ttu-id="0844e-119">boolean</span><span class="sxs-lookup"><span data-stu-id="0844e-119">boolean</span></span> |<span data-ttu-id="0844e-120">Primer valor cuya veracidad se comprueba.</span><span class="sxs-lookup"><span data-stu-id="0844e-120">The first value to check whether is true.</span></span> |
| <span data-ttu-id="0844e-121">arg2</span><span class="sxs-lookup"><span data-stu-id="0844e-121">arg2</span></span> |<span data-ttu-id="0844e-122">Sí</span><span class="sxs-lookup"><span data-stu-id="0844e-122">Yes</span></span> |<span data-ttu-id="0844e-123">boolean</span><span class="sxs-lookup"><span data-stu-id="0844e-123">boolean</span></span> |<span data-ttu-id="0844e-124">Segundo valor cuya veracidad se comprueba.</span><span class="sxs-lookup"><span data-stu-id="0844e-124">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="0844e-125">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="0844e-125">Return value</span></span>

<span data-ttu-id="0844e-126">Devuelve **True** si ambos valores son verdaderos; en caso contrario, devuelve **False**.</span><span class="sxs-lookup"><span data-stu-id="0844e-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="0844e-127">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="0844e-127">Examples</span></span>

<span data-ttu-id="0844e-128">En el ejemplo siguiente se muestra cómo usar las funciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="0844e-128">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="0844e-129">El resultado del ejemplo anterior es:</span><span class="sxs-lookup"><span data-stu-id="0844e-129">The output from the preceding example is:</span></span>

| <span data-ttu-id="0844e-130">Nombre</span><span class="sxs-lookup"><span data-stu-id="0844e-130">Name</span></span> | <span data-ttu-id="0844e-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-131">Type</span></span> | <span data-ttu-id="0844e-132">Valor</span><span class="sxs-lookup"><span data-stu-id="0844e-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="0844e-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-133">andExampleOutput</span></span> | <span data-ttu-id="0844e-134">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-134">Bool</span></span> | <span data-ttu-id="0844e-135">False</span><span class="sxs-lookup"><span data-stu-id="0844e-135">False</span></span> |
| <span data-ttu-id="0844e-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-136">orExampleOutput</span></span> | <span data-ttu-id="0844e-137">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-137">Bool</span></span> | <span data-ttu-id="0844e-138">True</span><span class="sxs-lookup"><span data-stu-id="0844e-138">True</span></span> |
| <span data-ttu-id="0844e-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-139">notExampleOutput</span></span> | <span data-ttu-id="0844e-140">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-140">Bool</span></span> | <span data-ttu-id="0844e-141">False</span><span class="sxs-lookup"><span data-stu-id="0844e-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="0844e-142">booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="0844e-143">Convierte el parámetro en un booleano.</span><span class="sxs-lookup"><span data-stu-id="0844e-143">Converts the parameter to a boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="0844e-144">parameters</span><span class="sxs-lookup"><span data-stu-id="0844e-144">Parameters</span></span>

| <span data-ttu-id="0844e-145">Parámetro</span><span class="sxs-lookup"><span data-stu-id="0844e-145">Parameter</span></span> | <span data-ttu-id="0844e-146">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0844e-146">Required</span></span> | <span data-ttu-id="0844e-147">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-147">Type</span></span> | <span data-ttu-id="0844e-148">Descripción</span><span class="sxs-lookup"><span data-stu-id="0844e-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0844e-149">arg1</span><span class="sxs-lookup"><span data-stu-id="0844e-149">arg1</span></span> |<span data-ttu-id="0844e-150">Sí</span><span class="sxs-lookup"><span data-stu-id="0844e-150">Yes</span></span> |<span data-ttu-id="0844e-151">cadena o entero</span><span class="sxs-lookup"><span data-stu-id="0844e-151">string or int</span></span> |<span data-ttu-id="0844e-152">El valor para convertir en booleano.</span><span class="sxs-lookup"><span data-stu-id="0844e-152">The value to convert to a boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="0844e-153">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="0844e-153">Return value</span></span>
<span data-ttu-id="0844e-154">Valor booleano del valor convertido.</span><span class="sxs-lookup"><span data-stu-id="0844e-154">A boolean of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="0844e-155">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="0844e-155">Examples</span></span>

<span data-ttu-id="0844e-156">En el ejemplo siguiente se muestra cómo usar bool con una cadena o un entero.</span><span class="sxs-lookup"><span data-stu-id="0844e-156">The following example shows how to use bool with a string or integer.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="0844e-157">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="0844e-157">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="0844e-158">Nombre</span><span class="sxs-lookup"><span data-stu-id="0844e-158">Name</span></span> | <span data-ttu-id="0844e-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-159">Type</span></span> | <span data-ttu-id="0844e-160">Valor</span><span class="sxs-lookup"><span data-stu-id="0844e-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="0844e-161">trueString</span><span class="sxs-lookup"><span data-stu-id="0844e-161">trueString</span></span> | <span data-ttu-id="0844e-162">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-162">Bool</span></span> | <span data-ttu-id="0844e-163">True</span><span class="sxs-lookup"><span data-stu-id="0844e-163">True</span></span> |
| <span data-ttu-id="0844e-164">falseString</span><span class="sxs-lookup"><span data-stu-id="0844e-164">falseString</span></span> | <span data-ttu-id="0844e-165">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-165">Bool</span></span> | <span data-ttu-id="0844e-166">False</span><span class="sxs-lookup"><span data-stu-id="0844e-166">False</span></span> |
| <span data-ttu-id="0844e-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="0844e-167">trueInt</span></span> | <span data-ttu-id="0844e-168">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-168">Bool</span></span> | <span data-ttu-id="0844e-169">True</span><span class="sxs-lookup"><span data-stu-id="0844e-169">True</span></span> |
| <span data-ttu-id="0844e-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="0844e-170">falseInt</span></span> | <span data-ttu-id="0844e-171">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-171">Bool</span></span> | <span data-ttu-id="0844e-172">False</span><span class="sxs-lookup"><span data-stu-id="0844e-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="0844e-173">if</span><span class="sxs-lookup"><span data-stu-id="0844e-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="0844e-174">Devuelve un valor dependiendo de si una condición es verdadera o falsa.</span><span class="sxs-lookup"><span data-stu-id="0844e-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="0844e-175">parameters</span><span class="sxs-lookup"><span data-stu-id="0844e-175">Parameters</span></span>

| <span data-ttu-id="0844e-176">Parámetro</span><span class="sxs-lookup"><span data-stu-id="0844e-176">Parameter</span></span> | <span data-ttu-id="0844e-177">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0844e-177">Required</span></span> | <span data-ttu-id="0844e-178">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-178">Type</span></span> | <span data-ttu-id="0844e-179">Descripción</span><span class="sxs-lookup"><span data-stu-id="0844e-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0844e-180">condition</span><span class="sxs-lookup"><span data-stu-id="0844e-180">condition</span></span> |<span data-ttu-id="0844e-181">Sí</span><span class="sxs-lookup"><span data-stu-id="0844e-181">Yes</span></span> |<span data-ttu-id="0844e-182">boolean</span><span class="sxs-lookup"><span data-stu-id="0844e-182">boolean</span></span> |<span data-ttu-id="0844e-183">Valor cuya veracidad se comprueba.</span><span class="sxs-lookup"><span data-stu-id="0844e-183">The value to check whether it is true.</span></span> |
| <span data-ttu-id="0844e-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="0844e-184">trueValue</span></span> |<span data-ttu-id="0844e-185">Sí</span><span class="sxs-lookup"><span data-stu-id="0844e-185">Yes</span></span> | <span data-ttu-id="0844e-186">cadena, int, objeto o matriz</span><span class="sxs-lookup"><span data-stu-id="0844e-186">string, int, object, or array</span></span> |<span data-ttu-id="0844e-187">Valor que se devuelve cuando la condición es verdadera.</span><span class="sxs-lookup"><span data-stu-id="0844e-187">The value to return when the condition is true.</span></span> |
| <span data-ttu-id="0844e-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="0844e-188">falseValue</span></span> |<span data-ttu-id="0844e-189">Sí</span><span class="sxs-lookup"><span data-stu-id="0844e-189">Yes</span></span> | <span data-ttu-id="0844e-190">cadena, int, objeto o matriz</span><span class="sxs-lookup"><span data-stu-id="0844e-190">string, int, object, or array</span></span> |<span data-ttu-id="0844e-191">Valor que se devuelve cuando la condición es falsa.</span><span class="sxs-lookup"><span data-stu-id="0844e-191">The value to return when the condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="0844e-192">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="0844e-192">Return value</span></span>

<span data-ttu-id="0844e-193">Devuelve el segundo parámetro si el primer parámetro es **True**; en caso contrario, devuelve el tercer parámetro.</span><span class="sxs-lookup"><span data-stu-id="0844e-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="0844e-194">Comentarios</span><span class="sxs-lookup"><span data-stu-id="0844e-194">Remarks</span></span>

<span data-ttu-id="0844e-195">Puede usar esta función para establecer una propiedad de recurso de forma condicional.</span><span class="sxs-lookup"><span data-stu-id="0844e-195">You can use this function to conditionally set a resource property.</span></span> <span data-ttu-id="0844e-196">El siguiente ejemplo no es una plantilla completa, pero en él se muestran las partes relevantes para establecer el conjunto de disponibilidad de forma condicional.</span><span class="sxs-lookup"><span data-stu-id="0844e-196">The following example is not a full template, but it shows the relevant portions for conditionally setting the availability set.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a><span data-ttu-id="0844e-197">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="0844e-197">Examples</span></span>

<span data-ttu-id="0844e-198">En el ejemplo siguiente se muestra cómo usar la función `if`.</span><span class="sxs-lookup"><span data-stu-id="0844e-198">The following example shows how to use the `if` function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

<span data-ttu-id="0844e-199">El resultado del ejemplo anterior es:</span><span class="sxs-lookup"><span data-stu-id="0844e-199">The output from the preceding example is:</span></span>

| <span data-ttu-id="0844e-200">Nombre</span><span class="sxs-lookup"><span data-stu-id="0844e-200">Name</span></span> | <span data-ttu-id="0844e-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-201">Type</span></span> | <span data-ttu-id="0844e-202">Valor</span><span class="sxs-lookup"><span data-stu-id="0844e-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="0844e-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-203">yesOutput</span></span> | <span data-ttu-id="0844e-204">String</span><span class="sxs-lookup"><span data-stu-id="0844e-204">String</span></span> | <span data-ttu-id="0844e-205">yes</span><span class="sxs-lookup"><span data-stu-id="0844e-205">yes</span></span> |
| <span data-ttu-id="0844e-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-206">noOutput</span></span> | <span data-ttu-id="0844e-207">String</span><span class="sxs-lookup"><span data-stu-id="0844e-207">String</span></span> | <span data-ttu-id="0844e-208">no</span><span class="sxs-lookup"><span data-stu-id="0844e-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="0844e-209">not</span><span class="sxs-lookup"><span data-stu-id="0844e-209">not</span></span>
`not(arg1)`

<span data-ttu-id="0844e-210">Convierte el valor booleano en su valor opuesto.</span><span class="sxs-lookup"><span data-stu-id="0844e-210">Converts boolean value to its opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="0844e-211">parameters</span><span class="sxs-lookup"><span data-stu-id="0844e-211">Parameters</span></span>

| <span data-ttu-id="0844e-212">Parámetro</span><span class="sxs-lookup"><span data-stu-id="0844e-212">Parameter</span></span> | <span data-ttu-id="0844e-213">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0844e-213">Required</span></span> | <span data-ttu-id="0844e-214">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-214">Type</span></span> | <span data-ttu-id="0844e-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="0844e-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0844e-216">arg1</span><span class="sxs-lookup"><span data-stu-id="0844e-216">arg1</span></span> |<span data-ttu-id="0844e-217">Sí</span><span class="sxs-lookup"><span data-stu-id="0844e-217">Yes</span></span> |<span data-ttu-id="0844e-218">boolean</span><span class="sxs-lookup"><span data-stu-id="0844e-218">boolean</span></span> |<span data-ttu-id="0844e-219">Valor que se va a convertir.</span><span class="sxs-lookup"><span data-stu-id="0844e-219">The value to convert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="0844e-220">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="0844e-220">Return value</span></span>

<span data-ttu-id="0844e-221">Devuelve **True** si el parámetro es **False**.</span><span class="sxs-lookup"><span data-stu-id="0844e-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="0844e-222">Devuelve **False** si el parámetro es **True**.</span><span class="sxs-lookup"><span data-stu-id="0844e-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="0844e-223">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="0844e-223">Examples</span></span>

<span data-ttu-id="0844e-224">En el ejemplo siguiente se muestra cómo usar las funciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="0844e-224">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="0844e-225">El resultado del ejemplo anterior es:</span><span class="sxs-lookup"><span data-stu-id="0844e-225">The output from the preceding example is:</span></span>

| <span data-ttu-id="0844e-226">Nombre</span><span class="sxs-lookup"><span data-stu-id="0844e-226">Name</span></span> | <span data-ttu-id="0844e-227">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-227">Type</span></span> | <span data-ttu-id="0844e-228">Valor</span><span class="sxs-lookup"><span data-stu-id="0844e-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="0844e-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-229">andExampleOutput</span></span> | <span data-ttu-id="0844e-230">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-230">Bool</span></span> | <span data-ttu-id="0844e-231">False</span><span class="sxs-lookup"><span data-stu-id="0844e-231">False</span></span> |
| <span data-ttu-id="0844e-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-232">orExampleOutput</span></span> | <span data-ttu-id="0844e-233">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-233">Bool</span></span> | <span data-ttu-id="0844e-234">True</span><span class="sxs-lookup"><span data-stu-id="0844e-234">True</span></span> |
| <span data-ttu-id="0844e-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-235">notExampleOutput</span></span> | <span data-ttu-id="0844e-236">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-236">Bool</span></span> | <span data-ttu-id="0844e-237">False</span><span class="sxs-lookup"><span data-stu-id="0844e-237">False</span></span> |

<span data-ttu-id="0844e-238">En el siguiente ejemplo se usa **not** con [equals](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="0844e-238">The following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "checkNotEquals": {
            "type": "bool",
            "value": "[not(equals(1, 2))]"
        }
    }
```

<span data-ttu-id="0844e-239">El resultado del ejemplo anterior es:</span><span class="sxs-lookup"><span data-stu-id="0844e-239">The output from the preceding example is:</span></span>

| <span data-ttu-id="0844e-240">Nombre</span><span class="sxs-lookup"><span data-stu-id="0844e-240">Name</span></span> | <span data-ttu-id="0844e-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-241">Type</span></span> | <span data-ttu-id="0844e-242">Valor</span><span class="sxs-lookup"><span data-stu-id="0844e-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="0844e-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="0844e-243">checkNotEquals</span></span> | <span data-ttu-id="0844e-244">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-244">Bool</span></span> | <span data-ttu-id="0844e-245">True</span><span class="sxs-lookup"><span data-stu-id="0844e-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="0844e-246">o</span><span class="sxs-lookup"><span data-stu-id="0844e-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="0844e-247">Comprueba si cualquiera de los valores de parámetro es verdadero.</span><span class="sxs-lookup"><span data-stu-id="0844e-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="0844e-248">parameters</span><span class="sxs-lookup"><span data-stu-id="0844e-248">Parameters</span></span>

| <span data-ttu-id="0844e-249">Parámetro</span><span class="sxs-lookup"><span data-stu-id="0844e-249">Parameter</span></span> | <span data-ttu-id="0844e-250">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="0844e-250">Required</span></span> | <span data-ttu-id="0844e-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-251">Type</span></span> | <span data-ttu-id="0844e-252">Descripción</span><span class="sxs-lookup"><span data-stu-id="0844e-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0844e-253">arg1</span><span class="sxs-lookup"><span data-stu-id="0844e-253">arg1</span></span> |<span data-ttu-id="0844e-254">Sí</span><span class="sxs-lookup"><span data-stu-id="0844e-254">Yes</span></span> |<span data-ttu-id="0844e-255">boolean</span><span class="sxs-lookup"><span data-stu-id="0844e-255">boolean</span></span> |<span data-ttu-id="0844e-256">Primer valor cuya veracidad se comprueba.</span><span class="sxs-lookup"><span data-stu-id="0844e-256">The first value to check whether is true.</span></span> |
| <span data-ttu-id="0844e-257">arg2</span><span class="sxs-lookup"><span data-stu-id="0844e-257">arg2</span></span> |<span data-ttu-id="0844e-258">Sí</span><span class="sxs-lookup"><span data-stu-id="0844e-258">Yes</span></span> |<span data-ttu-id="0844e-259">boolean</span><span class="sxs-lookup"><span data-stu-id="0844e-259">boolean</span></span> |<span data-ttu-id="0844e-260">Segundo valor cuya veracidad se comprueba.</span><span class="sxs-lookup"><span data-stu-id="0844e-260">The second value to check whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="0844e-261">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="0844e-261">Return value</span></span>

<span data-ttu-id="0844e-262">Devuelve **True** si cualquiera de los valores es verdadero; en caso contrario, devuelve **False**.</span><span class="sxs-lookup"><span data-stu-id="0844e-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="0844e-263">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="0844e-263">Examples</span></span>

<span data-ttu-id="0844e-264">En el ejemplo siguiente se muestra cómo usar las funciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="0844e-264">The following example shows how to use logical functions.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

<span data-ttu-id="0844e-265">El resultado del ejemplo anterior es:</span><span class="sxs-lookup"><span data-stu-id="0844e-265">The output from the preceding example is:</span></span>

| <span data-ttu-id="0844e-266">Nombre</span><span class="sxs-lookup"><span data-stu-id="0844e-266">Name</span></span> | <span data-ttu-id="0844e-267">Tipo</span><span class="sxs-lookup"><span data-stu-id="0844e-267">Type</span></span> | <span data-ttu-id="0844e-268">Valor</span><span class="sxs-lookup"><span data-stu-id="0844e-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="0844e-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-269">andExampleOutput</span></span> | <span data-ttu-id="0844e-270">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-270">Bool</span></span> | <span data-ttu-id="0844e-271">False</span><span class="sxs-lookup"><span data-stu-id="0844e-271">False</span></span> |
| <span data-ttu-id="0844e-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-272">orExampleOutput</span></span> | <span data-ttu-id="0844e-273">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-273">Bool</span></span> | <span data-ttu-id="0844e-274">True</span><span class="sxs-lookup"><span data-stu-id="0844e-274">True</span></span> |
| <span data-ttu-id="0844e-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="0844e-275">notExampleOutput</span></span> | <span data-ttu-id="0844e-276">Booleano</span><span class="sxs-lookup"><span data-stu-id="0844e-276">Bool</span></span> | <span data-ttu-id="0844e-277">False</span><span class="sxs-lookup"><span data-stu-id="0844e-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="0844e-278">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0844e-278">Next steps</span></span>
* <span data-ttu-id="0844e-279">Para obtener una descripción de las secciones de una plantilla de Azure Resource Manager, vea [Creación de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0844e-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="0844e-280">Para combinar varias plantillas, vea [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0844e-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="0844e-281">Para iterar una cantidad de veces específica al crear un tipo de recurso, vea [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="0844e-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="0844e-282">Para saber cómo implementar la plantilla que creó, consulte [Implementación de una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="0844e-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

