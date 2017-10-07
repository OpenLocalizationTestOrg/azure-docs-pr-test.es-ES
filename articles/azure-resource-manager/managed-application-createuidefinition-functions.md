---
title: "aaaAzure aplicación administrada crear funciones de definición de interfaz de usuario | Documentos de Microsoft"
description: Describe Hola funciones toouse al construir las definiciones de interfaz de usuario para las aplicaciones administradas de Azure
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
ms.openlocfilehash: 7a311a25404ccaec8c19c3ed8cd7038f6887c013
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-functions"></a><span data-ttu-id="bc29c-103">Funciones CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="bc29c-103">CreateUiDefinition functions</span></span>
<span data-ttu-id="bc29c-104">Esta sección contiene las firmas de Hola para todas las funciones compatibles de un CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="bc29c-104">This section contains hello signatures for all supported functions of a CreateUiDefinition.</span></span>

<span data-ttu-id="bc29c-105">toouse una función de la declaración de hello rodear con corchetes.</span><span class="sxs-lookup"><span data-stu-id="bc29c-105">toouse a function, surround hello declaration with square brackets.</span></span> <span data-ttu-id="bc29c-106">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bc29c-106">For example:</span></span>

```json
"[function()]"
```

<span data-ttu-id="bc29c-107">Puede hacerse referencia a cadenas y otras funciones como parámetros para una función, pero las cadenas deben encerrarse entre comillas simples.</span><span class="sxs-lookup"><span data-stu-id="bc29c-107">Strings and other functions can be referenced as parameters for a function, but strings must be surrounded in single quotes.</span></span> <span data-ttu-id="bc29c-108">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bc29c-108">For example:</span></span>

```json
"[fn1(fn2(), 'foobar')]"
```

<span data-ttu-id="bc29c-109">Si procede, puede hacer referencia a propiedades de salida de hello de una función utilizando el operador de punto de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-109">Where applicable, you can reference properties of hello output of a function by using hello dot operator.</span></span> <span data-ttu-id="bc29c-110">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bc29c-110">For example:</span></span>

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a><span data-ttu-id="bc29c-111">Referencias a funciones</span><span class="sxs-lookup"><span data-stu-id="bc29c-111">Referencing functions</span></span>
<span data-ttu-id="bc29c-112">Estas funciones pueden ser salidas tooreference usado en el contexto de un CreateUiDefinition o propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-112">These functions can be used tooreference outputs from hello properties or context of a CreateUiDefinition.</span></span>

### <a name="basics"></a><span data-ttu-id="bc29c-113">basics</span><span class="sxs-lookup"><span data-stu-id="bc29c-113">basics</span></span>
<span data-ttu-id="bc29c-114">Devuelve valores de salida de hello de un elemento que se define en el paso de conceptos básicos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-114">Returns hello output values of an element that is defined in hello Basics step.</span></span>

<span data-ttu-id="bc29c-115">Hello en el ejemplo siguiente se devuelve la salida de hello elemento Hola denominado `foo` en el paso de hello conceptos básicos:</span><span class="sxs-lookup"><span data-stu-id="bc29c-115">hello following example returns hello output of hello element named `foo` in hello Basics step:</span></span>

```json
"[basics('foo')]"
```

### <a name="steps"></a><span data-ttu-id="bc29c-116">steps</span><span class="sxs-lookup"><span data-stu-id="bc29c-116">steps</span></span>
<span data-ttu-id="bc29c-117">Devuelve valores de salida de hello de un elemento que se define en el paso especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-117">Returns hello output values of an element that is defined in hello specified step.</span></span> <span data-ttu-id="bc29c-118">usar valores de salida de hello tooget de elementos en el paso de conceptos básicos de hello, `basics()` en su lugar.</span><span class="sxs-lookup"><span data-stu-id="bc29c-118">tooget hello output values of elements in hello Basics step, use `basics()` instead.</span></span>

<span data-ttu-id="bc29c-119">Hello en el ejemplo siguiente se devuelve la salida de hello elemento Hola denominado `bar` en el paso de hello denominado `foo`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-119">hello following example returns hello output of hello element named `bar` in hello step named `foo`:</span></span>

```json
"[steps('foo').bar]"
```

### <a name="location"></a><span data-ttu-id="bc29c-120">location</span><span class="sxs-lookup"><span data-stu-id="bc29c-120">location</span></span>
<span data-ttu-id="bc29c-121">Devuelve la ubicación de hello seleccionada en el paso de conceptos básicos de Hola o contexto actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-121">Returns hello location selected in hello Basics step or hello current context.</span></span>

<span data-ttu-id="bc29c-122">Hello en el ejemplo siguiente se podría devolver `"westus"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-122">hello following example could return `"westus"`:</span></span>

```json
"[location()]"
```

## <a name="string-functions"></a><span data-ttu-id="bc29c-123">Funciones de cadena</span><span class="sxs-lookup"><span data-stu-id="bc29c-123">String functions</span></span>
<span data-ttu-id="bc29c-124">Estas funciones solo se pueden usar con cadenas de JSON.</span><span class="sxs-lookup"><span data-stu-id="bc29c-124">These functions can only be used with JSON strings.</span></span>

### <a name="concat"></a><span data-ttu-id="bc29c-125">concat</span><span class="sxs-lookup"><span data-stu-id="bc29c-125">concat</span></span>
<span data-ttu-id="bc29c-126">Concatena una o varias cadenas.</span><span class="sxs-lookup"><span data-stu-id="bc29c-126">Concatenates one or more strings.</span></span>

<span data-ttu-id="bc29c-127">Por ejemplo, si el valor de salida de hello `element1` si `"bar"`, a continuación, en este ejemplo devuelve la cadena Hola `"foobar!"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-127">For example, if hello output value of `element1` if `"bar"`, then this example returns hello string `"foobar!"`:</span></span>

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a><span data-ttu-id="bc29c-128">substring</span><span class="sxs-lookup"><span data-stu-id="bc29c-128">substring</span></span>
<span data-ttu-id="bc29c-129">Devuelve Hola subcadena del programa Hola a la cadena especificada.</span><span class="sxs-lookup"><span data-stu-id="bc29c-129">Returns hello substring of hello specified string.</span></span> <span data-ttu-id="bc29c-130">subcadena de Hello comienza en el índice especificado de Hola y Hola se especifica longitud.</span><span class="sxs-lookup"><span data-stu-id="bc29c-130">hello substring starts at hello specified index and has hello specified length.</span></span>

