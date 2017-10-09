---
title: plantilla de administrador de recursos de aaaExport con CLI de Azure | Documentos de Microsoft
description: Use el Administrador de recursos de Azure y Azure CLI tooexport una plantilla a partir de un grupo de recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a>Exportación de plantillas de Azure Resource Manager con CLI de Azure

El Administrador de recursos permite tooexport una plantilla de administrador de recursos de los recursos existentes en su suscripción. Puede usar ese toolearn plantilla generada sobre Hola plantilla sintaxis o tooautomate Hola volver a implementar la solución según sea necesario.

Es importante toonote que hay dos tooexport de distintas formas una plantilla:

* Puede exportar Hola real de la plantilla que usa para una implementación. plantilla exportada Hola incluye todas las variables y parámetros de hello exactamente tal y como aparecían en la plantilla original Hola. Este enfoque es útil cuando es necesario tooretrieve una plantilla.
* Puede exportar una plantilla que representa el estado actual de Hola Hola del grupo de recursos. plantilla exportada Hello no se basa en cualquier plantilla que utiliza para la implementación. En su lugar, crea una plantilla que es una instantánea Hola del grupo de recursos. plantilla exportada Hello tiene muchos valores codificados de forma rígida y probablemente no tantos parámetros como normalmente tendría que definir. Este enfoque es útil cuando se ha modificado el grupo de recursos de Hola. Ahora, debe grupo de recursos de hello toocapture como una plantilla.

En este tema se muestran ambos métodos.

## <a name="deploy-a-solution"></a>Implementación de una solución

tooillustrate ambos enfoques para exportar una plantilla, puede empezar mediante la implementación de una suscripción de tooyour de solución. Si ya tiene un grupo de recursos en la suscripción que desea tooexport, no es necesario toodeploy esta solución. Sin embargo, Hola resto de este artículo se hace referencia toohello plantilla para esta solución. script de ejemplo de Hola implementa una cuenta de almacenamiento.

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a>Guardado de una plantilla desde el historial de implementación

Puede recuperar una plantilla desde el historial de implementación mediante hello [exportación de implementación de grupo az](/cli/azure/group/deployment#export) comando. Hola siguiendo el ejemplo de plantilla de hello guarda antes de implementar:

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

Devuelve la plantilla de Hola. Copie Hola JSON y guárdelo como un archivo. Tenga en cuenta que es Hola plantilla exacto utilizado para la implementación. variables y parámetros de hello coinciden con plantilla de Hola desde GitHub. Puede volver a implementar esta plantilla.


## <a name="export-resource-group-as-template"></a>Exportación de un grupo de recursos como una plantilla

En lugar de recuperar una plantilla de historial de implementación de hello, puede recuperar una plantilla que representa el estado actual de Hola de un grupo de recursos mediante el uso de hello [exportación de grupo az](/cli/azure/group#export) comando. Utilice este comando cuando haya realizado muchos cambios tooyour grupo de recursos y ninguna plantilla existente representa todos los cambios de Hola.

```azurecli
az group export --name ExampleGroup
```

Devuelve la plantilla de Hola. Copie Hola JSON y guárdelo como un archivo. Tenga en cuenta que es diferente de la plantilla de hello en GitHub. Tiene parámetros diferentes y no hay ninguna variable. almacenamiento de Hello SKU y la ubicación son toovalues codificado de forma rígida. Hello en el ejemplo siguiente se muestra plantilla exportada hello, pero la plantilla tiene un nombre de parámetro ligeramente diferente:

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

Puede volver a esta plantilla, pero requiere adivinar un nombre único para la cuenta de almacenamiento de Hola. nombre de Hola de su parámetro es ligeramente diferente.

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a>Personalización de la plantilla exportada

Puede modificar esta plantilla toomake se toouse más fácil y más flexibles. tooallow para obtener más ubicaciones, toouse de propiedad de ubicación de cambio Hola Hola misma ubicación que el grupo de recursos de hello:

```json
"location": "[resourceGroup().location]",
```

tooavoid tener tooguess un nombre de UNIQUE para la cuenta de almacenamiento, remove Hola parámetro de nombre de cuenta de almacenamiento de Hola. Agregue un parámetro para un sufijo de nombre de almacenamiento y una SKU de almacenamiento:

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

Agregue una variable que se construye el nombre de cuenta de almacenamiento de hello con función de hello uniqueString:

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

Hola nombre de variable de toohello de cuenta de almacenamiento de hello del conjunto:

```json
"name": "[variables('storageAccountName')]",
```

Establecer Hola SKU toohello parámetro:

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

La plantilla ahora tiene el aspecto siguiente:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Volver a implementar la plantilla modificada Hola.

## <a name="next-steps"></a>Pasos siguientes
* Para obtener información acerca del uso de hello portal tooexport una plantilla, consulte [exportar una plantilla de Azure Resource Manager de los recursos existentes](resource-manager-export-template.md).
* toodefine parámetros de plantilla, vea [crear plantillas](resource-group-authoring-templates.md#parameters).
* Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).