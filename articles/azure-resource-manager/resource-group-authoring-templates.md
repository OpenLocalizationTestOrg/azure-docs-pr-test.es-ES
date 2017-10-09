---
title: el Administrador de recursos de aaaAzure estructura de plantilla y la sintaxis | Documentos de Microsoft
description: Describe la estructura de Hola y las propiedades de plantillas de Azure Resource Manager mediante la sintaxis declarativa de JSON.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 19694cb4-d9ed-499a-a2cc-bcfc4922d7f5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/14/2017
ms.author: tomfitz
ms.openlocfilehash: b0709852f8777c91cc1704d6bca16257a017d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-structure-and-syntax-of-azure-resource-manager-templates"></a>Comprender la estructura de Hola y la sintaxis de plantillas del Administrador de recursos de Azure
Este tema describe la estructura de Hola de una plantilla de Azure Resource Manager. Muestra las diferentes secciones de Hola de propiedades de plantilla y Hola que están disponibles en dichas secciones. plantilla de Hello consta de JSON y expresiones que puede utilizar valores de tooconstruct para su implementación. Para obtener instrucciones detalladas sobre cómo crear una plantilla, consulte [Creación de la primera plantilla de Azure Resource Manager](resource-manager-create-first-template.md).

## <a name="template-format"></a>Formato de plantilla
En la estructura más sencilla, una plantilla contiene Hola siguientes elementos:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  },
    "variables": {  },
    "resources": [  ],
    "outputs": {  }
}
```

| Nombre del elemento | Obligatorio | Descripción |
|:--- |:--- |:--- |
| $schema |Sí |Ubicación del archivo de esquema JSON de Hola que describe la versión de Hola de idioma de plantilla de Hola. Dirección URL de Hola de uso que se muestra en el anterior ejemplo de Hola. |
| contentVersion |Sí |Versión de plantilla de hello (por ejemplo, 1.0.0.0). Puede especificar cualquier valor para este elemento. Al implementar los recursos mediante la plantilla de hello, este valor puede ser usado toomake que dicha plantilla derecho Hola esté en uso. |
| parameters |No |Valores que se proporcionan cuando la implementación es ejecutan toocustomize implementación de los recursos. |
| variables |No |Valores que se usan como fragmentos JSON en expresiones de idioma de plantilla de hello plantilla toosimplify. |
| resources |Sí |Tipos de servicios que se implementan o actualizan en un grupo de recursos. |
| outputs |No |Valores que se devuelven después de la implementación. |

Cada elemento contiene propiedades que pueden incluirse. Hola siguiente ejemplo contiene sintaxis completa de Hola para una plantilla:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "",
    "parameters": {  
        "<parameter-name>" : {
            "type" : "<type-of-parameter-value>",
            "defaultValue": "<default-value-of-parameter>",
            "allowedValues": [ "<array-of-allowed-values>" ],
            "minValue": <minimum-value-for-int>,
            "maxValue": <maximum-value-for-int>,
            "minLength": <minimum-length-for-string-or-array>,
            "maxLength": <maximum-length-for-string-or-array-parameters>,
            "metadata": {
                "description": "<description-of-hello parameter>" 
            }
        }
    },
    "variables": {  
        "<variable-name>": "<variable-value>",
        "<variable-name>": { 
            <variable-complex-type-value> 
        }
    },
    "resources": [
      {
          "condition": "<boolean-value-whether-to-deploy>",
          "apiVersion": "<api-version-of-resource>",
          "type": "<resource-provider-namespace/resource-type-name>",
          "name": "<name-of-the-resource>",
          "location": "<location-of-resource>",
          "tags": {
              "<tag-name1>": "<tag-value1>",
              "<tag-name2>": "<tag-value2>"
          },
          "comments": "<your-reference-notes>",
          "copy": {
              "name": "<name-of-copy-loop>",
              "count": "<number-of-iterations>",
              "mode": "<serial-or-parallel>",
              "batchSize": "<number-to-deploy-serially>"
          },
          "dependsOn": [
              "<array-of-related-resource-names>"
          ],
          "properties": {
              "<settings-for-the-resource>",
              "copy": [
                  {
                      "name": ,
                      "count": ,
                      "input": {}
                  }
              ]
          },
          "resources": [
              "<array-of-child-resources>"
          ]
      }
    ],
    "outputs": {
        "<outputName>" : {
            "type" : "<type-of-output-value>",
            "value": "<output-value-expression>"
        }
    }
}
```

Se examinan las secciones de Hola de plantilla de hello en mayor detalle más adelante en este tema.

