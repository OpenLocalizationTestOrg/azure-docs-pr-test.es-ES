---
title: 'Funciones de la plantilla de Azure Resource Manager: cadena | Microsoft Docs'
description: Describe las funciones para usar en una plantilla de Azure Resource Manager para trabajar con cadenas.
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
ms.openlocfilehash: 3e5c9ca546629f782a3d722b49f5fbaf5147e823
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="2f166-103">Funciones de cadena para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2f166-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="2f166-104">El Administrador de recursos ofrece las siguientes funciones para trabajar con cadenas:</span><span class="sxs-lookup"><span data-stu-id="2f166-104">Resource Manager provides the following functions for working with strings:</span></span>

* [<span data-ttu-id="2f166-105">base64</span><span class="sxs-lookup"><span data-stu-id="2f166-105">base64</span></span>](#base64)
* [<span data-ttu-id="2f166-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="2f166-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="2f166-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="2f166-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="2f166-108">concat</span><span class="sxs-lookup"><span data-stu-id="2f166-108">concat</span></span>](#concat)
* [<span data-ttu-id="2f166-109">contains</span><span class="sxs-lookup"><span data-stu-id="2f166-109">contains</span></span>](#contains)
* [<span data-ttu-id="2f166-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="2f166-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="2f166-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="2f166-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="2f166-112">empty</span><span class="sxs-lookup"><span data-stu-id="2f166-112">empty</span></span>](#empty)
* [<span data-ttu-id="2f166-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="2f166-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="2f166-114">first</span><span class="sxs-lookup"><span data-stu-id="2f166-114">first</span></span>](#first)
* [<span data-ttu-id="2f166-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="2f166-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="2f166-116">last</span><span class="sxs-lookup"><span data-stu-id="2f166-116">last</span></span>](#last)
* [<span data-ttu-id="2f166-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="2f166-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="2f166-118">length</span><span class="sxs-lookup"><span data-stu-id="2f166-118">length</span></span>](#length)
* [<span data-ttu-id="2f166-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="2f166-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="2f166-120">replace</span><span class="sxs-lookup"><span data-stu-id="2f166-120">replace</span></span>](#replace)
* [<span data-ttu-id="2f166-121">skip</span><span class="sxs-lookup"><span data-stu-id="2f166-121">skip</span></span>](#skip)
* [<span data-ttu-id="2f166-122">split</span><span class="sxs-lookup"><span data-stu-id="2f166-122">split</span></span>](#split)
* [<span data-ttu-id="2f166-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="2f166-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="2f166-124">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-124">string</span></span>](#string)
* [<span data-ttu-id="2f166-125">substring</span><span class="sxs-lookup"><span data-stu-id="2f166-125">substring</span></span>](#substring)
* [<span data-ttu-id="2f166-126">take</span><span class="sxs-lookup"><span data-stu-id="2f166-126">take</span></span>](#take)
* [<span data-ttu-id="2f166-127">toLower</span><span class="sxs-lookup"><span data-stu-id="2f166-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="2f166-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="2f166-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="2f166-129">trim</span><span class="sxs-lookup"><span data-stu-id="2f166-129">trim</span></span>](#trim)
* [<span data-ttu-id="2f166-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="2f166-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="2f166-131">uri</span><span class="sxs-lookup"><span data-stu-id="2f166-131">uri</span></span>](#uri)
* [<span data-ttu-id="2f166-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="2f166-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="2f166-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="2f166-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="2f166-134">base64</span><span class="sxs-lookup"><span data-stu-id="2f166-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="2f166-135">Devuelve la representación de base64 de la cadena de entrada.</span><span class="sxs-lookup"><span data-stu-id="2f166-135">Returns the base64 representation of the input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-136">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-136">Parameters</span></span>

| <span data-ttu-id="2f166-137">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-137">Parameter</span></span> | <span data-ttu-id="2f166-138">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-138">Required</span></span> | <span data-ttu-id="2f166-139">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-139">Type</span></span> | <span data-ttu-id="2f166-140">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-141">inputString</span><span class="sxs-lookup"><span data-stu-id="2f166-141">inputString</span></span> |<span data-ttu-id="2f166-142">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-142">Yes</span></span> |<span data-ttu-id="2f166-143">string</span><span class="sxs-lookup"><span data-stu-id="2f166-143">string</span></span> |<span data-ttu-id="2f166-144">Valor que se va a devolver como una representación de base64.</span><span class="sxs-lookup"><span data-stu-id="2f166-144">The value to return as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-145">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-145">Return value</span></span>

<span data-ttu-id="2f166-146">Una cadena que contiene la representación en base64.</span><span class="sxs-lookup"><span data-stu-id="2f166-146">A string containing the base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-147">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-147">Examples</span></span>

<span data-ttu-id="2f166-148">En el ejemplo siguiente se muestra cómo utilizar la función de base64.</span><span class="sxs-lookup"><span data-stu-id="2f166-148">The following example shows how to use the base64 function.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="2f166-149">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-149">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-150">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-150">Name</span></span> | <span data-ttu-id="2f166-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-151">Type</span></span> | <span data-ttu-id="2f166-152">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="2f166-153">base64Output</span></span> | <span data-ttu-id="2f166-154">String</span><span class="sxs-lookup"><span data-stu-id="2f166-154">String</span></span> | <span data-ttu-id="2f166-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="2f166-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="2f166-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-156">toStringOutput</span></span> | <span data-ttu-id="2f166-157">String</span><span class="sxs-lookup"><span data-stu-id="2f166-157">String</span></span> | <span data-ttu-id="2f166-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="2f166-158">one, two, three</span></span> |
| <span data-ttu-id="2f166-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-159">toJsonOutput</span></span> | <span data-ttu-id="2f166-160">Objeto</span><span class="sxs-lookup"><span data-stu-id="2f166-160">Object</span></span> | <span data-ttu-id="2f166-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="2f166-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="2f166-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="2f166-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="2f166-163">Convierte una representación en base64 a un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="2f166-163">Converts a base64 representation to a JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-164">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-164">Parameters</span></span>

| <span data-ttu-id="2f166-165">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-165">Parameter</span></span> | <span data-ttu-id="2f166-166">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-166">Required</span></span> | <span data-ttu-id="2f166-167">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-167">Type</span></span> | <span data-ttu-id="2f166-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="2f166-169">base64Value</span></span> |<span data-ttu-id="2f166-170">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-170">Yes</span></span> |<span data-ttu-id="2f166-171">string</span><span class="sxs-lookup"><span data-stu-id="2f166-171">string</span></span> |<span data-ttu-id="2f166-172">La representación en base64 para convertir en un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="2f166-172">The base64 representation to convert to a JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-173">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-173">Return value</span></span>

<span data-ttu-id="2f166-174">Un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="2f166-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-175">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-175">Examples</span></span>

<span data-ttu-id="2f166-176">En el ejemplo siguiente se utiliza la función base64ToJson para convertir un valor base64:</span><span class="sxs-lookup"><span data-stu-id="2f166-176">The following example uses the base64ToJson function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="2f166-177">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-177">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-178">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-178">Name</span></span> | <span data-ttu-id="2f166-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-179">Type</span></span> | <span data-ttu-id="2f166-180">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="2f166-181">base64Output</span></span> | <span data-ttu-id="2f166-182">String</span><span class="sxs-lookup"><span data-stu-id="2f166-182">String</span></span> | <span data-ttu-id="2f166-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="2f166-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="2f166-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-184">toStringOutput</span></span> | <span data-ttu-id="2f166-185">String</span><span class="sxs-lookup"><span data-stu-id="2f166-185">String</span></span> | <span data-ttu-id="2f166-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="2f166-186">one, two, three</span></span> |
| <span data-ttu-id="2f166-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-187">toJsonOutput</span></span> | <span data-ttu-id="2f166-188">Objeto</span><span class="sxs-lookup"><span data-stu-id="2f166-188">Object</span></span> | <span data-ttu-id="2f166-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="2f166-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="2f166-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="2f166-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="2f166-191">Convierte una representación en base64 en una cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-191">Converts a base64 representation to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-192">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-192">Parameters</span></span>

| <span data-ttu-id="2f166-193">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-193">Parameter</span></span> | <span data-ttu-id="2f166-194">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-194">Required</span></span> | <span data-ttu-id="2f166-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-195">Type</span></span> | <span data-ttu-id="2f166-196">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="2f166-197">base64Value</span></span> |<span data-ttu-id="2f166-198">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-198">Yes</span></span> |<span data-ttu-id="2f166-199">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-199">string</span></span> |<span data-ttu-id="2f166-200">La representación en base64 para convertir en una cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-200">The base64 representation to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-201">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-201">Return value</span></span>

<span data-ttu-id="2f166-202">Una cadena del valor convertido de base64.</span><span class="sxs-lookup"><span data-stu-id="2f166-202">A string of the converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-203">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-203">Examples</span></span>

<span data-ttu-id="2f166-204">En el ejemplo siguiente se utiliza la función base64ToString para convertir un valor base64:</span><span class="sxs-lookup"><span data-stu-id="2f166-204">The following example uses the base64ToString function to convert a base64 value:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringData": {
            "type": "string",
            "defaultValue": "one, two, three"
        },
        "jsonFormattedData": {
            "type": "string",
            "defaultValue": "{'one': 'a', 'two': 'b'}"
        }
    },
    "variables": {
        "base64String": "[base64(parameters('stringData'))]",
        "base64Object": "[base64(parameters('jsonFormattedData'))]"
    },
    "resources": [
    ],
    "outputs": {
        "base64Output": {
            "type": "string",
            "value": "[variables('base64String')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[base64ToString(variables('base64String'))]"
        },
        "toJsonOutput": {
            "type": "object",
            "value": "[base64ToJson(variables('base64Object'))]"
        }
    }
}
```

<span data-ttu-id="2f166-205">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-205">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-206">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-206">Name</span></span> | <span data-ttu-id="2f166-207">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-207">Type</span></span> | <span data-ttu-id="2f166-208">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="2f166-209">base64Output</span></span> | <span data-ttu-id="2f166-210">String</span><span class="sxs-lookup"><span data-stu-id="2f166-210">String</span></span> | <span data-ttu-id="2f166-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="2f166-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="2f166-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-212">toStringOutput</span></span> | <span data-ttu-id="2f166-213">String</span><span class="sxs-lookup"><span data-stu-id="2f166-213">String</span></span> | <span data-ttu-id="2f166-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="2f166-214">one, two, three</span></span> |
| <span data-ttu-id="2f166-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-215">toJsonOutput</span></span> | <span data-ttu-id="2f166-216">Objeto</span><span class="sxs-lookup"><span data-stu-id="2f166-216">Object</span></span> | <span data-ttu-id="2f166-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="2f166-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="2f166-218">concat</span><span class="sxs-lookup"><span data-stu-id="2f166-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="2f166-219">Combina varios valores de cadena y devuelve la cadena concatenada, o combina varias matrices y devuelve la matriz concatenada.</span><span class="sxs-lookup"><span data-stu-id="2f166-219">Combines multiple string values and returns the concatenated string, or combines multiple arrays and returns the concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-220">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-220">Parameters</span></span>

| <span data-ttu-id="2f166-221">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-221">Parameter</span></span> | <span data-ttu-id="2f166-222">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-222">Required</span></span> | <span data-ttu-id="2f166-223">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-223">Type</span></span> | <span data-ttu-id="2f166-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-225">arg1</span><span class="sxs-lookup"><span data-stu-id="2f166-225">arg1</span></span> |<span data-ttu-id="2f166-226">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-226">Yes</span></span> |<span data-ttu-id="2f166-227">cadena o matriz</span><span class="sxs-lookup"><span data-stu-id="2f166-227">string or array</span></span> |<span data-ttu-id="2f166-228">El primer valor para la concatenación.</span><span class="sxs-lookup"><span data-stu-id="2f166-228">The first value for concatenation.</span></span> |
| <span data-ttu-id="2f166-229">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="2f166-229">additional arguments</span></span> |<span data-ttu-id="2f166-230">No</span><span class="sxs-lookup"><span data-stu-id="2f166-230">No</span></span> |<span data-ttu-id="2f166-231">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-231">string</span></span> |<span data-ttu-id="2f166-232">Valores adicionales en orden secuencial para la concatenación.</span><span class="sxs-lookup"><span data-stu-id="2f166-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-233">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-233">Return value</span></span>
<span data-ttu-id="2f166-234">Una cadena o matriz de valores concatenados.</span><span class="sxs-lookup"><span data-stu-id="2f166-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-235">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-235">Examples</span></span>

<span data-ttu-id="2f166-236">En el ejemplo siguiente se muestra cómo combinar dos valores de cadena y devolver una cadena concatenada.</span><span class="sxs-lookup"><span data-stu-id="2f166-236">The following example shows how to combine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="2f166-237">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-237">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-238">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-238">Name</span></span> | <span data-ttu-id="2f166-239">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-239">Type</span></span> | <span data-ttu-id="2f166-240">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-241">concatOutput</span></span> | <span data-ttu-id="2f166-242">String</span><span class="sxs-lookup"><span data-stu-id="2f166-242">String</span></span> | <span data-ttu-id="2f166-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="2f166-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="2f166-244">En el ejemplo siguiente se muestra cómo combinar dos matrices.</span><span class="sxs-lookup"><span data-stu-id="2f166-244">The following example shows how to combine two arrays.</span></span>

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

<span data-ttu-id="2f166-245">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-245">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-246">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-246">Name</span></span> | <span data-ttu-id="2f166-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-247">Type</span></span> | <span data-ttu-id="2f166-248">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-249">return</span><span class="sxs-lookup"><span data-stu-id="2f166-249">return</span></span> | <span data-ttu-id="2f166-250">Matriz</span><span class="sxs-lookup"><span data-stu-id="2f166-250">Array</span></span> | <span data-ttu-id="2f166-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="2f166-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="2f166-252">contains</span><span class="sxs-lookup"><span data-stu-id="2f166-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="2f166-253">Comprueba si una matriz contiene un valor, un objeto contiene una clave o una cadena contiene una subcadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-254">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-254">Parameters</span></span>

| <span data-ttu-id="2f166-255">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-255">Parameter</span></span> | <span data-ttu-id="2f166-256">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-256">Required</span></span> | <span data-ttu-id="2f166-257">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-257">Type</span></span> | <span data-ttu-id="2f166-258">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-259">container</span><span class="sxs-lookup"><span data-stu-id="2f166-259">container</span></span> |<span data-ttu-id="2f166-260">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-260">Yes</span></span> |<span data-ttu-id="2f166-261">matriz, objeto o cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-261">array, object, or string</span></span> |<span data-ttu-id="2f166-262">El valor que contiene el valor para buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-262">The value that contains the value to find.</span></span> |
| <span data-ttu-id="2f166-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="2f166-263">itemToFind</span></span> |<span data-ttu-id="2f166-264">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-264">Yes</span></span> |<span data-ttu-id="2f166-265">cadena o entero</span><span class="sxs-lookup"><span data-stu-id="2f166-265">string or int</span></span> |<span data-ttu-id="2f166-266">El valor para buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-266">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-267">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-267">Return value</span></span>

<span data-ttu-id="2f166-268">**True** si el elemento se encuentra; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="2f166-268">**True** if the item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-269">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-269">Examples</span></span>

<span data-ttu-id="2f166-270">En el ejemplo siguiente se muestra cómo utilizar contains con diferentes tipos:</span><span class="sxs-lookup"><span data-stu-id="2f166-270">The following example shows how to use contains with different types:</span></span>

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

<span data-ttu-id="2f166-271">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-271">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-272">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-272">Name</span></span> | <span data-ttu-id="2f166-273">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-273">Type</span></span> | <span data-ttu-id="2f166-274">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-275">stringTrue</span></span> | <span data-ttu-id="2f166-276">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-276">Bool</span></span> | <span data-ttu-id="2f166-277">True</span><span class="sxs-lookup"><span data-stu-id="2f166-277">True</span></span> |
| <span data-ttu-id="2f166-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="2f166-278">stringFalse</span></span> | <span data-ttu-id="2f166-279">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-279">Bool</span></span> | <span data-ttu-id="2f166-280">False</span><span class="sxs-lookup"><span data-stu-id="2f166-280">False</span></span> |
| <span data-ttu-id="2f166-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-281">objectTrue</span></span> | <span data-ttu-id="2f166-282">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-282">Bool</span></span> | <span data-ttu-id="2f166-283">True</span><span class="sxs-lookup"><span data-stu-id="2f166-283">True</span></span> |
| <span data-ttu-id="2f166-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="2f166-284">objectFalse</span></span> | <span data-ttu-id="2f166-285">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-285">Bool</span></span> | <span data-ttu-id="2f166-286">False</span><span class="sxs-lookup"><span data-stu-id="2f166-286">False</span></span> |
| <span data-ttu-id="2f166-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-287">arrayTrue</span></span> | <span data-ttu-id="2f166-288">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-288">Bool</span></span> | <span data-ttu-id="2f166-289">True</span><span class="sxs-lookup"><span data-stu-id="2f166-289">True</span></span> |
| <span data-ttu-id="2f166-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="2f166-290">arrayFalse</span></span> | <span data-ttu-id="2f166-291">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-291">Bool</span></span> | <span data-ttu-id="2f166-292">False</span><span class="sxs-lookup"><span data-stu-id="2f166-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="2f166-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="2f166-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="2f166-294">Convierte un valor en un identificador URI de datos.</span><span class="sxs-lookup"><span data-stu-id="2f166-294">Converts a value to a data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-295">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-295">Parameters</span></span>

| <span data-ttu-id="2f166-296">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-296">Parameter</span></span> | <span data-ttu-id="2f166-297">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-297">Required</span></span> | <span data-ttu-id="2f166-298">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-298">Type</span></span> | <span data-ttu-id="2f166-299">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="2f166-300">stringToConvert</span></span> |<span data-ttu-id="2f166-301">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-301">Yes</span></span> |<span data-ttu-id="2f166-302">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-302">string</span></span> |<span data-ttu-id="2f166-303">El valor para convertir en un identificador URI de datos.</span><span class="sxs-lookup"><span data-stu-id="2f166-303">The value to convert to a data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-304">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-304">Return value</span></span>

<span data-ttu-id="2f166-305">Una cadena con formato de identificador URI de datos.</span><span class="sxs-lookup"><span data-stu-id="2f166-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-306">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-306">Examples</span></span>

<span data-ttu-id="2f166-307">En el ejemplo siguiente se convierte un valor en un identificador URI de datos, y se convierte un identificador URI de datos en una cadena:</span><span class="sxs-lookup"><span data-stu-id="2f166-307">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="2f166-308">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-308">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-309">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-309">Name</span></span> | <span data-ttu-id="2f166-310">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-310">Type</span></span> | <span data-ttu-id="2f166-311">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-312">dataUriOutput</span></span> | <span data-ttu-id="2f166-313">String</span><span class="sxs-lookup"><span data-stu-id="2f166-313">String</span></span> | <span data-ttu-id="2f166-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="2f166-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="2f166-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-315">toStringOutput</span></span> | <span data-ttu-id="2f166-316">String</span><span class="sxs-lookup"><span data-stu-id="2f166-316">String</span></span> | <span data-ttu-id="2f166-317">Hola mundo.</span><span class="sxs-lookup"><span data-stu-id="2f166-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="2f166-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="2f166-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="2f166-319">Convierte un valor con formato de identificador URI de datos en una cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-319">Converts a data URI formatted value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-320">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-320">Parameters</span></span>

| <span data-ttu-id="2f166-321">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-321">Parameter</span></span> | <span data-ttu-id="2f166-322">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-322">Required</span></span> | <span data-ttu-id="2f166-323">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-323">Type</span></span> | <span data-ttu-id="2f166-324">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="2f166-325">dataUriToConvert</span></span> |<span data-ttu-id="2f166-326">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-326">Yes</span></span> |<span data-ttu-id="2f166-327">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-327">string</span></span> |<span data-ttu-id="2f166-328">El valor del identificador URI para convertir.</span><span class="sxs-lookup"><span data-stu-id="2f166-328">The data URI value to convert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-329">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-329">Return value</span></span>

<span data-ttu-id="2f166-330">Una cadena que contiene el valor convertido.</span><span class="sxs-lookup"><span data-stu-id="2f166-330">A string containing the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-331">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-331">Examples</span></span>

<span data-ttu-id="2f166-332">En el ejemplo siguiente se convierte un valor en un identificador URI de datos, y se convierte un identificador URI de datos en una cadena:</span><span class="sxs-lookup"><span data-stu-id="2f166-332">The following example converts a value to a data URI, and converts a data URI to a string:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringToTest": {
            "type": "string",
            "defaultValue": "Hello"
        },
        "dataFormattedString": {
            "type": "string",
            "defaultValue": "data:;base64,SGVsbG8sIFdvcmxkIQ=="
        }
    },
    "resources": [],
    "outputs": {
        "dataUriOutput": {
            "value": "[dataUri(parameters('stringToTest'))]",
            "type" : "string"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[dataUriToString(parameters('dataFormattedString'))]"
        }
    }
}
```

<span data-ttu-id="2f166-333">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-333">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-334">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-334">Name</span></span> | <span data-ttu-id="2f166-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-335">Type</span></span> | <span data-ttu-id="2f166-336">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-337">dataUriOutput</span></span> | <span data-ttu-id="2f166-338">String</span><span class="sxs-lookup"><span data-stu-id="2f166-338">String</span></span> | <span data-ttu-id="2f166-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="2f166-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="2f166-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-340">toStringOutput</span></span> | <span data-ttu-id="2f166-341">String</span><span class="sxs-lookup"><span data-stu-id="2f166-341">String</span></span> | <span data-ttu-id="2f166-342">Hola mundo.</span><span class="sxs-lookup"><span data-stu-id="2f166-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="2f166-343">empty</span><span class="sxs-lookup"><span data-stu-id="2f166-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="2f166-344">Determina si una matriz, un objeto o una cadena están vacíos.</span><span class="sxs-lookup"><span data-stu-id="2f166-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-345">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-345">Parameters</span></span>

| <span data-ttu-id="2f166-346">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-346">Parameter</span></span> | <span data-ttu-id="2f166-347">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-347">Required</span></span> | <span data-ttu-id="2f166-348">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-348">Type</span></span> | <span data-ttu-id="2f166-349">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="2f166-350">itemToTest</span></span> |<span data-ttu-id="2f166-351">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-351">Yes</span></span> |<span data-ttu-id="2f166-352">matriz, objeto o cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-352">array, object, or string</span></span> |<span data-ttu-id="2f166-353">El valor para comprobar si está vacío.</span><span class="sxs-lookup"><span data-stu-id="2f166-353">The value to check if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-354">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-354">Return value</span></span>

<span data-ttu-id="2f166-355">Devuelve **True** si el valor está vacío; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="2f166-355">Returns **True** if the value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-356">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-356">Examples</span></span>

<span data-ttu-id="2f166-357">En el ejemplo siguiente se comprueba si una matriz, un objeto y una cadena están vacíos.</span><span class="sxs-lookup"><span data-stu-id="2f166-357">The following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="2f166-358">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-358">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-359">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-359">Name</span></span> | <span data-ttu-id="2f166-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-360">Type</span></span> | <span data-ttu-id="2f166-361">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="2f166-362">arrayEmpty</span></span> | <span data-ttu-id="2f166-363">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-363">Bool</span></span> | <span data-ttu-id="2f166-364">True</span><span class="sxs-lookup"><span data-stu-id="2f166-364">True</span></span> |
| <span data-ttu-id="2f166-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="2f166-365">objectEmpty</span></span> | <span data-ttu-id="2f166-366">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-366">Bool</span></span> | <span data-ttu-id="2f166-367">True</span><span class="sxs-lookup"><span data-stu-id="2f166-367">True</span></span> |
| <span data-ttu-id="2f166-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="2f166-368">stringEmpty</span></span> | <span data-ttu-id="2f166-369">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-369">Bool</span></span> | <span data-ttu-id="2f166-370">True</span><span class="sxs-lookup"><span data-stu-id="2f166-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="2f166-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="2f166-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="2f166-372">Determina si una cadena termina con un valor.</span><span class="sxs-lookup"><span data-stu-id="2f166-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="2f166-373">La comparación distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-373">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-374">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-374">Parameters</span></span>

| <span data-ttu-id="2f166-375">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-375">Parameter</span></span> | <span data-ttu-id="2f166-376">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-376">Required</span></span> | <span data-ttu-id="2f166-377">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-377">Type</span></span> | <span data-ttu-id="2f166-378">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="2f166-379">stringToSearch</span></span> |<span data-ttu-id="2f166-380">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-380">Yes</span></span> |<span data-ttu-id="2f166-381">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-381">string</span></span> |<span data-ttu-id="2f166-382">El valor que contiene el elemento para buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-382">The value that contains the item to find.</span></span> |
| <span data-ttu-id="2f166-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="2f166-383">stringToFind</span></span> |<span data-ttu-id="2f166-384">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-384">Yes</span></span> |<span data-ttu-id="2f166-385">string</span><span class="sxs-lookup"><span data-stu-id="2f166-385">string</span></span> |<span data-ttu-id="2f166-386">El valor para buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-386">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-387">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-387">Return value</span></span>

<span data-ttu-id="2f166-388">**True** si el último carácter o caracteres de la cadena coinciden con el valor; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="2f166-388">**True** if the last character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-389">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-389">Examples</span></span>

<span data-ttu-id="2f166-390">En el ejemplo siguiente se muestra cómo utilizar las funciones startsWith y endsWith:</span><span class="sxs-lookup"><span data-stu-id="2f166-390">The following example shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="2f166-391">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-391">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-392">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-392">Name</span></span> | <span data-ttu-id="2f166-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-393">Type</span></span> | <span data-ttu-id="2f166-394">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-395">startsTrue</span></span> | <span data-ttu-id="2f166-396">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-396">Bool</span></span> | <span data-ttu-id="2f166-397">True</span><span class="sxs-lookup"><span data-stu-id="2f166-397">True</span></span> |
| <span data-ttu-id="2f166-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-398">startsCapTrue</span></span> | <span data-ttu-id="2f166-399">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-399">Bool</span></span> | <span data-ttu-id="2f166-400">True</span><span class="sxs-lookup"><span data-stu-id="2f166-400">True</span></span> |
| <span data-ttu-id="2f166-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="2f166-401">startsFalse</span></span> | <span data-ttu-id="2f166-402">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-402">Bool</span></span> | <span data-ttu-id="2f166-403">False</span><span class="sxs-lookup"><span data-stu-id="2f166-403">False</span></span> |
| <span data-ttu-id="2f166-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-404">endsTrue</span></span> | <span data-ttu-id="2f166-405">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-405">Bool</span></span> | <span data-ttu-id="2f166-406">True</span><span class="sxs-lookup"><span data-stu-id="2f166-406">True</span></span> |
| <span data-ttu-id="2f166-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-407">endsCapTrue</span></span> | <span data-ttu-id="2f166-408">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-408">Bool</span></span> | <span data-ttu-id="2f166-409">True</span><span class="sxs-lookup"><span data-stu-id="2f166-409">True</span></span> |
| <span data-ttu-id="2f166-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="2f166-410">endsFalse</span></span> | <span data-ttu-id="2f166-411">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-411">Bool</span></span> | <span data-ttu-id="2f166-412">False</span><span class="sxs-lookup"><span data-stu-id="2f166-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="2f166-413">first</span><span class="sxs-lookup"><span data-stu-id="2f166-413">first</span></span>
`first(arg1)`

<span data-ttu-id="2f166-414">Devuelve el primer carácter de la cadena o el primer elemento de la matriz.</span><span class="sxs-lookup"><span data-stu-id="2f166-414">Returns the first character of the string, or first element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-415">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-415">Parameters</span></span>

| <span data-ttu-id="2f166-416">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-416">Parameter</span></span> | <span data-ttu-id="2f166-417">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-417">Required</span></span> | <span data-ttu-id="2f166-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-418">Type</span></span> | <span data-ttu-id="2f166-419">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-420">arg1</span><span class="sxs-lookup"><span data-stu-id="2f166-420">arg1</span></span> |<span data-ttu-id="2f166-421">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-421">Yes</span></span> |<span data-ttu-id="2f166-422">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-422">array or string</span></span> |<span data-ttu-id="2f166-423">El valor para recuperar el primer elemento o carácter.</span><span class="sxs-lookup"><span data-stu-id="2f166-423">The value to retrieve the first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-424">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-424">Return value</span></span>

<span data-ttu-id="2f166-425">Una cadena del primer carácter, o el tipo (cadena, entero, matriz u objeto) del primer elemento en una matriz.</span><span class="sxs-lookup"><span data-stu-id="2f166-425">A string of the first character, or the type (string, int, array, or object) of the first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-426">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-426">Examples</span></span>

<span data-ttu-id="2f166-427">En el ejemplo siguiente se muestra cómo utilizar la primera función con una matriz y una cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-427">The following example shows how to use the first function with an array and string.</span></span>

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

<span data-ttu-id="2f166-428">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-428">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-429">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-429">Name</span></span> | <span data-ttu-id="2f166-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-430">Type</span></span> | <span data-ttu-id="2f166-431">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-432">arrayOutput</span></span> | <span data-ttu-id="2f166-433">String</span><span class="sxs-lookup"><span data-stu-id="2f166-433">String</span></span> | <span data-ttu-id="2f166-434">one</span><span class="sxs-lookup"><span data-stu-id="2f166-434">one</span></span> |
| <span data-ttu-id="2f166-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-435">stringOutput</span></span> | <span data-ttu-id="2f166-436">String</span><span class="sxs-lookup"><span data-stu-id="2f166-436">String</span></span> | <span data-ttu-id="2f166-437">O</span><span class="sxs-lookup"><span data-stu-id="2f166-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="2f166-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="2f166-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="2f166-439">Devuelve la primera posición de un valor dentro de una cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-439">Returns the first position of a value within a string.</span></span> <span data-ttu-id="2f166-440">La comparación distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-440">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-441">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-441">Parameters</span></span>

| <span data-ttu-id="2f166-442">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-442">Parameter</span></span> | <span data-ttu-id="2f166-443">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-443">Required</span></span> | <span data-ttu-id="2f166-444">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-444">Type</span></span> | <span data-ttu-id="2f166-445">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="2f166-446">stringToSearch</span></span> |<span data-ttu-id="2f166-447">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-447">Yes</span></span> |<span data-ttu-id="2f166-448">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-448">string</span></span> |<span data-ttu-id="2f166-449">El valor que contiene el elemento para buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-449">The value that contains the item to find.</span></span> |
| <span data-ttu-id="2f166-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="2f166-450">stringToFind</span></span> |<span data-ttu-id="2f166-451">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-451">Yes</span></span> |<span data-ttu-id="2f166-452">string</span><span class="sxs-lookup"><span data-stu-id="2f166-452">string</span></span> |<span data-ttu-id="2f166-453">El valor para buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-453">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-454">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-454">Return value</span></span>

<span data-ttu-id="2f166-455">Un entero que representa la posición del elemento que se va a buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-455">An integer that represents the position of the item to find.</span></span> <span data-ttu-id="2f166-456">El valor está basado en cero.</span><span class="sxs-lookup"><span data-stu-id="2f166-456">The value is zero-based.</span></span> <span data-ttu-id="2f166-457">Si no se encuentra el elemento, se devuelve -1.</span><span class="sxs-lookup"><span data-stu-id="2f166-457">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-458">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-458">Examples</span></span>

<span data-ttu-id="2f166-459">En el ejemplo siguiente se muestra cómo utilizar las funciones indexOf y lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="2f166-459">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="2f166-460">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-460">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-461">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-461">Name</span></span> | <span data-ttu-id="2f166-462">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-462">Type</span></span> | <span data-ttu-id="2f166-463">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-464">firstT</span><span class="sxs-lookup"><span data-stu-id="2f166-464">firstT</span></span> | <span data-ttu-id="2f166-465">int</span><span class="sxs-lookup"><span data-stu-id="2f166-465">Int</span></span> | <span data-ttu-id="2f166-466">0</span><span class="sxs-lookup"><span data-stu-id="2f166-466">0</span></span> |
| <span data-ttu-id="2f166-467">lastT</span><span class="sxs-lookup"><span data-stu-id="2f166-467">lastT</span></span> | <span data-ttu-id="2f166-468">int</span><span class="sxs-lookup"><span data-stu-id="2f166-468">Int</span></span> | <span data-ttu-id="2f166-469">3</span><span class="sxs-lookup"><span data-stu-id="2f166-469">3</span></span> |
| <span data-ttu-id="2f166-470">firstString</span><span class="sxs-lookup"><span data-stu-id="2f166-470">firstString</span></span> | <span data-ttu-id="2f166-471">int</span><span class="sxs-lookup"><span data-stu-id="2f166-471">Int</span></span> | <span data-ttu-id="2f166-472">2</span><span class="sxs-lookup"><span data-stu-id="2f166-472">2</span></span> |
| <span data-ttu-id="2f166-473">lastString</span><span class="sxs-lookup"><span data-stu-id="2f166-473">lastString</span></span> | <span data-ttu-id="2f166-474">int</span><span class="sxs-lookup"><span data-stu-id="2f166-474">Int</span></span> | <span data-ttu-id="2f166-475">0</span><span class="sxs-lookup"><span data-stu-id="2f166-475">0</span></span> |
| <span data-ttu-id="2f166-476">notFound</span><span class="sxs-lookup"><span data-stu-id="2f166-476">notFound</span></span> | <span data-ttu-id="2f166-477">int</span><span class="sxs-lookup"><span data-stu-id="2f166-477">Int</span></span> | <span data-ttu-id="2f166-478">-1</span><span class="sxs-lookup"><span data-stu-id="2f166-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="2f166-479">last</span><span class="sxs-lookup"><span data-stu-id="2f166-479">last</span></span>
`last (arg1)`

<span data-ttu-id="2f166-480">Devuelve el último carácter de la cadena, o el último elemento de la matriz.</span><span class="sxs-lookup"><span data-stu-id="2f166-480">Returns last character of the string, or the last element of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-481">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-481">Parameters</span></span>

| <span data-ttu-id="2f166-482">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-482">Parameter</span></span> | <span data-ttu-id="2f166-483">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-483">Required</span></span> | <span data-ttu-id="2f166-484">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-484">Type</span></span> | <span data-ttu-id="2f166-485">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-486">arg1</span><span class="sxs-lookup"><span data-stu-id="2f166-486">arg1</span></span> |<span data-ttu-id="2f166-487">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-487">Yes</span></span> |<span data-ttu-id="2f166-488">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-488">array or string</span></span> |<span data-ttu-id="2f166-489">El valor para recuperar el último elemento o carácter.</span><span class="sxs-lookup"><span data-stu-id="2f166-489">The value to retrieve the last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-490">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-490">Return value</span></span>

<span data-ttu-id="2f166-491">Una cadena del último carácter, o el tipo (cadena, entero, matriz u objeto) del último elemento de una matriz.</span><span class="sxs-lookup"><span data-stu-id="2f166-491">A string of the last character, or the type (string, int, array, or object) of the last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-492">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-492">Examples</span></span>

<span data-ttu-id="2f166-493">En el ejemplo siguiente se muestra cómo utilizar la última función con una matriz y una cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-493">The following example shows how to use the last function with an array and string.</span></span>

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

<span data-ttu-id="2f166-494">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-494">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-495">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-495">Name</span></span> | <span data-ttu-id="2f166-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-496">Type</span></span> | <span data-ttu-id="2f166-497">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-498">arrayOutput</span></span> | <span data-ttu-id="2f166-499">String</span><span class="sxs-lookup"><span data-stu-id="2f166-499">String</span></span> | <span data-ttu-id="2f166-500">three</span><span class="sxs-lookup"><span data-stu-id="2f166-500">three</span></span> |
| <span data-ttu-id="2f166-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-501">stringOutput</span></span> | <span data-ttu-id="2f166-502">String</span><span class="sxs-lookup"><span data-stu-id="2f166-502">String</span></span> | <span data-ttu-id="2f166-503">e</span><span class="sxs-lookup"><span data-stu-id="2f166-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="2f166-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="2f166-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="2f166-505">Devuelve la última posición de un valor dentro de una cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-505">Returns the last position of a value within a string.</span></span> <span data-ttu-id="2f166-506">La comparación distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-506">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-507">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-507">Parameters</span></span>

| <span data-ttu-id="2f166-508">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-508">Parameter</span></span> | <span data-ttu-id="2f166-509">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-509">Required</span></span> | <span data-ttu-id="2f166-510">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-510">Type</span></span> | <span data-ttu-id="2f166-511">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="2f166-512">stringToSearch</span></span> |<span data-ttu-id="2f166-513">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-513">Yes</span></span> |<span data-ttu-id="2f166-514">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-514">string</span></span> |<span data-ttu-id="2f166-515">El valor que contiene el elemento para buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-515">The value that contains the item to find.</span></span> |
| <span data-ttu-id="2f166-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="2f166-516">stringToFind</span></span> |<span data-ttu-id="2f166-517">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-517">Yes</span></span> |<span data-ttu-id="2f166-518">string</span><span class="sxs-lookup"><span data-stu-id="2f166-518">string</span></span> |<span data-ttu-id="2f166-519">El valor para buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-519">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-520">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-520">Return value</span></span>

<span data-ttu-id="2f166-521">Un entero que representa la última posición del elemento que se va a buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-521">An integer that represents the last position of the item to find.</span></span> <span data-ttu-id="2f166-522">El valor está basado en cero.</span><span class="sxs-lookup"><span data-stu-id="2f166-522">The value is zero-based.</span></span> <span data-ttu-id="2f166-523">Si no se encuentra el elemento, se devuelve -1.</span><span class="sxs-lookup"><span data-stu-id="2f166-523">If the item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-524">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-524">Examples</span></span>

<span data-ttu-id="2f166-525">En el ejemplo siguiente se muestra cómo utilizar las funciones indexOf y lastIndexOf:</span><span class="sxs-lookup"><span data-stu-id="2f166-525">The following example shows how to use the indexOf and lastIndexOf functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "firstT": {
            "value": "[indexOf('test', 't')]",
            "type" : "int"
        },
        "lastT": {
            "value": "[lastIndexOf('test', 't')]",
            "type" : "int"
        },
        "firstString": {
            "value": "[indexOf('abcdef', 'CD')]",
            "type" : "int"
        },
        "lastString": {
            "value": "[lastIndexOf('abcdef', 'AB')]",
            "type" : "int"
        },
        "notFound": {
            "value": "[indexOf('abcdef', 'z')]",
            "type" : "int"
        }
    }
}
```

<span data-ttu-id="2f166-526">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-526">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-527">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-527">Name</span></span> | <span data-ttu-id="2f166-528">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-528">Type</span></span> | <span data-ttu-id="2f166-529">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-530">firstT</span><span class="sxs-lookup"><span data-stu-id="2f166-530">firstT</span></span> | <span data-ttu-id="2f166-531">int</span><span class="sxs-lookup"><span data-stu-id="2f166-531">Int</span></span> | <span data-ttu-id="2f166-532">0</span><span class="sxs-lookup"><span data-stu-id="2f166-532">0</span></span> |
| <span data-ttu-id="2f166-533">lastT</span><span class="sxs-lookup"><span data-stu-id="2f166-533">lastT</span></span> | <span data-ttu-id="2f166-534">int</span><span class="sxs-lookup"><span data-stu-id="2f166-534">Int</span></span> | <span data-ttu-id="2f166-535">3</span><span class="sxs-lookup"><span data-stu-id="2f166-535">3</span></span> |
| <span data-ttu-id="2f166-536">firstString</span><span class="sxs-lookup"><span data-stu-id="2f166-536">firstString</span></span> | <span data-ttu-id="2f166-537">int</span><span class="sxs-lookup"><span data-stu-id="2f166-537">Int</span></span> | <span data-ttu-id="2f166-538">2</span><span class="sxs-lookup"><span data-stu-id="2f166-538">2</span></span> |
| <span data-ttu-id="2f166-539">lastString</span><span class="sxs-lookup"><span data-stu-id="2f166-539">lastString</span></span> | <span data-ttu-id="2f166-540">int</span><span class="sxs-lookup"><span data-stu-id="2f166-540">Int</span></span> | <span data-ttu-id="2f166-541">0</span><span class="sxs-lookup"><span data-stu-id="2f166-541">0</span></span> |
| <span data-ttu-id="2f166-542">notFound</span><span class="sxs-lookup"><span data-stu-id="2f166-542">notFound</span></span> | <span data-ttu-id="2f166-543">int</span><span class="sxs-lookup"><span data-stu-id="2f166-543">Int</span></span> | <span data-ttu-id="2f166-544">-1</span><span class="sxs-lookup"><span data-stu-id="2f166-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="2f166-545">length</span><span class="sxs-lookup"><span data-stu-id="2f166-545">length</span></span>
`length(string)`

<span data-ttu-id="2f166-546">Devuelve el número de caracteres de una cadena, o elementos de una matriz.</span><span class="sxs-lookup"><span data-stu-id="2f166-546">Returns the number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-547">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-547">Parameters</span></span>

| <span data-ttu-id="2f166-548">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-548">Parameter</span></span> | <span data-ttu-id="2f166-549">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-549">Required</span></span> | <span data-ttu-id="2f166-550">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-550">Type</span></span> | <span data-ttu-id="2f166-551">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-552">arg1</span><span class="sxs-lookup"><span data-stu-id="2f166-552">arg1</span></span> |<span data-ttu-id="2f166-553">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-553">Yes</span></span> |<span data-ttu-id="2f166-554">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-554">array or string</span></span> |<span data-ttu-id="2f166-555">La matriz que se usará para obtener el número de elementos, o la cadena que se usará para obtener el número de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2f166-555">The array to use for getting the number of elements, or the string to use for getting the number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-556">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-556">Return value</span></span>

<span data-ttu-id="2f166-557">Un entero.</span><span class="sxs-lookup"><span data-stu-id="2f166-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="2f166-558">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-558">Examples</span></span>

<span data-ttu-id="2f166-559">En el ejemplo siguiente se muestra cómo utilizar length con una matriz y una cadena:</span><span class="sxs-lookup"><span data-stu-id="2f166-559">The following example shows how to use length with an array and string:</span></span>

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

<span data-ttu-id="2f166-560">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-560">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-561">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-561">Name</span></span> | <span data-ttu-id="2f166-562">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-562">Type</span></span> | <span data-ttu-id="2f166-563">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="2f166-564">arrayLength</span></span> | <span data-ttu-id="2f166-565">int</span><span class="sxs-lookup"><span data-stu-id="2f166-565">Int</span></span> | <span data-ttu-id="2f166-566">3</span><span class="sxs-lookup"><span data-stu-id="2f166-566">3</span></span> |
| <span data-ttu-id="2f166-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="2f166-567">stringLength</span></span> | <span data-ttu-id="2f166-568">int</span><span class="sxs-lookup"><span data-stu-id="2f166-568">Int</span></span> | <span data-ttu-id="2f166-569">13</span><span class="sxs-lookup"><span data-stu-id="2f166-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="2f166-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="2f166-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="2f166-571">Devuelve una cadena alineada a la derecha agregando caracteres a la izquierda hasta alcanzar la longitud total especificada.</span><span class="sxs-lookup"><span data-stu-id="2f166-571">Returns a right-aligned string by adding characters to the left until reaching the total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-572">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-572">Parameters</span></span>

| <span data-ttu-id="2f166-573">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-573">Parameter</span></span> | <span data-ttu-id="2f166-574">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-574">Required</span></span> | <span data-ttu-id="2f166-575">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-575">Type</span></span> | <span data-ttu-id="2f166-576">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="2f166-577">valueToPad</span></span> |<span data-ttu-id="2f166-578">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-578">Yes</span></span> |<span data-ttu-id="2f166-579">cadena o entero</span><span class="sxs-lookup"><span data-stu-id="2f166-579">string or int</span></span> |<span data-ttu-id="2f166-580">Valor que se va a alinear a la derecha.</span><span class="sxs-lookup"><span data-stu-id="2f166-580">The value to right-align.</span></span> |
| <span data-ttu-id="2f166-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="2f166-581">totalLength</span></span> |<span data-ttu-id="2f166-582">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-582">Yes</span></span> |<span data-ttu-id="2f166-583">int</span><span class="sxs-lookup"><span data-stu-id="2f166-583">int</span></span> |<span data-ttu-id="2f166-584">El número total de caracteres de la cadena devuelta.</span><span class="sxs-lookup"><span data-stu-id="2f166-584">The total number of characters in the returned string.</span></span> |
| <span data-ttu-id="2f166-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="2f166-585">paddingCharacter</span></span> |<span data-ttu-id="2f166-586">No</span><span class="sxs-lookup"><span data-stu-id="2f166-586">No</span></span> |<span data-ttu-id="2f166-587">carácter individual</span><span class="sxs-lookup"><span data-stu-id="2f166-587">single character</span></span> |<span data-ttu-id="2f166-588">El carácter que se va a usar para el relleno a la izquierda hasta alcanza la longitud total.</span><span class="sxs-lookup"><span data-stu-id="2f166-588">The character to use for left-padding until the total length is reached.</span></span> <span data-ttu-id="2f166-589">El valor predeterminado es un espacio.</span><span class="sxs-lookup"><span data-stu-id="2f166-589">The default value is a space.</span></span> |

<span data-ttu-id="2f166-590">Si la cadena original es mayor que el número de caracteres que se va a rellenar, no se agrega ningún carácter.</span><span class="sxs-lookup"><span data-stu-id="2f166-590">If the original string is longer than the number of characters to pad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="2f166-591">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-591">Return value</span></span>

<span data-ttu-id="2f166-592">Una cadena con al menos el número de caracteres especificados.</span><span class="sxs-lookup"><span data-stu-id="2f166-592">A string with at least the number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-593">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-593">Examples</span></span>

<span data-ttu-id="2f166-594">En el ejemplo siguiente se muestra cómo rellenar el valor del parámetro proporcionado por el usuario agregando el carácter cero hasta que alcance el número total de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2f166-594">The following example shows how to pad the user-provided parameter value by adding the zero character until it reaches the total number of characters.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123"
        }
    },
    "resources": [],
    "outputs": {
        "stringOutput": {
            "type": "string",
            "value": "[padLeft(parameters('testString'),10,'0')]"
        }
    }
}
```

<span data-ttu-id="2f166-595">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-595">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-596">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-596">Name</span></span> | <span data-ttu-id="2f166-597">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-597">Type</span></span> | <span data-ttu-id="2f166-598">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-599">stringOutput</span></span> | <span data-ttu-id="2f166-600">String</span><span class="sxs-lookup"><span data-stu-id="2f166-600">String</span></span> | <span data-ttu-id="2f166-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="2f166-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="2f166-602">replace</span><span class="sxs-lookup"><span data-stu-id="2f166-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="2f166-603">Devuelve una nueva cadena con todas las instancias de una cadena reemplazadas por otra cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-604">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-604">Parameters</span></span>

| <span data-ttu-id="2f166-605">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-605">Parameter</span></span> | <span data-ttu-id="2f166-606">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-606">Required</span></span> | <span data-ttu-id="2f166-607">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-607">Type</span></span> | <span data-ttu-id="2f166-608">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-609">originalString</span><span class="sxs-lookup"><span data-stu-id="2f166-609">originalString</span></span> |<span data-ttu-id="2f166-610">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-610">Yes</span></span> |<span data-ttu-id="2f166-611">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-611">string</span></span> |<span data-ttu-id="2f166-612">Valor que tiene todas las instancias de una cadena reemplazadas por otra cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-612">The value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="2f166-613">oldString</span><span class="sxs-lookup"><span data-stu-id="2f166-613">oldString</span></span> |<span data-ttu-id="2f166-614">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-614">Yes</span></span> |<span data-ttu-id="2f166-615">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-615">string</span></span> |<span data-ttu-id="2f166-616">Cadena que se va a quitar de la cadena original.</span><span class="sxs-lookup"><span data-stu-id="2f166-616">The string to be removed from the original string.</span></span> |
| <span data-ttu-id="2f166-617">newString</span><span class="sxs-lookup"><span data-stu-id="2f166-617">newString</span></span> |<span data-ttu-id="2f166-618">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-618">Yes</span></span> |<span data-ttu-id="2f166-619">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-619">string</span></span> |<span data-ttu-id="2f166-620">La cadena que se va a agregar en lugar de la cadena eliminada.</span><span class="sxs-lookup"><span data-stu-id="2f166-620">The string to add in place of the removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-621">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-621">Return value</span></span>

<span data-ttu-id="2f166-622">Una cadena con los caracteres reemplazados.</span><span class="sxs-lookup"><span data-stu-id="2f166-622">A string with the replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-623">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-623">Examples</span></span>

<span data-ttu-id="2f166-624">El ejemplo siguiente muestra cómo quitar todos los guiones de la cadena proporcionada por el usuario y cómo reemplazar parte de la cadena por otra cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-624">The following example shows how to remove all dashes from the user-provided string, and how to replace part of the string with another string.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "123-123-1234"
        }
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'-', '')]"
        },
        "secodeOutput": {
            "type": "string",
            "value": "[replace(parameters('testString'),'1234', 'xxxx')]"
        }
    }
}
```

<span data-ttu-id="2f166-625">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-625">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-626">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-626">Name</span></span> | <span data-ttu-id="2f166-627">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-627">Type</span></span> | <span data-ttu-id="2f166-628">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-629">firstOutput</span></span> | <span data-ttu-id="2f166-630">String</span><span class="sxs-lookup"><span data-stu-id="2f166-630">String</span></span> | <span data-ttu-id="2f166-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="2f166-631">1231231234</span></span> |
| <span data-ttu-id="2f166-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-632">secodeOutput</span></span> | <span data-ttu-id="2f166-633">String</span><span class="sxs-lookup"><span data-stu-id="2f166-633">String</span></span> | <span data-ttu-id="2f166-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="2f166-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="2f166-635">skip</span><span class="sxs-lookup"><span data-stu-id="2f166-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="2f166-636">Devuelve una cadena con todos los caracteres después del número especificado de caracteres, o una matriz con todos los elementos después del número especificado de elementos.</span><span class="sxs-lookup"><span data-stu-id="2f166-636">Returns a string with all the characters after the specified number of characters, or an array with all the elements after the specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-637">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-637">Parameters</span></span>

| <span data-ttu-id="2f166-638">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-638">Parameter</span></span> | <span data-ttu-id="2f166-639">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-639">Required</span></span> | <span data-ttu-id="2f166-640">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-640">Type</span></span> | <span data-ttu-id="2f166-641">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="2f166-642">originalValue</span></span> |<span data-ttu-id="2f166-643">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-643">Yes</span></span> |<span data-ttu-id="2f166-644">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-644">array or string</span></span> |<span data-ttu-id="2f166-645">La matriz o cadena que se usará para la omisión.</span><span class="sxs-lookup"><span data-stu-id="2f166-645">The array or string to use for skipping.</span></span> |
| <span data-ttu-id="2f166-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="2f166-646">numberToSkip</span></span> |<span data-ttu-id="2f166-647">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-647">Yes</span></span> |<span data-ttu-id="2f166-648">int</span><span class="sxs-lookup"><span data-stu-id="2f166-648">int</span></span> |<span data-ttu-id="2f166-649">El número de elementos o caracteres que se van a omitir.</span><span class="sxs-lookup"><span data-stu-id="2f166-649">The number of elements or characters to skip.</span></span> <span data-ttu-id="2f166-650">Si este valor es 0 o un valor inferior, se devuelven todos los elementos o caracteres del valor.</span><span class="sxs-lookup"><span data-stu-id="2f166-650">If this value is 0 or less, all the elements or characters in the value are returned.</span></span> <span data-ttu-id="2f166-651">Si es mayor que la longitud de la matriz o la cadena, se devuelve una matriz o cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="2f166-651">If it is larger than the length of the array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-652">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-652">Return value</span></span>

<span data-ttu-id="2f166-653">Una matriz o cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-654">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-654">Examples</span></span>

<span data-ttu-id="2f166-655">En el ejemplo siguiente se omite el número especificado de elementos de la matriz, y el número especificado de caracteres de la cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-655">The following example skips the specified number of elements in the array, and the specified number of characters in a string.</span></span>

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

<span data-ttu-id="2f166-656">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-656">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-657">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-657">Name</span></span> | <span data-ttu-id="2f166-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-658">Type</span></span> | <span data-ttu-id="2f166-659">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-660">arrayOutput</span></span> | <span data-ttu-id="2f166-661">Matriz</span><span class="sxs-lookup"><span data-stu-id="2f166-661">Array</span></span> | <span data-ttu-id="2f166-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="2f166-662">["three"]</span></span> |
| <span data-ttu-id="2f166-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-663">stringOutput</span></span> | <span data-ttu-id="2f166-664">String</span><span class="sxs-lookup"><span data-stu-id="2f166-664">String</span></span> | <span data-ttu-id="2f166-665">two three</span><span class="sxs-lookup"><span data-stu-id="2f166-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="2f166-666">split</span><span class="sxs-lookup"><span data-stu-id="2f166-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="2f166-667">Devuelve una matriz de cadenas que contiene las subcadenas de la cadena de entrada que están delimitadas por los delimitadores especificados.</span><span class="sxs-lookup"><span data-stu-id="2f166-667">Returns an array of strings that contains the substrings of the input string that are delimited by the specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-668">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-668">Parameters</span></span>

| <span data-ttu-id="2f166-669">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-669">Parameter</span></span> | <span data-ttu-id="2f166-670">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-670">Required</span></span> | <span data-ttu-id="2f166-671">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-671">Type</span></span> | <span data-ttu-id="2f166-672">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-673">inputString</span><span class="sxs-lookup"><span data-stu-id="2f166-673">inputString</span></span> |<span data-ttu-id="2f166-674">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-674">Yes</span></span> |<span data-ttu-id="2f166-675">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-675">string</span></span> |<span data-ttu-id="2f166-676">La cadena que se va a dividir.</span><span class="sxs-lookup"><span data-stu-id="2f166-676">The string to split.</span></span> |
| <span data-ttu-id="2f166-677">delimiter</span><span class="sxs-lookup"><span data-stu-id="2f166-677">delimiter</span></span> |<span data-ttu-id="2f166-678">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-678">Yes</span></span> |<span data-ttu-id="2f166-679">cadena o matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="2f166-679">string or array of strings</span></span> |<span data-ttu-id="2f166-680">Delimitador que se utilizará para dividir la cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-680">The delimiter to use for splitting the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-681">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-681">Return value</span></span>

<span data-ttu-id="2f166-682">Una matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="2f166-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-683">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-683">Examples</span></span>

<span data-ttu-id="2f166-684">En el ejemplo siguiente se divide la cadena de entrada con una coma, y con una coma o un punto y coma.</span><span class="sxs-lookup"><span data-stu-id="2f166-684">The following example splits the input string with a comma, and with either a comma or a semi-colon.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "firstString": {
            "type": "string",
            "defaultValue": "one,two,three"
        },
        "secondString": {
            "type": "string",
            "defaultValue": "one;two,three"
        }
    },
    "variables": {
        "delimiters": [ ",", ";" ]
    },
    "resources": [],
    "outputs": {
        "firstOutput": {
            "type": "array",
            "value": "[split(parameters('firstString'),',')]"
        },
        "secondOutput": {
            "type": "array",
            "value": "[split(parameters('secondString'),variables('delimiters'))]"
        }
    }
}
```

<span data-ttu-id="2f166-685">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-685">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-686">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-686">Name</span></span> | <span data-ttu-id="2f166-687">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-687">Type</span></span> | <span data-ttu-id="2f166-688">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-689">firstOutput</span></span> | <span data-ttu-id="2f166-690">Matriz</span><span class="sxs-lookup"><span data-stu-id="2f166-690">Array</span></span> | <span data-ttu-id="2f166-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="2f166-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="2f166-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-692">secondOutput</span></span> | <span data-ttu-id="2f166-693">Matriz</span><span class="sxs-lookup"><span data-stu-id="2f166-693">Array</span></span> | <span data-ttu-id="2f166-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="2f166-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="2f166-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="2f166-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="2f166-696">Determina si una cadena empieza con un valor.</span><span class="sxs-lookup"><span data-stu-id="2f166-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="2f166-697">La comparación distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-697">The comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-698">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-698">Parameters</span></span>

| <span data-ttu-id="2f166-699">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-699">Parameter</span></span> | <span data-ttu-id="2f166-700">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-700">Required</span></span> | <span data-ttu-id="2f166-701">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-701">Type</span></span> | <span data-ttu-id="2f166-702">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="2f166-703">stringToSearch</span></span> |<span data-ttu-id="2f166-704">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-704">Yes</span></span> |<span data-ttu-id="2f166-705">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-705">string</span></span> |<span data-ttu-id="2f166-706">El valor que contiene el elemento para buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-706">The value that contains the item to find.</span></span> |
| <span data-ttu-id="2f166-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="2f166-707">stringToFind</span></span> |<span data-ttu-id="2f166-708">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-708">Yes</span></span> |<span data-ttu-id="2f166-709">string</span><span class="sxs-lookup"><span data-stu-id="2f166-709">string</span></span> |<span data-ttu-id="2f166-710">El valor para buscar.</span><span class="sxs-lookup"><span data-stu-id="2f166-710">The value to find.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-711">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-711">Return value</span></span>

<span data-ttu-id="2f166-712">**True** si el primer carácter o caracteres de la cadena coinciden con el valor; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="2f166-712">**True** if the first character or characters of the string match the value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-713">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-713">Examples</span></span>

<span data-ttu-id="2f166-714">En el ejemplo siguiente se muestra cómo utilizar las funciones startsWith y endsWith:</span><span class="sxs-lookup"><span data-stu-id="2f166-714">The following example shows how to use the startsWith and endsWith functions:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "startsTrue": {
            "value": "[startsWith('abcdef', 'ab')]",
            "type" : "bool"
        },
        "startsCapTrue": {
            "value": "[startsWith('abcdef', 'A')]",
            "type" : "bool"
        },
        "startsFalse": {
            "value": "[startsWith('abcdef', 'e')]",
            "type" : "bool"
        },
        "endsTrue": {
            "value": "[endsWith('abcdef', 'ef')]",
            "type" : "bool"
        },
        "endsCapTrue": {
            "value": "[endsWith('abcdef', 'F')]",
            "type" : "bool"
        },
        "endsFalse": {
            "value": "[endsWith('abcdef', 'e')]",
            "type" : "bool"
        }
    }
}
```

<span data-ttu-id="2f166-715">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-715">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-716">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-716">Name</span></span> | <span data-ttu-id="2f166-717">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-717">Type</span></span> | <span data-ttu-id="2f166-718">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-719">startsTrue</span></span> | <span data-ttu-id="2f166-720">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-720">Bool</span></span> | <span data-ttu-id="2f166-721">True</span><span class="sxs-lookup"><span data-stu-id="2f166-721">True</span></span> |
| <span data-ttu-id="2f166-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-722">startsCapTrue</span></span> | <span data-ttu-id="2f166-723">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-723">Bool</span></span> | <span data-ttu-id="2f166-724">True</span><span class="sxs-lookup"><span data-stu-id="2f166-724">True</span></span> |
| <span data-ttu-id="2f166-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="2f166-725">startsFalse</span></span> | <span data-ttu-id="2f166-726">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-726">Bool</span></span> | <span data-ttu-id="2f166-727">False</span><span class="sxs-lookup"><span data-stu-id="2f166-727">False</span></span> |
| <span data-ttu-id="2f166-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-728">endsTrue</span></span> | <span data-ttu-id="2f166-729">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-729">Bool</span></span> | <span data-ttu-id="2f166-730">True</span><span class="sxs-lookup"><span data-stu-id="2f166-730">True</span></span> |
| <span data-ttu-id="2f166-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="2f166-731">endsCapTrue</span></span> | <span data-ttu-id="2f166-732">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-732">Bool</span></span> | <span data-ttu-id="2f166-733">True</span><span class="sxs-lookup"><span data-stu-id="2f166-733">True</span></span> |
| <span data-ttu-id="2f166-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="2f166-734">endsFalse</span></span> | <span data-ttu-id="2f166-735">Booleano</span><span class="sxs-lookup"><span data-stu-id="2f166-735">Bool</span></span> | <span data-ttu-id="2f166-736">False</span><span class="sxs-lookup"><span data-stu-id="2f166-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="2f166-737">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="2f166-738">Convierte el valor especificado en cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-738">Converts the specified value to a string.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-739">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-739">Parameters</span></span>

| <span data-ttu-id="2f166-740">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-740">Parameter</span></span> | <span data-ttu-id="2f166-741">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-741">Required</span></span> | <span data-ttu-id="2f166-742">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-742">Type</span></span> | <span data-ttu-id="2f166-743">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="2f166-744">valueToConvert</span></span> |<span data-ttu-id="2f166-745">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-745">Yes</span></span> | <span data-ttu-id="2f166-746">Cualquiera</span><span class="sxs-lookup"><span data-stu-id="2f166-746">Any</span></span> |<span data-ttu-id="2f166-747">El valor que se convierte en cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-747">The value to convert to string.</span></span> <span data-ttu-id="2f166-748">Se puede convertir cualquier tipo de valor, incluidos objetos y matrices.</span><span class="sxs-lookup"><span data-stu-id="2f166-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-749">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-749">Return value</span></span>

<span data-ttu-id="2f166-750">Cadena del valor convertido.</span><span class="sxs-lookup"><span data-stu-id="2f166-750">A string of the converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-751">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-751">Examples</span></span>

<span data-ttu-id="2f166-752">En el ejemplo siguiente se muestra cómo convertir distintos tipos de valores en cadenas:</span><span class="sxs-lookup"><span data-stu-id="2f166-752">The following example shows how to convert different types of values to strings:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testObject": {
            "type": "object",
            "defaultValue": {
                "valueA": 10,
                "valueB": "Example Text"
            }
        },
        "testArray": {
            "type": "array",
            "defaultValue": [
                "a",
                "b",
                "c"
            ]
        },
        "testInt": {
            "type": "int",
            "defaultValue": 5
        }
    },
    "resources": [],
    "outputs": {
        "objectOutput": {
            "type": "string",
            "value": "[string(parameters('testObject'))]"
        },
        "arrayOutput": {
            "type": "string",
            "value": "[string(parameters('testArray'))]"
        },
        "intOutput": {
            "type": "string",
            "value": "[string(parameters('testInt'))]"
        }
    }
}
```

<span data-ttu-id="2f166-753">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-753">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-754">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-754">Name</span></span> | <span data-ttu-id="2f166-755">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-755">Type</span></span> | <span data-ttu-id="2f166-756">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-757">objectOutput</span></span> | <span data-ttu-id="2f166-758">String</span><span class="sxs-lookup"><span data-stu-id="2f166-758">String</span></span> | <span data-ttu-id="2f166-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="2f166-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="2f166-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-760">arrayOutput</span></span> | <span data-ttu-id="2f166-761">String</span><span class="sxs-lookup"><span data-stu-id="2f166-761">String</span></span> | <span data-ttu-id="2f166-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="2f166-762">["a","b","c"]</span></span> |
| <span data-ttu-id="2f166-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-763">intOutput</span></span> | <span data-ttu-id="2f166-764">String</span><span class="sxs-lookup"><span data-stu-id="2f166-764">String</span></span> | <span data-ttu-id="2f166-765">5</span><span class="sxs-lookup"><span data-stu-id="2f166-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="2f166-766">substring</span><span class="sxs-lookup"><span data-stu-id="2f166-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="2f166-767">Devuelve una subcadena que empieza en la posición de carácter especificada y que contiene el número especificado de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2f166-767">Returns a substring that starts at the specified character position and contains the specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-768">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-768">Parameters</span></span>

| <span data-ttu-id="2f166-769">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-769">Parameter</span></span> | <span data-ttu-id="2f166-770">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-770">Required</span></span> | <span data-ttu-id="2f166-771">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-771">Type</span></span> | <span data-ttu-id="2f166-772">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="2f166-773">stringToParse</span></span> |<span data-ttu-id="2f166-774">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-774">Yes</span></span> |<span data-ttu-id="2f166-775">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-775">string</span></span> |<span data-ttu-id="2f166-776">La cadena original desde la que se extrae la subcadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-776">The original string from which the substring is extracted.</span></span> |
| <span data-ttu-id="2f166-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="2f166-777">startIndex</span></span> |<span data-ttu-id="2f166-778">No</span><span class="sxs-lookup"><span data-stu-id="2f166-778">No</span></span> |<span data-ttu-id="2f166-779">int</span><span class="sxs-lookup"><span data-stu-id="2f166-779">int</span></span> |<span data-ttu-id="2f166-780">La posición de carácter inicial basado en cero de la subcadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-780">The zero-based starting character position for the substring.</span></span> |
| <span data-ttu-id="2f166-781">length</span><span class="sxs-lookup"><span data-stu-id="2f166-781">length</span></span> |<span data-ttu-id="2f166-782">No</span><span class="sxs-lookup"><span data-stu-id="2f166-782">No</span></span> |<span data-ttu-id="2f166-783">int</span><span class="sxs-lookup"><span data-stu-id="2f166-783">int</span></span> |<span data-ttu-id="2f166-784">El número de caracteres de la subcadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-784">The number of characters for the substring.</span></span> <span data-ttu-id="2f166-785">Debe hacer referencia a una ubicación dentro de la cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-785">Must refer to a location within the string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-786">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-786">Return value</span></span>

<span data-ttu-id="2f166-787">Subcadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-787">The substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="2f166-788">Comentarios</span><span class="sxs-lookup"><span data-stu-id="2f166-788">Remarks</span></span>

<span data-ttu-id="2f166-789">La función genera un error cuando la subcadena supera el final de la cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-789">The function fails when the substring extends beyond the end of the string.</span></span> <span data-ttu-id="2f166-790">En el ejemplo siguiente se produce el error "Los parámetros index y length deben hacer referencia a una ubicación dentro de la cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-790">The following example fails with the error "The index and length parameters must refer to a location within the string.</span></span> <span data-ttu-id="2f166-791">Parámetro index: '0'; parámetro length: '11'; longitud del parámetro string: '10'.</span><span class="sxs-lookup"><span data-stu-id="2f166-791">The index parameter: '0', the length parameter: '11', the length of the string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="2f166-792">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-792">Examples</span></span>

<span data-ttu-id="2f166-793">En el ejemplo siguiente se extrae una subcadena de un parámetro.</span><span class="sxs-lookup"><span data-stu-id="2f166-793">The following example extracts a substring from a parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "one two three"
        }
    },
    "resources": [],
    "outputs": {
        "substringOutput": {
            "value": "[substring(parameters('testString'), 4, 3)]",
            "type": "string"
        }
    }
}
```

<span data-ttu-id="2f166-794">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-794">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-795">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-795">Name</span></span> | <span data-ttu-id="2f166-796">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-796">Type</span></span> | <span data-ttu-id="2f166-797">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-798">substringOutput</span></span> | <span data-ttu-id="2f166-799">String</span><span class="sxs-lookup"><span data-stu-id="2f166-799">String</span></span> | <span data-ttu-id="2f166-800">two</span><span class="sxs-lookup"><span data-stu-id="2f166-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="2f166-801">take</span><span class="sxs-lookup"><span data-stu-id="2f166-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="2f166-802">Devuelve una cadena con el número especificado de caracteres desde el inicio de la cadena, o una matriz con el número especificado de elementos desde el inicio de la matriz.</span><span class="sxs-lookup"><span data-stu-id="2f166-802">Returns a string with the specified number of characters from the start of the string, or an array with the specified number of elements from the start of the array.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-803">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-803">Parameters</span></span>

| <span data-ttu-id="2f166-804">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-804">Parameter</span></span> | <span data-ttu-id="2f166-805">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-805">Required</span></span> | <span data-ttu-id="2f166-806">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-806">Type</span></span> | <span data-ttu-id="2f166-807">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="2f166-808">originalValue</span></span> |<span data-ttu-id="2f166-809">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-809">Yes</span></span> |<span data-ttu-id="2f166-810">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-810">array or string</span></span> |<span data-ttu-id="2f166-811">La matriz o cadena de la que se van a tomar los elementos.</span><span class="sxs-lookup"><span data-stu-id="2f166-811">The array or string to take the elements from.</span></span> |
| <span data-ttu-id="2f166-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="2f166-812">numberToTake</span></span> |<span data-ttu-id="2f166-813">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-813">Yes</span></span> |<span data-ttu-id="2f166-814">int</span><span class="sxs-lookup"><span data-stu-id="2f166-814">int</span></span> |<span data-ttu-id="2f166-815">El número de elementos o caracteres que se van a tomar.</span><span class="sxs-lookup"><span data-stu-id="2f166-815">The number of elements or characters to take.</span></span> <span data-ttu-id="2f166-816">Si este valor es 0 o un valor inferior, se devolverá una matriz o cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="2f166-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="2f166-817">Si es mayor que la longitud de la matriz o cadena especificada, se devuelven todos los elementos de la matriz o cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-817">If it is larger than the length of the given array or string, all the elements in the array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-818">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-818">Return value</span></span>

<span data-ttu-id="2f166-819">Una matriz o cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-820">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-820">Examples</span></span>

<span data-ttu-id="2f166-821">En el ejemplo siguiente se toma el número especificado de elementos de la matriz y de caracteres de la cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-821">The following example takes the specified number of elements from the array, and characters from a string.</span></span>

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

<span data-ttu-id="2f166-822">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-822">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-823">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-823">Name</span></span> | <span data-ttu-id="2f166-824">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-824">Type</span></span> | <span data-ttu-id="2f166-825">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-826">arrayOutput</span></span> | <span data-ttu-id="2f166-827">Matriz</span><span class="sxs-lookup"><span data-stu-id="2f166-827">Array</span></span> | <span data-ttu-id="2f166-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="2f166-828">["one", "two"]</span></span> |
| <span data-ttu-id="2f166-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-829">stringOutput</span></span> | <span data-ttu-id="2f166-830">String</span><span class="sxs-lookup"><span data-stu-id="2f166-830">String</span></span> | <span data-ttu-id="2f166-831">en</span><span class="sxs-lookup"><span data-stu-id="2f166-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="2f166-832">toLower</span><span class="sxs-lookup"><span data-stu-id="2f166-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="2f166-833">Convierte la cadena especificada a minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-833">Converts the specified string to lower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-834">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-834">Parameters</span></span>

| <span data-ttu-id="2f166-835">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-835">Parameter</span></span> | <span data-ttu-id="2f166-836">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-836">Required</span></span> | <span data-ttu-id="2f166-837">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-837">Type</span></span> | <span data-ttu-id="2f166-838">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="2f166-839">stringToChange</span></span> |<span data-ttu-id="2f166-840">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-840">Yes</span></span> |<span data-ttu-id="2f166-841">string</span><span class="sxs-lookup"><span data-stu-id="2f166-841">string</span></span> |<span data-ttu-id="2f166-842">Valor que se va a convertir a minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-842">The value to convert to lower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-843">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-843">Return value</span></span>

<span data-ttu-id="2f166-844">Cadena convertida a minúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-844">The string converted to lower case.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-845">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-845">Examples</span></span>

<span data-ttu-id="2f166-846">En el siguiente ejemplo se convierte un valor de parámetro a minúsculas y a mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-846">The following example converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="2f166-847">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-847">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-848">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-848">Name</span></span> | <span data-ttu-id="2f166-849">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-849">Type</span></span> | <span data-ttu-id="2f166-850">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-851">toLowerOutput</span></span> | <span data-ttu-id="2f166-852">String</span><span class="sxs-lookup"><span data-stu-id="2f166-852">String</span></span> | <span data-ttu-id="2f166-853">one two three</span><span class="sxs-lookup"><span data-stu-id="2f166-853">one two three</span></span> |
| <span data-ttu-id="2f166-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-854">toUpperOutput</span></span> | <span data-ttu-id="2f166-855">String</span><span class="sxs-lookup"><span data-stu-id="2f166-855">String</span></span> | <span data-ttu-id="2f166-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="2f166-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="2f166-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="2f166-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="2f166-858">Convierte la cadena especificada a mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-858">Converts the specified string to upper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-859">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-859">Parameters</span></span>

| <span data-ttu-id="2f166-860">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-860">Parameter</span></span> | <span data-ttu-id="2f166-861">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-861">Required</span></span> | <span data-ttu-id="2f166-862">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-862">Type</span></span> | <span data-ttu-id="2f166-863">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="2f166-864">stringToChange</span></span> |<span data-ttu-id="2f166-865">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-865">Yes</span></span> |<span data-ttu-id="2f166-866">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-866">string</span></span> |<span data-ttu-id="2f166-867">Valor que se va a convertir a mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-867">The value to convert to upper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-868">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-868">Return value</span></span>

<span data-ttu-id="2f166-869">Cadena convertida a mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-869">The string converted to upper case.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-870">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-870">Examples</span></span>

<span data-ttu-id="2f166-871">En el siguiente ejemplo se convierte un valor de parámetro a minúsculas y a mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="2f166-871">The following example converts a parameter value to lower case and to upper case.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "One Two Three"
        }
    },
    "resources": [],
    "outputs": {
        "toLowerOutput": {
            "value": "[toLower(parameters('testString'))]",
            "type": "string"
        },
        "toUpperOutput": {
            "type": "string",
            "value": "[toUpper(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="2f166-872">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-872">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-873">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-873">Name</span></span> | <span data-ttu-id="2f166-874">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-874">Type</span></span> | <span data-ttu-id="2f166-875">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-876">toLowerOutput</span></span> | <span data-ttu-id="2f166-877">String</span><span class="sxs-lookup"><span data-stu-id="2f166-877">String</span></span> | <span data-ttu-id="2f166-878">one two three</span><span class="sxs-lookup"><span data-stu-id="2f166-878">one two three</span></span> |
| <span data-ttu-id="2f166-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-879">toUpperOutput</span></span> | <span data-ttu-id="2f166-880">String</span><span class="sxs-lookup"><span data-stu-id="2f166-880">String</span></span> | <span data-ttu-id="2f166-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="2f166-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="2f166-882">trim</span><span class="sxs-lookup"><span data-stu-id="2f166-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="2f166-883">Quita todos los caracteres de espacio en blanco iniciales y finales de la cadena especificada.</span><span class="sxs-lookup"><span data-stu-id="2f166-883">Removes all leading and trailing white-space characters from the specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-884">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-884">Parameters</span></span>

| <span data-ttu-id="2f166-885">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-885">Parameter</span></span> | <span data-ttu-id="2f166-886">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-886">Required</span></span> | <span data-ttu-id="2f166-887">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-887">Type</span></span> | <span data-ttu-id="2f166-888">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="2f166-889">stringToTrim</span></span> |<span data-ttu-id="2f166-890">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-890">Yes</span></span> |<span data-ttu-id="2f166-891">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-891">string</span></span> |<span data-ttu-id="2f166-892">Valor que se recortará.</span><span class="sxs-lookup"><span data-stu-id="2f166-892">The value to trim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-893">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-893">Return value</span></span>

<span data-ttu-id="2f166-894">Cadena sin caracteres de espacio en blanco iniciales ni finales.</span><span class="sxs-lookup"><span data-stu-id="2f166-894">The string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-895">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-895">Examples</span></span>

<span data-ttu-id="2f166-896">En el ejemplo siguiente se recortan los caracteres de espacio en blanco del parámetro.</span><span class="sxs-lookup"><span data-stu-id="2f166-896">The following example trims the white-space characters from the parameter.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "testString": {
            "type": "string",
            "defaultValue": "    one two three   "
        }
    },
    "resources": [],
    "outputs": {
        "return": {
            "type": "string",
            "value": "[trim(parameters('testString'))]"
        }
    }
}
```