<span data-ttu-id="bc29c-131">Devuelve de Hello en el ejemplo siguiente se `"ftw"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-131">hello following example returns `"ftw"`:</span></span>

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a><span data-ttu-id="bc29c-132">replace</span><span class="sxs-lookup"><span data-stu-id="bc29c-132">replace</span></span>
<span data-ttu-id="bc29c-133">Devuelve una cadena en la que todas las apariciones de hello la cadena especificada en la cadena actual de Hola se reemplaza por otra cadena.</span><span class="sxs-lookup"><span data-stu-id="bc29c-133">Returns a string in which all occurrences of hello specified string in hello current string are replaced with another string.</span></span>

<span data-ttu-id="bc29c-134">Devuelve de Hello en el ejemplo siguiente se `"Everything is awesome!"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-134">hello following example returns `"Everything is awesome!"`:</span></span>

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a><span data-ttu-id="bc29c-135">GUID</span><span class="sxs-lookup"><span data-stu-id="bc29c-135">guid</span></span>
<span data-ttu-id="bc29c-136">Genera una cadena única global (GUID).</span><span class="sxs-lookup"><span data-stu-id="bc29c-136">Generates a globally unique string (GUID).</span></span>

<span data-ttu-id="bc29c-137">Hello en el ejemplo siguiente se podría devolver `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-137">hello following example could return `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:</span></span>

```json
"[guid()]"
```

### <a name="tolower"></a><span data-ttu-id="bc29c-138">toLower</span><span class="sxs-lookup"><span data-stu-id="bc29c-138">toLower</span></span>
<span data-ttu-id="bc29c-139">Devuelve una cadena convertida toolowercase.</span><span class="sxs-lookup"><span data-stu-id="bc29c-139">Returns a string converted toolowercase.</span></span>

<span data-ttu-id="bc29c-140">Devuelve de Hello en el ejemplo siguiente se `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-140">hello following example returns `"foobar"`:</span></span>

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a><span data-ttu-id="bc29c-141">toUpper</span><span class="sxs-lookup"><span data-stu-id="bc29c-141">toUpper</span></span>
<span data-ttu-id="bc29c-142">Devuelve una cadena convertida toouppercase.</span><span class="sxs-lookup"><span data-stu-id="bc29c-142">Returns a string converted toouppercase.</span></span>

<span data-ttu-id="bc29c-143">Devuelve de Hello en el ejemplo siguiente se `"FOOBAR"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-143">hello following example returns `"FOOBAR"`:</span></span>

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a><span data-ttu-id="bc29c-144">Funciones de colección</span><span class="sxs-lookup"><span data-stu-id="bc29c-144">Collection functions</span></span>
<span data-ttu-id="bc29c-145">Estas funciones se pueden usar con las colecciones, como las cadenas JSON, matrices y objetos.</span><span class="sxs-lookup"><span data-stu-id="bc29c-145">These functions can be used with collections, like JSON strings, arrays and objects.</span></span>

### <a name="contains"></a><span data-ttu-id="bc29c-146">contains</span><span class="sxs-lookup"><span data-stu-id="bc29c-146">contains</span></span>
<span data-ttu-id="bc29c-147">Devuelve `true` si una cadena contiene Hola subcadena especificada, que contiene una matriz Hola valor especificado o un objeto contiene la clave especificada de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-147">Returns `true` if a string contains hello specified substring, an array contains hello specified value, or an object contains hello specified key.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="bc29c-148">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="bc29c-148">Example 1: string</span></span>
<span data-ttu-id="bc29c-149">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-149">hello following example returns `true`:</span></span>

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="bc29c-150">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="bc29c-150">Example 2: array</span></span>
<span data-ttu-id="bc29c-151">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-151">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="bc29c-152">Devuelve de Hello en el ejemplo siguiente se `false`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-152">hello following example returns `false`:</span></span>

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="bc29c-153">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="bc29c-153">Example 3: object</span></span>
<span data-ttu-id="bc29c-154">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="bc29c-154">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="bc29c-155">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-155">hello following example returns `true`:</span></span>

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a><span data-ttu-id="bc29c-156">length</span><span class="sxs-lookup"><span data-stu-id="bc29c-156">length</span></span>
<span data-ttu-id="bc29c-157">Devuelve el número de Hola de caracteres en una cadena, número de Hola de valores en una matriz o número de Hola de claves en un objeto.</span><span class="sxs-lookup"><span data-stu-id="bc29c-157">Returns hello number of characters in a string, hello number of values in an array, or hello number of keys in an object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="bc29c-158">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="bc29c-158">Example 1: string</span></span>
<span data-ttu-id="bc29c-159">Devuelve de Hello en el ejemplo siguiente se `6`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-159">hello following example returns `6`:</span></span>

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="bc29c-160">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="bc29c-160">Example 2: array</span></span>
<span data-ttu-id="bc29c-161">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-161">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="bc29c-162">Devuelve de Hello en el ejemplo siguiente se `3`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-162">hello following example returns `3`:</span></span>

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="bc29c-163">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="bc29c-163">Example 3: object</span></span>
<span data-ttu-id="bc29c-164">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="bc29c-164">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="bc29c-165">Devuelve de Hello en el ejemplo siguiente se `2`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-165">hello following example returns `2`:</span></span>

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a><span data-ttu-id="bc29c-166">empty</span><span class="sxs-lookup"><span data-stu-id="bc29c-166">empty</span></span>
<span data-ttu-id="bc29c-167">Devuelve `true` Si cadena hello, matriz u objeto es null o está vacío.</span><span class="sxs-lookup"><span data-stu-id="bc29c-167">Returns `true` if hello string, array, or object is null or empty.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="bc29c-168">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="bc29c-168">Example 1: string</span></span>
<span data-ttu-id="bc29c-169">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-169">hello following example returns `true`:</span></span>

