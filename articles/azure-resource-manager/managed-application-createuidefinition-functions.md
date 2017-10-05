---
title: Funciones para crear definiciones de interfaz de usuario para aplicaciones administradas de Azure | Microsoft Docs
description: "Describe las funciones que se usarán al crear definiciones de interfaz de usuario para aplicaciones administradas de Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 62ee10eb8e6f33cc4d828cf01b405c846bef8aa4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="11d3d-103">Funciones CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="11d3d-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="11d3d-104">Esta sección contiene las firmas de todas las funciones compatibles de una CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="11d3d-104">This section contains the signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="11d3d-105">Para utilizar una función, encierre la declaración entre corchetes.</span><span class="sxs-lookup"><span data-stu-id="11d3d-105">To use a function, surround the declaration with square brackets.</span></span> <span data-ttu-id="11d3d-106">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="11d3d-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="11d3d-107">Puede hacerse referencia a cadenas y otras funciones como parámetros para una función, pero las cadenas deben encerrarse entre comillas simples.</span><span class="sxs-lookup"><span data-stu-id="11d3d-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="11d3d-108">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="11d3d-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="11d3d-109">Si corresponde, puede hacer referencia a propiedades de la salida de una función mediante el operador de punto.</span><span class="sxs-lookup"><span data-stu-id="11d3d-109">Where applicable, you can reference properties of the output of a function by using the dot operator.</span></span> <span data-ttu-id="11d3d-110">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="11d3d-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="11d3d-111">Referencias a funciones</span><span class="sxs-lookup"><span data-stu-id="11d3d-111">Referencing functions</span></span>
<span data-ttu-id="11d3d-112">Estas funciones se pueden usar para hacer referencia a salidas de propiedades o contexto de una instancia de CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="11d3d-112">These functions can be used to reference outputs from the properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="11d3d-113">basics</span><span class="sxs-lookup"><span data-stu-id="11d3d-113">basics</span></span>
<span data-ttu-id="11d3d-114">Devuelve los valores de salida de un elemento que se define en el paso Basics.</span><span class="sxs-lookup"><span data-stu-id="11d3d-114">Returns the output values of an element that is defined in the Basics step.</span></span>

<span data-ttu-id="11d3d-115">En el ejemplo siguiente, se devuelve el resultado del elemento denominado `foo` en el paso Basics:</span><span class="sxs-lookup"><span data-stu-id="11d3d-115">The following example returns the output of the element named `foo` in the Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="11d3d-116">steps</span><span class="sxs-lookup"><span data-stu-id="11d3d-116">steps</span></span>
<span data-ttu-id="11d3d-117">Devuelve los valores de salida de un elemento que se define en el paso especificado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-117">Returns the output values of an element that is defined in the specified step.</span></span> <span data-ttu-id="11d3d-118">Para obtener los valores de salida de los elementos en el paso Basics, use `basics()` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="11d3d-118">To get the output values of elements in the Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="11d3d-119">En el ejemplo siguiente, se devuelve el resultado del elemento denominado `bar` en el paso denominado `foo`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-119">The following example returns the output of the element named `bar` in the step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="11d3d-120">location</span><span class="sxs-lookup"><span data-stu-id="11d3d-120">location</span></span>
<span data-ttu-id="11d3d-121">Devuelve la ubicación seleccionada en el paso Basics o el contexto actual.</span><span class="sxs-lookup"><span data-stu-id="11d3d-121">Returns the location selected in the Basics step or the current context.</span></span>

