---
title: las directivas de recursos de aaaAzure para las convenciones de nomenclatura | Documentos de Microsoft
description: Describe las directivas de Azure Resource Manager para convenciones de nomenclatura de recursos.
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="34df8-103">Aplicación de directivas de recursos para nombres y texto</span><span class="sxs-lookup"><span data-stu-id="34df8-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="34df8-104">En este tema se muestra varios [las directivas de recursos](resource-manager-policy.md) puede aplicar las convenciones de nomenclatura y texto de tooestablish.</span><span class="sxs-lookup"><span data-stu-id="34df8-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply tooestablish naming and text conventions.</span></span> <span data-ttu-id="34df8-105">Estas directivas garantizan la coherencia para valores de etiquetas y nombres de recursos.</span><span class="sxs-lookup"><span data-stu-id="34df8-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="34df8-106">Establecimiento de la convención de nomenclatura con caracteres comodín</span><span class="sxs-lookup"><span data-stu-id="34df8-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="34df8-107">Hello en el ejemplo siguiente se muestra uso de Hola de carácter comodín, que es compatible con hello **como** condición.</span><span class="sxs-lookup"><span data-stu-id="34df8-107">hello following example shows hello use of wildcard, which is supported by hello **like** condition.</span></span> <span data-ttu-id="34df8-108">Hello condición indica que si hello nombre coincide con patrón mencionados hello (namePrefix\*nameSuffix), a continuación, denegar la solicitud de hello:</span><span class="sxs-lookup"><span data-stu-id="34df8-108">hello condition states that if hello name does match hello mentioned pattern (namePrefix\*nameSuffix) then deny hello request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="34df8-109">Establecimiento de la convención de nomenclatura con patrones</span><span class="sxs-lookup"><span data-stu-id="34df8-109">Set naming convention with pattern</span></span>

<span data-ttu-id="34df8-110">toospecify que los nombres de recursos coinciden con un patrón, use Hola coincide con la condición.</span><span class="sxs-lookup"><span data-stu-id="34df8-110">toospecify that resource names match a pattern, use hello match condition.</span></span> <span data-ttu-id="34df8-111">en el ejemplo siguiente se Hello requiere nombres toostart con `contoso` y contener seis letras adicionales:</span><span class="sxs-lookup"><span data-stu-id="34df8-111">hello following example requires names toostart with `contoso` and contain six additional letters:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="34df8-112">Establecimiento del patrón de fecha para el valor de etiqueta</span><span class="sxs-lookup"><span data-stu-id="34df8-112">Set date pattern for tag value</span></span>

<span data-ttu-id="34df8-113">toorequire un patrón de fecha de dos dígitos, guión, tres letras, guión y cuatro dígitos, use:</span><span class="sxs-lookup"><span data-stu-id="34df8-113">toorequire a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="34df8-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34df8-114">Next steps</span></span>
* <span data-ttu-id="34df8-115">Después de definir una regla de directiva (como se muestra en hello anteriores ejemplos), se necesita la definición de la directiva de toocreate hello y se asigna tooa ámbito.</span><span class="sxs-lookup"><span data-stu-id="34df8-115">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="34df8-116">Hola ámbito puede ser una suscripción, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="34df8-116">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="34df8-117">directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34df8-117">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="34df8-118">directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="34df8-118">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="34df8-119">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="34df8-119">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