```json
"[empty('')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="bc29c-170">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="bc29c-170">Example 2: array</span></span>
<span data-ttu-id="bc29c-171">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-171">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="bc29c-172">Devuelve de Hello en el ejemplo siguiente se `false`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-172">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="bc29c-173">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="bc29c-173">Example 3: object</span></span>
<span data-ttu-id="bc29c-174">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="bc29c-174">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="bc29c-175">Devuelve de Hello en el ejemplo siguiente se `false`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-175">hello following example returns `false`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a><span data-ttu-id="bc29c-176">Ejemplo 4: nulo y sin definir</span><span class="sxs-lookup"><span data-stu-id="bc29c-176">Example 4: null and undefined</span></span>
<span data-ttu-id="bc29c-177">Asuma que `element1` es `null` o no está definida.</span><span class="sxs-lookup"><span data-stu-id="bc29c-177">Assume `element1` is `null` or undefined.</span></span> <span data-ttu-id="bc29c-178">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-178">hello following example returns `true`:</span></span>

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a><span data-ttu-id="bc29c-179">first</span><span class="sxs-lookup"><span data-stu-id="bc29c-179">first</span></span>
<span data-ttu-id="bc29c-180">Devuelve Hola primer carácter de hello especifica cadena; primer valor de la matriz especificada de hello; o bien, Hola primera clave y el valor del objeto especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-180">Returns hello first character of hello specified string; first value of hello specified array; or hello first key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="bc29c-181">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="bc29c-181">Example 1: string</span></span>
<span data-ttu-id="bc29c-182">Devuelve de Hello en el ejemplo siguiente se `"f"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-182">hello following example returns `"f"`:</span></span>

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="bc29c-183">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="bc29c-183">Example 2: array</span></span>
<span data-ttu-id="bc29c-184">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-184">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="bc29c-185">Devuelve de Hello en el ejemplo siguiente se `1`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-185">hello following example returns `1`:</span></span>

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="bc29c-186">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="bc29c-186">Example 3: object</span></span>
<span data-ttu-id="bc29c-187">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="bc29c-187">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="bc29c-188">Devuelve de Hello en el ejemplo siguiente se `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-188">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a><span data-ttu-id="bc29c-189">last</span><span class="sxs-lookup"><span data-stu-id="bc29c-189">last</span></span>
<span data-ttu-id="bc29c-190">Devuelve Hola último carácter de hello especificado, Hola último valor de cadena Hola especificado de la matriz, u Hola última clave y el valor del objeto especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-190">Returns hello last character of hello specified string, hello last value of hello specified array, or hello last key and value of hello specified object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="bc29c-191">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="bc29c-191">Example 1: string</span></span>
<span data-ttu-id="bc29c-192">Devuelve de Hello en el ejemplo siguiente se `"r"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-192">hello following example returns `"r"`:</span></span>

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a><span data-ttu-id="bc29c-193">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="bc29c-193">Example 2: array</span></span>
<span data-ttu-id="bc29c-194">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-194">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="bc29c-195">Devuelve de Hello en el ejemplo siguiente se `2`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-195">hello following example returns `2`:</span></span>

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="bc29c-196">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="bc29c-196">Example 3: object</span></span>
<span data-ttu-id="bc29c-197">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="bc29c-197">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="bc29c-198">Devuelve de Hello en el ejemplo siguiente se `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-198">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a><span data-ttu-id="bc29c-199">take</span><span class="sxs-lookup"><span data-stu-id="bc29c-199">take</span></span>
<span data-ttu-id="bc29c-200">Devuelve un número especificado de caracteres contiguos desde el principio de Hola de cadena hello, un número especificado de valores no contiguos desde el principio de Hola de matriz de Hola o un número especificado de valores desde el inicio de hello del objeto de Hola y claves contiguas.</span><span class="sxs-lookup"><span data-stu-id="bc29c-200">Returns a specified number of contiguous characters from hello start of hello string, a specified number of contiguous values from hello start of hello array, or a specified number of contiguous keys and values from hello start of hello object.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="bc29c-201">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="bc29c-201">Example 1: string</span></span>
<span data-ttu-id="bc29c-202">Devuelve de Hello en el ejemplo siguiente se `"foo"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-202">hello following example returns `"foo"`:</span></span>

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="bc29c-203">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="bc29c-203">Example 2: array</span></span>
<span data-ttu-id="bc29c-204">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-204">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="bc29c-205">Devuelve de Hello en el ejemplo siguiente se `[1, 2]`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-205">hello following example returns `[1, 2]`:</span></span>

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="bc29c-206">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="bc29c-206">Example 3: object</span></span>
<span data-ttu-id="bc29c-207">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="bc29c-207">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

