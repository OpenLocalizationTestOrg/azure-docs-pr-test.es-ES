---
title: "reglas de firewall de aplicación aaaCustomize web en la puerta de enlace de la aplicación de Azure: portal de Azure | Documentos de Microsoft"
description: "Este artículo proporciona información sobre cómo las reglas firewall de aplicación web de toocustomize en la puerta de enlace de aplicaciones con hello portal de Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a>Personalizar reglas de firewall de aplicación web a través de hello portal de Azure

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [CLI de Azure 2.0](application-gateway-customize-waf-rules-cli.md)

servidor de aplicaciones web de Hello puerta de enlace de aplicaciones de Azure (WAFS) proporciona protección para las aplicaciones web. Estas protecciones proceden de hello Abrir proyecto de seguridad aplicación de Web (OWASP) Core regla establecer (CR). Algunas reglas pueden producir falsos positivos y bloquear el tráfico real. Por esta razón, puerta de enlace de aplicaciones proporciona reglas y grupos de reglas de hello capacidad toocustomize. Para obtener más información sobre los grupos de reglas específicos de Hola y reglas, consulte [lista de reglas y grupos de reglas de web application firewall CR](application-gateway-crs-rulegroups-rules.md).

>[!NOTE]
> Si la puerta de enlace de la aplicación no está usando capa de hello WAFS, Hola opción tooupgrade Hola puerta de enlace toohello WAFS capa de aplicación aparece en el panel derecho de Hola. 

![Habilitar WAF][fig1]

## <a name="view-rule-groups-and-rules"></a>Visualización de reglas y grupos de reglas

**las reglas y grupos de reglas de tooview**
   1. Vaya toohello puerta de enlace de aplicaciones y, a continuación, seleccione **firewall de aplicación Web**.  
   2. Seleccione **Configuración de reglas avanzada**.  
   Esta vista muestra una tabla en la página de Hola de todos los grupos de reglas de hello proporcionada con hello elegido el conjunto de reglas. Se seleccionan todos de casillas de verificación de la regla de Hola.

![Configurar reglas deshabilitadas][1]

## <a name="search-for-rules-toodisable"></a>Buscar reglas toodisable

Hola **configuración de firewall de aplicación Web** hoja proporciona capacidad de hello toofilter reglas de Hola a través de una búsqueda de texto. resultado de Hello muestra solo los grupos de reglas de Hola y las reglas que contengan texto hello buscado.

![Buscar reglas][2]

## <a name="disable-rule-groups-and-rules"></a>Deshabilitación de reglas y grupos de reglas

Al deshabilitar reglas, se puede deshabilitar un grupo de reglas completo o reglas específicas de uno o más grupos de reglas. 

**grupos de reglas de toodisable o reglas específicas**

   1. Buscar reglas de Hola o grupos de reglas que desea toodisable.
   2. Desactive casillas de verificación de Hola para hello las reglas que desea toodisable. 
   2. Seleccione **Guardar**. 

![Guardar cambios][3]

## <a name="next-steps"></a>Pasos siguientes

Después de configurar las reglas deshabilitadas, aprenderá cómo tooview los registros WAFS. Para más información, consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
