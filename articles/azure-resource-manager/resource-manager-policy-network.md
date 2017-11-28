---
title: las directivas de recursos de aaaAzure recursos de red | Documentos de Microsoft
description: "Describe las directivas del Administrador de recursos de Azure para administrar la implementación de Hola de los recursos de red."
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
ms.openlocfilehash: a6072c1c30db0a4e4a1cae04efc7828d14069709
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toonetwork-resources"></a><span data-ttu-id="ebd39-103">Aplicar directivas toonetwork de recursos</span><span class="sxs-lookup"><span data-stu-id="ebd39-103">Apply resource policies toonetwork resources</span></span>
<span data-ttu-id="ebd39-104">En este artículo se muestra un ejemplo [directiva recursos](resource-manager-policy.md) puede aplicar las puertas de enlace de red virtual de tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ebd39-104">This article shows an example [resource policy](resource-manager-policy.md) you can apply tooAzure virtual network gateways.</span></span> <span data-ttu-id="ebd39-105">Esta directiva garantiza la coherencia de las puertas de enlace implementadas en su organización.</span><span class="sxs-lookup"><span data-stu-id="ebd39-105">This policy ensures consistency for gateways deployed in your organization.</span></span> 

## <a name="define-permitted-virtual-network-gateway-sku"></a><span data-ttu-id="ebd39-106">Definición de la SKU de la puerta de enlace de red virtual permitida</span><span class="sxs-lookup"><span data-stu-id="ebd39-106">Define permitted virtual network gateway SKU</span></span>

<span data-ttu-id="ebd39-107">Hola después directiva restringe qué SKU se pueden implementar para puertas de enlace de red virtual:</span><span class="sxs-lookup"><span data-stu-id="ebd39-107">hello following policy restricts which SKUs can be deployed for virtual network gateways:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ebd39-108">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ebd39-108">Next steps</span></span>
* <span data-ttu-id="ebd39-109">Después de definir una regla de directiva (como se muestra en hello anteriores ejemplos), se necesita la definición de la directiva de toocreate hello y se asigna tooa ámbito.</span><span class="sxs-lookup"><span data-stu-id="ebd39-109">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="ebd39-110">Hola ámbito puede ser una suscripción, el grupo de recursos o el recurso.</span><span class="sxs-lookup"><span data-stu-id="ebd39-110">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="ebd39-111">directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ebd39-111">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="ebd39-112">directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="ebd39-112">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span> 
* <span data-ttu-id="ebd39-113">Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="ebd39-113">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