<span data-ttu-id="bc29c-208">Devuelve de Hello en el ejemplo siguiente se `{"key1": "foobar"}`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-208">hello following example returns `{"key1": "foobar"}`:</span></span>

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a><span data-ttu-id="bc29c-209">skip</span><span class="sxs-lookup"><span data-stu-id="bc29c-209">skip</span></span>
<span data-ttu-id="bc29c-210">Omite un número especificado de elementos de una colección y, a continuación, devuelve Hola elementos restantes.</span><span class="sxs-lookup"><span data-stu-id="bc29c-210">Bypasses a specified number of elements in a collection, and then returns hello remaining elements.</span></span>

#### <a name="example-1-string"></a><span data-ttu-id="bc29c-211">Ejemplo 1: cadena</span><span class="sxs-lookup"><span data-stu-id="bc29c-211">Example 1: string</span></span>
<span data-ttu-id="bc29c-212">Devuelve de Hello en el ejemplo siguiente se `"bar"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-212">hello following example returns `"bar"`:</span></span>

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a><span data-ttu-id="bc29c-213">Ejemplo 2: matriz</span><span class="sxs-lookup"><span data-stu-id="bc29c-213">Example 2: array</span></span>
<span data-ttu-id="bc29c-214">Asuma que `element1` devuelve `[1, 2, 3]`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-214">Assume `element1` returns `[1, 2, 3]`.</span></span> <span data-ttu-id="bc29c-215">Devuelve de Hello en el ejemplo siguiente se `[3]`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-215">hello following example returns `[3]`:</span></span>

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a><span data-ttu-id="bc29c-216">Ejemplo 3: objeto</span><span class="sxs-lookup"><span data-stu-id="bc29c-216">Example 3: object</span></span>
<span data-ttu-id="bc29c-217">Asuma que `element1` devuelve:</span><span class="sxs-lookup"><span data-stu-id="bc29c-217">Assume `element1` returns:</span></span>

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
<span data-ttu-id="bc29c-218">Devuelve de Hello en el ejemplo siguiente se `{"key2": "raboof"}`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-218">hello following example returns `{"key2": "raboof"}`:</span></span>

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a><span data-ttu-id="bc29c-219">Funciones lógicas</span><span class="sxs-lookup"><span data-stu-id="bc29c-219">Logical functions</span></span>
<span data-ttu-id="bc29c-220">Estas funciones se pueden usar en los condicionales.</span><span class="sxs-lookup"><span data-stu-id="bc29c-220">These functions can be used in conditionals.</span></span> <span data-ttu-id="bc29c-221">Algunas funciones pueden no admitir todos los tipos de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="bc29c-221">Some functions may not support all JSON data types.</span></span>

### <a name="equals"></a><span data-ttu-id="bc29c-222">equals</span><span class="sxs-lookup"><span data-stu-id="bc29c-222">equals</span></span>
<span data-ttu-id="bc29c-223">Devuelve `true` si ambos parámetros tienen Hola mismo tipo y valor.</span><span class="sxs-lookup"><span data-stu-id="bc29c-223">Returns `true` if both parameters have hello same type and value.</span></span> <span data-ttu-id="bc29c-224">Algunas funciones admiten todos los tipos de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="bc29c-224">This function supports all JSON data types.</span></span>

<span data-ttu-id="bc29c-225">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-225">hello following example returns `true`:</span></span>

```json
"[equals(0, 0)]"
```

<span data-ttu-id="bc29c-226">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-226">hello following example returns `true`:</span></span>

```json
"[equals('foo', 'foo')]"
```

<span data-ttu-id="bc29c-227">Devuelve de Hello en el ejemplo siguiente se `false`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-227">hello following example returns `false`:</span></span>

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a><span data-ttu-id="bc29c-228">less</span><span class="sxs-lookup"><span data-stu-id="bc29c-228">less</span></span>
<span data-ttu-id="bc29c-229">Devuelve `true` si Hola primer parámetro es estrictamente menor que el segundo parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-229">Returns `true` if hello first parameter is strictly less than hello second parameter.</span></span> <span data-ttu-id="bc29c-230">Esta función admite parámetros solo de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-230">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="bc29c-231">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-231">hello following example returns `true`:</span></span>

```json
"[less(1, 2)]"
```

<span data-ttu-id="bc29c-232">Devuelve de Hello en el ejemplo siguiente se `false`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-232">hello following example returns `false`:</span></span>

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a><span data-ttu-id="bc29c-233">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="bc29c-233">lessOrEquals</span></span>
<span data-ttu-id="bc29c-234">Devuelve `true` si Hola primer parámetro es menor o igual toohello segundo parámetro.</span><span class="sxs-lookup"><span data-stu-id="bc29c-234">Returns `true` if hello first parameter is less than or equal toohello second parameter.</span></span> <span data-ttu-id="bc29c-235">Esta función admite parámetros solo de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-235">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="bc29c-236">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-236">hello following example returns `true`:</span></span>

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a><span data-ttu-id="bc29c-237">greater</span><span class="sxs-lookup"><span data-stu-id="bc29c-237">greater</span></span>
<span data-ttu-id="bc29c-238">Devuelve `true` si Hola primer parámetro es estrictamente mayor que el segundo parámetro de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-238">Returns `true` if hello first parameter is strictly greater than hello second parameter.</span></span> <span data-ttu-id="bc29c-239">Esta función admite parámetros solo de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-239">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="bc29c-240">Devuelve de Hello en el ejemplo siguiente se `false`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-240">hello following example returns `false`:</span></span>

```json
"[greater(1, 2)]"
```

<span data-ttu-id="bc29c-241">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-241">hello following example returns `true`:</span></span>

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a><span data-ttu-id="bc29c-242">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="bc29c-242">greaterOrEquals</span></span>
<span data-ttu-id="bc29c-243">Devuelve `true` si Hola primer parámetro es igual o mayor que toohello segundo parámetro.</span><span class="sxs-lookup"><span data-stu-id="bc29c-243">Returns `true` if hello first parameter is greater than or equal toohello second parameter.</span></span> <span data-ttu-id="bc29c-244">Esta función admite parámetros solo de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-244">This function supports parameters only of type number and string.</span></span>

<span data-ttu-id="bc29c-245">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-245">hello following example returns `true`:</span></span>

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a><span data-ttu-id="bc29c-246">y</span><span class="sxs-lookup"><span data-stu-id="bc29c-246">and</span></span>
<span data-ttu-id="bc29c-247">Devuelve `true` si todos los parámetros de hello evaluación demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-247">Returns `true` if all hello parameters evaluate too`true`.</span></span> <span data-ttu-id="bc29c-248">Esta función admite dos o más parámetros solo de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="bc29c-248">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="bc29c-249">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-249">hello following example returns `true`:</span></span>

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="bc29c-250">Devuelve de Hello en el ejemplo siguiente se `false`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-250">hello following example returns `false`:</span></span>

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a><span data-ttu-id="bc29c-251">o</span><span class="sxs-lookup"><span data-stu-id="bc29c-251">or</span></span>
<span data-ttu-id="bc29c-252">Devuelve `true` si al menos uno de los parámetros de hello da como resultado demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-252">Returns `true` if at least one of hello parameters evaluates too`true`.</span></span> <span data-ttu-id="bc29c-253">Esta función admite dos o más parámetros solo de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="bc29c-253">This function supports two or more parameters only of type Boolean.</span></span>

<span data-ttu-id="bc29c-254">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-254">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

<span data-ttu-id="bc29c-255">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-255">hello following example returns `true`:</span></span>

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a><span data-ttu-id="bc29c-256">not</span><span class="sxs-lookup"><span data-stu-id="bc29c-256">not</span></span>
<span data-ttu-id="bc29c-257">Devuelve `true` si parámetro hello da como resultado demasiado`false`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-257">Returns `true` if hello parameter evaluates too`false`.</span></span> <span data-ttu-id="bc29c-258">Esta función admite parámetros solo de tipo booleano.</span><span class="sxs-lookup"><span data-stu-id="bc29c-258">This function supports parameters only of type Boolean.</span></span>

<span data-ttu-id="bc29c-259">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-259">hello following example returns `true`:</span></span>

```json
"[not(false)]"
```

<span data-ttu-id="bc29c-260">Devuelve de Hello en el ejemplo siguiente se `false`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-260">hello following example returns `false`:</span></span>

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a><span data-ttu-id="bc29c-261">coalesce</span><span class="sxs-lookup"><span data-stu-id="bc29c-261">coalesce</span></span>
<span data-ttu-id="bc29c-262">Devuelve Hola valor del parámetro no null de la primera Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-262">Returns hello value of hello first non-null parameter.</span></span> <span data-ttu-id="bc29c-263">Algunas funciones admiten todos los tipos de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="bc29c-263">This function supports all JSON data types.</span></span>

<span data-ttu-id="bc29c-264">Asuma que `element1` y `element2` son indefinidos.</span><span class="sxs-lookup"><span data-stu-id="bc29c-264">Assume `element1` and `element2` are undefined.</span></span> <span data-ttu-id="bc29c-265">Devuelve de Hello en el ejemplo siguiente se `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-265">hello following example returns `"foobar"`:</span></span>

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a><span data-ttu-id="bc29c-266">Funciones de conversión</span><span class="sxs-lookup"><span data-stu-id="bc29c-266">Conversion functions</span></span>
<span data-ttu-id="bc29c-267">Estas funciones pueden ser valores de uso tooconvert entre la codificación y tipos de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="bc29c-267">These functions can be used tooconvert values between JSON data types and encodings.</span></span>

