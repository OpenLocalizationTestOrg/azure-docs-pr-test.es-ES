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
# <a name="customize-web-application-firewall-rules-through-powershell"></a>Personalización de reglas de firewall de aplicaciones web mediante PowerShell

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [CLI de Azure 2.0](application-gateway-customize-waf-rules-cli.md)

servidor de aplicaciones web de Hello puerta de enlace de aplicaciones de Azure (WAFS) proporciona protección para las aplicaciones web. Estas protecciones proceden de hello Abrir proyecto de seguridad aplicación de Web (OWASP) Core regla establecer (CR). Algunas reglas pueden producir falsos positivos y bloquear el tráfico real. Por esta razón, puerta de enlace de aplicaciones proporciona reglas y grupos de reglas de hello capacidad toocustomize. Para obtener más información sobre los grupos de reglas específicos de Hola y reglas, consulte [lista de reglas y grupos de CRS regla de firewall de aplicación web](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Visualización de reglas y grupos de reglas

Hola, ejemplos de código siguientes muestra cómo tooview las reglas y grupos que se pueden configurables en una puerta de enlace de la aplicación habilitada para WAFS de reglas.

### <a name="view-rule-groups"></a>Visualización del grupos de reglas

Hola siguiente ejemplo se muestra cómo los grupos de reglas de tooview:

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

Hola después de salida es una respuesta truncada del anterior ejemplo de Hola:

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

## <a name="disable-rules"></a>Deshabilitar reglas

Hello en el ejemplo siguiente se deshabilita reglas `910018` y `910017` en una puerta de enlace de la aplicación:

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Pasos siguientes

Después de configurar las reglas deshabilitadas, aprenderá cómo tooview los registros WAFS. Para más información, consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