<span data-ttu-id="11d3d-122">El siguiente ejemplo podría devolver `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-122">The following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="11d3d-123">Funciones de cadena</span><span class="sxs-lookup"><span data-stu-id="11d3d-123">String functions</span></span>
<span data-ttu-id="11d3d-124">Estas funciones solo se pueden usar con cadenas de JSON.</span><span class="sxs-lookup"><span data-stu-id="11d3d-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="11d3d-125">concat</span><span class="sxs-lookup"><span data-stu-id="11d3d-125">concat</span></span>
<span data-ttu-id="11d3d-126">Concatena una o varias cadenas.</span><span class="sxs-lookup"><span data-stu-id="11d3d-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="11d3d-127">Por ejemplo, si el valor de salida de `element1` si `"bar"`, a continuación, en este ejemplo se devuelve la cadena de `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-127">For example, if the output value of `element1` if `"bar"`, then this example returns the string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="11d3d-128">substring</span><span class="sxs-lookup"><span data-stu-id="11d3d-128">substring</span></span>
<span data-ttu-id="11d3d-129">Devuelve la subcadena de la cadena especificada.</span><span class="sxs-lookup"><span data-stu-id="11d3d-129">Returns the substring of the specified string.</span></span> <span data-ttu-id="11d3d-130">La subcadena comienza en el índice especificado y tiene la longitud especificada.</span><span class="sxs-lookup"><span data-stu-id="11d3d-130">The substring starts at the specified index and has the specified length.</span></span>

<span data-ttu-id="11d3d-131">El siguiente ejemplo devuelve `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-131">The following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="11d3d-132">replace</span><span class="sxs-lookup"><span data-stu-id="11d3d-132">replace</span></span>
<span data-ttu-id="11d3d-133">Devuelve una cadena en la que se reemplazan todas las instancias de la cadena especificada en la cadena actual con otra cadena.</span><span class="sxs-lookup"><span data-stu-id="11d3d-133">Returns a string in which all occurrences of the specified string in the current string are replaced with another string.</span></span>

<span data-ttu-id="11d3d-134">El siguiente ejemplo devuelve `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-134">The following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="11d3d-135">GUID</span><span class="sxs-lookup"><span data-stu-id="11d3d-135">guid</span></span>
<span data-ttu-id="11d3d-136">Genera una cadena única global (GUID).</span><span class="sxs-lookup"><span data-stu-id="11d3d-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="11d3d-137">El siguiente ejemplo podría devolver `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-137">The following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="11d3d-138">toLower</span><span class="sxs-lookup"><span data-stu-id="11d3d-138">toLower</span></span>
<span data-ttu-id="11d3d-139">Devuelve una cadena convertida a minúsculas.</span><span class="sxs-lookup"><span data-stu-id="11d3d-139">Returns a string converted to lowercase.</span></span>

