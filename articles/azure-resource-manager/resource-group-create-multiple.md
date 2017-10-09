---
title: aaaDeploy varias instancias de recursos de Azure | Documentos de Microsoft
description: "Usar operación de copia y matrices en un tooiterate de plantilla de Azure Resource Manager varias veces al implementar los recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 94d95810-a87b-460f-8e82-c69d462ac3ca
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/26/2017
ms.author: tomfitz
ms.openlocfilehash: a3bd42f694053317c30b639c33dc4efae41a9a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-instances-of-a-resource-or-property-in-azure-resource-manager-templates"></a>Implementación de varias instancias de un recurso o una propiedad en plantillas de Azure Resource Manager
Este tema muestra cómo tooiterate en su toocreate de plantilla de Azure Resource Manager varias instancias de un recurso, o varias instancias de una propiedad en un recurso.

Si necesita tooadd lógica tooyour plantilla que le permite toospecify si se implementa un recurso, vea [implementar de forma condicional recursos](#conditionally-deploy-resource).

## <a name="resource-iteration"></a>Iteración de recursos
toocreate varias instancias de un tipo de recurso, agregue un `copy` tipo de recurso de toohello de elemento. En el elemento de la copia de hello, especificar número de Hola de iteraciones y un nombre para este bucle. el valor del recuento de Hello debe ser un entero positivo y no puede superar los 800. El Administrador de recursos crea recursos de hello en paralelo. Por lo tanto, no se garantiza el orden de hello en el que se crean. toocreate recorren en iteración los recursos de secuencia, vea [serie copia](#serial-copy). 

Hola recursos toocreate varias veces toma Hola siguiendo el formato:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        }
    ],
    "outputs": {}
}
```

Tenga en cuenta que Hola nombre de cada recurso incluye hello `copyIndex()` función, que devuelve la iteración actual de hello en bucle Hola. `copyIndex()` es de base cero. Por lo tanto, Hola siguiente ejemplo:

```json
"name": "[concat('storage', copyIndex())]",
```

Crea estos nombres:

* storage0
* storage1
* storage2.

valor de índice de hello toooffset, puede pasar un valor en función de copyIndex() Hola. Hello número de iteraciones tooperform todavía está especificada en el elemento de la copia de hello, pero valor Hola de copyIndex se desplaza por hello especificado valor. Por lo tanto, Hola siguiente ejemplo:

```json
"name": "[concat('storage', copyIndex(1))]",
```

Crea estos nombres:

* storage1
* storage2
* storage3

operación de copia de Hello es útil al trabajar con matrices, ya que puede recorrer en iteración cada elemento de matriz de Hola. Hola de uso `length` función en hello matriz toospecify Hola un recuento de iteraciones, y `copyIndex` índice actual de hello tooretrieve de matriz de Hola. Por lo tanto, Hola siguiente ejemplo:

```json
"parameters": { 
  "org": { 
     "type": "array", 
     "defaultValue": [ 
         "contoso", 
         "fabrikam", 
         "coho" 
      ] 
  }
}, 
"resources": [ 
  { 
      "name": "[concat('storage', parameters('org')[copyIndex()])]", 
      "copy": { 
         "name": "storagecopy", 
         "count": "[length(parameters('org'))]" 
      }, 
      ...
  } 
]
```

Crea estos nombres:

* storagecontoso
* storagefabrikam
* storagecoho

## <a name="serial-copy"></a>Copia en serie

Cuando usas Hola copiar elemento toocreate varias instancias de un tipo de recurso, el Administrador de recursos de forma predeterminada, implementa esas instancias en paralelo. Sin embargo, puede que desee toospecify ese Hola recursos se implementan en secuencia. Por ejemplo, al actualizar un entorno de producción, puede que desee toostagger Hola actualiza tan solo un número determinado se actualizan al mismo tiempo.

Administrador de recursos proporciona propiedades de elemento de la copia de Hola que permiten tooserially implementan varias instancias. En conjunto de elementos de la copia de hello, `mode` demasiado**serie** y `batchSize` toohello número de instancias toodeploy a la vez. Con el modo de serie, el Administrador de recursos crea una dependencia en las instancias anteriores de bucle de hello, por lo que no se inicia un proceso por lotes hasta que se completa el lote anterior Hola.

```json
"copy": {
    "name": "iterator",
    "count": "[parameters('numberToDeploy')]",
    "mode": "serial",
    "batchSize": 2
},
```

Hello propiedad mode también acepta **paralelo**, que es el valor predeterminado de Hola.

tootest serie copia sin crear recursos reales, Hola de uso después de plantilla que implementa las plantillas anidadas vacías:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex())]",
      "copy": {
        "name": "iterator",
        "count": "[parameters('numberToDeploy')]",
        "mode": "serial",
        "batchSize": 1
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
          }
        }
      }
    }
  ],
  "outputs": {
  }
}
```

