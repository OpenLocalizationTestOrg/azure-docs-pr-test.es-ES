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
# <a name="numeric-functions-for-azure-resource-manager-templates"></a>Funciones numéricas para las plantillas de Azure Resource Manager

Administrador de recursos proporciona Hola siguientes funciones para trabajar con números enteros:

* [agregar](#add)
* [copyIndex](#copyindex)
* [div](#div)
* [float](#float)
* [int](#int)
* [min](#min)
* [max](#max)
* [mod](#mod)
* [mul](#mul)
* [sub](#sub)

<a id="add" />

## <a name="add"></a>agregar
`add(operand1, operand2)`

Devuelve Hola suma de dos enteros proporcionado Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- | 
|operand1 |Sí |int |Primero debe numerar tooadd. |
|operand2 |Sí |int |Segundo número tooadd. |

### <a name="return-value"></a>Valor devuelto

Un entero que contiene la suma de Hola de parámetros de Hola.

### <a name="example"></a>Ejemplo

Hola ejemplo siguiente agrega dos parámetros.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| addResult | int | 8 |

<a id="copyindex" />

## <a name="copyindex"></a>copyIndex
`copyIndex(loopName, offset)`

Devuelve Hola índice de un bucle de iteración. 

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| loopName | No | cadena | nombre de Hola de bucle de Hola para obtener iteración Hola. |
| Offset |No |int |Hola tooadd toohello basado en cero del iteración valor numérico. |

### <a name="remarks"></a>Comentarios

Esta función siempre se usa con un objeto **copy** . Si no se proporciona ningún valor para **desplazamiento**, se devuelve el valor actual de la iteración de Hola. valor de la iteración de Hello comienza en cero.

Hola **loopName** propiedad le permite toospecify si hace referencia copyIndex tooa iteración de recursos o la iteración de la propiedad. Si no se proporciona ningún valor para **loopName**, se utiliza la iteración de tipo de recurso actual Hola. Proporcione un valor para **loopName** al iterar en una propiedad. 
 
Para ver una descripción completa de cómo usar **copyIndex**, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md).

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se muestra un valor copia hello y bucle índice incluido en el nombre de Hola. 

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

### <a name="return-value"></a>Valor devuelto

Un entero que representa el índice actual de hello del iteración Hola.

<a id="div" />

## <a name="div"></a>div
`div(operand1, operand2)`

Devuelve Hola división de enteros de dos enteros de proporcionado Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| operand1 |Sí |int |número de Hola que se va a dividir. |
| operand2 |Sí |int |Hola número toodivide usado. No puede ser 0. |

### <a name="return-value"></a>Valor devuelto

Una división Hola de enteros que representan.

### <a name="example"></a>Ejemplo

Hola siguiente ejemplo divide un parámetro por otro parámetro.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| divResult | int | 2 |

<a id="float" />

## <a name="float"></a>float
`float(arg1)`

Convierte Hola valor tooa números de punto flotante. Solo, esta función se usan al pasar parámetros personalizados aplicación tooan, por ejemplo, una aplicación de lógica.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |cadena o entero |Hola valor tooconvert tooa números de punto flotante. |

### <a name="return-value"></a>Valor devuelto
Un número de punto flotante.

### <a name="example"></a>Ejemplo

Hola de ejemplo siguiente muestra cómo toouse float toopass parámetros tooa aplicación lógica:

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

## <a name="int"></a>int
`int(valueToConvert)`

Convierte el entero de tooan de valor especificado de Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| valueToConvert |Sí |cadena o entero |entero de Hello valor tooconvert tooan. |

### <a name="return-value"></a>Valor devuelto

Un entero de hello valor convertido.

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se convierte toointeger de valor de parámetro proporcionado por el usuario de Hola.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| intResult | int | 4 |


<a id="min" />

## <a name="min"></a>Min
`min (arg1)`

Devuelve Hola valor mínimo de una matriz de enteros o una lista separada por comas de números enteros.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |matriz de enteros, o lista separada por comas de enteros |Hola tooget Hola mínimo valor de la colección. |

### <a name="return-value"></a>Valor devuelto

Un entero que representa el valor mínimo de colección de Hola.

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
`max (arg1)`

Devuelve Hola valor máximo de una matriz de enteros o una lista separada por comas de números enteros.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |matriz de enteros, o lista separada por comas de enteros |Hola tooget Hola máximo valor de la colección. |

### <a name="return-value"></a>Valor devuelto

Un entero que representa el valor máximo de Hola de colección de Hola.

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

<a id="mod" />

## <a name="mod"></a>mod
`mod(operand1, operand2)`

Devuelve el resto de Hola Hola división de enteros utilizando dos enteros de proporcionado Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| operand1 |Sí |int |número de Hola que se va a dividir. |
| operand2 |Sí |int |número de Hello toodivide utilizado, no puede ser 0. |

### <a name="return-value"></a>Valor devuelto
Un resto de Hola que representan entero.

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se devuelve Hola resto de dividir un parámetro por otro parámetro.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| modResult | int | 1 |

<a id="mul" />

## <a name="mul"></a>mul
`mul(operand1, operand2)`

Devuelve Hola multiplicación de dos enteros de proporcionado Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| operand1 |Sí |int |Primero debe numerar toomultiply. |
| operand2 |Sí |int |Segundo número toomultiply. |

### <a name="return-value"></a>Valor devuelto

Una entero que representa Hola la multiplicación.

### <a name="example"></a>Ejemplo

Hola de ejemplo siguiente multiplica un parámetro por otro parámetro.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| mulResult | int | 15 |

<a id="sub" />

## <a name="sub"></a>sub
`sub(operand1, operand2)`

Devuelve Hola resta de dos enteros de proporcionado Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| operand1 |Sí |int |número de Hola que se resta. |
| operand2 |Sí |int |número de Hola que se va a restar. |

### <a name="return-value"></a>Valor devuelto
Una resta Hola de enteros que representan.

### <a name="example"></a>Ejemplo

Hola siguiente ejemplo resta un parámetro de otro parámetro.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| subResult | int | 4 |

## <a name="next-steps"></a>Pasos siguientes
* Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).
* toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).
* tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).
* toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).

