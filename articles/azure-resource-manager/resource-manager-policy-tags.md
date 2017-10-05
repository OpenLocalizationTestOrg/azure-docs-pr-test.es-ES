---
title: Directivas de recursos de Azure para etiquetas | Microsoft Docs
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
ms.openlocfilehash: 469bd8d637337e5900ea84c6bfaf88064695fb7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="apply-resource-policies-for-tags"></a><span data-ttu-id="562e9-103">Aplicación de directivas de recursos para etiquetas</span><span class="sxs-lookup"><span data-stu-id="562e9-103">Apply resource policies for tags</span></span>

<span data-ttu-id="562e9-104">Este tema proporciona reglas de directiva comunes que se pueden aplicar para garantizar un uso coherente de las etiquetas en recursos.</span><span class="sxs-lookup"><span data-stu-id="562e9-104">This topic provides common policy rules you can apply to ensure consistent use of tags on resources.</span></span>

<span data-ttu-id="562e9-105">La aplicación de una directiva de etiqueta a un grupo de recursos o a una suscripción con recursos existentes no aplica con carácter retroactivo la directiva a esos recursos.</span><span class="sxs-lookup"><span data-stu-id="562e9-105">Applying a tag policy to a resource group or subscription with existing resources does not retroactively apply the policy to those resources.</span></span> <span data-ttu-id="562e9-106">Para aplicar las directivas en esos recursos, desencadene una actualización en los recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="562e9-106">To enforce the policies on those resources, trigger an update to the existing resources.</span></span> <span data-ttu-id="562e9-107">En este artículo se incluye un ejemplo de PowerShell para desencadenar una actualización.</span><span class="sxs-lookup"><span data-stu-id="562e9-107">This article includes a PowerShell example for triggering an update.</span></span>

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a><span data-ttu-id="562e9-108">Garantizar que todos los recursos de un grupo de recursos tienen una etiqueta y un valor</span><span class="sxs-lookup"><span data-stu-id="562e9-108">Ensure all resources in a resource group have a tag/value</span></span>

<span data-ttu-id="562e9-109">Un requisito común es que todos los recursos de un grupo de recursos tengan una etiqueta y un valor determinados.</span><span class="sxs-lookup"><span data-stu-id="562e9-109">A common requirement is that all resources in a resource group have a particular tag and value.</span></span> <span data-ttu-id="562e9-110">Este requisito a menudo es necesario para realizar un seguimiento de los costos por departamento.</span><span class="sxs-lookup"><span data-stu-id="562e9-110">This requirement is often needed to track costs by department.</span></span> <span data-ttu-id="562e9-111">Se deben cumplir las condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="562e9-111">The following conditions must be met:</span></span>

* <span data-ttu-id="562e9-112">La etiqueta y el valor obligatorios se anexan a los recursos nuevos y actualizados que no tienen la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="562e9-112">The required tag and value are appended to new and updated resources that do not have the tag.</span></span>
* <span data-ttu-id="562e9-113">La etiqueta y el valor necesarios no se pueden quitar de los recursos existentes.</span><span class="sxs-lookup"><span data-stu-id="562e9-113">The required tag and value cannot be removed from any existing resources.</span></span>

<span data-ttu-id="562e9-114">Este requisito se cumple aplicando dos directivas integradas a un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="562e9-114">You accomplish this requirement by applying two built-in policies to a resource group.</span></span>

| <span data-ttu-id="562e9-115">ID</span><span class="sxs-lookup"><span data-stu-id="562e9-115">ID</span></span> | <span data-ttu-id="562e9-116">Descripción</span><span class="sxs-lookup"><span data-stu-id="562e9-116">Description</span></span> |
| ---- | ---- |
| <span data-ttu-id="562e9-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span><span class="sxs-lookup"><span data-stu-id="562e9-117">2a0e14a6-b0a6-4fab-991a-187a4f81c498</span></span> | <span data-ttu-id="562e9-118">Aplica una etiqueta obligatoria y su valor predeterminado cuando el usuario no la especifica.</span><span class="sxs-lookup"><span data-stu-id="562e9-118">Applies a required tag and its default value when it is not specified by the user.</span></span> |
| <span data-ttu-id="562e9-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span><span class="sxs-lookup"><span data-stu-id="562e9-119">1e30110a-5ceb-460c-a204-c1c3969c6d62</span></span> | <span data-ttu-id="562e9-120">Aplica una etiqueta obligatoria y su valor.</span><span class="sxs-lookup"><span data-stu-id="562e9-120">Enforces a required tag and its value.</span></span> |

