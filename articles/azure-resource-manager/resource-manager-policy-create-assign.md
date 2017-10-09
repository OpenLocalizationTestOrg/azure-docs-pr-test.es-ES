---
title: aaaAssign y administrar las directivas de recursos de Azure | Documentos de Microsoft
description: "Describe cómo tooapply recursos de Azure directivas toosubscriptions grupos y de recursos y cómo las directivas de recursos de tooview."
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
ms.date: 07/26/2017
ms.author: tomfitz
ms.openlocfilehash: b6999b43bbcc80d2fde9911352fd4352fa453443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-and-manage-resource-policies"></a>Asignación y administración de directivas de recursos

tooimplement una directiva, debe realizar estos pasos:

1. Comprobar directiva definiciones (incluidas las directivas integradas proporcionadas por Azure) toosee si ya existe uno en la suscripción que cumple los requisitos.
2. Si existe una, obtenga el nombre.
3. Si no existe, definir la regla de directiva de hello con JSON y agréguela como una definición de directiva en su suscripción. Este paso pone a disposición para la asignación de directiva de hello pero no aplica tooyour suscripción de hello reglas.
4. Para cualquiera de los casos, asignar al ámbito de hello directiva tooa (por ejemplo, un suscripción o grupo de recursos). Ahora se aplican reglas de Hola de directiva de Hola.

En este artículo se centra en hello pasos toocreate una definición de directiva y asignar ese ámbito de tooa definición a través de la API de REST, PowerShell o CLI de Azure. Si prefiere que las directivas de toouse hello tooassign portal, consulte [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md). En este artículo no se centra en la sintaxis de Hola para crear la definición de la directiva de Hola. Para información sobre la sintaxis de directivas, consulte [Uso de directivas para administrar los recursos y controlar el acceso](resource-manager-policy.md).

## <a name="rest-api"></a>API de REST

### <a name="create-policy-definition"></a>Creación de definición de directiva

Puede crear una directiva con hello [API de REST para las definiciones de directiva](/rest/api/resources/policydefinitions). API de REST de Hello permite toocreate y eliminar definiciones de directiva y obtener información acerca de las definiciones existentes.

toocreate una definición de directiva, ejecute:

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

Incluir un toohello similar de cuerpo de solicitud siguiente ejemplo:

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

### <a name="assign-policy"></a>Asignación de directiva

Puede aplicar la definición de la directiva de hello en el ámbito de hello deseado a través de hello [API de REST para las asignaciones de directivas](/rest/api/resources/policyassignments). Hola REST API permite toocreate y eliminar las asignaciones de directivas y obtener información acerca de las asignaciones existentes.

toocreate una asignación de directiva, ejecute:

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

Hello {asignación de directiva} es el nombre del saludo de asignación de directiva de Hola.

Incluir un toohello similar de cuerpo de solicitud siguiente ejemplo:

```json
{
  "properties":{
    "displayName":"West US only policy assignment on hello subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a>Visualización de directiva
tooget una directiva, utilice hello [obtener la definición de directiva](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operación.

### <a name="get-aliases"></a>Obtención de alias
Puede recuperar alias a través de hello API de REST:

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

Hola de ejemplo siguiente muestra una definición de un alias. Como puede ver, un alias define rutas de acceso en distintas versiones de API, aunque se cambie el nombre de la propiedad. 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a>PowerShell

Antes de continuar con los ejemplos de PowerShell de hello, asegúrese de que tiene [instalada la versión más reciente de hello](/powershell/azure/install-azurerm-ps) de PowerShell de Azure. Se agregaron parámetros de directiva en la versión 3.6.0. Si tiene una versión anterior, los ejemplos de hello obtienen que un parámetro hello de error que indica que no se encuentra.

### <a name="view-policy-definitions"></a>Visualización de definiciones de directiva
toosee de comandos de todas las definiciones de directiva en su suscripción, Hola de uso siguientes:

```powershell
Get-AzureRmPolicyDefinition
```

Devuelve todas las definiciones de directiva disponibles, incluidas las directivas integradas. Cada directiva se devuelve en hello siguiendo el formato:

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict hello locations your organization can specify when deploying resources. Use tooenforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

Antes de continuar toocreate una definición de directiva, mire directivas integradas Hola. Si encuentra una directiva integrada que aplica límites de Hola que necesita, puede omitir la creación de una definición de directiva. En su lugar, asignar al ámbito de toohello deseado de hello directiva integrada.

### <a name="create-policy-definition"></a>Creación de definición de directiva
Puede crear una definición de directiva mediante hello `New-AzureRmPolicyDefinition` cmdlet.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'
```            

Hola resultado se almacena en un `$definition` objeto, que se usa durante la asignación de directiva. 

En vez de especificar Hola JSON como un parámetro, puede proporcionar Hola ruta tooa .json archivo que contiene la regla de directiva de Hola.

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

Hello en el ejemplo siguiente se crea una definición de directiva que incluya parámetros:

```powershell
$policy = '{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy toospecify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a>Asignación de directiva

Aplicar directiva de hello en el ámbito de hello deseado mediante hello `New-AzureRmPolicyAssignment` cmdlet. Hola siguiente ejemplo asigna a grupo de recursos de hello directiva tooa.

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

tooassign una directiva que requiere parámetros, cree y de objeto con esos valores. Hello en el ejemplo siguiente se recupera una directiva integrada y pasa los valores de parámetros:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a>Visualización de la asignación de directiva

tooget una asignación de directiva específica, use:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

regla de directiva de hello tooview para una definición de directiva, use:

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>Eliminación de la asignación de directiva 

tooremove una asignación de directiva, use:

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a>CLI de Azure

### <a name="view-policy-definitions"></a>Visualización de definiciones de directiva
toosee de comandos de todas las definiciones de directiva en su suscripción, Hola de uso siguientes:

```azurecli
az policy definition list
```

Devuelve todas las definiciones de directiva disponibles, incluidas las directivas integradas. Cada directiva se devuelve en hello siguiendo el formato:

```azurecli
{                                                            
  "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources. Use tooenforce your geo-compliance requirements.",                      
  "displayName": "Allowed locations",
  "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
  "policyRule": {
    "if": {
      "not": {
        "field": "location",
        "in": "[parameters('listOfAllowedLocations')]"
      }
    },
    "then": {
      "effect": "Deny"
    }
  },
  "policyType": "BuiltIn"
}
```

Antes de continuar toocreate una definición de directiva, mire directivas integradas Hola. Si encuentra una directiva integrada que aplica límites de Hola que necesita, puede omitir la creación de una definición de directiva. En su lugar, asignar al ámbito de toohello deseado de hello directiva integrada.

### <a name="create-policy-definition"></a>Creación de definición de directiva

Puede crear una definición de directiva mediante la CLI de Azure con el comando de definición de directiva de Hola.

```azurecli
az policy definition create --name coolAccessTier --description "Policy toospecify access tier." --rules '{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}'    
```

### <a name="assign-policy"></a>Asignación de directiva

Puede aplicar ámbito de hello directiva toohello deseado mediante el uso de comandos de asignación de directiva de Hola. Hola de ejemplo siguiente asigna a un grupo de recursos de tooa de directiva.

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a>Visualización de la asignación de directiva

tooview una asignación de directiva, proporcione el nombre de asignación de directiva de Hola y el ámbito de hello:

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a>Eliminación de la asignación de directiva 

tooremove una asignación de directiva, use:

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>Pasos siguientes
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

