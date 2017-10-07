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
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a><span data-ttu-id="a1440-103">Personalizar reglas de firewall de aplicación web a través de hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a1440-103">Customize web application firewall rules through hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1440-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a1440-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="a1440-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1440-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="a1440-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a1440-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="a1440-107">servidor de aplicaciones web de Hello puerta de enlace de aplicaciones de Azure (WAFS) proporciona protección para las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="a1440-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="a1440-108">Estas protecciones proceden de hello Abrir proyecto de seguridad aplicación de Web (OWASP) Core regla establecer (CR).</span><span class="sxs-lookup"><span data-stu-id="a1440-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="a1440-109">Algunas reglas pueden producir falsos positivos y bloquear el tráfico real.</span><span class="sxs-lookup"><span data-stu-id="a1440-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="a1440-110">Por esta razón, puerta de enlace de aplicaciones proporciona reglas y grupos de reglas de hello capacidad toocustomize.</span><span class="sxs-lookup"><span data-stu-id="a1440-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="a1440-111">Para obtener más información sobre los grupos de reglas específicos de Hola y reglas, consulte [lista de reglas y grupos de reglas de web application firewall CR](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="a1440-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="a1440-112">Visualización de reglas y grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="a1440-112">View rule groups and rules</span></span>

<span data-ttu-id="a1440-113">Hola, ejemplos de código siguientes muestra cómo tooview las reglas y grupos que se pueden configurables de reglas.</span><span class="sxs-lookup"><span data-stu-id="a1440-113">hello following code examples show how tooview rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="a1440-114">Visualización del grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="a1440-114">View rule groups</span></span>

<span data-ttu-id="a1440-115">Hola de ejemplo siguiente muestra cómo tooview Hola grupos de reglas:</span><span class="sxs-lookup"><span data-stu-id="a1440-115">hello following example shows how tooview hello rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="a1440-116">Hola después de salida es una respuesta truncada del anterior ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="a1440-116">hello following output is a truncated response from hello preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="a1440-117">Reglas de vista en un grupo de reglas</span><span class="sxs-lookup"><span data-stu-id="a1440-117">View rules in a rule group</span></span>

<span data-ttu-id="a1440-118">Hola de ejemplo siguiente muestra cómo las reglas de tooview en un grupo de reglas especificado:</span><span class="sxs-lookup"><span data-stu-id="a1440-118">hello following example shows how tooview rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="a1440-119">Hola después de salida es una respuesta truncada del anterior ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="a1440-119">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="a1440-120">Deshabilitar reglas</span><span class="sxs-lookup"><span data-stu-id="a1440-120">Disable rules</span></span>

<span data-ttu-id="a1440-121">Hello en el ejemplo siguiente se deshabilita reglas `910018` y `910017` en una puerta de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="a1440-121">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="a1440-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1440-122">Next steps</span></span>

<span data-ttu-id="a1440-123">Después de configurar las reglas deshabilitadas, aprenderá cómo tooview los registros WAFS.</span><span class="sxs-lookup"><span data-stu-id="a1440-123">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="a1440-124">Para más información, consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="a1440-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