## <a name="expressions-and-functions"></a>Expresiones y funciones
sintaxis básica de Hola de plantilla de hello es JSON. Sin embargo, las expresiones y funciones extienden los valores JSON de hello disponibles dentro de la plantilla de Hola.  Las expresiones se escriben a los literales de cadena JSON cuyo primer y últimos caracteres son corchetes hello: `[` y `]`, respectivamente. valor de Hola de expresión de Hola se evalúa cuando se implementa Hola plantilla. Mientras se escribe como un literal de cadena, el resultado de hello de la evaluación de expresión de hello puede ser de un tipo diferente de JSON, como una matriz o un entero, dependiendo de la expresión real Hola.  toohave iniciar una cadena literal con un corchete de cierre `[`, pero no hacer que se interpreta como una expresión, agregue una cadena de hello toostart corchete adicional con `[[`.

Por lo general, se usan expresiones con operaciones de tooperform de funciones para la configuración de implementación de Hola. Al igual que en JavaScript, las llamadas de función tienen el formato `functionName(arg1,arg2,arg3)`. Hacer referencia a propiedades mediante operadores de hello [índice] y de puntos.

Hola de ejemplo siguiente muestra cómo toouse varias funciones al construir valores:

```json
"variables": {
    "location": "[resourceGroup().location]",
    "usernameAndPassword": "[concat(parameters('username'), ':', parameters('password'))]",
    "authorizationHeader": "[concat('Basic ', base64(variables('usernameAndPassword')))]"
}
```

Para hello lista completa de las funciones de plantilla, consulte [funciones de plantilla de Azure Resource Manager](resource-group-template-functions.md). 

## <a name="parameters"></a>parameters
En la sección de parámetros de Hola de plantilla de hello, especifique los valores que puede introducir al implementar Hola recursos. Estos valores de parámetro permiten la implementación de hello toocustomize proporcionando los valores que se han adaptado en un entorno determinado (por ejemplo, desarrollo, prueba y producción). No tiene parámetros de tooprovide en la plantilla, pero sin parámetros de la plantilla implementa siempre Hola mismos recursos con Hola los mismos nombres, ubicaciones y propiedades.

Definir parámetros con hello siguiente estructura:

```json
"parameters": {
    "<parameter-name>" : {
        "type" : "<type-of-parameter-value>",
        "defaultValue": "<default-value-of-parameter>",
        "allowedValues": [ "<array-of-allowed-values>" ],
        "minValue": <minimum-value-for-int>,
        "maxValue": <maximum-value-for-int>,
        "minLength": <minimum-length-for-string-or-array>,
        "maxLength": <maximum-length-for-string-or-array-parameters>,
        "metadata": {
            "description": "<description-of-hello parameter>" 
        }
    }
}
```

| Nombre del elemento | Obligatorio | Description |
|:--- |:--- |:--- |
| parameterName |Sí |Nombre del parámetro hello. Debe ser un identificador válido de JavaScript. |
| type |Sí |Tipo del valor de parámetro de Hola. Ver lista de Hola de tipos permitidos después de esta tabla. |
| defaultValue |No |Valor predeterminado para el parámetro hello, si no se proporciona ningún valor para el parámetro hello. |
| allowedValues |No |Matriz de valores permitidos para hello parámetro toomake seguro de que se proporciona el valor correcto de Hola. |
| minValue |No |valor mínimo de Hola para parámetros de tipo int, este valor es inclusivo. |
| maxValue |No |valor máximo de Hola para parámetros de tipo int, este valor es inclusivo. |
| minLength |No |longitud mínima de Hola para cadenas, secureString y parámetros de tipo de matriz, este valor es inclusivo. |
| maxLength |No |longitud máxima de Hola para cadenas, secureString y parámetros de tipo de matriz, este valor es inclusivo. |
| description |No |Descripción del parámetro hello muestra toousers a través del portal de Hola. |

Hello valores y los tipos permitidos son:

* **cadena**
* **secureString**
* **int**
* **bool**
* **objeto** 
* **secureObject**
* **matriz**

toospecify un parámetro como opcional, proporcionan un defaultValue (puede ser una cadena vacía). 

