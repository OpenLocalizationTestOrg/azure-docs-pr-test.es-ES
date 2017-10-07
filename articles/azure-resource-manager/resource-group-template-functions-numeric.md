---
title: "funciones de plantilla de administrador de recursos aaaAzure - numéricas | Documentos de Microsoft"
description: "Hola toouse de funciones en un toowork de plantilla de Azure Resource Manager se describen con números."
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
ms.openlocfilehash: 855d5b354d094b9815edc160e3d72efbfd36ba77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="numeric-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="2bb86-103">Funciones numéricas para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2bb86-103">Numeric functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="2bb86-104">Administrador de recursos proporciona Hola siguientes funciones para trabajar con números enteros:</span><span class="sxs-lookup"><span data-stu-id="2bb86-104">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="2bb86-105">agregar</span><span class="sxs-lookup"><span data-stu-id="2bb86-105">add</span></span>](#add)
* [<span data-ttu-id="2bb86-106">copyIndex</span><span class="sxs-lookup"><span data-stu-id="2bb86-106">copyIndex</span></span>](#copyindex)
* [<span data-ttu-id="2bb86-107">div</span><span class="sxs-lookup"><span data-stu-id="2bb86-107">div</span></span>](#div)
* [<span data-ttu-id="2bb86-108">float</span><span class="sxs-lookup"><span data-stu-id="2bb86-108">float</span></span>](#float)
* [<span data-ttu-id="2bb86-109">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-109">int</span></span>](#int)
* [<span data-ttu-id="2bb86-110">min</span><span class="sxs-lookup"><span data-stu-id="2bb86-110">min</span></span>](#min)
* [<span data-ttu-id="2bb86-111">max</span><span class="sxs-lookup"><span data-stu-id="2bb86-111">max</span></span>](#max)
* [<span data-ttu-id="2bb86-112">mod</span><span class="sxs-lookup"><span data-stu-id="2bb86-112">mod</span></span>](#mod)
* [<span data-ttu-id="2bb86-113">mul</span><span class="sxs-lookup"><span data-stu-id="2bb86-113">mul</span></span>](#mul)
* [<span data-ttu-id="2bb86-114">sub</span><span class="sxs-lookup"><span data-stu-id="2bb86-114">sub</span></span>](#sub)

<a id="add" />

## <a name="add"></a><span data-ttu-id="2bb86-115">agregar</span><span class="sxs-lookup"><span data-stu-id="2bb86-115">add</span></span>
`add(operand1, operand2)`

<span data-ttu-id="2bb86-116">Devuelve Hola suma de dos enteros proporcionado Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-116">Returns hello sum of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="2bb86-117">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb86-117">Parameters</span></span>

| <span data-ttu-id="2bb86-118">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2bb86-118">Parameter</span></span> | <span data-ttu-id="2bb86-119">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2bb86-119">Required</span></span> | <span data-ttu-id="2bb86-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-120">Type</span></span> | <span data-ttu-id="2bb86-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="2bb86-121">Description</span></span> |
|:--- |:--- |:--- |:--- | 
|<span data-ttu-id="2bb86-122">operand1</span><span class="sxs-lookup"><span data-stu-id="2bb86-122">operand1</span></span> |<span data-ttu-id="2bb86-123">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-123">Yes</span></span> |<span data-ttu-id="2bb86-124">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-124">int</span></span> |<span data-ttu-id="2bb86-125">Primero debe numerar tooadd.</span><span class="sxs-lookup"><span data-stu-id="2bb86-125">First number tooadd.</span></span> |
|<span data-ttu-id="2bb86-126">operand2</span><span class="sxs-lookup"><span data-stu-id="2bb86-126">operand2</span></span> |<span data-ttu-id="2bb86-127">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-127">Yes</span></span> |<span data-ttu-id="2bb86-128">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-128">int</span></span> |<span data-ttu-id="2bb86-129">Segundo número tooadd.</span><span class="sxs-lookup"><span data-stu-id="2bb86-129">Second number tooadd.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2bb86-130">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2bb86-130">Return value</span></span>

<span data-ttu-id="2bb86-131">Un entero que contiene la suma de Hola de parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-131">An integer that contains hello sum of hello parameters.</span></span>

### <a name="example"></a><span data-ttu-id="2bb86-132">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2bb86-132">Example</span></span>

<span data-ttu-id="2bb86-133">Hola ejemplo siguiente agrega dos parámetros.</span><span class="sxs-lookup"><span data-stu-id="2bb86-133">hello following example adds two parameters.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer tooadd"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer tooadd"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "addResult": {
            "type": "int",
            "value": "[add(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="2bb86-134">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="2bb86-134">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2bb86-135">Nombre</span><span class="sxs-lookup"><span data-stu-id="2bb86-135">Name</span></span> | <span data-ttu-id="2bb86-136">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-136">Type</span></span> | <span data-ttu-id="2bb86-137">Valor</span><span class="sxs-lookup"><span data-stu-id="2bb86-137">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2bb86-138">addResult</span><span class="sxs-lookup"><span data-stu-id="2bb86-138">addResult</span></span> | <span data-ttu-id="2bb86-139">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-139">Int</span></span> | <span data-ttu-id="2bb86-140">8</span><span class="sxs-lookup"><span data-stu-id="2bb86-140">8</span></span> |

<a id="copyindex" />

## <a name="copyindex"></a><span data-ttu-id="2bb86-141">copyIndex</span><span class="sxs-lookup"><span data-stu-id="2bb86-141">copyIndex</span></span>
`copyIndex(loopName, offset)`

<span data-ttu-id="2bb86-142">Devuelve Hola índice de un bucle de iteración.</span><span class="sxs-lookup"><span data-stu-id="2bb86-142">Returns hello index of an iteration loop.</span></span> 

### <a name="parameters"></a><span data-ttu-id="2bb86-143">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb86-143">Parameters</span></span>

| <span data-ttu-id="2bb86-144">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2bb86-144">Parameter</span></span> | <span data-ttu-id="2bb86-145">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2bb86-145">Required</span></span> | <span data-ttu-id="2bb86-146">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-146">Type</span></span> | <span data-ttu-id="2bb86-147">Descripción</span><span class="sxs-lookup"><span data-stu-id="2bb86-147">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2bb86-148">loopName</span><span class="sxs-lookup"><span data-stu-id="2bb86-148">loopName</span></span> | <span data-ttu-id="2bb86-149">No</span><span class="sxs-lookup"><span data-stu-id="2bb86-149">No</span></span> | <span data-ttu-id="2bb86-150">cadena</span><span class="sxs-lookup"><span data-stu-id="2bb86-150">string</span></span> | <span data-ttu-id="2bb86-151">nombre de Hola de bucle de Hola para obtener iteración Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-151">hello name of hello loop for getting hello iteration.</span></span> |
| <span data-ttu-id="2bb86-152">Offset</span><span class="sxs-lookup"><span data-stu-id="2bb86-152">offset</span></span> |<span data-ttu-id="2bb86-153">No</span><span class="sxs-lookup"><span data-stu-id="2bb86-153">No</span></span> |<span data-ttu-id="2bb86-154">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-154">int</span></span> |<span data-ttu-id="2bb86-155">Hola tooadd toohello basado en cero del iteración valor numérico.</span><span class="sxs-lookup"><span data-stu-id="2bb86-155">hello number tooadd toohello zero-based iteration value.</span></span> |

### <a name="remarks"></a><span data-ttu-id="2bb86-156">Comentarios</span><span class="sxs-lookup"><span data-stu-id="2bb86-156">Remarks</span></span>

<span data-ttu-id="2bb86-157">Esta función siempre se usa con un objeto **copy** .</span><span class="sxs-lookup"><span data-stu-id="2bb86-157">This function is always used with a **copy** object.</span></span> <span data-ttu-id="2bb86-158">Si no se proporciona ningún valor para **desplazamiento**, se devuelve el valor actual de la iteración de Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-158">If no value is provided for **offset**, hello current iteration value is returned.</span></span> <span data-ttu-id="2bb86-159">valor de la iteración de Hello comienza en cero.</span><span class="sxs-lookup"><span data-stu-id="2bb86-159">hello iteration value starts at zero.</span></span>

<span data-ttu-id="2bb86-160">Hola **loopName** propiedad le permite toospecify si hace referencia copyIndex tooa iteración de recursos o la iteración de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="2bb86-160">hello **loopName** property enables you toospecify whether copyIndex is referring tooa resource iteration or property iteration.</span></span> <span data-ttu-id="2bb86-161">Si no se proporciona ningún valor para **loopName**, se utiliza la iteración de tipo de recurso actual Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-161">If no value is provided for **loopName**, hello current resource type iteration is used.</span></span> <span data-ttu-id="2bb86-162">Proporcione un valor para **loopName** al iterar en una propiedad.</span><span class="sxs-lookup"><span data-stu-id="2bb86-162">Provide a value for **loopName** when iterating on a property.</span></span> 
 
<span data-ttu-id="2bb86-163">Para ver una descripción completa de cómo usar **copyIndex**, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2bb86-163">For a complete description of how you use **copyIndex**, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

### <a name="example"></a><span data-ttu-id="2bb86-164">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2bb86-164">Example</span></span>

<span data-ttu-id="2bb86-165">Hello en el ejemplo siguiente se muestra un valor copia hello y bucle índice incluido en el nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-165">hello following example shows a copy loop and hello index value included in hello name.</span></span> 

```json
"resources": [ 
  { 
    "name": "[concat('examplecopy-', copyIndex())]", 
    "type": "Microsoft.Web/sites", 
    "copy": { 
      "name": "websitescopy", 
      "count": "[parameters('count')]" 
    }, 
    ...
  }
]
```

### <a name="return-value"></a><span data-ttu-id="2bb86-166">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2bb86-166">Return value</span></span>

<span data-ttu-id="2bb86-167">Un entero que representa el índice actual de hello del iteración Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-167">An integer representing hello current index of hello iteration.</span></span>

<a id="div" />

## <a name="div"></a><span data-ttu-id="2bb86-168">div</span><span class="sxs-lookup"><span data-stu-id="2bb86-168">div</span></span>
`div(operand1, operand2)`

<span data-ttu-id="2bb86-169">Devuelve Hola división de enteros de dos enteros de proporcionado Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-169">Returns hello integer division of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="2bb86-170">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb86-170">Parameters</span></span>

| <span data-ttu-id="2bb86-171">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2bb86-171">Parameter</span></span> | <span data-ttu-id="2bb86-172">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2bb86-172">Required</span></span> | <span data-ttu-id="2bb86-173">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-173">Type</span></span> | <span data-ttu-id="2bb86-174">Descripción</span><span class="sxs-lookup"><span data-stu-id="2bb86-174">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2bb86-175">operand1</span><span class="sxs-lookup"><span data-stu-id="2bb86-175">operand1</span></span> |<span data-ttu-id="2bb86-176">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-176">Yes</span></span> |<span data-ttu-id="2bb86-177">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-177">int</span></span> |<span data-ttu-id="2bb86-178">número de Hola que se va a dividir.</span><span class="sxs-lookup"><span data-stu-id="2bb86-178">hello number being divided.</span></span> |
| <span data-ttu-id="2bb86-179">operand2</span><span class="sxs-lookup"><span data-stu-id="2bb86-179">operand2</span></span> |<span data-ttu-id="2bb86-180">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-180">Yes</span></span> |<span data-ttu-id="2bb86-181">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-181">int</span></span> |<span data-ttu-id="2bb86-182">Hola número toodivide usado.</span><span class="sxs-lookup"><span data-stu-id="2bb86-182">hello number that is used toodivide.</span></span> <span data-ttu-id="2bb86-183">No puede ser 0.</span><span class="sxs-lookup"><span data-stu-id="2bb86-183">Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2bb86-184">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2bb86-184">Return value</span></span>

<span data-ttu-id="2bb86-185">Una división Hola de enteros que representan.</span><span class="sxs-lookup"><span data-stu-id="2bb86-185">An integer representing hello division.</span></span>

### <a name="example"></a><span data-ttu-id="2bb86-186">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2bb86-186">Example</span></span>

<span data-ttu-id="2bb86-187">Hola siguiente ejemplo divide un parámetro por otro parámetro.</span><span class="sxs-lookup"><span data-stu-id="2bb86-187">hello following example divides one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 8,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "divResult": {
            "type": "int",
            "value": "[div(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="2bb86-188">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="2bb86-188">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2bb86-189">Nombre</span><span class="sxs-lookup"><span data-stu-id="2bb86-189">Name</span></span> | <span data-ttu-id="2bb86-190">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-190">Type</span></span> | <span data-ttu-id="2bb86-191">Valor</span><span class="sxs-lookup"><span data-stu-id="2bb86-191">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2bb86-192">divResult</span><span class="sxs-lookup"><span data-stu-id="2bb86-192">divResult</span></span> | <span data-ttu-id="2bb86-193">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-193">Int</span></span> | <span data-ttu-id="2bb86-194">2</span><span class="sxs-lookup"><span data-stu-id="2bb86-194">2</span></span> |

<a id="float" />

## <a name="float"></a><span data-ttu-id="2bb86-195">float</span><span class="sxs-lookup"><span data-stu-id="2bb86-195">float</span></span>
`float(arg1)`

<span data-ttu-id="2bb86-196">Convierte Hola valor tooa números de punto flotante.</span><span class="sxs-lookup"><span data-stu-id="2bb86-196">Converts hello value tooa floating point number.</span></span> <span data-ttu-id="2bb86-197">Solo, esta función se usan al pasar parámetros personalizados aplicación tooan, por ejemplo, una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="2bb86-197">You only use this function when passing custom parameters tooan application, such as a Logic App.</span></span>

### <a name="parameters"></a><span data-ttu-id="2bb86-198">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb86-198">Parameters</span></span>

| <span data-ttu-id="2bb86-199">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2bb86-199">Parameter</span></span> | <span data-ttu-id="2bb86-200">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2bb86-200">Required</span></span> | <span data-ttu-id="2bb86-201">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-201">Type</span></span> | <span data-ttu-id="2bb86-202">Descripción</span><span class="sxs-lookup"><span data-stu-id="2bb86-202">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2bb86-203">arg1</span><span class="sxs-lookup"><span data-stu-id="2bb86-203">arg1</span></span> |<span data-ttu-id="2bb86-204">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-204">Yes</span></span> |<span data-ttu-id="2bb86-205">cadena o entero</span><span class="sxs-lookup"><span data-stu-id="2bb86-205">string or int</span></span> |<span data-ttu-id="2bb86-206">Hola valor tooconvert tooa números de punto flotante.</span><span class="sxs-lookup"><span data-stu-id="2bb86-206">hello value tooconvert tooa floating point number.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2bb86-207">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2bb86-207">Return value</span></span>
<span data-ttu-id="2bb86-208">Un número de punto flotante.</span><span class="sxs-lookup"><span data-stu-id="2bb86-208">A floating point number.</span></span>

### <a name="example"></a><span data-ttu-id="2bb86-209">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2bb86-209">Example</span></span>

<span data-ttu-id="2bb86-210">Hola de ejemplo siguiente muestra cómo toouse float toopass parámetros tooa aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="2bb86-210">hello following example shows how toouse float toopass parameters tooa Logic App:</span></span>

```json
{
    "type": "Microsoft.Logic/workflows",
    "properties": {
        ...
        "parameters": {
        "custom1": {
            "value": "[float('3.0')]"
        },
        "custom2": {
            "value": "[float(3)]"
        },
```

<a id="int" />

## <a name="int"></a><span data-ttu-id="2bb86-211">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-211">int</span></span>
`int(valueToConvert)`

<span data-ttu-id="2bb86-212">Convierte el entero de tooan de valor especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-212">Converts hello specified value tooan integer.</span></span>

### <a name="parameters"></a><span data-ttu-id="2bb86-213">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb86-213">Parameters</span></span>

| <span data-ttu-id="2bb86-214">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2bb86-214">Parameter</span></span> | <span data-ttu-id="2bb86-215">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2bb86-215">Required</span></span> | <span data-ttu-id="2bb86-216">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-216">Type</span></span> | <span data-ttu-id="2bb86-217">Descripción</span><span class="sxs-lookup"><span data-stu-id="2bb86-217">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2bb86-218">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="2bb86-218">valueToConvert</span></span> |<span data-ttu-id="2bb86-219">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-219">Yes</span></span> |<span data-ttu-id="2bb86-220">cadena o entero</span><span class="sxs-lookup"><span data-stu-id="2bb86-220">string or int</span></span> |<span data-ttu-id="2bb86-221">entero de Hello valor tooconvert tooan.</span><span class="sxs-lookup"><span data-stu-id="2bb86-221">hello value tooconvert tooan integer.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2bb86-222">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2bb86-222">Return value</span></span>

<span data-ttu-id="2bb86-223">Un entero de hello valor convertido.</span><span class="sxs-lookup"><span data-stu-id="2bb86-223">An integer of hello converted value.</span></span>

### <a name="example"></a><span data-ttu-id="2bb86-224">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2bb86-224">Example</span></span>

<span data-ttu-id="2bb86-225">Hello en el ejemplo siguiente se convierte toointeger de valor de parámetro proporcionado por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-225">hello following example converts hello user-provided parameter value toointeger.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToConvert": { 
            "type": "string",
            "defaultValue": "4"
        }
    },
    "resources": [
    ],
    "outputs": {
        "intResult": {
            "type": "int",
            "value": "[int(parameters('stringToConvert'))]"
        }
    }
}
```

<span data-ttu-id="2bb86-226">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="2bb86-226">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2bb86-227">Nombre</span><span class="sxs-lookup"><span data-stu-id="2bb86-227">Name</span></span> | <span data-ttu-id="2bb86-228">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-228">Type</span></span> | <span data-ttu-id="2bb86-229">Valor</span><span class="sxs-lookup"><span data-stu-id="2bb86-229">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2bb86-230">intResult</span><span class="sxs-lookup"><span data-stu-id="2bb86-230">intResult</span></span> | <span data-ttu-id="2bb86-231">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-231">Int</span></span> | <span data-ttu-id="2bb86-232">4</span><span class="sxs-lookup"><span data-stu-id="2bb86-232">4</span></span> |


<a id="min" />

## <a name="min"></a><span data-ttu-id="2bb86-233">Min</span><span class="sxs-lookup"><span data-stu-id="2bb86-233">min</span></span>
`min (arg1)`

<span data-ttu-id="2bb86-234">Devuelve Hola valor mínimo de una matriz de enteros o una lista separada por comas de números enteros.</span><span class="sxs-lookup"><span data-stu-id="2bb86-234">Returns hello minimum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="2bb86-235">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb86-235">Parameters</span></span>

| <span data-ttu-id="2bb86-236">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2bb86-236">Parameter</span></span> | <span data-ttu-id="2bb86-237">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2bb86-237">Required</span></span> | <span data-ttu-id="2bb86-238">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-238">Type</span></span> | <span data-ttu-id="2bb86-239">Descripción</span><span class="sxs-lookup"><span data-stu-id="2bb86-239">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2bb86-240">arg1</span><span class="sxs-lookup"><span data-stu-id="2bb86-240">arg1</span></span> |<span data-ttu-id="2bb86-241">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-241">Yes</span></span> |<span data-ttu-id="2bb86-242">matriz de enteros, o lista separada por comas de enteros</span><span class="sxs-lookup"><span data-stu-id="2bb86-242">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="2bb86-243">Hola tooget Hola mínimo valor de la colección.</span><span class="sxs-lookup"><span data-stu-id="2bb86-243">hello collection tooget hello minimum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2bb86-244">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2bb86-244">Return value</span></span>

<span data-ttu-id="2bb86-245">Un entero que representa el valor mínimo de colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-245">An integer representing minimum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="2bb86-246">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2bb86-246">Example</span></span>

<span data-ttu-id="2bb86-247">Hola siguiente ejemplo se muestra cómo min toouse con una matriz y una lista de enteros:</span><span class="sxs-lookup"><span data-stu-id="2bb86-247">hello following example shows how toouse min with an array and a list of integers:</span></span>

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

<span data-ttu-id="2bb86-248">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="2bb86-248">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2bb86-249">Nombre</span><span class="sxs-lookup"><span data-stu-id="2bb86-249">Name</span></span> | <span data-ttu-id="2bb86-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-250">Type</span></span> | <span data-ttu-id="2bb86-251">Valor</span><span class="sxs-lookup"><span data-stu-id="2bb86-251">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2bb86-252">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="2bb86-252">arrayOutput</span></span> | <span data-ttu-id="2bb86-253">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-253">Int</span></span> | <span data-ttu-id="2bb86-254">0</span><span class="sxs-lookup"><span data-stu-id="2bb86-254">0</span></span> |
| <span data-ttu-id="2bb86-255">intOutput</span><span class="sxs-lookup"><span data-stu-id="2bb86-255">intOutput</span></span> | <span data-ttu-id="2bb86-256">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-256">Int</span></span> | <span data-ttu-id="2bb86-257">0</span><span class="sxs-lookup"><span data-stu-id="2bb86-257">0</span></span> |

<a id="max" />

## <a name="max"></a><span data-ttu-id="2bb86-258">max</span><span class="sxs-lookup"><span data-stu-id="2bb86-258">max</span></span>
`max (arg1)`

<span data-ttu-id="2bb86-259">Devuelve Hola valor máximo de una matriz de enteros o una lista separada por comas de números enteros.</span><span class="sxs-lookup"><span data-stu-id="2bb86-259">Returns hello maximum value from an array of integers or a comma-separated list of integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="2bb86-260">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb86-260">Parameters</span></span>

| <span data-ttu-id="2bb86-261">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2bb86-261">Parameter</span></span> | <span data-ttu-id="2bb86-262">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2bb86-262">Required</span></span> | <span data-ttu-id="2bb86-263">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-263">Type</span></span> | <span data-ttu-id="2bb86-264">Descripción</span><span class="sxs-lookup"><span data-stu-id="2bb86-264">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2bb86-265">arg1</span><span class="sxs-lookup"><span data-stu-id="2bb86-265">arg1</span></span> |<span data-ttu-id="2bb86-266">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-266">Yes</span></span> |<span data-ttu-id="2bb86-267">matriz de enteros, o lista separada por comas de enteros</span><span class="sxs-lookup"><span data-stu-id="2bb86-267">array of integers, or comma-separated list of integers</span></span> |<span data-ttu-id="2bb86-268">Hola tooget Hola máximo valor de la colección.</span><span class="sxs-lookup"><span data-stu-id="2bb86-268">hello collection tooget hello maximum value.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2bb86-269">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2bb86-269">Return value</span></span>

<span data-ttu-id="2bb86-270">Un entero que representa el valor máximo de Hola de colección de Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-270">An integer representing hello maximum value from hello collection.</span></span>

### <a name="example"></a><span data-ttu-id="2bb86-271">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2bb86-271">Example</span></span>

<span data-ttu-id="2bb86-272">Hola siguiente ejemplo se muestra cómo toouse máximo con una matriz y una lista de enteros:</span><span class="sxs-lookup"><span data-stu-id="2bb86-272">hello following example shows how toouse max with an array and a list of integers:</span></span>

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

<span data-ttu-id="2bb86-273">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="2bb86-273">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2bb86-274">Nombre</span><span class="sxs-lookup"><span data-stu-id="2bb86-274">Name</span></span> | <span data-ttu-id="2bb86-275">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-275">Type</span></span> | <span data-ttu-id="2bb86-276">Valor</span><span class="sxs-lookup"><span data-stu-id="2bb86-276">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2bb86-277">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="2bb86-277">arrayOutput</span></span> | <span data-ttu-id="2bb86-278">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-278">Int</span></span> | <span data-ttu-id="2bb86-279">5</span><span class="sxs-lookup"><span data-stu-id="2bb86-279">5</span></span> |
| <span data-ttu-id="2bb86-280">intOutput</span><span class="sxs-lookup"><span data-stu-id="2bb86-280">intOutput</span></span> | <span data-ttu-id="2bb86-281">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-281">Int</span></span> | <span data-ttu-id="2bb86-282">5</span><span class="sxs-lookup"><span data-stu-id="2bb86-282">5</span></span> |

<a id="mod" />

## <a name="mod"></a><span data-ttu-id="2bb86-283">mod</span><span class="sxs-lookup"><span data-stu-id="2bb86-283">mod</span></span>
`mod(operand1, operand2)`

<span data-ttu-id="2bb86-284">Devuelve el resto de Hola Hola división de enteros utilizando dos enteros de proporcionado Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-284">Returns hello remainder of hello integer division using hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="2bb86-285">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb86-285">Parameters</span></span>

| <span data-ttu-id="2bb86-286">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2bb86-286">Parameter</span></span> | <span data-ttu-id="2bb86-287">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2bb86-287">Required</span></span> | <span data-ttu-id="2bb86-288">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-288">Type</span></span> | <span data-ttu-id="2bb86-289">Descripción</span><span class="sxs-lookup"><span data-stu-id="2bb86-289">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2bb86-290">operand1</span><span class="sxs-lookup"><span data-stu-id="2bb86-290">operand1</span></span> |<span data-ttu-id="2bb86-291">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-291">Yes</span></span> |<span data-ttu-id="2bb86-292">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-292">int</span></span> |<span data-ttu-id="2bb86-293">número de Hola que se va a dividir.</span><span class="sxs-lookup"><span data-stu-id="2bb86-293">hello number being divided.</span></span> |
| <span data-ttu-id="2bb86-294">operand2</span><span class="sxs-lookup"><span data-stu-id="2bb86-294">operand2</span></span> |<span data-ttu-id="2bb86-295">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-295">Yes</span></span> |<span data-ttu-id="2bb86-296">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-296">int</span></span> |<span data-ttu-id="2bb86-297">número de Hello toodivide utilizado, no puede ser 0.</span><span class="sxs-lookup"><span data-stu-id="2bb86-297">hello number that is used toodivide, Cannot be 0.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2bb86-298">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2bb86-298">Return value</span></span>
<span data-ttu-id="2bb86-299">Un resto de Hola que representan entero.</span><span class="sxs-lookup"><span data-stu-id="2bb86-299">An integer representing hello remainder.</span></span>

### <a name="example"></a><span data-ttu-id="2bb86-300">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2bb86-300">Example</span></span>

<span data-ttu-id="2bb86-301">Hello en el ejemplo siguiente se devuelve Hola resto de dividir un parámetro por otro parámetro.</span><span class="sxs-lookup"><span data-stu-id="2bb86-301">hello following example returns hello remainder of dividing one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer being divided"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer used toodivide"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "modResult": {
            "type": "int",
            "value": "[mod(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="2bb86-302">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="2bb86-302">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2bb86-303">Nombre</span><span class="sxs-lookup"><span data-stu-id="2bb86-303">Name</span></span> | <span data-ttu-id="2bb86-304">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-304">Type</span></span> | <span data-ttu-id="2bb86-305">Valor</span><span class="sxs-lookup"><span data-stu-id="2bb86-305">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2bb86-306">modResult</span><span class="sxs-lookup"><span data-stu-id="2bb86-306">modResult</span></span> | <span data-ttu-id="2bb86-307">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-307">Int</span></span> | <span data-ttu-id="2bb86-308">1</span><span class="sxs-lookup"><span data-stu-id="2bb86-308">1</span></span> |

<a id="mul" />

## <a name="mul"></a><span data-ttu-id="2bb86-309">mul</span><span class="sxs-lookup"><span data-stu-id="2bb86-309">mul</span></span>
`mul(operand1, operand2)`

<span data-ttu-id="2bb86-310">Devuelve Hola multiplicación de dos enteros de proporcionado Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-310">Returns hello multiplication of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="2bb86-311">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb86-311">Parameters</span></span>

| <span data-ttu-id="2bb86-312">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2bb86-312">Parameter</span></span> | <span data-ttu-id="2bb86-313">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2bb86-313">Required</span></span> | <span data-ttu-id="2bb86-314">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-314">Type</span></span> | <span data-ttu-id="2bb86-315">Descripción</span><span class="sxs-lookup"><span data-stu-id="2bb86-315">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2bb86-316">operand1</span><span class="sxs-lookup"><span data-stu-id="2bb86-316">operand1</span></span> |<span data-ttu-id="2bb86-317">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-317">Yes</span></span> |<span data-ttu-id="2bb86-318">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-318">int</span></span> |<span data-ttu-id="2bb86-319">Primero debe numerar toomultiply.</span><span class="sxs-lookup"><span data-stu-id="2bb86-319">First number toomultiply.</span></span> |
| <span data-ttu-id="2bb86-320">operand2</span><span class="sxs-lookup"><span data-stu-id="2bb86-320">operand2</span></span> |<span data-ttu-id="2bb86-321">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-321">Yes</span></span> |<span data-ttu-id="2bb86-322">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-322">int</span></span> |<span data-ttu-id="2bb86-323">Segundo número toomultiply.</span><span class="sxs-lookup"><span data-stu-id="2bb86-323">Second number toomultiply.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2bb86-324">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2bb86-324">Return value</span></span>

<span data-ttu-id="2bb86-325">Una entero que representa Hola la multiplicación.</span><span class="sxs-lookup"><span data-stu-id="2bb86-325">An integer representing hello multiplication.</span></span>

### <a name="example"></a><span data-ttu-id="2bb86-326">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2bb86-326">Example</span></span>

<span data-ttu-id="2bb86-327">Hola de ejemplo siguiente multiplica un parámetro por otro parámetro.</span><span class="sxs-lookup"><span data-stu-id="2bb86-327">hello following example multiplies one parameter by another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 5,
            "metadata": {
                "description": "First integer toomultiply"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Second integer toomultiply"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "mulResult": {
            "type": "int",
            "value": "[mul(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="2bb86-328">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="2bb86-328">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2bb86-329">Nombre</span><span class="sxs-lookup"><span data-stu-id="2bb86-329">Name</span></span> | <span data-ttu-id="2bb86-330">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-330">Type</span></span> | <span data-ttu-id="2bb86-331">Valor</span><span class="sxs-lookup"><span data-stu-id="2bb86-331">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2bb86-332">mulResult</span><span class="sxs-lookup"><span data-stu-id="2bb86-332">mulResult</span></span> | <span data-ttu-id="2bb86-333">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-333">Int</span></span> | <span data-ttu-id="2bb86-334">15</span><span class="sxs-lookup"><span data-stu-id="2bb86-334">15</span></span> |

<a id="sub" />

## <a name="sub"></a><span data-ttu-id="2bb86-335">sub</span><span class="sxs-lookup"><span data-stu-id="2bb86-335">sub</span></span>
`sub(operand1, operand2)`

<span data-ttu-id="2bb86-336">Devuelve Hola resta de dos enteros de proporcionado Hola.</span><span class="sxs-lookup"><span data-stu-id="2bb86-336">Returns hello subtraction of hello two provided integers.</span></span>

### <a name="parameters"></a><span data-ttu-id="2bb86-337">parameters</span><span class="sxs-lookup"><span data-stu-id="2bb86-337">Parameters</span></span>

| <span data-ttu-id="2bb86-338">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2bb86-338">Parameter</span></span> | <span data-ttu-id="2bb86-339">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2bb86-339">Required</span></span> | <span data-ttu-id="2bb86-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-340">Type</span></span> | <span data-ttu-id="2bb86-341">Descripción</span><span class="sxs-lookup"><span data-stu-id="2bb86-341">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2bb86-342">operand1</span><span class="sxs-lookup"><span data-stu-id="2bb86-342">operand1</span></span> |<span data-ttu-id="2bb86-343">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-343">Yes</span></span> |<span data-ttu-id="2bb86-344">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-344">int</span></span> |<span data-ttu-id="2bb86-345">número de Hola que se resta.</span><span class="sxs-lookup"><span data-stu-id="2bb86-345">hello number that is subtracted from.</span></span> |
| <span data-ttu-id="2bb86-346">operand2</span><span class="sxs-lookup"><span data-stu-id="2bb86-346">operand2</span></span> |<span data-ttu-id="2bb86-347">Sí</span><span class="sxs-lookup"><span data-stu-id="2bb86-347">Yes</span></span> |<span data-ttu-id="2bb86-348">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-348">int</span></span> |<span data-ttu-id="2bb86-349">número de Hola que se va a restar.</span><span class="sxs-lookup"><span data-stu-id="2bb86-349">hello number that is subtracted.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2bb86-350">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2bb86-350">Return value</span></span>
<span data-ttu-id="2bb86-351">Una resta Hola de enteros que representan.</span><span class="sxs-lookup"><span data-stu-id="2bb86-351">An integer representing hello subtraction.</span></span>

### <a name="example"></a><span data-ttu-id="2bb86-352">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2bb86-352">Example</span></span>

<span data-ttu-id="2bb86-353">Hola siguiente ejemplo resta un parámetro de otro parámetro.</span><span class="sxs-lookup"><span data-stu-id="2bb86-353">hello following example subtracts one parameter from another parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "first": {
            "type": "int",
            "defaultValue": 7,
            "metadata": {
                "description": "Integer subtracted from"
            }
        },
        "second": {
            "type": "int",
            "defaultValue": 3,
            "metadata": {
                "description": "Integer toosubtract"
            }
        }
    },
    "resources": [
    ],
    "outputs": {
        "subResult": {
            "type": "int",
            "value": "[sub(parameters('first'), parameters('second'))]"
        }
    }
}
```

<span data-ttu-id="2bb86-354">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="2bb86-354">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="2bb86-355">Nombre</span><span class="sxs-lookup"><span data-stu-id="2bb86-355">Name</span></span> | <span data-ttu-id="2bb86-356">Tipo</span><span class="sxs-lookup"><span data-stu-id="2bb86-356">Type</span></span> | <span data-ttu-id="2bb86-357">Valor</span><span class="sxs-lookup"><span data-stu-id="2bb86-357">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2bb86-358">subResult</span><span class="sxs-lookup"><span data-stu-id="2bb86-358">subResult</span></span> | <span data-ttu-id="2bb86-359">int</span><span class="sxs-lookup"><span data-stu-id="2bb86-359">Int</span></span> | <span data-ttu-id="2bb86-360">4</span><span class="sxs-lookup"><span data-stu-id="2bb86-360">4</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2bb86-361">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2bb86-361">Next steps</span></span>
* <span data-ttu-id="2bb86-362">Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2bb86-362">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="2bb86-363">toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2bb86-363">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="2bb86-364">tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2bb86-364">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="2bb86-365">toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2bb86-365">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

