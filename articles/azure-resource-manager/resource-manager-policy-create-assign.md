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
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="f6a12-103">Asignación y administración de directivas de recursos</span><span class="sxs-lookup"><span data-stu-id="f6a12-103">Assign and manage resource policies</span></span>

<span data-ttu-id="f6a12-104">tooimplement una directiva, debe realizar estos pasos:</span><span class="sxs-lookup"><span data-stu-id="f6a12-104">tooimplement a policy, you must perform these steps:</span></span>

1. <span data-ttu-id="f6a12-105">Comprobar directiva definiciones (incluidas las directivas integradas proporcionadas por Azure) toosee si ya existe uno en la suscripción que cumple los requisitos.</span><span class="sxs-lookup"><span data-stu-id="f6a12-105">Check policy definitions (including built-in policies provided by Azure) toosee if one already exists in your subscription that fulfills your requirements.</span></span>
2. <span data-ttu-id="f6a12-106">Si existe una, obtenga el nombre.</span><span class="sxs-lookup"><span data-stu-id="f6a12-106">If one exists, get its name.</span></span>
3. <span data-ttu-id="f6a12-107">Si no existe, definir la regla de directiva de hello con JSON y agréguela como una definición de directiva en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="f6a12-107">If one does not exist, define hello policy rule with JSON, and add it as a policy definition in your subscription.</span></span> <span data-ttu-id="f6a12-108">Este paso pone a disposición para la asignación de directiva de hello pero no aplica tooyour suscripción de hello reglas.</span><span class="sxs-lookup"><span data-stu-id="f6a12-108">This step makes hello policy available for assignment but does not apply hello rules tooyour subscription.</span></span>
4. <span data-ttu-id="f6a12-109">Para cualquiera de los casos, asignar al ámbito de hello directiva tooa (por ejemplo, un suscripción o grupo de recursos).</span><span class="sxs-lookup"><span data-stu-id="f6a12-109">For either case, assign hello policy tooa scope (such as a subscription or resource group).</span></span> <span data-ttu-id="f6a12-110">Ahora se aplican reglas de Hola de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6a12-110">hello rules of hello policy are now enforced.</span></span>

<span data-ttu-id="f6a12-111">En este artículo se centra en hello pasos toocreate una definición de directiva y asignar ese ámbito de tooa definición a través de la API de REST, PowerShell o CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6a12-111">This article focuses on hello steps toocreate a policy definition and assign that definition tooa scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="f6a12-112">Si prefiere que las directivas de toouse hello tooassign portal, consulte [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f6a12-112">If you prefer toouse hello portal tooassign policies, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="f6a12-113">En este artículo no se centra en la sintaxis de Hola para crear la definición de la directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6a12-113">This article does not focus on hello syntax for creating hello policy definition.</span></span> <span data-ttu-id="f6a12-114">Para información sobre la sintaxis de directivas, consulte [Uso de directivas para administrar los recursos y controlar el acceso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="f6a12-114">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="f6a12-115">API de REST</span><span class="sxs-lookup"><span data-stu-id="f6a12-115">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="f6a12-116">Creación de definición de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-116">Create policy definition</span></span>

