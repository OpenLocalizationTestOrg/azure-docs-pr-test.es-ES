---
title: "Personalización de reglas de firewall de aplicaciones web en Azure Application Gateway: PowerShell | Microsoft Docs"
description: "En este artículo se proporciona información acerca de cómo personalizar las reglas de firewall de aplicaciones web en Application Gateway con PowerShell."
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
ms.openlocfilehash: 681625e40035b05c593c6161236cb80b7db576b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="abe6b-103">Personalización de reglas de firewall de aplicaciones web mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="abe6b-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="abe6b-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="abe6b-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="abe6b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="abe6b-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="abe6b-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="abe6b-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="abe6b-107">El firewall de aplicaciones web (WAF) de Azure Application Gateway proporciona protección a las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="abe6b-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="abe6b-108">Dicha protección la proporciona Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span><span class="sxs-lookup"><span data-stu-id="abe6b-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="abe6b-109">Algunas reglas pueden producir falsos positivos y bloquear el tráfico real.</span><span class="sxs-lookup"><span data-stu-id="abe6b-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="abe6b-110">Por este motivo, Application Gateway ofrece la posibilidad de personalizar reglas y grupos de reglas.</span><span class="sxs-lookup"><span data-stu-id="abe6b-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="abe6b-111">Para más información acerca de reglas y grupos de reglas específicos, consulte [Lista de reglas y grupos de reglas de CRS de firewall de aplicaciones web que se ofrecen](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="abe6b-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="abe6b-112">Visualización de reglas y grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="abe6b-112">View rule groups and rules</span></span>

<span data-ttu-id="abe6b-113">Los siguientes ejemplos de código muestran cómo ver las reglas y los grupos de reglas que se pueden configurar en una puerta de enlace de aplicaciones con WAF habilitado.</span><span class="sxs-lookup"><span data-stu-id="abe6b-113">The following code examples show how to view rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="abe6b-114">Visualización del grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="abe6b-114">View rule groups</span></span>

<span data-ttu-id="abe6b-115">En el ejemplo siguiente se muestra cómo ver grupos de reglas:</span><span class="sxs-lookup"><span data-stu-id="abe6b-115">The following example shows how to view rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="abe6b-116">La siguiente salida es una respuesta truncada del ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="abe6b-116">The following output is a truncated response from the preceding example:</span></span>

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a><span data-ttu-id="abe6b-117">Deshabilitar reglas</span><span class="sxs-lookup"><span data-stu-id="abe6b-117">Disable rules</span></span>

<span data-ttu-id="abe6b-118">En el ejemplo siguiente se deshabilitan las reglas `910018` y `910017` en una puerta de enlace de aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="abe6b-118">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="abe6b-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="abe6b-119">Next steps</span></span>

<span data-ttu-id="abe6b-120">Después de configurar las reglas deshabilitadas, puede aprender a ver los registros de WAFS.</span><span class="sxs-lookup"><span data-stu-id="abe6b-120">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="abe6b-121">Para más información, consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="abe6b-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
