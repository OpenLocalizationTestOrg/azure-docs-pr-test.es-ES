---
title: 'Funciones de la plantilla de Azure Resource Manager: matrices y objetos | Microsoft Docs'
description: Describe las funciones para usar en una plantilla de Azure Resource Manager para trabajar con matrices y objetos.
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
ms.openlocfilehash: 0bd9ec41761c9ce575f3bcf4d1f8e8578b83e01c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="69823-103">Funciones de matriz y de objeto para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="69823-103">Array and object functions for Azure Resource Manager templates</span></span> 

<span data-ttu-id="69823-104">Resource Manager ofrece varias funciones para trabajar con matrices y objetos.</span><span class="sxs-lookup"><span data-stu-id="69823-104">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="69823-105">matriz</span><span class="sxs-lookup"><span data-stu-id="69823-105">array</span></span>](#array)
* [<span data-ttu-id="69823-106">coalesce</span><span class="sxs-lookup"><span data-stu-id="69823-106">coalesce</span></span>](#coalesce)
* [<span data-ttu-id="69823-107">concat</span><span class="sxs-lookup"><span data-stu-id="69823-107">concat</span></span>](#concat)
* [<span data-ttu-id="69823-108">contains</span><span class="sxs-lookup"><span data-stu-id="69823-108">contains</span></span>](#contains)
* [<span data-ttu-id="69823-109">createArray</span><span class="sxs-lookup"><span data-stu-id="69823-109">createArray</span></span>](#createarray)
* [<span data-ttu-id="69823-110">empty</span><span class="sxs-lookup"><span data-stu-id="69823-110">empty</span></span>](#empty)
* [<span data-ttu-id="69823-111">first</span><span class="sxs-lookup"><span data-stu-id="69823-111">first</span></span>](#first)
* [<span data-ttu-id="69823-112">intersection</span><span class="sxs-lookup"><span data-stu-id="69823-112">intersection</span></span>](#intersection)
* [<span data-ttu-id="69823-113">json</span><span class="sxs-lookup"><span data-stu-id="69823-113">json</span></span>](#json)
* [<span data-ttu-id="69823-114">last</span><span class="sxs-lookup"><span data-stu-id="69823-114">last</span></span>](#last)
* [<span data-ttu-id="69823-115">length</span><span class="sxs-lookup"><span data-stu-id="69823-115">length</span></span>](#length)
* [<span data-ttu-id="69823-116">min</span><span class="sxs-lookup"><span data-stu-id="69823-116">min</span></span>](#min)
* [<span data-ttu-id="69823-117">max</span><span class="sxs-lookup"><span data-stu-id="69823-117">max</span></span>](#max)
* [<span data-ttu-id="69823-118">range</span><span class="sxs-lookup"><span data-stu-id="69823-118">range</span></span>](#range)
* [<span data-ttu-id="69823-119">skip</span><span class="sxs-lookup"><span data-stu-id="69823-119">skip</span></span>](#skip)
* [<span data-ttu-id="69823-120">take</span><span class="sxs-lookup"><span data-stu-id="69823-120">take</span></span>](#take)
* [<span data-ttu-id="69823-121">union</span><span class="sxs-lookup"><span data-stu-id="69823-121">union</span></span>](#union)

<span data-ttu-id="69823-122">Para obtener una matriz de valores de cadena delimitada por un valor, consulte [split](resource-group-template-functions-string.md#split).</span><span class="sxs-lookup"><span data-stu-id="69823-122">To get an array of string values delimited by a value, see [split](resource-group-template-functions-string.md#split).</span></span>

<a id="array" />

## <a name="array"></a><span data-ttu-id="69823-123">array</span><span class="sxs-lookup"><span data-stu-id="69823-123">array</span></span>
`array(convertToArray)`

<span data-ttu-id="69823-124">Convierte el valor en una matriz.</span><span class="sxs-lookup"><span data-stu-id="69823-124">Converts the value to an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-125">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-125">Parameters</span></span>

| <span data-ttu-id="69823-126">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-126">Parameter</span></span> | <span data-ttu-id="69823-127">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-127">Required</span></span> | <span data-ttu-id="69823-128">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-128">Type</span></span> | <span data-ttu-id="69823-129">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-129">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-130">convertToArray</span><span class="sxs-lookup"><span data-stu-id="69823-130">convertToArray</span></span> |<span data-ttu-id="69823-131">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-131">Yes</span></span> |<span data-ttu-id="69823-132">entero, cadena, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-132">int, string, array, or object</span></span> |<span data-ttu-id="69823-133">Valor que se convierte en matriz.</span><span class="sxs-lookup"><span data-stu-id="69823-133">The value to convert to an array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-134">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-134">Return value</span></span>

<span data-ttu-id="69823-135">Una matriz.</span><span class="sxs-lookup"><span data-stu-id="69823-135">An array.</span></span>

### <a name="example"></a><span data-ttu-id="69823-136">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-136">Example</span></span>

<span data-ttu-id="69823-137">En el ejemplo siguiente se muestra cómo utilizar la función de matriz con diferentes tipos.</span><span class="sxs-lookup"><span data-stu-id="69823-137">The following example shows how to use the array function with different types.</span></span>

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

<span data-ttu-id="69823-138">El resultado del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-138">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-139">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-139">Name</span></span> | <span data-ttu-id="69823-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-140">Type</span></span> | <span data-ttu-id="69823-141">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-141">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-142">intOutput</span><span class="sxs-lookup"><span data-stu-id="69823-142">intOutput</span></span> | <span data-ttu-id="69823-143">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-143">Array</span></span> | <span data-ttu-id="69823-144">[1]</span><span class="sxs-lookup"><span data-stu-id="69823-144">[1]</span></span> |
| <span data-ttu-id="69823-145">stringOutput</span><span class="sxs-lookup"><span data-stu-id="69823-145">stringOutput</span></span> | <span data-ttu-id="69823-146">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-146">Array</span></span> | <span data-ttu-id="69823-147">["a"]</span><span class="sxs-lookup"><span data-stu-id="69823-147">["a"]</span></span> |
| <span data-ttu-id="69823-148">objectOutput</span><span class="sxs-lookup"><span data-stu-id="69823-148">objectOutput</span></span> | <span data-ttu-id="69823-149">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-149">Array</span></span> | <span data-ttu-id="69823-150">[{"a": "b", "c": "d"}]</span><span class="sxs-lookup"><span data-stu-id="69823-150">[{"a": "b", "c": "d"}]</span></span> |

<a id="coalesce" />

## <a name="coalesce"></a><span data-ttu-id="69823-151">coalesce</span><span class="sxs-lookup"><span data-stu-id="69823-151">coalesce</span></span>
`coalesce(arg1, arg2, arg3, ...)`

<span data-ttu-id="69823-152">Devuelve el primer valor no nulo de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="69823-152">Returns first non-null value from the parameters.</span></span> <span data-ttu-id="69823-153">Las cadenas vacías, las matrices vacías y los objetos vacíos no son nulos.</span><span class="sxs-lookup"><span data-stu-id="69823-153">Empty strings, empty arrays, and empty objects are not null.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-154">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-154">Parameters</span></span>

| <span data-ttu-id="69823-155">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-155">Parameter</span></span> | <span data-ttu-id="69823-156">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-156">Required</span></span> | <span data-ttu-id="69823-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-157">Type</span></span> | <span data-ttu-id="69823-158">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-158">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-159">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-159">arg1</span></span> |<span data-ttu-id="69823-160">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-160">Yes</span></span> |<span data-ttu-id="69823-161">entero, cadena, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-161">int, string, array, or object</span></span> |<span data-ttu-id="69823-162">El primer valor para comprobar si hay valores nulos.</span><span class="sxs-lookup"><span data-stu-id="69823-162">The first value to test for null.</span></span> |
| <span data-ttu-id="69823-163">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="69823-163">additional args</span></span> |<span data-ttu-id="69823-164">No</span><span class="sxs-lookup"><span data-stu-id="69823-164">No</span></span> |<span data-ttu-id="69823-165">entero, cadena, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-165">int, string, array, or object</span></span> |<span data-ttu-id="69823-166">Valores adicionales para probar si hay valores nulos.</span><span class="sxs-lookup"><span data-stu-id="69823-166">Additional values to test for null.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-167">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-167">Return value</span></span>

<span data-ttu-id="69823-168">El valor de los primeros parámetros que no son nulos, que puede ser una cadena, un entero, una matriz o un objeto.</span><span class="sxs-lookup"><span data-stu-id="69823-168">The value of the first non-null parameters, which can be a string, int, array, or object.</span></span> <span data-ttu-id="69823-169">Es nulo si todos los parámetros son nulos.</span><span class="sxs-lookup"><span data-stu-id="69823-169">Null if all parameters are null.</span></span> 

### <a name="example"></a><span data-ttu-id="69823-170">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-170">Example</span></span>

<span data-ttu-id="69823-171">En el ejemplo siguiente se muestra el resultado de los diferentes usos de coalesce.</span><span class="sxs-lookup"><span data-stu-id="69823-171">The following example shows the output from different uses of coalesce.</span></span>

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

<span data-ttu-id="69823-172">El resultado del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-172">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-173">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-173">Name</span></span> | <span data-ttu-id="69823-174">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-174">Type</span></span> | <span data-ttu-id="69823-175">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-175">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-176">stringOutput</span><span class="sxs-lookup"><span data-stu-id="69823-176">stringOutput</span></span> | <span data-ttu-id="69823-177">String</span><span class="sxs-lookup"><span data-stu-id="69823-177">String</span></span> | <span data-ttu-id="69823-178">default</span><span class="sxs-lookup"><span data-stu-id="69823-178">default</span></span> |
| <span data-ttu-id="69823-179">intOutput</span><span class="sxs-lookup"><span data-stu-id="69823-179">intOutput</span></span> | <span data-ttu-id="69823-180">int</span><span class="sxs-lookup"><span data-stu-id="69823-180">Int</span></span> | <span data-ttu-id="69823-181">1</span><span class="sxs-lookup"><span data-stu-id="69823-181">1</span></span> |
| <span data-ttu-id="69823-182">objectOutput</span><span class="sxs-lookup"><span data-stu-id="69823-182">objectOutput</span></span> | <span data-ttu-id="69823-183">Objeto</span><span class="sxs-lookup"><span data-stu-id="69823-183">Object</span></span> | <span data-ttu-id="69823-184">{"first": "default"}</span><span class="sxs-lookup"><span data-stu-id="69823-184">{"first": "default"}</span></span> |
| <span data-ttu-id="69823-185">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="69823-185">arrayOutput</span></span> | <span data-ttu-id="69823-186">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-186">Array</span></span> | <span data-ttu-id="69823-187">[1]</span><span class="sxs-lookup"><span data-stu-id="69823-187">[1]</span></span> |
| <span data-ttu-id="69823-188">emptyOutput</span><span class="sxs-lookup"><span data-stu-id="69823-188">emptyOutput</span></span> | <span data-ttu-id="69823-189">Booleano</span><span class="sxs-lookup"><span data-stu-id="69823-189">Bool</span></span> | <span data-ttu-id="69823-190">True</span><span class="sxs-lookup"><span data-stu-id="69823-190">True</span></span> |

<a id="concat" />

## <a name="concat"></a><span data-ttu-id="69823-191">concat</span><span class="sxs-lookup"><span data-stu-id="69823-191">concat</span></span>
`concat(arg1, arg2, arg3, ...)`

<span data-ttu-id="69823-192">Combina varias matrices y devuelve la matriz concatenada, o combina varios valores de cadena y devuelve la cadena concatenada.</span><span class="sxs-lookup"><span data-stu-id="69823-192">Combines multiple arrays and returns the concatenated array, or combines multiple string values and returns the concatenated string.</span></span> 

### <a name="parameters"></a><span data-ttu-id="69823-193">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-193">Parameters</span></span>

| <span data-ttu-id="69823-194">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-194">Parameter</span></span> | <span data-ttu-id="69823-195">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-195">Required</span></span> | <span data-ttu-id="69823-196">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-196">Type</span></span> | <span data-ttu-id="69823-197">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-197">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-198">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-198">arg1</span></span> |<span data-ttu-id="69823-199">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-199">Yes</span></span> |<span data-ttu-id="69823-200">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="69823-200">array or string</span></span> |<span data-ttu-id="69823-201">La primera matriz o cadena para la concatenación.</span><span class="sxs-lookup"><span data-stu-id="69823-201">The first array or string for concatenation.</span></span> |
| <span data-ttu-id="69823-202">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="69823-202">additional arguments</span></span> |<span data-ttu-id="69823-203">No</span><span class="sxs-lookup"><span data-stu-id="69823-203">No</span></span> |<span data-ttu-id="69823-204">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="69823-204">array or string</span></span> |<span data-ttu-id="69823-205">Matrices o cadenas adicionales en orden secuencial para la concatenación.</span><span class="sxs-lookup"><span data-stu-id="69823-205">Additional arrays or strings in sequential order for concatenation.</span></span> |

<span data-ttu-id="69823-206">Esta función puede tomar cualquier número de argumentos y puede aceptar cadenas o matrices para los parámetros.</span><span class="sxs-lookup"><span data-stu-id="69823-206">This function can take any number of arguments, and can accept either strings or arrays for the parameters.</span></span>

### <a name="return-value"></a><span data-ttu-id="69823-207">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-207">Return value</span></span>
<span data-ttu-id="69823-208">Una cadena o matriz de valores concatenados.</span><span class="sxs-lookup"><span data-stu-id="69823-208">A string or array of concatenated values.</span></span>

### <a name="example"></a><span data-ttu-id="69823-209">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-209">Example</span></span>

<span data-ttu-id="69823-210">En el ejemplo siguiente se muestra cómo combinar dos matrices.</span><span class="sxs-lookup"><span data-stu-id="69823-210">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="69823-211">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-211">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-212">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-212">Name</span></span> | <span data-ttu-id="69823-213">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-213">Type</span></span> | <span data-ttu-id="69823-214">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-214">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-215">return</span><span class="sxs-lookup"><span data-stu-id="69823-215">return</span></span> | <span data-ttu-id="69823-216">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-216">Array</span></span> | <span data-ttu-id="69823-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="69823-217">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<span data-ttu-id="69823-218">En el ejemplo siguiente se muestra cómo combinar dos valores de cadena y devolver una cadena concatenada.</span><span class="sxs-lookup"><span data-stu-id="69823-218">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="69823-219">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-219">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-220">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-220">Name</span></span> | <span data-ttu-id="69823-221">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-221">Type</span></span> | <span data-ttu-id="69823-222">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-222">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-223">concatOutput</span><span class="sxs-lookup"><span data-stu-id="69823-223">concatOutput</span></span> | <span data-ttu-id="69823-224">String</span><span class="sxs-lookup"><span data-stu-id="69823-224">String</span></span> | <span data-ttu-id="69823-225">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="69823-225">prefix-5yj4yjf5mbg72</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="69823-226">contains</span><span class="sxs-lookup"><span data-stu-id="69823-226">contains</span></span>
`contains(container, itemToFind)`

<span data-ttu-id="69823-227">Comprueba si una matriz contiene un valor, un objeto contiene una clave o una cadena contiene una subcadena.</span><span class="sxs-lookup"><span data-stu-id="69823-227">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-228">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-228">Parameters</span></span>

| <span data-ttu-id="69823-229">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-229">Parameter</span></span> | <span data-ttu-id="69823-230">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-230">Required</span></span> | <span data-ttu-id="69823-231">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-231">Type</span></span> | <span data-ttu-id="69823-232">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-232">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-233">container</span><span class="sxs-lookup"><span data-stu-id="69823-233">container</span></span> |<span data-ttu-id="69823-234">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-234">Yes</span></span> |<span data-ttu-id="69823-235">matriz, objeto o cadena</span><span class="sxs-lookup"><span data-stu-id="69823-235">array, object, or string</span></span> |<span data-ttu-id="69823-236">El valor que contiene el valor para buscar.</span><span class="sxs-lookup"><span data-stu-id="69823-236">The value that contains the value to find.</span></span> |
| <span data-ttu-id="69823-237">itemToFind</span><span class="sxs-lookup"><span data-stu-id="69823-237">itemToFind</span></span> |<span data-ttu-id="69823-238">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-238">Yes</span></span> |<span data-ttu-id="69823-239">cadena o entero</span><span class="sxs-lookup"><span data-stu-id="69823-239">string or int</span></span> |<span data-ttu-id="69823-240">El valor para buscar.</span><span class="sxs-lookup"><span data-stu-id="69823-240">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-241">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-241">Return value</span></span>

<span data-ttu-id="69823-242">**True** si el elemento se encuentra; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="69823-242">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="69823-243">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-243">Example</span></span>

<span data-ttu-id="69823-244">En el ejemplo siguiente se muestra cómo utilizar contains con diferentes tipos:</span><span class="sxs-lookup"><span data-stu-id="69823-244">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="69823-245">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-246">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-246">Name</span></span> | <span data-ttu-id="69823-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-247">Type</span></span> | <span data-ttu-id="69823-248">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-249">stringTrue</span><span class="sxs-lookup"><span data-stu-id="69823-249">stringTrue</span></span> | <span data-ttu-id="69823-250">Booleano</span><span class="sxs-lookup"><span data-stu-id="69823-250">Bool</span></span> | <span data-ttu-id="69823-251">True</span><span class="sxs-lookup"><span data-stu-id="69823-251">True</span></span> |
| <span data-ttu-id="69823-252">stringFalse</span><span class="sxs-lookup"><span data-stu-id="69823-252">stringFalse</span></span> | <span data-ttu-id="69823-253">Booleano</span><span class="sxs-lookup"><span data-stu-id="69823-253">Bool</span></span> | <span data-ttu-id="69823-254">False</span><span class="sxs-lookup"><span data-stu-id="69823-254">False</span></span> |
| <span data-ttu-id="69823-255">objectTrue</span><span class="sxs-lookup"><span data-stu-id="69823-255">objectTrue</span></span> | <span data-ttu-id="69823-256">Booleano</span><span class="sxs-lookup"><span data-stu-id="69823-256">Bool</span></span> | <span data-ttu-id="69823-257">True</span><span class="sxs-lookup"><span data-stu-id="69823-257">True</span></span> |
| <span data-ttu-id="69823-258">objectFalse</span><span class="sxs-lookup"><span data-stu-id="69823-258">objectFalse</span></span> | <span data-ttu-id="69823-259">Booleano</span><span class="sxs-lookup"><span data-stu-id="69823-259">Bool</span></span> | <span data-ttu-id="69823-260">False</span><span class="sxs-lookup"><span data-stu-id="69823-260">False</span></span> |
| <span data-ttu-id="69823-261">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="69823-261">arrayTrue</span></span> | <span data-ttu-id="69823-262">Booleano</span><span class="sxs-lookup"><span data-stu-id="69823-262">Bool</span></span> | <span data-ttu-id="69823-263">True</span><span class="sxs-lookup"><span data-stu-id="69823-263">True</span></span> |
| <span data-ttu-id="69823-264">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="69823-264">arrayFalse</span></span> | <span data-ttu-id="69823-265">Booleano</span><span class="sxs-lookup"><span data-stu-id="69823-265">Bool</span></span> | <span data-ttu-id="69823-266">False</span><span class="sxs-lookup"><span data-stu-id="69823-266">False</span></span> |

<a id="createarray" />

## <a name="createarray"></a><span data-ttu-id="69823-267">createarray</span><span class="sxs-lookup"><span data-stu-id="69823-267">createarray</span></span>
`createArray (arg1, arg2, arg3, ...)`

<span data-ttu-id="69823-268">Crea una matriz a partir de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="69823-268">Creates an array from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-269">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-269">Parameters</span></span>

| <span data-ttu-id="69823-270">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-270">Parameter</span></span> | <span data-ttu-id="69823-271">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-271">Required</span></span> | <span data-ttu-id="69823-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-272">Type</span></span> | <span data-ttu-id="69823-273">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-273">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-274">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-274">arg1</span></span> |<span data-ttu-id="69823-275">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-275">Yes</span></span> |<span data-ttu-id="69823-276">Cadena, entero, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-276">String, Integer, Array, or Object</span></span> |<span data-ttu-id="69823-277">El primer valor en la matriz.</span><span class="sxs-lookup"><span data-stu-id="69823-277">The first value in the array.</span></span> |
| <span data-ttu-id="69823-278">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="69823-278">additional arguments</span></span> |<span data-ttu-id="69823-279">No</span><span class="sxs-lookup"><span data-stu-id="69823-279">No</span></span> |<span data-ttu-id="69823-280">Cadena, entero, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-280">String, Integer, Array, or Object</span></span> |<span data-ttu-id="69823-281">Valores adicionales en la matriz.</span><span class="sxs-lookup"><span data-stu-id="69823-281">Additional values in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-282">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-282">Return value</span></span>

<span data-ttu-id="69823-283">Una matriz.</span><span class="sxs-lookup"><span data-stu-id="69823-283">An array.</span></span>

### <a name="example"></a><span data-ttu-id="69823-284">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-284">Example</span></span>

<span data-ttu-id="69823-285">En el ejemplo siguiente se muestra cómo utilizar createArray con diferentes tipos:</span><span class="sxs-lookup"><span data-stu-id="69823-285">The following example shows how to use createArray with different types:</span></span>

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

<span data-ttu-id="69823-286">El resultado del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-286">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-287">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-287">Name</span></span> | <span data-ttu-id="69823-288">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-288">Type</span></span> | <span data-ttu-id="69823-289">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-289">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-290">stringArray</span><span class="sxs-lookup"><span data-stu-id="69823-290">stringArray</span></span> | <span data-ttu-id="69823-291">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-291">Array</span></span> | <span data-ttu-id="69823-292">["a", "b", "c"]</span><span class="sxs-lookup"><span data-stu-id="69823-292">["a", "b", "c"]</span></span> |
| <span data-ttu-id="69823-293">intArray</span><span class="sxs-lookup"><span data-stu-id="69823-293">intArray</span></span> | <span data-ttu-id="69823-294">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-294">Array</span></span> | <span data-ttu-id="69823-295">[1, 2, 3]</span><span class="sxs-lookup"><span data-stu-id="69823-295">[1, 2, 3]</span></span> |
| <span data-ttu-id="69823-296">objectArray</span><span class="sxs-lookup"><span data-stu-id="69823-296">objectArray</span></span> | <span data-ttu-id="69823-297">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-297">Array</span></span> | <span data-ttu-id="69823-298">[{"one": "a", "two": "b", "three": "c"}]</span><span class="sxs-lookup"><span data-stu-id="69823-298">[{"one": "a", "two": "b", "three": "c"}]</span></span> |
| <span data-ttu-id="69823-299">arrayArray</span><span class="sxs-lookup"><span data-stu-id="69823-299">arrayArray</span></span> | <span data-ttu-id="69823-300">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-300">Array</span></span> | <span data-ttu-id="69823-301">[["one", "two", "three"]]</span><span class="sxs-lookup"><span data-stu-id="69823-301">[["one", "two", "three"]]</span></span> |

<a id="empty" />

## <a name="empty"></a><span data-ttu-id="69823-302">empty</span><span class="sxs-lookup"><span data-stu-id="69823-302">empty</span></span>

`empty(itemToTest)`

<span data-ttu-id="69823-303">Determina si una matriz, un objeto o una cadena están vacíos.</span><span class="sxs-lookup"><span data-stu-id="69823-303">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-304">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-304">Parameters</span></span>

| <span data-ttu-id="69823-305">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-305">Parameter</span></span> | <span data-ttu-id="69823-306">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-306">Required</span></span> | <span data-ttu-id="69823-307">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-307">Type</span></span> | <span data-ttu-id="69823-308">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-308">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-309">itemToTest</span><span class="sxs-lookup"><span data-stu-id="69823-309">itemToTest</span></span> |<span data-ttu-id="69823-310">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-310">Yes</span></span> |<span data-ttu-id="69823-311">matriz, objeto o cadena</span><span class="sxs-lookup"><span data-stu-id="69823-311">array, object, or string</span></span> |<span data-ttu-id="69823-312">El valor para comprobar si está vacío.</span><span class="sxs-lookup"><span data-stu-id="69823-312">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-313">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-313">Return value</span></span>

<span data-ttu-id="69823-314">Devuelve **True** si el valor está vacío; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="69823-314">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="69823-315">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-315">Example</span></span>

<span data-ttu-id="69823-316">En el ejemplo siguiente se comprueba si una matriz, un objeto y una cadena están vacíos.</span><span class="sxs-lookup"><span data-stu-id="69823-316">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="69823-317">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-317">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-318">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-318">Name</span></span> | <span data-ttu-id="69823-319">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-319">Type</span></span> | <span data-ttu-id="69823-320">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-320">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-321">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="69823-321">arrayEmpty</span></span> | <span data-ttu-id="69823-322">Booleano</span><span class="sxs-lookup"><span data-stu-id="69823-322">Bool</span></span> | <span data-ttu-id="69823-323">True</span><span class="sxs-lookup"><span data-stu-id="69823-323">True</span></span> |
| <span data-ttu-id="69823-324">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="69823-324">objectEmpty</span></span> | <span data-ttu-id="69823-325">Booleano</span><span class="sxs-lookup"><span data-stu-id="69823-325">Bool</span></span> | <span data-ttu-id="69823-326">True</span><span class="sxs-lookup"><span data-stu-id="69823-326">True</span></span> |
| <span data-ttu-id="69823-327">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="69823-327">stringEmpty</span></span> | <span data-ttu-id="69823-328">Booleano</span><span class="sxs-lookup"><span data-stu-id="69823-328">Bool</span></span> | <span data-ttu-id="69823-329">True</span><span class="sxs-lookup"><span data-stu-id="69823-329">True</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="69823-330">first</span><span class="sxs-lookup"><span data-stu-id="69823-330">first</span></span>
`first(arg1)`

<span data-ttu-id="69823-331">Devuelve el primer elemento de la matriz o el primer carácter de la cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-331">Returns the first element of the array, or first character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-332">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-332">Parameters</span></span>

| <span data-ttu-id="69823-333">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-333">Parameter</span></span> | <span data-ttu-id="69823-334">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-334">Required</span></span> | <span data-ttu-id="69823-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-335">Type</span></span> | <span data-ttu-id="69823-336">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-336">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-337">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-337">arg1</span></span> |<span data-ttu-id="69823-338">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-338">Yes</span></span> |<span data-ttu-id="69823-339">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="69823-339">array or string</span></span> |<span data-ttu-id="69823-340">El valor para recuperar el primer elemento o carácter.</span><span class="sxs-lookup"><span data-stu-id="69823-340">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-341">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-341">Return value</span></span>

<span data-ttu-id="69823-342">El tipo (cadena, entero, matriz u objeto) del primer elemento en una matriz o el primer carácter de una cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-342">The type (string, int, array, or object) of the first element in an array, or the first character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="69823-343">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-343">Example</span></span>

<span data-ttu-id="69823-344">En el ejemplo siguiente se muestra cómo utilizar la primera función con una matriz y una cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-344">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="69823-345">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-345">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-346">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-346">Name</span></span> | <span data-ttu-id="69823-347">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-347">Type</span></span> | <span data-ttu-id="69823-348">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-348">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-349">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="69823-349">arrayOutput</span></span> | <span data-ttu-id="69823-350">String</span><span class="sxs-lookup"><span data-stu-id="69823-350">String</span></span> | <span data-ttu-id="69823-351">one</span><span class="sxs-lookup"><span data-stu-id="69823-351">one</span></span> |
| <span data-ttu-id="69823-352">stringOutput</span><span class="sxs-lookup"><span data-stu-id="69823-352">stringOutput</span></span> | <span data-ttu-id="69823-353">String</span><span class="sxs-lookup"><span data-stu-id="69823-353">String</span></span> | <span data-ttu-id="69823-354">O</span><span class="sxs-lookup"><span data-stu-id="69823-354">O</span></span> |

<a id="intersection" />

## <a name="intersection"></a><span data-ttu-id="69823-355">intersección</span><span class="sxs-lookup"><span data-stu-id="69823-355">intersection</span></span>
`intersection(arg1, arg2, arg3, ...)`

<span data-ttu-id="69823-356">Devuelve una única matriz u objeto con los elementos comunes de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="69823-356">Returns a single array or object with the common elements from the parameters.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-357">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-357">Parameters</span></span>

| <span data-ttu-id="69823-358">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-358">Parameter</span></span> | <span data-ttu-id="69823-359">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-359">Required</span></span> | <span data-ttu-id="69823-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-360">Type</span></span> | <span data-ttu-id="69823-361">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-361">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-362">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-362">arg1</span></span> |<span data-ttu-id="69823-363">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-363">Yes</span></span> |<span data-ttu-id="69823-364">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-364">array or object</span></span> |<span data-ttu-id="69823-365">El primer valor que se utilizará para buscar elementos comunes.</span><span class="sxs-lookup"><span data-stu-id="69823-365">The first value to use for finding common elements.</span></span> |
| <span data-ttu-id="69823-366">arg2</span><span class="sxs-lookup"><span data-stu-id="69823-366">arg2</span></span> |<span data-ttu-id="69823-367">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-367">Yes</span></span> |<span data-ttu-id="69823-368">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-368">array or object</span></span> |<span data-ttu-id="69823-369">El segundo valor que se utilizará para buscar elementos comunes.</span><span class="sxs-lookup"><span data-stu-id="69823-369">The second value to use for finding common elements.</span></span> |
| <span data-ttu-id="69823-370">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="69823-370">additional arguments</span></span> |<span data-ttu-id="69823-371">No</span><span class="sxs-lookup"><span data-stu-id="69823-371">No</span></span> |<span data-ttu-id="69823-372">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-372">array or object</span></span> |<span data-ttu-id="69823-373">Valores adicionales que se utilizarán para buscar elementos comunes.</span><span class="sxs-lookup"><span data-stu-id="69823-373">Additional values to use for finding common elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-374">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-374">Return value</span></span>

<span data-ttu-id="69823-375">Una matriz o un objeto con los elementos comunes.</span><span class="sxs-lookup"><span data-stu-id="69823-375">An array or object with the common elements.</span></span>

### <a name="example"></a><span data-ttu-id="69823-376">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-376">Example</span></span>

<span data-ttu-id="69823-377">En el ejemplo siguiente se muestra cómo utilizar la intersección con matrices y objetos:</span><span class="sxs-lookup"><span data-stu-id="69823-377">The following example shows how to use intersection with arrays and objects:</span></span>

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

<span data-ttu-id="69823-378">El resultado del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-378">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-379">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-379">Name</span></span> | <span data-ttu-id="69823-380">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-380">Type</span></span> | <span data-ttu-id="69823-381">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-381">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-382">objectOutput</span><span class="sxs-lookup"><span data-stu-id="69823-382">objectOutput</span></span> | <span data-ttu-id="69823-383">Objeto</span><span class="sxs-lookup"><span data-stu-id="69823-383">Object</span></span> | <span data-ttu-id="69823-384">{"one": "a", "three": "c"}</span><span class="sxs-lookup"><span data-stu-id="69823-384">{"one": "a", "three": "c"}</span></span> |
| <span data-ttu-id="69823-385">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="69823-385">arrayOutput</span></span> | <span data-ttu-id="69823-386">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-386">Array</span></span> | <span data-ttu-id="69823-387">["two", "three"]</span><span class="sxs-lookup"><span data-stu-id="69823-387">["two", "three"]</span></span> |


## <a name="json"></a><span data-ttu-id="69823-388">json</span><span class="sxs-lookup"><span data-stu-id="69823-388">json</span></span>
`json(arg1)`

<span data-ttu-id="69823-389">Devuelve un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="69823-389">Returns a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-390">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-390">Parameters</span></span>

| <span data-ttu-id="69823-391">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-391">Parameter</span></span> | <span data-ttu-id="69823-392">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-392">Required</span></span> | <span data-ttu-id="69823-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-393">Type</span></span> | <span data-ttu-id="69823-394">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-394">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-395">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-395">arg1</span></span> |<span data-ttu-id="69823-396">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-396">Yes</span></span> |<span data-ttu-id="69823-397">cadena</span><span class="sxs-lookup"><span data-stu-id="69823-397">string</span></span> |<span data-ttu-id="69823-398">Valor que se va a convertir en JSON.</span><span class="sxs-lookup"><span data-stu-id="69823-398">The value to convert to JSON.</span></span> |


### <a name="return-value"></a><span data-ttu-id="69823-399">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-399">Return value</span></span>

<span data-ttu-id="69823-400">Objeto JSON de la cadena especificada o un objeto vacío si se especifica **null**.</span><span class="sxs-lookup"><span data-stu-id="69823-400">The JSON object from the specified string, or an empty object when **null** is specified.</span></span>

### <a name="example"></a><span data-ttu-id="69823-401">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-401">Example</span></span>

<span data-ttu-id="69823-402">En el ejemplo siguiente se muestra cómo utilizar la intersección con matrices y objetos:</span><span class="sxs-lookup"><span data-stu-id="69823-402">The following example shows how to use intersection with arrays and objects:</span></span>

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

<span data-ttu-id="69823-403">El resultado del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-403">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-404">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-404">Name</span></span> | <span data-ttu-id="69823-405">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-405">Type</span></span> | <span data-ttu-id="69823-406">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-406">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-407">jsonOutput</span><span class="sxs-lookup"><span data-stu-id="69823-407">jsonOutput</span></span> | <span data-ttu-id="69823-408">Objeto</span><span class="sxs-lookup"><span data-stu-id="69823-408">Object</span></span> | <span data-ttu-id="69823-409">{"a": "b"}</span><span class="sxs-lookup"><span data-stu-id="69823-409">{"a": "b"}</span></span> |
| <span data-ttu-id="69823-410">nullOutput</span><span class="sxs-lookup"><span data-stu-id="69823-410">nullOutput</span></span> | <span data-ttu-id="69823-411">boolean</span><span class="sxs-lookup"><span data-stu-id="69823-411">Boolean</span></span> | <span data-ttu-id="69823-412">True</span><span class="sxs-lookup"><span data-stu-id="69823-412">True</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="69823-413">last</span><span class="sxs-lookup"><span data-stu-id="69823-413">last</span></span>
`last (arg1)`

<span data-ttu-id="69823-414">Devuelve el último elemento de la matriz o el último carácter de la cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-414">Returns the last element of the array, or last character of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-415">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-415">Parameters</span></span>

| <span data-ttu-id="69823-416">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-416">Parameter</span></span> | <span data-ttu-id="69823-417">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-417">Required</span></span> | <span data-ttu-id="69823-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-418">Type</span></span> | <span data-ttu-id="69823-419">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-420">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-420">arg1</span></span> |<span data-ttu-id="69823-421">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-421">Yes</span></span> |<span data-ttu-id="69823-422">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="69823-422">array or string</span></span> |<span data-ttu-id="69823-423">El valor para recuperar el último elemento o carácter.</span><span class="sxs-lookup"><span data-stu-id="69823-423">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-424">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-424">Return value</span></span>

<span data-ttu-id="69823-425">El tipo (cadena, entero, matriz u objeto) del último elemento de una matriz o el último carácter de una cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-425">The type (string, int, array, or object) of the last element in an array, or the last character of a string.</span></span>

### <a name="example"></a><span data-ttu-id="69823-426">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-426">Example</span></span>

<span data-ttu-id="69823-427">En el ejemplo siguiente se muestra cómo utilizar la última función con una matriz y una cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-427">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="69823-428">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-429">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-429">Name</span></span> | <span data-ttu-id="69823-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-430">Type</span></span> | <span data-ttu-id="69823-431">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="69823-432">arrayOutput</span></span> | <span data-ttu-id="69823-433">String</span><span class="sxs-lookup"><span data-stu-id="69823-433">String</span></span> | <span data-ttu-id="69823-434">three</span><span class="sxs-lookup"><span data-stu-id="69823-434">three</span></span> |
| <span data-ttu-id="69823-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="69823-435">stringOutput</span></span> | <span data-ttu-id="69823-436">String</span><span class="sxs-lookup"><span data-stu-id="69823-436">String</span></span> | <span data-ttu-id="69823-437">e</span><span class="sxs-lookup"><span data-stu-id="69823-437">e</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="69823-438">length</span><span class="sxs-lookup"><span data-stu-id="69823-438">length</span></span>
`length(arg1)`

<span data-ttu-id="69823-439">Devuelve el número de elementos de una matriz, o los caracteres de una cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-439">Returns the number of elements in an array, or characters in a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-440">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-440">Parameters</span></span>

| <span data-ttu-id="69823-441">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-441">Parameter</span></span> | <span data-ttu-id="69823-442">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-442">Required</span></span> | <span data-ttu-id="69823-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-443">Type</span></span> | <span data-ttu-id="69823-444">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-444">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-445">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-445">arg1</span></span> |<span data-ttu-id="69823-446">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-446">Yes</span></span> |<span data-ttu-id="69823-447">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="69823-447">array or string</span></span> |<span data-ttu-id="69823-448">La matriz que se usará para obtener el número de elementos, o la cadena que se usará para obtener el número de caracteres.</span><span class="sxs-lookup"><span data-stu-id="69823-448">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-449">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-449">Return value</span></span>

<span data-ttu-id="69823-450">Un entero.</span><span class="sxs-lookup"><span data-stu-id="69823-450">An int.</span></span> 

### <a name="example"></a><span data-ttu-id="69823-451">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-451">Example</span></span>

<span data-ttu-id="69823-452">En el ejemplo siguiente se muestra cómo utilizar length con una matriz y una cadena:</span><span class="sxs-lookup"><span data-stu-id="69823-452">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="69823-453">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-453">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-454">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-454">Name</span></span> | <span data-ttu-id="69823-455">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-455">Type</span></span> | <span data-ttu-id="69823-456">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-456">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-457">arrayLength</span><span class="sxs-lookup"><span data-stu-id="69823-457">arrayLength</span></span> | <span data-ttu-id="69823-458">int</span><span class="sxs-lookup"><span data-stu-id="69823-458">Int</span></span> | <span data-ttu-id="69823-459">3</span><span class="sxs-lookup"><span data-stu-id="69823-459">3</span></span> |
| <span data-ttu-id="69823-460">stringLength</span><span class="sxs-lookup"><span data-stu-id="69823-460">stringLength</span></span> | <span data-ttu-id="69823-461">int</span><span class="sxs-lookup"><span data-stu-id="69823-461">Int</span></span> | <span data-ttu-id="69823-462">13</span><span class="sxs-lookup"><span data-stu-id="69823-462">13</span></span> |

<span data-ttu-id="69823-463">Puede usar esta función con una matriz para especificar el número de iteraciones al crear recursos.</span><span class="sxs-lookup"><span data-stu-id="69823-463">You can use this function with an array to specify the number of iterations when creating resources.</span></span> <span data-ttu-id="69823-464">En el ejemplo siguiente, el parámetro **siteNames** debería hacer referencia a una matriz de nombres que se usará al crear los sitios web.</span><span class="sxs-lookup"><span data-stu-id="69823-464">In the following example, the parameter **siteNames** would refer to an array of names to use when creating the web sites.</span></span>

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

<span data-ttu-id="69823-465">Para más información sobre cómo usar esta función con una matriz, vea [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="69823-465">For more information about using this function with an array, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<a id="min" />

## <a name="min"></a><span data-ttu-id="69823-466">Min</span><span class="sxs-lookup"><span data-stu-id="69823-466">min</span></span>
`min(arg1)`

<span data-ttu-id="69823-467">Devuelve el valor mínimo de una matriz de enteros o una lista separada por comas de enteros.</span><span class="sxs-lookup"><span data-stu-id="69823-467">Returns the minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-468">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-468">Parameters</span></span>

| <span data-ttu-id="69823-469">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-469">Parameter</span></span> | <span data-ttu-id="69823-470">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-470">Required</span></span> | <span data-ttu-id="69823-471">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-471">Type</span></span> | <span data-ttu-id="69823-472">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-472">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-473">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-473">arg1</span></span> |<span data-ttu-id="69823-474">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-474">Yes</span></span> |<span data-ttu-id="69823-475">matriz de enteros, o lista separada por comas de enteros</span><span class="sxs-lookup"><span data-stu-id="69823-475">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="69823-476">La colección para obtener el valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="69823-476">The collection to get the minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-477">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-477">Return value</span></span>

<span data-ttu-id="69823-478">Un entero que representa el valor mínimo.</span><span class="sxs-lookup"><span data-stu-id="69823-478">An int representing the minimum value.</span></span>

### <a name="example"></a><span data-ttu-id="69823-479">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-479">Example</span></span>

<span data-ttu-id="69823-480">En el ejemplo siguiente se muestra cómo utilizar min con una matriz y una lista de enteros:</span><span class="sxs-lookup"><span data-stu-id="69823-480">The following example shows how to use min with an array and a list of integers:</span></span>

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

<span data-ttu-id="69823-481">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-481">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-482">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-482">Name</span></span> | <span data-ttu-id="69823-483">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-483">Type</span></span> | <span data-ttu-id="69823-484">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-484">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-485">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="69823-485">arrayOutput</span></span> | <span data-ttu-id="69823-486">int</span><span class="sxs-lookup"><span data-stu-id="69823-486">Int</span></span> | <span data-ttu-id="69823-487">0</span><span class="sxs-lookup"><span data-stu-id="69823-487">0</span></span> |
| <span data-ttu-id="69823-488">intOutput</span><span class="sxs-lookup"><span data-stu-id="69823-488">intOutput</span></span> | <span data-ttu-id="69823-489">int</span><span class="sxs-lookup"><span data-stu-id="69823-489">Int</span></span> | <span data-ttu-id="69823-490">0</span><span class="sxs-lookup"><span data-stu-id="69823-490">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="69823-491">max</span><span class="sxs-lookup"><span data-stu-id="69823-491">max</span></span>
`max(arg1)`

<span data-ttu-id="69823-492">Devuelve el valor máximo de una matriz de enteros o una lista separada por comas de enteros.</span><span class="sxs-lookup"><span data-stu-id="69823-492">Returns the maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-493">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-493">Parameters</span></span>

| <span data-ttu-id="69823-494">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-494">Parameter</span></span> | <span data-ttu-id="69823-495">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-495">Required</span></span> | <span data-ttu-id="69823-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-496">Type</span></span> | <span data-ttu-id="69823-497">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-497">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-498">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-498">arg1</span></span> |<span data-ttu-id="69823-499">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-499">Yes</span></span> |<span data-ttu-id="69823-500">matriz de enteros, o lista separada por comas de enteros</span><span class="sxs-lookup"><span data-stu-id="69823-500">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="69823-501">La colección para obtener el valor máximo.</span><span class="sxs-lookup"><span data-stu-id="69823-501">The collection to get the maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-502">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-502">Return value</span></span>

<span data-ttu-id="69823-503">Un entero que representa el valor máximo.</span><span class="sxs-lookup"><span data-stu-id="69823-503">An int representing the maximum value.</span></span>

### <a name="example"></a><span data-ttu-id="69823-504">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-504">Example</span></span>

<span data-ttu-id="69823-505">En el ejemplo siguiente se muestra cómo utilizar max con una matriz y una lista de enteros:</span><span class="sxs-lookup"><span data-stu-id="69823-505">The following example shows how to use max with an array and a list of integers:</span></span>

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

<span data-ttu-id="69823-506">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-506">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-507">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-507">Name</span></span> | <span data-ttu-id="69823-508">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-508">Type</span></span> | <span data-ttu-id="69823-509">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-509">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-510">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="69823-510">arrayOutput</span></span> | <span data-ttu-id="69823-511">int</span><span class="sxs-lookup"><span data-stu-id="69823-511">Int</span></span> | <span data-ttu-id="69823-512">5</span><span class="sxs-lookup"><span data-stu-id="69823-512">5</span></span> |
| <span data-ttu-id="69823-513">intOutput</span><span class="sxs-lookup"><span data-stu-id="69823-513">intOutput</span></span> | <span data-ttu-id="69823-514">int</span><span class="sxs-lookup"><span data-stu-id="69823-514">Int</span></span> | <span data-ttu-id="69823-515">5</span><span class="sxs-lookup"><span data-stu-id="69823-515">5</span></span> |

<a id="range" />

## <a name="range"></a><span data-ttu-id="69823-516">range</span><span class="sxs-lookup"><span data-stu-id="69823-516">range</span></span>
`range(startingInteger, numberOfElements)`

<span data-ttu-id="69823-517">Crea una matriz de enteros a partir de un entero de inicio y contiene un número de elementos.</span><span class="sxs-lookup"><span data-stu-id="69823-517">Creates an array of integers from a starting integer and containing a number of items.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-518">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-518">Parameters</span></span>

| <span data-ttu-id="69823-519">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-519">Parameter</span></span> | <span data-ttu-id="69823-520">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-520">Required</span></span> | <span data-ttu-id="69823-521">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-521">Type</span></span> | <span data-ttu-id="69823-522">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-522">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-523">startingInteger</span><span class="sxs-lookup"><span data-stu-id="69823-523">startingInteger</span></span> |<span data-ttu-id="69823-524">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-524">Yes</span></span> |<span data-ttu-id="69823-525">int</span><span class="sxs-lookup"><span data-stu-id="69823-525">int</span></span> |<span data-ttu-id="69823-526">El primer entero de la matriz.</span><span class="sxs-lookup"><span data-stu-id="69823-526">The first integer in the array.</span></span> |
| <span data-ttu-id="69823-527">numberofElements</span><span class="sxs-lookup"><span data-stu-id="69823-527">numberofElements</span></span> |<span data-ttu-id="69823-528">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-528">Yes</span></span> |<span data-ttu-id="69823-529">int</span><span class="sxs-lookup"><span data-stu-id="69823-529">int</span></span> |<span data-ttu-id="69823-530">El número de enteros en la matriz.</span><span class="sxs-lookup"><span data-stu-id="69823-530">The number of integers in the array.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-531">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-531">Return value</span></span>

<span data-ttu-id="69823-532">Una matriz de enteros.</span><span class="sxs-lookup"><span data-stu-id="69823-532">An array of integers.</span></span>

### <a name="example"></a><span data-ttu-id="69823-533">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-533">Example</span></span>

<span data-ttu-id="69823-534">En el ejemplo siguiente se muestra cómo utilizar la función range:</span><span class="sxs-lookup"><span data-stu-id="69823-534">The following example shows how to use the range function:</span></span>

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

<span data-ttu-id="69823-535">El resultado del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-535">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-536">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-536">Name</span></span> | <span data-ttu-id="69823-537">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-537">Type</span></span> | <span data-ttu-id="69823-538">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-538">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-539">rangeOutput</span><span class="sxs-lookup"><span data-stu-id="69823-539">rangeOutput</span></span> | <span data-ttu-id="69823-540">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-540">Array</span></span> | <span data-ttu-id="69823-541">[5, 6, 7]</span><span class="sxs-lookup"><span data-stu-id="69823-541">[5, 6, 7]</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="69823-542">skip</span><span class="sxs-lookup"><span data-stu-id="69823-542">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="69823-543">Devuelve una matriz con todos los elementos después del número especificado de la matriz, o devuelve una cadena con todos los caracteres después del número especificado en la cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-543">Returns an array with all the elements after the specified number in the array, or returns a string with all the characters after the specified number in the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-544">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-544">Parameters</span></span>

| <span data-ttu-id="69823-545">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-545">Parameter</span></span> | <span data-ttu-id="69823-546">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-546">Required</span></span> | <span data-ttu-id="69823-547">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-547">Type</span></span> | <span data-ttu-id="69823-548">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-548">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-549">originalValue</span><span class="sxs-lookup"><span data-stu-id="69823-549">originalValue</span></span> |<span data-ttu-id="69823-550">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-550">Yes</span></span> |<span data-ttu-id="69823-551">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="69823-551">array or string</span></span> |<span data-ttu-id="69823-552">La matriz o cadena que se usará para la omisión.</span><span class="sxs-lookup"><span data-stu-id="69823-552">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="69823-553">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="69823-553">numberToSkip</span></span> |<span data-ttu-id="69823-554">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-554">Yes</span></span> |<span data-ttu-id="69823-555">int</span><span class="sxs-lookup"><span data-stu-id="69823-555">int</span></span> |<span data-ttu-id="69823-556">El número de elementos o caracteres que se van a omitir.</span><span class="sxs-lookup"><span data-stu-id="69823-556">The number of elements or characters to skip.</span></span> <span data-ttu-id="69823-557">Si este valor es 0 o un valor inferior, se devuelven todos los elementos o caracteres del valor.</span><span class="sxs-lookup"><span data-stu-id="69823-557">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="69823-558">Si es mayor que la longitud de la matriz o la cadena, se devuelve una matriz o cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="69823-558">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-559">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-559">Return value</span></span>

<span data-ttu-id="69823-560">Una matriz o cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-560">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="69823-561">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-561">Example</span></span>

<span data-ttu-id="69823-562">En el ejemplo siguiente se omite el número especificado de elementos de la matriz, y el número especificado de caracteres de la cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-562">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="69823-563">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-563">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-564">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-564">Name</span></span> | <span data-ttu-id="69823-565">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-565">Type</span></span> | <span data-ttu-id="69823-566">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-566">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-567">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="69823-567">arrayOutput</span></span> | <span data-ttu-id="69823-568">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-568">Array</span></span> | <span data-ttu-id="69823-569">["three"]</span><span class="sxs-lookup"><span data-stu-id="69823-569">["three"]</span></span> |
| <span data-ttu-id="69823-570">stringOutput</span><span class="sxs-lookup"><span data-stu-id="69823-570">stringOutput</span></span> | <span data-ttu-id="69823-571">String</span><span class="sxs-lookup"><span data-stu-id="69823-571">String</span></span> | <span data-ttu-id="69823-572">two three</span><span class="sxs-lookup"><span data-stu-id="69823-572">two three</span></span> |

<a id="take" />

## <a name="take"></a><span data-ttu-id="69823-573">take</span><span class="sxs-lookup"><span data-stu-id="69823-573">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="69823-574">Devuelve una matriz con el número especificado de elementos desde el inicio de la matriz, o una cadena con el número especificado de caracteres desde el inicio de la cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-574">Returns an array with the specified number of elements from the start of the array, or a string with the specified number of characters from the start of the string.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-575">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-575">Parameters</span></span>

| <span data-ttu-id="69823-576">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-576">Parameter</span></span> | <span data-ttu-id="69823-577">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-577">Required</span></span> | <span data-ttu-id="69823-578">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-578">Type</span></span> | <span data-ttu-id="69823-579">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-579">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-580">originalValue</span><span class="sxs-lookup"><span data-stu-id="69823-580">originalValue</span></span> |<span data-ttu-id="69823-581">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-581">Yes</span></span> |<span data-ttu-id="69823-582">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="69823-582">array or string</span></span> |<span data-ttu-id="69823-583">La matriz o cadena de la que se van a tomar los elementos.</span><span class="sxs-lookup"><span data-stu-id="69823-583">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="69823-584">numberToTake</span><span class="sxs-lookup"><span data-stu-id="69823-584">numberToTake</span></span> |<span data-ttu-id="69823-585">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-585">Yes</span></span> |<span data-ttu-id="69823-586">int</span><span class="sxs-lookup"><span data-stu-id="69823-586">int</span></span> |<span data-ttu-id="69823-587">El número de elementos o caracteres que se van a tomar.</span><span class="sxs-lookup"><span data-stu-id="69823-587">The number of elements or characters to take.</span></span> <span data-ttu-id="69823-588">Si este valor es 0 o un valor inferior, se devolverá una matriz o cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="69823-588">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="69823-589">Si es mayor que la longitud de la matriz o cadena especificada, se devuelven todos los elementos de la matriz o cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-589">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-590">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-590">Return value</span></span>

<span data-ttu-id="69823-591">Una matriz o cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-591">An array or string.</span></span>

### <a name="example"></a><span data-ttu-id="69823-592">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-592">Example</span></span>

<span data-ttu-id="69823-593">En el ejemplo siguiente se toma el número especificado de elementos de la matriz y de caracteres de la cadena.</span><span class="sxs-lookup"><span data-stu-id="69823-593">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="69823-594">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-594">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-595">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-595">Name</span></span> | <span data-ttu-id="69823-596">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-596">Type</span></span> | <span data-ttu-id="69823-597">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-597">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-598">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="69823-598">arrayOutput</span></span> | <span data-ttu-id="69823-599">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-599">Array</span></span> | <span data-ttu-id="69823-600">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="69823-600">["one", "two"]</span></span> |
| <span data-ttu-id="69823-601">stringOutput</span><span class="sxs-lookup"><span data-stu-id="69823-601">stringOutput</span></span> | <span data-ttu-id="69823-602">String</span><span class="sxs-lookup"><span data-stu-id="69823-602">String</span></span> | <span data-ttu-id="69823-603">en</span><span class="sxs-lookup"><span data-stu-id="69823-603">on</span></span> |

<a id="union" />

## <a name="union"></a><span data-ttu-id="69823-604">union</span><span class="sxs-lookup"><span data-stu-id="69823-604">union</span></span>
`union(arg1, arg2, arg3, ...)`

<span data-ttu-id="69823-605">Devuelve una única matriz u objeto con todos los elementos de los parámetros.</span><span class="sxs-lookup"><span data-stu-id="69823-605">Returns a single array or object with all elements from the parameters.</span></span> <span data-ttu-id="69823-606">Los valores o las claves duplicados solo se incluyen una vez.</span><span class="sxs-lookup"><span data-stu-id="69823-606">Duplicate values or keys are only included once.</span></span>

### <a name="parameters"></a><span data-ttu-id="69823-607">parameters</span><span class="sxs-lookup"><span data-stu-id="69823-607">Parameters</span></span>

| <span data-ttu-id="69823-608">Parámetro</span><span class="sxs-lookup"><span data-stu-id="69823-608">Parameter</span></span> | <span data-ttu-id="69823-609">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="69823-609">Required</span></span> | <span data-ttu-id="69823-610">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-610">Type</span></span> | <span data-ttu-id="69823-611">Descripción</span><span class="sxs-lookup"><span data-stu-id="69823-611">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="69823-612">arg1</span><span class="sxs-lookup"><span data-stu-id="69823-612">arg1</span></span> |<span data-ttu-id="69823-613">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-613">Yes</span></span> |<span data-ttu-id="69823-614">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-614">array or object</span></span> |<span data-ttu-id="69823-615">El primer valor que se utiliza para unir elementos.</span><span class="sxs-lookup"><span data-stu-id="69823-615">The first value to use for joining elements.</span></span> |
| <span data-ttu-id="69823-616">arg2</span><span class="sxs-lookup"><span data-stu-id="69823-616">arg2</span></span> |<span data-ttu-id="69823-617">Sí</span><span class="sxs-lookup"><span data-stu-id="69823-617">Yes</span></span> |<span data-ttu-id="69823-618">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-618">array or object</span></span> |<span data-ttu-id="69823-619">El segundo valor que se utiliza para unir elementos.</span><span class="sxs-lookup"><span data-stu-id="69823-619">The second value to use for joining elements.</span></span> |
| <span data-ttu-id="69823-620">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="69823-620">additional arguments</span></span> |<span data-ttu-id="69823-621">No</span><span class="sxs-lookup"><span data-stu-id="69823-621">No</span></span> |<span data-ttu-id="69823-622">matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="69823-622">array or object</span></span> |<span data-ttu-id="69823-623">Valores adicionales que se utilizan para unir elementos.</span><span class="sxs-lookup"><span data-stu-id="69823-623">Additional values to use for joining elements.</span></span> |

### <a name="return-value"></a><span data-ttu-id="69823-624">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="69823-624">Return value</span></span>

<span data-ttu-id="69823-625">Una matriz u objeto.</span><span class="sxs-lookup"><span data-stu-id="69823-625">An array or object.</span></span>

### <a name="example"></a><span data-ttu-id="69823-626">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="69823-626">Example</span></span>

<span data-ttu-id="69823-627">En el ejemplo siguiente se muestra cómo utilizar la unión con matrices y objetos:</span><span class="sxs-lookup"><span data-stu-id="69823-627">The following example shows how to use union with arrays and objects:</span></span>

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

<span data-ttu-id="69823-628">El resultado del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="69823-628">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="69823-629">Nombre</span><span class="sxs-lookup"><span data-stu-id="69823-629">Name</span></span> | <span data-ttu-id="69823-630">Tipo</span><span class="sxs-lookup"><span data-stu-id="69823-630">Type</span></span> | <span data-ttu-id="69823-631">Valor</span><span class="sxs-lookup"><span data-stu-id="69823-631">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="69823-632">objectOutput</span><span class="sxs-lookup"><span data-stu-id="69823-632">objectOutput</span></span> | <span data-ttu-id="69823-633">Objeto</span><span class="sxs-lookup"><span data-stu-id="69823-633">Object</span></span> | <span data-ttu-id="69823-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span><span class="sxs-lookup"><span data-stu-id="69823-634">{"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"}</span></span> |
| <span data-ttu-id="69823-635">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="69823-635">arrayOutput</span></span> | <span data-ttu-id="69823-636">Matriz</span><span class="sxs-lookup"><span data-stu-id="69823-636">Array</span></span> | <span data-ttu-id="69823-637">["one", "two", "three", "four"]</span><span class="sxs-lookup"><span data-stu-id="69823-637">["one", "two", "three", "four"]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="69823-638">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69823-638">Next steps</span></span>
* <span data-ttu-id="69823-639">Para obtener una descripción de las secciones de una plantilla de Azure Resource Manager, vea [Creación de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="69823-639">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="69823-640">Para combinar varias plantillas, vea [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="69823-640">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="69823-641">Para iterar una cantidad de veces específica al crear un tipo de recurso, vea [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="69823-641">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="69823-642">Para saber cómo implementar la plantilla que creó, consulte [Implementación de una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="69823-642">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