<span data-ttu-id="11d3d-140">El siguiente ejemplo devuelve `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-140">The following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="11d3d-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="11d3d-141">toUpper</span></span>
<span data-ttu-id="11d3d-142">Devuelve una cadena convertida a mayúsculas.</span><span class="sxs-lookup"><span data-stu-id="11d3d-142">Returns a string converted to uppercase.</span></span>

<span data-ttu-id="11d3d-143">El siguiente ejemplo devuelve `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-143">The following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="11d3d-144">Funciones de colección</span><span class="sxs-lookup"><span data-stu-id="11d3d-144">Collection functions</span></span>
<span data-ttu-id="11d3d-145">Estas funciones se pueden usar con las colecciones, como las cadenas JSON, matrices y objetos.</span><span class="sxs-lookup"><span data-stu-id="11d3d-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="11d3d-146">contains</span><span class="sxs-lookup"><span data-stu-id="11d3d-146">contains</span></span>
<span data-ttu-id="11d3d-147">Devuelve `true` si una cadena contiene la subcadena especificada, una matriz contiene el valor especificado o un objeto contiene la clave especificada.</span><span class="sxs-lookup"><span data-stu-id="11d3d-147">Returns `true` if a string contains the specified substring, an array contains the specified value, or an object contains the specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="11d3d-148">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="11d3d-148">Example 1: string</span></span>
<span data-ttu-id="11d3d-149">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-149">The following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="11d3d-150">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="11d3d-150">Example 2: array</span></span>
<span data-ttu-id="11d3d-151">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="11d3d-152">El siguiente ejemplo devuelve `false`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-152">The following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="11d3d-153">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="11d3d-153">Example 3: object</span></span>
<span data-ttu-id="11d3d-154">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="11d3d-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="11d3d-155">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-155">The following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="11d3d-156">length</span><span class="sxs-lookup"><span data-stu-id="11d3d-156">length</span></span>
<span data-ttu-id="11d3d-157">Devuelve el número de caracteres de una cadena, el número de valores de una matriz o el número de claves en un objeto.</span><span class="sxs-lookup"><span data-stu-id="11d3d-157">Returns the number of characters in a string, the number of values in an array, or the number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="11d3d-158">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="11d3d-158">Example 1: string</span></span>
<span data-ttu-id="11d3d-159">El siguiente ejemplo devuelve `6`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-159">The following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="11d3d-160">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="11d3d-160">Example 2: array</span></span>
<span data-ttu-id="11d3d-161">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="11d3d-162">El siguiente ejemplo devuelve `3`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-162">The following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="11d3d-163">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="11d3d-163">Example 3: object</span></span>
<span data-ttu-id="11d3d-164">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="11d3d-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="11d3d-165">El siguiente ejemplo devuelve `2`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-165">The following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="11d3d-166">empty</span><span class="sxs-lookup"><span data-stu-id="11d3d-166">empty</span></span>
<span data-ttu-id="11d3d-167">Devuelve `true` si la cadena, la matriz o el objeto es nulo o está vacío.</span><span class="sxs-lookup"><span data-stu-id="11d3d-167">Returns `true` if the string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="11d3d-168">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="11d3d-168">Example 1: string</span></span>
<span data-ttu-id="11d3d-169">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-169">The following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="11d3d-170">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="11d3d-170">Example 2: array</span></span>
<span data-ttu-id="11d3d-171">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="11d3d-172">El siguiente ejemplo devuelve `false`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-172">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="11d3d-173">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="11d3d-173">Example 3: object</span></span>
<span data-ttu-id="11d3d-174">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="11d3d-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="11d3d-175">El siguiente ejemplo devuelve `false`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-175">The following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="11d3d-176">Ejemplo 4: nulo y sin definir</span><span class="sxs-lookup"><span data-stu-id="11d3d-176">Example 4: null and undefined</span></span>
<span data-ttu-id="11d3d-177">Asuma que `element1` es `null` o no está definida.</span><span class="sxs-lookup"><span data-stu-id="11d3d-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="11d3d-178">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-178">The following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="11d3d-179">first</span><span class="sxs-lookup"><span data-stu-id="11d3d-179">first</span></span>
<span data-ttu-id="11d3d-180">Devuelve el primer carácter de la cadena especificada, el primer valor de la matriz especificada o la primera clave y valor del objeto especificado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-180">Returns the first character of the specified string; first value of the specified array; or the first key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="11d3d-181">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="11d3d-181">Example 1: string</span></span>
<span data-ttu-id="11d3d-182">El siguiente ejemplo devuelve `"f"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-182">The following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="11d3d-183">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="11d3d-183">Example 2: array</span></span>
<span data-ttu-id="11d3d-184">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="11d3d-185">El siguiente ejemplo devuelve `1`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-185">The following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="11d3d-186">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="11d3d-186">Example 3: object</span></span>
<span data-ttu-id="11d3d-187">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="11d3d-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="11d3d-188">El siguiente ejemplo devuelve `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-188">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="11d3d-189">last</span><span class="sxs-lookup"><span data-stu-id="11d3d-189">last</span></span>
<span data-ttu-id="11d3d-190">Devuelve el último carácter de la cadena especificada, el último valor de la matriz especificada o la última clave y valor del objeto especificado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-190">Returns the last character of the specified string, the last value of the specified array, or the last key and value of the specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="11d3d-191">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="11d3d-191">Example 1: string</span></span>
<span data-ttu-id="11d3d-192">El siguiente ejemplo devuelve `"r"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-192">The following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="11d3d-193">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="11d3d-193">Example 2: array</span></span>
<span data-ttu-id="11d3d-194">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="11d3d-195">El siguiente ejemplo devuelve `2`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-195">The following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="11d3d-196">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="11d3d-196">Example 3: object</span></span>
<span data-ttu-id="11d3d-197">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="11d3d-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="11d3d-198">El siguiente ejemplo devuelve `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-198">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="11d3d-199">take</span><span class="sxs-lookup"><span data-stu-id="11d3d-199">take</span></span>
<span data-ttu-id="11d3d-200">Devuelve un número especificado de caracteres contiguos desde el principio de la cadena, un número especificado de valores contiguos desde el principio de la matriz o un número de claves y valores contiguos desde el principio del objeto especificado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-200">Returns a specified number of contiguous characters from the start of the string, a specified number of contiguous values from the start of the array, or a specified number of contiguous keys and values from the start of the object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="11d3d-201">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="11d3d-201">Example 1: string</span></span>
<span data-ttu-id="11d3d-202">El siguiente ejemplo devuelve `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-202">The following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="11d3d-203">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="11d3d-203">Example 2: array</span></span>
<span data-ttu-id="11d3d-204">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="11d3d-205">El siguiente ejemplo devuelve `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-205">The following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="11d3d-206">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="11d3d-206">Example 3: object</span></span>
<span data-ttu-id="11d3d-207">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="11d3d-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="11d3d-208">El siguiente ejemplo devuelve `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-208">The following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="11d3d-209">skip</span><span class="sxs-lookup"><span data-stu-id="11d3d-209">skip</span></span>
<span data-ttu-id="11d3d-210">Omite un número especificado de elementos de una colección y, a continuación, devuelve los elementos restantes.</span><span class="sxs-lookup"><span data-stu-id="11d3d-210">Bypasses a specified number of elements in a collection, and then returns the remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="11d3d-211">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="11d3d-211">Example 1: string</span></span>
<span data-ttu-id="11d3d-212">El siguiente ejemplo devuelve `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-212">The following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="11d3d-213">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="11d3d-213">Example 2: array</span></span>
<span data-ttu-id="11d3d-214">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="11d3d-215">El siguiente ejemplo devuelve `[3]`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-215">The following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="11d3d-216">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="11d3d-216">Example 3: object</span></span>
<span data-ttu-id="11d3d-217">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="11d3d-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="11d3d-218">El siguiente ejemplo devuelve `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-218">The following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="11d3d-219">Funciones lógicas</span><span class="sxs-lookup"><span data-stu-id="11d3d-219">Logical functions</span></span>
<span data-ttu-id="11d3d-220">Estas funciones se pueden usar en los condicionales.</span><span class="sxs-lookup"><span data-stu-id="11d3d-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="11d3d-221">Algunas funciones pueden no admitir todos los tipos de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="11d3d-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="11d3d-222">equals</span><span class="sxs-lookup"><span data-stu-id="11d3d-222">equals</span></span>
<span data-ttu-id="11d3d-223">Devuelve `true` si ambos parámetros tienen el mismo tipo y valor.</span><span class="sxs-lookup"><span data-stu-id="11d3d-223">Returns `true` if both parameters have the same type and value.</span></span> <span data-ttu-id="11d3d-224">Algunas funciones admiten todos los tipos de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="11d3d-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="11d3d-225">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-225">The following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="11d3d-226">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-226">The following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="11d3d-227">El siguiente ejemplo devuelve `false`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-227">The following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="11d3d-228">less</span><span class="sxs-lookup"><span data-stu-id="11d3d-228">less</span></span>
<span data-ttu-id="11d3d-229">Devuelve `true` si el primer parámetro es estrictamente menor que el segundo parámetro.</span><span class="sxs-lookup"><span data-stu-id="11d3d-229">Returns `true` if the first parameter is strictly less than the second parameter.</span></span> <span data-ttu-id="11d3d-230">Esta función admite parámetros solo de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="11d3d-231">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-231">The following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="11d3d-232">El siguiente ejemplo devuelve `false`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-232">The following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="11d3d-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="11d3d-233">lessOrEquals</span></span>
<span data-ttu-id="11d3d-234">Devuelve `true` si el primer parámetro es estrictamente menor o igual que el segundo parámetro.</span><span class="sxs-lookup"><span data-stu-id="11d3d-234">Returns `true` if the first parameter is less than or equal to the second parameter.</span></span> <span data-ttu-id="11d3d-235">Esta función admite parámetros solo de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="11d3d-236">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-236">The following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="11d3d-237">greater</span><span class="sxs-lookup"><span data-stu-id="11d3d-237">greater</span></span>
<span data-ttu-id="11d3d-238">Devuelve `true` si el primer parámetro es estrictamente mayor que el segundo parámetro.</span><span class="sxs-lookup"><span data-stu-id="11d3d-238">Returns `true` if the first parameter is strictly greater than the second parameter.</span></span> <span data-ttu-id="11d3d-239">Esta función admite parámetros solo de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="11d3d-240">El siguiente ejemplo devuelve `false`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-240">The following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="11d3d-241">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-241">The following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="11d3d-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="11d3d-242">greaterOrEquals</span></span>
<span data-ttu-id="11d3d-243">Devuelve `true` si el primer parámetro es estrictamente mayor o igual que el segundo parámetro.</span><span class="sxs-lookup"><span data-stu-id="11d3d-243">Returns `true` if the first parameter is greater than or equal to the second parameter.</span></span> <span data-ttu-id="11d3d-244">Esta función admite parámetros solo de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="11d3d-245">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-245">The following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="11d3d-246">y</span><span class="sxs-lookup"><span data-stu-id="11d3d-246">and</span></span>
<span data-ttu-id="11d3d-247">Devuelve `true` si todos los parámetros se evalúan como `true`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-247">Returns `true` if all the parameters evaluate to `true`.</span></span> <span data-ttu-id="11d3d-248">Esta función admite dos o más parámetros solo de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="11d3d-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="11d3d-249">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-249">The following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="11d3d-250">El siguiente ejemplo devuelve `false`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-250">The following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="11d3d-251">o</span><span class="sxs-lookup"><span data-stu-id="11d3d-251">or</span></span>
<span data-ttu-id="11d3d-252">Devuelve `true` si al menos uno de los parámetros se evalúa como `true`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-252">Returns `true` if at least one of the parameters evaluates to `true`.</span></span> <span data-ttu-id="11d3d-253">Esta función admite dos o más parámetros solo de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="11d3d-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="11d3d-254">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-254">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="11d3d-255">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-255">The following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="11d3d-256">not</span><span class="sxs-lookup"><span data-stu-id="11d3d-256">not</span></span>
<span data-ttu-id="11d3d-257">Devuelve `true` si el parámetro se evalúa como `false`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-257">Returns `true` if the parameter evaluates to `false`.</span></span> <span data-ttu-id="11d3d-258">Esta función admite parámetros solo de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="11d3d-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="11d3d-259">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-259">The following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="11d3d-260">El siguiente ejemplo devuelve `false`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-260">The following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="11d3d-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="11d3d-261">coalesce</span></span>
<span data-ttu-id="11d3d-262">Devuelve el valor del primer parámetro no nulo.</span><span class="sxs-lookup"><span data-stu-id="11d3d-262">Returns the value of the first non-null parameter.</span></span> <span data-ttu-id="11d3d-263">Algunas funciones admiten todos los tipos de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="11d3d-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="11d3d-264">Asuma que `element1` y `element2` son indefinidos.</span><span class="sxs-lookup"><span data-stu-id="11d3d-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="11d3d-265">El siguiente ejemplo devuelve `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-265">The following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="11d3d-266">Funciones de conversión</span><span class="sxs-lookup"><span data-stu-id="11d3d-266">Conversion functions</span></span>
<span data-ttu-id="11d3d-267">Estas funciones se pueden usar para convertir valores entre tipos de datos JSON y codificaciones.</span><span class="sxs-lookup"><span data-stu-id="11d3d-267">These functions can be used to convert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="11d3d-268">int</span><span class="sxs-lookup"><span data-stu-id="11d3d-268">int</span></span>
<span data-ttu-id="11d3d-269">Convierte el parámetro en un número entero.</span><span class="sxs-lookup"><span data-stu-id="11d3d-269">Converts the parameter to an integer.</span></span> <span data-ttu-id="11d3d-270">Esta función admite parámetros de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="11d3d-271">El siguiente ejemplo devuelve `1`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-271">The following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="11d3d-272">El siguiente ejemplo devuelve `2`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-272">The following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="11d3d-273">float</span><span class="sxs-lookup"><span data-stu-id="11d3d-273">float</span></span>
<span data-ttu-id="11d3d-274">Convierte el parámetro en un número de punto flotante.</span><span class="sxs-lookup"><span data-stu-id="11d3d-274">Converts the parameter to a floating-point.</span></span> <span data-ttu-id="11d3d-275">Esta función admite parámetros de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="11d3d-276">El siguiente ejemplo devuelve `1.0`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-276">The following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="11d3d-277">El siguiente ejemplo devuelve `2.9`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-277">The following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="11d3d-278">cadena</span><span class="sxs-lookup"><span data-stu-id="11d3d-278">string</span></span>
<span data-ttu-id="11d3d-279">Convierte el parámetro en una cadena.</span><span class="sxs-lookup"><span data-stu-id="11d3d-279">Converts the parameter to a string.</span></span> <span data-ttu-id="11d3d-280">Esta función admite parámetros de todos los tipos de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="11d3d-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="11d3d-281">El siguiente ejemplo devuelve `"1"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-281">The following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="11d3d-282">El siguiente ejemplo devuelve `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-282">The following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="11d3d-283">El siguiente ejemplo devuelve `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-283">The following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="11d3d-284">El siguiente ejemplo devuelve `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-284">The following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="11d3d-285">booleano</span><span class="sxs-lookup"><span data-stu-id="11d3d-285">bool</span></span>
<span data-ttu-id="11d3d-286">Convierte el parámetro en un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="11d3d-286">Converts the parameter to a Boolean.</span></span> <span data-ttu-id="11d3d-287">Esta función admite parámetros de tipo number, string y booleano.</span><span class="sxs-lookup"><span data-stu-id="11d3d-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="11d3d-288">Similar a los booleanos en JavaScript, cualquier valor excepto `0` o `'false'` devuelve `true`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-288">Similar to Booleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="11d3d-289">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-289">The following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="11d3d-290">El siguiente ejemplo devuelve `false`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-290">The following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="11d3d-291">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-291">The following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="11d3d-292">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-292">The following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="11d3d-293">parse</span><span class="sxs-lookup"><span data-stu-id="11d3d-293">parse</span></span>
<span data-ttu-id="11d3d-294">Convierte el parámetro en un tipo nativo.</span><span class="sxs-lookup"><span data-stu-id="11d3d-294">Converts the parameter to a native type.</span></span> <span data-ttu-id="11d3d-295">En otras palabras, esta función es el inverso de `string()`.</span><span class="sxs-lookup"><span data-stu-id="11d3d-295">In other words, this function is the inverse of `string()`.</span></span> <span data-ttu-id="11d3d-296">Esta función admite parámetros solo de tipo string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="11d3d-297">El siguiente ejemplo devuelve `1`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-297">The following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="11d3d-298">El siguiente ejemplo devuelve `true`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-298">The following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="11d3d-299">El siguiente ejemplo devuelve `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-299">The following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="11d3d-300">El siguiente ejemplo devuelve `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-300">The following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="11d3d-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="11d3d-301">encodeBase64</span></span>
<span data-ttu-id="11d3d-302">Codifica el parámetro a una cadena de codificación Base 64.</span><span class="sxs-lookup"><span data-stu-id="11d3d-302">Encodes the parameter to a base-64 encoded string.</span></span> <span data-ttu-id="11d3d-303">Esta función admite parámetros solo de tipo string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="11d3d-304">El siguiente ejemplo devuelve `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-304">The following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="11d3d-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="11d3d-305">decodeBase64</span></span>
<span data-ttu-id="11d3d-306">Decodifica el parámetro de una cadena de codificación Base 64.</span><span class="sxs-lookup"><span data-stu-id="11d3d-306">Decodes the parameter from a base-64 encoded string.</span></span> <span data-ttu-id="11d3d-307">Esta función admite parámetros solo de tipo string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="11d3d-308">El siguiente ejemplo devuelve `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-308">The following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="11d3d-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="11d3d-309">encodeUriComponent</span></span>
<span data-ttu-id="11d3d-310">Codifica el parámetro a una cadena de codificación con dirección URL.</span><span class="sxs-lookup"><span data-stu-id="11d3d-310">Encodes the parameter to a URL encoded string.</span></span> <span data-ttu-id="11d3d-311">Esta función admite parámetros solo de tipo string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="11d3d-312">El siguiente ejemplo devuelve `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-312">The following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="11d3d-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="11d3d-313">decodeUriComponent</span></span>
<span data-ttu-id="11d3d-314">Decodifica el parámetro de una cadena de codificación con dirección URL.</span><span class="sxs-lookup"><span data-stu-id="11d3d-314">Decodes the parameter from a URL encoded string.</span></span> <span data-ttu-id="11d3d-315">Esta función admite parámetros solo de tipo string.</span><span class="sxs-lookup"><span data-stu-id="11d3d-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="11d3d-316">El siguiente ejemplo devuelve `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-316">The following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="11d3d-317">Funciones matemáticas</span><span class="sxs-lookup"><span data-stu-id="11d3d-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="11d3d-318">agregar</span><span class="sxs-lookup"><span data-stu-id="11d3d-318">add</span></span>
<span data-ttu-id="11d3d-319">Agrega dos números y devuelve el resultado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-319">Adds two numbers, and returns the result.</span></span>

