---
title: las directivas de recursos de aaaAzure para etiquetas | Documentos de Microsoft
description: Proporciona ejemplos de directivas de recursos para administrar etiquetas en recursos
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
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="9b7d0-103">Aplicación de directivas de recursos para etiquetas</span><span class="sxs-lookup"><span data-stu-id="9b7d0-103">Apply resource policies for tags</span></span>

<span data-ttu-id="9b7d0-104">Este tema proporciona reglas de directiva común que se puede aplicar tooensure un uso coherente de etiquetas de recursos.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-104">This topic provides common policy rules you can apply tooensure consistent use of tags on resources.</span></span>

<span data-ttu-id="9b7d0-105">Aplicar un grupo de recursos de tooa de directiva de etiqueta o suscripción con los recursos existentes, recursos de hello directiva toothose no aplica con carácter retroactivo.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-105">Applying a tag policy tooa resource group or subscription with existing resources does not retroactively apply hello policy toothose resources.</span></span> <span data-ttu-id="9b7d0-106">directivas de Hola de tooenforce en esos recursos, desencadenar una toohello de actualización de recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-106">tooenforce hello policies on those resources, trigger an update toohello existing resources.</span></span> <span data-ttu-id="9b7d0-107">En este artículo se incluye un ejemplo de PowerShell para desencadenar una actualización.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="9b7d0-108">Garantizar que todos los recursos de un grupo de recursos tienen una etiqueta y un valor</span><span class="sxs-lookup"><span data-stu-id="9b7d0-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="9b7d0-109">Un requisito común es que todos los recursos de un grupo de recursos tengan una etiqueta y un valor determinados.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="9b7d0-110">Este requisito suele ser necesario tootrack costos por departamento.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-110">This requirement is often needed tootrack costs by department.</span></span> <span data-ttu-id="9b7d0-111">debe cumplirse Hola condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="9b7d0-111">hello following conditions must be met:</span></span>

* <span data-ttu-id="9b7d0-112">Hola requiere la etiqueta y el valor se toonew anexado y actualizan los recursos que no tienen etiqueta Hola.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-112">hello required tag and value are appended toonew and updated resources that do not have hello tag.</span></span>
* <span data-ttu-id="9b7d0-113">la etiqueta requerida de Hello y no se puede quitar el valor de los recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-113">hello required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="9b7d0-114">Este requisito se consigue mediante la aplicación de grupo de recursos de tooa de dos directivas integradas.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-114">You accomplish this requirement by applying two built-in policies tooa resource group.</span></span>

| <span data-ttu-id="9b7d0-115">ID</span><span class="sxs-lookup"><span data-stu-id="9b7d0-115">ID</span></span> | <span data-ttu-id="9b7d0-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="9b7d0-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="9b7d0-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="9b7d0-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="9b7d0-118">Se aplica una etiqueta obligatoria y su valor predeterminado cuando no se especifica por el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-118">Applies a required tag and its default value when it is not specified by hello user.</span></span> |
| <span data-ttu-id="9b7d0-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="9b7d0-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="9b7d0-120">Aplica una etiqueta obligatoria y su valor.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="9b7d0-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b7d0-121">PowerShell</span></span>

<span data-ttu-id="9b7d0-122">Hola siguiente script de PowerShell asigna el grupo de recursos de hello directiva integrada dos definiciones tooa.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-122">hello following PowerShell script assigns hello two built-in policy definitions tooa resource group.</span></span> <span data-ttu-id="9b7d0-123">Antes de ejecutar script de Hola, asigne el grupo de recursos de todas las etiquetas necesarias toohello.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-123">Before running hello script, assign all required tags toohello resource group.</span></span> <span data-ttu-id="9b7d0-124">Cada etiqueta del grupo de recursos de hello es necesaria para recursos de hello en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-124">Each tag on hello resource group is required for hello resources in hello group.</span></span> <span data-ttu-id="9b7d0-125">grupos de recursos de tooassign tooall en su suscripción, no proporcionan hello `-Name` parámetro al obtener grupos de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-125">tooassign tooall resource groups in your subscription, do not provide hello `-Name` parameter when getting hello resource groups.</span></span>

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

<span data-ttu-id="9b7d0-126">Después de la asignación de directivas de hello, puede desencadenar una tooall de actualización existente recursos tooenforce Hola etiqueta las directivas que haya agregado.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-126">After assigning hello policies, you can trigger an update tooall existing resources tooenforce hello tag policies you have added.</span></span> <span data-ttu-id="9b7d0-127">Hello secuencia de comandos siguiente conserva cualquier otra etiqueta que existían en los recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="9b7d0-127">hello following script retains any other tags that existed on hello resources:</span></span>

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="9b7d0-128">Requerir etiquetas para un tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="9b7d0-128">Require tags for a resource type</span></span>
<span data-ttu-id="9b7d0-129">Hola de ejemplo siguiente muestra cómo etiquetar toonest operadores lógicos toorequire una aplicación para un tipo de recurso especificado (en este caso, las cuentas de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="9b7d0-129">hello following example shows how toonest logical operators toorequire an application tag for only a specified resource type (in this case, storage accounts).</span></span>

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a><span data-ttu-id="9b7d0-130">Requerir etiqueta</span><span class="sxs-lookup"><span data-stu-id="9b7d0-130">Require tag</span></span>
<span data-ttu-id="9b7d0-131">Hello directiva siguiente deniega las solicitudes que no tienen una etiqueta que contiene la clave "costCenter" (cualquier valor puede aplicarse):</span><span class="sxs-lookup"><span data-stu-id="9b7d0-131">hello following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="9b7d0-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b7d0-132">Next steps</span></span>
* <span data-ttu-id="9b7d0-133">Después de definir una regla de directiva (como se muestra en hello anteriores ejemplos), se necesita la definición de la directiva de toocreate hello y se asigna tooa ámbito.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-133">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="9b7d0-134">Hola ámbito puede ser una suscripción, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="9b7d0-134">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="9b7d0-135">directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9b7d0-135">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="9b7d0-136">directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="9b7d0-136">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="9b7d0-137">Una directivas tooresource de introducción, consulte [información general de directivas de recursos](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9b7d0-137">For an introduction tooresource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="9b7d0-138">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="9b7d0-138">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