<span data-ttu-id="2f166-897">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-897">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-898">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-898">Name</span></span> | <span data-ttu-id="2f166-899">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-899">Type</span></span> | <span data-ttu-id="2f166-900">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-901">return</span><span class="sxs-lookup"><span data-stu-id="2f166-901">return</span></span> | <span data-ttu-id="2f166-902">String</span><span class="sxs-lookup"><span data-stu-id="2f166-902">String</span></span> | <span data-ttu-id="2f166-903">one two three</span><span class="sxs-lookup"><span data-stu-id="2f166-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="2f166-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="2f166-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="2f166-905">Crea una cadena de hash determinista basada en los valores proporcionados como parámetros.</span><span class="sxs-lookup"><span data-stu-id="2f166-905">Creates a deterministic hash string based on the values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="2f166-906">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-906">Parameters</span></span>

| <span data-ttu-id="2f166-907">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-907">Parameter</span></span> | <span data-ttu-id="2f166-908">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-908">Required</span></span> | <span data-ttu-id="2f166-909">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-909">Type</span></span> | <span data-ttu-id="2f166-910">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-911">baseString</span><span class="sxs-lookup"><span data-stu-id="2f166-911">baseString</span></span> |<span data-ttu-id="2f166-912">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-912">Yes</span></span> |<span data-ttu-id="2f166-913">string</span><span class="sxs-lookup"><span data-stu-id="2f166-913">string</span></span> |<span data-ttu-id="2f166-914">Valor utilizado en la función hash para crear una cadena única.</span><span class="sxs-lookup"><span data-stu-id="2f166-914">The value used in the hash function to create a unique string.</span></span> |
| <span data-ttu-id="2f166-915">parámetros adicionales según sea necesario</span><span class="sxs-lookup"><span data-stu-id="2f166-915">additional parameters as needed</span></span> |<span data-ttu-id="2f166-916">No</span><span class="sxs-lookup"><span data-stu-id="2f166-916">No</span></span> |<span data-ttu-id="2f166-917">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-917">string</span></span> |<span data-ttu-id="2f166-918">Puede agregar tantas cadenas como necesite para crear el valor que especifica el nivel de unicidad.</span><span class="sxs-lookup"><span data-stu-id="2f166-918">You can add as many strings as needed to create the value that specifies the level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="2f166-919">Comentarios</span><span class="sxs-lookup"><span data-stu-id="2f166-919">Remarks</span></span>