### <a name="int"></a><span data-ttu-id="bc29c-268">int</span><span class="sxs-lookup"><span data-stu-id="bc29c-268">int</span></span>
<span data-ttu-id="bc29c-269">Convierte el entero de hello parámetro tooan.</span><span class="sxs-lookup"><span data-stu-id="bc29c-269">Converts hello parameter tooan integer.</span></span> <span data-ttu-id="bc29c-270">Esta función admite parámetros de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-270">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="bc29c-271">Devuelve de Hello en el ejemplo siguiente se `1`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-271">hello following example returns `1`:</span></span>

```json
"[int('1')]"
```

<span data-ttu-id="bc29c-272">Devuelve de Hello en el ejemplo siguiente se `2`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-272">hello following example returns `2`:</span></span>

```json
"[int(2.9)]"
```

### <a name="float"></a><span data-ttu-id="bc29c-273">float</span><span class="sxs-lookup"><span data-stu-id="bc29c-273">float</span></span>
<span data-ttu-id="bc29c-274">Convierte Hola parámetro tooa punto flotante.</span><span class="sxs-lookup"><span data-stu-id="bc29c-274">Converts hello parameter tooa floating-point.</span></span> <span data-ttu-id="bc29c-275">Esta función admite parámetros de tipo number y string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-275">This function supports parameters of type number and string.</span></span>

<span data-ttu-id="bc29c-276">Devuelve de Hello en el ejemplo siguiente se `1.0`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-276">hello following example returns `1.0`:</span></span>

```json
"[float('1.0')]"
```

<span data-ttu-id="bc29c-277">Devuelve de Hello en el ejemplo siguiente se `2.9`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-277">hello following example returns `2.9`:</span></span>

```json
"[float(2.9)]"
```

### <a name="string"></a><span data-ttu-id="bc29c-278">cadena</span><span class="sxs-lookup"><span data-stu-id="bc29c-278">string</span></span>
<span data-ttu-id="bc29c-279">Convierte la cadena de tooa de parámetros de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-279">Converts hello parameter tooa string.</span></span> <span data-ttu-id="bc29c-280">Esta función admite parámetros de todos los tipos de datos JSON.</span><span class="sxs-lookup"><span data-stu-id="bc29c-280">This function supports parameters of all JSON data types.</span></span>

