---
title: aaaFrequently pregunta para puerta de enlace de aplicaciones de Azure | Documentos de Microsoft
description: "Esta página proporciona respuestas toofrequently preguntas más frecuentes sobre la puerta de enlace de aplicaciones de Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a>Preguntas más frecuentes sobre Application Gateway

## <a name="general"></a>General

**P. ¿Qué es Application Gateway?**

Azure Application Gateway es un controlador de entrega de aplicaciones (ADC) como servicio que ofrece diversas funcionalidades de equilibrio de carga de nivel 7 para sus aplicaciones. Ofrece un servicio altamente disponible y escalable que está completamente administrado por Azure.

**P. ¿Qué características admite Application Gateway?**

Puerta de enlace de aplicaciones admite SSL tooend final y la descarga de SSL, servidor de aplicaciones Web, afinidad de sesión basado en cookies, dirección url basada en la ruta de acceso enrutamiento, alojamiento de varios sitios y otros. Para obtener una lista completa de las características admitidas, visite [Introducción tooApplication puerta de enlace](application-gateway-introduction.md)

**P. ¿Cuál es la diferencia de hello entre la puerta de enlace de aplicaciones y el equilibrador de carga de Azure?**

Application Gateway es un equilibrador de carga de nivel 7, lo que significa que funciona solo tráfico web (HTTP/HTTPS/WebSocket). Admite funcionalidades como la terminación SSL, la afinidad de sesión basada en cookies y la distribución round robin para el tráfico de equilibrio de carga. Load Balancer equilibra la carga de tráfico en el nivel 4 (TCP/UDP).

**P. ¿Qué protocolos admite Application Gateway?**

Application Gateway admite HTTP, HTTPS y WebSocket.

**P. ¿Qué recursos son compatibles actualmente como parte del grupo de back-end?**

Los grupos de back-end pueden constar de NIC, conjuntos de escalado de máquinas virtuales, direcciones IP públicas e internas, nombres de dominio completos (FQDN) y servidores back-end multiinquilino como Azure Web Apps. Puerta de enlace de aplicaciones los miembros del grupo back-end no están unidos tooan conjunto de disponibilidad. Los miembros de grupos de back-end pueden estar repartidos entre clústeres, centros de datos o fuera de Azure siempre y cuando dispongan de conectividad IP.

**P. ¿Qué regiones es servicio de hello disponibles en?**