Si especifica un nombre de parámetro en la plantilla que coincide con un parámetro de plantilla de hello comando toodeploy Hola, no hay ambigüedad acerca de los valores de hello que proporcione. El Administrador de recursos resuelve esta confusión mediante la adición de postfijo hello **FromTemplate** toohello parámetro de plantilla. Por ejemplo, si incluye un parámetro denominado **ResourceGroupName** en la plantilla, entra en conflicto con hello **ResourceGroupName** parámetro Hola [ Nueva AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet. Durante la implementación, son tooprovide solicitada un valor para **ResourceGroupNameFromTemplate**. En general, debe evitar esta confusión por no nombrar parámetros con el mismo nombre como parámetros que se utilizan para las operaciones de implementación de Hola.

> [!NOTE]
> Todas las contraseñas, claves y otros secretos deben usar hello **secureString** tipo. Si pasa datos confidenciales en un objeto JSON, use hello **secureObject** tipo. No se pueden leer los parámetros con los tipos secureString o secureObject después de la implementación de recursos. 
> 
> Por ejemplo, hello siguiente entrada en el historial de implementación de hello muestra hello valor para una cadena y un objeto, pero no para secureString y secureObject.
>
> ![Visualización de los valores de implementación](./media/resource-group-authoring-templates/show-parameters.png)  
>

Hola siguiente ejemplo se muestra cómo toodefine parámetros:

```json
"parameters": {
    "siteName": {
        "type": "string",
        "defaultValue": "[concat('site', uniqueString(resourceGroup().id))]"
    },
    "hostingPlanName": {
        "type": "string",
        "defaultValue": "[concat(parameters('siteName'),'-plan')]"
    },
    "skuName": {
        "type": "string",
        "defaultValue": "F1",
        "allowedValues": [
          "F1",
          "D1",
          "B1",
          "B2",
          "B3",
          "S1",
          "S2",
          "S3",
          "P1",
          "P2",
          "P3",
          "P4"
        ]
    },
    "skuCapacity": {
        "type": "int",
        "defaultValue": 1,
        "minValue": 1
    }
}
```

Para cómo valores de parámetro de hello tooinput durante la implementación, consulte [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md). 

## <a name="variables"></a>variables
En la sección de variables de hello, crear valores que se pueden utilizar a lo largo de la plantilla. No es necesario toodefine variables, pero a menudo simplifican la plantilla reduciendo expresiones complejas.

Defina variables con hello siguiente estructura:

```json
"variables": {
    "<variable-name>": "<variable-value>",
    "<variable-name>": { 
        <variable-complex-type-value> 
    }
}
```

Hola siguiente ejemplo se muestra cómo toodefine una variable que se construye a partir de dos valores de parámetro:

```json
"variables": {
    "connectionString": "[concat('Name=', parameters('username'), ';Password=', parameters('password'))]"
}
```

ejemplo de Hola siguiente muestra una variable que es un tipo complejo de JSON y las variables que se construyen a partir de otras variables:

```json
"parameters": {
    "environmentName": {
        "type": "string",
        "allowedValues": [
          "test",
          "prod"
        ]
    }
},
"variables": {
    "environmentSettings": {
        "test": {
            "instancesSize": "Small",
            "instancesCount": 1
        },
        "prod": {
            "instancesSize": "Large",
            "instancesCount": 4
        }
    },
    "currentEnvironmentSettings": "[variables('environmentSettings')[parameters('environmentName')]]",
    "instancesSize": "[variables('currentEnvironmentSettings').instancesSize]",
    "instancesCount": "[variables('currentEnvironmentSettings').instancesCount]"
}
```

## <a name="resources"></a>Recursos
En la sección de recursos de hello, definir recursos de Hola que se implementa o se actualizan. En esta sección puede resultar complicada porque debe entender Hola tipos que se va a implementar valores correctos de tooprovide Hola. Para saludo específico del recurso valores (el elemento apiVersion, tipo y propiedades) que necesita tooset, vea [definir los recursos en las plantillas de Azure Resource Manager](/azure/templates/). 

Definir recursos con hello siguiente estructura:

```json
"resources": [
  {
      "condition": "<boolean-value-whether-to-deploy>",
      "apiVersion": "<api-version-of-resource>",
      "type": "<resource-provider-namespace/resource-type-name>",
      "name": "<name-of-the-resource>",
      "location": "<location-of-resource>",
      "tags": {
          "<tag-name1>": "<tag-value1>",
          "<tag-name2>": "<tag-value2>"
      },
      "comments": "<your-reference-notes>",
      "copy": {
          "name": "<name-of-copy-loop>",
          "count": "<number-of-iterations>",
          "mode": "<serial-or-parallel>",
          "batchSize": "<number-to-deploy-serially>"
      },
      "dependsOn": [
          "<array-of-related-resource-names>"
      ],
      "properties": {
          "<settings-for-the-resource>",
          "copy": [
              {
                  "name": ,
                  "count": ,
                  "input": {}
              }
          ]
      },
      "resources": [
          "<array-of-child-resources>"
      ]
  }
]
```

| Nombre del elemento | Obligatorio | Descripción |
|:--- |:--- |:--- |
| condition | No | Valor booleano que indica si se implementa el recurso de Hola. |
| apiVersion |Sí |Versión de hello toouse de API de REST para crear recursos de Hola. |
| type |Sí |Tipo de recurso de Hola. Este valor es una combinación de espacio de nombres de hello del proveedor de recursos de Hola y el tipo de recurso de hello (como **Microsoft.Storage/storageaccounts**). |
| name |Sí |Nombre del recurso de Hola. nombre de Hello debe seguir las restricciones de componente URI definidas en RFC3986. Además, los servicios de Azure que exponen las partes toooutside de nombre de recurso de hello validan hello toomake de nombre seguro no es un intento de toospoof otra identidad. |
| location |Varía |Ubicaciones geográficas admitidas de hello proporcionan recursos. Puede seleccionar cualquiera de las ubicaciones disponibles hello, pero normalmente tiene sentido toopick uno que sea tooyour cierre a los usuarios. Normalmente, también conviene recursos tooplace que interactúan entre sí en hello misma región. La mayoría de los tipos de recursos requieren una ubicación, pero algunos (por ejemplo, una asignación de roles) no la necesitan. Consulte [Establecimiento de la ubicación para recursos en plantillas de Azure Resource Manager](resource-manager-template-location.md). |
| etiquetas |No |Etiquetas que están asociadas con el recurso de Hola. Consulte [Aplicación de etiquetas a recursos en plantillas de Azure Resource Manager](resource-manager-template-tags.md). |
| comentarios |No |Las notas para documentar recursos hello en la plantilla |
| copia |No |Si se necesita más de una instancia, Hola número de recursos toocreate. modo de saludo predeterminado es paralelo. Especificar el modo de serie cuando no desea que todos los ni Hola toodeploy recursos en hello mismo tiempo. Para más información, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md). |
| dependsOn |No |Recursos que se deben implementar antes de implementar este. Administrador de recursos evalúa las dependencias de hello entre los recursos y se implementa en el orden correcto de Hola. Cuando no hay recursos dependientes entre sí, se implementan en paralelo. Hello valor puede ser una lista separada por comas de un recurso de nombres o identificadores únicos de recursos. Solo los recursos de lista que se implementan en esta plantilla. Deben existir los recursos que no estén definidos en esta plantilla. Evite agregar dependencias innecesarias, ya que pueden ralentizar la implementación y crear dependencias circulares. Para obtener instrucciones sobre la configuración de dependencias, consulte [Definición de dependencias en plantillas de Azure Resource Manager](resource-group-define-dependencies.md). |
| propiedades |No |Opciones de configuración específicas de recursos. valores de Hello para propiedades de Hola se Hola mismo como valores de hello que proporcione en el cuerpo de la solicitud de Hola Hola API de REST operación (método PUT) toocreate Hola recurso. También puede especificar un toocreate de matriz de copia de varias instancias de una propiedad. Para más información, consulte [Creación de varias instancias de recursos en Azure Resource Manager](resource-group-create-multiple.md). |
| resources |No |Recursos secundarios que dependen del recurso de Hola que se está definiendo. Solo se proporcionan tipos de recursos que se permiten en esquema de Hola de recurso primario de Hola. Hello nombre completo del tipo de recurso de hello secundario incluye tipo de recurso de hello primario, como **Microsoft.Web/sites/extensions**. Dependencia de recurso de hello primario no está implícita. Debe definirla explícitamente. |