<span data-ttu-id="bc29c-281">Devuelve de Hello en el ejemplo siguiente se `"1"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-281">hello following example returns `"1"`:</span></span>

```json
"[string(1)]"
```

<span data-ttu-id="bc29c-282">Devuelve de Hello en el ejemplo siguiente se `"2.9"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-282">hello following example returns `"2.9"`:</span></span>

```json
"[string(2.9)]"
```

<span data-ttu-id="bc29c-283">Devuelve de Hello en el ejemplo siguiente se `"[1,2,3]"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-283">hello following example returns `"[1,2,3]"`:</span></span>

```json
"[string([1,2,3])]"
```

<span data-ttu-id="bc29c-284">Devuelve de Hello en el ejemplo siguiente se `"{"foo":"bar"}"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-284">hello following example returns `"{"foo":"bar"}"`:</span></span>

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a><span data-ttu-id="bc29c-285">booleano</span><span class="sxs-lookup"><span data-stu-id="bc29c-285">bool</span></span>
<span data-ttu-id="bc29c-286">Convierte Hola parámetro tooa un valor booleano.</span><span class="sxs-lookup"><span data-stu-id="bc29c-286">Converts hello parameter tooa Boolean.</span></span> <span data-ttu-id="bc29c-287">Esta función admite parámetros de tipo number, string y booleano.</span><span class="sxs-lookup"><span data-stu-id="bc29c-287">This function supports parameters of type number, string, and Boolean.</span></span> <span data-ttu-id="bc29c-288">TooBooleans similar en JavaScript, cualquier valor excepto `0` o `'false'` devuelve `true`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-288">Similar tooBooleans in JavaScript, any value except `0` or `'false'` returns `true`.</span></span>

<span data-ttu-id="bc29c-289">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-289">hello following example returns `true`:</span></span>

```json
"[bool(1)]"
```

<span data-ttu-id="bc29c-290">Devuelve de Hello en el ejemplo siguiente se `false`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-290">hello following example returns `false`:</span></span>

```json
"[bool(0)]"
```

<span data-ttu-id="bc29c-291">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-291">hello following example returns `true`:</span></span>

```json
"[bool(true)]"
```

<span data-ttu-id="bc29c-292">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-292">hello following example returns `true`:</span></span>

```json
"[bool('true')]"
```

### <a name="parse"></a><span data-ttu-id="bc29c-293">parse</span><span class="sxs-lookup"><span data-stu-id="bc29c-293">parse</span></span>
<span data-ttu-id="bc29c-294">Convierte a un tipo nativo Hola parámetro tooa.</span><span class="sxs-lookup"><span data-stu-id="bc29c-294">Converts hello parameter tooa native type.</span></span> <span data-ttu-id="bc29c-295">En otras palabras, esta función es el inverso de Hola de `string()`.</span><span class="sxs-lookup"><span data-stu-id="bc29c-295">In other words, this function is hello inverse of `string()`.</span></span> <span data-ttu-id="bc29c-296">Esta función admite parámetros solo de tipo string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-296">This function supports parameters only of type string.</span></span>

<span data-ttu-id="bc29c-297">Devuelve de Hello en el ejemplo siguiente se `1`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-297">hello following example returns `1`:</span></span>

```json
"[parse('1')]"
```

<span data-ttu-id="bc29c-298">Devuelve de Hello en el ejemplo siguiente se `true`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-298">hello following example returns `true`:</span></span>

```json
"[parse('true')]"
```

<span data-ttu-id="bc29c-299">Devuelve de Hello en el ejemplo siguiente se `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-299">hello following example returns `[1,2,3]`:</span></span>

```json
"[parse('[1,2,3]')]"
```

<span data-ttu-id="bc29c-300">Devuelve de Hello en el ejemplo siguiente se `{"foo":"bar"}`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-300">hello following example returns `{"foo":"bar"}`:</span></span>

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a><span data-ttu-id="bc29c-301">encodeBase64</span><span class="sxs-lookup"><span data-stu-id="bc29c-301">encodeBase64</span></span>
<span data-ttu-id="bc29c-302">Codifica la cadena codificada en base 64 Hola parámetro tooa.</span><span class="sxs-lookup"><span data-stu-id="bc29c-302">Encodes hello parameter tooa base-64 encoded string.</span></span> <span data-ttu-id="bc29c-303">Esta función admite parámetros solo de tipo string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-303">This function supports parameters only of type string.</span></span>

<span data-ttu-id="bc29c-304">Devuelve de Hello en el ejemplo siguiente se `"Zm9vYmFy"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-304">hello following example returns `"Zm9vYmFy"`:</span></span>

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a><span data-ttu-id="bc29c-305">decodeBase64</span><span class="sxs-lookup"><span data-stu-id="bc29c-305">decodeBase64</span></span>
<span data-ttu-id="bc29c-306">Descodifica el parámetro hello desde una cadena codificada en base 64.</span><span class="sxs-lookup"><span data-stu-id="bc29c-306">Decodes hello parameter from a base-64 encoded string.</span></span> <span data-ttu-id="bc29c-307">Esta función admite parámetros solo de tipo string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-307">This function supports parameters only of type string.</span></span>

