---
title: 'plantilla de administrador de recursos de aaaAzure las funciones: las matrices y los objetos | Documentos de Microsoft'
description: Describe hello toouse de funciones en una plantilla de administrador de recursos de Azure para trabajar con objetos y matrices.
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
ms.date: 06/12/2017
ms.author: tomfitz
ms.openlocfilehash: e5f1a9b2a71039562eae7e48c2474a1fa59a7bea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="6d48d-103">Funciones de matriz y de objeto para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d48d-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="6d48d-104">Resource Manager ofrece varias funciones para trabajar con matrices y objetos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="6d48d-105">matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-105">array</span></span>](#array)
* [<span data-ttu-id="6d48d-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="6d48d-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="6d48d-107">concat</span><span class="sxs-lookup"><span data-stu-id="6d48d-107">concat</span></span>](#concat)
* [<span data-ttu-id="6d48d-108">contains</span><span class="sxs-lookup"><span data-stu-id="6d48d-108">contains</span></span>](#contains)
* [<span data-ttu-id="6d48d-109">createArray</span><span class="sxs-lookup"><span data-stu-id="6d48d-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="6d48d-110">empty</span><span class="sxs-lookup"><span data-stu-id="6d48d-110">empty</span></span>](#empty)
* [<span data-ttu-id="6d48d-111">first</span><span class="sxs-lookup"><span data-stu-id="6d48d-111">first</span></span>](#first)
* [<span data-ttu-id="6d48d-112">intersection</span><span class="sxs-lookup"><span data-stu-id="6d48d-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="6d48d-113">json</span><span class="sxs-lookup"><span data-stu-id="6d48d-113">json</span></span>](#json)
* [<span data-ttu-id="6d48d-114">last</span><span class="sxs-lookup"><span data-stu-id="6d48d-114">last</span></span>](#last)
* [<span data-ttu-id="6d48d-115">length</span><span class="sxs-lookup"><span data-stu-id="6d48d-115">length</span></span>](#length)
* [<span data-ttu-id="6d48d-116">min</span><span class="sxs-lookup"><span data-stu-id="6d48d-116">min</span></span>](#min)
* [<span data-ttu-id="6d48d-117">max</span><span class="sxs-lookup"><span data-stu-id="6d48d-117">max</span></span>](#max)
* [<span data-ttu-id="6d48d-118">range</span><span class="sxs-lookup"><span data-stu-id="6d48d-118">range</span></span>](#range)
* [<span data-ttu-id="6d48d-119">skip</span><span class="sxs-lookup"><span data-stu-id="6d48d-119">skip</span></span>](#skip)
* [<span data-ttu-id="6d48d-120">take</span><span class="sxs-lookup"><span data-stu-id="6d48d-120">take</span></span>](#take)
* [<span data-ttu-id="6d48d-121">union</span><span class="sxs-lookup"><span data-stu-id="6d48d-121">union</span></span>](#union)

<span data-ttu-id="6d48d-122">tooget una matriz de valores de cadena delimitada por un valor, vea [dividir](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="6d48d-122">tooget an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="6d48d-123">array</span><span class="sxs-lookup"><span data-stu-id="6d48d-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="6d48d-124">Convierte la matriz de hello valores tooan.</span><span class="sxs-lookup"><span data-stu-id="6d48d-124">Converts hello value tooan array.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-125">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-125">Parameters</span></span>

| <span data-ttu-id="6d48d-126">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-126">Parameter</span></span> | <span data-ttu-id="6d48d-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-127">Required</span></span> | <span data-ttu-id="6d48d-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-128">Type</span></span> | <span data-ttu-id="6d48d-129">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="6d48d-130">convertToArray</span></span> |<span data-ttu-id="6d48d-131">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-131">Yes</span></span> |<span data-ttu-id="6d48d-132">entero, cadena, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-132">int, string, array, or object</span></span> |<span data-ttu-id="6d48d-133">matriz de Hello valores tooconvert tooan.</span><span class="sxs-lookup"><span data-stu-id="6d48d-133">hello value tooconvert tooan array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-134">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-134">Return value</span></span>

<span data-ttu-id="6d48d-135">Una matriz.</span><span class="sxs-lookup"><span data-stu-id="6d48d-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-136">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-136">Example</span></span>

<span data-ttu-id="6d48d-137">Hello en el ejemplo siguiente se muestra cómo toouse Hola función de matriz con los diferentes tipos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-137">hello following example shows how toouse hello array function with different types.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "intToConvert": {
            "type": "int",
            "defaultValue": 1
        },
        "stringToConvert": {
            "type": "string",
            "defaultValue": "a"
        },
        "objectToConvert": {
            "type": "object",
            "defaultValue": {"a": "b", "c": "d"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "intOutput": {
            "type": "array",
            "value": "[array(parameters('intToConvert'))]"
        },
        "stringOutput": {
            "type": "array",
            "value": "[array(parameters('stringToConvert'))]"
        },
        "objectOutput": {
            "type": "array",
            "value": "[array(parameters('objectToConvert'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-138">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-138">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-139">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-139">Name</span></span> | <span data-ttu-id="6d48d-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-140">Type</span></span> | <span data-ttu-id="6d48d-141">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-142">intOutput</span></span> | <span data-ttu-id="6d48d-143">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-143">Array</span></span> | <span data-ttu-id="6d48d-144">[1]</span><span class="sxs-lookup"><span data-stu-id="6d48d-144">[1]</span></span> |
| <span data-ttu-id="6d48d-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-145">stringOutput</span></span> | <span data-ttu-id="6d48d-146">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-146">Array</span></span> | <span data-ttu-id="6d48d-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="6d48d-147">["a"]</span></span> |
| <span data-ttu-id="6d48d-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-148">objectOutput</span></span> | <span data-ttu-id="6d48d-149">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-149">Array</span></span> | <span data-ttu-id="6d48d-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="6d48d-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="6d48d-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="6d48d-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="6d48d-152">Devuelve el primer valor distinto de null de parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-152">Returns first non-null value from hello parameters.</span></span> <span data-ttu-id="6d48d-153">Las cadenas vacías, las matrices vacías y los objetos vacíos no son nulos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-154">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-154">Parameters</span></span>

| <span data-ttu-id="6d48d-155">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-155">Parameter</span></span> | <span data-ttu-id="6d48d-156">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-156">Required</span></span> | <span data-ttu-id="6d48d-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-157">Type</span></span> | <span data-ttu-id="6d48d-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-159">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-159">arg1</span></span> |<span data-ttu-id="6d48d-160">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-160">Yes</span></span> |<span data-ttu-id="6d48d-161">entero, cadena, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-161">int, string, array, or object</span></span> |<span data-ttu-id="6d48d-162">Hola primer valor tootest si hay valores null.</span><span class="sxs-lookup"><span data-stu-id="6d48d-162">hello first value tootest for null.</span></span> |
| <span data-ttu-id="6d48d-163">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="6d48d-163">additional args</span></span> |<span data-ttu-id="6d48d-164">No</span><span class="sxs-lookup"><span data-stu-id="6d48d-164">No</span></span> |<span data-ttu-id="6d48d-165">entero, cadena, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-165">int, string, array, or object</span></span> |<span data-ttu-id="6d48d-166">Valores adicionales tootest si hay valores null.</span><span class="sxs-lookup"><span data-stu-id="6d48d-166">Additional values tootest for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-167">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-167">Return value</span></span>

<span data-ttu-id="6d48d-168">valor de Hola de parámetros distintos de null primera hello, que puede ser una cadena, int, matriz u objeto.</span><span class="sxs-lookup"><span data-stu-id="6d48d-168">hello value of hello first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="6d48d-169">Es nulo si todos los parámetros son nulos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="6d48d-170">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-170">Example</span></span>

<span data-ttu-id="6d48d-171">Hello en el ejemplo siguiente se muestra la salida de hello desde diferentes usos de coalesce.</span><span class="sxs-lookup"><span data-stu-id="6d48d-171">hello following example shows hello output from different uses of coalesce.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {
                "null1": null, 
                "null2": null,
                "string": "default",
                "int": 1,
                "object": {"first": "default"},
                "array": [1]
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').string)]"
        },
        "intOutput": {
            "type": "int",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').int)]"
        },
        "objectOutput": {
            "type": "object",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').object)]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2, parameters('objectToTest').array)]"
        },
        "emptyOutput": {
            "type": "bool",
            "value": "[empty(coalesce(parameters('objectToTest').null1, parameters('objectToTest').null2))]"
        }
    }
}
```

<span data-ttu-id="6d48d-172">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-172">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-173">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-173">Name</span></span> | <span data-ttu-id="6d48d-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-174">Type</span></span> | <span data-ttu-id="6d48d-175">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-176">stringOutput</span></span> | <span data-ttu-id="6d48d-177">String</span><span class="sxs-lookup"><span data-stu-id="6d48d-177">String</span></span> | <span data-ttu-id="6d48d-178">default</span><span class="sxs-lookup"><span data-stu-id="6d48d-178">default</span></span> |
| <span data-ttu-id="6d48d-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-179">intOutput</span></span> | <span data-ttu-id="6d48d-180">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-180">Int</span></span> | <span data-ttu-id="6d48d-181">1</span><span class="sxs-lookup"><span data-stu-id="6d48d-181">1</span></span> |
| <span data-ttu-id="6d48d-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-182">objectOutput</span></span> | <span data-ttu-id="6d48d-183">Objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-183">Object</span></span> | <span data-ttu-id="6d48d-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="6d48d-184">{"first": "default"}</span></span> |
| <span data-ttu-id="6d48d-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-185">arrayOutput</span></span> | <span data-ttu-id="6d48d-186">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-186">Array</span></span> | <span data-ttu-id="6d48d-187">[1]</span><span class="sxs-lookup"><span data-stu-id="6d48d-187">[1]</span></span> |
| <span data-ttu-id="6d48d-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-188">emptyOutput</span></span> | <span data-ttu-id="6d48d-189">Booleano</span><span class="sxs-lookup"><span data-stu-id="6d48d-189">Bool</span></span> | <span data-ttu-id="6d48d-190">True</span><span class="sxs-lookup"><span data-stu-id="6d48d-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="6d48d-191">concat</span><span class="sxs-lookup"><span data-stu-id="6d48d-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="6d48d-192">Combina varias matrices y devuelve una matriz concatenado de hello, o combina varios valores de cadena y devuelve la cadena Hola concatenado.</span><span class="sxs-lookup"><span data-stu-id="6d48d-192">Combines multiple arrays and returns hello concatenated array, or combines multiple string values and returns hello concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="6d48d-193">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-193">Parameters</span></span>

| <span data-ttu-id="6d48d-194">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-194">Parameter</span></span> | <span data-ttu-id="6d48d-195">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-195">Required</span></span> | <span data-ttu-id="6d48d-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-196">Type</span></span> | <span data-ttu-id="6d48d-197">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-198">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-198">arg1</span></span> |<span data-ttu-id="6d48d-199">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-199">Yes</span></span> |<span data-ttu-id="6d48d-200">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="6d48d-200">array or string</span></span> |<span data-ttu-id="6d48d-201">Hola primera matriz o cadena para la concatenación.</span><span class="sxs-lookup"><span data-stu-id="6d48d-201">hello first array or string for concatenation.</span></span> |
| <span data-ttu-id="6d48d-202">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="6d48d-202">additional arguments</span></span> |<span data-ttu-id="6d48d-203">No</span><span class="sxs-lookup"><span data-stu-id="6d48d-203">No</span></span> |<span data-ttu-id="6d48d-204">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="6d48d-204">array or string</span></span> |<span data-ttu-id="6d48d-205">Matrices o cadenas adicionales en orden secuencial para la concatenación.</span><span class="sxs-lookup"><span data-stu-id="6d48d-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="6d48d-206">Esta función puede tomar cualquier número de argumentos y puede aceptar cadenas o las matrices de parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-206">This function can take any number of arguments, and can accept either strings or arrays for hello parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="6d48d-207">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-207">Return value</span></span>
<span data-ttu-id="6d48d-208">Una cadena o matriz de valores concatenados.</span><span class="sxs-lookup"><span data-stu-id="6d48d-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-209">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-209">Example</span></span>

<span data-ttu-id="6d48d-210">Hola de ejemplo siguiente muestra cómo toocombine dos matrices.</span><span class="sxs-lookup"><span data-stu-id="6d48d-210">hello following example shows how toocombine two arrays.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "firstArray": { 
            "type": "array", 
            "defaultValue": [ 
                "1-1", 
                "1-2", 
                "1-3" 
            ] 
        },
        "secondArray": {
            "type": "array", 
            "defaultValue": [ 
                "2-1", 
                "2-2",
                "2-3" 
            ] 
        }
    },
    "resources": [
    ],
    "outputs": {
        "return": {
            "type": "array",
            "value": "[concat(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-211">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-211">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-212">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-212">Name</span></span> | <span data-ttu-id="6d48d-213">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-213">Type</span></span> | <span data-ttu-id="6d48d-214">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-215">return</span><span class="sxs-lookup"><span data-stu-id="6d48d-215">return</span></span> | <span data-ttu-id="6d48d-216">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-216">Array</span></span> | <span data-ttu-id="6d48d-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="6d48d-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="6d48d-218">Hola de ejemplo siguiente muestra cómo toocombine dos valores de cadena y devolver una cadena concatenada.</span><span class="sxs-lookup"><span data-stu-id="6d48d-218">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "prefix": {
            "type": "string",
            "defaultValue": "prefix"
        }
    },
    "resources": [],
    "outputs": {
        "concatOutput": {
            "value": "[concat(parameters('prefix'), '-', uniqueString(resourceGroup().id))]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="6d48d-219">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-219">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-220">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-220">Name</span></span> | <span data-ttu-id="6d48d-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-221">Type</span></span> | <span data-ttu-id="6d48d-222">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-223">concatOutput</span></span> | <span data-ttu-id="6d48d-224">String</span><span class="sxs-lookup"><span data-stu-id="6d48d-224">String</span></span> | <span data-ttu-id="6d48d-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="6d48d-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="6d48d-226">contains</span><span class="sxs-lookup"><span data-stu-id="6d48d-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="6d48d-227">Comprueba si una matriz contiene un valor, un objeto contiene una clave o una cadena contiene una subcadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-228">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-228">Parameters</span></span>

| <span data-ttu-id="6d48d-229">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-229">Parameter</span></span> | <span data-ttu-id="6d48d-230">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-230">Required</span></span> | <span data-ttu-id="6d48d-231">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-231">Type</span></span> | <span data-ttu-id="6d48d-232">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-233">container</span><span class="sxs-lookup"><span data-stu-id="6d48d-233">container</span></span> |<span data-ttu-id="6d48d-234">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-234">Yes</span></span> |<span data-ttu-id="6d48d-235">matriz, objeto o cadena</span><span class="sxs-lookup"><span data-stu-id="6d48d-235">array, object, or string</span></span> |<span data-ttu-id="6d48d-236">valor de Hola que contiene Hola valor toofind.</span><span class="sxs-lookup"><span data-stu-id="6d48d-236">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="6d48d-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="6d48d-237">itemToFind</span></span> |<span data-ttu-id="6d48d-238">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-238">Yes</span></span> |<span data-ttu-id="6d48d-239">cadena o entero</span><span class="sxs-lookup"><span data-stu-id="6d48d-239">string or int</span></span> |<span data-ttu-id="6d48d-240">Hola toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="6d48d-240">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-241">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-241">Return value</span></span>

<span data-ttu-id="6d48d-242">**True** si Hola elemento se encuentra; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="6d48d-242">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-243">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-243">Example</span></span>

<span data-ttu-id="6d48d-244">Hello en el ejemplo siguiente se muestra cómo toouse contiene con tipos diferentes:</span><span class="sxs-lookup"><span data-stu-id="6d48d-244">hello following example shows how toouse contains with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "OneTwoThree"
        },
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringTrue": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'e')]"
        },
        "stringFalse": {
            "type": "bool",
            "value": "[contains(parameters('stringToTest'), 'z')]"
        },
        "objectTrue": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'one')]"
        },
        "objectFalse": {
            "type": "bool",
            "value": "[contains(parameters('objectToTest'), 'a')]"
        },
        "arrayTrue": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'three')]"
        },
        "arrayFalse": {
            "type": "bool",
            "value": "[contains(parameters('arrayToTest'), 'four')]"
        }
    }
}
```

<span data-ttu-id="6d48d-245">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-246">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-246">Name</span></span> | <span data-ttu-id="6d48d-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-247">Type</span></span> | <span data-ttu-id="6d48d-248">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="6d48d-249">stringTrue</span></span> | <span data-ttu-id="6d48d-250">Booleano</span><span class="sxs-lookup"><span data-stu-id="6d48d-250">Bool</span></span> | <span data-ttu-id="6d48d-251">True</span><span class="sxs-lookup"><span data-stu-id="6d48d-251">True</span></span> |
| <span data-ttu-id="6d48d-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="6d48d-252">stringFalse</span></span> | <span data-ttu-id="6d48d-253">Booleano</span><span class="sxs-lookup"><span data-stu-id="6d48d-253">Bool</span></span> | <span data-ttu-id="6d48d-254">False</span><span class="sxs-lookup"><span data-stu-id="6d48d-254">False</span></span> |
| <span data-ttu-id="6d48d-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="6d48d-255">objectTrue</span></span> | <span data-ttu-id="6d48d-256">Booleano</span><span class="sxs-lookup"><span data-stu-id="6d48d-256">Bool</span></span> | <span data-ttu-id="6d48d-257">True</span><span class="sxs-lookup"><span data-stu-id="6d48d-257">True</span></span> |
| <span data-ttu-id="6d48d-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="6d48d-258">objectFalse</span></span> | <span data-ttu-id="6d48d-259">Booleano</span><span class="sxs-lookup"><span data-stu-id="6d48d-259">Bool</span></span> | <span data-ttu-id="6d48d-260">False</span><span class="sxs-lookup"><span data-stu-id="6d48d-260">False</span></span> |
| <span data-ttu-id="6d48d-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="6d48d-261">arrayTrue</span></span> | <span data-ttu-id="6d48d-262">Booleano</span><span class="sxs-lookup"><span data-stu-id="6d48d-262">Bool</span></span> | <span data-ttu-id="6d48d-263">True</span><span class="sxs-lookup"><span data-stu-id="6d48d-263">True</span></span> |
| <span data-ttu-id="6d48d-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="6d48d-264">arrayFalse</span></span> | <span data-ttu-id="6d48d-265">Booleano</span><span class="sxs-lookup"><span data-stu-id="6d48d-265">Bool</span></span> | <span data-ttu-id="6d48d-266">False</span><span class="sxs-lookup"><span data-stu-id="6d48d-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="6d48d-267">createarray</span><span class="sxs-lookup"><span data-stu-id="6d48d-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="6d48d-268">Crea una matriz de parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-268">Creates an array from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-269">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-269">Parameters</span></span>

| <span data-ttu-id="6d48d-270">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-270">Parameter</span></span> | <span data-ttu-id="6d48d-271">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-271">Required</span></span> | <span data-ttu-id="6d48d-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-272">Type</span></span> | <span data-ttu-id="6d48d-273">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-274">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-274">arg1</span></span> |<span data-ttu-id="6d48d-275">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-275">Yes</span></span> |<span data-ttu-id="6d48d-276">Cadena, entero, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="6d48d-277">Hola primer valor de matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-277">hello first value in hello array.</span></span> |
| <span data-ttu-id="6d48d-278">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="6d48d-278">additional arguments</span></span> |<span data-ttu-id="6d48d-279">No</span><span class="sxs-lookup"><span data-stu-id="6d48d-279">No</span></span> |<span data-ttu-id="6d48d-280">Cadena, entero, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="6d48d-281">Valores adicionales en la matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-281">Additional values in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-282">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-282">Return value</span></span>

<span data-ttu-id="6d48d-283">Una matriz.</span><span class="sxs-lookup"><span data-stu-id="6d48d-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-284">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-284">Example</span></span>

<span data-ttu-id="6d48d-285">Hola siguiente ejemplo se muestra cómo toouse createArray con tipos diferentes:</span><span class="sxs-lookup"><span data-stu-id="6d48d-285">hello following example shows how toouse createArray with different types:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "objectToTest": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "stringArray": {
            "type": "array",
            "value": "[createArray('a', 'b', 'c')]"
        },
        "intArray": {
            "type": "array",
            "value": "[createArray(1, 2, 3)]"
        },
        "objectArray": {
            "type": "array",
            "value": "[createArray(parameters('objectToTest'))]"
        },
        "arrayArray": {
            "type": "array",
            "value": "[createArray(parameters('arrayToTest'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-286">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-286">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-287">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-287">Name</span></span> | <span data-ttu-id="6d48d-288">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-288">Type</span></span> | <span data-ttu-id="6d48d-289">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="6d48d-290">stringArray</span></span> | <span data-ttu-id="6d48d-291">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-291">Array</span></span> | <span data-ttu-id="6d48d-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="6d48d-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="6d48d-293">intArray</span><span class="sxs-lookup"><span data-stu-id="6d48d-293">intArray</span></span> | <span data-ttu-id="6d48d-294">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-294">Array</span></span> | <span data-ttu-id="6d48d-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="6d48d-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="6d48d-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="6d48d-296">objectArray</span></span> | <span data-ttu-id="6d48d-297">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-297">Array</span></span> | <span data-ttu-id="6d48d-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="6d48d-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="6d48d-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="6d48d-299">arrayArray</span></span> | <span data-ttu-id="6d48d-300">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-300">Array</span></span> | <span data-ttu-id="6d48d-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="6d48d-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="6d48d-302">empty</span><span class="sxs-lookup"><span data-stu-id="6d48d-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="6d48d-303">Determina si una matriz, un objeto o una cadena están vacíos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-304">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-304">Parameters</span></span>

| <span data-ttu-id="6d48d-305">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-305">Parameter</span></span> | <span data-ttu-id="6d48d-306">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-306">Required</span></span> | <span data-ttu-id="6d48d-307">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-307">Type</span></span> | <span data-ttu-id="6d48d-308">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="6d48d-309">itemToTest</span></span> |<span data-ttu-id="6d48d-310">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-310">Yes</span></span> |<span data-ttu-id="6d48d-311">matriz, objeto o cadena</span><span class="sxs-lookup"><span data-stu-id="6d48d-311">array, object, or string</span></span> |<span data-ttu-id="6d48d-312">Hola toocheck valor si está vacía.</span><span class="sxs-lookup"><span data-stu-id="6d48d-312">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-313">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-313">Return value</span></span>

<span data-ttu-id="6d48d-314">Devuelve **True** si el valor de hello está vacía; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="6d48d-314">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-315">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-315">Example</span></span>

<span data-ttu-id="6d48d-316">Hola siguiente ejemplo comprueba si una matriz, el objeto y la cadena están vacías.</span><span class="sxs-lookup"><span data-stu-id="6d48d-316">hello following example checks whether an array, object, and string are empty.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": []
        },
        "testObject": {
            "type": "object",
            "defaultValue": {}
        },
        "testString": {
            "type": "string",
            "defaultValue": ""
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testArray'))]"
        },
        "objectEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testObject'))]"
        },
        "stringEmpty": {
            "type": "bool",
            "value": "[empty(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-317">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-317">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-318">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-318">Name</span></span> | <span data-ttu-id="6d48d-319">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-319">Type</span></span> | <span data-ttu-id="6d48d-320">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="6d48d-321">arrayEmpty</span></span> | <span data-ttu-id="6d48d-322">Booleano</span><span class="sxs-lookup"><span data-stu-id="6d48d-322">Bool</span></span> | <span data-ttu-id="6d48d-323">True</span><span class="sxs-lookup"><span data-stu-id="6d48d-323">True</span></span> |
| <span data-ttu-id="6d48d-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="6d48d-324">objectEmpty</span></span> | <span data-ttu-id="6d48d-325">Booleano</span><span class="sxs-lookup"><span data-stu-id="6d48d-325">Bool</span></span> | <span data-ttu-id="6d48d-326">True</span><span class="sxs-lookup"><span data-stu-id="6d48d-326">True</span></span> |
| <span data-ttu-id="6d48d-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="6d48d-327">stringEmpty</span></span> | <span data-ttu-id="6d48d-328">Booleano</span><span class="sxs-lookup"><span data-stu-id="6d48d-328">Bool</span></span> | <span data-ttu-id="6d48d-329">True</span><span class="sxs-lookup"><span data-stu-id="6d48d-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="6d48d-330">first</span><span class="sxs-lookup"><span data-stu-id="6d48d-330">first</span></span>
`first(arg1)`

<span data-ttu-id="6d48d-331">Devuelve Hola el primer elemento de matriz de Hola o el primer carácter de la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-331">Returns hello first element of hello array, or first character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-332">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-332">Parameters</span></span>

| <span data-ttu-id="6d48d-333">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-333">Parameter</span></span> | <span data-ttu-id="6d48d-334">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-334">Required</span></span> | <span data-ttu-id="6d48d-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-335">Type</span></span> | <span data-ttu-id="6d48d-336">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-337">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-337">arg1</span></span> |<span data-ttu-id="6d48d-338">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-338">Yes</span></span> |<span data-ttu-id="6d48d-339">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="6d48d-339">array or string</span></span> |<span data-ttu-id="6d48d-340">Hola valor tooretrieve Hola primer elemento o carácter.</span><span class="sxs-lookup"><span data-stu-id="6d48d-340">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-341">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-341">Return value</span></span>

<span data-ttu-id="6d48d-342">Hola tipo (string, int, matriz u objeto) del primer elemento en una matriz de Hola u Hola el primer carácter de una cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-342">hello type (string, int, array, or object) of hello first element in an array, or hello first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-343">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-343">Example</span></span>

<span data-ttu-id="6d48d-344">Hello en el ejemplo siguiente se muestra cómo toouse Hola primera función con una matriz y una cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-344">hello following example shows how toouse hello first function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[first(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[first('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="6d48d-345">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-345">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-346">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-346">Name</span></span> | <span data-ttu-id="6d48d-347">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-347">Type</span></span> | <span data-ttu-id="6d48d-348">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-349">arrayOutput</span></span> | <span data-ttu-id="6d48d-350">String</span><span class="sxs-lookup"><span data-stu-id="6d48d-350">String</span></span> | <span data-ttu-id="6d48d-351">one</span><span class="sxs-lookup"><span data-stu-id="6d48d-351">one</span></span> |
| <span data-ttu-id="6d48d-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-352">stringOutput</span></span> | <span data-ttu-id="6d48d-353">String</span><span class="sxs-lookup"><span data-stu-id="6d48d-353">String</span></span> | <span data-ttu-id="6d48d-354">O</span><span class="sxs-lookup"><span data-stu-id="6d48d-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="6d48d-355">intersección</span><span class="sxs-lookup"><span data-stu-id="6d48d-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="6d48d-356">Devuelve una matriz único o un objeto con elementos comunes de Hola de parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-356">Returns a single array or object with hello common elements from hello parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-357">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-357">Parameters</span></span>

| <span data-ttu-id="6d48d-358">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-358">Parameter</span></span> | <span data-ttu-id="6d48d-359">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-359">Required</span></span> | <span data-ttu-id="6d48d-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-360">Type</span></span> | <span data-ttu-id="6d48d-361">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-362">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-362">arg1</span></span> |<span data-ttu-id="6d48d-363">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-363">Yes</span></span> |<span data-ttu-id="6d48d-364">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-364">array or object</span></span> |<span data-ttu-id="6d48d-365">Hola primer toouse de valor para buscar elementos comunes.</span><span class="sxs-lookup"><span data-stu-id="6d48d-365">hello first value toouse for finding common elements.</span></span> |
| <span data-ttu-id="6d48d-366">arg2</span><span class="sxs-lookup"><span data-stu-id="6d48d-366">arg2</span></span> |<span data-ttu-id="6d48d-367">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-367">Yes</span></span> |<span data-ttu-id="6d48d-368">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-368">array or object</span></span> |<span data-ttu-id="6d48d-369">Hola segundo toouse de valor para buscar elementos comunes.</span><span class="sxs-lookup"><span data-stu-id="6d48d-369">hello second value toouse for finding common elements.</span></span> |
| <span data-ttu-id="6d48d-370">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="6d48d-370">additional arguments</span></span> |<span data-ttu-id="6d48d-371">No</span><span class="sxs-lookup"><span data-stu-id="6d48d-371">No</span></span> |<span data-ttu-id="6d48d-372">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-372">array or object</span></span> |<span data-ttu-id="6d48d-373">Toouse valores adicionales para buscar elementos comunes.</span><span class="sxs-lookup"><span data-stu-id="6d48d-373">Additional values toouse for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-374">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-374">Return value</span></span>

<span data-ttu-id="6d48d-375">Una matriz o un objeto con elementos comunes de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-375">An array or object with hello common elements.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-376">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-376">Example</span></span>

<span data-ttu-id="6d48d-377">Hola de ejemplo siguiente muestra cómo toouse intersección con las matrices y los objetos:</span><span class="sxs-lookup"><span data-stu-id="6d48d-377">hello following example shows how toouse intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "z", "three": "c"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[intersection(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[intersection(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-378">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-378">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-379">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-379">Name</span></span> | <span data-ttu-id="6d48d-380">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-380">Type</span></span> | <span data-ttu-id="6d48d-381">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-382">objectOutput</span></span> | <span data-ttu-id="6d48d-383">Objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-383">Object</span></span> | <span data-ttu-id="6d48d-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="6d48d-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="6d48d-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-385">arrayOutput</span></span> | <span data-ttu-id="6d48d-386">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-386">Array</span></span> | <span data-ttu-id="6d48d-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="6d48d-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="6d48d-388">json</span><span class="sxs-lookup"><span data-stu-id="6d48d-388">json</span></span>
`json(arg1)`

<span data-ttu-id="6d48d-389">Devuelve un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="6d48d-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-390">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-390">Parameters</span></span>

| <span data-ttu-id="6d48d-391">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-391">Parameter</span></span> | <span data-ttu-id="6d48d-392">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-392">Required</span></span> | <span data-ttu-id="6d48d-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-393">Type</span></span> | <span data-ttu-id="6d48d-394">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-395">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-395">arg1</span></span> |<span data-ttu-id="6d48d-396">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-396">Yes</span></span> |<span data-ttu-id="6d48d-397">cadena</span><span class="sxs-lookup"><span data-stu-id="6d48d-397">string</span></span> |<span data-ttu-id="6d48d-398">Hola valor tooconvert tooJSON.</span><span class="sxs-lookup"><span data-stu-id="6d48d-398">hello value tooconvert tooJSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="6d48d-399">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-399">Return value</span></span>

<span data-ttu-id="6d48d-400">Especifica el objeto JSON de Hola de hello cadena o un objeto vacío cuando **null** se especifica.</span><span class="sxs-lookup"><span data-stu-id="6d48d-400">hello JSON object from hello specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-401">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-401">Example</span></span>

<span data-ttu-id="6d48d-402">Hola de ejemplo siguiente muestra cómo toouse intersección con las matrices y los objetos:</span><span class="sxs-lookup"><span data-stu-id="6d48d-402">hello following example shows how toouse intersection with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "jsonOutput": {
            "type": "object",
            "value": "[json('{\"a\": \"b\"}')]"
        },
        "nullOutput": {
            "type": "bool",
            "value": "[empty(json('null'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-403">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-403">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-404">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-404">Name</span></span> | <span data-ttu-id="6d48d-405">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-405">Type</span></span> | <span data-ttu-id="6d48d-406">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-407">jsonOutput</span></span> | <span data-ttu-id="6d48d-408">Objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-408">Object</span></span> | <span data-ttu-id="6d48d-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="6d48d-409">{"a": "b"}</span></span> |
| <span data-ttu-id="6d48d-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-410">nullOutput</span></span> | <span data-ttu-id="6d48d-411">boolean</span><span class="sxs-lookup"><span data-stu-id="6d48d-411">Boolean</span></span> | <span data-ttu-id="6d48d-412">True</span><span class="sxs-lookup"><span data-stu-id="6d48d-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="6d48d-413">last</span><span class="sxs-lookup"><span data-stu-id="6d48d-413">last</span></span>
`last (arg1)`

<span data-ttu-id="6d48d-414">Devuelve Hola último elemento de matriz de Hola o último carácter de la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-414">Returns hello last element of hello array, or last character of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-415">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-415">Parameters</span></span>

| <span data-ttu-id="6d48d-416">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-416">Parameter</span></span> | <span data-ttu-id="6d48d-417">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-417">Required</span></span> | <span data-ttu-id="6d48d-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-418">Type</span></span> | <span data-ttu-id="6d48d-419">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-420">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-420">arg1</span></span> |<span data-ttu-id="6d48d-421">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-421">Yes</span></span> |<span data-ttu-id="6d48d-422">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="6d48d-422">array or string</span></span> |<span data-ttu-id="6d48d-423">Hola value tooretrieve Hola última (elemento) o carácter.</span><span class="sxs-lookup"><span data-stu-id="6d48d-423">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-424">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-424">Return value</span></span>

<span data-ttu-id="6d48d-425">Hola tipo (string, int, matriz u objeto) del último elemento en una matriz de Hola u Hola último carácter de una cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-425">hello type (string, int, array, or object) of hello last element in an array, or hello last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-426">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-426">Example</span></span>

<span data-ttu-id="6d48d-427">Hello en el ejemplo siguiente se muestra cómo toouse Hola última función con una matriz y una cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-427">hello following example shows how toouse hello last function with an array and string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "arrayOutput": {
            "type": "string",
            "value": "[last(parameters('arrayToTest'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[last('One Two Three')]"
        }
    }
}
```

<span data-ttu-id="6d48d-428">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-429">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-429">Name</span></span> | <span data-ttu-id="6d48d-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-430">Type</span></span> | <span data-ttu-id="6d48d-431">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-432">arrayOutput</span></span> | <span data-ttu-id="6d48d-433">String</span><span class="sxs-lookup"><span data-stu-id="6d48d-433">String</span></span> | <span data-ttu-id="6d48d-434">three</span><span class="sxs-lookup"><span data-stu-id="6d48d-434">three</span></span> |
| <span data-ttu-id="6d48d-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-435">stringOutput</span></span> | <span data-ttu-id="6d48d-436">String</span><span class="sxs-lookup"><span data-stu-id="6d48d-436">String</span></span> | <span data-ttu-id="6d48d-437">e</span><span class="sxs-lookup"><span data-stu-id="6d48d-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="6d48d-438">length</span><span class="sxs-lookup"><span data-stu-id="6d48d-438">length</span></span>
`length(arg1)`

<span data-ttu-id="6d48d-439">Devuelve el número de Hola de elementos de una matriz o caracteres de una cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-439">Returns hello number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-440">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-440">Parameters</span></span>

| <span data-ttu-id="6d48d-441">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-441">Parameter</span></span> | <span data-ttu-id="6d48d-442">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-442">Required</span></span> | <span data-ttu-id="6d48d-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-443">Type</span></span> | <span data-ttu-id="6d48d-444">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-445">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-445">arg1</span></span> |<span data-ttu-id="6d48d-446">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-446">Yes</span></span> |<span data-ttu-id="6d48d-447">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="6d48d-447">array or string</span></span> |<span data-ttu-id="6d48d-448">Hola toouse de matriz para obtener el número de Hola de elementos u Hola toouse de cadena para obtener el número de Hola de caracteres.</span><span class="sxs-lookup"><span data-stu-id="6d48d-448">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-449">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-449">Return value</span></span>

<span data-ttu-id="6d48d-450">Un entero.</span><span class="sxs-lookup"><span data-stu-id="6d48d-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="6d48d-451">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-451">Example</span></span>

<span data-ttu-id="6d48d-452">Hola siguiente ejemplo se muestra cómo toouse longitud con una matriz y la cadena:</span><span class="sxs-lookup"><span data-stu-id="6d48d-452">hello following example shows how toouse length with an array and string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "stringToTest": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "arrayLength": {
            "type": "int",
            "value": "[length(parameters('arrayToTest'))]"
        },
        "stringLength": {
            "type": "int",
            "value": "[length(parameters('stringToTest'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-453">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-453">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-454">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-454">Name</span></span> | <span data-ttu-id="6d48d-455">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-455">Type</span></span> | <span data-ttu-id="6d48d-456">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="6d48d-457">arrayLength</span></span> | <span data-ttu-id="6d48d-458">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-458">Int</span></span> | <span data-ttu-id="6d48d-459">3</span><span class="sxs-lookup"><span data-stu-id="6d48d-459">3</span></span> |
| <span data-ttu-id="6d48d-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="6d48d-460">stringLength</span></span> | <span data-ttu-id="6d48d-461">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-461">Int</span></span> | <span data-ttu-id="6d48d-462">13</span><span class="sxs-lookup"><span data-stu-id="6d48d-462">13</span></span> |

<span data-ttu-id="6d48d-463">Puede usar esta función con un número de iteraciones Hola de toospecify de matriz al crear recursos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-463">You can use this function with an array toospecify hello number of iterations when creating resources.</span></span> <span data-ttu-id="6d48d-464">En el siguiente ejemplo de Hola Hola parámetro **siteNames** haría referencia tooan matriz de nombres toouse al crear sitios web de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-464">In hello following example, hello parameter **siteNames** would refer tooan array of names toouse when creating hello web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="6d48d-465">Para más información sobre cómo usar esta función con una matriz, vea [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="6d48d-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="6d48d-466">Min</span><span class="sxs-lookup"><span data-stu-id="6d48d-466">min</span></span>
`min(arg1)`

<span data-ttu-id="6d48d-467">Devuelve Hola valor mínimo de una matriz de enteros o una lista separada por comas de números enteros.</span><span class="sxs-lookup"><span data-stu-id="6d48d-467">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-468">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-468">Parameters</span></span>

| <span data-ttu-id="6d48d-469">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-469">Parameter</span></span> | <span data-ttu-id="6d48d-470">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-470">Required</span></span> | <span data-ttu-id="6d48d-471">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-471">Type</span></span> | <span data-ttu-id="6d48d-472">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-473">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-473">arg1</span></span> |<span data-ttu-id="6d48d-474">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-474">Yes</span></span> |<span data-ttu-id="6d48d-475">matriz de enteros, o lista separada por comas de enteros</span><span class="sxs-lookup"><span data-stu-id="6d48d-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="6d48d-476">Hola tooget Hola mínimo valor de la colección.</span><span class="sxs-lookup"><span data-stu-id="6d48d-476">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-477">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-477">Return value</span></span>

<span data-ttu-id="6d48d-478">Un entero que representa el valor mínimo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-478">An int representing hello minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-479">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-479">Example</span></span>

<span data-ttu-id="6d48d-480">Hola siguiente ejemplo se muestra cómo min toouse con una matriz y una lista de enteros:</span><span class="sxs-lookup"><span data-stu-id="6d48d-480">hello following example shows how toouse min with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[min(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[min(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="6d48d-481">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-481">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-482">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-482">Name</span></span> | <span data-ttu-id="6d48d-483">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-483">Type</span></span> | <span data-ttu-id="6d48d-484">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-485">arrayOutput</span></span> | <span data-ttu-id="6d48d-486">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-486">Int</span></span> | <span data-ttu-id="6d48d-487">0</span><span class="sxs-lookup"><span data-stu-id="6d48d-487">0</span></span> |
| <span data-ttu-id="6d48d-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-488">intOutput</span></span> | <span data-ttu-id="6d48d-489">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-489">Int</span></span> | <span data-ttu-id="6d48d-490">0</span><span class="sxs-lookup"><span data-stu-id="6d48d-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="6d48d-491">max</span><span class="sxs-lookup"><span data-stu-id="6d48d-491">max</span></span>
`max(arg1)`

<span data-ttu-id="6d48d-492">Devuelve Hola valor máximo de una matriz de enteros o una lista separada por comas de números enteros.</span><span class="sxs-lookup"><span data-stu-id="6d48d-492">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-493">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-493">Parameters</span></span>

| <span data-ttu-id="6d48d-494">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-494">Parameter</span></span> | <span data-ttu-id="6d48d-495">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-495">Required</span></span> | <span data-ttu-id="6d48d-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-496">Type</span></span> | <span data-ttu-id="6d48d-497">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-498">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-498">arg1</span></span> |<span data-ttu-id="6d48d-499">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-499">Yes</span></span> |<span data-ttu-id="6d48d-500">matriz de enteros, o lista separada por comas de enteros</span><span class="sxs-lookup"><span data-stu-id="6d48d-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="6d48d-501">Hola tooget Hola máximo valor de la colección.</span><span class="sxs-lookup"><span data-stu-id="6d48d-501">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-502">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-502">Return value</span></span>

<span data-ttu-id="6d48d-503">Un entero que representa el valor máximo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-503">An int representing hello maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-504">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-504">Example</span></span>

<span data-ttu-id="6d48d-505">Hola siguiente ejemplo se muestra cómo toouse máximo con una matriz y una lista de enteros:</span><span class="sxs-lookup"><span data-stu-id="6d48d-505">hello following example shows how toouse max with an array and a list of integers:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "arrayToTest": {
            "type": "array",
            "defaultValue": [0,3,2,5,4]
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "int",
            "value": "[max(parameters('arrayToTest'))]"
        },
        "intOutput": {
            "type": "int",
            "value": "[max(0,3,2,5,4)]"
        }
    }
}
```

<span data-ttu-id="6d48d-506">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-506">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-507">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-507">Name</span></span> | <span data-ttu-id="6d48d-508">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-508">Type</span></span> | <span data-ttu-id="6d48d-509">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-510">arrayOutput</span></span> | <span data-ttu-id="6d48d-511">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-511">Int</span></span> | <span data-ttu-id="6d48d-512">5</span><span class="sxs-lookup"><span data-stu-id="6d48d-512">5</span></span> |
| <span data-ttu-id="6d48d-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-513">intOutput</span></span> | <span data-ttu-id="6d48d-514">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-514">Int</span></span> | <span data-ttu-id="6d48d-515">5</span><span class="sxs-lookup"><span data-stu-id="6d48d-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="6d48d-516">range</span><span class="sxs-lookup"><span data-stu-id="6d48d-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="6d48d-517">Crea una matriz de enteros a partir de un entero de inicio y contiene un número de elementos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-518">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-518">Parameters</span></span>

| <span data-ttu-id="6d48d-519">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-519">Parameter</span></span> | <span data-ttu-id="6d48d-520">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-520">Required</span></span> | <span data-ttu-id="6d48d-521">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-521">Type</span></span> | <span data-ttu-id="6d48d-522">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="6d48d-523">startingInteger</span></span> |<span data-ttu-id="6d48d-524">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-524">Yes</span></span> |<span data-ttu-id="6d48d-525">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-525">int</span></span> |<span data-ttu-id="6d48d-526">primer entero de Hello en la matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-526">hello first integer in hello array.</span></span> |
| <span data-ttu-id="6d48d-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="6d48d-527">numberofElements</span></span> |<span data-ttu-id="6d48d-528">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-528">Yes</span></span> |<span data-ttu-id="6d48d-529">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-529">int</span></span> |<span data-ttu-id="6d48d-530">número de Hola de enteros en la matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-530">hello number of integers in hello array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-531">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-531">Return value</span></span>

<span data-ttu-id="6d48d-532">Una matriz de enteros.</span><span class="sxs-lookup"><span data-stu-id="6d48d-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-533">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-533">Example</span></span>

<span data-ttu-id="6d48d-534">Hola de ejemplo siguiente muestra cómo toouse Hola función intervalo:</span><span class="sxs-lookup"><span data-stu-id="6d48d-534">hello following example shows how toouse hello range function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "startingInt": {
            "type": "int",
            "defaultValue": 5
        },
        "numberOfElements": {
            "type": "int",
            "defaultValue": 3
        }
    },
    "resources": [],
    "outputs": {
        "rangeOutput": {
            "type": "array",
            "value": "[range(parameters('startingInt'),parameters('numberOfElements'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-535">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-535">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-536">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-536">Name</span></span> | <span data-ttu-id="6d48d-537">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-537">Type</span></span> | <span data-ttu-id="6d48d-538">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-539">rangeOutput</span></span> | <span data-ttu-id="6d48d-540">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-540">Array</span></span> | <span data-ttu-id="6d48d-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="6d48d-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="6d48d-542">skip</span><span class="sxs-lookup"><span data-stu-id="6d48d-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="6d48d-543">Devuelve una matriz con todos los elementos de hello después Hola número especificado en la matriz de Hola o devuelve una cadena con todos los caracteres de hello después Hola el número especificado en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-543">Returns an array with all hello elements after hello specified number in hello array, or returns a string with all hello characters after hello specified number in hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-544">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-544">Parameters</span></span>

| <span data-ttu-id="6d48d-545">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-545">Parameter</span></span> | <span data-ttu-id="6d48d-546">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-546">Required</span></span> | <span data-ttu-id="6d48d-547">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-547">Type</span></span> | <span data-ttu-id="6d48d-548">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="6d48d-549">originalValue</span></span> |<span data-ttu-id="6d48d-550">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-550">Yes</span></span> |<span data-ttu-id="6d48d-551">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="6d48d-551">array or string</span></span> |<span data-ttu-id="6d48d-552">Hola toouse de matriz o de cadena para pasar por alto.</span><span class="sxs-lookup"><span data-stu-id="6d48d-552">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="6d48d-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="6d48d-553">numberToSkip</span></span> |<span data-ttu-id="6d48d-554">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-554">Yes</span></span> |<span data-ttu-id="6d48d-555">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-555">int</span></span> |<span data-ttu-id="6d48d-556">número de Hola de tooskip elementos o caracteres.</span><span class="sxs-lookup"><span data-stu-id="6d48d-556">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="6d48d-557">Si este valor es 0 o menos, todos los elementos de Hola o se devuelven los caracteres en valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-557">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="6d48d-558">Si es mayor que la longitud de cadena o matriz de Hola Hola, se devuelve una matriz vacía o una cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-558">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-559">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-559">Return value</span></span>

<span data-ttu-id="6d48d-560">Una matriz o cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-561">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-561">Example</span></span>

<span data-ttu-id="6d48d-562">Hola siguiendo el ejemplo omite Hola número especificado de elementos de matriz de Hola y Hola especifica el número de caracteres en una cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-562">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToSkip": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToSkip": {
            "type": "int",
            "defaultValue": 4
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[skip(parameters('testArray'),parameters('elementsToSkip'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[skip(parameters('testString'),parameters('charactersToSkip'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-563">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-563">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-564">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-564">Name</span></span> | <span data-ttu-id="6d48d-565">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-565">Type</span></span> | <span data-ttu-id="6d48d-566">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-567">arrayOutput</span></span> | <span data-ttu-id="6d48d-568">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-568">Array</span></span> | <span data-ttu-id="6d48d-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="6d48d-569">["three"]</span></span> |
| <span data-ttu-id="6d48d-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-570">stringOutput</span></span> | <span data-ttu-id="6d48d-571">String</span><span class="sxs-lookup"><span data-stu-id="6d48d-571">String</span></span> | <span data-ttu-id="6d48d-572">two three</span><span class="sxs-lookup"><span data-stu-id="6d48d-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="6d48d-573">take</span><span class="sxs-lookup"><span data-stu-id="6d48d-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="6d48d-574">Devuelve una matriz con hello un número especificado de elementos de Hola inicio de matriz de hello, o una cadena con hello número especificado de caracteres desde el principio de Hola de cadena Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-574">Returns an array with hello specified number of elements from hello start of hello array, or a string with hello specified number of characters from hello start of hello string.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-575">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-575">Parameters</span></span>

| <span data-ttu-id="6d48d-576">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-576">Parameter</span></span> | <span data-ttu-id="6d48d-577">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-577">Required</span></span> | <span data-ttu-id="6d48d-578">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-578">Type</span></span> | <span data-ttu-id="6d48d-579">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="6d48d-580">originalValue</span></span> |<span data-ttu-id="6d48d-581">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-581">Yes</span></span> |<span data-ttu-id="6d48d-582">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="6d48d-582">array or string</span></span> |<span data-ttu-id="6d48d-583">Hola array o string tootake Hola elementos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-583">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="6d48d-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="6d48d-584">numberToTake</span></span> |<span data-ttu-id="6d48d-585">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-585">Yes</span></span> |<span data-ttu-id="6d48d-586">int</span><span class="sxs-lookup"><span data-stu-id="6d48d-586">int</span></span> |<span data-ttu-id="6d48d-587">número de Hola de tootake elementos o caracteres.</span><span class="sxs-lookup"><span data-stu-id="6d48d-587">hello number of elements or characters tootake.</span></span> <span data-ttu-id="6d48d-588">Si este valor es 0 o un valor inferior, se devolverá una matriz o cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="6d48d-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="6d48d-589">Si es mayor que la longitud de Hola de hello con cadena o una matriz, se devuelven todos los elementos de hello en la matriz de Hola o de cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-589">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-590">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-590">Return value</span></span>

<span data-ttu-id="6d48d-591">Una matriz o cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-592">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-592">Example</span></span>

<span data-ttu-id="6d48d-593">Hola siguiendo el ejemplo hello de toma un número especificado de elementos de matriz de Hola y los caracteres de una cadena.</span><span class="sxs-lookup"><span data-stu-id="6d48d-593">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testArray": {
            "type": "array",
            "defaultValue": [
                "one",
                "two",
                "three"
            ]
        },
        "elementsToTake": {
            "type": "int",
            "defaultValue": 2
        },
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        },
        "charactersToTake": {
            "type": "int",
            "defaultValue": 2
        }
    },
    "resources": [],
    "outputs": {
        "arrayOutput": {
            "type": "array",
            "value": "[take(parameters('testArray'),parameters('elementsToTake'))]"
        },
        "stringOutput": {
            "type": "string",
            "value": "[take(parameters('testString'),parameters('charactersToTake'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-594">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-594">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-595">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-595">Name</span></span> | <span data-ttu-id="6d48d-596">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-596">Type</span></span> | <span data-ttu-id="6d48d-597">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-598">arrayOutput</span></span> | <span data-ttu-id="6d48d-599">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-599">Array</span></span> | <span data-ttu-id="6d48d-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="6d48d-600">["one", "two"]</span></span> |
| <span data-ttu-id="6d48d-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-601">stringOutput</span></span> | <span data-ttu-id="6d48d-602">String</span><span class="sxs-lookup"><span data-stu-id="6d48d-602">String</span></span> | <span data-ttu-id="6d48d-603">en</span><span class="sxs-lookup"><span data-stu-id="6d48d-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="6d48d-604">union</span><span class="sxs-lookup"><span data-stu-id="6d48d-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="6d48d-605">Devuelve una matriz único o un objeto con todos los elementos de parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d48d-605">Returns a single array or object with all elements from hello parameters.</span></span> <span data-ttu-id="6d48d-606">Los valores o las claves duplicados solo se incluyen una vez.</span><span class="sxs-lookup"><span data-stu-id="6d48d-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="6d48d-607">parameters</span><span class="sxs-lookup"><span data-stu-id="6d48d-607">Parameters</span></span>

| <span data-ttu-id="6d48d-608">Parámetro</span><span class="sxs-lookup"><span data-stu-id="6d48d-608">Parameter</span></span> | <span data-ttu-id="6d48d-609">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="6d48d-609">Required</span></span> | <span data-ttu-id="6d48d-610">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-610">Type</span></span> | <span data-ttu-id="6d48d-611">Descripción</span><span class="sxs-lookup"><span data-stu-id="6d48d-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="6d48d-612">arg1</span><span class="sxs-lookup"><span data-stu-id="6d48d-612">arg1</span></span> |<span data-ttu-id="6d48d-613">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-613">Yes</span></span> |<span data-ttu-id="6d48d-614">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-614">array or object</span></span> |<span data-ttu-id="6d48d-615">Hola primer valor toouse para combinar elementos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-615">hello first value toouse for joining elements.</span></span> |
| <span data-ttu-id="6d48d-616">arg2</span><span class="sxs-lookup"><span data-stu-id="6d48d-616">arg2</span></span> |<span data-ttu-id="6d48d-617">Sí</span><span class="sxs-lookup"><span data-stu-id="6d48d-617">Yes</span></span> |<span data-ttu-id="6d48d-618">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-618">array or object</span></span> |<span data-ttu-id="6d48d-619">Hola segundo valor toouse para combinar elementos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-619">hello second value toouse for joining elements.</span></span> |
| <span data-ttu-id="6d48d-620">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="6d48d-620">additional arguments</span></span> |<span data-ttu-id="6d48d-621">No</span><span class="sxs-lookup"><span data-stu-id="6d48d-621">No</span></span> |<span data-ttu-id="6d48d-622">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-622">array or object</span></span> |<span data-ttu-id="6d48d-623">Toouse valores adicionales para combinar elementos.</span><span class="sxs-lookup"><span data-stu-id="6d48d-623">Additional values toouse for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="6d48d-624">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="6d48d-624">Return value</span></span>

<span data-ttu-id="6d48d-625">Una matriz u objeto.</span><span class="sxs-lookup"><span data-stu-id="6d48d-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="6d48d-626">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d48d-626">Example</span></span>

<span data-ttu-id="6d48d-627">Hola de ejemplo siguiente muestra cómo toouse unión con las matrices y los objetos:</span><span class="sxs-lookup"><span data-stu-id="6d48d-627">hello following example shows how toouse union with arrays and objects:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstObject": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b", "three": "c"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"three": "c", "four": "d", "five": "e"}
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["one", "two", "three"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["three", "four"]
        }
    },
    "resources": [
    ],
    "outputs": {
        "objectOutput": {
            "type": "object",
            "value": "[union(parameters('firstObject'), parameters('secondObject'))]"
        },
        "arrayOutput": {
            "type": "array",
            "value": "[union(parameters('firstArray'), parameters('secondArray'))]"
        }
    }
}
```

<span data-ttu-id="6d48d-628">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="6d48d-628">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="6d48d-629">Nombre</span><span class="sxs-lookup"><span data-stu-id="6d48d-629">Name</span></span> | <span data-ttu-id="6d48d-630">Tipo</span><span class="sxs-lookup"><span data-stu-id="6d48d-630">Type</span></span> | <span data-ttu-id="6d48d-631">Valor</span><span class="sxs-lookup"><span data-stu-id="6d48d-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="6d48d-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-632">objectOutput</span></span> | <span data-ttu-id="6d48d-633">Objeto</span><span class="sxs-lookup"><span data-stu-id="6d48d-633">Object</span></span> | <span data-ttu-id="6d48d-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="6d48d-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="6d48d-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="6d48d-635">arrayOutput</span></span> | <span data-ttu-id="6d48d-636">Matriz</span><span class="sxs-lookup"><span data-stu-id="6d48d-636">Array</span></span> | <span data-ttu-id="6d48d-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="6d48d-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6d48d-638">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d48d-638">Next steps</span></span>
* <span data-ttu-id="6d48d-639">Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6d48d-639">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="6d48d-640">toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6d48d-640">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="6d48d-641">tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="6d48d-641">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="6d48d-642">toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6d48d-642">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