### <a name="powershell"></a><span data-ttu-id="562e9-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="562e9-121">PowerShell</span></span>

<span data-ttu-id="562e9-122">En el siguiente script de PowerShell, se asignan las dos definiciones de directivas integradas a un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="562e9-122">The following PowerShell script assigns the two built-in policy definitions to a resource group.</span></span> <span data-ttu-id="562e9-123">Antes de ejecutar el script, asigne todas las etiquetas obligatorias al grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="562e9-123">Before running the script, assign all required tags to the resource group.</span></span> <span data-ttu-id="562e9-124">Se necesita cada etiqueta en el grupo de recursos para los recursos del grupo.</span><span class="sxs-lookup"><span data-stu-id="562e9-124">Each tag on the resource group is required for the resources in the group.</span></span> <span data-ttu-id="562e9-125">Para asignarlas a todos los grupos de recursos en su suscripción, no proporcione el parámetro `-Name` cuando obtenga los grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="562e9-125">To assign to all resource groups in your subscription, do not provide the `-Name` parameter when getting the resource groups.</span></span>

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

<span data-ttu-id="562e9-126">Después de asignar las directivas, puede desencadenar una actualización a todos los recursos existentes para aplicar las directivas de etiqueta que ha agregado.</span><span class="sxs-lookup"><span data-stu-id="562e9-126">After assigning the policies, you can trigger an update to all existing resources to enforce the tag policies you have added.</span></span> <span data-ttu-id="562e9-127">En el siguiente script se conservan las demás etiquetas que existían en los recursos:</span><span class="sxs-lookup"><span data-stu-id="562e9-127">The following script retains any other tags that existed on the resources:</span></span>

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

## <a name="require-tags-for-a-resource-type"></a><span data-ttu-id="562e9-128">Requerir etiquetas para un tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="562e9-128">Require tags for a resource type</span></span>
<span data-ttu-id="562e9-129">En el ejemplo siguiente se muestra cómo anidar operadores lógicos para requerir una etiqueta de aplicación solo para un tipo de recurso especificado (en este caso, cuentas de almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="562e9-129">The following example shows how to nest logical operators to require an application tag for only a specified resource type (in this case, storage accounts).</span></span>

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

## <a name="require-tag"></a><span data-ttu-id="562e9-130">Requerir etiqueta</span><span class="sxs-lookup"><span data-stu-id="562e9-130">Require tag</span></span>
<span data-ttu-id="562e9-131">La siguiente directiva deniega todas las solicitudes que no tienen una etiqueta que contenga la clave "costCenter" (se puede aplicar cualquier valor):</span><span class="sxs-lookup"><span data-stu-id="562e9-131">The following policy denies requests that don't have a tag containing "costCenter" key (any value can be applied):</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="562e9-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="562e9-132">Next steps</span></span>
* <span data-ttu-id="562e9-133">Después de definir una regla de directiva (como se muestra en los ejemplos anteriores), debe crear la definición de directiva y asignarla a un ámbito.</span><span class="sxs-lookup"><span data-stu-id="562e9-133">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="562e9-134">El ámbito puede ser una suscripción, un grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="562e9-134">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="562e9-135">Para asignar directivas a través del portal, consulte [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Uso de Azure Portal para asignar y administrar directivas de recursos).</span><span class="sxs-lookup"><span data-stu-id="562e9-135">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="562e9-136">Para asignar directivas a través de la API de REST, PowerShell o la CLI de Azure, consulte [Assign and manage policies through script](resource-manager-policy-create-assign.md) (Asignación y administración de directivas a través de scripts).</span><span class="sxs-lookup"><span data-stu-id="562e9-136">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="562e9-137">Para obtener una introducción a las directivas de recursos, consulte [Uso de directivas para administrar los recursos y controlar el acceso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="562e9-137">For an introduction to resource policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="562e9-138">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="562e9-138">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