<span data-ttu-id="bc29c-308">Devuelve de Hello en el ejemplo siguiente se `"foobar"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-308">hello following example returns `"foobar"`:</span></span>

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a><span data-ttu-id="bc29c-309">encodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="bc29c-309">encodeUriComponent</span></span>
<span data-ttu-id="bc29c-310">Codifica la cadena de dirección URL codificada de hello parámetros tooa.</span><span class="sxs-lookup"><span data-stu-id="bc29c-310">Encodes hello parameter tooa URL encoded string.</span></span> <span data-ttu-id="bc29c-311">Esta función admite parámetros solo de tipo string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-311">This function supports parameters only of type string.</span></span>

<span data-ttu-id="bc29c-312">Devuelve de Hello en el ejemplo siguiente se `"https%3A%2F%2Fportal.azure.com%2F"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-312">hello following example returns `"https%3A%2F%2Fportal.azure.com%2F"`:</span></span>

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a><span data-ttu-id="bc29c-313">decodeUriComponent</span><span class="sxs-lookup"><span data-stu-id="bc29c-313">decodeUriComponent</span></span>
<span data-ttu-id="bc29c-314">Descodifica el parámetro hello de una cadena de dirección URL codificada.</span><span class="sxs-lookup"><span data-stu-id="bc29c-314">Decodes hello parameter from a URL encoded string.</span></span> <span data-ttu-id="bc29c-315">Esta función admite parámetros solo de tipo string.</span><span class="sxs-lookup"><span data-stu-id="bc29c-315">This function supports parameters only of type string.</span></span>

<span data-ttu-id="bc29c-316">Devuelve de Hello en el ejemplo siguiente se `"https://portal.azure.com/"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-316">hello following example returns `"https://portal.azure.com/"`:</span></span>

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a><span data-ttu-id="bc29c-317">Funciones matemáticas</span><span class="sxs-lookup"><span data-stu-id="bc29c-317">Math functions</span></span>
### <a name="add"></a><span data-ttu-id="bc29c-318">agregar</span><span class="sxs-lookup"><span data-stu-id="bc29c-318">add</span></span>
<span data-ttu-id="bc29c-319">Suma dos números y devuelve el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="bc29c-319">Adds two numbers, and returns hello result.</span></span>

<span data-ttu-id="bc29c-320">Devuelve de Hello en el ejemplo siguiente se `3`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-320">hello following example returns `3`:</span></span>

```json
"[add(1, 2)]"
```

### <a name="sub"></a><span data-ttu-id="bc29c-321">sub</span><span class="sxs-lookup"><span data-stu-id="bc29c-321">sub</span></span>
<span data-ttu-id="bc29c-322">Resta Hola segundo número desde el primer número de Hola y devuelve el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="bc29c-322">Subtracts hello second number from hello first number, and returns hello result.</span></span>

<span data-ttu-id="bc29c-323">Devuelve de Hello en el ejemplo siguiente se `1`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-323">hello following example returns `1`:</span></span>

```json
"[sub(3, 2)]"
```

### <a name="mul"></a><span data-ttu-id="bc29c-324">mul</span><span class="sxs-lookup"><span data-stu-id="bc29c-324">mul</span></span>
<span data-ttu-id="bc29c-325">Multiplica a dos números y devuelve el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="bc29c-325">Multiplies two numbers, and returns hello result.</span></span>

<span data-ttu-id="bc29c-326">Devuelve de Hello en el ejemplo siguiente se `6`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-326">hello following example returns `6`:</span></span>

```json
"[mul(2, 3)]"
```

### <a name="div"></a><span data-ttu-id="bc29c-327">div</span><span class="sxs-lookup"><span data-stu-id="bc29c-327">div</span></span>
<span data-ttu-id="bc29c-328">Divide Hola primer número por segundo número de Hola y devuelve el resultado de hello.</span><span class="sxs-lookup"><span data-stu-id="bc29c-328">Divides hello first number by hello second number, and returns hello result.</span></span> <span data-ttu-id="bc29c-329">resultado de Hello siempre es un entero.</span><span class="sxs-lookup"><span data-stu-id="bc29c-329">hello result is always an integer.</span></span>

<span data-ttu-id="bc29c-330">Devuelve de Hello en el ejemplo siguiente se `2`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-330">hello following example returns `2`:</span></span>

```json
"[div(6, 3)]"
```

### <a name="mod"></a><span data-ttu-id="bc29c-331">mod</span><span class="sxs-lookup"><span data-stu-id="bc29c-331">mod</span></span>
<span data-ttu-id="bc29c-332">Divide Hola primer número por segundo número de Hola y devuelve el resto de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-332">Divides hello first number by hello second number, and returns hello remainder.</span></span>

<span data-ttu-id="bc29c-333">Devuelve de Hello en el ejemplo siguiente se `0`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-333">hello following example returns `0`:</span></span>

```json
"[mod(6, 3)]"
```

<span data-ttu-id="bc29c-334">Devuelve de Hello en el ejemplo siguiente se `2`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-334">hello following example returns `2`:</span></span>

```json
"[mod(6, 4)]"
```

### <a name="min"></a><span data-ttu-id="bc29c-335">Min</span><span class="sxs-lookup"><span data-stu-id="bc29c-335">min</span></span>
<span data-ttu-id="bc29c-336">Devuelve Hola pequeño de números de hello dos.</span><span class="sxs-lookup"><span data-stu-id="bc29c-336">Returns hello small of hello two numbers.</span></span>

<span data-ttu-id="bc29c-337">Devuelve de Hello en el ejemplo siguiente se `1`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-337">hello following example returns `1`:</span></span>

```json
"[min(1, 2)]"
```

### <a name="max"></a><span data-ttu-id="bc29c-338">max</span><span class="sxs-lookup"><span data-stu-id="bc29c-338">max</span></span>
<span data-ttu-id="bc29c-339">Hola de devuelve mayor de dos números de Hola.</span><span class="sxs-lookup"><span data-stu-id="bc29c-339">Returns hello larger of hello two numbers.</span></span>

<span data-ttu-id="bc29c-340">Devuelve de Hello en el ejemplo siguiente se `2`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-340">hello following example returns `2`:</span></span>

```json
"[max(1, 2)]"
```

### <a name="range"></a><span data-ttu-id="bc29c-341">range</span><span class="sxs-lookup"><span data-stu-id="bc29c-341">range</span></span>
<span data-ttu-id="bc29c-342">Genera una secuencia de entero especificado de números dentro de hello intervalo.</span><span class="sxs-lookup"><span data-stu-id="bc29c-342">Generates a sequence of integral numbers within hello specified range.</span></span>

<span data-ttu-id="bc29c-343">Devuelve de Hello en el ejemplo siguiente se `[1,2,3]`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-343">hello following example returns `[1,2,3]`:</span></span>

```json
"[range(1, 3)]"
```

### <a name="rand"></a><span data-ttu-id="bc29c-344">rand</span><span class="sxs-lookup"><span data-stu-id="bc29c-344">rand</span></span>
<span data-ttu-id="bc29c-345">Devuelve un aleatorio número integral de hello especifica el intervalo.</span><span class="sxs-lookup"><span data-stu-id="bc29c-345">Returns a random integral number within hello specified range.</span></span> <span data-ttu-id="bc29c-346">Esta función no genera números aleatorios criptográficamente seguros.</span><span class="sxs-lookup"><span data-stu-id="bc29c-346">This function does not generate cryptographically secure random numbers.</span></span>

<span data-ttu-id="bc29c-347">Hello en el ejemplo siguiente se podría devolver `42`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-347">hello following example could return `42`:</span></span>

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a><span data-ttu-id="bc29c-348">floor</span><span class="sxs-lookup"><span data-stu-id="bc29c-348">floor</span></span>
<span data-ttu-id="bc29c-349">Devuelve Hola mayor entero menor o igual toohello del número especificado.</span><span class="sxs-lookup"><span data-stu-id="bc29c-349">Returns hello largest integer less than or equal toohello specified number.</span></span>

<span data-ttu-id="bc29c-350">Devuelve de Hello en el ejemplo siguiente se `3`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-350">hello following example returns `3`:</span></span>

```json
"[floor(3.14)]"
```

### <a name="ceil"></a><span data-ttu-id="bc29c-351">ceil</span><span class="sxs-lookup"><span data-stu-id="bc29c-351">ceil</span></span>
<span data-ttu-id="bc29c-352">Devuelve Hola mayor número entero mayor que o igual toohello del número especificado.</span><span class="sxs-lookup"><span data-stu-id="bc29c-352">Returns hello largest integer greater than or equal toohello specified number.</span></span>

<span data-ttu-id="bc29c-353">Devuelve de Hello en el ejemplo siguiente se `4`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-353">hello following example returns `4`:</span></span>

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a><span data-ttu-id="bc29c-354">Funciones de fecha</span><span class="sxs-lookup"><span data-stu-id="bc29c-354">Date functions</span></span>
### <a name="utcnow"></a><span data-ttu-id="bc29c-355">utcNow</span><span class="sxs-lookup"><span data-stu-id="bc29c-355">utcNow</span></span>
<span data-ttu-id="bc29c-356">Devuelve una cadena en formato ISO 8601 de hello fecha y hora en el equipo local de hello actual.</span><span class="sxs-lookup"><span data-stu-id="bc29c-356">Returns a string in ISO 8601 format of hello current date and time on hello local computer.</span></span>

<span data-ttu-id="bc29c-357">Hello en el ejemplo siguiente se podría devolver `"1990-12-31T23:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-357">hello following example could return `"1990-12-31T23:59:59.000Z"`:</span></span>

