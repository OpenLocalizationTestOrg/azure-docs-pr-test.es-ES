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
# <a name="apply-resource-policies-toonetwork-resources"></a>Aplicar directivas toonetwork de recursos
En este artículo se muestra un ejemplo [directiva recursos](resource-manager-policy.md) puede aplicar las puertas de enlace de red virtual de tooAzure. Esta directiva garantiza la coherencia de las puertas de enlace implementadas en su organización. 

## <a name="define-permitted-virtual-network-gateway-sku"></a>Definición de la SKU de la puerta de enlace de red virtual permitida

Hola después directiva restringe qué SKU se pueden implementar para puertas de enlace de red virtual:

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

## <a name="next-steps"></a>Pasos siguientes
* Después de definir una regla de directiva (como se muestra en hello anteriores ejemplos), se necesita la definición de la directiva de toocreate hello y se asigna tooa ámbito. Hola ámbito puede ser una suscripción, el grupo de recursos o el recurso. directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md). directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md). 
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

