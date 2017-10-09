---
title: "reglas de firewall de aplicación aaaCustomize web en la puerta de enlace de la aplicación de Azure - PowerShell | Documentos de Microsoft"
description: "En este artículo se proporciona información sobre cómo las reglas de firewall de aplicación web de toocustomize en la puerta de enlace de aplicaciones con PowerShell."
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
ms.openlocfilehash: f320e687b0f621515255469dac8e375cdd900dda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="c6595-103">Personalización de reglas de firewall de aplicaciones web mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6595-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6595-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c6595-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="c6595-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6595-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="c6595-106">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c6595-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="c6595-107">servidor de aplicaciones web de Hello puerta de enlace de aplicaciones de Azure (WAFS) proporciona protección para las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="c6595-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="c6595-108">Estas protecciones proceden de hello Abrir proyecto de seguridad aplicación de Web (OWASP) Core regla establecer (CR).</span><span class="sxs-lookup"><span data-stu-id="c6595-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="c6595-109">Algunas reglas pueden producir falsos positivos y bloquear el tráfico real.</span><span class="sxs-lookup"><span data-stu-id="c6595-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="c6595-110">Por esta razón, puerta de enlace de aplicaciones proporciona reglas y grupos de reglas de hello capacidad toocustomize.</span><span class="sxs-lookup"><span data-stu-id="c6595-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="c6595-111">Para obtener más información sobre los grupos de reglas específicos de Hola y reglas, consulte [lista de reglas y grupos de CRS regla de firewall de aplicación web](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="c6595-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="c6595-112">Visualización de reglas y grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="c6595-112">View rule groups and rules</span></span>

<span data-ttu-id="c6595-113">Hola, ejemplos de código siguientes muestra cómo tooview las reglas y grupos que se pueden configurables en una puerta de enlace de la aplicación habilitada para WAFS de reglas.</span><span class="sxs-lookup"><span data-stu-id="c6595-113">hello following code examples show how tooview rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="c6595-114">Visualización del grupos de reglas</span><span class="sxs-lookup"><span data-stu-id="c6595-114">View rule groups</span></span>

<span data-ttu-id="c6595-115">Hola siguiente ejemplo se muestra cómo los grupos de reglas de tooview:</span><span class="sxs-lookup"><span data-stu-id="c6595-115">hello following example shows how tooview rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="c6595-116">Hola después de salida es una respuesta truncada del anterior ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c6595-116">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="c6595-117">Deshabilitar reglas</span><span class="sxs-lookup"><span data-stu-id="c6595-117">Disable rules</span></span>

<span data-ttu-id="c6595-118">Hello en el ejemplo siguiente se deshabilita reglas `910018` y `910017` en una puerta de enlace de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="c6595-118">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="c6595-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c6595-119">Next steps</span></span>

<span data-ttu-id="c6595-120">Después de configurar las reglas deshabilitadas, aprenderá cómo tooview los registros WAFS.</span><span class="sxs-lookup"><span data-stu-id="c6595-120">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="c6595-121">Para más información, consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="c6595-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