Application Gateway está disponible en todas las regiones de Azure global. También está disponible en [Azure China](https://www.azure.cn/) y [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)

**P. ¿Se trata de una implementación dedicada para mi suscripción o compartida entre los clientes?**

Application Gateway es una implementación dedicada en su red virtual.

**P. ¿Se admite la redirección HTTP->HTTPS?**

Se admite el redireccionamiento. Visite [introducción de redirección de puerta de enlace de aplicaciones](application-gateway-redirect-overview.md) toolearn más.

**P. ¿En qué orden se procesan los agentes de escucha?**

Los agentes de escucha se procesan en orden de Hola se muestran. Por este motivo, si un agente de escucha coincide con una solicitud entrante, se procesa primero.  Los agentes de escucha de varios sitios deben configurarse antes de que el tráfico de tooensure de un agente de escucha básico es toohello enrutado correcto back-end.

**P. ¿Dónde se encuentra la dirección IP y el DNS de Application Gateway?**

Cuando se usa una dirección IP pública como un punto de conexión, puede encontrar esta información en recurso de dirección IP público de Hola o en la página de información general de Hola para hello puerta de enlace de aplicaciones en portal de Hola. Para las direcciones IP internas, se puede encontrar en la página de información general de Hola.

**P. ¿Hello IP o DNS cambia largo de duración de Hola de hello puerta de enlace de aplicaciones?**

Hola VIP puede cambiar si se detiene e inicia por el cliente de hello puerta de enlace de Hola. Hola DNS asociado con la puerta de enlace de aplicación no cambia con el ciclo de vida de Hola de puerta de enlace de Hola. Por esta razón, es recomendable toouse un alias CNAME y haga que señale toohello dirección DNS de hello Application Gateway.

**P. ¿Admite Application Gateway direcciones IP estáticas?**

No, Application Gateway no admite direcciones IP públicas estáticas, pero admite direcciones IP internas estáticas.

**P. ¿Puerta de enlace de aplicaciones admite varias direcciones IP públicas en puerta de enlace de hello?**

Solo se admite una dirección IP pública en una instancia de Application Gateway.

**P. ¿Admite Application Gateway encabezados x-forwarded-for?**

Sí, puerta de enlace de aplicación inserta x reenvían para, proto reenviados x, y puerto x reenviados encabezados de solicitud de hello reenvían toohello back-end. formato de Hello para el encabezado x-reenviados-para es una lista separada por comas de IP: Port. valores válidos de Hola para proto reenviados x son http o https. Puerto reenviados X especifica puerto hello en qué solicitud Hola alcanzada en hello Application Gateway.

**P. ¿Durante cuánto tiempo tarda toodeploy una puerta de enlace de la aplicación? ¿Sigue funcionando Application Gateway mientras se actualiza?**

Nuevas implementaciones de puerta de enlace de aplicaciones pueden tardar hasta too20 minutos tooprovision. Cambios tooinstance tamaño/recuento no son perjudiciales, y puerta de enlace de hello permanece activo durante este tiempo.

## <a name="configuration"></a>Configuración

**P. ¿Se implementa Application Gateway siempre en una red virtual?**

Sí, Application Gateway se implementa siempre en una red virtual. Esta subred solo puede contener instancias de Application Gateway.

**P. ¿Puede comunicarse Application Gateway tooinstances fuera de su red virtual?**

Puerta de enlace de aplicaciones puede comunicarse tooinstances fuera de la red virtual de Hola que resulta siempre que hay conectividad IP. Si tiene previsto toouse direcciones IP internas como miembros del grupo back-end, entonces se requiere [emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md) o [puerta de enlace VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).

**P. ¿Puedo implementar algo más en la subred de puerta de enlace de aplicación Hola?**

No, pero se pueden implementar otras puertas de enlace de aplicaciones en la subred de Hola.

**P. ¿Se admiten grupos de seguridad de red en la subred de puerta de enlace de aplicación Hola?**

Grupos de seguridad de red son compatibles en la subred de puerta de enlace de aplicación Hola con hello siguientes restricciones:

* Las excepciones deben situarse el tráfico entrante en los puertos 65503-65534 para toowork de mantenimiento de back-end correctamente.

* No puede bloquearse la conectividad saliente de Internet.

* Se debe permitir el tráfico de hello etiqueta AzureLoadBalancer.

**P. ¿Cuáles son los límites de hello en puerta de enlace de aplicaciones? ¿Puedo aumentar estos límites?**

Visite [límites de puerta de enlace de aplicaciones](../azure-subscription-service-limits.md#application-gateway-limits) tooview Hola límites.

**P. ¿Puedo usar Application Gateway para tráfico externo e interno al mismo tiempo?**

Sí, Application Gateway admite una dirección IP interna y una dirección IP externa por cada instancia de Application Gateway.

**P. ¿Se admite el emparejamiento de VNet?**

Sí, se admite el emparejamiento de VNet y, además, es beneficioso para el tráfico de equilibrio de carga en otras redes virtuales.

**P. ¿Se puede hablar servidores tooon locales cuando están conectados a través de túneles VPN o de ExpressRoute?**

Sí, siempre que se permita el tráfico.

**P. ¿Se puede tener un grupo de back-end que preste servicio a muchas aplicaciones en puertos diferentes?**

Se admite la arquitectura de microservicios. Debe generar varios tooprobe de configuración de http en puertos diferentes.

**P. ¿Admiten los sondeos personalizados caracteres comodín o regex en los datos de respuesta?**

Los sondeos personalizados no admiten caracteres comodín o regex en los datos de respuesta. 

**P. ¿Cómo se procesan las reglas?**

Las reglas se procesan en orden de hello que están configurados. Se recomienda que las reglas de varios sitios estén configuradas antes improbable de hello tooreduce de reglas básicas que tráfico enrutarse toohello inapropiados backend reglas básicas de hello coincidiría con tráfico basado en la regla de varios sitios de toohello anteriores de puerto que se va a evaluar.

**P. ¿Cómo se procesan las reglas?**

Las reglas se procesan en orden de Hola se crean. Se recomienda configurar las reglas multisitio antes que las reglas básicas. Al configurar los agentes de escucha de varios sitios en primer lugar, esta configuración reduce Hola posibilidad de que el tráfico enrutado toohello inapropiados backend. Este problema de enrutamiento puede producirse como reglas básicas de hello coincidiría con tráfico basado en la regla de varios sitios de toohello anteriores de puerto que se va a evaluar.

**P. ¿Qué significan el campo de Host de Hola para los sondeos personalizados?**

El campo host especifica Hola nombre toosend Hola sondeo. Solo se puede aplicar cuando se ha configurado un entorno multisitio en Application Gateway; de lo contrario hay que usar '127.0.0.1'. Este valor es diferente del nombre de host de máquina virtual y está en formato \<protocolo\>://\<host\>:\<puerto\>\<ruta de acceso\>.

**P. ¿Puede tooa de acceso de puerta de enlace de aplicación de lista blanca pocas direcciones IP de origen?**

Este escenario puede hacerse mediante el uso de grupos de seguridad de red en la subred de Application Gateway. Hola después restricciones debe colocarse en subred hello en hello aparecen orden de prioridad:

* Permitir el tráfico entrante de la IP o intervalo IP de origen.

* Permitir que las solicitudes entrantes de todos los orígenes tooports 65534 65503 para [comunicación de mantenimiento de back-end](application-gateway-diagnostics.md).

* Permitir entrantes sondeos del equilibrador de carga de Azure (etiqueta AzureLoadBalancer) y el tráfico de red virtual (etiqueta VirtualNetwork) entrante en hello [NSG](../virtual-network/virtual-networks-nsg.md).

* Bloquear todo el tráfico entrante restante con una regla Denegar todo.

* Permitir el tráfico saliente toohello internet para todos los destinos.

## <a name="performance"></a>Rendimiento

**P. ¿Cómo admite Application Gateway la alta disponibilidad y la escalabilidad?**

Application Gateway admite escenarios de alta disponibilidad cuando tiene dos o más instancias implementadas. Azure distribuye estas instancias a través de la actualización y error tooensure de dominios que no todas las instancias en hello mismo tiempo. Puerta de enlace de aplicación es compatible con la escalabilidad mediante la adición de varias instancias de hello misma carga de hello tooshare de puerta de enlace.

**P. ¿Cómo se puede lograr el escenario de recuperación ante desastres a través de centros de datos con Application Gateway?**

Los clientes pueden usar Traffic Manager toodistribute tráfico a través de varias puertas de enlace de aplicaciones en distintos centros de datos.

**P. ¿Se admite el escalado automático?**

No, pero la puerta de enlace de aplicaciones tiene una métrica de rendimiento que puede ser tooalert usado cuando se alcanza un umbral. Manualmente agregando instancias o cambiar el tamaño no se reinicie la puerta de enlace de hello y no afecta a tráfico existente.

**P. ¿Provoca el escalado o reducción vertical algún tiempo de inactividad?**

No hay ningún tiempo de inactividad, las instancias se distribuyen entre varios dominios de actualización y dominios de error.

**P. ¿Puedo cambiar tamaño de la instancia de Media toolarge sin interrupciones?**

Sí, Azure distribuye las instancias a través de la actualización y error tooensure de dominios que no todas las instancias en hello mismo tiempo. Aplicación puerta de enlace admite el escalado mediante la adición de varias instancias de Hola la misma carga de hello tooshare de puerta de enlace.

## <a name="ssl-configuration"></a>Configuración de SSL

**P. ¿Qué certificados se admiten en Application Gateway?**

Se admiten los certificados autofirmados, los certificados de entidad emisora de certificados y los certificados comodín. No se admiten los certificados de validación extendida (EV).

**P. ¿Cuáles son los conjuntos de cifrado actual Hola admitidos por la puerta de enlace de aplicaciones?**

los siguientes Hola son conjuntos de cifrado actual de hello admitidos por la puerta de enlace de aplicaciones. Visita: [configurar SSL versiones de directivas y conjuntos de cifrado en la puerta de enlace de aplicaciones](application-gateway-configure-ssl-policy-powershell.md) toolearn cómo toocustomize opciones de SSL.

- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

**P. ¿Puerta de enlace de aplicaciones también admite recifrado de back-end de tráfico toohello?**

Sí, descarga SSL de puerta de enlace de aplicaciones admite y end tooend SSL, que vuelve a cifra Hola tráfico toohello back-end.

**P. ¿Puedo configurar las versiones SSL directiva toocontrol protocolo SSL?**

Sí, puede configurar la puerta de enlace de aplicaciones toodeny TLS1.0, TLS1.1 y TLS1.2. SSL 2.0 y 3.0 ya están deshabilitados de forma predeterminada y no se pueden configurar.

**P. ¿Puedo configurar los conjuntos de cifrado y el orden de las directivas?**

Sí, se admite la [configuración de conjuntos de cifrado](application-gateway-ssl-policy-overview.md). Al definir una directiva personalizada, debe habilitarse al menos uno de los siguientes conjuntos de cifrado de Hola. Puerta de enlace de aplicación utiliza la administración de back-end de toofor SHA256.

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

**P. ¿Cuántos certificados SSL se admiten?**

Configurar SSL too20 se admiten certificados.

**P. ¿Cuántos certificados de autenticación de recifrado de back-end se admiten?**

Se admiten certificados de autenticación hasta too10 con un valor predeterminado es 5.

**P. ¿Se integra Application Gateway con Azure Key Vault de forma nativa?**

No, no se integra con Azure Key Vault.

## <a name="web-application-firewall-waf-configuration"></a>Firewall de aplicaciones web (WAF): Configuración

**P. ¿Hola WAFS SKU ofrece todas las características de hello disponibles con hello SKU estándar?**

Sí, WAFS admite todas las características de Hola Hola SKU estándar.

**P. ¿Qué es la versión CRS Hola que admite la puerta de enlace de aplicaciones?**

Application Gateway admite CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) y CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).