<span data-ttu-id="2f166-920">Esta función es útil cuando se debe crear un nombre único para un recurso.</span><span class="sxs-lookup"><span data-stu-id="2f166-920">This function is helpful when you need to create a unique name for a resource.</span></span> <span data-ttu-id="2f166-921">Proporciona valores de parámetros que limitan el ámbito de unicidad del resultado.</span><span class="sxs-lookup"><span data-stu-id="2f166-921">You provide parameter values that limit the scope of uniqueness for the result.</span></span> <span data-ttu-id="2f166-922">Puede especificar si el nombre es único para la suscripción, el grupo de recursos o la implementación.</span><span class="sxs-lookup"><span data-stu-id="2f166-922">You can specify whether the name is unique down to subscription, resource group, or deployment.</span></span> 

<span data-ttu-id="2f166-923">El valor devuelto no es una cadena aleatoria, sino que es el resultado de una función hash.</span><span class="sxs-lookup"><span data-stu-id="2f166-923">The returned value is not a random string, but rather the result of a hash function.</span></span> <span data-ttu-id="2f166-924">El valor devuelto tiene 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="2f166-924">The returned value is 13 characters long.</span></span> <span data-ttu-id="2f166-925">Debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="2f166-925">It is not globally unique.</span></span> <span data-ttu-id="2f166-926">Puede que desee combinar el valor con un prefijo de su convención de nomenclatura para crear un nombre que sea más fácil de reconocer.</span><span class="sxs-lookup"><span data-stu-id="2f166-926">You may want to combine the value with a prefix from your naming convention to create a name that is meaningful.</span></span> <span data-ttu-id="2f166-927">En el ejemplo siguiente se muestra el formato del valor devuelto.</span><span class="sxs-lookup"><span data-stu-id="2f166-927">The following example shows the format of the returned value.</span></span> <span data-ttu-id="2f166-928">El valor real varía según los parámetros proporcionados.</span><span class="sxs-lookup"><span data-stu-id="2f166-928">The actual value varies by the provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="2f166-929">En los ejemplos siguientes se muestra cómo utilizar uniqueString a fin de crear un valor único para niveles de uso común.</span><span class="sxs-lookup"><span data-stu-id="2f166-929">The following examples show how to use uniqueString to create a unique value for commonly used levels.</span></span>

