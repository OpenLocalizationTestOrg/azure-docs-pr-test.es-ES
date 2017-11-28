---
title: Directivas de recursos de Azure para la nomenclatura de convenciones | Microsoft Docs
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
ms.openlocfilehash: 51b3519bbba8cb4c768bfdd7dadf92fced434f22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a><span data-ttu-id="23a6b-103">Aplicación de directivas de recursos para nombres y texto</span><span class="sxs-lookup"><span data-stu-id="23a6b-103">Apply resource policies for names and text</span></span>
<span data-ttu-id="23a6b-104">Este tema muestra varias [directivas de recurso](resource-manager-policy.md) que puede aplicar para establecer las convenciones de texto y nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="23a6b-104">This topic shows several [resource policies](resource-manager-policy.md) you can apply to establish naming and text conventions.</span></span> <span data-ttu-id="23a6b-105">Estas directivas garantizan la coherencia para valores de etiquetas y nombres de recursos.</span><span class="sxs-lookup"><span data-stu-id="23a6b-105">These policies ensure consistency for resource names and tag values.</span></span> 

## <a name="set-naming-convention-with-wildcard"></a><span data-ttu-id="23a6b-106">Establecimiento de la convención de nomenclatura con caracteres comodín</span><span class="sxs-lookup"><span data-stu-id="23a6b-106">Set naming convention with wildcard</span></span>
<span data-ttu-id="23a6b-107">En el ejemplo siguiente se muestra el uso de caracteres comodín que admite la condición **like**.</span><span class="sxs-lookup"><span data-stu-id="23a6b-107">The following example shows the use of wildcard, which is supported by the **like** condition.</span></span> <span data-ttu-id="23a6b-108">La condición indica que se denegará la solicitud si el nombre coincide con el patrón indicado (namePrefix\*nameSuffix):</span><span class="sxs-lookup"><span data-stu-id="23a6b-108">The condition states that if the name does match the mentioned pattern (namePrefix\*nameSuffix) then deny the request:</span></span>

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

## <a name="set-naming-convention-with-pattern"></a><span data-ttu-id="23a6b-109">Establecimiento de la convención de nomenclatura con patrones</span><span class="sxs-lookup"><span data-stu-id="23a6b-109">Set naming convention with pattern</span></span>

<span data-ttu-id="23a6b-110">Para especificar que los nombres de recursos coincidan con un patrón, use la condición match.</span><span class="sxs-lookup"><span data-stu-id="23a6b-110">To specify that resource names match a pattern, use the match condition.</span></span> <span data-ttu-id="23a6b-111">El ejemplo siguiente requiere que los nombres empiecen por `contoso` y contengan seis letras adicionales:</span><span class="sxs-lookup"><span data-stu-id="23a6b-111">The following example requires names to start with `contoso` and contain six additional letters:</span></span>

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

## <a name="set-date-pattern-for-tag-value"></a><span data-ttu-id="23a6b-112">Establecimiento del patrón de fecha para el valor de etiqueta</span><span class="sxs-lookup"><span data-stu-id="23a6b-112">Set date pattern for tag value</span></span>

<span data-ttu-id="23a6b-113">Para requerir un patrón de fecha de dos dígitos, guion, tres letras, guion y cuatro dígitos, use:</span><span class="sxs-lookup"><span data-stu-id="23a6b-113">To require a date pattern of two digits, dash, three letters, dash, and four digits, use:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="23a6b-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23a6b-114">Next steps</span></span>
* <span data-ttu-id="23a6b-115">Después de definir una regla de directiva (como se muestra en los ejemplos anteriores), debe crear la definición de directiva y asignarla a un ámbito.</span><span class="sxs-lookup"><span data-stu-id="23a6b-115">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="23a6b-116">El ámbito puede ser una suscripción, un grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="23a6b-116">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="23a6b-117">Para asignar directivas a través del portal, consulte [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Uso de Azure Portal para asignar y administrar directivas de recursos).</span><span class="sxs-lookup"><span data-stu-id="23a6b-117">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="23a6b-118">Para asignar directivas a través de la API de REST, PowerShell o la CLI de Azure, consulte [Assign and manage policies through script](resource-manager-policy-create-assign.md) (Asignación y administración de directivas a través de scripts).</span><span class="sxs-lookup"><span data-stu-id="23a6b-118">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="23a6b-119">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="23a6b-119">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

