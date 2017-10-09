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
# <a name="comparison-functions-for-azure-resource-manager-templates"></a>Funciones de comparación para las plantillas de Azure Resource Manager

Resource Manager proporciona varias funciones para realizar comparaciones en las plantillas.

* [equals](#equals)
* [greater](#greater)
* [greaterOrEquals](#greaterorequals)
* [less](#less)
* [lessOrEquals](#lessorequals)

## <a name="equals"></a>equals
`equals(arg1, arg2)`

Comprueba si dos valores son iguales.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |entero, cadena, matriz u objeto |Hola primer toocheck de valor para la igualdad. |
| arg2 |Sí |entero, cadena, matriz u objeto |Hola segundo toocheck de valor para la igualdad. |

### <a name="return-value"></a>Valor devuelto

Devuelve **True** si Hola valores son iguales; en caso contrario, **False**.

### <a name="remarks"></a>Comentarios

Hello es igual a función se suele utilizar con hello `condition` tootest del elemento si se implementa un recurso.

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

### <a name="example"></a>Ejemplo

plantilla de ejemplo de Hola comprueba diferentes tipos de valores para la igualdad. Todos los valores predeterminados de hello devuelven True.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| checkInts | Booleano | True |
| checkStrings | Booleano | True |
| checkArrays | Booleano | True |
| checkObjects | Booleano | True |


Hello siguiente ejemplo se utiliza [no](resource-group-template-functions-logical.md#not) con **es igual a**.

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

resultado Hola Hola anterior ejemplo es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| checkNotEquals | Booleano | True |


## <a name="greater"></a>greater
`greater(arg1, arg2)`

Comprueba si el primer valor de hello es mayor que el segundo valor de Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |entero o cadena |Hola primer valor de comparación mayor Hola. |
| arg2 |Sí |entero o cadena |Hola segundo valor de comparación mayor Hola. |

### <a name="return-value"></a>Valor devuelto

Devuelve **True** si Hola primer valor es mayor que el segundo valor de hello; en caso contrario, **False**.

### <a name="example"></a>Ejemplo

plantilla de ejemplo de Hola comprueba si un valor de hello es mayor que Hola otro.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| checkInts | Booleano | False |
| checkStrings | Booleano | True |


## <a name="greaterorequals"></a>greaterOrEquals
`greaterOrEquals(arg1, arg2)`

Comprueba si el primer valor de hello es igual o mayor que toohello segundo valor.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |entero o cadena |Hola primer valor de comparación mayor o igual que de Hola. |
| arg2 |Sí |entero o cadena |Hola segundo valor de comparación mayor o igual que de Hola. |

### <a name="return-value"></a>Valor devuelto

Devuelve **True** si Hola primer valor es mayor o igual toohello segundo; en caso contrario, **False**.

### <a name="example"></a>Ejemplo

plantilla de ejemplo de Hola comprueba si un valor de hello es mayor que o igual toohello otro.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| checkInts | Booleano | False |
| checkStrings | Booleano | True |



## <a name="less"></a>less
`less(arg1, arg2)`

Comprueba si Hola primer valor es menor que Hola segundo valor.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |entero o cadena |primer valor de Hola para hello menos comparación. |
| arg2 |Sí |entero o cadena |segundo valor de Hola para hello menos comparación. |

### <a name="return-value"></a>Valor devuelto

Devuelve **True** si Hola primer valor es menor que Hola segundo valor; en caso contrario, **False**.

### <a name="example"></a>Ejemplo

plantilla de ejemplo de Hola comprueba si un valor de hello es menor que Hola otro.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| checkInts | Booleano | True |
| checkStrings | Booleano | False |


## <a name="lessorequals"></a>lessOrEquals
`lessOrEquals(arg1, arg2)`

Comprueba si el primer valor de hello es menor o igual toohello segundo valor.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |entero o cadena |primer valor de Hola para hello menos o comparación de igualdad. |
| arg2 |Sí |entero o cadena |Hola segundo valor de hello menor o igual que comparación. |

### <a name="return-value"></a>Valor devuelto

Devuelve **True** si Hola primer valor es menor o igual toohello segundo valor; en caso contrario, **False**.

### <a name="example"></a>Ejemplo

Hello plantilla en el ejemplo se comprueba si un valor de hello es menor o igual toohello otro.

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

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| checkInts | Booleano | True |
| checkStrings | Booleano | False |



## <a name="next-steps"></a>Pasos siguientes
* Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).
* toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).
* tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).
* toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).

