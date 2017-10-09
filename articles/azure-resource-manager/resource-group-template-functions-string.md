---
title: funciones de plantilla de administrador de recursos de aaaAzure - cadena | Documentos de Microsoft
description: Describe hello toouse de funciones en un toowork de plantilla de Azure Resource Manager con cadenas.
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
ms.openlocfilehash: 27f7f6a52cbe4e9915718184433e92ca92999346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="string-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="d1a3d-103">Funciones de cadena para las plantillas de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d1a3d-103">String functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="d1a3d-104">Administrador de recursos proporciona Hola siguientes funciones para trabajar con cadenas:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-104">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="d1a3d-105">base64</span><span class="sxs-lookup"><span data-stu-id="d1a3d-105">base64</span></span>](#base64)
* [<span data-ttu-id="d1a3d-106">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="d1a3d-106">base64ToJson</span></span>](#base64tojson)
* [<span data-ttu-id="d1a3d-107">base64ToString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-107">base64ToString</span></span>](#base64tostring)
* [<span data-ttu-id="d1a3d-108">concat</span><span class="sxs-lookup"><span data-stu-id="d1a3d-108">concat</span></span>](#concat)
* [<span data-ttu-id="d1a3d-109">contains</span><span class="sxs-lookup"><span data-stu-id="d1a3d-109">contains</span></span>](#contains)
* [<span data-ttu-id="d1a3d-110">dataUri</span><span class="sxs-lookup"><span data-stu-id="d1a3d-110">dataUri</span></span>](#datauri)
* [<span data-ttu-id="d1a3d-111">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-111">dataUriToString</span></span>](#datauritostring)
* [<span data-ttu-id="d1a3d-112">empty</span><span class="sxs-lookup"><span data-stu-id="d1a3d-112">empty</span></span>](#empty)
* [<span data-ttu-id="d1a3d-113">endsWith</span><span class="sxs-lookup"><span data-stu-id="d1a3d-113">endsWith</span></span>](#endswith)
* [<span data-ttu-id="d1a3d-114">first</span><span class="sxs-lookup"><span data-stu-id="d1a3d-114">first</span></span>](#first)
* [<span data-ttu-id="d1a3d-115">indexOf</span><span class="sxs-lookup"><span data-stu-id="d1a3d-115">indexOf</span></span>](#indexof)
* [<span data-ttu-id="d1a3d-116">last</span><span class="sxs-lookup"><span data-stu-id="d1a3d-116">last</span></span>](#last)
* [<span data-ttu-id="d1a3d-117">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="d1a3d-117">lastIndexOf</span></span>](#lastindexof)
* [<span data-ttu-id="d1a3d-118">length</span><span class="sxs-lookup"><span data-stu-id="d1a3d-118">length</span></span>](#length)
* [<span data-ttu-id="d1a3d-119">padLeft</span><span class="sxs-lookup"><span data-stu-id="d1a3d-119">padLeft</span></span>](#padleft)
* [<span data-ttu-id="d1a3d-120">replace</span><span class="sxs-lookup"><span data-stu-id="d1a3d-120">replace</span></span>](#replace)
* [<span data-ttu-id="d1a3d-121">skip</span><span class="sxs-lookup"><span data-stu-id="d1a3d-121">skip</span></span>](#skip)
* [<span data-ttu-id="d1a3d-122">split</span><span class="sxs-lookup"><span data-stu-id="d1a3d-122">split</span></span>](#split)
* [<span data-ttu-id="d1a3d-123">startsWith</span><span class="sxs-lookup"><span data-stu-id="d1a3d-123">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="d1a3d-124">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-124">string</span></span>](#string)
* [<span data-ttu-id="d1a3d-125">substring</span><span class="sxs-lookup"><span data-stu-id="d1a3d-125">substring</span></span>](#substring)
* [<span data-ttu-id="d1a3d-126">take</span><span class="sxs-lookup"><span data-stu-id="d1a3d-126">take</span></span>](#take)
* [<span data-ttu-id="d1a3d-127">toLower</span><span class="sxs-lookup"><span data-stu-id="d1a3d-127">toLower</span></span>](#tolower)
* [<span data-ttu-id="d1a3d-128">toUpper</span><span class="sxs-lookup"><span data-stu-id="d1a3d-128">toUpper</span></span>](#toupper)
* [<span data-ttu-id="d1a3d-129">trim</span><span class="sxs-lookup"><span data-stu-id="d1a3d-129">trim</span></span>](#trim)
* [<span data-ttu-id="d1a3d-130">uniqueString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-130">uniqueString</span></span>](#uniquestring)
* [<span data-ttu-id="d1a3d-131">uri</span><span class="sxs-lookup"><span data-stu-id="d1a3d-131">uri</span></span>](#uri)
* [<span data-ttu-id="d1a3d-132">uriComponent</span><span class="sxs-lookup"><span data-stu-id="d1a3d-132">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="d1a3d-133">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-133">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)

<a id="base64" />

## <a name="base64"></a><span data-ttu-id="d1a3d-134">base64</span><span class="sxs-lookup"><span data-stu-id="d1a3d-134">base64</span></span>
`base64(inputString)`

<span data-ttu-id="d1a3d-135">Devuelve Hola representación base64 de la cadena de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-135">Returns hello base64 representation of hello input string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-136">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-136">Parameters</span></span>

| <span data-ttu-id="d1a3d-137">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-137">Parameter</span></span> | <span data-ttu-id="d1a3d-138">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-138">Required</span></span> | <span data-ttu-id="d1a3d-139">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-139">Type</span></span> | <span data-ttu-id="d1a3d-140">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-140">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-141">inputString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-141">inputString</span></span> |<span data-ttu-id="d1a3d-142">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-142">Yes</span></span> |<span data-ttu-id="d1a3d-143">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-143">string</span></span> |<span data-ttu-id="d1a3d-144">Hola tooreturn de valor como una representación base64.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-144">hello value tooreturn as a base64 representation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-145">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-145">Return value</span></span>

<span data-ttu-id="d1a3d-146">Una cadena que contiene la representación en forma de hello en base64.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-146">A string containing hello base64 representation.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-147">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-147">Examples</span></span>

<span data-ttu-id="d1a3d-148">Hola de ejemplo siguiente muestra cómo toouse Hola función base64.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-148">hello following example shows how toouse hello base64 function.</span></span>

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

<span data-ttu-id="d1a3d-149">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-149">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-150">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-150">Name</span></span> | <span data-ttu-id="d1a3d-151">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-151">Type</span></span> | <span data-ttu-id="d1a3d-152">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-152">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-153">base64Output</span><span class="sxs-lookup"><span data-stu-id="d1a3d-153">base64Output</span></span> | <span data-ttu-id="d1a3d-154">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-154">String</span></span> | <span data-ttu-id="d1a3d-155">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="d1a3d-155">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="d1a3d-156">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-156">toStringOutput</span></span> | <span data-ttu-id="d1a3d-157">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-157">String</span></span> | <span data-ttu-id="d1a3d-158">one, two, three</span><span class="sxs-lookup"><span data-stu-id="d1a3d-158">one, two, three</span></span> |
| <span data-ttu-id="d1a3d-159">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-159">toJsonOutput</span></span> | <span data-ttu-id="d1a3d-160">Objeto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-160">Object</span></span> | <span data-ttu-id="d1a3d-161">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="d1a3d-161">{"one": "a", "two": "b"}</span></span> |

<a id="base64tojson" />

## <a name="base64tojson"></a><span data-ttu-id="d1a3d-162">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="d1a3d-162">base64ToJson</span></span>
`base64tojson`

<span data-ttu-id="d1a3d-163">Convierte un objeto JSON de base64 representación tooa.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-163">Converts a base64 representation tooa JSON object.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-164">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-164">Parameters</span></span>

| <span data-ttu-id="d1a3d-165">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-165">Parameter</span></span> | <span data-ttu-id="d1a3d-166">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-166">Required</span></span> | <span data-ttu-id="d1a3d-167">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-167">Type</span></span> | <span data-ttu-id="d1a3d-168">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-168">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-169">base64Value</span><span class="sxs-lookup"><span data-stu-id="d1a3d-169">base64Value</span></span> |<span data-ttu-id="d1a3d-170">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-170">Yes</span></span> |<span data-ttu-id="d1a3d-171">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-171">string</span></span> |<span data-ttu-id="d1a3d-172">Hola base64 representación tooconvert tooa JSON en com.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-172">hello base64 representation tooconvert tooa JSON object.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-173">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-173">Return value</span></span>

<span data-ttu-id="d1a3d-174">Un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-174">A JSON object.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-175">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-175">Examples</span></span>

<span data-ttu-id="d1a3d-176">Hello en el ejemplo siguiente se utiliza hello base64ToJson función tooconvert un valor base64:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-176">hello following example uses hello base64ToJson function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="d1a3d-177">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-177">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-178">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-178">Name</span></span> | <span data-ttu-id="d1a3d-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-179">Type</span></span> | <span data-ttu-id="d1a3d-180">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-180">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-181">base64Output</span><span class="sxs-lookup"><span data-stu-id="d1a3d-181">base64Output</span></span> | <span data-ttu-id="d1a3d-182">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-182">String</span></span> | <span data-ttu-id="d1a3d-183">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="d1a3d-183">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="d1a3d-184">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-184">toStringOutput</span></span> | <span data-ttu-id="d1a3d-185">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-185">String</span></span> | <span data-ttu-id="d1a3d-186">one, two, three</span><span class="sxs-lookup"><span data-stu-id="d1a3d-186">one, two, three</span></span> |
| <span data-ttu-id="d1a3d-187">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-187">toJsonOutput</span></span> | <span data-ttu-id="d1a3d-188">Objeto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-188">Object</span></span> | <span data-ttu-id="d1a3d-189">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="d1a3d-189">{"one": "a", "two": "b"}</span></span> |

<a id="base64tostring" />

## <a name="base64tostring"></a><span data-ttu-id="d1a3d-190">base64ToString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-190">base64ToString</span></span>
`base64ToString(base64Value)`

<span data-ttu-id="d1a3d-191">Convierte una cadena de tooa de representación base64.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-191">Converts a base64 representation tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-192">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-192">Parameters</span></span>

| <span data-ttu-id="d1a3d-193">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-193">Parameter</span></span> | <span data-ttu-id="d1a3d-194">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-194">Required</span></span> | <span data-ttu-id="d1a3d-195">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-195">Type</span></span> | <span data-ttu-id="d1a3d-196">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-196">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-197">base64Value</span><span class="sxs-lookup"><span data-stu-id="d1a3d-197">base64Value</span></span> |<span data-ttu-id="d1a3d-198">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-198">Yes</span></span> |<span data-ttu-id="d1a3d-199">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-199">string</span></span> |<span data-ttu-id="d1a3d-200">cadena de Hello base64 representación tooconvert tooa.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-200">hello base64 representation tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-201">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-201">Return value</span></span>

<span data-ttu-id="d1a3d-202">Convertir de una cadena de hello valor base64.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-202">A string of hello converted base64 value.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-203">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-203">Examples</span></span>

<span data-ttu-id="d1a3d-204">Hello en el ejemplo siguiente se utiliza hello base64ToString función tooconvert un valor base64:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-204">hello following example uses hello base64ToString function tooconvert a base64 value:</span></span>

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

<span data-ttu-id="d1a3d-205">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-205">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-206">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-206">Name</span></span> | <span data-ttu-id="d1a3d-207">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-207">Type</span></span> | <span data-ttu-id="d1a3d-208">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-208">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-209">base64Output</span><span class="sxs-lookup"><span data-stu-id="d1a3d-209">base64Output</span></span> | <span data-ttu-id="d1a3d-210">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-210">String</span></span> | <span data-ttu-id="d1a3d-211">b25lLCB0d28sIHRocmVl</span><span class="sxs-lookup"><span data-stu-id="d1a3d-211">b25lLCB0d28sIHRocmVl</span></span> |
| <span data-ttu-id="d1a3d-212">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-212">toStringOutput</span></span> | <span data-ttu-id="d1a3d-213">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-213">String</span></span> | <span data-ttu-id="d1a3d-214">one, two, three</span><span class="sxs-lookup"><span data-stu-id="d1a3d-214">one, two, three</span></span> |
| <span data-ttu-id="d1a3d-215">toJsonOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-215">toJsonOutput</span></span> | <span data-ttu-id="d1a3d-216">Objeto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-216">Object</span></span> | <span data-ttu-id="d1a3d-217">{"one": "a", "two": "b"}</span><span class="sxs-lookup"><span data-stu-id="d1a3d-217">{"one": "a", "two": "b"}</span></span> |



<a id="concat" />

## <a name="concat"></a><span data-ttu-id="d1a3d-218">concat</span><span class="sxs-lookup"><span data-stu-id="d1a3d-218">concat</span></span>
`concat (arg1, arg2, arg3, ...)`

<span data-ttu-id="d1a3d-219">Combina varios valores de cadena y devuelve la cadena concatenada de hello, o combina varias matrices y devuelve la matriz de hello concatenado.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-219">Combines multiple string values and returns hello concatenated string, or combines multiple arrays and returns hello concatenated array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-220">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-220">Parameters</span></span>

| <span data-ttu-id="d1a3d-221">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-221">Parameter</span></span> | <span data-ttu-id="d1a3d-222">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-222">Required</span></span> | <span data-ttu-id="d1a3d-223">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-223">Type</span></span> | <span data-ttu-id="d1a3d-224">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-224">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-225">arg1</span><span class="sxs-lookup"><span data-stu-id="d1a3d-225">arg1</span></span> |<span data-ttu-id="d1a3d-226">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-226">Yes</span></span> |<span data-ttu-id="d1a3d-227">cadena o matriz</span><span class="sxs-lookup"><span data-stu-id="d1a3d-227">string or array</span></span> |<span data-ttu-id="d1a3d-228">primer valor de Hello para la concatenación.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-228">hello first value for concatenation.</span></span> |
| <span data-ttu-id="d1a3d-229">argumentos adicionales</span><span class="sxs-lookup"><span data-stu-id="d1a3d-229">additional arguments</span></span> |<span data-ttu-id="d1a3d-230">No</span><span class="sxs-lookup"><span data-stu-id="d1a3d-230">No</span></span> |<span data-ttu-id="d1a3d-231">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-231">string</span></span> |<span data-ttu-id="d1a3d-232">Valores adicionales en orden secuencial para la concatenación.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-232">Additional values in sequential order for concatenation.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-233">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-233">Return value</span></span>
<span data-ttu-id="d1a3d-234">Una cadena o matriz de valores concatenados.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-234">A string or array of concatenated values.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-235">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-235">Examples</span></span>

<span data-ttu-id="d1a3d-236">Hola de ejemplo siguiente muestra cómo toocombine dos valores de cadena y devolver una cadena concatenada.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-236">hello following example shows how toocombine two string values and return a concatenated string.</span></span>

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

<span data-ttu-id="d1a3d-237">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-237">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-238">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-238">Name</span></span> | <span data-ttu-id="d1a3d-239">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-239">Type</span></span> | <span data-ttu-id="d1a3d-240">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-240">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-241">concatOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-241">concatOutput</span></span> | <span data-ttu-id="d1a3d-242">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-242">String</span></span> | <span data-ttu-id="d1a3d-243">prefix-5yj4yjf5mbg72</span><span class="sxs-lookup"><span data-stu-id="d1a3d-243">prefix-5yj4yjf5mbg72</span></span> |

<span data-ttu-id="d1a3d-244">Hola de ejemplo siguiente muestra cómo toocombine dos matrices.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-244">hello following example shows how toocombine two arrays.</span></span>

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

<span data-ttu-id="d1a3d-245">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-245">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-246">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-246">Name</span></span> | <span data-ttu-id="d1a3d-247">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-247">Type</span></span> | <span data-ttu-id="d1a3d-248">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-248">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-249">return</span><span class="sxs-lookup"><span data-stu-id="d1a3d-249">return</span></span> | <span data-ttu-id="d1a3d-250">Matriz</span><span class="sxs-lookup"><span data-stu-id="d1a3d-250">Array</span></span> | <span data-ttu-id="d1a3d-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span><span class="sxs-lookup"><span data-stu-id="d1a3d-251">["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"]</span></span> |

<a id="contains" />

## <a name="contains"></a><span data-ttu-id="d1a3d-252">contains</span><span class="sxs-lookup"><span data-stu-id="d1a3d-252">contains</span></span>
`contains (container, itemToFind)`

<span data-ttu-id="d1a3d-253">Comprueba si una matriz contiene un valor, un objeto contiene una clave o una cadena contiene una subcadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-253">Checks whether an array contains a value, an object contains a key, or a string contains a substring.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-254">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-254">Parameters</span></span>

| <span data-ttu-id="d1a3d-255">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-255">Parameter</span></span> | <span data-ttu-id="d1a3d-256">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-256">Required</span></span> | <span data-ttu-id="d1a3d-257">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-257">Type</span></span> | <span data-ttu-id="d1a3d-258">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-258">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-259">container</span><span class="sxs-lookup"><span data-stu-id="d1a3d-259">container</span></span> |<span data-ttu-id="d1a3d-260">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-260">Yes</span></span> |<span data-ttu-id="d1a3d-261">matriz, objeto o cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-261">array, object, or string</span></span> |<span data-ttu-id="d1a3d-262">valor de Hola que contiene Hola valor toofind.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-262">hello value that contains hello value toofind.</span></span> |
| <span data-ttu-id="d1a3d-263">itemToFind</span><span class="sxs-lookup"><span data-stu-id="d1a3d-263">itemToFind</span></span> |<span data-ttu-id="d1a3d-264">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-264">Yes</span></span> |<span data-ttu-id="d1a3d-265">cadena o entero</span><span class="sxs-lookup"><span data-stu-id="d1a3d-265">string or int</span></span> |<span data-ttu-id="d1a3d-266">Hola toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-266">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-267">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-267">Return value</span></span>

<span data-ttu-id="d1a3d-268">**True** si Hola elemento se encuentra; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-268">**True** if hello item is found; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-269">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-269">Examples</span></span>

<span data-ttu-id="d1a3d-270">Hello en el ejemplo siguiente se muestra cómo toouse contiene con tipos diferentes:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-270">hello following example shows how toouse contains with different types:</span></span>

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

<span data-ttu-id="d1a3d-271">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-271">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-272">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-272">Name</span></span> | <span data-ttu-id="d1a3d-273">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-273">Type</span></span> | <span data-ttu-id="d1a3d-274">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-274">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-275">stringTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-275">stringTrue</span></span> | <span data-ttu-id="d1a3d-276">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-276">Bool</span></span> | <span data-ttu-id="d1a3d-277">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-277">True</span></span> |
| <span data-ttu-id="d1a3d-278">stringFalse</span><span class="sxs-lookup"><span data-stu-id="d1a3d-278">stringFalse</span></span> | <span data-ttu-id="d1a3d-279">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-279">Bool</span></span> | <span data-ttu-id="d1a3d-280">False</span><span class="sxs-lookup"><span data-stu-id="d1a3d-280">False</span></span> |
| <span data-ttu-id="d1a3d-281">objectTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-281">objectTrue</span></span> | <span data-ttu-id="d1a3d-282">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-282">Bool</span></span> | <span data-ttu-id="d1a3d-283">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-283">True</span></span> |
| <span data-ttu-id="d1a3d-284">objectFalse</span><span class="sxs-lookup"><span data-stu-id="d1a3d-284">objectFalse</span></span> | <span data-ttu-id="d1a3d-285">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-285">Bool</span></span> | <span data-ttu-id="d1a3d-286">False</span><span class="sxs-lookup"><span data-stu-id="d1a3d-286">False</span></span> |
| <span data-ttu-id="d1a3d-287">arrayTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-287">arrayTrue</span></span> | <span data-ttu-id="d1a3d-288">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-288">Bool</span></span> | <span data-ttu-id="d1a3d-289">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-289">True</span></span> |
| <span data-ttu-id="d1a3d-290">arrayFalse</span><span class="sxs-lookup"><span data-stu-id="d1a3d-290">arrayFalse</span></span> | <span data-ttu-id="d1a3d-291">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-291">Bool</span></span> | <span data-ttu-id="d1a3d-292">False</span><span class="sxs-lookup"><span data-stu-id="d1a3d-292">False</span></span> |

<a id="datauri" />

## <a name="datauri"></a><span data-ttu-id="d1a3d-293">dataUri</span><span class="sxs-lookup"><span data-stu-id="d1a3d-293">dataUri</span></span>
`dataUri(stringToConvert)`

<span data-ttu-id="d1a3d-294">Convierte el valor tooa datos URI.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-294">Converts a value tooa data URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-295">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-295">Parameters</span></span>

| <span data-ttu-id="d1a3d-296">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-296">Parameter</span></span> | <span data-ttu-id="d1a3d-297">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-297">Required</span></span> | <span data-ttu-id="d1a3d-298">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-298">Type</span></span> | <span data-ttu-id="d1a3d-299">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-299">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-300">stringToConvert</span><span class="sxs-lookup"><span data-stu-id="d1a3d-300">stringToConvert</span></span> |<span data-ttu-id="d1a3d-301">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-301">Yes</span></span> |<span data-ttu-id="d1a3d-302">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-302">string</span></span> |<span data-ttu-id="d1a3d-303">Hola valor tooconvert tooa URI de datos.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-303">hello value tooconvert tooa data URI.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-304">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-304">Return value</span></span>

<span data-ttu-id="d1a3d-305">Una cadena con formato de identificador URI de datos.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-305">A string formatted as a data URI.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-306">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-306">Examples</span></span>

<span data-ttu-id="d1a3d-307">Hola ejemplo siguiente convierte datos tooa valor URI y convierte una cadena URI tooa de datos:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-307">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="d1a3d-308">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-308">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-309">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-309">Name</span></span> | <span data-ttu-id="d1a3d-310">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-310">Type</span></span> | <span data-ttu-id="d1a3d-311">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-311">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-312">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-312">dataUriOutput</span></span> | <span data-ttu-id="d1a3d-313">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-313">String</span></span> | <span data-ttu-id="d1a3d-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="d1a3d-314">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="d1a3d-315">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-315">toStringOutput</span></span> | <span data-ttu-id="d1a3d-316">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-316">String</span></span> | <span data-ttu-id="d1a3d-317">Hola mundo.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-317">Hello, World!</span></span> |

<a id="datauritostring" />

## <a name="datauritostring"></a><span data-ttu-id="d1a3d-318">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-318">dataUriToString</span></span>
`dataUriToString(dataUriToConvert)`

<span data-ttu-id="d1a3d-319">Convierte un URI de datos con formato de cadena del valor tooa.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-319">Converts a data URI formatted value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-320">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-320">Parameters</span></span>

| <span data-ttu-id="d1a3d-321">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-321">Parameter</span></span> | <span data-ttu-id="d1a3d-322">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-322">Required</span></span> | <span data-ttu-id="d1a3d-323">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-323">Type</span></span> | <span data-ttu-id="d1a3d-324">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-324">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-325">dataUriToConvert</span><span class="sxs-lookup"><span data-stu-id="d1a3d-325">dataUriToConvert</span></span> |<span data-ttu-id="d1a3d-326">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-326">Yes</span></span> |<span data-ttu-id="d1a3d-327">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-327">string</span></span> |<span data-ttu-id="d1a3d-328">valor de los datos de Hello URI tooconvert.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-328">hello data URI value tooconvert.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-329">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-329">Return value</span></span>

<span data-ttu-id="d1a3d-330">Una cadena que contiene Hola valor convertido.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-330">A string containing hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-331">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-331">Examples</span></span>

<span data-ttu-id="d1a3d-332">Hola ejemplo siguiente convierte datos tooa valor URI y convierte una cadena URI tooa de datos:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-332">hello following example converts a value tooa data URI, and converts a data URI tooa string:</span></span>

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

<span data-ttu-id="d1a3d-333">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-333">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-334">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-334">Name</span></span> | <span data-ttu-id="d1a3d-335">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-335">Type</span></span> | <span data-ttu-id="d1a3d-336">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-336">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-337">dataUriOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-337">dataUriOutput</span></span> | <span data-ttu-id="d1a3d-338">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-338">String</span></span> | <span data-ttu-id="d1a3d-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span><span class="sxs-lookup"><span data-stu-id="d1a3d-339">data:text/plain;charset=utf8;base64,SGVsbG8=</span></span> |
| <span data-ttu-id="d1a3d-340">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-340">toStringOutput</span></span> | <span data-ttu-id="d1a3d-341">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-341">String</span></span> | <span data-ttu-id="d1a3d-342">Hola mundo.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-342">Hello, World!</span></span> |

<a id="empty" /> 

## <a name="empty"></a><span data-ttu-id="d1a3d-343">empty</span><span class="sxs-lookup"><span data-stu-id="d1a3d-343">empty</span></span>
`empty(itemToTest)`

<span data-ttu-id="d1a3d-344">Determina si una matriz, un objeto o una cadena están vacíos.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-344">Determines if an array, object, or string is empty.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-345">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-345">Parameters</span></span>

| <span data-ttu-id="d1a3d-346">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-346">Parameter</span></span> | <span data-ttu-id="d1a3d-347">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-347">Required</span></span> | <span data-ttu-id="d1a3d-348">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-348">Type</span></span> | <span data-ttu-id="d1a3d-349">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-349">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-350">itemToTest</span><span class="sxs-lookup"><span data-stu-id="d1a3d-350">itemToTest</span></span> |<span data-ttu-id="d1a3d-351">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-351">Yes</span></span> |<span data-ttu-id="d1a3d-352">matriz, objeto o cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-352">array, object, or string</span></span> |<span data-ttu-id="d1a3d-353">Hola toocheck valor si está vacía.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-353">hello value toocheck if it is empty.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-354">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-354">Return value</span></span>

<span data-ttu-id="d1a3d-355">Devuelve **True** si el valor de hello está vacía; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-355">Returns **True** if hello value is empty; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-356">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-356">Examples</span></span>

<span data-ttu-id="d1a3d-357">Hola siguiente ejemplo comprueba si una matriz, el objeto y la cadena están vacías.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-357">hello following example checks whether an array, object, and string are empty.</span></span>

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

<span data-ttu-id="d1a3d-358">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-358">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-359">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-359">Name</span></span> | <span data-ttu-id="d1a3d-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-360">Type</span></span> | <span data-ttu-id="d1a3d-361">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-361">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-362">arrayEmpty</span><span class="sxs-lookup"><span data-stu-id="d1a3d-362">arrayEmpty</span></span> | <span data-ttu-id="d1a3d-363">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-363">Bool</span></span> | <span data-ttu-id="d1a3d-364">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-364">True</span></span> |
| <span data-ttu-id="d1a3d-365">objectEmpty</span><span class="sxs-lookup"><span data-stu-id="d1a3d-365">objectEmpty</span></span> | <span data-ttu-id="d1a3d-366">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-366">Bool</span></span> | <span data-ttu-id="d1a3d-367">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-367">True</span></span> |
| <span data-ttu-id="d1a3d-368">stringEmpty</span><span class="sxs-lookup"><span data-stu-id="d1a3d-368">stringEmpty</span></span> | <span data-ttu-id="d1a3d-369">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-369">Bool</span></span> | <span data-ttu-id="d1a3d-370">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-370">True</span></span> |

<a id="endswith" />

## <a name="endswith"></a><span data-ttu-id="d1a3d-371">endsWith</span><span class="sxs-lookup"><span data-stu-id="d1a3d-371">endsWith</span></span>
`endsWith(stringToSearch, stringToFind)`

<span data-ttu-id="d1a3d-372">Determina si una cadena termina con un valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-372">Determines whether a string ends with a value.</span></span> <span data-ttu-id="d1a3d-373">comparación de Hello distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-373">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-374">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-374">Parameters</span></span>

| <span data-ttu-id="d1a3d-375">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-375">Parameter</span></span> | <span data-ttu-id="d1a3d-376">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-376">Required</span></span> | <span data-ttu-id="d1a3d-377">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-377">Type</span></span> | <span data-ttu-id="d1a3d-378">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-378">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-379">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="d1a3d-379">stringToSearch</span></span> |<span data-ttu-id="d1a3d-380">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-380">Yes</span></span> |<span data-ttu-id="d1a3d-381">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-381">string</span></span> |<span data-ttu-id="d1a3d-382">valor de Hola que contiene Hola elemento toofind.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-382">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="d1a3d-383">stringToFind</span><span class="sxs-lookup"><span data-stu-id="d1a3d-383">stringToFind</span></span> |<span data-ttu-id="d1a3d-384">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-384">Yes</span></span> |<span data-ttu-id="d1a3d-385">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-385">string</span></span> |<span data-ttu-id="d1a3d-386">Hola toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-386">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-387">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-387">Return value</span></span>

<span data-ttu-id="d1a3d-388">**True** si último carácter de Hola o caracteres de la cadena de hello coincide con el valor de hello; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-388">**True** if hello last character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-389">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-389">Examples</span></span>

<span data-ttu-id="d1a3d-390">Hola de ejemplo siguiente muestra cómo toouse Hola startsWith y endsWith funciones:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-390">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="d1a3d-391">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-391">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-392">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-392">Name</span></span> | <span data-ttu-id="d1a3d-393">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-393">Type</span></span> | <span data-ttu-id="d1a3d-394">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-394">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-395">startsTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-395">startsTrue</span></span> | <span data-ttu-id="d1a3d-396">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-396">Bool</span></span> | <span data-ttu-id="d1a3d-397">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-397">True</span></span> |
| <span data-ttu-id="d1a3d-398">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-398">startsCapTrue</span></span> | <span data-ttu-id="d1a3d-399">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-399">Bool</span></span> | <span data-ttu-id="d1a3d-400">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-400">True</span></span> |
| <span data-ttu-id="d1a3d-401">startsFalse</span><span class="sxs-lookup"><span data-stu-id="d1a3d-401">startsFalse</span></span> | <span data-ttu-id="d1a3d-402">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-402">Bool</span></span> | <span data-ttu-id="d1a3d-403">False</span><span class="sxs-lookup"><span data-stu-id="d1a3d-403">False</span></span> |
| <span data-ttu-id="d1a3d-404">endsTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-404">endsTrue</span></span> | <span data-ttu-id="d1a3d-405">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-405">Bool</span></span> | <span data-ttu-id="d1a3d-406">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-406">True</span></span> |
| <span data-ttu-id="d1a3d-407">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-407">endsCapTrue</span></span> | <span data-ttu-id="d1a3d-408">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-408">Bool</span></span> | <span data-ttu-id="d1a3d-409">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-409">True</span></span> |
| <span data-ttu-id="d1a3d-410">endsFalse</span><span class="sxs-lookup"><span data-stu-id="d1a3d-410">endsFalse</span></span> | <span data-ttu-id="d1a3d-411">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-411">Bool</span></span> | <span data-ttu-id="d1a3d-412">False</span><span class="sxs-lookup"><span data-stu-id="d1a3d-412">False</span></span> |

<a id="first" />

## <a name="first"></a><span data-ttu-id="d1a3d-413">first</span><span class="sxs-lookup"><span data-stu-id="d1a3d-413">first</span></span>
`first(arg1)`

<span data-ttu-id="d1a3d-414">Devuelve Hola primer carácter de la cadena de Hola o el primer elemento de matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-414">Returns hello first character of hello string, or first element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-415">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-415">Parameters</span></span>

| <span data-ttu-id="d1a3d-416">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-416">Parameter</span></span> | <span data-ttu-id="d1a3d-417">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-417">Required</span></span> | <span data-ttu-id="d1a3d-418">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-418">Type</span></span> | <span data-ttu-id="d1a3d-419">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-419">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-420">arg1</span><span class="sxs-lookup"><span data-stu-id="d1a3d-420">arg1</span></span> |<span data-ttu-id="d1a3d-421">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-421">Yes</span></span> |<span data-ttu-id="d1a3d-422">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-422">array or string</span></span> |<span data-ttu-id="d1a3d-423">Hola valor tooretrieve Hola primer elemento o carácter.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-423">hello value tooretrieve hello first element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-424">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-424">Return value</span></span>

<span data-ttu-id="d1a3d-425">Cadena del primer carácter de Hola o tipo hello (string, int, matriz u objeto) del primer elemento de hello en una matriz.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-425">A string of hello first character, or hello type (string, int, array, or object) of hello first element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-426">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-426">Examples</span></span>

<span data-ttu-id="d1a3d-427">Hello en el ejemplo siguiente se muestra cómo toouse Hola primera función con una matriz y una cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-427">hello following example shows how toouse hello first function with an array and string.</span></span>

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

<span data-ttu-id="d1a3d-428">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-428">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-429">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-429">Name</span></span> | <span data-ttu-id="d1a3d-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-430">Type</span></span> | <span data-ttu-id="d1a3d-431">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-431">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-432">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-432">arrayOutput</span></span> | <span data-ttu-id="d1a3d-433">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-433">String</span></span> | <span data-ttu-id="d1a3d-434">one</span><span class="sxs-lookup"><span data-stu-id="d1a3d-434">one</span></span> |
| <span data-ttu-id="d1a3d-435">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-435">stringOutput</span></span> | <span data-ttu-id="d1a3d-436">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-436">String</span></span> | <span data-ttu-id="d1a3d-437">O</span><span class="sxs-lookup"><span data-stu-id="d1a3d-437">O</span></span> |

<a id="indexof" />

## <a name="indexof"></a><span data-ttu-id="d1a3d-438">indexOf</span><span class="sxs-lookup"><span data-stu-id="d1a3d-438">indexOf</span></span>
`indexOf(stringToSearch, stringToFind)`

<span data-ttu-id="d1a3d-439">Devuelve Hola primera posición de un valor dentro de una cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-439">Returns hello first position of a value within a string.</span></span> <span data-ttu-id="d1a3d-440">comparación de Hello distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-440">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-441">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-441">Parameters</span></span>

| <span data-ttu-id="d1a3d-442">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-442">Parameter</span></span> | <span data-ttu-id="d1a3d-443">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-443">Required</span></span> | <span data-ttu-id="d1a3d-444">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-444">Type</span></span> | <span data-ttu-id="d1a3d-445">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-445">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-446">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="d1a3d-446">stringToSearch</span></span> |<span data-ttu-id="d1a3d-447">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-447">Yes</span></span> |<span data-ttu-id="d1a3d-448">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-448">string</span></span> |<span data-ttu-id="d1a3d-449">valor de Hola que contiene Hola elemento toofind.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-449">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="d1a3d-450">stringToFind</span><span class="sxs-lookup"><span data-stu-id="d1a3d-450">stringToFind</span></span> |<span data-ttu-id="d1a3d-451">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-451">Yes</span></span> |<span data-ttu-id="d1a3d-452">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-452">string</span></span> |<span data-ttu-id="d1a3d-453">Hola toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-453">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-454">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-454">Return value</span></span>

<span data-ttu-id="d1a3d-455">Un entero que representa la posición de Hola de hello elemento toofind.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-455">An integer that represents hello position of hello item toofind.</span></span> <span data-ttu-id="d1a3d-456">valor de Hello está basado en cero.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-456">hello value is zero-based.</span></span> <span data-ttu-id="d1a3d-457">Si no se encuentra el elemento de hello, se devuelve -1.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-457">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-458">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-458">Examples</span></span>

<span data-ttu-id="d1a3d-459">Hola de ejemplo siguiente muestra cómo toouse Hola indexOf y lastIndexOf funciones:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-459">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="d1a3d-460">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-460">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-461">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-461">Name</span></span> | <span data-ttu-id="d1a3d-462">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-462">Type</span></span> | <span data-ttu-id="d1a3d-463">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-463">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-464">firstT</span><span class="sxs-lookup"><span data-stu-id="d1a3d-464">firstT</span></span> | <span data-ttu-id="d1a3d-465">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-465">Int</span></span> | <span data-ttu-id="d1a3d-466">0</span><span class="sxs-lookup"><span data-stu-id="d1a3d-466">0</span></span> |
| <span data-ttu-id="d1a3d-467">lastT</span><span class="sxs-lookup"><span data-stu-id="d1a3d-467">lastT</span></span> | <span data-ttu-id="d1a3d-468">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-468">Int</span></span> | <span data-ttu-id="d1a3d-469">3</span><span class="sxs-lookup"><span data-stu-id="d1a3d-469">3</span></span> |
| <span data-ttu-id="d1a3d-470">firstString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-470">firstString</span></span> | <span data-ttu-id="d1a3d-471">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-471">Int</span></span> | <span data-ttu-id="d1a3d-472">2</span><span class="sxs-lookup"><span data-stu-id="d1a3d-472">2</span></span> |
| <span data-ttu-id="d1a3d-473">lastString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-473">lastString</span></span> | <span data-ttu-id="d1a3d-474">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-474">Int</span></span> | <span data-ttu-id="d1a3d-475">0</span><span class="sxs-lookup"><span data-stu-id="d1a3d-475">0</span></span> |
| <span data-ttu-id="d1a3d-476">notFound</span><span class="sxs-lookup"><span data-stu-id="d1a3d-476">notFound</span></span> | <span data-ttu-id="d1a3d-477">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-477">Int</span></span> | <span data-ttu-id="d1a3d-478">-1</span><span class="sxs-lookup"><span data-stu-id="d1a3d-478">-1</span></span> |

<a id="last" />

## <a name="last"></a><span data-ttu-id="d1a3d-479">last</span><span class="sxs-lookup"><span data-stu-id="d1a3d-479">last</span></span>
`last (arg1)`

<span data-ttu-id="d1a3d-480">Devuelve el último carácter de la cadena de Hola o último elemento de matriz de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-480">Returns last character of hello string, or hello last element of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-481">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-481">Parameters</span></span>

| <span data-ttu-id="d1a3d-482">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-482">Parameter</span></span> | <span data-ttu-id="d1a3d-483">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-483">Required</span></span> | <span data-ttu-id="d1a3d-484">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-484">Type</span></span> | <span data-ttu-id="d1a3d-485">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-485">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-486">arg1</span><span class="sxs-lookup"><span data-stu-id="d1a3d-486">arg1</span></span> |<span data-ttu-id="d1a3d-487">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-487">Yes</span></span> |<span data-ttu-id="d1a3d-488">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-488">array or string</span></span> |<span data-ttu-id="d1a3d-489">Hola value tooretrieve Hola última (elemento) o carácter.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-489">hello value tooretrieve hello last element or character.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-490">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-490">Return value</span></span>

<span data-ttu-id="d1a3d-491">Cadena del último carácter de Hola o tipo hello (string, int, matriz u objeto) del último elemento de hello en una matriz.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-491">A string of hello last character, or hello type (string, int, array, or object) of hello last element in an array.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-492">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-492">Examples</span></span>

<span data-ttu-id="d1a3d-493">Hello en el ejemplo siguiente se muestra cómo toouse Hola última función con una matriz y una cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-493">hello following example shows how toouse hello last function with an array and string.</span></span>

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

<span data-ttu-id="d1a3d-494">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-494">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-495">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-495">Name</span></span> | <span data-ttu-id="d1a3d-496">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-496">Type</span></span> | <span data-ttu-id="d1a3d-497">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-497">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-498">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-498">arrayOutput</span></span> | <span data-ttu-id="d1a3d-499">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-499">String</span></span> | <span data-ttu-id="d1a3d-500">three</span><span class="sxs-lookup"><span data-stu-id="d1a3d-500">three</span></span> |
| <span data-ttu-id="d1a3d-501">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-501">stringOutput</span></span> | <span data-ttu-id="d1a3d-502">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-502">String</span></span> | <span data-ttu-id="d1a3d-503">e</span><span class="sxs-lookup"><span data-stu-id="d1a3d-503">e</span></span> |

<a id="lastindexof" />

## <a name="lastindexof"></a><span data-ttu-id="d1a3d-504">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="d1a3d-504">lastIndexOf</span></span>
`lastIndexOf(stringToSearch, stringToFind)`

<span data-ttu-id="d1a3d-505">Devuelve Hola última posición de un valor dentro de una cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-505">Returns hello last position of a value within a string.</span></span> <span data-ttu-id="d1a3d-506">comparación de Hello distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-506">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-507">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-507">Parameters</span></span>

| <span data-ttu-id="d1a3d-508">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-508">Parameter</span></span> | <span data-ttu-id="d1a3d-509">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-509">Required</span></span> | <span data-ttu-id="d1a3d-510">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-510">Type</span></span> | <span data-ttu-id="d1a3d-511">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-511">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-512">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="d1a3d-512">stringToSearch</span></span> |<span data-ttu-id="d1a3d-513">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-513">Yes</span></span> |<span data-ttu-id="d1a3d-514">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-514">string</span></span> |<span data-ttu-id="d1a3d-515">valor de Hola que contiene Hola elemento toofind.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-515">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="d1a3d-516">stringToFind</span><span class="sxs-lookup"><span data-stu-id="d1a3d-516">stringToFind</span></span> |<span data-ttu-id="d1a3d-517">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-517">Yes</span></span> |<span data-ttu-id="d1a3d-518">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-518">string</span></span> |<span data-ttu-id="d1a3d-519">Hola toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-519">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-520">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-520">Return value</span></span>

<span data-ttu-id="d1a3d-521">Un entero que representa la última posición de Hola de hello elemento toofind.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-521">An integer that represents hello last position of hello item toofind.</span></span> <span data-ttu-id="d1a3d-522">valor de Hello está basado en cero.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-522">hello value is zero-based.</span></span> <span data-ttu-id="d1a3d-523">Si no se encuentra el elemento de hello, se devuelve -1.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-523">If hello item is not found, -1 is returned.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-524">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-524">Examples</span></span>

<span data-ttu-id="d1a3d-525">Hola de ejemplo siguiente muestra cómo toouse Hola indexOf y lastIndexOf funciones:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-525">hello following example shows how toouse hello indexOf and lastIndexOf functions:</span></span>

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

<span data-ttu-id="d1a3d-526">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-526">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-527">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-527">Name</span></span> | <span data-ttu-id="d1a3d-528">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-528">Type</span></span> | <span data-ttu-id="d1a3d-529">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-529">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-530">firstT</span><span class="sxs-lookup"><span data-stu-id="d1a3d-530">firstT</span></span> | <span data-ttu-id="d1a3d-531">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-531">Int</span></span> | <span data-ttu-id="d1a3d-532">0</span><span class="sxs-lookup"><span data-stu-id="d1a3d-532">0</span></span> |
| <span data-ttu-id="d1a3d-533">lastT</span><span class="sxs-lookup"><span data-stu-id="d1a3d-533">lastT</span></span> | <span data-ttu-id="d1a3d-534">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-534">Int</span></span> | <span data-ttu-id="d1a3d-535">3</span><span class="sxs-lookup"><span data-stu-id="d1a3d-535">3</span></span> |
| <span data-ttu-id="d1a3d-536">firstString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-536">firstString</span></span> | <span data-ttu-id="d1a3d-537">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-537">Int</span></span> | <span data-ttu-id="d1a3d-538">2</span><span class="sxs-lookup"><span data-stu-id="d1a3d-538">2</span></span> |
| <span data-ttu-id="d1a3d-539">lastString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-539">lastString</span></span> | <span data-ttu-id="d1a3d-540">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-540">Int</span></span> | <span data-ttu-id="d1a3d-541">0</span><span class="sxs-lookup"><span data-stu-id="d1a3d-541">0</span></span> |
| <span data-ttu-id="d1a3d-542">notFound</span><span class="sxs-lookup"><span data-stu-id="d1a3d-542">notFound</span></span> | <span data-ttu-id="d1a3d-543">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-543">Int</span></span> | <span data-ttu-id="d1a3d-544">-1</span><span class="sxs-lookup"><span data-stu-id="d1a3d-544">-1</span></span> |

<a id="length" />

## <a name="length"></a><span data-ttu-id="d1a3d-545">length</span><span class="sxs-lookup"><span data-stu-id="d1a3d-545">length</span></span>
`length(string)`

<span data-ttu-id="d1a3d-546">Devuelve el número de Hola de caracteres en una cadena o elementos de una matriz.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-546">Returns hello number of characters in a string, or elements in an array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-547">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-547">Parameters</span></span>

| <span data-ttu-id="d1a3d-548">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-548">Parameter</span></span> | <span data-ttu-id="d1a3d-549">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-549">Required</span></span> | <span data-ttu-id="d1a3d-550">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-550">Type</span></span> | <span data-ttu-id="d1a3d-551">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-551">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-552">arg1</span><span class="sxs-lookup"><span data-stu-id="d1a3d-552">arg1</span></span> |<span data-ttu-id="d1a3d-553">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-553">Yes</span></span> |<span data-ttu-id="d1a3d-554">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-554">array or string</span></span> |<span data-ttu-id="d1a3d-555">Hola toouse de matriz para obtener el número de Hola de elementos u Hola toouse de cadena para obtener el número de Hola de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-555">hello array toouse for getting hello number of elements, or hello string toouse for getting hello number of characters.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-556">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-556">Return value</span></span>

<span data-ttu-id="d1a3d-557">Un entero.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-557">An int.</span></span> 

### <a name="examples"></a><span data-ttu-id="d1a3d-558">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-558">Examples</span></span>

<span data-ttu-id="d1a3d-559">Hola siguiente ejemplo se muestra cómo toouse longitud con una matriz y la cadena:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-559">hello following example shows how toouse length with an array and string:</span></span>

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

<span data-ttu-id="d1a3d-560">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-560">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-561">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-561">Name</span></span> | <span data-ttu-id="d1a3d-562">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-562">Type</span></span> | <span data-ttu-id="d1a3d-563">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-563">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-564">arrayLength</span><span class="sxs-lookup"><span data-stu-id="d1a3d-564">arrayLength</span></span> | <span data-ttu-id="d1a3d-565">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-565">Int</span></span> | <span data-ttu-id="d1a3d-566">3</span><span class="sxs-lookup"><span data-stu-id="d1a3d-566">3</span></span> |
| <span data-ttu-id="d1a3d-567">stringLength</span><span class="sxs-lookup"><span data-stu-id="d1a3d-567">stringLength</span></span> | <span data-ttu-id="d1a3d-568">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-568">Int</span></span> | <span data-ttu-id="d1a3d-569">13</span><span class="sxs-lookup"><span data-stu-id="d1a3d-569">13</span></span> |

<a id="padleft" />

## <a name="padleft"></a><span data-ttu-id="d1a3d-570">padLeft</span><span class="sxs-lookup"><span data-stu-id="d1a3d-570">padLeft</span></span>
`padLeft(valueToPad, totalLength, paddingCharacter)`

<span data-ttu-id="d1a3d-571">Devuelve una cadena alineada a la derecha agregando caracteres toohello izquierda hasta alcanzar la longitud total especificada Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-571">Returns a right-aligned string by adding characters toohello left until reaching hello total specified length.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-572">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-572">Parameters</span></span>

| <span data-ttu-id="d1a3d-573">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-573">Parameter</span></span> | <span data-ttu-id="d1a3d-574">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-574">Required</span></span> | <span data-ttu-id="d1a3d-575">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-575">Type</span></span> | <span data-ttu-id="d1a3d-576">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-576">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-577">valueToPad</span><span class="sxs-lookup"><span data-stu-id="d1a3d-577">valueToPad</span></span> |<span data-ttu-id="d1a3d-578">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-578">Yes</span></span> |<span data-ttu-id="d1a3d-579">cadena o entero</span><span class="sxs-lookup"><span data-stu-id="d1a3d-579">string or int</span></span> |<span data-ttu-id="d1a3d-580">Hola valor tooright-alinear.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-580">hello value tooright-align.</span></span> |
| <span data-ttu-id="d1a3d-581">totalLength</span><span class="sxs-lookup"><span data-stu-id="d1a3d-581">totalLength</span></span> |<span data-ttu-id="d1a3d-582">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-582">Yes</span></span> |<span data-ttu-id="d1a3d-583">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-583">int</span></span> |<span data-ttu-id="d1a3d-584">número total de Hola de caracteres de hello devuelve la cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-584">hello total number of characters in hello returned string.</span></span> |
| <span data-ttu-id="d1a3d-585">paddingCharacter</span><span class="sxs-lookup"><span data-stu-id="d1a3d-585">paddingCharacter</span></span> |<span data-ttu-id="d1a3d-586">No</span><span class="sxs-lookup"><span data-stu-id="d1a3d-586">No</span></span> |<span data-ttu-id="d1a3d-587">carácter individual</span><span class="sxs-lookup"><span data-stu-id="d1a3d-587">single character</span></span> |<span data-ttu-id="d1a3d-588">Hola toouse de caracteres de relleno izquierda hasta alcanza la longitud total de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-588">hello character toouse for left-padding until hello total length is reached.</span></span> <span data-ttu-id="d1a3d-589">valor predeterminado de Hello es un espacio.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-589">hello default value is a space.</span></span> |

<span data-ttu-id="d1a3d-590">Si cadena original hello es mayor que el número de Hola de toopad caracteres, no se agrega ningún carácter.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-590">If hello original string is longer than hello number of characters toopad, no characters are added.</span></span>

### <a name="return-value"></a><span data-ttu-id="d1a3d-591">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-591">Return value</span></span>

<span data-ttu-id="d1a3d-592">Una cadena con Hola mínimo número de caracteres especificados.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-592">A string with at least hello number of specified characters.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-593">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-593">Examples</span></span>

<span data-ttu-id="d1a3d-594">Hola de ejemplo siguiente muestra cómo toopad Hola valor del parámetro proporcionado por el usuario mediante la adición de hello carácter cero hasta que alcanza el número total de Hola de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-594">hello following example shows how toopad hello user-provided parameter value by adding hello zero character until it reaches hello total number of characters.</span></span> 

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

<span data-ttu-id="d1a3d-595">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-595">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-596">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-596">Name</span></span> | <span data-ttu-id="d1a3d-597">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-597">Type</span></span> | <span data-ttu-id="d1a3d-598">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-598">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-599">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-599">stringOutput</span></span> | <span data-ttu-id="d1a3d-600">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-600">String</span></span> | <span data-ttu-id="d1a3d-601">0000000123</span><span class="sxs-lookup"><span data-stu-id="d1a3d-601">0000000123</span></span> |

<a id="replace" />

## <a name="replace"></a><span data-ttu-id="d1a3d-602">replace</span><span class="sxs-lookup"><span data-stu-id="d1a3d-602">replace</span></span>
`replace(originalString, oldString, newString)`

<span data-ttu-id="d1a3d-603">Devuelve una nueva cadena con todas las instancias de una cadena reemplazadas por otra cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-603">Returns a new string with all instances of one string replaced by another string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-604">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-604">Parameters</span></span>

| <span data-ttu-id="d1a3d-605">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-605">Parameter</span></span> | <span data-ttu-id="d1a3d-606">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-606">Required</span></span> | <span data-ttu-id="d1a3d-607">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-607">Type</span></span> | <span data-ttu-id="d1a3d-608">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-608">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-609">originalString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-609">originalString</span></span> |<span data-ttu-id="d1a3d-610">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-610">Yes</span></span> |<span data-ttu-id="d1a3d-611">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-611">string</span></span> |<span data-ttu-id="d1a3d-612">valor de Hola que tiene todas las instancias de una cadena que se reemplaza por otra cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-612">hello value that has all instances of one string replaced by another string.</span></span> |
| <span data-ttu-id="d1a3d-613">oldString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-613">oldString</span></span> |<span data-ttu-id="d1a3d-614">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-614">Yes</span></span> |<span data-ttu-id="d1a3d-615">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-615">string</span></span> |<span data-ttu-id="d1a3d-616">cadena de Hello toobe quitado de la cadena original Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-616">hello string toobe removed from hello original string.</span></span> |
| <span data-ttu-id="d1a3d-617">newString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-617">newString</span></span> |<span data-ttu-id="d1a3d-618">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-618">Yes</span></span> |<span data-ttu-id="d1a3d-619">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-619">string</span></span> |<span data-ttu-id="d1a3d-620">Hola tooadd de cadena en lugar de hello quita la cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-620">hello string tooadd in place of hello removed string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-621">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-621">Return value</span></span>

<span data-ttu-id="d1a3d-622">Una cadena con hello reemplaza caracteres.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-622">A string with hello replaced characters.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-623">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-623">Examples</span></span>

<span data-ttu-id="d1a3d-624">Hola de ejemplo siguiente muestra cómo tooremove todos los guiones de cadena proporcionado por el usuario de Hola y cómo tooreplace parte del programa Hola de cadena con otra cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-624">hello following example shows how tooremove all dashes from hello user-provided string, and how tooreplace part of hello string with another string.</span></span>

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

<span data-ttu-id="d1a3d-625">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-625">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-626">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-626">Name</span></span> | <span data-ttu-id="d1a3d-627">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-627">Type</span></span> | <span data-ttu-id="d1a3d-628">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-628">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-629">firstOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-629">firstOutput</span></span> | <span data-ttu-id="d1a3d-630">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-630">String</span></span> | <span data-ttu-id="d1a3d-631">1231231234</span><span class="sxs-lookup"><span data-stu-id="d1a3d-631">1231231234</span></span> |
| <span data-ttu-id="d1a3d-632">secodeOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-632">secodeOutput</span></span> | <span data-ttu-id="d1a3d-633">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-633">String</span></span> | <span data-ttu-id="d1a3d-634">123-123-xxxx</span><span class="sxs-lookup"><span data-stu-id="d1a3d-634">123-123-xxxx</span></span> |

<a id="skip" />

## <a name="skip"></a><span data-ttu-id="d1a3d-635">skip</span><span class="sxs-lookup"><span data-stu-id="d1a3d-635">skip</span></span>
`skip(originalValue, numberToSkip)`

<span data-ttu-id="d1a3d-636">Devuelve una cadena con todos los caracteres de hello después Hola un número especificado de caracteres o una matriz con todos los elementos de hello después Hola un número especificado de elementos.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-636">Returns a string with all hello characters after hello specified number of characters, or an array with all hello elements after hello specified number of elements.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-637">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-637">Parameters</span></span>

| <span data-ttu-id="d1a3d-638">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-638">Parameter</span></span> | <span data-ttu-id="d1a3d-639">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-639">Required</span></span> | <span data-ttu-id="d1a3d-640">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-640">Type</span></span> | <span data-ttu-id="d1a3d-641">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-641">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-642">originalValue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-642">originalValue</span></span> |<span data-ttu-id="d1a3d-643">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-643">Yes</span></span> |<span data-ttu-id="d1a3d-644">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-644">array or string</span></span> |<span data-ttu-id="d1a3d-645">Hola toouse de matriz o de cadena para pasar por alto.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-645">hello array or string toouse for skipping.</span></span> |
| <span data-ttu-id="d1a3d-646">numberToSkip</span><span class="sxs-lookup"><span data-stu-id="d1a3d-646">numberToSkip</span></span> |<span data-ttu-id="d1a3d-647">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-647">Yes</span></span> |<span data-ttu-id="d1a3d-648">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-648">int</span></span> |<span data-ttu-id="d1a3d-649">número de Hola de tooskip elementos o caracteres.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-649">hello number of elements or characters tooskip.</span></span> <span data-ttu-id="d1a3d-650">Si este valor es 0 o menos, todos los elementos de Hola o se devuelven los caracteres en valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-650">If this value is 0 or less, all hello elements or characters in hello value are returned.</span></span> <span data-ttu-id="d1a3d-651">Si es mayor que la longitud de cadena o matriz de Hola Hola, se devuelve una matriz vacía o una cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-651">If it is larger than hello length of hello array or string, an empty array or string is returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-652">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-652">Return value</span></span>

<span data-ttu-id="d1a3d-653">Una matriz o cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-653">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-654">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-654">Examples</span></span>

<span data-ttu-id="d1a3d-655">Hola siguiendo el ejemplo omite Hola número especificado de elementos de matriz de Hola y Hola especifica el número de caracteres en una cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-655">hello following example skips hello specified number of elements in hello array, and hello specified number of characters in a string.</span></span>

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

<span data-ttu-id="d1a3d-656">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-656">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-657">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-657">Name</span></span> | <span data-ttu-id="d1a3d-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-658">Type</span></span> | <span data-ttu-id="d1a3d-659">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-659">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-660">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-660">arrayOutput</span></span> | <span data-ttu-id="d1a3d-661">Matriz</span><span class="sxs-lookup"><span data-stu-id="d1a3d-661">Array</span></span> | <span data-ttu-id="d1a3d-662">["three"]</span><span class="sxs-lookup"><span data-stu-id="d1a3d-662">["three"]</span></span> |
| <span data-ttu-id="d1a3d-663">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-663">stringOutput</span></span> | <span data-ttu-id="d1a3d-664">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-664">String</span></span> | <span data-ttu-id="d1a3d-665">two three</span><span class="sxs-lookup"><span data-stu-id="d1a3d-665">two three</span></span> |

<a id="split" />

## <a name="split"></a><span data-ttu-id="d1a3d-666">split</span><span class="sxs-lookup"><span data-stu-id="d1a3d-666">split</span></span>
`split(inputString, delimiter)`

<span data-ttu-id="d1a3d-667">Devuelve una matriz de cadenas que contiene las subcadenas de Hola Hola la cadena de entrada que está delimitadas por hello Especifica delimitadores.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-667">Returns an array of strings that contains hello substrings of hello input string that are delimited by hello specified delimiters.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-668">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-668">Parameters</span></span>

| <span data-ttu-id="d1a3d-669">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-669">Parameter</span></span> | <span data-ttu-id="d1a3d-670">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-670">Required</span></span> | <span data-ttu-id="d1a3d-671">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-671">Type</span></span> | <span data-ttu-id="d1a3d-672">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-672">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-673">inputString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-673">inputString</span></span> |<span data-ttu-id="d1a3d-674">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-674">Yes</span></span> |<span data-ttu-id="d1a3d-675">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-675">string</span></span> |<span data-ttu-id="d1a3d-676">Hola toosplit de cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-676">hello string toosplit.</span></span> |
| <span data-ttu-id="d1a3d-677">delimiter</span><span class="sxs-lookup"><span data-stu-id="d1a3d-677">delimiter</span></span> |<span data-ttu-id="d1a3d-678">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-678">Yes</span></span> |<span data-ttu-id="d1a3d-679">cadena o matriz de cadenas</span><span class="sxs-lookup"><span data-stu-id="d1a3d-679">string or array of strings</span></span> |<span data-ttu-id="d1a3d-680">Hola toouse delimitador para dividir la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-680">hello delimiter toouse for splitting hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-681">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-681">Return value</span></span>

<span data-ttu-id="d1a3d-682">Una matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-682">An array of strings.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-683">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-683">Examples</span></span>

<span data-ttu-id="d1a3d-684">Hello en el ejemplo siguiente se divide Hola la cadena de entrada con una coma y con una coma o un punto y coma.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-684">hello following example splits hello input string with a comma, and with either a comma or a semi-colon.</span></span>

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

<span data-ttu-id="d1a3d-685">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-685">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-686">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-686">Name</span></span> | <span data-ttu-id="d1a3d-687">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-687">Type</span></span> | <span data-ttu-id="d1a3d-688">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-688">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-689">firstOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-689">firstOutput</span></span> | <span data-ttu-id="d1a3d-690">Matriz</span><span class="sxs-lookup"><span data-stu-id="d1a3d-690">Array</span></span> | <span data-ttu-id="d1a3d-691">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="d1a3d-691">["one", "two", "three"]</span></span> |
| <span data-ttu-id="d1a3d-692">secondOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-692">secondOutput</span></span> | <span data-ttu-id="d1a3d-693">Matriz</span><span class="sxs-lookup"><span data-stu-id="d1a3d-693">Array</span></span> | <span data-ttu-id="d1a3d-694">["one", "two", "three"]</span><span class="sxs-lookup"><span data-stu-id="d1a3d-694">["one", "two", "three"]</span></span> |

<a id="startswith" />

## <a name="startswith"></a><span data-ttu-id="d1a3d-695">startsWith</span><span class="sxs-lookup"><span data-stu-id="d1a3d-695">startsWith</span></span>
`startsWith(stringToSearch, stringToFind)`

<span data-ttu-id="d1a3d-696">Determina si una cadena empieza con un valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-696">Determines whether a string starts with a value.</span></span> <span data-ttu-id="d1a3d-697">comparación de Hello distingue entre mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-697">hello comparison is case-insensitive.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-698">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-698">Parameters</span></span>

| <span data-ttu-id="d1a3d-699">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-699">Parameter</span></span> | <span data-ttu-id="d1a3d-700">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-700">Required</span></span> | <span data-ttu-id="d1a3d-701">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-701">Type</span></span> | <span data-ttu-id="d1a3d-702">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-702">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-703">stringToSearch</span><span class="sxs-lookup"><span data-stu-id="d1a3d-703">stringToSearch</span></span> |<span data-ttu-id="d1a3d-704">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-704">Yes</span></span> |<span data-ttu-id="d1a3d-705">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-705">string</span></span> |<span data-ttu-id="d1a3d-706">valor de Hola que contiene Hola elemento toofind.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-706">hello value that contains hello item toofind.</span></span> |
| <span data-ttu-id="d1a3d-707">stringToFind</span><span class="sxs-lookup"><span data-stu-id="d1a3d-707">stringToFind</span></span> |<span data-ttu-id="d1a3d-708">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-708">Yes</span></span> |<span data-ttu-id="d1a3d-709">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-709">string</span></span> |<span data-ttu-id="d1a3d-710">Hola toofind de valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-710">hello value toofind.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-711">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-711">Return value</span></span>

<span data-ttu-id="d1a3d-712">**True** si Hola primer carácter o caracteres de la cadena de hello coincide con el valor de hello; en caso contrario, **False**.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-712">**True** if hello first character or characters of hello string match hello value; otherwise, **False**.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-713">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-713">Examples</span></span>

<span data-ttu-id="d1a3d-714">Hola de ejemplo siguiente muestra cómo toouse Hola startsWith y endsWith funciones:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-714">hello following example shows how toouse hello startsWith and endsWith functions:</span></span>

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

<span data-ttu-id="d1a3d-715">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-715">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-716">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-716">Name</span></span> | <span data-ttu-id="d1a3d-717">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-717">Type</span></span> | <span data-ttu-id="d1a3d-718">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-718">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-719">startsTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-719">startsTrue</span></span> | <span data-ttu-id="d1a3d-720">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-720">Bool</span></span> | <span data-ttu-id="d1a3d-721">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-721">True</span></span> |
| <span data-ttu-id="d1a3d-722">startsCapTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-722">startsCapTrue</span></span> | <span data-ttu-id="d1a3d-723">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-723">Bool</span></span> | <span data-ttu-id="d1a3d-724">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-724">True</span></span> |
| <span data-ttu-id="d1a3d-725">startsFalse</span><span class="sxs-lookup"><span data-stu-id="d1a3d-725">startsFalse</span></span> | <span data-ttu-id="d1a3d-726">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-726">Bool</span></span> | <span data-ttu-id="d1a3d-727">False</span><span class="sxs-lookup"><span data-stu-id="d1a3d-727">False</span></span> |
| <span data-ttu-id="d1a3d-728">endsTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-728">endsTrue</span></span> | <span data-ttu-id="d1a3d-729">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-729">Bool</span></span> | <span data-ttu-id="d1a3d-730">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-730">True</span></span> |
| <span data-ttu-id="d1a3d-731">endsCapTrue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-731">endsCapTrue</span></span> | <span data-ttu-id="d1a3d-732">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-732">Bool</span></span> | <span data-ttu-id="d1a3d-733">True</span><span class="sxs-lookup"><span data-stu-id="d1a3d-733">True</span></span> |
| <span data-ttu-id="d1a3d-734">endsFalse</span><span class="sxs-lookup"><span data-stu-id="d1a3d-734">endsFalse</span></span> | <span data-ttu-id="d1a3d-735">Booleano</span><span class="sxs-lookup"><span data-stu-id="d1a3d-735">Bool</span></span> | <span data-ttu-id="d1a3d-736">False</span><span class="sxs-lookup"><span data-stu-id="d1a3d-736">False</span></span> |

<a id="string" />

## <a name="string"></a><span data-ttu-id="d1a3d-737">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-737">string</span></span>
`string(valueToConvert)`

<span data-ttu-id="d1a3d-738">Hola convierte especificado tooa cadena del valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-738">Converts hello specified value tooa string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-739">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-739">Parameters</span></span>

| <span data-ttu-id="d1a3d-740">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-740">Parameter</span></span> | <span data-ttu-id="d1a3d-741">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-741">Required</span></span> | <span data-ttu-id="d1a3d-742">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-742">Type</span></span> | <span data-ttu-id="d1a3d-743">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-743">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-744">valueToConvert</span><span class="sxs-lookup"><span data-stu-id="d1a3d-744">valueToConvert</span></span> |<span data-ttu-id="d1a3d-745">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-745">Yes</span></span> | <span data-ttu-id="d1a3d-746">Cualquiera</span><span class="sxs-lookup"><span data-stu-id="d1a3d-746">Any</span></span> |<span data-ttu-id="d1a3d-747">Hola valor tooconvert toostring.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-747">hello value tooconvert toostring.</span></span> <span data-ttu-id="d1a3d-748">Se puede convertir cualquier tipo de valor, incluidos objetos y matrices.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-748">Any type of value can be converted, including objects and arrays.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-749">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-749">Return value</span></span>

<span data-ttu-id="d1a3d-750">Una cadena de hello valor convertido.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-750">A string of hello converted value.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-751">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-751">Examples</span></span>

<span data-ttu-id="d1a3d-752">Hola de ejemplo siguiente muestra cómo tooconvert distintos tipos de valores toostrings:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-752">hello following example shows how tooconvert different types of values toostrings:</span></span>

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

<span data-ttu-id="d1a3d-753">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-753">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-754">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-754">Name</span></span> | <span data-ttu-id="d1a3d-755">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-755">Type</span></span> | <span data-ttu-id="d1a3d-756">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-756">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-757">objectOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-757">objectOutput</span></span> | <span data-ttu-id="d1a3d-758">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-758">String</span></span> | <span data-ttu-id="d1a3d-759">{"valueA":10,"valueB":"Example Text"}</span><span class="sxs-lookup"><span data-stu-id="d1a3d-759">{"valueA":10,"valueB":"Example Text"}</span></span> |
| <span data-ttu-id="d1a3d-760">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-760">arrayOutput</span></span> | <span data-ttu-id="d1a3d-761">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-761">String</span></span> | <span data-ttu-id="d1a3d-762">["a","b","c"]</span><span class="sxs-lookup"><span data-stu-id="d1a3d-762">["a","b","c"]</span></span> |
| <span data-ttu-id="d1a3d-763">intOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-763">intOutput</span></span> | <span data-ttu-id="d1a3d-764">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-764">String</span></span> | <span data-ttu-id="d1a3d-765">5</span><span class="sxs-lookup"><span data-stu-id="d1a3d-765">5</span></span> |

<a id="substring" />

## <a name="substring"></a><span data-ttu-id="d1a3d-766">substring</span><span class="sxs-lookup"><span data-stu-id="d1a3d-766">substring</span></span>
`substring(stringToParse, startIndex, length)`

<span data-ttu-id="d1a3d-767">Devuelve una subcadena que comienza en hello especificado posición de carácter y contiene Hola del número de caracteres especificado.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-767">Returns a substring that starts at hello specified character position and contains hello specified number of characters.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-768">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-768">Parameters</span></span>

| <span data-ttu-id="d1a3d-769">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-769">Parameter</span></span> | <span data-ttu-id="d1a3d-770">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-770">Required</span></span> | <span data-ttu-id="d1a3d-771">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-771">Type</span></span> | <span data-ttu-id="d1a3d-772">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-772">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-773">stringToParse</span><span class="sxs-lookup"><span data-stu-id="d1a3d-773">stringToParse</span></span> |<span data-ttu-id="d1a3d-774">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-774">Yes</span></span> |<span data-ttu-id="d1a3d-775">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-775">string</span></span> |<span data-ttu-id="d1a3d-776">cadena original de Hola desde qué Hola se extrae la subcadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-776">hello original string from which hello substring is extracted.</span></span> |
| <span data-ttu-id="d1a3d-777">startIndex</span><span class="sxs-lookup"><span data-stu-id="d1a3d-777">startIndex</span></span> |<span data-ttu-id="d1a3d-778">No</span><span class="sxs-lookup"><span data-stu-id="d1a3d-778">No</span></span> |<span data-ttu-id="d1a3d-779">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-779">int</span></span> |<span data-ttu-id="d1a3d-780">Hola basado en cero posición de carácter inicial de la subcadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-780">hello zero-based starting character position for hello substring.</span></span> |
| <span data-ttu-id="d1a3d-781">length</span><span class="sxs-lookup"><span data-stu-id="d1a3d-781">length</span></span> |<span data-ttu-id="d1a3d-782">No</span><span class="sxs-lookup"><span data-stu-id="d1a3d-782">No</span></span> |<span data-ttu-id="d1a3d-783">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-783">int</span></span> |<span data-ttu-id="d1a3d-784">número de Hola de caracteres de la subcadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-784">hello number of characters for hello substring.</span></span> <span data-ttu-id="d1a3d-785">Debe hacer referencia tooa ubicación dentro de la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-785">Must refer tooa location within hello string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-786">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-786">Return value</span></span>

<span data-ttu-id="d1a3d-787">subcadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-787">hello substring.</span></span>

### <a name="remarks"></a><span data-ttu-id="d1a3d-788">Comentarios</span><span class="sxs-lookup"><span data-stu-id="d1a3d-788">Remarks</span></span>

<span data-ttu-id="d1a3d-789">se produce un error en la función Hello cuando subsecuencia de Hola se extiende más allá del final de Hola de cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-789">hello function fails when hello substring extends beyond hello end of hello string.</span></span> <span data-ttu-id="d1a3d-790">se produce un error en la siguiente ejemplo de Hola con hello error "parámetros de índice y la longitud de hello deben hacer referencia tooa ubicación dentro de la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-790">hello following example fails with hello error "hello index and length parameters must refer tooa location within hello string.</span></span> <span data-ttu-id="d1a3d-791">Hola parámetro index: '0', Hola parámetro length: Hola '11', longitud del parámetro de cadena de hello: '10'. ".</span><span class="sxs-lookup"><span data-stu-id="d1a3d-791">hello index parameter: '0', hello length parameter: '11', hello length of hello string parameter: '10'.".</span></span>

```json
"parameters": {
    "inputString": { "type": "string", "value": "1234567890" }
},
"variables": { 
    "prefix": "[substring(parameters('inputString'), 0, 11)]"
}
```

### <a name="examples"></a><span data-ttu-id="d1a3d-792">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-792">Examples</span></span>

<span data-ttu-id="d1a3d-793">Hola de ejemplo siguiente extrae una subcadena de un parámetro.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-793">hello following example extracts a substring from a parameter.</span></span>

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

<span data-ttu-id="d1a3d-794">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-794">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-795">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-795">Name</span></span> | <span data-ttu-id="d1a3d-796">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-796">Type</span></span> | <span data-ttu-id="d1a3d-797">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-797">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-798">substringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-798">substringOutput</span></span> | <span data-ttu-id="d1a3d-799">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-799">String</span></span> | <span data-ttu-id="d1a3d-800">two</span><span class="sxs-lookup"><span data-stu-id="d1a3d-800">two</span></span> |


<a id="take" />

## <a name="take"></a><span data-ttu-id="d1a3d-801">take</span><span class="sxs-lookup"><span data-stu-id="d1a3d-801">take</span></span>
`take(originalValue, numberToTake)`

<span data-ttu-id="d1a3d-802">Devuelve una cadena con hello número especificado de caracteres desde el principio de Hola de Hola cadena o una matriz con hello un número especificado de elementos desde el principio de Hola de matriz de Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-802">Returns a string with hello specified number of characters from hello start of hello string, or an array with hello specified number of elements from hello start of hello array.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-803">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-803">Parameters</span></span>

| <span data-ttu-id="d1a3d-804">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-804">Parameter</span></span> | <span data-ttu-id="d1a3d-805">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-805">Required</span></span> | <span data-ttu-id="d1a3d-806">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-806">Type</span></span> | <span data-ttu-id="d1a3d-807">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-807">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-808">originalValue</span><span class="sxs-lookup"><span data-stu-id="d1a3d-808">originalValue</span></span> |<span data-ttu-id="d1a3d-809">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-809">Yes</span></span> |<span data-ttu-id="d1a3d-810">matriz o cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-810">array or string</span></span> |<span data-ttu-id="d1a3d-811">Hola array o string tootake Hola elementos.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-811">hello array or string tootake hello elements from.</span></span> |
| <span data-ttu-id="d1a3d-812">numberToTake</span><span class="sxs-lookup"><span data-stu-id="d1a3d-812">numberToTake</span></span> |<span data-ttu-id="d1a3d-813">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-813">Yes</span></span> |<span data-ttu-id="d1a3d-814">int</span><span class="sxs-lookup"><span data-stu-id="d1a3d-814">int</span></span> |<span data-ttu-id="d1a3d-815">número de Hola de tootake elementos o caracteres.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-815">hello number of elements or characters tootake.</span></span> <span data-ttu-id="d1a3d-816">Si este valor es 0 o un valor inferior, se devolverá una matriz o cadena vacía.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-816">If this value is 0 or less, an empty array or string is returned.</span></span> <span data-ttu-id="d1a3d-817">Si es mayor que la longitud de Hola de hello con cadena o una matriz, se devuelven todos los elementos de hello en la matriz de Hola o de cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-817">If it is larger than hello length of hello given array or string, all hello elements in hello array or string are returned.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-818">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-818">Return value</span></span>

<span data-ttu-id="d1a3d-819">Una matriz o cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-819">An array or string.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-820">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-820">Examples</span></span>

<span data-ttu-id="d1a3d-821">Hola siguiendo el ejemplo hello de toma un número especificado de elementos de matriz de Hola y los caracteres de una cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-821">hello following example takes hello specified number of elements from hello array, and characters from a string.</span></span>

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

<span data-ttu-id="d1a3d-822">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-822">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-823">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-823">Name</span></span> | <span data-ttu-id="d1a3d-824">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-824">Type</span></span> | <span data-ttu-id="d1a3d-825">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-825">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-826">arrayOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-826">arrayOutput</span></span> | <span data-ttu-id="d1a3d-827">Matriz</span><span class="sxs-lookup"><span data-stu-id="d1a3d-827">Array</span></span> | <span data-ttu-id="d1a3d-828">["one", "two"]</span><span class="sxs-lookup"><span data-stu-id="d1a3d-828">["one", "two"]</span></span> |
| <span data-ttu-id="d1a3d-829">stringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-829">stringOutput</span></span> | <span data-ttu-id="d1a3d-830">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-830">String</span></span> | <span data-ttu-id="d1a3d-831">en</span><span class="sxs-lookup"><span data-stu-id="d1a3d-831">on</span></span> |

<a id="tolower" />

## <a name="tolower"></a><span data-ttu-id="d1a3d-832">toLower</span><span class="sxs-lookup"><span data-stu-id="d1a3d-832">toLower</span></span>
`toLower(stringToChange)`

<span data-ttu-id="d1a3d-833">Hola convierte especificado case de toolower la cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-833">Converts hello specified string toolower case.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-834">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-834">Parameters</span></span>

| <span data-ttu-id="d1a3d-835">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-835">Parameter</span></span> | <span data-ttu-id="d1a3d-836">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-836">Required</span></span> | <span data-ttu-id="d1a3d-837">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-837">Type</span></span> | <span data-ttu-id="d1a3d-838">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-838">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-839">stringToChange</span><span class="sxs-lookup"><span data-stu-id="d1a3d-839">stringToChange</span></span> |<span data-ttu-id="d1a3d-840">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-840">Yes</span></span> |<span data-ttu-id="d1a3d-841">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-841">string</span></span> |<span data-ttu-id="d1a3d-842">caso de Hello valor tooconvert toolower.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-842">hello value tooconvert toolower case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-843">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-843">Return value</span></span>

<span data-ttu-id="d1a3d-844">cadena de Hello convertida toolower caso.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-844">hello string converted toolower case.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-845">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-845">Examples</span></span>

<span data-ttu-id="d1a3d-846">Hola siguiente ejemplo convierte un caso de toolower del valor de parámetro y el caso de tooupper.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-846">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="d1a3d-847">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-847">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-848">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-848">Name</span></span> | <span data-ttu-id="d1a3d-849">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-849">Type</span></span> | <span data-ttu-id="d1a3d-850">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-850">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-851">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-851">toLowerOutput</span></span> | <span data-ttu-id="d1a3d-852">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-852">String</span></span> | <span data-ttu-id="d1a3d-853">one two three</span><span class="sxs-lookup"><span data-stu-id="d1a3d-853">one two three</span></span> |
| <span data-ttu-id="d1a3d-854">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-854">toUpperOutput</span></span> | <span data-ttu-id="d1a3d-855">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-855">String</span></span> | <span data-ttu-id="d1a3d-856">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="d1a3d-856">ONE TWO THREE</span></span> |

<a id="toupper" />

## <a name="toupper"></a><span data-ttu-id="d1a3d-857">toUpper</span><span class="sxs-lookup"><span data-stu-id="d1a3d-857">toUpper</span></span>
`toUpper(stringToChange)`

<span data-ttu-id="d1a3d-858">Hola convierte especificado case de tooupper la cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-858">Converts hello specified string tooupper case.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-859">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-859">Parameters</span></span>

| <span data-ttu-id="d1a3d-860">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-860">Parameter</span></span> | <span data-ttu-id="d1a3d-861">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-861">Required</span></span> | <span data-ttu-id="d1a3d-862">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-862">Type</span></span> | <span data-ttu-id="d1a3d-863">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-863">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-864">stringToChange</span><span class="sxs-lookup"><span data-stu-id="d1a3d-864">stringToChange</span></span> |<span data-ttu-id="d1a3d-865">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-865">Yes</span></span> |<span data-ttu-id="d1a3d-866">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-866">string</span></span> |<span data-ttu-id="d1a3d-867">caso de Hello valor tooconvert tooupper.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-867">hello value tooconvert tooupper case.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-868">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-868">Return value</span></span>

<span data-ttu-id="d1a3d-869">cadena de Hello convertida tooupper caso.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-869">hello string converted tooupper case.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-870">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-870">Examples</span></span>

<span data-ttu-id="d1a3d-871">Hola siguiente ejemplo convierte un caso de toolower del valor de parámetro y el caso de tooupper.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-871">hello following example converts a parameter value toolower case and tooupper case.</span></span>

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

<span data-ttu-id="d1a3d-872">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-872">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-873">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-873">Name</span></span> | <span data-ttu-id="d1a3d-874">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-874">Type</span></span> | <span data-ttu-id="d1a3d-875">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-875">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-876">toLowerOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-876">toLowerOutput</span></span> | <span data-ttu-id="d1a3d-877">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-877">String</span></span> | <span data-ttu-id="d1a3d-878">one two three</span><span class="sxs-lookup"><span data-stu-id="d1a3d-878">one two three</span></span> |
| <span data-ttu-id="d1a3d-879">toUpperOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-879">toUpperOutput</span></span> | <span data-ttu-id="d1a3d-880">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-880">String</span></span> | <span data-ttu-id="d1a3d-881">ONE TWO THREE</span><span class="sxs-lookup"><span data-stu-id="d1a3d-881">ONE TWO THREE</span></span> |

<a id="trim" />

## <a name="trim"></a><span data-ttu-id="d1a3d-882">trim</span><span class="sxs-lookup"><span data-stu-id="d1a3d-882">trim</span></span>
`trim (stringToTrim)`

<span data-ttu-id="d1a3d-883">Quita todas las iniciales y finales de caracteres de espacio en blanco de Hola la cadena especificada.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-883">Removes all leading and trailing white-space characters from hello specified string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-884">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-884">Parameters</span></span>

| <span data-ttu-id="d1a3d-885">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-885">Parameter</span></span> | <span data-ttu-id="d1a3d-886">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-886">Required</span></span> | <span data-ttu-id="d1a3d-887">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-887">Type</span></span> | <span data-ttu-id="d1a3d-888">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-888">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-889">stringToTrim</span><span class="sxs-lookup"><span data-stu-id="d1a3d-889">stringToTrim</span></span> |<span data-ttu-id="d1a3d-890">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-890">Yes</span></span> |<span data-ttu-id="d1a3d-891">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-891">string</span></span> |<span data-ttu-id="d1a3d-892">Hola tootrim de valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-892">hello value tootrim.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-893">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-893">Return value</span></span>

<span data-ttu-id="d1a3d-894">cadena de Hello sin caracteres de espacio en blanco iniciales y finales.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-894">hello string without leading and trailing white-space characters.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-895">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-895">Examples</span></span>

<span data-ttu-id="d1a3d-896">Hello en el ejemplo siguiente se recorta caracteres de espacio en blanco de Hola de parámetro hello.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-896">hello following example trims hello white-space characters from hello parameter.</span></span>

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

<span data-ttu-id="d1a3d-897">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-897">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-898">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-898">Name</span></span> | <span data-ttu-id="d1a3d-899">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-899">Type</span></span> | <span data-ttu-id="d1a3d-900">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-900">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-901">return</span><span class="sxs-lookup"><span data-stu-id="d1a3d-901">return</span></span> | <span data-ttu-id="d1a3d-902">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-902">String</span></span> | <span data-ttu-id="d1a3d-903">one two three</span><span class="sxs-lookup"><span data-stu-id="d1a3d-903">one two three</span></span> |

<a id="uniquestring" />

## <a name="uniquestring"></a><span data-ttu-id="d1a3d-904">uniqueString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-904">uniqueString</span></span>
`uniqueString (baseString, ...)`

<span data-ttu-id="d1a3d-905">Crea una cadena de hash determinista basada en valores de hello proporcionados como parámetros.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-905">Creates a deterministic hash string based on hello values provided as parameters.</span></span> 

### <a name="parameters"></a><span data-ttu-id="d1a3d-906">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-906">Parameters</span></span>

| <span data-ttu-id="d1a3d-907">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-907">Parameter</span></span> | <span data-ttu-id="d1a3d-908">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-908">Required</span></span> | <span data-ttu-id="d1a3d-909">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-909">Type</span></span> | <span data-ttu-id="d1a3d-910">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-910">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-911">baseString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-911">baseString</span></span> |<span data-ttu-id="d1a3d-912">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-912">Yes</span></span> |<span data-ttu-id="d1a3d-913">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-913">string</span></span> |<span data-ttu-id="d1a3d-914">valor de Hello usa en hello hash función toocreate una cadena única.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-914">hello value used in hello hash function toocreate a unique string.</span></span> |
| <span data-ttu-id="d1a3d-915">parámetros adicionales según sea necesario</span><span class="sxs-lookup"><span data-stu-id="d1a3d-915">additional parameters as needed</span></span> |<span data-ttu-id="d1a3d-916">No</span><span class="sxs-lookup"><span data-stu-id="d1a3d-916">No</span></span> |<span data-ttu-id="d1a3d-917">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-917">string</span></span> |<span data-ttu-id="d1a3d-918">Puede agregar tantos cadenas como valor de hello toocreate necesaria que especifica el nivel de unicidad Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-918">You can add as many strings as needed toocreate hello value that specifies hello level of uniqueness.</span></span> |

### <a name="remarks"></a><span data-ttu-id="d1a3d-919">Comentarios</span><span class="sxs-lookup"><span data-stu-id="d1a3d-919">Remarks</span></span>

<span data-ttu-id="d1a3d-920">Esta función es útil cuando es necesario toocreate un nombre único para un recurso.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-920">This function is helpful when you need toocreate a unique name for a resource.</span></span> <span data-ttu-id="d1a3d-921">Se proporcionan valores de parámetro que limitan el ámbito de Hola de unicidad de resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-921">You provide parameter values that limit hello scope of uniqueness for hello result.</span></span> <span data-ttu-id="d1a3d-922">Puede especificar si el nombre de hello es único hacia abajo toosubscription, el grupo de recursos o la implementación.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-922">You can specify whether hello name is unique down toosubscription, resource group, or deployment.</span></span> 

<span data-ttu-id="d1a3d-923">Hola devuelve el valor no es una cadena aleatoria, pero en su lugar Hola resultado de una función hash.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-923">hello returned value is not a random string, but rather hello result of a hash function.</span></span> <span data-ttu-id="d1a3d-924">Hola devuelve el valor es 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-924">hello returned value is 13 characters long.</span></span> <span data-ttu-id="d1a3d-925">Debe ser único globalmente.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-925">It is not globally unique.</span></span> <span data-ttu-id="d1a3d-926">Puede que desee valor de hello toocombine con un prefijo de su toocreate de convención de nomenclatura un nombre que sea significativo.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-926">You may want toocombine hello value with a prefix from your naming convention toocreate a name that is meaningful.</span></span> <span data-ttu-id="d1a3d-927">Hello en el ejemplo siguiente se muestra formato Hola de hello devolvió el valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-927">hello following example shows hello format of hello returned value.</span></span> <span data-ttu-id="d1a3d-928">valor real de Hello varía según el saludo de los parámetros proporcionado.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-928">hello actual value varies by hello provided parameters.</span></span>

    tcvhiyu5h2o5o

<span data-ttu-id="d1a3d-929">Hello en los ejemplos siguientes muestra cómo toouse uniqueString toocreate un único valor de frecuencia niveles usados.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-929">hello following examples show how toouse uniqueString toocreate a unique value for commonly used levels.</span></span>

<span data-ttu-id="d1a3d-930">Toosubscription de ámbito único</span><span class="sxs-lookup"><span data-stu-id="d1a3d-930">Unique scoped toosubscription</span></span>

```json
"[uniqueString(subscription().subscriptionId)]"
```

<span data-ttu-id="d1a3d-931">Grupo de tooresource ámbito único</span><span class="sxs-lookup"><span data-stu-id="d1a3d-931">Unique scoped tooresource group</span></span>

```json
"[uniqueString(resourceGroup().id)]"
```

<span data-ttu-id="d1a3d-932">Toodeployment de ámbito único para un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-932">Unique scoped toodeployment for a resource group</span></span>

```json
"[uniqueString(resourceGroup().id, deployment().name)]"
```

<span data-ttu-id="d1a3d-933">Hola de ejemplo siguiente muestra cómo se toocreate un nombre único para una cuenta de almacenamiento basada en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-933">hello following example shows how toocreate a unique name for a storage account based on your resource group.</span></span> <span data-ttu-id="d1a3d-934">Dentro del grupo de recursos de hello, nombre de hello no es único si construyó Hola igual.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-934">Inside hello resource group, hello name is not unique if constructed hello same way.</span></span>

```json
"resources": [{ 
    "name": "[concat('storage', uniqueString(resourceGroup().id))]", 
    "type": "Microsoft.Storage/storageAccounts", 
    ...
```

### <a name="return-value"></a><span data-ttu-id="d1a3d-935">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-935">Return value</span></span>

<span data-ttu-id="d1a3d-936">Cadena que contiene 13 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-936">A string containing 13 characters.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-937">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-937">Examples</span></span>

<span data-ttu-id="d1a3d-938">Hola ejemplo siguiente devuelve los resultados de uniquestring:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-938">hello following example returns results from uniquestring:</span></span>

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

## <a name="uri"></a><span data-ttu-id="d1a3d-939">uri</span><span class="sxs-lookup"><span data-stu-id="d1a3d-939">uri</span></span>
`uri (baseUri, relativeUri)`

<span data-ttu-id="d1a3d-940">Crea un URI absoluto combinando baseUri hello y cadena de relativeUri Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-940">Creates an absolute URI by combining hello baseUri and hello relativeUri string.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-941">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-941">Parameters</span></span>

| <span data-ttu-id="d1a3d-942">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-942">Parameter</span></span> | <span data-ttu-id="d1a3d-943">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-943">Required</span></span> | <span data-ttu-id="d1a3d-944">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-944">Type</span></span> | <span data-ttu-id="d1a3d-945">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-945">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-946">baseUri</span><span class="sxs-lookup"><span data-stu-id="d1a3d-946">baseUri</span></span> |<span data-ttu-id="d1a3d-947">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-947">Yes</span></span> |<span data-ttu-id="d1a3d-948">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-948">string</span></span> |<span data-ttu-id="d1a3d-949">cadena de uri base Hola.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-949">hello base uri string.</span></span> |
| <span data-ttu-id="d1a3d-950">relativeUri</span><span class="sxs-lookup"><span data-stu-id="d1a3d-950">relativeUri</span></span> |<span data-ttu-id="d1a3d-951">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-951">Yes</span></span> |<span data-ttu-id="d1a3d-952">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-952">string</span></span> |<span data-ttu-id="d1a3d-953">Hola uri relativo tooadd toohello uri base cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-953">hello relative uri string tooadd toohello base uri string.</span></span> |

<span data-ttu-id="d1a3d-954">Hola valor para hello **baseUri** parámetro puede incluir un archivo específico, pero solo Hola ruta de acceso base se utiliza para crear Hola URI.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-954">hello value for hello **baseUri** parameter can include a specific file, but only hello base path is used when constructing hello URI.</span></span> <span data-ttu-id="d1a3d-955">Por ejemplo, si se pasa `http://contoso.com/resources/azuredeploy.json` como Hola baseUri parámetro da como resultado un identificador URI base del `http://contoso.com/resources/`.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-955">For example, passing `http://contoso.com/resources/azuredeploy.json` as hello baseUri parameter results in a base URI of `http://contoso.com/resources/`.</span></span>

### <a name="return-value"></a><span data-ttu-id="d1a3d-956">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-956">Return value</span></span>

<span data-ttu-id="d1a3d-957">Una cadena que representa Hola URI absoluto para valores de hello base y relativo.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-957">A string representing hello absolute URI for hello base and relative values.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-958">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-958">Examples</span></span>

<span data-ttu-id="d1a3d-959">Hola de ejemplo siguiente muestra cómo tooconstruct una plantilla anidada de vínculo tooa con valor Hola de plantilla de hello principal.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-959">hello following example shows how tooconstruct a link tooa nested template based on hello value of hello parent template.</span></span>

```json
"templateLink": "[uri(deployment().properties.templateLink.uri, 'nested/azuredeploy.json')]"
```

<span data-ttu-id="d1a3d-960">Hola siguiente ejemplo se muestra cómo toouse uri, componente y uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-960">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="d1a3d-961">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-961">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-962">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-962">Name</span></span> | <span data-ttu-id="d1a3d-963">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-963">Type</span></span> | <span data-ttu-id="d1a3d-964">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-964">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-965">uriOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-965">uriOutput</span></span> | <span data-ttu-id="d1a3d-966">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-966">String</span></span> | <span data-ttu-id="d1a3d-967">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d1a3d-967">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="d1a3d-968">componentOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-968">componentOutput</span></span> | <span data-ttu-id="d1a3d-969">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-969">String</span></span> | <span data-ttu-id="d1a3d-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d1a3d-970">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="d1a3d-971">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-971">toStringOutput</span></span> | <span data-ttu-id="d1a3d-972">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-972">String</span></span> | <span data-ttu-id="d1a3d-973">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d1a3d-973">http://contoso.com/resources/nested/azuredeploy.json</span></span> |

<a id="uricomponent" />

## <a name="uricomponent"></a><span data-ttu-id="d1a3d-974">uriComponent</span><span class="sxs-lookup"><span data-stu-id="d1a3d-974">uriComponent</span></span>
`uricomponent(stringToEncode)`

<span data-ttu-id="d1a3d-975">Codifica un identificador URI.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-975">Encodes a URI.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-976">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-976">Parameters</span></span>

| <span data-ttu-id="d1a3d-977">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-977">Parameter</span></span> | <span data-ttu-id="d1a3d-978">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-978">Required</span></span> | <span data-ttu-id="d1a3d-979">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-979">Type</span></span> | <span data-ttu-id="d1a3d-980">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-980">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-981">stringToEncode</span><span class="sxs-lookup"><span data-stu-id="d1a3d-981">stringToEncode</span></span> |<span data-ttu-id="d1a3d-982">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-982">Yes</span></span> |<span data-ttu-id="d1a3d-983">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-983">string</span></span> |<span data-ttu-id="d1a3d-984">Hola tooencode de valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-984">hello value tooencode.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-985">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-985">Return value</span></span>

<span data-ttu-id="d1a3d-986">Una cadena de hello URI había codificado valor.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-986">A string of hello URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-987">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-987">Examples</span></span>

<span data-ttu-id="d1a3d-988">Hola siguiente ejemplo se muestra cómo toouse uri, componente y uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-988">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="d1a3d-989">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-989">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-990">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-990">Name</span></span> | <span data-ttu-id="d1a3d-991">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-991">Type</span></span> | <span data-ttu-id="d1a3d-992">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-992">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-993">uriOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-993">uriOutput</span></span> | <span data-ttu-id="d1a3d-994">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-994">String</span></span> | <span data-ttu-id="d1a3d-995">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d1a3d-995">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="d1a3d-996">componentOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-996">componentOutput</span></span> | <span data-ttu-id="d1a3d-997">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-997">String</span></span> | <span data-ttu-id="d1a3d-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d1a3d-998">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="d1a3d-999">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-999">toStringOutput</span></span> | <span data-ttu-id="d1a3d-1000">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1000">String</span></span> | <span data-ttu-id="d1a3d-1001">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1001">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


<a id="uricomponenttostring" />

## <a name="uricomponenttostring"></a><span data-ttu-id="d1a3d-1002">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1002">uriComponentToString</span></span>
`uriComponentToString(uriEncodedString)`

<span data-ttu-id="d1a3d-1003">Devuelve una cadena del valor codificado por el identificador URI.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1003">Returns a string of a URI encoded value.</span></span>

### <a name="parameters"></a><span data-ttu-id="d1a3d-1004">parameters</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1004">Parameters</span></span>

| <span data-ttu-id="d1a3d-1005">Parámetro</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1005">Parameter</span></span> | <span data-ttu-id="d1a3d-1006">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1006">Required</span></span> | <span data-ttu-id="d1a3d-1007">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1007">Type</span></span> | <span data-ttu-id="d1a3d-1008">Descripción</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1008">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="d1a3d-1009">uriEncodedString</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1009">uriEncodedString</span></span> |<span data-ttu-id="d1a3d-1010">Sí</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1010">Yes</span></span> |<span data-ttu-id="d1a3d-1011">cadena</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1011">string</span></span> |<span data-ttu-id="d1a3d-1012">Hola URI había codificado valor tooconvert tooa cadena.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1012">hello URI encoded value tooconvert tooa string.</span></span> |

### <a name="return-value"></a><span data-ttu-id="d1a3d-1013">Valor devuelto</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1013">Return value</span></span>

<span data-ttu-id="d1a3d-1014">Una cadena descodificada del valor codificado por el identificador URI.</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1014">A decoded string of URI encoded value.</span></span>

### <a name="examples"></a><span data-ttu-id="d1a3d-1015">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1015">Examples</span></span>

<span data-ttu-id="d1a3d-1016">Hola siguiente ejemplo se muestra cómo toouse uri, componente y uriComponentToString:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1016">hello following example shows how toouse uri, uriComponent, and uriComponentToString:</span></span>

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

<span data-ttu-id="d1a3d-1017">Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1017">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="d1a3d-1018">Nombre</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1018">Name</span></span> | <span data-ttu-id="d1a3d-1019">Tipo</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1019">Type</span></span> | <span data-ttu-id="d1a3d-1020">Valor</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1020">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="d1a3d-1021">uriOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1021">uriOutput</span></span> | <span data-ttu-id="d1a3d-1022">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1022">String</span></span> | <span data-ttu-id="d1a3d-1023">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1023">http://contoso.com/resources/nested/azuredeploy.json</span></span> |
| <span data-ttu-id="d1a3d-1024">componentOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1024">componentOutput</span></span> | <span data-ttu-id="d1a3d-1025">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1025">String</span></span> | <span data-ttu-id="d1a3d-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1026">http%3A%2F%2Fcontoso.com%2Fresources%2Fnested%2Fazuredeploy.json</span></span> |
| <span data-ttu-id="d1a3d-1027">toStringOutput</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1027">toStringOutput</span></span> | <span data-ttu-id="d1a3d-1028">String</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1028">String</span></span> | <span data-ttu-id="d1a3d-1029">http://contoso.com/resources/nested/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1029">http://contoso.com/resources/nested/azuredeploy.json</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d1a3d-1030">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1030">Next steps</span></span>
* <span data-ttu-id="d1a3d-1031">Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1031">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d1a3d-1032">toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1032">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="d1a3d-1033">tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1033">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="d1a3d-1034">toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d1a3d-1034">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

