---
title: Directivas de recursos de Azure para recursos de red | Microsoft Docs
description: "Se describen las directivas de Azure Resource Manager para administrar la implementación de recursos de red."
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
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: bca66bbdd9da9b3e4099d0d961f42c9368a17f5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="apply-resource-policies-to-network-resources"></a><span data-ttu-id="d8650-103">Aplicación de directivas de recursos a recursos de red</span><span class="sxs-lookup"><span data-stu-id="d8650-103">Apply resource policies to network resources</span></span>
<span data-ttu-id="d8650-104">En este artículo se muestra una [directiva de recursos](resource-manager-policy.md) de ejemplo que se puede aplicar a las puertas de enlace de red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="d8650-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply to Azure virtual network gateways.</span></span> <span data-ttu-id="d8650-105">Esta directiva garantiza la coherencia de las puertas de enlace implementadas en su organización.</span><span class="sxs-lookup"><span data-stu-id="d8650-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="d8650-106">Definición de la SKU de la puerta de enlace de red virtual permitida</span><span class="sxs-lookup"><span data-stu-id="d8650-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="d8650-107">La siguiente directiva restringe las SKU que se pueden implementar para las puertas de enlace de red virtual:</span><span class="sxs-lookup"><span data-stu-id="d8650-107">The following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Network/virtualNetworkGateways"
      },
      {
        "not": {
          "field": "Microsoft.Network/virtualNetworkGateways/sku.name",
          "in": [
            "Basic",
            "VpnGw1"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="d8650-108">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d8650-108">Next steps</span></span>
* <span data-ttu-id="d8650-109">Después de definir una regla de directiva (como se muestra en los ejemplos anteriores), debe crear la definición de directiva y asignarla a un ámbito.</span><span class="sxs-lookup"><span data-stu-id="d8650-109">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="d8650-110">El ámbito puede ser una suscripción, un grupo de recursos o un recurso.</span><span class="sxs-lookup"><span data-stu-id="d8650-110">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="d8650-111">Para asignar directivas a través del portal, consulte [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) (Uso de Azure Portal para asignar y administrar directivas de recursos).</span><span class="sxs-lookup"><span data-stu-id="d8650-111">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="d8650-112">Para asignar directivas a través de la API de REST, PowerShell o la CLI de Azure, consulte [Assign and manage policies through script](resource-manager-policy-create-assign.md) (Asignación y administración de directivas a través de scripts).</span><span class="sxs-lookup"><span data-stu-id="d8650-112">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="d8650-113">Para obtener instrucciones sobre cómo las empresas pueden utilizar Resource Manager para administrar eficazmente las suscripciones, vea [Scaffold empresarial de Azure: Gobierno de suscripción prescriptivo](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="d8650-113">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