**P. ¿Cómo se supervisa el WAF?**

WAF se supervisa a través del registro de diagnóstico. Puede encontrar más información sobre el registro de diagnóstico en [Métricas y registro de diagnóstico de Application Gateway](application-gateway-diagnostics.md)

**P. ¿Bloquea el modo de detección el tráfico?**

No, el modo de detección solo registra el tráfico, que desencadenó una regla de WAF.

**P. ¿Cómo se personalizan las reglas de WAF?**

Sí, las reglas de WAFS son personalizables, para obtener más información sobre cómo toocustomize les visitan [reglas y grupos de reglas de personalizar WAFS](application-gateway-customize-waf-rules-portal.md)

**P. ¿Qué reglas están disponibles actualmente?**

WAFS actualmente admite CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) y [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), que proporcionan seguridad de línea de base en la mayoría de hello vulnerabilidades de 10 mejores identificadas por hello Abrir Web aplicación seguridad proyecto (OWASP) encontrar aquí [OWASP top 10 vulnerabilidades](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)

* Protección contra la inyección de código SQL

* Protección contra scripts entre sitios

* Protección contra ataques web comunes, como inyección de comandos, contrabando de solicitudes HTTP, división de respuestas HTTP y ataque remoto de inclusión de archivos

* Protección contra infracciones del protocolo HTTP

