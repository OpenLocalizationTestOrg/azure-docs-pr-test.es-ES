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
# <a name="createuidefinition-functions"></a>Funciones CreateUiDefinition
Esta sección contiene las firmas de Hola para todas las funciones compatibles de un CreateUiDefinition.

toouse una función de la declaración de hello rodear con corchetes. Por ejemplo:

```json
"[function()]"
```

Puede hacerse referencia a cadenas y otras funciones como parámetros para una función, pero las cadenas deben encerrarse entre comillas simples. Por ejemplo:

```json
"[fn1(fn2(), 'foobar')]"
```

Si procede, puede hacer referencia a propiedades de salida de hello de una función utilizando el operador de punto de Hola. Por ejemplo:

```json
"[func().prop1]"
```

## <a name="referencing-functions"></a>Referencias a funciones
Estas funciones pueden ser salidas tooreference usado en el contexto de un CreateUiDefinition o propiedades de Hola.

### <a name="basics"></a>basics
Devuelve valores de salida de hello de un elemento que se define en el paso de conceptos básicos de Hola.

Hello en el ejemplo siguiente se devuelve la salida de hello elemento Hola denominado `foo` en el paso de hello conceptos básicos:

```json
"[basics('foo')]"
```

### <a name="steps"></a>steps
Devuelve valores de salida de hello de un elemento que se define en el paso especificado Hola. usar valores de salida de hello tooget de elementos en el paso de conceptos básicos de hello, `basics()` en su lugar.

Hello en el ejemplo siguiente se devuelve la salida de hello elemento Hola denominado `bar` en el paso de hello denominado `foo`:

```json
"[steps('foo').bar]"
```

### <a name="location"></a>location
Devuelve la ubicación de hello seleccionada en el paso de conceptos básicos de Hola o contexto actual de Hola.

Hello en el ejemplo siguiente se podría devolver `"westus"`:

```json
"[location()]"
```

## <a name="string-functions"></a>Funciones de cadena
Estas funciones solo se pueden usar con cadenas de JSON.

### <a name="concat"></a>concat
Concatena una o varias cadenas.

Por ejemplo, si el valor de salida de hello `element1` si `"bar"`, a continuación, en este ejemplo devuelve la cadena Hola `"foobar!"`:

```json
"[concat('foo', steps('step1').element1), '!']"
```

### <a name="substring"></a>substring
Devuelve Hola subcadena del programa Hola a la cadena especificada. subcadena de Hello comienza en el índice especificado de Hola y Hola se especifica longitud.

Devuelve de Hello en el ejemplo siguiente se `"ftw"`:

```json
"[substring('azure-ftw!!!1one', 6, 3)]"
```

### <a name="replace"></a>replace
Devuelve una cadena en la que todas las apariciones de hello la cadena especificada en la cadena actual de Hola se reemplaza por otra cadena.

Devuelve de Hello en el ejemplo siguiente se `"Everything is awesome!"`:

```json
"[replace('Everything is terrible!', 'terrible', 'awesome')]"
```

### <a name="guid"></a>GUID
Genera una cadena única global (GUID).

Hello en el ejemplo siguiente se podría devolver `"c7bc8bdc-7252-4a82-ba53-7c468679a511"`:

```json
"[guid()]"
```

### <a name="tolower"></a>toLower
Devuelve una cadena convertida toolowercase.

Devuelve de Hello en el ejemplo siguiente se `"foobar"`:

```json
"[toLower('FOOBAR')]"
```

### <a name="toupper"></a>toUpper
Devuelve una cadena convertida toouppercase.

Devuelve de Hello en el ejemplo siguiente se `"FOOBAR"`:

```json
"[toUpper('foobar')]"
```

## <a name="collection-functions"></a>Funciones de colección
Estas funciones se pueden usar con las colecciones, como las cadenas JSON, matrices y objetos.

### <a name="contains"></a>contains
Devuelve `true` si una cadena contiene Hola subcadena especificada, que contiene una matriz Hola valor especificado o un objeto contiene la clave especificada de Hola.

