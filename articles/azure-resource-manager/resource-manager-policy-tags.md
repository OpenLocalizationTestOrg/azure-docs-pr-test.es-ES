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
# <a name="apply-resource-policies-for-tags"></a>Aplicación de directivas de recursos para etiquetas

Este tema proporciona reglas de directiva común que se puede aplicar tooensure un uso coherente de etiquetas de recursos.

Aplicar un grupo de recursos de tooa de directiva de etiqueta o suscripción con los recursos existentes, recursos de hello directiva toothose no aplica con carácter retroactivo. directivas de Hola de tooenforce en esos recursos, desencadenar una toohello de actualización de recursos existentes. En este artículo se incluye un ejemplo de PowerShell para desencadenar una actualización.

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>Garantizar que todos los recursos de un grupo de recursos tienen una etiqueta y un valor

Un requisito común es que todos los recursos de un grupo de recursos tengan una etiqueta y un valor determinados. Este requisito suele ser necesario tootrack costos por departamento. debe cumplirse Hola condiciones siguientes:

* Hola requiere la etiqueta y el valor se toonew anexado y actualizan los recursos que no tienen etiqueta Hola.
* la etiqueta requerida de Hello y no se puede quitar el valor de los recursos existentes.

Este requisito se consigue mediante la aplicación de grupo de recursos de tooa de dos directivas integradas.

| ID | Descripción |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Se aplica una etiqueta obligatoria y su valor predeterminado cuando no se especifica por el usuario de Hola. |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | Aplica una etiqueta obligatoria y su valor. |

### <a name="powershell"></a>PowerShell

Hola siguiente script de PowerShell asigna el grupo de recursos de hello directiva integrada dos definiciones tooa. Antes de ejecutar script de Hola, asigne el grupo de recursos de todas las etiquetas necesarias toohello. Cada etiqueta del grupo de recursos de hello es necesaria para recursos de hello en el grupo de Hola. grupos de recursos de tooassign tooall en su suscripción, no proporcionan hello `-Name` parámetro al obtener grupos de recursos de Hola.

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

Después de la asignación de directivas de hello, puede desencadenar una tooall de actualización existente recursos tooenforce Hola etiqueta las directivas que haya agregado. Hello secuencia de comandos siguiente conserva cualquier otra etiqueta que existían en los recursos de hello:

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

## <a name="require-tags-for-a-resource-type"></a>Requerir etiquetas para un tipo de recurso
Hola de ejemplo siguiente muestra cómo etiquetar toonest operadores lógicos toorequire una aplicación para un tipo de recurso especificado (en este caso, las cuentas de almacenamiento).

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

## <a name="require-tag"></a>Requerir etiqueta
Hello directiva siguiente deniega las solicitudes que no tienen una etiqueta que contiene la clave "costCenter" (cualquier valor puede aplicarse):

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

## <a name="next-steps"></a>Pasos siguientes
* Después de definir una regla de directiva (como se muestra en hello anteriores ejemplos), se necesita la definición de la directiva de toocreate hello y se asigna tooa ámbito. Hola ámbito puede ser una suscripción, el grupo de recursos o el recurso. directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md). directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md).
* Una directivas tooresource de introducción, consulte [información general de directivas de recursos](resource-manager-policy.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