En el historial de implementación de hello, tenga en cuenta que Hola implementaciones anidadas se procesan en secuencia.

![implementación en serie](./media/resource-group-create-multiple/serial-copy.png)

Para un escenario más realista, Hola siguiente ejemplo implementa dos instancias en el momento de una VM de Linux desde una plantilla anidada:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "User name for hello Virtual Machine."
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Password for hello Virtual Machine."
            }
        },
        "dnsLabelPrefix": {
            "type": "string",
            "metadata": {
                "description": "Unique DNS Name for hello Public IP used tooaccess hello Virtual Machine."
            }
        },
        "ubuntuOSVersion": {
            "type": "string",
            "defaultValue": "16.04.0-LTS",
            "allowedValues": [
                "12.04.5-LTS",
                "14.04.5-LTS",
                "15.10",
                "16.04.0-LTS"
            ],
            "metadata": {
                "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version."
            }
        }
    },
    "variables": {
        "templatelink": "https://raw.githubusercontent.com/rjmax/Build2017/master/Act1.TemplateEnhancements/Chapter03.LinuxVM.json"
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "[concat('nestedDeployment',copyIndex())]",
            "type": "Microsoft.Resources/deployments",
            "copy": {
                "name": "myCopySet",
                "count": 4,
                "mode": "serial",
                "batchSize": 2
            },
            "properties": {
                "mode": "Incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "adminUsername": {
                        "value": "[parameters('adminUsername')]"
                    },
                    "adminPassword": {
                        "value": "[parameters('adminPassword')]"
                    },
                    "dnsLabelPrefix": {
                        "value": "[parameters('dnsLabelPrefix')]"
                    },
                    "ubuntuOSVersion": {
                        "value": "[parameters('ubuntuOSVersion')]"
                    },
                    "index":{
                        "value": "[copyIndex()]"
                    }
                }
            }
        }
    ]
}
```

## <a name="property-iteration"></a>Iteración de propiedades

toocreate varios valores para una propiedad en un recurso, agregue un `copy` matriz en elemento de propiedades de Hola. Esta matriz contiene objetos, y cada objeto tiene Hola propiedades siguientes:

* nombre: nombre de Hola de hello propiedad toocreate varios valores para
* número - número de Hola de toocreate de valores
* entrada: un objeto que contiene la propiedad Hola valores tooassign toohello  

Hola siguiente ejemplo se muestra cómo tooapply `copy` toohello dataDisks propiedad en una máquina virtual:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "copy": [{
          "name": "dataDisks",
          "count": 3,
          "input": {
              "lun": "[copyIndex('dataDisks')]",
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Tenga en cuenta que, cuando se usa `copyIndex` dentro de una iteración de la propiedad, debe proporcionar el nombre de Hola de iteración de Hola. No tiene nombre de hello tooprovide cuando se usa con la iteración de recursos.

El Administrador de recursos se expande hello `copy` matriz durante la implementación. nombre de Hola de matriz de Hola se convierte en nombre de Hola de propiedad Hola. los valores de entrada de Hola se convierten en Propiedades del objeto Hola. plantilla de Hello implementado se convierte en:

```json
{
  "name": "examplevm",
  "type": "Microsoft.Compute/virtualMachines",
  "apiVersion": "2017-03-30",
  "properties": {
    "storageProfile": {
      "dataDisks": [
          {
              "lun": 0,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 1,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          },
          {
              "lun": 2,
              "createOption": "Empty",
              "diskSizeGB": "1023"
          }
      }],
      ...
```

Puede usar la iteración de recursos y propiedades conjuntamente. Iteración de propiedad de Hola de referencia por su nombre.

```json
{
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[concat(parameters('vnetname'), copyIndex())]",
    "apiVersion": "2016-06-01",
    "copy":{
        "count": 2,
        "name": "vnetloop"
    },
    "location": "[resourceGroup().location]",
    "properties": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "copy": [
            {
                "name": "subnets",
                "count": 2,
                "input": {
                    "name": "[concat('subnet-', copyIndex('subnets'))]",
                    "properties": {
                        "addressPrefix": "[variables('subnetAddressPrefix')[copyIndex('subnets')]]"
                    }
                }
            }
        ]
    }
}
```

Solo puede incluir un elemento de la copia en Propiedades de Hola para cada recurso. toospecify un bucle de iteración de más de una propiedad, se definen varios objetos de matriz de copia de Hola. Cada objeto se recorre en iteración por separado. Por ejemplo, toocreate varias instancias de ambos hello `frontendIPConfigurations` hello y propiedad `loadBalancingRules` propiedad en un equilibrador de carga, definir los objetos en un elemento de solo copia: 

```json
{
    "name": "[variables('loadBalancerName')]",
    "type": "Microsoft.Network/loadBalancers",
    "properties": {
        "copy": [
          {
              "name": "frontendIPConfigurations",
              "count": 2,
              "input": {
                  "name": "[concat('loadBalancerFrontEnd', copyIndex('frontendIPConfigurations', 1))]",
                  "properties": {
                      "publicIPAddress": {
                          "id": "[variables(concat('publicIPAddressID', copyIndex('frontendIPConfigurations', 1)))]"
                      }
                  }
              }
          },
          {
              "name": "loadBalancingRules",
              "count": 2,
              "input": {
                  "name": "[concat('LBRuleForVIP', copyIndex('loadBalancingRules', 1))]",
                  "properties": {
                      "frontendIPConfiguration": {
                          "id": "[variables(concat('frontEndIPConfigID', copyIndex('loadBalancingRules', 1)))]"
                      },
                      "backendAddressPool": {
                          "id": "[variables('lbBackendPoolID')]"
                      },
                      "protocol": "tcp",
                      "frontendPort": "[variables(concat('frontEndPort' copyIndex('loadBalancingRules', 1))]",
                      "backendPort": "[variables(concat('backEndPort' copyIndex('loadBalancingRules', 1))]",
                      "probe": {
                          "id": "[variables('lbProbeID')]"
                      }
                  }
              }
          }
        ],
        ...
    }
}
```

## <a name="depend-on-resources-in-a-loop"></a>Dependencia de los recursos de un bucle
Especifica que se ha implementado un recurso después de otro recurso mediante el uso de hello `dependsOn` elemento. toodeploy un recurso que dependa de colección de Hola de recursos en un bucle, proporcionar nombre Hola de bucle de copia de hello en el elemento dependsOn de Hola. Hola de ejemplo siguiente muestra cómo toodeploy tres cuentas de almacenamiento antes de implementar Hola Máquina Virtual. no se muestra la definición de máquina Virtual completa Hola. Observe que ese elemento de la copia de hello tiene nombre establecido demasiado`storagecopy` y elemento de dependsOn de Hola para hello máquinas virtuales también se establece demasiado`storagecopy`.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "resources": [
        {
            "apiVersion": "2016-01-01",
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(copyIndex(),'storage', uniqueString(resourceGroup().id))]",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {},
            "copy": {
                "name": "storagecopy",
                "count": 3
            }
        },
        {
            "apiVersion": "2015-06-15", 
            "type": "Microsoft.Compute/virtualMachines", 
            "name": "[concat('VM', uniqueString(resourceGroup().id))]",  
            "dependsOn": ["storagecopy"],
            ...
        }
    ],
    "outputs": {}
}
```

## <a name="create-multiple-instances-of-a-child-resource"></a>Creación de varias instancias de un recurso secundario
No puede usar un bucle copy en un recurso secundario. toocreate varias instancias de un recurso que se define normalmente como anidados dentro de otro recurso, en su lugar, debe crear ese recurso como un recurso de nivel superior. Definir relación Hola con recurso primario de Hola a través de las propiedades de tipo y el nombre de Hola.

Por ejemplo, supongamos que suele definir un conjunto de datos como un recurso secundario dentro de una factoría de datos.

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
    "resources": [
    {
        "type": "datasets",
        "name": "exampleDataSet",
        "dependsOn": [
            "exampleDataFactory"
        ],
        ...
    }
}]
```

toocreate varias instancias de conjuntos de datos, muévala fuera de la factoría de datos de Hola. Hola conjunto de datos debe estar en hello como factoría de datos de Hola de mismo nivel, pero sigue siendo un recurso secundario Hola factoría de datos. Conservar la relación de hello entre factoría de datos a través de las propiedades de tipo y el nombre de Hola y el conjunto de datos. Puesto que ya no se puede inferir el tipo de su posición en la plantilla de hello, debe proporcionar el tipo hello completo en formato de hello: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`.

