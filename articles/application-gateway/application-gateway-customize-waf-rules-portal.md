---
title: "Personalización de reglas de firewall de aplicaciones web en Azure Application Gateway (Azure Portal) | Microsoft Docs"
description: "En este artículo se proporciona información acerca de cómo personalizar reglas de firewall de aplicaciones web en Application Gateway con Azure Portal."
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
ms.openlocfilehash: cdcbadbc3765dfc583c26e1b1453863d421c9a72
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-portal"></a>Personalización de reglas de firewall de aplicaciones web mediante Azure Portal

> [!div class="op_single_selector"]
> * [Portal de Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [CLI de Azure 2.0](application-gateway-customize-waf-rules-cli.md)

El firewall de aplicaciones web (WAF) de Azure Application Gateway proporciona protección a las aplicaciones web. Dicha protección la proporciona Open Web Application Security Project (OWASP) Core Rule Set (CRS). Algunas reglas pueden producir falsos positivos y bloquear el tráfico real. Por este motivo, Application Gateway ofrece la posibilidad de personalizar reglas y grupos de reglas. Para más información acerca de reglas y grupos de reglas específicos, consulte [Lista de reglas y grupos de reglas de CRS de firewall de aplicaciones web que se ofrecen](application-gateway-crs-rulegroups-rules.md).

>[!NOTE]
> Si la puerta de enlace de aplicaciones no usa el nivel WAF, la opción para actualizar la puerta de enlace de aplicaciones al nivel WAF aparece en el panel derecho. 

![Habilitar WAF][fig1]

## <a name="view-rule-groups-and-rules"></a>Visualización de reglas y grupos de reglas

**Para ver reglas y grupos de reglas**
   1. Navegue hasta la puerta de enlace de aplicaciones y seleccione **Firewall de aplicaciones web**.  
   2. Seleccione **Configuración de reglas avanzada**.  
   Esta vista muestra una tabla en la página de todos los grupos de reglas proporcionados con el conjunto de reglas elegido. Todas las casillas de la regla están seleccionadas.

![Configurar reglas deshabilitadas][1]

## <a name="search-for-rules-to-disable"></a>Búsqueda de reglas para deshabilitar

La hoja **Web application firewall settings** (Configuración del firewall de aplicaciones web) ofrece la posibilidad de filtrar las reglas a través de una búsqueda de texto. El resultado muestra solo las reglas y los grupos de reglas que contienen el texto que se ha buscado.

![Buscar reglas][2]

## <a name="disable-rule-groups-and-rules"></a>Deshabilitación de reglas y grupos de reglas

Al deshabilitar reglas, se puede deshabilitar un grupo de reglas completo o reglas específicas de uno o más grupos de reglas. 

**Para deshabilitar grupos de reglas o reglas concretas**

   1. Busque las reglas o los grupos de reglas que desea deshabilitar.
   2. Desactive las casillas de las reglas que desea deshabilitar. 
   2. Seleccione **Guardar**. 

![Guardar cambios][3]

## <a name="next-steps"></a>Pasos siguientes

Después de configurar las reglas deshabilitadas, puede aprender a ver los registros de WAFS. Para más información, consulte [Diagnósticos de Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
