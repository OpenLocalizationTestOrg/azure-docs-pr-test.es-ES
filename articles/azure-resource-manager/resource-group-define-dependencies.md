---
title: "orden de implementación de aaaSet para recursos de Azure | Documentos de Microsoft"
description: "Describe cómo se implementan tooset un recurso como dependiente de otro recurso durante tooensure los recursos de implementación en el orden correcto de Hola."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a>Definir el criterio de Hola para implementar recursos en las plantillas de Azure Resource Manager
Para un recurso determinado, puede haber otros recursos que deben existir antes de implementan los recursos de Hola. Por ejemplo, un servidor SQL server debe existir antes de intentar toodeploy una base de datos SQL. Definir esta relación marcando un recurso como dependiente de hello otro recurso. Definir una dependencia con hello **dependsOn** elemento, o mediante el uso de hello **referencia** función. 

Administrador de recursos evalúa las dependencias de hello entre los recursos y se implementa en su orden dependiente. Cuando no hay recursos dependientes entre sí, Administrador de recursos los implementa en paralelo. Solo necesita toodefine dependencias de recursos que se implementan en hello misma plantilla. 

## <a name="dependson"></a>dependsOn
Dentro de la plantilla, Hola dependsOn elemento le permite toodefine un recurso como una dependencia en uno o varios recursos. Su valor puede ser una lista de nombres de recursos separados por coma. 

Hello en el ejemplo siguiente se muestra un conjunto de escalas de máquina virtual que depende de un equilibrador de carga, la red virtual y un bucle que crea varias cuentas de almacenamiento. Estos otros recursos no se muestran en el siguiente ejemplo de Hola, pero se necesitan tooexist en otra parte de la plantilla de Hola.

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

En el anterior ejemplo de Hola, se incluye una dependencia en los recursos de Hola que se crean a través de un bucle de copia con el nombre **storageLoop**. Para ver un ejemplo, consulte [Creación de varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md)

Al definir las dependencias, puede incluir Hola recursos proveedor espacio de nombres y el recurso de tipo tooavoid ambigüedad. Por ejemplo, tooclarify con formato de un equilibrador de carga y la red virtual que puede tener Hola de que mismos nombres de otros recursos, Hola de uso después:

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

Aunque puede ser toouse inclinada dependsOn toomap relaciones entre los recursos, es importante toounderstand ¿por qué se está realizando. Por ejemplo, toodocument cómo están conectados entre sí en recursos, dependsOn no es el enfoque correcto de Hola. No se pueden consultar los recursos que se definieron en el elemento dependsOn de hello después de la implementación. El uso de dependsOn podría llegar a repercutir en el tiempo de implementación, ya que Resource Manager no implementa dos recursos en paralelo que tengan una dependencia. en su lugar use toodocument relaciones entre los recursos, [vincular los recursos](/rest/api/resources/resourcelinks).

## <a name="child-resources"></a>Recursos secundarios
propiedad de recursos de Hello permite recursos secundarios de toospecify que recursos toohello relacionados que se está definiendo. Los recursos secundarios solo se pueden definir en cinco niveles de profundidad. Es importante creado toonote que no es de una dependencia implícita entre un recurso secundario y el recurso primario de Hola. Si necesita hello toobe de recursos secundarios implementada después de recurso primario de hello, debe indicar explícitamente esa dependencia con la propiedad de dependsOn de Hola. 

