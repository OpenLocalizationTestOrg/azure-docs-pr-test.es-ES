---
title: "funciones de plantilla de administrador de recursos aaaAzure - lógicas | Documentos de Microsoft"
description: "Describe hello toouse de funciones en una lógica de valores de toodetermine de plantilla Azure Resource Manager."
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
ms.openlocfilehash: aec6341fbde00b4eba3b4539ff9a9aec774333fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="logical-functions-for-azure-resource-manager-templates"></a>Funciones lógicas para las plantillas de Azure Resource Manager

Resource Manager proporciona varias funciones para realizar comparaciones en las plantillas.

* [and](#and)
* [bool](#bool)
* [if](#if)
* [not](#not)
* [or](#or)

## <a name="and"></a>y
`and(arg1, arg2)`

Comprueba si los dos valores de parámetro son verdaderos.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |boolean |Hola primera toocheck valor si es true. |
| arg2 |Sí |boolean |Hola segundo toocheck valor si es true. |

### <a name="return-value"></a>Valor devuelto

Devuelve **True** si ambos valores son verdaderos; en caso contrario, devuelve **False**.

### <a name="examples"></a>Ejemplos

Hola siguiente ejemplo se muestra cómo las funciones lógicas de toouse.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

resultado Hola Hola anterior ejemplo es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| andExampleOutput | Booleano | False |
| orExampleOutput | Booleano | True |
| notExampleOutput | Booleano | False |


## <a name="bool"></a>booleano
`bool(arg1)`

Convierte Hola tooa parámetro booleano.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |cadena o entero |Hola tooa tooconvert de valor booleano. |

### <a name="return-value"></a>Valor devuelto
Un valor booleano de hello valor convertido.

### <a name="examples"></a>Ejemplos

Hola siguiente ejemplo se muestra cómo bool toouse con una cadena o un entero.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "trueString": {
            "value": "[bool('true')]",
            "type" : "bool"
        },
        "falseString": {
            "value": "[bool('false')]",
            "type" : "bool"
        },
        "trueInt": {
            "value": "[bool(1)]",
            "type" : "bool"
        },
        "falseInt": {
            "value": "[bool(0)]",
            "type" : "bool"
        }
    }
}
```

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| trueString | Booleano | True |
| falseString | Booleano | False |
| trueInt | Booleano | True |
| falseInt | Booleano | False |

## <a name="if"></a>if
`if(condition, trueValue, falseValue)`

Devuelve un valor dependiendo de si una condición es verdadera o falsa.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| condition |Sí |boolean |Hola toocheck valor si es true. |
| trueValue |Sí | cadena, int, objeto o matriz |Hola valor tooreturn cuando Hola condición sea verdadera. |
| falseValue |Sí | cadena, int, objeto o matriz |Hola valor tooreturn cuando Hola condición es false. |

### <a name="return-value"></a>Valor devuelto

Devuelve el segundo parámetro si el primer parámetro es **True**; en caso contrario, devuelve el tercer parámetro.

### <a name="remarks"></a>Comentarios

Puede utilizar este conjunto de tooconditionally de función de una propiedad de recurso. Hello en el ejemplo siguiente no se es una plantilla completa, pero muestra las partes relevantes de Hola para establecer condicionalmente el conjunto de disponibilidad de Hola.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "availabilitySet": {
            "type": "string",
            "allowedValues": [
                "yes",
                "no"
            ]
        }
    },
    "variables": {
        ...
        "availabilitySetName": "availabilitySet1",
        "availabilitySet": {
            "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
        }
    },
    "resources": [
        {
            "condition": "[equals(parameters('availabilitySet'),'yes')]",
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            ...
        },
        {
            "apiVersion": "2016-03-30",
            "type": "Microsoft.Compute/virtualMachines",
            "properties": {
                "availabilitySet": "[if(equals(parameters('availabilitySet'),'yes'), variables('availabilitySet'), json('null'))]",
                ...
            }
        },
        ...
    ],
    ...
}
```

### <a name="examples"></a>Ejemplos

Hola siguiente ejemplo se muestra cómo toouse hello `if` función.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    ],
    "outputs": {
        "yesOutput": {
            "type": "string",
            "value": "[if(equals('a', 'a'), 'yes', 'no')]"
        },
        "noOutput": {
            "type": "string",
            "value": "[if(equals('a', 'b'), 'yes', 'no')]"
        }
    }
}
```

resultado Hola Hola anterior ejemplo es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| yesOutput | String | yes |
| noOutput | String | no |


## <a name="not"></a>not
`not(arg1)`

Convierte el valor booleano tooits opuesto valor.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |boolean |Hola tooconvert de valor. |


### <a name="return-value"></a>Valor devuelto

Devuelve **True** si el parámetro es **False**. Devuelve **False** si el parámetro es **True**.

### <a name="examples"></a>Ejemplos

Hola siguiente ejemplo se muestra cómo las funciones lógicas de toouse.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

resultado Hola Hola anterior ejemplo es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| andExampleOutput | Booleano | False |
| orExampleOutput | Booleano | True |
| notExampleOutput | Booleano | False |

Hello siguiente ejemplo se utiliza **no** con [es igual a](resource-group-template-functions-comparison.md#equals).

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


## <a name="or"></a>o
`or(arg1, arg2)`

Comprueba si cualquiera de los valores de parámetro es verdadero.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| arg1 |Sí |boolean |Hola primera toocheck valor si es true. |
| arg2 |Sí |boolean |Hola segundo toocheck valor si es true. |

### <a name="return-value"></a>Valor devuelto

Devuelve **True** si cualquiera de los valores es verdadero; en caso contrario, devuelve **False**.

### <a name="examples"></a>Ejemplos

Hola siguiente ejemplo se muestra cómo las funciones lógicas de toouse.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [ ],
    "outputs": {
        "andExampleOutput": {
            "value": "[and(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "orExampleOutput": {
            "value": "[or(bool('true'), bool('false'))]",
            "type": "bool"
        },
        "notExampleOutput": {
            "value": "[not(bool('true'))]",
            "type": "bool"
        }
    }
}
```

resultado Hola Hola anterior ejemplo es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| andExampleOutput | Booleano | False |
| orExampleOutput | Booleano | True |
| notExampleOutput | Booleano | False |


## <a name="next-steps"></a>Pasos siguientes
* Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).
* toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).
* tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).
* toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).

