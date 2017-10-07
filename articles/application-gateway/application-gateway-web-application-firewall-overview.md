---
title: el servidor de aplicaciones de tooweb de aaaIntroduction (WAFS) para la puerta de enlace de aplicaciones de Azure | Documentos de Microsoft
description: "En esta página se proporciona información general sobre el firewall de aplicaciones web (WAF) de Application Gateway."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 04b362bc-6653-4765-86f6-55ee8ec2a0ff
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: amsriva
ms.openlocfilehash: 5a42ce0fb2bd12a391844099e2de8fa2571195e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="web-application-firewall-waf"></a>Firewall de aplicaciones web (WAF)

Firewall de aplicaciones web (WAF) es una característica de Application Gateway que proporciona a las aplicaciones una protección centralizada contra vulnerabilidades de seguridad comunes. 

Servidor de aplicaciones Web se basa en reglas de hello [conjuntos de reglas de núcleo OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 o 2.2.9. Las aplicaciones web son cada vez más los objetivos de ataques malintencionados que aprovechan vulnerabilidades comunes conocidas, como Comunes entre estas vulnerabilidades de seguridad son los ataques de inyección de SQL, scripting entre sitios ataques tooname algunos. Evitar estos ataques en el código de aplicación puede ser complicada y pueden requerir riguroso mantenimiento, supervisión en varias capas de la topología de la aplicación hello y aplicación de revisiones. Un servidor de seguridad de la aplicación web centralizada le ayuda a hacer mucho más fácil la administración de seguridad y ofrece una mejor seguridad a los administradores de tooapplication frente a amenazas o intrusiones. Una solución WAFS también puedan reaccionar de amenaza para la seguridad tooa más rápido por una vulnerabilidad conocida en una ubicación central en comparación con la protección de cada una de las aplicaciones web individuales de la aplicación de revisiones. Puertas de enlace de aplicaciones existentes pueden ser puerta de enlace de la aplicación de firewall habilitado de tooa convertido web aplicación fácilmente.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/WAF1.png)

Puerta de enlace de aplicaciones funciona como una finalización de SSL de controlador y las ofertas para la entrega de aplicación, afinidad de sesión basado en cookies, distribución de carga round robin, enrutamiento por contenidos, capacidad toohost varias mejoras de seguridad y sitios Web. Mejoras de seguridad que ofrece la puerta de enlace de aplicaciones incluyen la administración de directivas SSL, tooend final compatibilidad con SSL. Ahora se refuerza la seguridad de la aplicación mediante WAFS (servidor de aplicaciones web) que se integra directamente en la oferta de hello ADC. Esto proporciona un toomanage de ubicación central tooconfigure fácil y proteger las aplicaciones web contra vulnerabilidades de web comunes.

## <a name="benefits"></a>Ventajas

Hola Hola principales ventajas proporcionado por el servidor de aplicaciones web y de puerta de enlace de aplicaciones son:

### <a name="protection"></a>Protección

* Proteger la aplicación web frente a vulnerabilidades de web y ataques sin código de toobackend de modificación.

* Proteger web varias aplicaciones en hello mismo tiempo detrás de una puerta de enlace de la aplicación. Puerta de enlace de aplicaciones admite el hospedaje de sitios Web de too20 detrás de una sola puerta de enlace que puede protegerse contra los ataques de web con WAFS.

### <a name="monitoring"></a>Supervisión

* Supervise la aplicación web frente a ataques mediante un registro de WAF en tiempo real. Este registro se integra con [Monitor Azure](../monitoring-and-diagnostics/monitoring-overview.md) tootrack WAFS alertas y registra y supervisar las tendencias con facilidad.

* WAF se integrará con Azure Security Center pronto. Centro de seguridad de Azure permite una vista central del estado de seguridad de Hola de todos los recursos de Azure.

### <a name="customization"></a>Personalización