#### <a name="example-1-string"></a>Ejemplo 1: cadena
Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[contains('foobar', 'foo')]"
```

#### <a name="example-2-array"></a>Ejemplo 2: matriz
Asuma que `element1` devuelve `[1, 2, 3]`. Devuelve de Hello en el ejemplo siguiente se `false`:

```json
"[contains(steps('foo').element1, 4)]"
```

#### <a name="example-3-object"></a>Ejemplo 3: objeto
Asuma que `element1` devuelve:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[contains(steps('foo').element1, 'key1')]"
```

### <a name="length"></a>length
Devuelve el número de Hola de caracteres en una cadena, número de Hola de valores en una matriz o número de Hola de claves en un objeto.

#### <a name="example-1-string"></a>Ejemplo 1: cadena
Devuelve de Hello en el ejemplo siguiente se `6`:

```json
"[length('foobar')]"
```

#### <a name="example-2-array"></a>Ejemplo 2: matriz
Asuma que `element1` devuelve `[1, 2, 3]`. Devuelve de Hello en el ejemplo siguiente se `3`:

```json
"[length(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Ejemplo 3: objeto
Asuma que `element1` devuelve:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Devuelve de Hello en el ejemplo siguiente se `2`:

```json
"[length(steps('foo').element1)]"
```

### <a name="empty"></a>empty
Devuelve `true` Si cadena hello, matriz u objeto es null o está vacío.

#### <a name="example-1-string"></a>Ejemplo 1: cadena
Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[empty('')]"
```

#### <a name="example-2-array"></a>Ejemplo 2: matriz
Asuma que `element1` devuelve `[1, 2, 3]`. Devuelve de Hello en el ejemplo siguiente se `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Ejemplo 3: objeto
Asuma que `element1` devuelve:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Devuelve de Hello en el ejemplo siguiente se `false`:

```json
"[empty(steps('foo').element1)]"
```

#### <a name="example-4-null-and-undefined"></a>Ejemplo 4: nulo y sin definir
Asuma que `element1` es `null` o no está definida. Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[empty(steps('foo').element1)]"
```

### <a name="first"></a>first
Devuelve Hola primer carácter de hello especifica cadena; primer valor de la matriz especificada de hello; o bien, Hola primera clave y el valor del objeto especificado de Hola.

#### <a name="example-1-string"></a>Ejemplo 1: cadena
Devuelve de Hello en el ejemplo siguiente se `"f"`:

```json
"[first('foobar')]"
```

#### <a name="example-2-array"></a>Ejemplo 2: matriz
Asuma que `element1` devuelve `[1, 2, 3]`. Devuelve de Hello en el ejemplo siguiente se `1`:

