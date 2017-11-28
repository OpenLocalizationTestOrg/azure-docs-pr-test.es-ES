---
title: "Asignación y administración de directivas de recursos de Azure | Microsoft Docs"
description: "Describe cómo aplicar directivas de recursos de Azure a las suscripciones y a los grupos de recursos y cómo ver directivas de recursos."
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
ms.openlocfilehash: b204cffa8fab0ad27a9f78a81c04f0a0225d95f5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="92e54-103">Asignación y administración de directivas de recursos</span><span class="sxs-lookup"><span data-stu-id="92e54-103">Assign and manage resource policies</span></span>

<span data-ttu-id="92e54-104">Para implementar una directiva, debe realizar estos pasos:</span><span class="sxs-lookup"><span data-stu-id="92e54-104">To implement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="92e54-105">Compruebe las definiciones de directiva (incluidas las directivas integradas proporcionadas por Azure) para ver si ya existe una en la suscripción que cumpla sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="92e54-105">Check policy definitions (including built-in policies provided by Azure) to see if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="92e54-106">Si existe una, obtenga el nombre.</span><span class="sxs-lookup"><span data-stu-id="92e54-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="92e54-107">Si no existe, defina la regla de directiva con JSON y agréguela como una definición de directiva en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="92e54-107">If one does not exist, define the policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="92e54-108">Este paso hace que la directiva esté disponible para la asignación, pero no aplica las reglas a la suscripción.</span><span class="sxs-lookup"><span data-stu-id="92e54-108">This step makes the policy available for assignment but does not apply the rules to your subscription.</span></span>
4. <span data-ttu-id="92e54-109">En cada caso, asigne la directiva a un ámbito (por ejemplo, una suscripción o un grupo de recursos).</span><span class="sxs-lookup"><span data-stu-id="92e54-109">For either case, assign the policy to a scope (such as a subscription or resource group).</span></span> <span data-ttu-id="92e54-110">Ahora se exige el cumplimiento de las reglas de la directiva.</span><span class="sxs-lookup"><span data-stu-id="92e54-110">The rules of the policy are now enforced.</span></span>

