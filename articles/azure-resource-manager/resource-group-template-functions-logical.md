---
title: "funciones de plantilla de administrador de recursos aaaAzure - lógicas | Documentos de Microsoft"
description: "Describe hello toouse de funciones en una lógica de valores de toodetermine de plantilla Azure Resource Manager."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="ad968-103">Funciones lógicas para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ad968-103">Logical functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="ad968-104">Resource Manager proporciona varias funciones para realizar comparaciones en las plantillas.</span><span class="sxs-lookup"><span data-stu-id="ad968-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="ad968-105">and</span><span class="sxs-lookup"><span data-stu-id="ad968-105">and</span></span>](#and)
* [<span data-ttu-id="ad968-106">bool</span><span class="sxs-lookup"><span data-stu-id="ad968-106">bool</span></span>](#bool)
* [<span data-ttu-id="ad968-107">if</span><span class="sxs-lookup"><span data-stu-id="ad968-107">if</span></span>](#if)
* [<span data-ttu-id="ad968-108">not</span><span class="sxs-lookup"><span data-stu-id="ad968-108">not</span></span>](#not)
* [<span data-ttu-id="ad968-109">or</span><span class="sxs-lookup"><span data-stu-id="ad968-109">or</span></span>](#or)

## <a name="and"></a><span data-ttu-id="ad968-110">y</span><span class="sxs-lookup"><span data-stu-id="ad968-110">and</span></span>
`and(arg1, arg2)`

<span data-ttu-id="ad968-111">Comprueba si los dos valores de parámetro son verdaderos.</span><span class="sxs-lookup"><span data-stu-id="ad968-111">Checks whether both parameter values are true.</span></span>

### <a name="parameters"></a><span data-ttu-id="ad968-112">parameters</span><span class="sxs-lookup"><span data-stu-id="ad968-112">Parameters</span></span>

| <span data-ttu-id="ad968-113">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ad968-113">Parameter</span></span> | <span data-ttu-id="ad968-114">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ad968-114">Required</span></span> | <span data-ttu-id="ad968-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-115">Type</span></span> | <span data-ttu-id="ad968-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="ad968-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ad968-117">arg1</span><span class="sxs-lookup"><span data-stu-id="ad968-117">arg1</span></span> |<span data-ttu-id="ad968-118">Sí</span><span class="sxs-lookup"><span data-stu-id="ad968-118">Yes</span></span> |<span data-ttu-id="ad968-119">boolean</span><span class="sxs-lookup"><span data-stu-id="ad968-119">boolean</span></span> |<span data-ttu-id="ad968-120">Hola primera toocheck valor si es true.</span><span class="sxs-lookup"><span data-stu-id="ad968-120">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="ad968-121">arg2</span><span class="sxs-lookup"><span data-stu-id="ad968-121">arg2</span></span> |<span data-ttu-id="ad968-122">Sí</span><span class="sxs-lookup"><span data-stu-id="ad968-122">Yes</span></span> |<span data-ttu-id="ad968-123">boolean</span><span class="sxs-lookup"><span data-stu-id="ad968-123">boolean</span></span> |<span data-ttu-id="ad968-124">Hola segundo toocheck valor si es true.</span><span class="sxs-lookup"><span data-stu-id="ad968-124">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ad968-125">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ad968-125">Return value</span></span>

<span data-ttu-id="ad968-126">Devuelve **True** si ambos valores son verdaderos; en caso contrario, devuelve **False**.</span><span class="sxs-lookup"><span data-stu-id="ad968-126">Returns **True** if both values are true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="ad968-127">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ad968-127">Examples</span></span>

<span data-ttu-id="ad968-128">Hola siguiente ejemplo se muestra cómo las funciones lógicas de toouse.</span><span class="sxs-lookup"><span data-stu-id="ad968-128">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="ad968-129">resultado Hola Hola anterior ejemplo es:</span><span class="sxs-lookup"><span data-stu-id="ad968-129">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="ad968-130">Nombre</span><span class="sxs-lookup"><span data-stu-id="ad968-130">Name</span></span> | <span data-ttu-id="ad968-131">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-131">Type</span></span> | <span data-ttu-id="ad968-132">Valor</span><span class="sxs-lookup"><span data-stu-id="ad968-132">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ad968-133">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-133">andExampleOutput</span></span> | <span data-ttu-id="ad968-134">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-134">Bool</span></span> | <span data-ttu-id="ad968-135">False</span><span class="sxs-lookup"><span data-stu-id="ad968-135">False</span></span> |
| <span data-ttu-id="ad968-136">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-136">orExampleOutput</span></span> | <span data-ttu-id="ad968-137">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-137">Bool</span></span> | <span data-ttu-id="ad968-138">True</span><span class="sxs-lookup"><span data-stu-id="ad968-138">True</span></span> |
| <span data-ttu-id="ad968-139">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-139">notExampleOutput</span></span> | <span data-ttu-id="ad968-140">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-140">Bool</span></span> | <span data-ttu-id="ad968-141">False</span><span class="sxs-lookup"><span data-stu-id="ad968-141">False</span></span> |


## <a name="bool"></a><span data-ttu-id="ad968-142">booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-142">bool</span></span>
`bool(arg1)`

<span data-ttu-id="ad968-143">Convierte Hola tooa parámetro booleano.</span><span class="sxs-lookup"><span data-stu-id="ad968-143">Converts hello parameter tooa boolean.</span></span>

### <a name="parameters"></a><span data-ttu-id="ad968-144">parameters</span><span class="sxs-lookup"><span data-stu-id="ad968-144">Parameters</span></span>

| <span data-ttu-id="ad968-145">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ad968-145">Parameter</span></span> | <span data-ttu-id="ad968-146">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ad968-146">Required</span></span> | <span data-ttu-id="ad968-147">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-147">Type</span></span> | <span data-ttu-id="ad968-148">Descripción</span><span class="sxs-lookup"><span data-stu-id="ad968-148">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ad968-149">arg1</span><span class="sxs-lookup"><span data-stu-id="ad968-149">arg1</span></span> |<span data-ttu-id="ad968-150">Sí</span><span class="sxs-lookup"><span data-stu-id="ad968-150">Yes</span></span> |<span data-ttu-id="ad968-151">cadena o entero</span><span class="sxs-lookup"><span data-stu-id="ad968-151">string or int</span></span> |<span data-ttu-id="ad968-152">Hola tooa tooconvert de valor booleano.</span><span class="sxs-lookup"><span data-stu-id="ad968-152">hello value tooconvert tooa boolean.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ad968-153">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ad968-153">Return value</span></span>
<span data-ttu-id="ad968-154">Un valor booleano de hello valor convertido.</span><span class="sxs-lookup"><span data-stu-id="ad968-154">A boolean of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="ad968-155">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ad968-155">Examples</span></span>

<span data-ttu-id="ad968-156">Hola siguiente ejemplo se muestra cómo bool toouse con una cadena o un entero.</span><span class="sxs-lookup"><span data-stu-id="ad968-156">hello following example shows how toouse bool with a string or integer.</span></span>

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

<span data-ttu-id="ad968-157">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="ad968-157">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ad968-158">Nombre</span><span class="sxs-lookup"><span data-stu-id="ad968-158">Name</span></span> | <span data-ttu-id="ad968-159">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-159">Type</span></span> | <span data-ttu-id="ad968-160">Valor</span><span class="sxs-lookup"><span data-stu-id="ad968-160">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ad968-161">trueString</span><span class="sxs-lookup"><span data-stu-id="ad968-161">trueString</span></span> | <span data-ttu-id="ad968-162">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-162">Bool</span></span> | <span data-ttu-id="ad968-163">True</span><span class="sxs-lookup"><span data-stu-id="ad968-163">True</span></span> |
| <span data-ttu-id="ad968-164">falseString</span><span class="sxs-lookup"><span data-stu-id="ad968-164">falseString</span></span> | <span data-ttu-id="ad968-165">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-165">Bool</span></span> | <span data-ttu-id="ad968-166">False</span><span class="sxs-lookup"><span data-stu-id="ad968-166">False</span></span> |
| <span data-ttu-id="ad968-167">trueInt</span><span class="sxs-lookup"><span data-stu-id="ad968-167">trueInt</span></span> | <span data-ttu-id="ad968-168">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-168">Bool</span></span> | <span data-ttu-id="ad968-169">True</span><span class="sxs-lookup"><span data-stu-id="ad968-169">True</span></span> |
| <span data-ttu-id="ad968-170">falseInt</span><span class="sxs-lookup"><span data-stu-id="ad968-170">falseInt</span></span> | <span data-ttu-id="ad968-171">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-171">Bool</span></span> | <span data-ttu-id="ad968-172">False</span><span class="sxs-lookup"><span data-stu-id="ad968-172">False</span></span> |

## <a name="if"></a><span data-ttu-id="ad968-173">if</span><span class="sxs-lookup"><span data-stu-id="ad968-173">if</span></span>
`if(condition, trueValue, falseValue)`

<span data-ttu-id="ad968-174">Devuelve un valor dependiendo de si una condición es verdadera o falsa.</span><span class="sxs-lookup"><span data-stu-id="ad968-174">Returns a value based on whether a condition is true or false.</span></span>

### <a name="parameters"></a><span data-ttu-id="ad968-175">parameters</span><span class="sxs-lookup"><span data-stu-id="ad968-175">Parameters</span></span>

| <span data-ttu-id="ad968-176">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ad968-176">Parameter</span></span> | <span data-ttu-id="ad968-177">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ad968-177">Required</span></span> | <span data-ttu-id="ad968-178">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-178">Type</span></span> | <span data-ttu-id="ad968-179">Descripción</span><span class="sxs-lookup"><span data-stu-id="ad968-179">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ad968-180">condition</span><span class="sxs-lookup"><span data-stu-id="ad968-180">condition</span></span> |<span data-ttu-id="ad968-181">Sí</span><span class="sxs-lookup"><span data-stu-id="ad968-181">Yes</span></span> |<span data-ttu-id="ad968-182">boolean</span><span class="sxs-lookup"><span data-stu-id="ad968-182">boolean</span></span> |<span data-ttu-id="ad968-183">Hola toocheck valor si es true.</span><span class="sxs-lookup"><span data-stu-id="ad968-183">hello value toocheck whether it is true.</span></span> |
| <span data-ttu-id="ad968-184">trueValue</span><span class="sxs-lookup"><span data-stu-id="ad968-184">trueValue</span></span> |<span data-ttu-id="ad968-185">Sí</span><span class="sxs-lookup"><span data-stu-id="ad968-185">Yes</span></span> | <span data-ttu-id="ad968-186">cadena, int, objeto o matriz</span><span class="sxs-lookup"><span data-stu-id="ad968-186">string, int, object, or array</span></span> |<span data-ttu-id="ad968-187">Hola valor tooreturn cuando Hola condición sea verdadera.</span><span class="sxs-lookup"><span data-stu-id="ad968-187">hello value tooreturn when hello condition is true.</span></span> |
| <span data-ttu-id="ad968-188">falseValue</span><span class="sxs-lookup"><span data-stu-id="ad968-188">falseValue</span></span> |<span data-ttu-id="ad968-189">Sí</span><span class="sxs-lookup"><span data-stu-id="ad968-189">Yes</span></span> | <span data-ttu-id="ad968-190">cadena, int, objeto o matriz</span><span class="sxs-lookup"><span data-stu-id="ad968-190">string, int, object, or array</span></span> |<span data-ttu-id="ad968-191">Hola valor tooreturn cuando Hola condición es false.</span><span class="sxs-lookup"><span data-stu-id="ad968-191">hello value tooreturn when hello condition is false.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ad968-192">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ad968-192">Return value</span></span>

<span data-ttu-id="ad968-193">Devuelve el segundo parámetro si el primer parámetro es **True**; en caso contrario, devuelve el tercer parámetro.</span><span class="sxs-lookup"><span data-stu-id="ad968-193">Returns second parameter when first parameter is **True**; otherwise, returns third parameter.</span></span>

### <a name="remarks"></a><span data-ttu-id="ad968-194">Comentarios</span><span class="sxs-lookup"><span data-stu-id="ad968-194">Remarks</span></span>

<span data-ttu-id="ad968-195">Puede utilizar este conjunto de tooconditionally de función de una propiedad de recurso.</span><span class="sxs-lookup"><span data-stu-id="ad968-195">You can use this function tooconditionally set a resource property.</span></span> <span data-ttu-id="ad968-196">Hello en el ejemplo siguiente no se es una plantilla completa, pero muestra las partes relevantes de Hola para establecer condicionalmente el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad968-196">hello following example is not a full template, but it shows hello relevant portions for conditionally setting hello availability set.</span></span>

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

### <a name="examples"></a><span data-ttu-id="ad968-197">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ad968-197">Examples</span></span>

<span data-ttu-id="ad968-198">Hola siguiente ejemplo se muestra cómo toouse hello `if` función.</span><span class="sxs-lookup"><span data-stu-id="ad968-198">hello following example shows how toouse hello `if` function.</span></span>

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

<span data-ttu-id="ad968-199">resultado Hola Hola anterior ejemplo es:</span><span class="sxs-lookup"><span data-stu-id="ad968-199">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="ad968-200">Nombre</span><span class="sxs-lookup"><span data-stu-id="ad968-200">Name</span></span> | <span data-ttu-id="ad968-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-201">Type</span></span> | <span data-ttu-id="ad968-202">Valor</span><span class="sxs-lookup"><span data-stu-id="ad968-202">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ad968-203">yesOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-203">yesOutput</span></span> | <span data-ttu-id="ad968-204">String</span><span class="sxs-lookup"><span data-stu-id="ad968-204">String</span></span> | <span data-ttu-id="ad968-205">yes</span><span class="sxs-lookup"><span data-stu-id="ad968-205">yes</span></span> |
| <span data-ttu-id="ad968-206">noOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-206">noOutput</span></span> | <span data-ttu-id="ad968-207">String</span><span class="sxs-lookup"><span data-stu-id="ad968-207">String</span></span> | <span data-ttu-id="ad968-208">no</span><span class="sxs-lookup"><span data-stu-id="ad968-208">no</span></span> |


## <a name="not"></a><span data-ttu-id="ad968-209">not</span><span class="sxs-lookup"><span data-stu-id="ad968-209">not</span></span>
`not(arg1)`

<span data-ttu-id="ad968-210">Convierte el valor booleano tooits opuesto valor.</span><span class="sxs-lookup"><span data-stu-id="ad968-210">Converts boolean value tooits opposite value.</span></span>

### <a name="parameters"></a><span data-ttu-id="ad968-211">parameters</span><span class="sxs-lookup"><span data-stu-id="ad968-211">Parameters</span></span>

| <span data-ttu-id="ad968-212">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ad968-212">Parameter</span></span> | <span data-ttu-id="ad968-213">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ad968-213">Required</span></span> | <span data-ttu-id="ad968-214">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-214">Type</span></span> | <span data-ttu-id="ad968-215">Descripción</span><span class="sxs-lookup"><span data-stu-id="ad968-215">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ad968-216">arg1</span><span class="sxs-lookup"><span data-stu-id="ad968-216">arg1</span></span> |<span data-ttu-id="ad968-217">Sí</span><span class="sxs-lookup"><span data-stu-id="ad968-217">Yes</span></span> |<span data-ttu-id="ad968-218">boolean</span><span class="sxs-lookup"><span data-stu-id="ad968-218">boolean</span></span> |<span data-ttu-id="ad968-219">Hola tooconvert de valor.</span><span class="sxs-lookup"><span data-stu-id="ad968-219">hello value tooconvert.</span></span> |


### <a name="return-value"></a><span data-ttu-id="ad968-220">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ad968-220">Return value</span></span>

<span data-ttu-id="ad968-221">Devuelve **True** si el parámetro es **False**.</span><span class="sxs-lookup"><span data-stu-id="ad968-221">Returns **True** when parameter is **False**.</span></span> <span data-ttu-id="ad968-222">Devuelve **False** si el parámetro es **True**.</span><span class="sxs-lookup"><span data-stu-id="ad968-222">Returns **False** when parameter is **True**.</span></span>

### <a name="examples"></a><span data-ttu-id="ad968-223">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ad968-223">Examples</span></span>

<span data-ttu-id="ad968-224">Hola siguiente ejemplo se muestra cómo las funciones lógicas de toouse.</span><span class="sxs-lookup"><span data-stu-id="ad968-224">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="ad968-225">resultado Hola Hola anterior ejemplo es:</span><span class="sxs-lookup"><span data-stu-id="ad968-225">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="ad968-226">Nombre</span><span class="sxs-lookup"><span data-stu-id="ad968-226">Name</span></span> | <span data-ttu-id="ad968-227">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-227">Type</span></span> | <span data-ttu-id="ad968-228">Valor</span><span class="sxs-lookup"><span data-stu-id="ad968-228">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ad968-229">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-229">andExampleOutput</span></span> | <span data-ttu-id="ad968-230">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-230">Bool</span></span> | <span data-ttu-id="ad968-231">False</span><span class="sxs-lookup"><span data-stu-id="ad968-231">False</span></span> |
| <span data-ttu-id="ad968-232">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-232">orExampleOutput</span></span> | <span data-ttu-id="ad968-233">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-233">Bool</span></span> | <span data-ttu-id="ad968-234">True</span><span class="sxs-lookup"><span data-stu-id="ad968-234">True</span></span> |
| <span data-ttu-id="ad968-235">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-235">notExampleOutput</span></span> | <span data-ttu-id="ad968-236">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-236">Bool</span></span> | <span data-ttu-id="ad968-237">False</span><span class="sxs-lookup"><span data-stu-id="ad968-237">False</span></span> |

<span data-ttu-id="ad968-238">Hello siguiente ejemplo se utiliza **no** con [es igual a](resource-group-template-functions-comparison.md#equals).</span><span class="sxs-lookup"><span data-stu-id="ad968-238">hello following example uses **not** with [equals](resource-group-template-functions-comparison.md#equals).</span></span>

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

<span data-ttu-id="ad968-239">resultado Hola Hola anterior ejemplo es:</span><span class="sxs-lookup"><span data-stu-id="ad968-239">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="ad968-240">Nombre</span><span class="sxs-lookup"><span data-stu-id="ad968-240">Name</span></span> | <span data-ttu-id="ad968-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-241">Type</span></span> | <span data-ttu-id="ad968-242">Valor</span><span class="sxs-lookup"><span data-stu-id="ad968-242">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ad968-243">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="ad968-243">checkNotEquals</span></span> | <span data-ttu-id="ad968-244">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-244">Bool</span></span> | <span data-ttu-id="ad968-245">True</span><span class="sxs-lookup"><span data-stu-id="ad968-245">True</span></span> |


## <a name="or"></a><span data-ttu-id="ad968-246">o</span><span class="sxs-lookup"><span data-stu-id="ad968-246">or</span></span>
`or(arg1, arg2)`

<span data-ttu-id="ad968-247">Comprueba si cualquiera de los valores de parámetro es verdadero.</span><span class="sxs-lookup"><span data-stu-id="ad968-247">Checks whether either parameter value is true.</span></span>

### <a name="parameters"></a><span data-ttu-id="ad968-248">parameters</span><span class="sxs-lookup"><span data-stu-id="ad968-248">Parameters</span></span>

| <span data-ttu-id="ad968-249">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ad968-249">Parameter</span></span> | <span data-ttu-id="ad968-250">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ad968-250">Required</span></span> | <span data-ttu-id="ad968-251">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-251">Type</span></span> | <span data-ttu-id="ad968-252">Descripción</span><span class="sxs-lookup"><span data-stu-id="ad968-252">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ad968-253">arg1</span><span class="sxs-lookup"><span data-stu-id="ad968-253">arg1</span></span> |<span data-ttu-id="ad968-254">Sí</span><span class="sxs-lookup"><span data-stu-id="ad968-254">Yes</span></span> |<span data-ttu-id="ad968-255">boolean</span><span class="sxs-lookup"><span data-stu-id="ad968-255">boolean</span></span> |<span data-ttu-id="ad968-256">Hola primera toocheck valor si es true.</span><span class="sxs-lookup"><span data-stu-id="ad968-256">hello first value toocheck whether is true.</span></span> |
| <span data-ttu-id="ad968-257">arg2</span><span class="sxs-lookup"><span data-stu-id="ad968-257">arg2</span></span> |<span data-ttu-id="ad968-258">Sí</span><span class="sxs-lookup"><span data-stu-id="ad968-258">Yes</span></span> |<span data-ttu-id="ad968-259">boolean</span><span class="sxs-lookup"><span data-stu-id="ad968-259">boolean</span></span> |<span data-ttu-id="ad968-260">Hola segundo toocheck valor si es true.</span><span class="sxs-lookup"><span data-stu-id="ad968-260">hello second value toocheck whether is true.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ad968-261">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ad968-261">Return value</span></span>

<span data-ttu-id="ad968-262">Devuelve **True** si cualquiera de los valores es verdadero; en caso contrario, devuelve **False**.</span><span class="sxs-lookup"><span data-stu-id="ad968-262">Returns **True** if either value is true; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="ad968-263">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="ad968-263">Examples</span></span>

<span data-ttu-id="ad968-264">Hola siguiente ejemplo se muestra cómo las funciones lógicas de toouse.</span><span class="sxs-lookup"><span data-stu-id="ad968-264">hello following example shows how toouse logical functions.</span></span>

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

<span data-ttu-id="ad968-265">resultado Hola Hola anterior ejemplo es:</span><span class="sxs-lookup"><span data-stu-id="ad968-265">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="ad968-266">Nombre</span><span class="sxs-lookup"><span data-stu-id="ad968-266">Name</span></span> | <span data-ttu-id="ad968-267">Tipo</span><span class="sxs-lookup"><span data-stu-id="ad968-267">Type</span></span> | <span data-ttu-id="ad968-268">Valor</span><span class="sxs-lookup"><span data-stu-id="ad968-268">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ad968-269">andExampleOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-269">andExampleOutput</span></span> | <span data-ttu-id="ad968-270">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-270">Bool</span></span> | <span data-ttu-id="ad968-271">False</span><span class="sxs-lookup"><span data-stu-id="ad968-271">False</span></span> |
| <span data-ttu-id="ad968-272">orExampleOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-272">orExampleOutput</span></span> | <span data-ttu-id="ad968-273">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-273">Bool</span></span> | <span data-ttu-id="ad968-274">True</span><span class="sxs-lookup"><span data-stu-id="ad968-274">True</span></span> |
| <span data-ttu-id="ad968-275">notExampleOutput</span><span class="sxs-lookup"><span data-stu-id="ad968-275">notExampleOutput</span></span> | <span data-ttu-id="ad968-276">Booleano</span><span class="sxs-lookup"><span data-stu-id="ad968-276">Bool</span></span> | <span data-ttu-id="ad968-277">False</span><span class="sxs-lookup"><span data-stu-id="ad968-277">False</span></span> |


## <a name="next-steps"></a><span data-ttu-id="ad968-278">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad968-278">Next steps</span></span>
* <span data-ttu-id="ad968-279">Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ad968-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="ad968-280">toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ad968-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="ad968-281">tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="ad968-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="ad968-282">toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ad968-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