```json
"[first(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Ejemplo 3: objeto
Asuma que `element1` devuelve:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Devuelve de Hello en el ejemplo siguiente se `{"key1": "foobar"}`:

```json
"[first(steps('foo').element1)]"
```

### <a name="last"></a>last
Devuelve Hola último carácter de hello especificado, Hola último valor de cadena Hola especificado de la matriz, u Hola última clave y el valor del objeto especificado de Hola.

#### <a name="example-1-string"></a>Ejemplo 1: cadena
Devuelve de Hello en el ejemplo siguiente se `"r"`:

```json
"[last('foobar')]"
```

#### <a name="example-2-array"></a>Ejemplo 2: matriz
Asuma que `element1` devuelve `[1, 2, 3]`. Devuelve de Hello en el ejemplo siguiente se `2`:

```json
"[last(steps('foo').element1)]"
```

#### <a name="example-3-object"></a>Ejemplo 3: objeto
Asuma que `element1` devuelve:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Devuelve de Hello en el ejemplo siguiente se `{"key2": "raboof"}`:

```json
"[last(steps('foo').element1)]"
```

### <a name="take"></a>take
Devuelve un número especificado de caracteres contiguos desde el principio de Hola de cadena hello, un número especificado de valores no contiguos desde el principio de Hola de matriz de Hola o un número especificado de valores desde el inicio de hello del objeto de Hola y claves contiguas.

#### <a name="example-1-string"></a>Ejemplo 1: cadena
Devuelve de Hello en el ejemplo siguiente se `"foo"`:

```json
"[take('foobar', 3)]"
```

#### <a name="example-2-array"></a>Ejemplo 2: matriz
Asuma que `element1` devuelve `[1, 2, 3]`. Devuelve de Hello en el ejemplo siguiente se `[1, 2]`:

```json
"[take(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Ejemplo 3: objeto
Asuma que `element1` devuelve:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```

Devuelve de Hello en el ejemplo siguiente se `{"key1": "foobar"}`:

```json
"[take(steps('foo').element1, 1)]"
```

### <a name="skip"></a>skip
Omite un número especificado de elementos de una colección y, a continuación, devuelve Hola elementos restantes.

#### <a name="example-1-string"></a>Ejemplo 1: cadena
Devuelve de Hello en el ejemplo siguiente se `"bar"`:

```json
"[skip('foobar', 3)]"
```

#### <a name="example-2-array"></a>Ejemplo 2: matriz
Asuma que `element1` devuelve `[1, 2, 3]`. Devuelve de Hello en el ejemplo siguiente se `[3]`:

```json
"[skip(steps('foo').element1, 2)]"
```

#### <a name="example-3-object"></a>Ejemplo 3: objeto
Asuma que `element1` devuelve:

```json
{
  "key1": "foobar",
  "key2": "raboof"
}
```
Devuelve de Hello en el ejemplo siguiente se `{"key2": "raboof"}`:

```json
"[skip(steps('foo').element1, 1)]"
```

## <a name="logical-functions"></a>Funciones lógicas
Estas funciones se pueden usar en los condicionales. Algunas funciones pueden no admitir todos los tipos de datos JSON.

### <a name="equals"></a>equals
Devuelve `true` si ambos parámetros tienen Hola mismo tipo y valor. Algunas funciones admiten todos los tipos de datos JSON.

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[equals(0, 0)]"
```

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[equals('foo', 'foo')]"
```

Devuelve de Hello en el ejemplo siguiente se `false`:

```json
"[equals('abc', ['a', 'b', 'c'])]"
```

### <a name="less"></a>less
Devuelve `true` si Hola primer parámetro es estrictamente menor que el segundo parámetro de Hola. Esta función admite parámetros solo de tipo number y string.

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[less(1, 2)]"
```

Devuelve de Hello en el ejemplo siguiente se `false`:

```json
"[less('9', '10')]"
```

### <a name="lessorequals"></a>lessOrEquals
Devuelve `true` si Hola primer parámetro es menor o igual toohello segundo parámetro. Esta función admite parámetros solo de tipo number y string.

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[lessOrEquals(2, 2)]"
```

### <a name="greater"></a>greater
Devuelve `true` si Hola primer parámetro es estrictamente mayor que el segundo parámetro de Hola. Esta función admite parámetros solo de tipo number y string.

Devuelve de Hello en el ejemplo siguiente se `false`:

```json
"[greater(1, 2)]"
```

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[greater('9', '10')]"
```

### <a name="greaterorequals"></a>greaterOrEquals
Devuelve `true` si Hola primer parámetro es igual o mayor que toohello segundo parámetro. Esta función admite parámetros solo de tipo number y string.

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[greaterOrEquals(2, 2)]"
```

### <a name="and"></a>y
Devuelve `true` si todos los parámetros de hello evaluación demasiado`true`. Esta función admite dos o más parámetros solo de tipo booleano.

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[and(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Devuelve de Hello en el ejemplo siguiente se `false`:

```json
"[and(equals(0, 0), greater(1, 2))]"
```

### <a name="or"></a>o
Devuelve `true` si al menos uno de los parámetros de hello da como resultado demasiado`true`. Esta función admite dos o más parámetros solo de tipo booleano.

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[or(equals(0, 0), equals('foo', 'foo'), less(1, 2))]"
```

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[or(equals(0, 0), greater(1, 2))]"
```

### <a name="not"></a>not
Devuelve `true` si parámetro hello da como resultado demasiado`false`. Esta función admite parámetros solo de tipo booleano.

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[not(false)]"
```

Devuelve de Hello en el ejemplo siguiente se `false`:

```json
"[not(equals(0, 0))]"
```

### <a name="coalesce"></a>coalesce
Devuelve Hola valor del parámetro no null de la primera Hola. Algunas funciones admiten todos los tipos de datos JSON.

