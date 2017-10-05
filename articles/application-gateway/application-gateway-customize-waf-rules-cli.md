---
title: "Personalización de reglas de firewall de aplicaciones web en Azure Application Gateway mediante la CLI de Azure 2.0 | Microsoft Docs"
description: "En este artículo se proporciona información acerca de cómo personalizar reglas de firewall de aplicaciones web en Application Gateway con la CLI de Azure 2.0."
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
ms.openlocfilehash: 456be048dc2d82cd50d145b71f17a84a7189ea96
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-cli-20"></a><span data-ttu-id="98b11-103">Personalización de reglas de firewall de aplicaciones web mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="98b11-103">Customize web application firewall rules through the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="98b11-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="98b11-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="98b11-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="98b11-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="98b11-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="98b11-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="98b11-107">El firewall de aplicaciones web (WAF) de Azure Application Gateway proporciona protección a las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="98b11-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="98b11-108">Dicha protección la proporciona Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span><span class="sxs-lookup"><span data-stu-id="98b11-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="98b11-109">Algunas reglas pueden producir falsos positivos y bloquear el tráfico real.</span><span class="sxs-lookup"><span data-stu-id="98b11-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="98b11-110">Por este motivo, Application Gateway ofrece la posibilidad de personalizar reglas y grupos de reglas.</span><span class="sxs-lookup"><span data-stu-id="98b11-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="98b11-111">Para más información acerca de reglas y grupos de reglas específicos, consulte [Lista de reglas y grupos de reglas de CRS de firewall de aplicaciones web que se ofrecen](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="98b11-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="98b11-112">Visualización de reglas y grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="98b11-112">View rule groups and rules</span></span>

<span data-ttu-id="98b11-113">Los siguientes ejemplos de código muestran cómo ver las reglas y los grupos de reglas que se pueden configurar.</span><span class="sxs-lookup"><span data-stu-id="98b11-113">The following code examples show how to view rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="98b11-114">Visualización del grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="98b11-114">View rule groups</span></span>

<span data-ttu-id="98b11-115">En el ejemplo siguiente se muestra cómo ver los grupos de reglas:</span><span class="sxs-lookup"><span data-stu-id="98b11-115">The following example shows how to view the rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="98b11-116">La siguiente salida es una respuesta truncada del ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="98b11-116">The following output is a truncated response from the preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="98b11-117">Reglas de vista en un grupo de reglas</span><span class="sxs-lookup"><span data-stu-id="98b11-117">View rules in a rule group</span></span>

<span data-ttu-id="98b11-118">En el ejemplo siguiente se muestra cómo ver las reglas en un grupo de reglas específico:</span><span class="sxs-lookup"><span data-stu-id="98b11-118">The following example shows how to view rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="98b11-119">La siguiente salida es una respuesta truncada del ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="98b11-119">The following output is a truncated response from the preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="98b11-120">Deshabilitar reglas</span><span class="sxs-lookup"><span data-stu-id="98b11-120">Disable rules</span></span>

<span data-ttu-id="98b11-121">En el ejemplo siguiente se deshabilitan las reglas `910018` y `910017` en una puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="98b11-121">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="98b11-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="98b11-122">Next steps</span></span>

<span data-ttu-id="98b11-123">Después de configurar las reglas deshabilitadas, puede aprender a ver los registros de WAFS.</span><span class="sxs-lookup"><span data-stu-id="98b11-123">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="98b11-124">Para más información, consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="98b11-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