```json
"[utcNow()]"
```

### <a name="addseconds"></a><span data-ttu-id="bc29c-358">addSeconds</span><span class="sxs-lookup"><span data-stu-id="bc29c-358">addSeconds</span></span>
<span data-ttu-id="bc29c-359">Agrega un número integral de toohello de segundos especificado marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="bc29c-359">Adds an integral number of seconds toohello specified timestamp.</span></span>

<span data-ttu-id="bc29c-360">Devuelve de Hello en el ejemplo siguiente se `"1991-01-01T00:00:00.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-360">hello following example returns `"1991-01-01T00:00:00.000Z"`:</span></span>

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a><span data-ttu-id="bc29c-361">addMinutes</span><span class="sxs-lookup"><span data-stu-id="bc29c-361">addMinutes</span></span>
<span data-ttu-id="bc29c-362">Agrega un número integral de toohello de minutos especificado marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="bc29c-362">Adds an integral number of minutes toohello specified timestamp.</span></span>

<span data-ttu-id="bc29c-363">Devuelve de Hello en el ejemplo siguiente se `"1991-01-01T00:00:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-363">hello following example returns `"1991-01-01T00:00:59.000Z"`:</span></span>

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a><span data-ttu-id="bc29c-364">addHours</span><span class="sxs-lookup"><span data-stu-id="bc29c-364">addHours</span></span>
<span data-ttu-id="bc29c-365">Agrega un número integral de toohello de horas especificado marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="bc29c-365">Adds an integral number of hours toohello specified timestamp.</span></span>

<span data-ttu-id="bc29c-366">Devuelve de Hello en el ejemplo siguiente se `"1991-01-01T00:59:59.000Z"`:</span><span class="sxs-lookup"><span data-stu-id="bc29c-366">hello following example returns `"1991-01-01T00:59:59.000Z"`:</span></span>

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a><span data-ttu-id="bc29c-367">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bc29c-367">Next steps</span></span>
* <span data-ttu-id="bc29c-368">Para un administrador de recursos de introducción tooAzure, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc29c-368">For an introduction tooAzure Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