Asuma que `element1` y `element2` son indefinidos. Devuelve de Hello en el ejemplo siguiente se `"foobar"`:

```json
"[coalesce(steps('foo').element1, steps('foo').element2, 'foobar')]"
```

## <a name="conversion-functions"></a>Funciones de conversión
Estas funciones pueden ser valores de uso tooconvert entre la codificación y tipos de datos JSON.

### <a name="int"></a>int
Convierte el entero de hello parámetro tooan. Esta función admite parámetros de tipo number y string.

Devuelve de Hello en el ejemplo siguiente se `1`:

```json
"[int('1')]"
```

Devuelve de Hello en el ejemplo siguiente se `2`:

```json
"[int(2.9)]"
```

### <a name="float"></a>float
Convierte Hola parámetro tooa punto flotante. Esta función admite parámetros de tipo number y string.

Devuelve de Hello en el ejemplo siguiente se `1.0`:

```json
"[float('1.0')]"
```

Devuelve de Hello en el ejemplo siguiente se `2.9`:

```json
"[float(2.9)]"
```

### <a name="string"></a>cadena
Convierte la cadena de tooa de parámetros de Hola. Esta función admite parámetros de todos los tipos de datos JSON.

Devuelve de Hello en el ejemplo siguiente se `"1"`:

```json
"[string(1)]"
```

Devuelve de Hello en el ejemplo siguiente se `"2.9"`:

```json
"[string(2.9)]"
```

Devuelve de Hello en el ejemplo siguiente se `"[1,2,3]"`:

```json
"[string([1,2,3])]"
```

Devuelve de Hello en el ejemplo siguiente se `"{"foo":"bar"}"`:

```json
"[string({\"foo\":\"bar\"})]"
```