sección de recursos de Hello contiene una matriz de hello recursos toodeploy. En cada recurso, puede definir también una matriz de recursos secundarios. Por lo tanto, la sección de recursos podría tener una estructura como:

```json
"resources": [
  {
      "name": "resourceA",
  },
  {
      "name": "resourceB",
      "resources": [
        {
            "name": "firstChildResourceB",
        },
        {   
            "name": "secondChildResourceB",
        }
      ]
  },
  {
      "name": "resourceC",
  }
]
```      

Para obtener más información sobre la definición de recursos secundarios, consulte [Establecimiento del nombre y el tipo de recurso secundario en la plantilla de Resource Manager](resource-manager-template-child-resource.md).

Hola **condición** elemento especifica si se implementa el recurso de Hola. valor de Hola de este elemento resuelve tootrue o false. Por ejemplo, toospecify si se implementa una nueva cuenta de almacenamiento, use:

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

Para obtener un ejemplo del uso de un recurso nuevo o existente, vea la [plantilla de condición nueva o existente](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResources.NewOrExisting.json).

toospecify si se implementa una máquina virtual con una contraseña o clave SSH, definir dos versiones de la máquina virtual de hello en la plantilla y usar **condición** toodifferentiate uso. Pasar un parámetro que especifica qué toodeploy escenario.