Cada recurso primario solo acepta determinados tipos de recursos como recursos secundarios. Hola acepta tipos de recursos se especifican en hello [esquema de la plantilla](https://github.com/Azure/azure-resource-manager-schemas) de recurso primario de Hola. Hola nombre secundario del tipo de recurso incluye Hola de tipo de recurso de hello primario, como **Microsoft.Web/sites/config** y **Microsoft.Web/sites/extensions** son ambos recursos secundarios de hello  **Microsoft.Web/sites**.

Hola de ejemplo siguiente muestra un SQL server y la base de datos SQL. Tenga en cuenta que se define una dependencia explícita entre la base de datos SQL de Hola y SQL server, incluso si la base de datos de hello es un elemento secundario del servidor de Hola.

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a>función reference
Hola [hacen referencia a función](resource-group-template-functions-resource.md#reference) permite una expresión tooderive su valor desde otros pares de nombre y valor JSON o recursos en tiempo de ejecución. Las expresiones de referencia declaran implícitamente que un recurso depende de otro. Hola de formato general es:

```json
reference('resourceName').propertyPath
```

En el siguiente ejemplo de Hola, un punto de conexión de red CDN depende explícitamente de perfil de CDN Hola e implícitamente depende de una aplicación web.

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

Puede usar este elemento u Hola dependencias de toospecify de elemento dependsOn, pero no es necesario toouse ambos para hello mismo recurso dependiente. Siempre que sea posible, utilice un tooavoid de referencia implícita agregando una dependencia innecesaria.

más información, consulte toolearn [hacen referencia a función](resource-group-template-functions-resource.md#reference).

## <a name="recommendations-for-setting-dependencies"></a>Recomendaciones para configurar las dependencias

La hora de decidir qué tooset dependencias, use Hola siguientes instrucciones:

* Establezca el menor número de dependencias posible.
* Establezca un recurso secundario como dependiente de su recurso principal.
* Hola de uso **referencia** funcionar tooset implícita dependencias entre los recursos que necesitan tooshare una propiedad. No agregue una dependencia explícita (**dependsOn**) cuando ya haya definido una dependencia implícita. Este enfoque reduce el riesgo de Hola de que tengan dependencias innecesarias. 
* Establezca una dependencia cuando no se pueda **crear** un recurso sin la funcionalidad de otro recurso. No establezca una dependencia si los recursos de hello interactúan solo después de la implementación.
* Permita dependencias en cascada sin establecerlas explícitamente. Por ejemplo, la máquina virtual depende de una interfaz de red virtual, y depende de la interfaz de red virtual de hello en una red virtual y las direcciones IP públicas. Por lo tanto, máquina virtual de hello es implementados tres todos los recursos, pero no establece explícitamente como dependiente de todos los recursos de tres máquinas virtuales de Hola. Este enfoque aclara el orden de dependencia de Hola y resulta más fácil de plantilla de hello toochange más adelante.
* Si no se puede determinar un valor antes de la implementación, intente realizar la implementación de recursos de hello sin una dependencia. Por ejemplo, si un valor de configuración requiere nombre de Hola de otro recurso, no necesitará una dependencia. Esta guía no siempre funcionará porque algunos recursos comprueban la existencia de hello del programa Hola a otro recurso. Si recibe un error, agregue una dependencia. 

Resource Manager identifica dependencias circulares durante la validación de plantillas. Si recibe un error que indica que existe una dependencia circular, evaluar su toosee plantilla si todas las dependencias no son necesarios y se pueden quitar. Si quitar dependencias no funciona, puede evitar dependencias circulares moviendo algunas operaciones de implementación a los recursos secundarios que se implementan después de recursos de Hola que tienen una dependencia circular Hola. Por ejemplo, suponga que va a implementar dos máquinas virtuales pero debe establecer las propiedades en cada uno de ellos que hacen referencia toohello otro. Puede implementarlos en hello siguiente orden:

1. vm1
2. vm2
3. La extensión en vm1 depende de vm1 y vm2. extensión de Hello establece valores en vm1 que obtiene de vm2.
4. La extensión en vm2 depende de vm1 y vm2. extensión de Hello establece valores en vm2 que obtiene de vm1.

Para obtener información sobre cómo evaluar el orden de implementación de Hola y resolver errores de dependencia, vea [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md).

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de cómo solucionar problemas de dependencias durante la implementación, consulte [solucionar errores comunes de implementación de Azure con el Administrador de recursos de Azure](resource-manager-common-deployment-errors.md).
* toolearn acerca de cómo crear plantillas de Azure Resource Manager, consulte [crear plantillas](resource-group-authoring-templates.md). 
* Para obtener una lista de funciones disponibles de hello en una plantilla, consulte [funciones de plantilla](resource-group-template-functions.md).