<span data-ttu-id="2f166-930">Único basado en la suscripción</span><span class="sxs-lookup"><span data-stu-id="2f166-930">Unique scoped to subscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="2f166-931">Único basado en el grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2f166-931">Unique scoped to resource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="2f166-932">Único basado en la implementación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2f166-932">Unique scoped to deployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="2f166-933">En el ejemplo siguiente se muestra cómo crear un nombre único para una cuenta de almacenamiento basada en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2f166-933">The following example shows how to create a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="2f166-934">Dentro del grupo de recursos, el nombre no es único si crea de la misma manera.</span><span class="sxs-lookup"><span data-stu-id="2f166-934">Inside the resource group, the name is not unique if constructed the same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="2f166-935">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-935">Return value</span></span>

<span data-ttu-id="2f166-936">Cadena que contiene 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="2f166-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-937">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-937">Examples</span></span>

<span data-ttu-id="2f166-938">En el ejemplo siguiente se devuelven los resultados de uniquestring:</span><span class="sxs-lookup"><span data-stu-id="2f166-938">The following example returns results from uniquestring:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "uniqueRG": {
            "value": "[uniqueString(resourceGroup().id)]",
            "type" : "string"
        },
        "uniqueDeploy": {
            "value": "[uniqueString(resourceGroup().id, deployment().name)]",
            "type" : "string"
        }
    }
}
```

<a id="uri" />

## <a name="uri"></a><span data-ttu-id="2f166-939">uri</span><span class="sxs-lookup"><span data-stu-id="2f166-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="2f166-940">Crea un URI absoluto mediante la combinación de la cadena de relativeUri y baseUri.</span><span class="sxs-lookup"><span data-stu-id="2f166-940">Creates an absolute URI by combining the baseUri and the relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-941">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-941">Parameters</span></span>

| <span data-ttu-id="2f166-942">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-942">Parameter</span></span> | <span data-ttu-id="2f166-943">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-943">Required</span></span> | <span data-ttu-id="2f166-944">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-944">Type</span></span> | <span data-ttu-id="2f166-945">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="2f166-946">baseUri</span></span> |<span data-ttu-id="2f166-947">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-947">Yes</span></span> |<span data-ttu-id="2f166-948">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-948">string</span></span> |<span data-ttu-id="2f166-949">La cadena de uri base.</span><span class="sxs-lookup"><span data-stu-id="2f166-949">The base uri string.</span></span> |
| <span data-ttu-id="2f166-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="2f166-950">relativeUri</span></span> |<span data-ttu-id="2f166-951">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-951">Yes</span></span> |<span data-ttu-id="2f166-952">string</span><span class="sxs-lookup"><span data-stu-id="2f166-952">string</span></span> |<span data-ttu-id="2f166-953">La cadena de uri relativo que se agregará a la cadena de uri base.</span><span class="sxs-lookup"><span data-stu-id="2f166-953">The relative uri string to add to the base uri string.</span></span> |

<span data-ttu-id="2f166-954">El valor del parámetro **baseUri** puede incluir un archivo específico, pero al construir el identificador URI, solo se usa la ruta de acceso base.</span><span class="sxs-lookup"><span data-stu-id="2f166-954">The value for the **baseUri** parameter can include a specific file, but only the base path is used when constructing the URI.</span></span> <span data-ttu-id="2f166-955">Por ejemplo, al pasar `http://contoso.com/resources/azuredeploy.json` como parámetro baseUri, se obtiene como resultado un identificador URI base de `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="2f166-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as the baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="2f166-956">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-956">Return value</span></span>