<span data-ttu-id="11d3d-320">El siguiente ejemplo devuelve `3`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-320">The following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="11d3d-321">sub</span><span class="sxs-lookup"><span data-stu-id="11d3d-321">sub</span></span>
<span data-ttu-id="11d3d-322">Resta el segundo número al primer número y devuelve el resultado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-322">Subtracts the second number from the first number, and returns the result.</span></span>

<span data-ttu-id="11d3d-323">El siguiente ejemplo devuelve `1`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-323">The following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="11d3d-324">mul</span><span class="sxs-lookup"><span data-stu-id="11d3d-324">mul</span></span>
<span data-ttu-id="11d3d-325">Multiplica dos números y devuelve el resultado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-325">Multiplies two numbers, and returns the result.</span></span>

<span data-ttu-id="11d3d-326">El siguiente ejemplo devuelve `6`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-326">The following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="11d3d-327">div</span><span class="sxs-lookup"><span data-stu-id="11d3d-327">div</span></span>
<span data-ttu-id="11d3d-328">Divide el segundo número por el primer número y devuelve el resultado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-328">Divides the first number by the second number, and returns the result.</span></span> <span data-ttu-id="11d3d-329">El resultado es siempre un número entero.</span><span class="sxs-lookup"><span data-stu-id="11d3d-329">The result is always an integer.</span></span>