* Protección contra anomalías del protocolo HTTP, como la falta de agentes de usuario de host y encabezados de aceptación

* Prevención contra bots, rastreadores y escáneres

* Detección de errores de configuración comunes en aplicaciones (es decir, Apache, IIS, etc.)

**P. ¿Admite también WAF la prevención DDoS?**

No, WAF no ofrece prevención DDoS.

## <a name="diagnostics-and-logging"></a>Diagnósticos y registro

**P. ¿Qué tipos de registros están disponibles con Application Gateway?**

Hay tres registros disponibles para Application Gateway. Para más información sobre estos registros y otras funcionalidades de diagnóstico, visite [Mantenimiento del back-end, registro de diagnóstico y métricas de Application Gateway](application-gateway-diagnostics.md).

- **ApplicationGatewayAccessLog** -registro de acceso de hello contiene cada solicitud enviada front-end de toohello Application Gateway. datos de Hello incluyen IP del llamador Hola, dirección URL solicitada, latencia de la respuesta, devolver el código de bytes de entrada y salida. El registro de acceso se recopila cada 300 segundos. Este registro contiene un registro por cada instancia de Application Gateway.
- **ApplicationGatewayPerformanceLog** -registro de rendimiento de hello recopila información de rendimiento por instancia en incluida en solicitud total servirse, rendimiento, en bytes, número total de solicitudes servidas, recuento de solicitudes con error, positivos y negativo recuento de instancias de back-end.
- **ApplicationGatewayFirewallLog** -registro de firewall de hello contiene las solicitudes que se registran con el modo de detección o prevención de una puerta de enlace de la aplicación que está configurado con el servidor de aplicaciones web.