<span data-ttu-id="2f166-957">Una cadena que representa el identificador URI absoluto para los valores base y relativos.</span><span class="sxs-lookup"><span data-stu-id="2f166-957">A string representing the absolute URI for the base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-958">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-958">Examples</span></span>

<span data-ttu-id="2f166-959">En el ejemplo siguiente se muestra cómo construir un vínculo a una plantilla anidada en función del valor de la plantilla principal.</span><span class="sxs-lookup"><span data-stu-id="2f166-959">The following example shows how to construct a link to a nested template based on the value of the parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="2f166-960">En el ejemplo siguiente se muestra cómo usar uri, uriComponent y uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="2f166-960">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="2f166-961">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-961">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-962">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-962">Name</span></span> | <span data-ttu-id="2f166-963">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-963">Type</span></span> | <span data-ttu-id="2f166-964">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-965">uriOutput</span></span> | <span data-ttu-id="2f166-966">String</span><span class="sxs-lookup"><span data-stu-id="2f166-966">String</span></span> | <span data-ttu-id="2f166-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="2f166-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="2f166-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-968">componentOutput</span></span> | <span data-ttu-id="2f166-969">String</span><span class="sxs-lookup"><span data-stu-id="2f166-969">String</span></span> | <span data-ttu-id="2f166-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="2f166-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="2f166-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-971">toStringOutput</span></span> | <span data-ttu-id="2f166-972">String</span><span class="sxs-lookup"><span data-stu-id="2f166-972">String</span></span> | <span data-ttu-id="2f166-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="2f166-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="2f166-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="2f166-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="2f166-975">Codifica un identificador URI.</span><span class="sxs-lookup"><span data-stu-id="2f166-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-976">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-976">Parameters</span></span>