```json
{
    "condition": "[equals(parameters('passwordOrSshKey'),'password')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'password')]",
    "properties": {
        "osProfile": {
            "computerName": "[variables('vmName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
        },
        ...
    },
    ...
},
{
    "condition": "[equals(parameters('passwordOrSshKey'),'sshKey')]",
    "apiVersion": "2016-03-30",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('vmName'),'ssh')]",
    "properties": {
        "osProfile": {
            "linuxConfiguration": {
                "disablePasswordAuthentication": "true",
                "ssh": {
                    "publicKeys": [
                        {
                            "path": "[variables('sshKeyPath')]",
                            "keyData": "[parameters('adminSshKey')]"
                        }
                    ]
                }
            }
        },
        ...
    },
    ...
}
``` 

Para obtener un ejemplo del uso de una contraseña o una máquina virtual de toodeploy clave de SSH, consulte [plantilla de condición de nombre de usuario o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="outputs"></a>Salidas
En la sección de salidas de hello, especifique los valores que se devuelven de la implementación. Por ejemplo, podría devolver Hola URI tooaccess un recurso implementado.

Hello en el ejemplo siguiente se muestra hello estructura de una definición de salida:

```json
"outputs": {
    "<outputName>" : {
        "type" : "<type-of-output-value>",
        "value": "<output-value-expression>"
    }
}
```

| Nombre del elemento | Obligatorio | Descripción |
|:--- |:--- |:--- |
| outputName |Sí |Nombre del valor de salida de hello. Debe ser un identificador válido de JavaScript. |
| type |Sí |Tipo de valor de salida de hello. Los valores de salida admiten Hola mismo tipos como parámetros de entrada de plantilla. |
| value |yes |Expresión de lenguaje de plantilla que se evaluará y devolverá como valor de salida. |

Hello en el ejemplo siguiente se muestra un valor que se devuelve en la sección de salidas de Hola.

```json
"outputs": {
    "siteUri" : {
        "type" : "string",
        "value": "[concat('http://',reference(resourceId('Microsoft.Web/sites', parameters('siteName'))).hostNames[0])]"
    }
}
```

Para más información sobre cómo trabajar con resultados, consulte [Uso compartido del estado con las plantillas de Azure Resource Manager](best-practices-resource-manager-state.md).

## <a name="template-limits"></a>Límites de plantilla

Limitar tamaño de saludo de la plantilla too1 MB y cada parámetro too64 KB de archivo. límite de 1 MB de Hola aplica toohello estado final de la plantilla de hello después de que se ha ampliado con las definiciones de recursos iterativo y valores para las variables y parámetros. 

También está limitado a:

* 256 parámetros
* 256 variables
* 800 recursos (incluido el recuento de copia)
* 64 valores de salida
* 24 576 caracteres en una expresión de plantilla

Puede superar algunos límites de plantilla utilizando una plantilla anidada. Para más información, consulte [Uso de plantillas vinculadas en la implementación de recursos de Azure](resource-group-linked-templates.md). número de hello tooreduce de parámetros, variables o salidas, puede combinar varios valores en un objeto. Para más información, consulte [Objetos como parámetros](resource-manager-objects-as-parameters.md).

## <a name="next-steps"></a>Pasos siguientes
* tooview completa plantillas para muchos tipos distintos de soluciones, vea hello [plantillas de inicio rápido de Azure](https://azure.microsoft.com/documentation/templates/).
* Para obtener más información acerca de las funciones de Hola que puede utilizar desde dentro de una plantilla, consulte [funciones de plantilla de administrador de recursos de Azure](resource-group-template-functions.md).
* toocombine varias plantillas durante la implementación, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).
* Puede que tenga recursos toouse que existen dentro de otro grupo de recursos. Este escenario es habitual al trabajar con cuentas de almacenamiento o redes virtuales que se comparten entre varios grupos de recursos. Para obtener más información, vea hello [función resourceId](resource-group-template-functions-resource.md#resourceid).