<span data-ttu-id="11d3d-330">El siguiente ejemplo devuelve `2`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-330">The following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="11d3d-331">mod</span><span class="sxs-lookup"><span data-stu-id="11d3d-331">mod</span></span>
<span data-ttu-id="11d3d-332">Divide el primer número por el segundo número y devuelve el resto.</span><span class="sxs-lookup"><span data-stu-id="11d3d-332">Divides the first number by the second number, and returns the remainder.</span></span>

<span data-ttu-id="11d3d-333">El siguiente ejemplo devuelve `0`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-333">The following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="11d3d-334">El siguiente ejemplo devuelve `2`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-334">The following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="11d3d-335">Min</span><span class="sxs-lookup"><span data-stu-id="11d3d-335">min</span></span>
<span data-ttu-id="11d3d-336">Devuelve el número más pequeño de los dos.</span><span class="sxs-lookup"><span data-stu-id="11d3d-336">Returns the small of the two numbers.</span></span>

<span data-ttu-id="11d3d-337">El siguiente ejemplo devuelve `1`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-337">The following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="11d3d-338">max</span><span class="sxs-lookup"><span data-stu-id="11d3d-338">max</span></span>
<span data-ttu-id="11d3d-339">Devuelve el número más grande de los dos.</span><span class="sxs-lookup"><span data-stu-id="11d3d-339">Returns the larger of the two numbers.</span></span>