| <span data-ttu-id="2f166-977">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-977">Parameter</span></span> | <span data-ttu-id="2f166-978">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-978">Required</span></span> | <span data-ttu-id="2f166-979">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-979">Type</span></span> | <span data-ttu-id="2f166-980">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="2f166-981">stringToEncode</span></span> |<span data-ttu-id="2f166-982">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-982">Yes</span></span> |<span data-ttu-id="2f166-983">string</span><span class="sxs-lookup"><span data-stu-id="2f166-983">string</span></span> |<span data-ttu-id="2f166-984">El valor para codificar.</span><span class="sxs-lookup"><span data-stu-id="2f166-984">The value to encode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-985">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-985">Return value</span></span>

<span data-ttu-id="2f166-986">Una cadena del valor codificado por el identificador URI.</span><span class="sxs-lookup"><span data-stu-id="2f166-986">A string of the URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-987">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-987">Examples</span></span>

<span data-ttu-id="2f166-988">En el ejemplo siguiente se muestra cómo usar uri, uriComponent y uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="2f166-988">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="2f166-989">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-989">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-990">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-990">Name</span></span> | <span data-ttu-id="2f166-991">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-991">Type</span></span> | <span data-ttu-id="2f166-992">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-993">uriOutput</span></span> | <span data-ttu-id="2f166-994">String</span><span class="sxs-lookup"><span data-stu-id="2f166-994">String</span></span> | <span data-ttu-id="2f166-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="2f166-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="2f166-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-996">componentOutput</span></span> | <span data-ttu-id="2f166-997">String</span><span class="sxs-lookup"><span data-stu-id="2f166-997">String</span></span> | <span data-ttu-id="2f166-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="2f166-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="2f166-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-999">toStringOutput</span></span> | <span data-ttu-id="2f166-1000">String</span><span class="sxs-lookup"><span data-stu-id="2f166-1000">String</span></span> | <span data-ttu-id="2f166-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="2f166-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="2f166-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="2f166-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="2f166-1003">Devuelve una cadena del valor codificado por el identificador URI.</span><span class="sxs-lookup"><span data-stu-id="2f166-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="2f166-1004">parameters</span><span class="sxs-lookup"><span data-stu-id="2f166-1004">Parameters</span></span>