**P. ¿Cómo se puede saber si mis miembros del grupo de back-end están en buenas condiciones?**

Puede usar el cmdlet de PowerShell de hello `Get-AzureRmApplicationGatewayBackendHealth` o comprobar el estado a través del portal de hello visitando [diagnóstico de puerta de enlace de aplicaciones](application-gateway-diagnostics.md)

**P. ¿Qué es la directiva de retención de hello en los registros de diagnósticos de hello?**

Cuenta de almacenamiento de los clientes de toohello de flujo de registros de diagnóstico y los clientes pueden establecer Directiva de retención de hello en función de sus preferencias. También se pueden enviar registros de diagnóstico tooan concentrador de eventos o análisis de registros. Visite [Diagnósticos de Application Gateway](application-gateway-diagnostics.md) para más información.

**P. ¿Cómo se pueden obtener los registros de auditoría de Application Gateway?**

Los registros de auditoría están disponibles para Application Gateway. En el portal de hello, haga clic en **registro de actividad** en hoja del menú de Hola de un registro de auditoría de puerta de enlace de aplicaciones tooaccess Hola. 

**P. ¿Se pueden establecer alertas con Application Gateway?**

Sí, Application Gateway admite alertas, y estas se configuran a partir de las métricas.  Puerta de enlace de aplicaciones no tiene actualmente una métrica de "rendimiento", que puede ser tooalert configurado. toolearn más información acerca de las alertas, visite [recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

**P. El estado de back-end devuelve un estado desconocido, ¿que puede haberlo provocado?**

razón más común de Hello es está bloqueando el back-end de acceso toohello un NSG o DNS personalizado. Visite [back-end de estado, registro de diagnósticos y las métricas de puerta de enlace de aplicaciones](application-gateway-diagnostics.md) toolearn más.

## <a name="next-steps"></a>Pasos siguientes

toolearn sobre la puerta de enlace de aplicaciones, visite [Introducción tooApplication puerta de enlace](application-gateway-introduction.md).
