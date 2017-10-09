---
title: grupos de recursos de toomultiple aaaDeploy recursos de Azure | Documentos de Microsoft
description: "Muestra cómo agrupar tootarget más de un recurso de Azure durante la implementación."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a>Implementar toomore de recursos de Azure a un grupo de recursos

Normalmente, implementar todos los recursos de hello en el plantilla tooa único grupo de recursos. Sin embargo, hay escenarios donde desea toodeploy un conjunto de recursos entre sí pero colocarlas en distintos grupos de recursos. Por ejemplo, puede que desee máquina toodeploy Hola de copia de seguridad virtual para la ubicación y el grupo de recursos independiente de Azure Site Recovery tooa. El Administrador de recursos permite toouse anidado plantillas tootarget distintos grupos de recursos de grupo de recursos de hello utilizado para la plantilla de elemento primario de Hola.

grupo de recursos de Hello es el contenedor de ciclo de vida de hello para la aplicación hello y su colección de recursos. Crear grupo de recursos de hello fuera de la plantilla de Hola y especificar tootarget de grupo de recursos de Hola durante la implementación. Para un grupos de tooresource introducción, consulte [Introducción a Azure Resource Manager](resource-group-overview.md).

## <a name="example-template"></a>Plantilla de ejemplo

tootarget un recurso diferente, debe usar una plantilla anidada o vinculada durante la implementación. Hola `Microsoft.Resources/deployments` tipo de recurso proporciona un `resourceGroup` parámetro que permite toospecify otro grupo de recursos para hello anidados implementación. Todos los grupos de recursos de hello deben existir antes de ejecutar la implementación de Hola. Hello en el ejemplo siguiente se implementa dos cuentas de almacenamiento: uno en el grupo de recursos de hello especificado durante la implementación y uno en un grupo de recursos denominado `crossResourceGroupDeployment`:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

Si establece `resourceGroup` toohello el nombre de un grupo de recursos que no existe, Hola implementación produce un error. Si no proporciona un valor para `resourceGroup`, Administrador de recursos usa el grupo de recursos de hello primario.  

## <a name="deploy-hello-template"></a>Implementar la plantilla de Hola

plantilla de ejemplo de Hola toodeploy, puede usar el portal hello, Azure PowerShell o CLI de Azure. En el caso de Azure PowerShell o la CLI de Azure, debe usar una versión de mayo de 2017 o posterior. Hola ejemplos se supone que ha guardado localmente plantilla Hola como un archivo denominado **crossrgdeployment.json**.

Para PowerShell:

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

Para la CLI de Azure:

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

Una vez finalizada la implementación, verá dos grupos de recursos. Cada uno contiene una cuenta de almacenamiento.

## <a name="use-resourcegroup-function"></a>Usar la función resourceGroup()

De entre las implementaciones del grupo de recursos, hello [resouceGroup() función](resource-group-template-functions-resource.md#resourcegroup) resuelve diferente en función de cómo especificar plantilla anidada Hola. 

Si incrusta una plantilla dentro de otra, resouceGroup() en plantillas anidadas Hola resuelve grupo de recursos de toohello primario. Una plantilla de embedded utiliza Hola siguiendo el formato:

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

Si crea un vínculo tooa de plantilla independiente, resouceGroup() en la plantilla vinculada Hola resuelve toohello grupo de recursos anidados. Una plantilla vinculada usa Hola siguiendo el formato:

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a>Pasos siguientes

* toounderstand toodefine parámetros de la plantilla, vea [comprender la estructura de Hola y la sintaxis de plantillas de Azure Resource Manager](resource-group-authoring-templates.md).
* Para obtener sugerencias para resolver los errores de implementación más comunes, consulte [Solución de errores comunes de implementación de Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Para más información sobre la implementación de una plantilla que requiere un token de SAS, vea [Implementación de una plantilla privada con el token de SAS](resource-manager-powershell-sas-token.md).
