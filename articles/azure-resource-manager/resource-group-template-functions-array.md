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
# <a name="array-and-object-functions-for-azure-resource-manager-templates"></a>Funciones de matriz y de objeto para las plantillas de Azure Resource Manager 

Resource Manager ofrece varias funciones para trabajar con matrices y objetos.

* [matriz](#array)
* [coalesce](#coalesce)
* [concat](#concat)
* [contains](#contains)
* [createArray](#createarray)
* [empty](#empty)
* [first](#first)
* [intersection](#intersection)
* [json](#json)
* [last](#last)
* [length](#length)
* [min](#min)
* [max](#max)
* [range](#range)
* [skip](#skip)
* [take](#take)
* [union](#union)

tooget una matriz de valores de cadena delimitada por un valor, vea [dividir](resource-group-template-functions-string.md#split).

<a id="array" />

## <a name="array"></a>array
`array(convertToArray)`

Convierte la matriz de hello valores tooan.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| convertToArray |Sí |entero, cadena, matriz u objeto |matriz de Hello valores tooconvert tooan. |

### <a name="return-value"></a>Valor devuelto

Una matriz.

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se muestra cómo toouse Hola función de matriz con los diferentes tipos.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| intOutput | Matriz | [1] |
| stringOutput | Matriz | ["a"] |
| objectOutput | Matriz | [{"a": "b", "c": "d"}] |

<a id="coalesce" />

## <a name="coalesce"></a>coalesce
`coalesce(arg1, arg2, arg3, ...)`

Devuelve el primer valor distinto de null de parámetros de Hola. Las cadenas vacías, las matrices vacías y los objetos vacíos no son nulos.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |entero, cadena, matriz u objeto |Hola primer valor tootest si hay valores null. |
| argumentos adicionales |No |entero, cadena, matriz u objeto |Valores adicionales tootest si hay valores null. |

### <a name="return-value"></a>Valor devuelto

valor de Hola de parámetros distintos de null primera hello, que puede ser una cadena, int, matriz u objeto. Es nulo si todos los parámetros son nulos. 

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se muestra la salida de hello desde diferentes usos de coalesce.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| stringOutput | String | default |
| intOutput | int | 1 |
| objectOutput | Objeto | {"first": "default"} |
| arrayOutput | Matriz | [1] |
| emptyOutput | Booleano | True |

<a id="concat" />

## <a name="concat"></a>concat
`concat(arg1, arg2, arg3, ...)`

Combina varias matrices y devuelve una matriz concatenado de hello, o combina varios valores de cadena y devuelve la cadena Hola concatenado. 

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |matriz o cadena |Hola primera matriz o cadena para la concatenación. |
| argumentos adicionales |No |matriz o cadena |Matrices o cadenas adicionales en orden secuencial para la concatenación. |

Esta función puede tomar cualquier número de argumentos y puede aceptar cadenas o las matrices de parámetros de Hola.

### <a name="return-value"></a>Valor devuelto
Una cadena o matriz de valores concatenados.

### <a name="example"></a>Ejemplo

Hola de ejemplo siguiente muestra cómo toocombine dos matrices.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| return | Matriz | ["1-1", "1-2", "1-3", "2-1", "2-2", "2-3"] |

Hola de ejemplo siguiente muestra cómo toocombine dos valores de cadena y devolver una cadena concatenada.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| concatOutput | String | prefix-5yj4yjf5mbg72 |

<a id="contains" />

## <a name="contains"></a>contains
`contains(container, itemToFind)`

Comprueba si una matriz contiene un valor, un objeto contiene una clave o una cadena contiene una subcadena.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| container |Sí |matriz, objeto o cadena |valor de Hola que contiene Hola valor toofind. |
| itemToFind |Sí |cadena o entero |Hola toofind de valor. |

### <a name="return-value"></a>Valor devuelto

**True** si Hola elemento se encuentra; en caso contrario, **False**.

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se muestra cómo toouse contiene con tipos diferentes:

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| stringTrue | Booleano | True |
| stringFalse | Booleano | False |
| objectTrue | Booleano | True |
| objectFalse | Booleano | False |
| arrayTrue | Booleano | True |
| arrayFalse | Booleano | False |

<a id="createarray" />

## <a name="createarray"></a>createarray
`createArray (arg1, arg2, arg3, ...)`

Crea una matriz de parámetros de Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |Cadena, entero, matriz u objeto |Hola primer valor de matriz de Hola. |
| argumentos adicionales |No |Cadena, entero, matriz u objeto |Valores adicionales en la matriz de Hola. |

### <a name="return-value"></a>Valor devuelto

Una matriz.

### <a name="example"></a>Ejemplo

Hola siguiente ejemplo se muestra cómo toouse createArray con tipos diferentes:

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| stringArray | Matriz | ["a", "b", "c"] |
| intArray | Matriz | [1, 2, 3] |
| objectArray | Matriz | [{"one": "a", "two": "b", "three": "c"}] |
| arrayArray | Matriz | [["one", "two", "three"]] |

<a id="empty" />

## <a name="empty"></a>empty

`empty(itemToTest)`

Determina si una matriz, un objeto o una cadena están vacíos.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| itemToTest |Sí |matriz, objeto o cadena |Hola toocheck valor si está vacía. |

### <a name="return-value"></a>Valor devuelto

Devuelve **True** si el valor de hello está vacía; en caso contrario, **False**.

### <a name="example"></a>Ejemplo

Hola siguiente ejemplo comprueba si una matriz, el objeto y la cadena están vacías.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| arrayEmpty | Booleano | True |
| objectEmpty | Booleano | True |
| stringEmpty | Booleano | True |

<a id="first" />

## <a name="first"></a>first
`first(arg1)`

Devuelve Hola el primer elemento de matriz de Hola o el primer carácter de la cadena de Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |matriz o cadena |Hola valor tooretrieve Hola primer elemento o carácter. |

### <a name="return-value"></a>Valor devuelto

Hola tipo (string, int, matriz u objeto) del primer elemento en una matriz de Hola u Hola el primer carácter de una cadena.

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se muestra cómo toouse Hola primera función con una matriz y una cadena.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | String | one |
| stringOutput | String | O |

<a id="intersection" />

## <a name="intersection"></a>intersección
`intersection(arg1, arg2, arg3, ...)`

Devuelve una matriz único o un objeto con elementos comunes de Hola de parámetros de Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |matriz u objeto |Hola primer toouse de valor para buscar elementos comunes. |
| arg2 |Sí |matriz u objeto |Hola segundo toouse de valor para buscar elementos comunes. |
| argumentos adicionales |No |matriz u objeto |Toouse valores adicionales para buscar elementos comunes. |

### <a name="return-value"></a>Valor devuelto

Una matriz o un objeto con elementos comunes de Hola.

### <a name="example"></a>Ejemplo

Hola de ejemplo siguiente muestra cómo toouse intersección con las matrices y los objetos:

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| objectOutput | Objeto | {"one": "a", "three": "c"} |
| arrayOutput | Matriz | ["two", "three"] |


## <a name="json"></a>json
`json(arg1)`

Devuelve un objeto JSON.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |cadena |Hola valor tooconvert tooJSON. |


### <a name="return-value"></a>Valor devuelto

Especifica el objeto JSON de Hola de hello cadena o un objeto vacío cuando **null** se especifica.

### <a name="example"></a>Ejemplo

Hola de ejemplo siguiente muestra cómo toouse intersección con las matrices y los objetos:

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| jsonOutput | Objeto | {"a": "b"} |
| nullOutput | boolean | True |

<a id="last" />

## <a name="last"></a>last
`last (arg1)`

Devuelve Hola último elemento de matriz de Hola o último carácter de la cadena de Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |matriz o cadena |Hola value tooretrieve Hola última (elemento) o carácter. |

### <a name="return-value"></a>Valor devuelto

Hola tipo (string, int, matriz u objeto) del último elemento en una matriz de Hola u Hola último carácter de una cadena.

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se muestra cómo toouse Hola última función con una matriz y una cadena.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | String | three |
| stringOutput | String | e |

<a id="length" />

## <a name="length"></a>length
`length(arg1)`

Devuelve el número de Hola de elementos de una matriz o caracteres de una cadena.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |matriz o cadena |Hola toouse de matriz para obtener el número de Hola de elementos u Hola toouse de cadena para obtener el número de Hola de caracteres. |

### <a name="return-value"></a>Valor devuelto

Un entero. 

### <a name="example"></a>Ejemplo

Hola siguiente ejemplo se muestra cómo toouse longitud con una matriz y la cadena:

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| arrayLength | int | 3 |
| stringLength | int | 13 |

Puede usar esta función con un número de iteraciones Hola de toospecify de matriz al crear recursos. En el siguiente ejemplo de Hola Hola parámetro **siteNames** haría referencia tooan matriz de nombres toouse al crear sitios web de Hola.

```json
"copy": {
    "name": "websitescopy",
    "count": "[length(parameters('siteNames'))]"
}
```

Para más información sobre cómo usar esta función con una matriz, vea [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).

<a id="min" />

## <a name="min"></a>Min
`min(arg1)`

Devuelve Hola valor mínimo de una matriz de enteros o una lista separada por comas de números enteros.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |matriz de enteros, o lista separada por comas de enteros |Hola tooget Hola mínimo valor de la colección. |

### <a name="return-value"></a>Valor devuelto

Un entero que representa el valor mínimo de Hola.

### <a name="example"></a>Ejemplo

Hola siguiente ejemplo se muestra cómo min toouse con una matriz y una lista de enteros:

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | int | 0 |
| intOutput | int | 0 |

<a id="max" />

## <a name="max"></a>max
`max(arg1)`

Devuelve Hola valor máximo de una matriz de enteros o una lista separada por comas de números enteros.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |matriz de enteros, o lista separada por comas de enteros |Hola tooget Hola máximo valor de la colección. |

### <a name="return-value"></a>Valor devuelto

Un entero que representa el valor máximo de Hola.

### <a name="example"></a>Ejemplo

Hola siguiente ejemplo se muestra cómo toouse máximo con una matriz y una lista de enteros:

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | int | 5 |
| intOutput | int | 5 |

<a id="range" />

## <a name="range"></a>range
`range(startingInteger, numberOfElements)`

Crea una matriz de enteros a partir de un entero de inicio y contiene un número de elementos.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| startingInteger |Sí |int |primer entero de Hello en la matriz de Hola. |
| numberofElements |Sí |int |número de Hola de enteros en la matriz de Hola. |

### <a name="return-value"></a>Valor devuelto

Una matriz de enteros.

### <a name="example"></a>Ejemplo

Hola de ejemplo siguiente muestra cómo toouse Hola función intervalo:

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| rangeOutput | Matriz | [5, 6, 7] |

<a id="skip" />

## <a name="skip"></a>skip
`skip(originalValue, numberToSkip)`

Devuelve una matriz con todos los elementos de hello después Hola número especificado en la matriz de Hola o devuelve una cadena con todos los caracteres de hello después Hola el número especificado en la cadena de Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| originalValue |Sí |matriz o cadena |Hola toouse de matriz o de cadena para pasar por alto. |
| numberToSkip |Sí |int |número de Hola de tooskip elementos o caracteres. Si este valor es 0 o menos, todos los elementos de Hola o se devuelven los caracteres en valor de Hola. Si es mayor que la longitud de cadena o matriz de Hola Hola, se devuelve una matriz vacía o una cadena. |

### <a name="return-value"></a>Valor devuelto

Una matriz o cadena.

### <a name="example"></a>Ejemplo

Hola siguiendo el ejemplo omite Hola número especificado de elementos de matriz de Hola y Hola especifica el número de caracteres en una cadena.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | Matriz | ["three"] |
| stringOutput | String | two three |

<a id="take" />

## <a name="take"></a>take
`take(originalValue, numberToTake)`

Devuelve una matriz con hello un número especificado de elementos de Hola inicio de matriz de hello, o una cadena con hello número especificado de caracteres desde el principio de Hola de cadena Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| originalValue |Sí |matriz o cadena |Hola array o string tootake Hola elementos. |
| numberToTake |Sí |int |número de Hola de tootake elementos o caracteres. Si este valor es 0 o un valor inferior, se devolverá una matriz o cadena vacía. Si es mayor que la longitud de Hola de hello con cadena o una matriz, se devuelven todos los elementos de hello en la matriz de Hola o de cadena. |

### <a name="return-value"></a>Valor devuelto

Una matriz o cadena.

### <a name="example"></a>Ejemplo

Hola siguiendo el ejemplo hello de toma un número especificado de elementos de matriz de Hola y los caracteres de una cadena.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| arrayOutput | Matriz | ["one", "two"] |
| stringOutput | String | en |

<a id="union" />

## <a name="union"></a>union
`union(arg1, arg2, arg3, ...)`

Devuelve una matriz único o un objeto con todos los elementos de parámetros de Hola. Los valores o las claves duplicados solo se incluyen una vez.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |matriz u objeto |Hola primer valor toouse para combinar elementos. |
| arg2 |Sí |matriz u objeto |Hola segundo valor toouse para combinar elementos. |
| argumentos adicionales |No |matriz u objeto |Toouse valores adicionales para combinar elementos. |

### <a name="return-value"></a>Valor devuelto

Una matriz u objeto.

### <a name="example"></a>Ejemplo

Hola de ejemplo siguiente muestra cómo toouse unión con las matrices y los objetos:

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| objectOutput | Objeto | {"one": "a", "two": "b", "three": "c", "four": "d", "five": "e"} |
| arrayOutput | Matriz | ["one", "two", "three", "four"] |

## <a name="next-steps"></a>Pasos siguientes
* Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).
* toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).
* tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).
* toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).