### <a name="bool"></a>booleano
Convierte Hola parámetro tooa un valor booleano. Esta función admite parámetros de tipo number, string y booleano. TooBooleans similar en JavaScript, cualquier valor excepto `0` o `'false'` devuelve `true`.

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[bool(1)]"
```

Devuelve de Hello en el ejemplo siguiente se `false`:

```json
"[bool(0)]"
```

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[bool(true)]"
```

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[bool('true')]"
```

### <a name="parse"></a>parse
Convierte a un tipo nativo Hola parámetro tooa. En otras palabras, esta función es el inverso de Hola de `string()`. Esta función admite parámetros solo de tipo string.

Devuelve de Hello en el ejemplo siguiente se `1`:

```json
"[parse('1')]"
```

Devuelve de Hello en el ejemplo siguiente se `true`:

```json
"[parse('true')]"
```

Devuelve de Hello en el ejemplo siguiente se `[1,2,3]`:

```json
"[parse('[1,2,3]')]"
```

Devuelve de Hello en el ejemplo siguiente se `{"foo":"bar"}`:

```json
"[parse('{\"foo\":\"bar\"}')]"
```

### <a name="encodebase64"></a>encodeBase64
Codifica la cadena codificada en base 64 Hola parámetro tooa. Esta función admite parámetros solo de tipo string.

Devuelve de Hello en el ejemplo siguiente se `"Zm9vYmFy"`:

```json
"[encodeBase64('foobar')]"
```

### <a name="decodebase64"></a>decodeBase64
Descodifica el parámetro hello desde una cadena codificada en base 64. Esta función admite parámetros solo de tipo string.

Devuelve de Hello en el ejemplo siguiente se `"foobar"`:

```json
"[decodeBase64('Zm9vYmFy')]"
```

### <a name="encodeuricomponent"></a>encodeUriComponent
Codifica la cadena de dirección URL codificada de hello parámetros tooa. Esta función admite parámetros solo de tipo string.

Devuelve de Hello en el ejemplo siguiente se `"https%3A%2F%2Fportal.azure.com%2F"`:

```json
"[encodeUriComponent('https://portal.azure.com/')]"
```

### <a name="decodeuricomponent"></a>decodeUriComponent
Descodifica el parámetro hello de una cadena de dirección URL codificada. Esta función admite parámetros solo de tipo string.

Devuelve de Hello en el ejemplo siguiente se `"https://portal.azure.com/"`:

```json
"[decodeUriComponent('https%3A%2F%2Fportal.azure.com%2F')]"
```

## <a name="math-functions"></a>Funciones matemáticas
### <a name="add"></a>agregar
Suma dos números y devuelve el resultado de hello.

Devuelve de Hello en el ejemplo siguiente se `3`:

```json
"[add(1, 2)]"
```

### <a name="sub"></a>sub
Resta Hola segundo número desde el primer número de Hola y devuelve el resultado de hello.

Devuelve de Hello en el ejemplo siguiente se `1`:

```json
"[sub(3, 2)]"
```

### <a name="mul"></a>mul
Multiplica a dos números y devuelve el resultado de hello.

Devuelve de Hello en el ejemplo siguiente se `6`:

```json
"[mul(2, 3)]"
```

### <a name="div"></a>div
Divide Hola primer número por segundo número de Hola y devuelve el resultado de hello. resultado de Hello siempre es un entero.

Devuelve de Hello en el ejemplo siguiente se `2`:

```json
"[div(6, 3)]"
```

### <a name="mod"></a>mod
Divide Hola primer número por segundo número de Hola y devuelve el resto de Hola.

Devuelve de Hello en el ejemplo siguiente se `0`:

```json
"[mod(6, 3)]"
```

Devuelve de Hello en el ejemplo siguiente se `2`:

```json
"[mod(6, 4)]"
```

### <a name="min"></a>Min
Devuelve Hola pequeño de números de hello dos.

Devuelve de Hello en el ejemplo siguiente se `1`:

```json
"[min(1, 2)]"
```

### <a name="max"></a>max
Hola de devuelve mayor de dos números de Hola.

Devuelve de Hello en el ejemplo siguiente se `2`:

```json
"[max(1, 2)]"
```

### <a name="range"></a>range
Genera una secuencia de entero especificado de números dentro de hello intervalo.

Devuelve de Hello en el ejemplo siguiente se `[1,2,3]`:

```json
"[range(1, 3)]"
```

### <a name="rand"></a>rand
Devuelve un aleatorio número integral de hello especifica el intervalo. Esta función no genera números aleatorios criptográficamente seguros.

Hello en el ejemplo siguiente se podría devolver `42`:

```json
"[rand(-100, 100)]"
```

### <a name="floor"></a>floor
Devuelve Hola mayor entero menor o igual toohello del número especificado.

Devuelve de Hello en el ejemplo siguiente se `3`:

```json
"[floor(3.14)]"
```

### <a name="ceil"></a>ceil
Devuelve Hola mayor número entero mayor que o igual toohello del número especificado.

Devuelve de Hello en el ejemplo siguiente se `4`:

```json
"[ceil(3.14)]"
```

## <a name="date-functions"></a>Funciones de fecha
### <a name="utcnow"></a>utcNow
Devuelve una cadena en formato ISO 8601 de hello fecha y hora en el equipo local de hello actual.

Hello en el ejemplo siguiente se podría devolver `"1990-12-31T23:59:59.000Z"`:

```json
"[utcNow()]"
```

### <a name="addseconds"></a>addSeconds
Agrega un número integral de toohello de segundos especificado marca de tiempo.

Devuelve de Hello en el ejemplo siguiente se `"1991-01-01T00:00:00.000Z"`:

```json
"[addSeconds('1990-12-31T23:59:60Z', 1)]"
```

### <a name="addminutes"></a>addMinutes
Agrega un número integral de toohello de minutos especificado marca de tiempo.

Devuelve de Hello en el ejemplo siguiente se `"1991-01-01T00:00:59.000Z"`:

```json
"[addMinutes('1990-12-31T23:59:59Z', 1)]"
```

### <a name="addhours"></a>addHours
Agrega un número integral de toohello de horas especificado marca de tiempo.

Devuelve de Hello en el ejemplo siguiente se `"1991-01-01T00:59:59.000Z"`:

```json
"[addHours('1990-12-31T23:59:59Z', 1)]"
```

## <a name="next-steps"></a>Pasos siguientes
* Para un administrador de recursos de introducción tooAzure, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).