* las reglas de Hello capacidad toocustomize WAFS y regla agrupa toosuit los requisitos de la aplicación y eliminar los falsos positivos.

## <a name="features"></a>Características

Servidor de aplicaciones Web viene preconfigurado con CRS 3.0 de forma predeterminada o puede elegir toouse 2.2.9. CRS 3.0 permite reducir el número de falsos positivos con respecto a la versión 2.2.9. Hola capacidad demasiado[Personalizar reglas toosuit sus necesidades](application-gateway-customize-waf-rules-portal.md) se proporciona. Algunos de hello web las vulnerabilidades más comunes que firewall de la aplicación web protege contra incluye:

* Protección contra la inyección de código SQL
* Protección contra scripts entre sitios
* Protección contra ataques web comunes, como inyección de comandos, contrabando de solicitudes HTTP, división de respuestas HTTP y ataque remoto de inclusión de archivos
* Protección contra infracciones del protocolo HTTP
* Protección contra anomalías del protocolo HTTP, como la falta de agentes de usuario de host y encabezados de aceptación
* Prevención contra bots, rastreadores y escáneres
* Detección de errores de configuración comunes (es decir, Apache, IIS, etc.)

Para una lista más detallada de las reglas y los mecanismos de protección, consulte siguiente hello [principales de conjuntos de reglas](#core-rule-sets).

### <a name="core-rule-sets"></a>Conjuntos de reglas principales

Application Gateway admite dos conjuntos de reglas: CRS 3.0 y CRS 2.2.9. Estos conjuntos de reglas principales son colecciones de reglas que protegen las aplicaciones web frente a actividades malintencionadas.

#### <a name="owasp30"></a>OWASP_3.0

conjunto de reglas de núcleo de Hello 3.0 proporciona tiene 13 grupos de reglas como se muestra en hello en la tabla siguiente. Cada uno de estos grupos de reglas contiene varias reglas que se pueden deshabilitar.

|RuleGroup|Descripción|
|---|---|
|**[REQUEST-910-IP-REPUTATION](application-gateway-crs-rulegroups-rules.md#crs910)**|Contiene reglas tooprotect contra correo basura conocidos o actividad malintencionada.|
|**[REQUEST-911-METHOD-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs911)**|Contiene reglas toolock métodos descendentes (PUT, PATCH <..)|
|**[REQUEST-912-DOS-PROTECTION](application-gateway-crs-rulegroups-rules.md#crs912)**| Contiene reglas tooprotect frente a ataques de denegación de servicio (DoS).|
|**[REQUEST-913-SCANNER-DETECTION](application-gateway-crs-rulegroups-rules.md#crs913)**| Contiene reglas tooprotect con escáneres de puerto y el entorno.|
|**[REQUEST-920-PROTOCOL-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs920)**|Contiene reglas tooprotect en protocolo y codificación de problemas.|
|**[REQUEST-921-PROTOCOL-ATTACK](application-gateway-crs-rulegroups-rules.md#crs921)**|Contiene reglas tooprotect frente a inyección de encabezado, solicitudes no autorizadas y respuesta dividir|
|**[REQUEST-930-APPLICATION-ATTACK-LFI](application-gateway-crs-rulegroups-rules.md#crs930)**|Contiene reglas tooprotect frente a ataques de archivo y ruta de acceso.|
|**[REQUEST-931-APPLICATION-ATTACK-RFI](application-gateway-crs-rulegroups-rules.md#crs931)**|Contiene reglas tooprotect contra la inclusión de archivo remoto (RFI)|
|**[REQUEST-932-APPLICATION-ATTACK-RCE](application-gateway-crs-rulegroups-rules.md#crs932)**|Contiene reglas tooprotect volver a la ejecución remota de código.|
|**[REQUEST-933-APPLICATION-ATTACK-PHP](application-gateway-crs-rulegroups-rules.md#crs933)**|Contiene reglas tooprotect frente a ataques de inyección de PHP.|
|**[REQUEST-941-APPLICATION-ATTACK-XSS](application-gateway-crs-rulegroups-rules.md#crs941)**|Contiene reglas para protegerse contra los scripts entre sitios.|
|**[REQUEST-942-APPLICATION-ATTACK-SQLI](application-gateway-crs-rulegroups-rules.md#crs942)**|Contiene reglas para protegerse contra los ataques de inyección de código SQL.|
|**[REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION](application-gateway-crs-rulegroups-rules.md#crs943)**|Contiene reglas tooprotect frente a ataques de fijación de sesión.|

#### <a name="owasp229"></a>OWASP_2.2.9

conjunto de reglas de núcleo de Hello 2.2.9 proporcionado tiene 10 grupos de reglas como se muestra en hello en la tabla siguiente. Cada uno de estos grupos de reglas contiene varias reglas que se pueden deshabilitar.

|RuleGroup|Descripción|
|---|---|
|**[crs_20_protocol_violations](application-gateway-crs-rulegroups-rules.md#crs20)**|Contiene reglas tooprotect contra las infracciones de protocolos (caracteres no válidos, GET con un cuerpo de la solicitud, etcetera).|
|**[crs_21_protocol_anomalies](application-gateway-crs-rulegroups-rules.md#crs21)**|Contiene reglas tooprotect comparándolas con la información de encabezado incorrecto.|
|**[crs_23_request_limits](application-gateway-crs-rulegroups-rules.md#crs23)**|Contiene reglas tooprotect frente a argumentos o archivos que superan las limitaciones.|
|**[crs_30_http_policy](application-gateway-crs-rulegroups-rules.md#crs30)**|Contiene reglas tooprotect con métodos restringidos, los encabezados y los tipos de archivo. |
|**[crs_35_bad_robots](application-gateway-crs-rulegroups-rules.md#crs35)**|Contiene reglas tooprotect con rastreadores web y escáneres.|
|**[crs_40_generic_attacks](application-gateway-crs-rulegroups-rules.md#crs40)**|Contiene reglas tooprotect frente a ataques genéricos (fijación de sesión, inclusión de archivos remoto, inyección de PHP, etcetera.)|
|**[crs_41_sql_injection_attacks](application-gateway-crs-rulegroups-rules.md#crs41sql)**|Contiene reglas tooprotect contra los ataques de inyección de SQL|
|**[crs_41_xss_attacks](application-gateway-crs-rulegroups-rules.md#crs41xss)**|Contiene reglas tooprotect con scripts entre sitios.|
|**[crs_42_tight_security](application-gateway-crs-rulegroups-rules.md#crs42)**|Contiene un tooprotect regla contra los ataques de salto de ruta de acceso|
|**[crs_45_trojans](application-gateway-crs-rulegroups-rules.md#crs45)**|Contiene reglas tooprotect contra troyanos de puerta trasera.|

### <a name="waf-modes"></a>Modos de WAF

WAFS de puerta de enlace de aplicaciones puede ser configurado toorun Hola después de dos modos:

* **Modo de detección** : cuando toorun configurado en modo de detección, WAFS de puerta de enlace de aplicaciones supervisa y registra todas las alertas de amenaza en el archivo de registro tooa. Diagnósticos de registro de puerta de enlace de aplicaciones deben activarse con hello **diagnósticos** sección. También debe tooensure que Hola WAFS registro está seleccionado y activado. Cuando se ejecuta en modo de detección, el firewall de aplicaciones de web no bloquea las solicitudes entrantes.
* **Modo de prevención** : cuando toorun configurado en modo de prevención, puerta de enlace de aplicación bloquea activamente las intrusiones y ataques detectados por sus reglas. atacante Hola recibe una excepción de acceso no autorizado 403 y Hola conexión se termina. Modo de prevención continúa toolog estos ataques en los registros de hello WAFS.

### <a name="application-gateway-waf-reports"></a>Supervisión de WAF

Es importante supervisar el estado de saludo de la puerta de enlace de la aplicación. Supervisar el estado de hello las aplicaciones aplicación de web hello y firewall que protege se proporcionan a través de registro y la integración con Monitor de Azure y Azure Security Center (próximamente), análisis de registros.

![diagnóstico](./media/application-gateway-web-application-firewall-overview/diagnostics.png)

#### <a name="azure-monitor"></a>Azure Monitor

Cada registro de Application Gateway se integra con [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md).  Esto le permite la información de diagnóstico de tootrack incluidos registros y alertas de WAFS.  Esta funcionalidad se proporciona en recursos de puerta de enlace de aplicaciones en portal de hello en Hola Hola **diagnósticos** pestaña o a través de hello Azure Monitor de servicio directamente. toolearn más acerca de cómo habilitar los registros de diagnóstico de puerta de enlace de aplicaciones, visite [diagnóstico de puerta de enlace de aplicaciones](application-gateway-diagnostics.md)

#### <a name="azure-security-center"></a>Azure Security Center

[Centro de seguridad de Azure](../security-center/security-center-intro.md) Hola de ayuda a evitar, detectar y responder toothreats con una mayor visibilidad de y control sobre la seguridad de los recursos de Azure. Application Gateway ahora [se integra en Azure Security Center](application-gateway-integration-security-center.md). Centro de seguridad de Azure examina las aplicaciones web de toodetect desprotegido de entorno. Ahora pueden recomendar a aplicación puerta de enlace WAFS tooprotect estos recursos vulnerables. Puede crear directamente WAFS de puerta de enlace de aplicaciones de hello Azure Security Center.  Estas instancias WAFS se integran con el centro de seguridad de Azure y se devuelva alertas e información de estado tooAzure centro de seguridad para los informes.

![Figura 1](./media/application-gateway-web-application-firewall-overview/figure1.png)

#### <a name="logging"></a>Registro

WAF de Application Gateway ofrece informes detallados sobre las amenazas detectadas. El registro se integra con los registros de Diagnósticos de Azure y las alertas se registran en formato json. Estos registros pueden integrarse con [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).

![imageURLroute](./media/application-gateway-web-application-firewall-overview/waf2.png)

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

## <a name="application-gateway-waf-sku-pricing"></a>Precios de las SKU de WAF de Application Gateway

El firewall de aplicaciones web está disponible en una nueva SKU de WAF. Esta SKU está disponible solo en el modelo de aprovisionamiento de Azure Resource Manager y no en el modelo de implementación clásica de Hola. Además, la SKU de WAF está solo disponible para tamaños de instancias medianas y grandes de Application Gateway. También aplican en todos los límites de Hola para puerta de enlace de aplicaciones toohello WAFS SKU. El precio se basa en una tarifa por instancia de puerta de enlace por hora y una tarifa de procesamiento de datos. El precio de puerta de enlace por hora para una SKU de WAF es diferente a los costos de una SKU estándar y puede encontrar más información sobre estos en los [detalles de precios de Application Gateway](https://azure.microsoft.com/pricing/details/application-gateway/). Procesamiento de datos siguen siendo cargos Hola igual. No hay ningún costo por regla o grupo de reglas. Puede proteger varias aplicaciones web detrás de hello mismo web servidor de aplicaciones y no hay ningún cargo adicional para admitir varias aplicaciones. 

La facturación de WAFS eficazmente inicia 5/5/2017 hasta hello, a continuación, las puertas de enlace de SKU WAFS continúa toobe cobra tarifas estándar.

## <a name="next-steps"></a>Pasos siguientes

Después de obtener más información acerca de las capacidades de Hola de WAFS, visite [cómo tooconfigure web firewall de la aplicación en Application Gateway](application-gateway-web-application-firewall-portal.md).