| <span data-ttu-id="2f166-1005">Parámetro</span><span class="sxs-lookup"><span data-stu-id="2f166-1005">Parameter</span></span> | <span data-ttu-id="2f166-1006">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="2f166-1006">Required</span></span> | <span data-ttu-id="2f166-1007">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-1007">Type</span></span> | <span data-ttu-id="2f166-1008">Descripción</span><span class="sxs-lookup"><span data-stu-id="2f166-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2f166-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="2f166-1009">uriEncodedString</span></span> |<span data-ttu-id="2f166-1010">Sí</span><span class="sxs-lookup"><span data-stu-id="2f166-1010">Yes</span></span> |<span data-ttu-id="2f166-1011">cadena</span><span class="sxs-lookup"><span data-stu-id="2f166-1011">string</span></span> |<span data-ttu-id="2f166-1012">El valor codificado por el identificador URI para convertir en una cadena.</span><span class="sxs-lookup"><span data-stu-id="2f166-1012">The URI encoded value to convert to a string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="2f166-1013">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="2f166-1013">Return value</span></span>

<span data-ttu-id="2f166-1014">Una cadena descodificada del valor codificado por el identificador URI.</span><span class="sxs-lookup"><span data-stu-id="2f166-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="2f166-1015">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="2f166-1015">Examples</span></span>