tooestablish una relación primaria-secundaria con una instancia de la factoría de datos de hello, proporcione un nombre para el conjunto de datos de Hola que incluye el nombre del recurso primario Hola. Usar el formato de hello: `{parent-resource-name}/{child-resource-name}`.  

Hello en el ejemplo siguiente se muestra hello implementación:

```json
"resources": [
{
    "type": "Microsoft.DataFactory/datafactories",
    "name": "exampleDataFactory",
    ...
},
{
    "type": "Microsoft.DataFactory/datafactories/datasets",
    "name": "[concat('exampleDataFactory', '/', 'exampleDataSet', copyIndex())]",
    "dependsOn": [
        "exampleDataFactory"
    ],
    "copy": { 
        "name": "datasetcopy", 
        "count": "3" 
    } 
    ...
}]
```

## <a name="conditionally-deploy-resource"></a>Implementar recursos de forma condicional

toospecify si se implementa un recurso, usar hello `condition` elemento. valor de Hola de este elemento resuelve tootrue o false. Hola valor es true, se implementa el recurso de Hola. Hola valor es false, no se implementa el recurso de Hola. Por ejemplo, toospecify si se implementa una nueva cuenta de almacenamiento o se utiliza una cuenta de almacenamiento existente, use:

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

Para obtener un ejemplo del uso de una contraseña o una máquina virtual de toodeploy clave de SSH, consulte [plantilla de condición de nombre de usuario o SSH](https://github.com/rjmax/Build2017/blob/master/Act1.TemplateEnhancements/Chapter05.ConditionalResourcesUsernameOrSsh.json).

## <a name="next-steps"></a>Pasos siguientes
* Si desea toolearn sobre secciones de Hola de una plantilla, consulte [creación de plantillas de administrador de recursos de Azure](resource-group-authoring-templates.md).
* toolearn cómo toodeploy la plantilla, vea [implementar una aplicación con la plantilla de administrador de recursos de Azure](resource-group-template-deploy.md).