<span data-ttu-id="f6a12-117">Puede crear una directiva con hello [API de REST para las definiciones de directiva](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="f6a12-117">You can create a policy with hello [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="f6a12-118">API de REST de Hello permite toocreate y eliminar definiciones de directiva y obtener información acerca de las definiciones existentes.</span><span class="sxs-lookup"><span data-stu-id="f6a12-118">hello REST API enables you toocreate and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="f6a12-119">toocreate una definición de directiva, ejecute:</span><span class="sxs-lookup"><span data-stu-id="f6a12-119">toocreate a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="f6a12-120">Incluir un toohello similar de cuerpo de solicitud siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f6a12-120">Include a request body similar toohello following example:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="f6a12-121">Asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-121">Assign policy</span></span>

<span data-ttu-id="f6a12-122">Puede aplicar la definición de la directiva de hello en el ámbito de hello deseado a través de hello [API de REST para las asignaciones de directivas](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="f6a12-122">You can apply hello policy definition at hello desired scope through hello [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="f6a12-123">Hola REST API permite toocreate y eliminar las asignaciones de directivas y obtener información acerca de las asignaciones existentes.</span><span class="sxs-lookup"><span data-stu-id="f6a12-123">hello REST API enables you toocreate and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="f6a12-124">toocreate una asignación de directiva, ejecute:</span><span class="sxs-lookup"><span data-stu-id="f6a12-124">toocreate a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="f6a12-125">Hello {asignación de directiva} es el nombre del saludo de asignación de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6a12-125">hello {policy-assignment} is hello name of hello policy assignment.</span></span>

<span data-ttu-id="f6a12-126">Incluir un toohello similar de cuerpo de solicitud siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f6a12-126">Include a request body similar toohello following example:</span></span>

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

### <a name="view-policy"></a><span data-ttu-id="f6a12-127">Visualización de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-127">View policy</span></span>
<span data-ttu-id="f6a12-128">tooget una directiva, utilice hello [obtener la definición de directiva](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operación.</span><span class="sxs-lookup"><span data-stu-id="f6a12-128">tooget a policy, use hello [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="f6a12-129">Obtención de alias</span><span class="sxs-lookup"><span data-stu-id="f6a12-129">Get aliases</span></span>
<span data-ttu-id="f6a12-130">Puede recuperar alias a través de hello API de REST:</span><span class="sxs-lookup"><span data-stu-id="f6a12-130">You can retrieve aliases through hello REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="f6a12-131">Hola de ejemplo siguiente muestra una definición de un alias.</span><span class="sxs-lookup"><span data-stu-id="f6a12-131">hello following example shows a definition of an alias.</span></span> <span data-ttu-id="f6a12-132">Como puede ver, un alias define rutas de acceso en distintas versiones de API, aunque se cambie el nombre de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="f6a12-132">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

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

## <a name="powershell"></a><span data-ttu-id="f6a12-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6a12-133">PowerShell</span></span>

<span data-ttu-id="f6a12-134">Antes de continuar con los ejemplos de PowerShell de hello, asegúrese de que tiene [instalada la versión más reciente de hello](/powershell/azure/install-azurerm-ps) de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6a12-134">Before proceeding with hello PowerShell examples, make sure you have [installed hello latest version](/powershell/azure/install-azurerm-ps) of Azure PowerShell.</span></span> <span data-ttu-id="f6a12-135">Se agregaron parámetros de directiva en la versión 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="f6a12-135">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="f6a12-136">Si tiene una versión anterior, los ejemplos de hello obtienen que un parámetro hello de error que indica que no se encuentra.</span><span class="sxs-lookup"><span data-stu-id="f6a12-136">If you have an earlier version, hello examples return an error indicating hello parameter cannot be found.</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="f6a12-137">Visualización de definiciones de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-137">View policy definitions</span></span>
<span data-ttu-id="f6a12-138">toosee de comandos de todas las definiciones de directiva en su suscripción, Hola de uso siguientes:</span><span class="sxs-lookup"><span data-stu-id="f6a12-138">toosee all policy definitions in your subscription, use hello following command:</span></span>

```powershell
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="f6a12-139">Devuelve todas las definiciones de directiva disponibles, incluidas las directivas integradas.</span><span class="sxs-lookup"><span data-stu-id="f6a12-139">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="f6a12-140">Cada directiva se devuelve en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="f6a12-140">Each policy is returned in hello following format:</span></span>

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

<span data-ttu-id="f6a12-141">Antes de continuar toocreate una definición de directiva, mire directivas integradas Hola.</span><span class="sxs-lookup"><span data-stu-id="f6a12-141">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="f6a12-142">Si encuentra una directiva integrada que aplica límites de Hola que necesita, puede omitir la creación de una definición de directiva.</span><span class="sxs-lookup"><span data-stu-id="f6a12-142">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="f6a12-143">En su lugar, asignar al ámbito de toohello deseado de hello directiva integrada.</span><span class="sxs-lookup"><span data-stu-id="f6a12-143">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="f6a12-144">Creación de definición de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-144">Create policy definition</span></span>
<span data-ttu-id="f6a12-145">Puede crear una definición de directiva mediante hello `New-AzureRmPolicyDefinition` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f6a12-145">You can create a policy definition using hello `New-AzureRmPolicyDefinition` cmdlet.</span></span>

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

<span data-ttu-id="f6a12-146">Hola resultado se almacena en un `$definition` objeto, que se usa durante la asignación de directiva.</span><span class="sxs-lookup"><span data-stu-id="f6a12-146">hello output is stored in a `$definition` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="f6a12-147">En vez de especificar Hola JSON como un parámetro, puede proporcionar Hola ruta tooa .json archivo que contiene la regla de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6a12-147">Rather than specifying hello JSON as a parameter, you can provide hello path tooa .json file containing hello policy rule.</span></span>

```powershell
$definition = New-AzureRmPolicyDefinition -Name coolAccessTier -Description "Policy toospecify access tier." -Policy "c:\policies\coolAccessTier.json"
```

<span data-ttu-id="f6a12-148">Hello en el ejemplo siguiente se crea una definición de directiva que incluya parámetros:</span><span class="sxs-lookup"><span data-stu-id="f6a12-148">hello following example creates a policy definition that includes parameters:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="f6a12-149">Asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-149">Assign policy</span></span>

<span data-ttu-id="f6a12-150">Aplicar directiva de hello en el ámbito de hello deseado mediante hello `New-AzureRmPolicyAssignment` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f6a12-150">You apply hello policy at hello desired scope by using hello `New-AzureRmPolicyAssignment` cmdlet.</span></span> <span data-ttu-id="f6a12-151">Hola siguiente ejemplo asigna a grupo de recursos de hello directiva tooa.</span><span class="sxs-lookup"><span data-stu-id="f6a12-151">hello following example assigns hello policy tooa resource group.</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
New-AzureRMPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="f6a12-152">tooassign una directiva que requiere parámetros, cree y de objeto con esos valores.</span><span class="sxs-lookup"><span data-stu-id="f6a12-152">tooassign a policy that requires parameters, create and object with those values.</span></span> <span data-ttu-id="f6a12-153">Hello en el ejemplo siguiente se recupera una directiva integrada y pasa los valores de parámetros:</span><span class="sxs-lookup"><span data-stu-id="f6a12-153">hello following example retrieves a built-in policy and passes in parameters values:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$definition = Get-AzureRmPolicyDefinition -Id /providers/Microsoft.Authorization/policyDefinitions/e5662a6-4747-49cd-b67b-bf8b01975c4c
$array = @("West US", "West US 2")
$param = @{"listOfAllowedLocations"=$array}
New-AzureRMPolicyAssignment -Name locationAssignment -Scope $rg.ResourceId -PolicyDefinition $definition -PolicyParameterObject $param
```

### <a name="view-policy-assignment"></a><span data-ttu-id="f6a12-154">Visualización de la asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-154">View policy assignment</span></span>

<span data-ttu-id="f6a12-155">tooget una asignación de directiva específica, use:</span><span class="sxs-lookup"><span data-stu-id="f6a12-155">tooget a specific policy assignment, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name accessTierAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="f6a12-156">regla de directiva de hello tooview para una definición de directiva, use:</span><span class="sxs-lookup"><span data-stu-id="f6a12-156">tooview hello policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name coolAccessTier).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="f6a12-157">Eliminación de la asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-157">Remove policy assignment</span></span> 

<span data-ttu-id="f6a12-158">tooremove una asignación de directiva, use:</span><span class="sxs-lookup"><span data-stu-id="f6a12-158">tooremove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli"></a><span data-ttu-id="f6a12-159">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f6a12-159">Azure CLI</span></span>

### <a name="view-policy-definitions"></a><span data-ttu-id="f6a12-160">Visualización de definiciones de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-160">View policy definitions</span></span>
<span data-ttu-id="f6a12-161">toosee de comandos de todas las definiciones de directiva en su suscripción, Hola de uso siguientes:</span><span class="sxs-lookup"><span data-stu-id="f6a12-161">toosee all policy definitions in your subscription, use hello following command:</span></span>

```azurecli
az policy definition list
```

<span data-ttu-id="f6a12-162">Devuelve todas las definiciones de directiva disponibles, incluidas las directivas integradas.</span><span class="sxs-lookup"><span data-stu-id="f6a12-162">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="f6a12-163">Cada directiva se devuelve en hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="f6a12-163">Each policy is returned in hello following format:</span></span>

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

<span data-ttu-id="f6a12-164">Antes de continuar toocreate una definición de directiva, mire directivas integradas Hola.</span><span class="sxs-lookup"><span data-stu-id="f6a12-164">Before proceeding toocreate a policy definition, look at hello built-in policies.</span></span> <span data-ttu-id="f6a12-165">Si encuentra una directiva integrada que aplica límites de Hola que necesita, puede omitir la creación de una definición de directiva.</span><span class="sxs-lookup"><span data-stu-id="f6a12-165">If you find a built-in policy that applies hello limits you need, you can skip creating a policy definition.</span></span> <span data-ttu-id="f6a12-166">En su lugar, asignar al ámbito de toohello deseado de hello directiva integrada.</span><span class="sxs-lookup"><span data-stu-id="f6a12-166">Instead, assign hello built-in policy toohello desired scope.</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="f6a12-167">Creación de definición de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-167">Create policy definition</span></span>

<span data-ttu-id="f6a12-168">Puede crear una definición de directiva mediante la CLI de Azure con el comando de definición de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6a12-168">You can create a policy definition using Azure CLI with hello policy definition command.</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="f6a12-169">Asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-169">Assign policy</span></span>

<span data-ttu-id="f6a12-170">Puede aplicar ámbito de hello directiva toohello deseado mediante el uso de comandos de asignación de directiva de Hola.</span><span class="sxs-lookup"><span data-stu-id="f6a12-170">You can apply hello policy toohello desired scope by using hello policy assignment command.</span></span> <span data-ttu-id="f6a12-171">Hola de ejemplo siguiente asigna a un grupo de recursos de tooa de directiva.</span><span class="sxs-lookup"><span data-stu-id="f6a12-171">hello following example assigns a policy tooa resource group.</span></span>

```azurecli
az policy assignment create --name coolAccessTierAssignment --policy coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-assignment"></a><span data-ttu-id="f6a12-172">Visualización de la asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-172">View policy assignment</span></span>

<span data-ttu-id="f6a12-173">tooview una asignación de directiva, proporcione el nombre de asignación de directiva de Hola y el ámbito de hello:</span><span class="sxs-lookup"><span data-stu-id="f6a12-173">tooview a policy assignment, provide hello policy assignment name and hello scope:</span></span>

```azurecli
az policy assignment show --name coolAccessTierAssignment --scope "/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}"
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="f6a12-174">Eliminación de la asignación de directiva</span><span class="sxs-lookup"><span data-stu-id="f6a12-174">Remove policy assignment</span></span> 

<span data-ttu-id="f6a12-175">tooremove una asignación de directiva, use:</span><span class="sxs-lookup"><span data-stu-id="f6a12-175">tooremove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name coolAccessTier --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="f6a12-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6a12-176">Next steps</span></span>
* <span data-ttu-id="f6a12-177">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f6a12-177">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

