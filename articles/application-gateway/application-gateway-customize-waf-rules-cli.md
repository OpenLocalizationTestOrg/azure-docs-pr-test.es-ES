---
title: "reglas de firewall de aplicación aaaCustomize web en la puerta de enlace de la aplicación de Azure - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Este artículo proporciona información sobre cómo las reglas firewall de aplicación web de toocustomize en la puerta de enlace de aplicaciones con hello 2.0 de CLI de Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b83ffb9f6a7e0d0c8c970885d2bcb3b63d32581c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a>Personalizar reglas de firewall de aplicación web a través de hello 2.0 de CLI de Azure

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [CLI de Azure 2.0](application-gateway-customize-waf-rules-cli.md)

servidor de aplicaciones web de Hello puerta de enlace de aplicaciones de Azure (WAFS) proporciona protección para las aplicaciones web. Estas protecciones proceden de hello Abrir proyecto de seguridad aplicación de Web (OWASP) Core regla establecer (CR). Algunas reglas pueden producir falsos positivos y bloquear el tráfico real. Por esta razón, puerta de enlace de aplicaciones proporciona reglas y grupos de reglas de hello capacidad toocustomize. Para obtener más información sobre los grupos de reglas específicos de Hola y reglas, consulte [lista de reglas y grupos de reglas de web application firewall CR](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Visualización de reglas y grupos de reglas

Hola, ejemplos de código siguientes muestra cómo tooview las reglas y grupos que se pueden configurables de reglas.

### <a name="view-rule-groups"></a>Visualización del grupos de reglas

Hola de ejemplo siguiente muestra cómo tooview Hola grupos de reglas:

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

Hola después de salida es una respuesta truncada del anterior ejemplo de Hola:

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a>Reglas de vista en un grupo de reglas

Hola de ejemplo siguiente muestra cómo las reglas de tooview en un grupo de reglas especificado:

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

Hola después de salida es una respuesta truncada del anterior ejemplo de Hola:

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a>Deshabilitar reglas

Hello en el ejemplo siguiente se deshabilita reglas `910018` y `910017` en una puerta de enlace de la aplicación:

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Pasos siguientes

Después de configurar las reglas deshabilitadas, aprenderá cómo tooview los registros WAFS. Para más información, consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
