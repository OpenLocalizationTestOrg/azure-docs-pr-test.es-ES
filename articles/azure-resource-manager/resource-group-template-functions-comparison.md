---
title: "funciones de plantilla de administrador de recursos de aaaAzure - comparación | Documentos de Microsoft"
description: Describe hello toouse de funciones en un toocompare de valores de la plantilla de Azure Resource Manager.
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
ms.openlocfilehash: ebcfc9ed6c93f8b540ec4c066e9457c621800b7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="ee617-103">Funciones de comparación para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee617-103">Comparison functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="ee617-104">Resource Manager proporciona varias funciones para realizar comparaciones en las plantillas.</span><span class="sxs-lookup"><span data-stu-id="ee617-104">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="ee617-105">equals</span><span class="sxs-lookup"><span data-stu-id="ee617-105">equals</span></span>](#equals)
* [<span data-ttu-id="ee617-106">greater</span><span class="sxs-lookup"><span data-stu-id="ee617-106">greater</span></span>](#greater)
* [<span data-ttu-id="ee617-107">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="ee617-107">greaterOrEquals</span></span>](#greaterorequals)
* [<span data-ttu-id="ee617-108">less</span><span class="sxs-lookup"><span data-stu-id="ee617-108">less</span></span>](#less)
* [<span data-ttu-id="ee617-109">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="ee617-109">lessOrEquals</span></span>](#lessorequals)

## <a name="equals"></a><span data-ttu-id="ee617-110">equals</span><span class="sxs-lookup"><span data-stu-id="ee617-110">equals</span></span>
`equals(arg1, arg2)`

<span data-ttu-id="ee617-111">Comprueba si dos valores son iguales.</span><span class="sxs-lookup"><span data-stu-id="ee617-111">Checks whether two values equal each other.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee617-112">parameters</span><span class="sxs-lookup"><span data-stu-id="ee617-112">Parameters</span></span>

| <span data-ttu-id="ee617-113">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ee617-113">Parameter</span></span> | <span data-ttu-id="ee617-114">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ee617-114">Required</span></span> | <span data-ttu-id="ee617-115">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-115">Type</span></span> | <span data-ttu-id="ee617-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="ee617-116">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ee617-117">arg1</span><span class="sxs-lookup"><span data-stu-id="ee617-117">arg1</span></span> |<span data-ttu-id="ee617-118">Sí</span><span class="sxs-lookup"><span data-stu-id="ee617-118">Yes</span></span> |<span data-ttu-id="ee617-119">entero, cadena, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="ee617-119">int, string, array, or object</span></span> |<span data-ttu-id="ee617-120">Hola primer toocheck de valor para la igualdad.</span><span class="sxs-lookup"><span data-stu-id="ee617-120">hello first value toocheck for equality.</span></span> |
| <span data-ttu-id="ee617-121">arg2</span><span class="sxs-lookup"><span data-stu-id="ee617-121">arg2</span></span> |<span data-ttu-id="ee617-122">Sí</span><span class="sxs-lookup"><span data-stu-id="ee617-122">Yes</span></span> |<span data-ttu-id="ee617-123">entero, cadena, matriz u objeto</span><span class="sxs-lookup"><span data-stu-id="ee617-123">int, string, array, or object</span></span> |<span data-ttu-id="ee617-124">Hola segundo toocheck de valor para la igualdad.</span><span class="sxs-lookup"><span data-stu-id="ee617-124">hello second value toocheck for equality.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ee617-125">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ee617-125">Return value</span></span>

<span data-ttu-id="ee617-126">Devuelve **True** si Hola valores son iguales; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="ee617-126">Returns **True** if hello values are equal; otherwise, **False**.</span></span>

### <a name="remarks"></a><span data-ttu-id="ee617-127">Comentarios</span><span class="sxs-lookup"><span data-stu-id="ee617-127">Remarks</span></span>

<span data-ttu-id="ee617-128">Hello es igual a función se suele utilizar con hello `condition` tootest del elemento si se implementa un recurso.</span><span class="sxs-lookup"><span data-stu-id="ee617-128">hello equals function is often used with hello `condition` element tootest whether a resource is deployed.</span></span>

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

### <a name="example"></a><span data-ttu-id="ee617-129">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ee617-129">Example</span></span>

<span data-ttu-id="ee617-130">plantilla de ejemplo de Hola comprueba diferentes tipos de valores para la igualdad.</span><span class="sxs-lookup"><span data-stu-id="ee617-130">hello example template checks different types of values for equality.</span></span> <span data-ttu-id="ee617-131">Todos los valores predeterminados de hello devuelven True.</span><span class="sxs-lookup"><span data-stu-id="ee617-131">All hello default values return True.</span></span>

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

<span data-ttu-id="ee617-132">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="ee617-132">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ee617-133">Nombre</span><span class="sxs-lookup"><span data-stu-id="ee617-133">Name</span></span> | <span data-ttu-id="ee617-134">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-134">Type</span></span> | <span data-ttu-id="ee617-135">Valor</span><span class="sxs-lookup"><span data-stu-id="ee617-135">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ee617-136">checkInts</span><span class="sxs-lookup"><span data-stu-id="ee617-136">checkInts</span></span> | <span data-ttu-id="ee617-137">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-137">Bool</span></span> | <span data-ttu-id="ee617-138">True</span><span class="sxs-lookup"><span data-stu-id="ee617-138">True</span></span> |
| <span data-ttu-id="ee617-139">checkStrings</span><span class="sxs-lookup"><span data-stu-id="ee617-139">checkStrings</span></span> | <span data-ttu-id="ee617-140">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-140">Bool</span></span> | <span data-ttu-id="ee617-141">True</span><span class="sxs-lookup"><span data-stu-id="ee617-141">True</span></span> |
| <span data-ttu-id="ee617-142">checkArrays</span><span class="sxs-lookup"><span data-stu-id="ee617-142">checkArrays</span></span> | <span data-ttu-id="ee617-143">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-143">Bool</span></span> | <span data-ttu-id="ee617-144">True</span><span class="sxs-lookup"><span data-stu-id="ee617-144">True</span></span> |
| <span data-ttu-id="ee617-145">checkObjects</span><span class="sxs-lookup"><span data-stu-id="ee617-145">checkObjects</span></span> | <span data-ttu-id="ee617-146">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-146">Bool</span></span> | <span data-ttu-id="ee617-147">True</span><span class="sxs-lookup"><span data-stu-id="ee617-147">True</span></span> |


<span data-ttu-id="ee617-148">Hello siguiente ejemplo se utiliza [no](resource-group-template-functions-logical.md#not) con **es igual a**.</span><span class="sxs-lookup"><span data-stu-id="ee617-148">hello following example uses [not](resource-group-template-functions-logical.md#not) with **equals**.</span></span>

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

<span data-ttu-id="ee617-149">resultado Hola Hola anterior ejemplo es:</span><span class="sxs-lookup"><span data-stu-id="ee617-149">hello output from hello preceding example is:</span></span>

| <span data-ttu-id="ee617-150">Nombre</span><span class="sxs-lookup"><span data-stu-id="ee617-150">Name</span></span> | <span data-ttu-id="ee617-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-151">Type</span></span> | <span data-ttu-id="ee617-152">Valor</span><span class="sxs-lookup"><span data-stu-id="ee617-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ee617-153">checkNotEquals</span><span class="sxs-lookup"><span data-stu-id="ee617-153">checkNotEquals</span></span> | <span data-ttu-id="ee617-154">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-154">Bool</span></span> | <span data-ttu-id="ee617-155">True</span><span class="sxs-lookup"><span data-stu-id="ee617-155">True</span></span> |


## <a name="greater"></a><span data-ttu-id="ee617-156">greater</span><span class="sxs-lookup"><span data-stu-id="ee617-156">greater</span></span>
`greater(arg1, arg2)`

<span data-ttu-id="ee617-157">Comprueba si el primer valor de hello es mayor que el segundo valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee617-157">Checks whether hello first value is greater than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee617-158">parameters</span><span class="sxs-lookup"><span data-stu-id="ee617-158">Parameters</span></span>

| <span data-ttu-id="ee617-159">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ee617-159">Parameter</span></span> | <span data-ttu-id="ee617-160">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ee617-160">Required</span></span> | <span data-ttu-id="ee617-161">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-161">Type</span></span> | <span data-ttu-id="ee617-162">Descripción</span><span class="sxs-lookup"><span data-stu-id="ee617-162">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ee617-163">arg1</span><span class="sxs-lookup"><span data-stu-id="ee617-163">arg1</span></span> |<span data-ttu-id="ee617-164">Sí</span><span class="sxs-lookup"><span data-stu-id="ee617-164">Yes</span></span> |<span data-ttu-id="ee617-165">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="ee617-165">int or string</span></span> |<span data-ttu-id="ee617-166">Hola primer valor de comparación mayor Hola.</span><span class="sxs-lookup"><span data-stu-id="ee617-166">hello first value for hello greater comparison.</span></span> |
| <span data-ttu-id="ee617-167">arg2</span><span class="sxs-lookup"><span data-stu-id="ee617-167">arg2</span></span> |<span data-ttu-id="ee617-168">Sí</span><span class="sxs-lookup"><span data-stu-id="ee617-168">Yes</span></span> |<span data-ttu-id="ee617-169">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="ee617-169">int or string</span></span> |<span data-ttu-id="ee617-170">Hola segundo valor de comparación mayor Hola.</span><span class="sxs-lookup"><span data-stu-id="ee617-170">hello second value for hello greater comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ee617-171">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ee617-171">Return value</span></span>

<span data-ttu-id="ee617-172">Devuelve **True** si Hola primer valor es mayor que el segundo valor de hello; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="ee617-172">Returns **True** if hello first value is greater than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="ee617-173">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ee617-173">Example</span></span>

<span data-ttu-id="ee617-174">plantilla de ejemplo de Hola comprueba si un valor de hello es mayor que Hola otro.</span><span class="sxs-lookup"><span data-stu-id="ee617-174">hello example template checks whether hello one value is greater than hello other.</span></span>

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

<span data-ttu-id="ee617-175">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="ee617-175">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ee617-176">Nombre</span><span class="sxs-lookup"><span data-stu-id="ee617-176">Name</span></span> | <span data-ttu-id="ee617-177">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-177">Type</span></span> | <span data-ttu-id="ee617-178">Valor</span><span class="sxs-lookup"><span data-stu-id="ee617-178">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ee617-179">checkInts</span><span class="sxs-lookup"><span data-stu-id="ee617-179">checkInts</span></span> | <span data-ttu-id="ee617-180">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-180">Bool</span></span> | <span data-ttu-id="ee617-181">False</span><span class="sxs-lookup"><span data-stu-id="ee617-181">False</span></span> |
| <span data-ttu-id="ee617-182">checkStrings</span><span class="sxs-lookup"><span data-stu-id="ee617-182">checkStrings</span></span> | <span data-ttu-id="ee617-183">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-183">Bool</span></span> | <span data-ttu-id="ee617-184">True</span><span class="sxs-lookup"><span data-stu-id="ee617-184">True</span></span> |


## <a name="greaterorequals"></a><span data-ttu-id="ee617-185">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="ee617-185">greaterOrEquals</span></span>
`greaterOrEquals(arg1, arg2)`

<span data-ttu-id="ee617-186">Comprueba si el primer valor de hello es igual o mayor que toohello segundo valor.</span><span class="sxs-lookup"><span data-stu-id="ee617-186">Checks whether hello first value is greater than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee617-187">parameters</span><span class="sxs-lookup"><span data-stu-id="ee617-187">Parameters</span></span>

| <span data-ttu-id="ee617-188">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ee617-188">Parameter</span></span> | <span data-ttu-id="ee617-189">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ee617-189">Required</span></span> | <span data-ttu-id="ee617-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-190">Type</span></span> | <span data-ttu-id="ee617-191">Descripción</span><span class="sxs-lookup"><span data-stu-id="ee617-191">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ee617-192">arg1</span><span class="sxs-lookup"><span data-stu-id="ee617-192">arg1</span></span> |<span data-ttu-id="ee617-193">Sí</span><span class="sxs-lookup"><span data-stu-id="ee617-193">Yes</span></span> |<span data-ttu-id="ee617-194">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="ee617-194">int or string</span></span> |<span data-ttu-id="ee617-195">Hola primer valor de comparación mayor o igual que de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee617-195">hello first value for hello greater or equal comparison.</span></span> |
| <span data-ttu-id="ee617-196">arg2</span><span class="sxs-lookup"><span data-stu-id="ee617-196">arg2</span></span> |<span data-ttu-id="ee617-197">Sí</span><span class="sxs-lookup"><span data-stu-id="ee617-197">Yes</span></span> |<span data-ttu-id="ee617-198">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="ee617-198">int or string</span></span> |<span data-ttu-id="ee617-199">Hola segundo valor de comparación mayor o igual que de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee617-199">hello second value for hello greater or equal comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ee617-200">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ee617-200">Return value</span></span>

<span data-ttu-id="ee617-201">Devuelve **True** si Hola primer valor es mayor o igual toohello segundo; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="ee617-201">Returns **True** if hello first value is greater than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="ee617-202">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ee617-202">Example</span></span>

<span data-ttu-id="ee617-203">plantilla de ejemplo de Hola comprueba si un valor de hello es mayor que o igual toohello otro.</span><span class="sxs-lookup"><span data-stu-id="ee617-203">hello example template checks whether hello one value is greater than or equal toohello other.</span></span>

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

<span data-ttu-id="ee617-204">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="ee617-204">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ee617-205">Nombre</span><span class="sxs-lookup"><span data-stu-id="ee617-205">Name</span></span> | <span data-ttu-id="ee617-206">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-206">Type</span></span> | <span data-ttu-id="ee617-207">Valor</span><span class="sxs-lookup"><span data-stu-id="ee617-207">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ee617-208">checkInts</span><span class="sxs-lookup"><span data-stu-id="ee617-208">checkInts</span></span> | <span data-ttu-id="ee617-209">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-209">Bool</span></span> | <span data-ttu-id="ee617-210">False</span><span class="sxs-lookup"><span data-stu-id="ee617-210">False</span></span> |
| <span data-ttu-id="ee617-211">checkStrings</span><span class="sxs-lookup"><span data-stu-id="ee617-211">checkStrings</span></span> | <span data-ttu-id="ee617-212">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-212">Bool</span></span> | <span data-ttu-id="ee617-213">True</span><span class="sxs-lookup"><span data-stu-id="ee617-213">True</span></span> |



## <a name="less"></a><span data-ttu-id="ee617-214">less</span><span class="sxs-lookup"><span data-stu-id="ee617-214">less</span></span>
`less(arg1, arg2)`

<span data-ttu-id="ee617-215">Comprueba si Hola primer valor es menor que Hola segundo valor.</span><span class="sxs-lookup"><span data-stu-id="ee617-215">Checks whether hello first value is less than hello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee617-216">parameters</span><span class="sxs-lookup"><span data-stu-id="ee617-216">Parameters</span></span>

| <span data-ttu-id="ee617-217">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ee617-217">Parameter</span></span> | <span data-ttu-id="ee617-218">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ee617-218">Required</span></span> | <span data-ttu-id="ee617-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-219">Type</span></span> | <span data-ttu-id="ee617-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="ee617-220">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ee617-221">arg1</span><span class="sxs-lookup"><span data-stu-id="ee617-221">arg1</span></span> |<span data-ttu-id="ee617-222">Sí</span><span class="sxs-lookup"><span data-stu-id="ee617-222">Yes</span></span> |<span data-ttu-id="ee617-223">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="ee617-223">int or string</span></span> |<span data-ttu-id="ee617-224">primer valor de Hola para hello menos comparación.</span><span class="sxs-lookup"><span data-stu-id="ee617-224">hello first value for hello less comparison.</span></span> |
| <span data-ttu-id="ee617-225">arg2</span><span class="sxs-lookup"><span data-stu-id="ee617-225">arg2</span></span> |<span data-ttu-id="ee617-226">Sí</span><span class="sxs-lookup"><span data-stu-id="ee617-226">Yes</span></span> |<span data-ttu-id="ee617-227">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="ee617-227">int or string</span></span> |<span data-ttu-id="ee617-228">segundo valor de Hola para hello menos comparación.</span><span class="sxs-lookup"><span data-stu-id="ee617-228">hello second value for hello less comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ee617-229">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ee617-229">Return value</span></span>

<span data-ttu-id="ee617-230">Devuelve **True** si Hola primer valor es menor que Hola segundo valor; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="ee617-230">Returns **True** if hello first value is less than hello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="ee617-231">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ee617-231">Example</span></span>

<span data-ttu-id="ee617-232">plantilla de ejemplo de Hola comprueba si un valor de hello es menor que Hola otro.</span><span class="sxs-lookup"><span data-stu-id="ee617-232">hello example template checks whether hello one value is less than hello other.</span></span>

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

<span data-ttu-id="ee617-233">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="ee617-233">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ee617-234">Nombre</span><span class="sxs-lookup"><span data-stu-id="ee617-234">Name</span></span> | <span data-ttu-id="ee617-235">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-235">Type</span></span> | <span data-ttu-id="ee617-236">Valor</span><span class="sxs-lookup"><span data-stu-id="ee617-236">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ee617-237">checkInts</span><span class="sxs-lookup"><span data-stu-id="ee617-237">checkInts</span></span> | <span data-ttu-id="ee617-238">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-238">Bool</span></span> | <span data-ttu-id="ee617-239">True</span><span class="sxs-lookup"><span data-stu-id="ee617-239">True</span></span> |
| <span data-ttu-id="ee617-240">checkStrings</span><span class="sxs-lookup"><span data-stu-id="ee617-240">checkStrings</span></span> | <span data-ttu-id="ee617-241">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-241">Bool</span></span> | <span data-ttu-id="ee617-242">False</span><span class="sxs-lookup"><span data-stu-id="ee617-242">False</span></span> |


## <a name="lessorequals"></a><span data-ttu-id="ee617-243">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="ee617-243">lessOrEquals</span></span>
`lessOrEquals(arg1, arg2)`

<span data-ttu-id="ee617-244">Comprueba si el primer valor de hello es menor o igual toohello segundo valor.</span><span class="sxs-lookup"><span data-stu-id="ee617-244">Checks whether hello first value is less than or equal toohello second value.</span></span>

### <a name="parameters"></a><span data-ttu-id="ee617-245">parameters</span><span class="sxs-lookup"><span data-stu-id="ee617-245">Parameters</span></span>

| <span data-ttu-id="ee617-246">Parámetro</span><span class="sxs-lookup"><span data-stu-id="ee617-246">Parameter</span></span> | <span data-ttu-id="ee617-247">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="ee617-247">Required</span></span> | <span data-ttu-id="ee617-248">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-248">Type</span></span> | <span data-ttu-id="ee617-249">Descripción</span><span class="sxs-lookup"><span data-stu-id="ee617-249">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="ee617-250">arg1</span><span class="sxs-lookup"><span data-stu-id="ee617-250">arg1</span></span> |<span data-ttu-id="ee617-251">Sí</span><span class="sxs-lookup"><span data-stu-id="ee617-251">Yes</span></span> |<span data-ttu-id="ee617-252">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="ee617-252">int or string</span></span> |<span data-ttu-id="ee617-253">primer valor de Hola para hello menos o comparación de igualdad.</span><span class="sxs-lookup"><span data-stu-id="ee617-253">hello first value for hello less or equals comparison.</span></span> |
| <span data-ttu-id="ee617-254">arg2</span><span class="sxs-lookup"><span data-stu-id="ee617-254">arg2</span></span> |<span data-ttu-id="ee617-255">Sí</span><span class="sxs-lookup"><span data-stu-id="ee617-255">Yes</span></span> |<span data-ttu-id="ee617-256">entero o cadena</span><span class="sxs-lookup"><span data-stu-id="ee617-256">int or string</span></span> |<span data-ttu-id="ee617-257">Hola segundo valor de hello menor o igual que comparación.</span><span class="sxs-lookup"><span data-stu-id="ee617-257">hello second value for hello less or equals comparison.</span></span> |

### <a name="return-value"></a><span data-ttu-id="ee617-258">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="ee617-258">Return value</span></span>

<span data-ttu-id="ee617-259">Devuelve **True** si Hola primer valor es menor o igual toohello segundo valor; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="ee617-259">Returns **True** if hello first value is less than or equal toohello second value; otherwise, **False**.</span></span>

### <a name="example"></a><span data-ttu-id="ee617-260">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ee617-260">Example</span></span>

<span data-ttu-id="ee617-261">Hello plantilla en el ejemplo se comprueba si un valor de hello es menor o igual toohello otro.</span><span class="sxs-lookup"><span data-stu-id="ee617-261">hello example template checks whether hello one value is less than or equal toohello other.</span></span>

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

<span data-ttu-id="ee617-262">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="ee617-262">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="ee617-263">Nombre</span><span class="sxs-lookup"><span data-stu-id="ee617-263">Name</span></span> | <span data-ttu-id="ee617-264">Tipo</span><span class="sxs-lookup"><span data-stu-id="ee617-264">Type</span></span> | <span data-ttu-id="ee617-265">Valor</span><span class="sxs-lookup"><span data-stu-id="ee617-265">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="ee617-266">checkInts</span><span class="sxs-lookup"><span data-stu-id="ee617-266">checkInts</span></span> | <span data-ttu-id="ee617-267">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-267">Bool</span></span> | <span data-ttu-id="ee617-268">True</span><span class="sxs-lookup"><span data-stu-id="ee617-268">True</span></span> |
| <span data-ttu-id="ee617-269">checkStrings</span><span class="sxs-lookup"><span data-stu-id="ee617-269">checkStrings</span></span> | <span data-ttu-id="ee617-270">Booleano</span><span class="sxs-lookup"><span data-stu-id="ee617-270">Bool</span></span> | <span data-ttu-id="ee617-271">False</span><span class="sxs-lookup"><span data-stu-id="ee617-271">False</span></span> |



## <a name="next-steps"></a><span data-ttu-id="ee617-272">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee617-272">Next steps</span></span>
* <span data-ttu-id="ee617-273">Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ee617-273">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="ee617-274">toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ee617-274">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="ee617-275">tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="ee617-275">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="ee617-276">toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ee617-276">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