<span data-ttu-id="11d3d-340">El siguiente ejemplo devuelve `2`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-340">The following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="11d3d-341">range</span><span class="sxs-lookup"><span data-stu-id="11d3d-341">range</span></span>
<span data-ttu-id="11d3d-342">Genera una secuencia de números enteros en el intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-342">Generates a sequence of integral numbers within the specified range.</span></span>

<span data-ttu-id="11d3d-343">El siguiente ejemplo devuelve `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-343">The following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="11d3d-344">rand</span><span class="sxs-lookup"><span data-stu-id="11d3d-344">rand</span></span>
<span data-ttu-id="11d3d-345">Genera un número integral aleatorio en el intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-345">Returns a random integral number within the specified range.</span></span> <span data-ttu-id="11d3d-346">Esta función no genera números aleatorios criptográficamente seguros.</span><span class="sxs-lookup"><span data-stu-id="11d3d-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="11d3d-347">El siguiente ejemplo podría devolver `42`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-347">The following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="11d3d-348">floor</span><span class="sxs-lookup"><span data-stu-id="11d3d-348">floor</span></span>
<span data-ttu-id="11d3d-349">Devuelve el valor entero más grande menor o igual que el número especificado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-349">Returns the largest integer less than or equal to the specified number.</span></span>

<span data-ttu-id="11d3d-350">El siguiente ejemplo devuelve `3`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-350">The following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="11d3d-351">ceil</span><span class="sxs-lookup"><span data-stu-id="11d3d-351">ceil</span></span>
<span data-ttu-id="11d3d-352">Devuelve el valor entero más grande mayor o igual que el número especificado.</span><span class="sxs-lookup"><span data-stu-id="11d3d-352">Returns the largest integer greater than or equal to the specified number.</span></span>

<span data-ttu-id="11d3d-353">El siguiente ejemplo devuelve `4`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-353">The following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="11d3d-354">Funciones de fecha</span><span class="sxs-lookup"><span data-stu-id="11d3d-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="11d3d-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="11d3d-355">utcNow</span></span>
<span data-ttu-id="11d3d-356">Devuelve una cadena en formato ISO 8601 de la fecha y hora actuales en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="11d3d-356">Returns a string in ISO 8601 format of the current date and time on the local computer.</span></span>

<span data-ttu-id="11d3d-357">El siguiente ejemplo podría devolver `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-357">The following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="11d3d-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="11d3d-358">addSeconds</span></span>
<span data-ttu-id="11d3d-359">Agrega un número entero de segundos a la marca de tiempo especificada.</span><span class="sxs-lookup"><span data-stu-id="11d3d-359">Adds an integral number of seconds to the specified timestamp.</span></span>

<span data-ttu-id="11d3d-360">El siguiente ejemplo devuelve `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-360">The following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="11d3d-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="11d3d-361">addMinutes</span></span>
<span data-ttu-id="11d3d-362">Agrega un número entero de minutos a la marca de tiempo especificada.</span><span class="sxs-lookup"><span data-stu-id="11d3d-362">Adds an integral number of minutes to the specified timestamp.</span></span>

<span data-ttu-id="11d3d-363">El siguiente ejemplo devuelve `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-363">The following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="11d3d-364">addHours</span><span class="sxs-lookup"><span data-stu-id="11d3d-364">addHours</span></span>
<span data-ttu-id="11d3d-365">Agrega un número entero de horas a la marca de tiempo especificada.</span><span class="sxs-lookup"><span data-stu-id="11d3d-365">Adds an integral number of hours to the specified timestamp.</span></span>

<span data-ttu-id="11d3d-366">El siguiente ejemplo devuelve `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="11d3d-366">The following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="11d3d-367">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11d3d-367">Next steps</span></span>
* <span data-ttu-id="11d3d-368">Para ver una introducción a Azure Resource Manager, consulte [Información general sobre Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11d3d-368">For an introduction to Azure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

