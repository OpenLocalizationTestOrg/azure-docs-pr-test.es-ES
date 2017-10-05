---
title: "Funciones de la plantilla de Azure Resource Manager: comparación | Microsoft Docs"
description: Describe las funciones para usar en una plantilla de Azure Resource Manager para comparar valores.
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
ms.openlocfilehash: 521e5ed06c138bcd374913588f06a2e6c1e99963
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="82c31-103">Funciones de comparación para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="82c31-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="82c31-104">Resource Manager proporciona varias funciones para realizar comparaciones en las plantillas.</span><span class="sxs-lookup"><span data-stu-id="82c31-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="82c31-105">equals</span><span class="sxs-lookup"><span data-stu-id="82c31-105">equals</span></span>](#equals)
* [<span data-ttu-id="82c31-106">greater</span><span class="sxs-lookup"><span data-stu-id="82c31-106">greater</span></span>](#greater)
* [<span data-ttu-id="82c31-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="82c31-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="82c31-108">less</span><span class="sxs-lookup"><span data-stu-id="82c31-108">less</span></span>](#less)
* [<span data-ttu-id="82c31-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="82c31-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="82c31-110">equals</span><span class="sxs-lookup"><span data-stu-id="82c31-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="82c31-111">Comprueba si dos valores son iguales.</span><span class="sxs-lookup"><span data-stu-id="82c31-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="82c31-112">parameters</span><span class="sxs-lookup"><span data-stu-id="82c31-112">Parameters</span></span>

| <span data-ttu-id="82c31-113">Parámetro</span><span class="sxs-lookup"><span data-stu-id="82c31-113">Parameter</span></span> | <span data-ttu-id="82c31-114">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="82c31-114">Required</span></span> | <span data-ttu-id="82c31-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-115">Type</span></span> | <span data-ttu-id="82c31-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="82c31-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="82c31-117">arg1</span><span class="sxs-lookup"><span data-stu-id="82c31-117">arg1</span></span> |<span data-ttu-id="82c31-118">Sí</span><span class="sxs-lookup"><span data-stu-id="82c31-118">Yes</span></span> |<span data-ttu-id="82c31-119">entero, cadena, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="82c31-119">int, string, array, or object</span></span> |<span data-ttu-id="82c31-120">El primer valor en el que comprobar la igualdad.</span><span class="sxs-lookup"><span data-stu-id="82c31-120">The first value to check for equality.</span></span> |
| <span data-ttu-id="82c31-121">arg2</span><span class="sxs-lookup"><span data-stu-id="82c31-121">arg2</span></span> |<span data-ttu-id="82c31-122">Sí</span><span class="sxs-lookup"><span data-stu-id="82c31-122">Yes</span></span> |<span data-ttu-id="82c31-123">entero, cadena, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="82c31-123">int, string, array, or object</span></span> |<span data-ttu-id="82c31-124">El segundo valor en el que comprobar la igualdad.</span><span class="sxs-lookup"><span data-stu-id="82c31-124">The second value to check for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="82c31-125">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="82c31-125">Return value</span></span>

<span data-ttu-id="82c31-126">Devuelve **True** si los valores son iguales; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="82c31-126">Returns **True** if the values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="82c31-127">Comentarios</span><span class="sxs-lookup"><span data-stu-id="82c31-127">Remarks</span></span>

<span data-ttu-id="82c31-128">La función equals se suele usar con el elemento `condition` para comprobar si está implementado un recurso.</span><span class="sxs-lookup"><span data-stu-id="82c31-128">The equals function is often used with the `condition` element to test whether a resource is deployed.</span></span>

```json
{
    "condition": "[equals(parameters('newOrExisting'),'new')]",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2017-06-01",
    "location": "[resourceGroup().location]",
    "sku": {
        "name": "[variables('storageAccountType')]"
    },
    "kind": "Storage",
    "properties": {}
}
```

### <a name="example"></a><span data-ttu-id="82c31-129">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="82c31-129">Example</span></span>

<span data-ttu-id="82c31-130">La plantilla de ejemplo comprueba diferentes tipos de valores para la igualdad.</span><span class="sxs-lookup"><span data-stu-id="82c31-130">The example template checks different types of values for equality.</span></span> <span data-ttu-id="82c31-131">Todos los valores predeterminados devuelven True.</span><span class="sxs-lookup"><span data-stu-id="82c31-131">All the default values return True.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 1
        },
        "firstString": {
            "type": "string",
            "defaultValue": "a"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        },
        "firstArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "secondArray": {
            "type": "array",
            "defaultValue": ["a", "b"]
        },
        "firstObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        },
        "secondObject": {
            "type": "object",
            "defaultValue": {"a": "b"}
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[equals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[equals(parameters('firstString'), parameters('secondString'))]"
        },
        "checkArrays": {
            "type": "bool",
            "value": "[equals(parameters('firstArray'), parameters('secondArray'))]"
        },
        "checkObjects": {
            "type": "bool",
            "value": "[equals(parameters('firstObject'), parameters('secondObject'))]"
        }
    }
}
```

<span data-ttu-id="82c31-132">La salida del ejemplo anterior con el valor predeterminado es:</span><span class="sxs-lookup"><span data-stu-id="82c31-132">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="82c31-133">Nombre</span><span class="sxs-lookup"><span data-stu-id="82c31-133">Name</span></span> | <span data-ttu-id="82c31-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-134">Type</span></span> | <span data-ttu-id="82c31-135">Valor</span><span class="sxs-lookup"><span data-stu-id="82c31-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="82c31-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="82c31-136">checkInts</span></span> | <span data-ttu-id="82c31-137">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-137">Bool</span></span> | <span data-ttu-id="82c31-138">True</span><span class="sxs-lookup"><span data-stu-id="82c31-138">True</span></span> |
| <span data-ttu-id="82c31-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="82c31-139">checkStrings</span></span> | <span data-ttu-id="82c31-140">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-140">Bool</span></span> | <span data-ttu-id="82c31-141">True</span><span class="sxs-lookup"><span data-stu-id="82c31-141">True</span></span> |
| <span data-ttu-id="82c31-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="82c31-142">checkArrays</span></span> | <span data-ttu-id="82c31-143">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-143">Bool</span></span> | <span data-ttu-id="82c31-144">True</span><span class="sxs-lookup"><span data-stu-id="82c31-144">True</span></span> |
| <span data-ttu-id="82c31-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="82c31-145">checkObjects</span></span> | <span data-ttu-id="82c31-146">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-146">Bool</span></span> | <span data-ttu-id="82c31-147">True</span><span class="sxs-lookup"><span data-stu-id="82c31-147">True</span></span> |


<span data-ttu-id="82c31-148">En el siguiente ejemplo se usa [not](resource-group-template-functions-logical.md#not) con **equals**.</span><span class="sxs-lookup"><span data-stu-id="82c31-148">The following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="82c31-149">El resultado del ejemplo anterior es:</span><span class="sxs-lookup"><span data-stu-id="82c31-149">The output from the preceding example is:</span></span>

| <span data-ttu-id="82c31-150">Nombre</span><span class="sxs-lookup"><span data-stu-id="82c31-150">Name</span></span> | <span data-ttu-id="82c31-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-151">Type</span></span> | <span data-ttu-id="82c31-152">Valor</span><span class="sxs-lookup"><span data-stu-id="82c31-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="82c31-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="82c31-153">checkNotEquals</span></span> | <span data-ttu-id="82c31-154">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-154">Bool</span></span> | <span data-ttu-id="82c31-155">True</span><span class="sxs-lookup"><span data-stu-id="82c31-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="82c31-156">greater</span><span class="sxs-lookup"><span data-stu-id="82c31-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="82c31-157">Comprueba si el primer valor es mayor que el segundo.</span><span class="sxs-lookup"><span data-stu-id="82c31-157">Checks whether the first value is greater than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="82c31-158">parameters</span><span class="sxs-lookup"><span data-stu-id="82c31-158">Parameters</span></span>

| <span data-ttu-id="82c31-159">Parámetro</span><span class="sxs-lookup"><span data-stu-id="82c31-159">Parameter</span></span> | <span data-ttu-id="82c31-160">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="82c31-160">Required</span></span> | <span data-ttu-id="82c31-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-161">Type</span></span> | <span data-ttu-id="82c31-162">Descripción</span><span class="sxs-lookup"><span data-stu-id="82c31-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="82c31-163">arg1</span><span class="sxs-lookup"><span data-stu-id="82c31-163">arg1</span></span> |<span data-ttu-id="82c31-164">Sí</span><span class="sxs-lookup"><span data-stu-id="82c31-164">Yes</span></span> |<span data-ttu-id="82c31-165">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="82c31-165">int or string</span></span> |<span data-ttu-id="82c31-166">El primer valor de la comparación mayor.</span><span class="sxs-lookup"><span data-stu-id="82c31-166">The first value for the greater comparison.</span></span> |
| <span data-ttu-id="82c31-167">arg2</span><span class="sxs-lookup"><span data-stu-id="82c31-167">arg2</span></span> |<span data-ttu-id="82c31-168">Sí</span><span class="sxs-lookup"><span data-stu-id="82c31-168">Yes</span></span> |<span data-ttu-id="82c31-169">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="82c31-169">int or string</span></span> |<span data-ttu-id="82c31-170">El segundo valor de la comparación mayor.</span><span class="sxs-lookup"><span data-stu-id="82c31-170">The second value for the greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="82c31-171">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="82c31-171">Return value</span></span>

<span data-ttu-id="82c31-172">Devuelve **True** si el primer valor es mayor que el segundo; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="82c31-172">Returns **True** if the first value is greater than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="82c31-173">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="82c31-173">Example</span></span>

<span data-ttu-id="82c31-174">La plantilla de ejemplo comprueba si un valor es mayor que el otro.</span><span class="sxs-lookup"><span data-stu-id="82c31-174">The example template checks whether the one value is greater than the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greater(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greater(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="82c31-175">La salida del ejemplo anterior con el valor predeterminado es:</span><span class="sxs-lookup"><span data-stu-id="82c31-175">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="82c31-176">Nombre</span><span class="sxs-lookup"><span data-stu-id="82c31-176">Name</span></span> | <span data-ttu-id="82c31-177">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-177">Type</span></span> | <span data-ttu-id="82c31-178">Valor</span><span class="sxs-lookup"><span data-stu-id="82c31-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="82c31-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="82c31-179">checkInts</span></span> | <span data-ttu-id="82c31-180">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-180">Bool</span></span> | <span data-ttu-id="82c31-181">False</span><span class="sxs-lookup"><span data-stu-id="82c31-181">False</span></span> |
| <span data-ttu-id="82c31-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="82c31-182">checkStrings</span></span> | <span data-ttu-id="82c31-183">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-183">Bool</span></span> | <span data-ttu-id="82c31-184">True</span><span class="sxs-lookup"><span data-stu-id="82c31-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="82c31-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="82c31-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="82c31-186">Comprueba si el primer valor es mayor o igual que el segundo.</span><span class="sxs-lookup"><span data-stu-id="82c31-186">Checks whether the first value is greater than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="82c31-187">parameters</span><span class="sxs-lookup"><span data-stu-id="82c31-187">Parameters</span></span>

| <span data-ttu-id="82c31-188">Parámetro</span><span class="sxs-lookup"><span data-stu-id="82c31-188">Parameter</span></span> | <span data-ttu-id="82c31-189">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="82c31-189">Required</span></span> | <span data-ttu-id="82c31-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-190">Type</span></span> | <span data-ttu-id="82c31-191">Descripción</span><span class="sxs-lookup"><span data-stu-id="82c31-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="82c31-192">arg1</span><span class="sxs-lookup"><span data-stu-id="82c31-192">arg1</span></span> |<span data-ttu-id="82c31-193">Sí</span><span class="sxs-lookup"><span data-stu-id="82c31-193">Yes</span></span> |<span data-ttu-id="82c31-194">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="82c31-194">int or string</span></span> |<span data-ttu-id="82c31-195">El primer valor de la comparación mayor o igual.</span><span class="sxs-lookup"><span data-stu-id="82c31-195">The first value for the greater or equal comparison.</span></span> |
| <span data-ttu-id="82c31-196">arg2</span><span class="sxs-lookup"><span data-stu-id="82c31-196">arg2</span></span> |<span data-ttu-id="82c31-197">Sí</span><span class="sxs-lookup"><span data-stu-id="82c31-197">Yes</span></span> |<span data-ttu-id="82c31-198">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="82c31-198">int or string</span></span> |<span data-ttu-id="82c31-199">El segundo valor de la comparación mayor o igual.</span><span class="sxs-lookup"><span data-stu-id="82c31-199">The second value for the greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="82c31-200">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="82c31-200">Return value</span></span>

<span data-ttu-id="82c31-201">Devuelve **True** si el primer valor es mayor o igual que el segundo; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="82c31-201">Returns **True** if the first value is greater than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="82c31-202">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="82c31-202">Example</span></span>

<span data-ttu-id="82c31-203">La plantilla de ejemplo comprueba si un valor es mayor o igual que el otro.</span><span class="sxs-lookup"><span data-stu-id="82c31-203">The example template checks whether the one value is greater than or equal to the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[greaterOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="82c31-204">La salida del ejemplo anterior con el valor predeterminado es:</span><span class="sxs-lookup"><span data-stu-id="82c31-204">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="82c31-205">Nombre</span><span class="sxs-lookup"><span data-stu-id="82c31-205">Name</span></span> | <span data-ttu-id="82c31-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-206">Type</span></span> | <span data-ttu-id="82c31-207">Valor</span><span class="sxs-lookup"><span data-stu-id="82c31-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="82c31-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="82c31-208">checkInts</span></span> | <span data-ttu-id="82c31-209">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-209">Bool</span></span> | <span data-ttu-id="82c31-210">False</span><span class="sxs-lookup"><span data-stu-id="82c31-210">False</span></span> |
| <span data-ttu-id="82c31-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="82c31-211">checkStrings</span></span> | <span data-ttu-id="82c31-212">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-212">Bool</span></span> | <span data-ttu-id="82c31-213">True</span><span class="sxs-lookup"><span data-stu-id="82c31-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="82c31-214">less</span><span class="sxs-lookup"><span data-stu-id="82c31-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="82c31-215">Comprueba si el primer valor es menor que el segundo.</span><span class="sxs-lookup"><span data-stu-id="82c31-215">Checks whether the first value is less than the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="82c31-216">parameters</span><span class="sxs-lookup"><span data-stu-id="82c31-216">Parameters</span></span>

| <span data-ttu-id="82c31-217">Parámetro</span><span class="sxs-lookup"><span data-stu-id="82c31-217">Parameter</span></span> | <span data-ttu-id="82c31-218">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="82c31-218">Required</span></span> | <span data-ttu-id="82c31-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-219">Type</span></span> | <span data-ttu-id="82c31-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="82c31-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="82c31-221">arg1</span><span class="sxs-lookup"><span data-stu-id="82c31-221">arg1</span></span> |<span data-ttu-id="82c31-222">Sí</span><span class="sxs-lookup"><span data-stu-id="82c31-222">Yes</span></span> |<span data-ttu-id="82c31-223">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="82c31-223">int or string</span></span> |<span data-ttu-id="82c31-224">El primer valor de la comparación menor.</span><span class="sxs-lookup"><span data-stu-id="82c31-224">The first value for the less comparison.</span></span> |
| <span data-ttu-id="82c31-225">arg2</span><span class="sxs-lookup"><span data-stu-id="82c31-225">arg2</span></span> |<span data-ttu-id="82c31-226">Sí</span><span class="sxs-lookup"><span data-stu-id="82c31-226">Yes</span></span> |<span data-ttu-id="82c31-227">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="82c31-227">int or string</span></span> |<span data-ttu-id="82c31-228">El segundo valor de la comparación menor.</span><span class="sxs-lookup"><span data-stu-id="82c31-228">The second value for the less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="82c31-229">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="82c31-229">Return value</span></span>

<span data-ttu-id="82c31-230">Devuelve **True** si el primer valor es menor que el segundo; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="82c31-230">Returns **True** if the first value is less than the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="82c31-231">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="82c31-231">Example</span></span>

<span data-ttu-id="82c31-232">La plantilla de ejemplo comprueba si un valor es menor que el otro.</span><span class="sxs-lookup"><span data-stu-id="82c31-232">The example template checks whether the one value is less than the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[less(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[less(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="82c31-233">La salida del ejemplo anterior con el valor predeterminado es:</span><span class="sxs-lookup"><span data-stu-id="82c31-233">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="82c31-234">Nombre</span><span class="sxs-lookup"><span data-stu-id="82c31-234">Name</span></span> | <span data-ttu-id="82c31-235">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-235">Type</span></span> | <span data-ttu-id="82c31-236">Valor</span><span class="sxs-lookup"><span data-stu-id="82c31-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="82c31-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="82c31-237">checkInts</span></span> | <span data-ttu-id="82c31-238">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-238">Bool</span></span> | <span data-ttu-id="82c31-239">True</span><span class="sxs-lookup"><span data-stu-id="82c31-239">True</span></span> |
| <span data-ttu-id="82c31-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="82c31-240">checkStrings</span></span> | <span data-ttu-id="82c31-241">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-241">Bool</span></span> | <span data-ttu-id="82c31-242">False</span><span class="sxs-lookup"><span data-stu-id="82c31-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="82c31-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="82c31-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="82c31-244">Comprueba si el primer valor es menor o igual que el segundo.</span><span class="sxs-lookup"><span data-stu-id="82c31-244">Checks whether the first value is less than or equal to the second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="82c31-245">parameters</span><span class="sxs-lookup"><span data-stu-id="82c31-245">Parameters</span></span>

| <span data-ttu-id="82c31-246">Parámetro</span><span class="sxs-lookup"><span data-stu-id="82c31-246">Parameter</span></span> | <span data-ttu-id="82c31-247">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="82c31-247">Required</span></span> | <span data-ttu-id="82c31-248">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-248">Type</span></span> | <span data-ttu-id="82c31-249">Descripción</span><span class="sxs-lookup"><span data-stu-id="82c31-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="82c31-250">arg1</span><span class="sxs-lookup"><span data-stu-id="82c31-250">arg1</span></span> |<span data-ttu-id="82c31-251">Sí</span><span class="sxs-lookup"><span data-stu-id="82c31-251">Yes</span></span> |<span data-ttu-id="82c31-252">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="82c31-252">int or string</span></span> |<span data-ttu-id="82c31-253">El primer valor de la comparación menor o igual.</span><span class="sxs-lookup"><span data-stu-id="82c31-253">The first value for the less or equals comparison.</span></span> |
| <span data-ttu-id="82c31-254">arg2</span><span class="sxs-lookup"><span data-stu-id="82c31-254">arg2</span></span> |<span data-ttu-id="82c31-255">Sí</span><span class="sxs-lookup"><span data-stu-id="82c31-255">Yes</span></span> |<span data-ttu-id="82c31-256">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="82c31-256">int or string</span></span> |<span data-ttu-id="82c31-257">El segundo valor de la comparación menor o igual.</span><span class="sxs-lookup"><span data-stu-id="82c31-257">The second value for the less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="82c31-258">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="82c31-258">Return value</span></span>

<span data-ttu-id="82c31-259">Devuelve **True** si el primer valor es menor o igual que el segundo; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="82c31-259">Returns **True** if the first value is less than or equal to the second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="82c31-260">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="82c31-260">Example</span></span>

<span data-ttu-id="82c31-261">La plantilla de ejemplo comprueba si un valor es menor o igual que el otro.</span><span class="sxs-lookup"><span data-stu-id="82c31-261">The example template checks whether the one value is less than or equal to the other.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstInt": {
            "type": "int",
            "defaultValue": 1
        },
        "secondInt": {
            "type": "int",
            "defaultValue": 2
        },
        "firstString": {
            "type": "string",
            "defaultValue": "A"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "a"
        }
    },
    "resources": [
    ],
    "outputs": {
        "checkInts": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstInt'), parameters('secondInt') )]"
        },
        "checkStrings": {
            "type": "bool",
            "value": "[lessOrEquals(parameters('firstString'), parameters('secondString'))]"
        }
    }
}
```

<span data-ttu-id="82c31-262">La salida del ejemplo anterior con el valor predeterminado es:</span><span class="sxs-lookup"><span data-stu-id="82c31-262">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="82c31-263">Nombre</span><span class="sxs-lookup"><span data-stu-id="82c31-263">Name</span></span> | <span data-ttu-id="82c31-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="82c31-264">Type</span></span> | <span data-ttu-id="82c31-265">Valor</span><span class="sxs-lookup"><span data-stu-id="82c31-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="82c31-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="82c31-266">checkInts</span></span> | <span data-ttu-id="82c31-267">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-267">Bool</span></span> | <span data-ttu-id="82c31-268">True</span><span class="sxs-lookup"><span data-stu-id="82c31-268">True</span></span> |
| <span data-ttu-id="82c31-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="82c31-269">checkStrings</span></span> | <span data-ttu-id="82c31-270">Booleano</span><span class="sxs-lookup"><span data-stu-id="82c31-270">Bool</span></span> | <span data-ttu-id="82c31-271">False</span><span class="sxs-lookup"><span data-stu-id="82c31-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="82c31-272">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82c31-272">Next steps</span></span>
* <span data-ttu-id="82c31-273">Para obtener una descripción de las secciones de una plantilla de Azure Resource Manager, vea [Creación de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="82c31-273">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="82c31-274">Para combinar varias plantillas, vea [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="82c31-274">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="82c31-275">Para iterar una cantidad de veces específica al crear un tipo de recurso, vea [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="82c31-275">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="82c31-276">Para saber cómo implementar la plantilla que creó, consulte [Implementación de una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="82c31-276">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