<span data-ttu-id="92e54-111">Este artículo se centra en los pasos necesarios para crear una definición de directiva y asignarla a un ámbito mediante la API de REST, PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="92e54-111">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="92e54-112">Si prefiere usar el portal para asignar directivas, consulte [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Uso de Azure Portal para asignar y administrar directivas de recursos).</span><span class="sxs-lookup"><span data-stu-id="92e54-112">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="92e54-113">El artículo no se centra en la sintaxis para crear la definición de la directiva.</span><span class="sxs-lookup"><span data-stu-id="92e54-113">This article does not focus on the syntax for creating the policy definition.</span></span> <span data-ttu-id="92e54-114">Para información sobre la sintaxis de directivas, consulte [Uso de directivas para administrar los recursos y controlar el acceso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="92e54-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="92e54-115">API de REST</span><span class="sxs-lookup"><span data-stu-id="92e54-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="92e54-116">Creación de definición de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-116">Create policy definition</span></span>

<span data-ttu-id="92e54-117">Puede crear una directiva con la [API de REST para definiciones de directiva](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="92e54-117">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="92e54-118">La API de REST permite crear y eliminar definiciones de directiva, así como recuperar información sobre las definiciones existentes.</span><span class="sxs-lookup"><span data-stu-id="92e54-118">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="92e54-119">Para crear una definición de directiva, ejecute:</span><span class="sxs-lookup"><span data-stu-id="92e54-119">To create a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="92e54-120">Incluya un cuerpo de solicitud similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="92e54-120">Include a request body similar to the following example:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
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

### <a name="assign-policy"></a><span data-ttu-id="92e54-121">Asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-121">Assign policy</span></span>

<span data-ttu-id="92e54-122">Puede aplicar la definición de la directiva en el ámbito deseado a través de la [API de REST para asignaciones de directivas](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="92e54-122">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="92e54-123">La API de REST permite crear y eliminar asignaciones de directiva, así como recuperar información sobre las asignaciones existentes.</span><span class="sxs-lookup"><span data-stu-id="92e54-123">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="92e54-124">Para crear una nueva asignación de directiva, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="92e54-124">To create a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="92e54-125">{policy-assignment} es el nombre de la asignación de directiva.</span><span class="sxs-lookup"><span data-stu-id="92e54-125">The {policy-assignment} is the name of the policy assignment.</span></span>

<span data-ttu-id="92e54-126">Incluya un cuerpo de solicitud similar al ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="92e54-126">Include a request body similar to the following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on the subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="92e54-127">Visualización de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-127">View policy</span></span>
<span data-ttu-id="92e54-128">Para obtener una directiva, use la operación [Obtener definición de directiva](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get).</span><span class="sxs-lookup"><span data-stu-id="92e54-128">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="92e54-129">Obtención de alias</span><span class="sxs-lookup"><span data-stu-id="92e54-129">Get aliases</span></span>
<span data-ttu-id="92e54-130">Puede recuperar alias a través de la API de REST:</span><span class="sxs-lookup"><span data-stu-id="92e54-130">You can retrieve aliases through the REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="92e54-131">En el ejemplo siguiente se muestra una definición de un alias.</span><span class="sxs-lookup"><span data-stu-id="92e54-131">The following example shows a definition of an alias.</span></span> <span data-ttu-id="92e54-132">Como puede ver, un alias define rutas de acceso en distintas versiones de API, aunque se cambie el nombre de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="92e54-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="92e54-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="92e54-133">PowerShell</span></span>

<span data-ttu-id="92e54-134">Antes de continuar con los ejemplos de PowerShell, asegúrese de que tiene [instalada la última versión](/powershell/azure/install-azurerm-ps) de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92e54-134">Before proceeding with the PowerShell examples, make sure you have [installed the latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="92e54-135">Se agregaron parámetros de directiva en la versión 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="92e54-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="92e54-136">Si tiene una versión anterior, los ejemplos devuelven un error que indica que no se encuentra el parámetro.</span><span class="sxs-lookup"><span data-stu-id="92e54-136">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="92e54-137">Visualización de definiciones de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-137">View policy definitions</span></span>
<span data-ttu-id="92e54-138">Para ver todas las definiciones de directiva en su suscripción, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="92e54-138">To see all policy definitions in your subscription, use the following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="92e54-139">Devuelve todas las definiciones de directiva disponibles, incluidas las directivas integradas.</span><span class="sxs-lookup"><span data-stu-id="92e54-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="92e54-140">Cada directiva se devuelve con el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="92e54-140">Each policy is returned in the following format:</span></span>

```powershell
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict the locations your organization can specify when deploying resources. Use to enforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

<span data-ttu-id="92e54-141">Antes de continuar con la creación de la definición de la directiva, observe las directivas integradas.</span><span class="sxs-lookup"><span data-stu-id="92e54-141">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="92e54-142">Si encuentra una directiva integrada que se aplica a los límites que necesita, puede omitir la creación de una definición de directiva.</span><span class="sxs-lookup"><span data-stu-id="92e54-142">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="92e54-143">En su lugar, asigne la directiva integrada al ámbito deseado.</span><span class="sxs-lookup"><span data-stu-id="92e54-143">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="92e54-144">Creación de definición de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-144">Create policy definition</span></span>
<span data-ttu-id="92e54-145">Puede crear una definición de directiva con el cmdlet `New-AzureRmPolicyDefinition`.</span><span class="sxs-lookup"><span data-stu-id="92e54-145">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy '{
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

<span data-ttu-id="92e54-146">La salida se almacena en un objeto `$definition`, que se usa durante la asignación de directivas.</span><span class="sxs-lookup"><span data-stu-id="92e54-146">The output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="92e54-147">En vez de especificar JSON como un parámetro, puede proporcionar la ruta de acceso a un archivo .json que contiene la regla de directiva.</span><span class="sxs-lookup"><span data-stu-id="92e54-147">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy to specify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="92e54-148">En el ejemplo siguiente se crea una definición de directiva que incluye parámetros:</span><span class="sxs-lookup"><span data-stu-id="92e54-148">The following example creates a policy definition that includes parameters:</span></span>

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
          "description": "The list of locations that can be specified when deploying storage accounts.",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
    }
}' 

$definition = New-AzureRmPolicyDefinition -Name storageLocations -Description "Policy to specify locations for storage accounts." -Policy $policy -Parameter $parameters 
```

### <a name="assign-policy"></a><span data-ttu-id="92e54-149">Asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-149">Assign policy</span></span>

<span data-ttu-id="92e54-150">Aplique la directiva al ámbito deseado mediante el cmdlet `New-AzureRmPolicyAssignment`.</span><span class="sxs-lookup"><span data-stu-id="92e54-150">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="92e54-151">En el ejemplo siguiente se asigna la directiva a un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="92e54-151">The following example assigns the policy to a resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="92e54-152">Para asignar una directiva que requiera parámetros, realice la creación y establezca el objeto con esos valores.</span><span class="sxs-lookup"><span data-stu-id="92e54-152">To assign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="92e54-153">En el ejemplo siguiente se recupera una directiva integrada y se pasan los valores de parámetros:</span><span class="sxs-lookup"><span data-stu-id="92e54-153">The following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="92e54-154">Visualización de la asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-154">View policy assignment</span></span>

<span data-ttu-id="92e54-155">Para obtener una asignación de directiva específica, use:</span><span class="sxs-lookup"><span data-stu-id="92e54-155">To get a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="92e54-156">Para ver la regla de directiva de una definición de directiva, use:</span><span class="sxs-lookup"><span data-stu-id="92e54-156">To view the policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="92e54-157">Eliminación de la asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-157">Remove policy assignment</span></span> 

<span data-ttu-id="92e54-158">Para quitar una asignación de directiva, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="92e54-158">To remove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="92e54-159">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="92e54-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="92e54-160">Visualización de definiciones de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-160">View policy definitions</span></span>
<span data-ttu-id="92e54-161">Para ver todas las definiciones de directiva en su suscripción, utilice el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="92e54-161">To see all policy definitions in your subscription, use the following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="92e54-162">Devuelve todas las definiciones de directiva disponibles, incluidas las directivas integradas.</span><span class="sxs-lookup"><span data-stu-id="92e54-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="92e54-163">Cada directiva se devuelve con el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="92e54-163">Each policy is returned in the following format:</span></span>

```azurecli
{                                                            
  "description": "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.",                      
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

<span data-ttu-id="92e54-164">Antes de continuar con la creación de la definición de la directiva, observe las directivas integradas.</span><span class="sxs-lookup"><span data-stu-id="92e54-164">Before proceeding to create a policy definition, look at the built-in policies.</span></span> <span data-ttu-id="92e54-165">Si encuentra una directiva integrada que se aplica a los límites que necesita, puede omitir la creación de una definición de directiva.</span><span class="sxs-lookup"><span data-stu-id="92e54-165">If you find a built-in policy that applies the limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="92e54-166">En su lugar, asigne la directiva integrada al ámbito deseado.</span><span class="sxs-lookup"><span data-stu-id="92e54-166">Instead, assign the built-in policy to the desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="92e54-167">Creación de definición de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-167">Create policy definition</span></span>

<span data-ttu-id="92e54-168">Puede crear una definición de directiva mediante la CLI de Azure con el comando de definición de directiva.</span><span class="sxs-lookup"><span data-stu-id="92e54-168">You can create a policy definition using Azure CLI with the policy definition command.</span></span>

```azurecli
az policy definition create --name coolAccessTier --description "Policy to specify access tier." --rules '{
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

### <a name="assign-policy"></a><span data-ttu-id="92e54-169">Asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-169">Assign policy</span></span>

<span data-ttu-id="92e54-170">Puede aplicar la directiva en el ámbito que quiera mediante el comando de asignación de directiva.</span><span class="sxs-lookup"><span data-stu-id="92e54-170">You can apply the policy to the desired scope by using the policy assignment command.</span></span> <span data-ttu-id="92e54-171">En el ejemplo siguiente se asigna la directiva a un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="92e54-171">The following example assigns a policy to a resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="92e54-172">Visualización de la asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-172">View policy assignment</span></span>

<span data-ttu-id="92e54-173">Para ver una asignación de directiva, proporcione el nombre de la asignación de directiva y el ámbito:</span><span class="sxs-lookup"><span data-stu-id="92e54-173">To view a policy assignment, provide the policy assignment name and the scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="92e54-174">Eliminación de la asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="92e54-174">Remove policy assignment</span></span> 

<span data-ttu-id="92e54-175">Para quitar una asignación de directiva, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="92e54-175">To remove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="92e54-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="92e54-176">Next steps</span></span>
* <span data-ttu-id="92e54-177">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="92e54-177">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

