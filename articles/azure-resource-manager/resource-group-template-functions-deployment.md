---
title: funciones de plantilla de administrador de recursos de aaaAzure - deployment | Documentos de Microsoft
description: "Describe hello toouse de funciones en una información de la implementación de la plantilla tooretrieve Azure Resource Manager."
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
ms.openlocfilehash: 458c3f740504fdd6799ed24cc386219726737636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-functions-for-azure-resource-manager-templates"></a>Funciones de implementación para las plantillas de Azure Resource Manager 

Administrador de recursos proporciona siguiente hello las funciones para obtener los valores de las secciones de plantilla de Hola y los valores relacionados toohello implementación:

* [deployment](#deployment)
* [parameters](#parameters)
* [variables](#variables)

valores de tooget de recursos, grupos de recursos o suscripciones, vea [las funciones de recursos](resource-group-template-functions-resource.md).

<a id="deployment" />

## <a name="deployment"></a>deployment
`deployment()`

Devuelve información acerca de la operación de implementación actual de Hola.

### <a name="return-value"></a>Valor devuelto

Esta función devuelve el objeto de Hola que se pasa durante la implementación. propiedades de Hola Hola devolvió objeto varían en función de si hello implementación objeto se pasa como un vínculo o como un objeto en línea. Cuando se pasa el objeto de implementación de hello en línea, como cuando se usa hello **- TemplateFile** parámetro en el archivo local de Azure PowerShell toopoint tooa, Hola devuelve objeto tiene Hola siguiendo el formato:

```json
{
    "name": "",
    "properties": {
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [
            ],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

Cuando se pasa el objeto de Hola como un vínculo, como al usar Hola **TemplateUri -** parámetro toopoint tooa remoto del objeto, se devuelve el objeto de Hola Hola siguiendo el formato: 

```json
{
    "name": "",
    "properties": {
        "templateLink": {
            "uri": ""
        },
        "template": {
            "$schema": "",
            "contentVersion": "",
            "parameters": {},
            "variables": {},
            "resources": [],
            "outputs": {}
        },
        "parameters": {},
        "mode": "",
        "provisioningState": ""
    }
}
```

### <a name="remarks"></a>Comentarios

Puede usar deployment() toolink tooanother plantilla basado en el URI de la plantilla principal de Hola Hola.

```json
"variables": {  
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"  
}
```  

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se devuelve el objeto de implementación de hello:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[deployment()]",
            "type" : "object"
        }
    }
}
```

Hello en el ejemplo anterior se devuelve Hola después de objeto:

```json
{
  "name": "deployment",
  "properties": {
    "template": {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "resources": [],
      "outputs": {
        "subscriptionOutput": {
          "type": "Object",
          "value": "[deployment()]"
        }
      }
    },
    "parameters": {},
    "mode": "Incremental",
    "provisioningState": "Accepted"
  }
}
```

<a id="parameters" />

## <a name="parameters"></a>parameters
`parameters(parameterName)`

Devuelve un valor de parámetro. nombre de parámetro especificado de Hello debe definirse en la sección de parámetros de Hola de plantilla de Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| parameterName |Sí |cadena |nombre de Hola de hello parámetro tooreturn. |

### <a name="return-value"></a>Valor devuelto

valor de Hola de hello parámetro especifica.

### <a name="remarks"></a>Comentarios

Por lo general, utilice valores de parámetros tooset recursos. Hello en el ejemplo siguiente se establece Hola nombre del valor de parámetro de sitio web toohello pasado durante la implementación.

```json
"parameters": { 
  "siteName": {
      "type": "string"
  }
},
"resources": [
   {
      "apiVersion": "2016-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/Sites",
      ...
   }
]
```

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se muestra un uso simplificado de función de parámetros de Hola.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "stringParameter": {
            "type" : "string",
            "defaultValue": "option 1"
        },
        "intParameter": {
            "type": "int",
            "defaultValue": 1
        },
        "objectParameter": {
            "type": "object",
            "defaultValue": {"one": "a", "two": "b"}
        },
        "arrayParameter": {
            "type": "array",
            "defaultValue": [1, 2, 3]
        },
        "crossParameter": {
            "type": "string",
            "defaultValue": "[parameters('stringParameter')]"
        }
    },
    "variables": {},
    "resources": [],
    "outputs": {
        "stringOutput": {
            "value": "[parameters('stringParameter')]",
            "type" : "string"
        },
        "intOutput": {
            "value": "[parameters('intParameter')]",
            "type" : "int"
        },
        "objectOutput": {
            "value": "[parameters('objectParameter')]",
            "type" : "object"
        },
        "arrayOutput": {
            "value": "[parameters('arrayParameter')]",
            "type" : "array"
        },
        "crossOutput": {
            "value": "[parameters('crossParameter')]",
            "type" : "string"
        }
    }
}
```

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| stringOutput | String | opción 1 |
| intOutput | int | 1 |
| objectOutput | Objeto | {"one": "a", "two": "b"} |
| arrayOutput | Matriz | [1, 2, 3] |
| crossOutput | String | opción 1 |

<a id="variables" />

## <a name="variables"></a>variables
`variables(variableName)`

Devuelve Hola valor de variable. nombre de variable especificado Hola debe definirse en la sección de variables de Hola de plantilla de Hola.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| variableName |Sí |String |nombre de Hola de hello variable tooreturn. |

### <a name="return-value"></a>Valor devuelto

valor de Hola de variable especificado Hola.

### <a name="remarks"></a>Comentarios

Normalmente, se usa variables toosimplify la plantilla mediante la creación de una sola vez valores complejos. Hello en el ejemplo siguiente se crea un nombre único para una cuenta de almacenamiento.

```json
"variables": {
    "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
},
"resources": [
    {
        "type": "Microsoft.Storage/storageAccounts",
        "name": "[variables('storageName')]",
        ...
    },
    {
        "type": "Microsoft.Compute/virtualMachines",
        "dependsOn": [
            "[variables('storageName')]"
        ],
        ...
    }
],
```

### <a name="example"></a>Ejemplo

plantilla de ejemplo de Hola devuelve distintos valores de variable.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {
        "var1": "myVariable",
        "var2": [ 1,2,3,4 ],
        "var3": "[ variables('var1') ]",
        "var4": {
            "property1": "value1",
            "property2": "value2"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput1": {
            "value": "[variables('var1')]",
            "type" : "string"
        },
        "exampleOutput2": {
            "value": "[variables('var2')]",
            "type" : "array"
        },
        "exampleOutput3": {
            "value": "[variables('var3')]",
            "type" : "string"
        },
        "exampleOutput4": {
            "value": "[variables('var4')]",
            "type" : "object"
        }
    }
}
```

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| exampleOutput1 | String | myVariable |
| exampleOutput2 | Matriz | [1, 2, 3, 4] |
| exampleOutput3 | String | myVariable |
| exampleOutput4 |  Objeto | {"property1": "value1", "property2": "value2"} |

## <a name="next-steps"></a>Pasos siguientes
* Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).
* toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).
* tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).
* toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).