<span data-ttu-id="2f166-1016">En el ejemplo siguiente se muestra cómo usar uri, uriComponent y uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="2f166-1016">The following example shows how to use uri, uriComponent, and uriComponentToString:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
        "uriFormat": "[uri('http://contoso.com/resources/', 'nested/azuredeploy.json')]",
        "uriEncoded": "[uriComponent(variables('uriFormat'))]" 
    },
    "resources": [
    ],
    "outputs": {
        "uriOutput": {
            "type": "string",
            "value": "[variables('uriFormat')]"
        },
        "componentOutput": {
            "type": "string",
            "value": "[variables('uriEncoded')]"
        },
        "toStringOutput": {
            "type": "string",
            "value": "[uriComponentToString(variables('uriEncoded'))]"
        }
    }
}
```

<span data-ttu-id="2f166-1017">La salida del ejemplo anterior con los valores predeterminados es:</span><span class="sxs-lookup"><span data-stu-id="2f166-1017">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="2f166-1018">Nombre</span><span class="sxs-lookup"><span data-stu-id="2f166-1018">Name</span></span> | <span data-ttu-id="2f166-1019">Tipo</span><span class="sxs-lookup"><span data-stu-id="2f166-1019">Type</span></span> | <span data-ttu-id="2f166-1020">Valor</span><span class="sxs-lookup"><span data-stu-id="2f166-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="2f166-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-1021">uriOutput</span></span> | <span data-ttu-id="2f166-1022">String</span><span class="sxs-lookup"><span data-stu-id="2f166-1022">String</span></span> | <span data-ttu-id="2f166-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="2f166-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="2f166-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-1024">componentOutput</span></span> | <span data-ttu-id="2f166-1025">String</span><span class="sxs-lookup"><span data-stu-id="2f166-1025">String</span></span> | <span data-ttu-id="2f166-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="2f166-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="2f166-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="2f166-1027">toStringOutput</span></span> | <span data-ttu-id="2f166-1028">String</span><span class="sxs-lookup"><span data-stu-id="2f166-1028">String</span></span> | <span data-ttu-id="2f166-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="2f166-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="2f166-1030">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f166-1030">Next steps</span></span>
* <span data-ttu-id="2f166-1031">Para obtener una descripción de las secciones de una plantilla de Azure Resource Manager, vea [Creación de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2f166-1031">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="2f166-1032">Para combinar varias plantillas, vea [Uso de plantillas vinculadas con Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2f166-1032">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="2f166-1033">Para iterar una cantidad de veces específica al crear un tipo de recurso, vea [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2f166-1033">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="2f166-1034">Para saber cómo implementar la plantilla que creó, consulte [Implementación de una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2f166-1034">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

