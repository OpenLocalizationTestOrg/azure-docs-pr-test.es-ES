---
title: "Preguntas más frecuentes de aplicación visión aaaAzure | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0e3b103c-6e2a-4634-9e8c-8b85cf5e9c84
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: e27ee9b7d040a04828a9892865a6681b83f94326
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-frequently-asked-questions"></a>Application Insights: peguntas más frecuentes

## <a name="configuration-problems"></a>Problemas de configuración
*Tengo problemas con la configuración de:*

* [Aplicación .NET](app-insights-asp-net-troubleshoot-no-data.md)
* [Supervisión de una aplicación que ya se está ejecutando](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)
* [Diagnóstico de Azure](app-insights-azure-diagnostics.md)
* [Aplicaciones web de Java](app-insights-java-troubleshoot.md)

*No recibo datos de mi servidor*

* [Establecer excepciones del firewall](app-insights-ip-addresses.md)
* [Configurar un servidor ASP.NET](app-insights-monitor-performance-live-website-now.md)
* [Configurar un servidor de Java](app-insights-java-agent.md)

## <a name="can-i-use-application-insights-with-"></a>¿Se puede usar Application Insights con...?

* [Aplicaciones web en un servidor de IIS: local o en una máquina virtual](app-insights-asp-net.md)
* [Aplicaciones web de Java](app-insights-java-get-started.md)
* [Aplicaciones de Node.js](app-insights-nodejs.md)
* [Aplicaciones web de Azure](app-insights-azure-web-apps.md)
* [Cloud Services en Azure](app-insights-cloudservices.md)
* [Servidores de aplicaciones que se ejecutan en Docker](app-insights-docker.md)
* [Aplicaciones web de una sola página](app-insights-javascript.md)
* [Sharepoint](app-insights-sharepoint.md)
* [Aplicación de escritorio de Windows](app-insights-windows-desktop.md)
* [Otras plataformas](app-insights-platforms.md)

## <a name="is-it-free"></a>¿Es gratis?

Sí, para su uso experimental. Hola básica de plan de precios, la aplicación puede enviar un determinado asignación de datos cada mes de forma gratuita. asignación libre de Hello sea lo suficientemente grande como toocover desarrollo y publicación de una aplicación para un número reducido de usuarios. Puede establecer un límite tooprevent más de una determinada cantidad de datos desde que se va a procesar.

Volúmenes más grandes de telemetría se cobran por hello Gb. Se proporcionan algunas sugerencias sobre cómo demasiado[limitar los cargos de](app-insights-pricing.md).

plan empresarial de Hello incurre en un cargo por cada día en que cada nodo del servidor web envía la telemetría. Es adecuado si desea toouse exportar continua a gran escala.

[Hola de lectura plan de precios](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="how-much-is-it-costing"></a>¿Cuánto costará?

* Abra hello **características + precios** página en un recurso de Application Insights. Hay un gráfico de uso reciente. Puede establecer un límite de volumen de datos, si quiere.
* Abra hello [hoja facturación de Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade/Overview) toosee sus facturas a través de todos los recursos.

## <a name="q14"></a>¿Qué modifica Application Insights en mi proyecto?
detalles de Hello dependen de tipo hello de proyecto. Para una aplicación web:

* Agrega un proyecto tooyour de estos archivos:

  * ApplicationInsights.config.
  * ai.js
* Instale estos paquetes de NuGet:

  * *API de visión de la aplicación* : hello principales de API
  * *API de visión de la aplicación para aplicaciones Web* -usa telemetría toosend desde servidor hello
  * *API de visión de la aplicación para aplicaciones de JavaScript* -usa toosend telemetría de cliente hello

    paquetes de saludo incluyen estos ensamblados:
  * Microsoft.ApplicationInsights
  * Microsoft.ApplicationInsights.Platform
* Inserta elementos en:

  * Web.config
  * packages.config
* (Nuevo solo - proyectos si se [Agregar proyecto existente de Application Insights tooan][start], tienes toodo esto manualmente.) Inserta tooinitialize de código de cliente y servidor hello en fragmentos de código con el identificador de recurso de Application Insights Hola. Por ejemplo, en una aplicación MVC, se inserta código en la página principal de hello Views/Shared/_Layout.cshtml

## <a name="how-do-i-upgrade-from-older-sdk-versions"></a>¿Cómo se puede actualizar desde versiones anteriores de SDK?
Vea hello [notas de la versión](app-insights-release-notes.md) para hello SDK adecuados tooyour tipo de aplicación.

## <a name="update"></a>¿Cómo puedo cambiar el recurso de Azure al que mi proyecto envía datos?
En el Explorador de soluciones, haga clic con el botón derecho en `ApplicationInsights.config` y elija **Actualizar Application Insights**. Puede enviar hello tooan existente o nuevo recurso de datos en Azure. cambios del Asistente para actualización Hola Hola clave de instrumentación en ApplicationInsights.config, que determina donde servidor hello SDK envía los datos. A menos que se anule la selección de "Actualizar todo", también cambiará clave Hola donde aparecerá en las páginas web.

## <a name="what-is-status-monitor"></a>¿Qué es el Monitor de estado?

Una aplicación de escritorio que puede usar en su toohelp de servidor web IIS configurar Application Insights en aplicaciones web. No recopila telemetría: puede detenerla cuando no vaya a configurar una aplicación. 

[Más información](app-insights-monitor-performance-live-website-now.md#questions).

## <a name="what-telemetry-is-collected-by-application-insights"></a>¿Qué telemetría recopila Application Insights?

De las aplicaciones web de servidor:

* Solicitudes HTTP
* [Dependencias](app-insights-asp-net-dependencies.md). Llamadas a: bases de datos SQL; HTTP llama a los servicios de tooexternal; Azure Cosmos DB, tabla, almacenamiento de blob y cola. 
* [Excepciones](app-insights-asp-net-exceptions.md) y seguimientos de pila.
* [Contadores de rendimiento](app-insights-performance-counters.md) : Si usas [Monitor de estado](app-insights-monitor-performance-live-website-now.md), Azure monitoring(app-insights-azure-web-apps.md) o hello [el sistema de escritura de Application Insights collectd](app-insights-java-collectd.md).
* [Eventos y métricas personalizados](app-insights-api-custom-events-metrics.md) que puede crear mediante código.
* [Los registros de seguimiento](app-insights-asp-net-trace-logs.md) si configura el selector de hello adecuado.

De las [páginas web de cliente](app-insights-javascript.md):

* [Recuentos de vistas de página](app-insights-web-track-usage.md)
* [Llamadas AJAX](app-insights-asp-net-dependencies.md): solicitudes realizadas desde un script en funcionamiento
* Datos de carga de vista de página
* Recuentos de usuarios y sesiones
* [Id. de usuario autenticados](app-insights-api-custom-events-metrics.md#authenticated-users).

De otros orígenes, si los configura:

* [Diagnóstico de Azure](app-insights-azure-diagnostics.md)
* [Contenedores de Docker](app-insights-docker.md)
* [Importación de tablas tooAnalytics](app-insights-analytics-import.md)
* [OMS (Log Analytics)](https://azure.microsoft.com/blog/omssolutionforappinsightspublicpreview/)
* [Logstash](app-insights-analytics-import.md)

## <a name="can-i-filter-out-or-modify-some-telemetry"></a>¿Puedo filtrar o modificar algunos datos de telemetría?

Sí, en el servidor de hello puede escribir:

* Telemetría procesador toofilter o agregar elementos de telemetría de propiedades tooselected antes de que se envíen desde su aplicación.
* Telemetría inicializador tooadd propiedades tooall elementos de telemetría.

Más información sobre [ASP.NET](app-insights-api-filtering-sampling.md) o [Java](app-insights-java-filter-telemetry.md).

## <a name="how-are-city-country-and-other-geo-location-data-calculated"></a>¿Cómo se calculan los datos de ciudad, país y otros datos de ubicación geográfica?

Adentrarnos Hola dirección IP (IPv4 o IPv6) del cliente de web de hello mediante [GeoLite2](http://dev.maxmind.com/geoip/geoip2/geolite2/).

* Telemetría de explorador: recopilamos dirección IP del remitente de Hola.
* Telemetría de servidor: módulo de Application Insights Hola recopila la dirección IP del cliente Hola. No se recopila si `X-Forwarded-For` está establecido.

Puede configurar hello `ClientIpHeaderTelemetryInitializer` dirección IP de hello tootake de un encabezado distinto. En algunos sistemas, por ejemplo, se mueve un servidor proxy, carga equilibrador o CDN demasiado`X-Originating-IP`. [Más información](http://apmtips.com/blog/2016/07/05/client-ip-address/).

También puede [usar Power BI](app-insights-export-power-bi.md) toodisplay la telemetría de solicitud en un mapa.


## <a name="data"></a>¿Cuánto tiempo se retienen los datos en el portal de hello? ¿Es seguro?
Eche un vistazo a [Privacidad y retención de los datos][data].

## <a name="might-personally-identifiable-information-pii-be-sent-in-hello-telemetry"></a>¿Personal información personal identificable (PII) se pueden enviar telemetría Hola?

Es posible si el código envía tales datos. También puede ocurrir si las variables de los seguimientos de pila incluyen PII. El equipo de desarrollo debe efectuar tooensure de evaluaciones de riesgo que PII se administra correctamente. [Más información sobre la retención y la privacidad de los datos](app-insights-data-retention-privacy.md).

último octeto de la dirección web de cliente de Hola de Hello siempre se establece too0 después de la ingesta de portal de Hola.

## <a name="my-ikey-is-visible-in-my-web-page-source"></a>Mi iKey es visible en el origen de mi página web. 

* Esta es una práctica común en las soluciones de supervisión.
* No puede ser usado toosteal los datos.
* Se podría ser utilizado tooskew las alertas de datos o un desencadenador.
* No hemos tenido noticias de que algún cliente haya tenido esos problemas.

Podría:

* Usar dos iKeys independientes (recursos independientes de Application Insights), para los datos de cliente y servidor. O
* Escribir a un proxy que se ejecuta en el servidor y tener el cliente web de hello enviar datos a través de ese proxy.

## <a name="post"></a>¿Cómo puedo ver datos POST en Búsqueda de diagnóstico?
Automáticamente no registramos datos POST, pero se puede utilizar una llamada TrackTrace: colocar datos de hello en el parámetro de mensaje de Hola. Esto tiene un límite de tamaño mayor que los límites de hello en las propiedades de cadena, aunque no se puede filtrar en él.

## <a name="should-i-use-single-or-multiple-application-insights-resources"></a>¿Debo usar uno o varios recursos de Application Insights?

Utilizar un único recurso de todos los componentes de Hola o de roles en un sistema de negocio individual. Use recursos independientes para las versiones de desarrollo, prueba y lanzamiento, y para aplicaciones independientes.

* [Vea la explicación de Hola](app-insights-separate-resources.md)
* [Ejemplo: servicio en la nube con roles web y de trabajo](app-insights-cloudservices.md)

## <a name="how-do-i-dynamically-change-hello-instrumentation-key"></a>¿Cómo se cambia de forma dinámica clave de instrumentación de hello?

* [La explicación aquí](app-insights-separate-resources.md)
* [Ejemplo: servicio en la nube con roles web y de trabajo](app-insights-cloudservices.md)

## <a name="what-are-hello-user-and-session-counts"></a>¿Qué usuario hello y sesión cuenta?

* Hola SDK de JavaScript establece una cookie de usuario en el cliente web de hello, tooidentify devuelve usuarios y las actividades una toogroup de cookie de sesión.
* Si hay un script de cliente, puede [establecer cookies en el servidor de hello](http://apmtips.com/blog/2016/07/09/tracking-users-in-api-apps/).
* Si un usuario real usa su sitio en exploradores diferentes o usa la exploración InPrivate o de incógnito, o distintas máquinas, entonces se contabilizará más de una vez.
* tooidentify un usuario ha iniciado la sesión a través de máquinas y exploradores, agregue una llamada demasiado[setAuthenticatedUserContect()](app-insights-api-custom-events-metrics.md#authenticated-users).

## <a name="q17"></a> ¿He habilitado todo en Application Insights?
| Qué debería ver | ¿Cómo tooget, | Razones para quererlo |
| --- | --- | --- |
| Gráficos de disponibilidad |[Pruebas web](app-insights-monitor-web-app-availability.md) |Saber que la aplicación web funciona |
| Rendimiento de la aplicación de servidor: tiempos de respuesta, etc. |[Agregar proyecto de Application Insights tooyour](app-insights-asp-net.md) o [instalar Monitor de estado de AI en servidor](app-insights-monitor-performance-live-website-now.md) (o escribir su propio código demasiado[realizar un seguimiento de dependencias](app-insights-api-custom-events-metrics.md#trackdependency)) |Detectar problemas de rendimiento |
| Telemetría de dependencia |[Instalar el Monitor de estado de Application Insights en el servidor](app-insights-monitor-performance-live-website-now.md) |Diagnosticar problemas con las bases de datos u otros componentes externos |
| Obtener seguimientos de pila de las excepciones |[Insertar llamadas TrackException en el código](app-insights-asp-net-exceptions.md) (aunque algunas se notifican automáticamente) |Detectar y diagnosticar excepciones |
| Buscar seguimientos del registro |[Agregar un adaptador de registro](app-insights-asp-net-trace-logs.md) |Diagnosticar excepciones, problemas de rendimiento |
| Aspectos básicos del uso de cliente: vistas de página, sesiones,... |[Inicializador de JavaScript en páginas web](app-insights-javascript.md) |Análisis de uso |
| Métricas personalizadas de cliente |[Seguimiento de llamadas en páginas web](app-insights-api-custom-events-metrics.md) |Mejorar la experiencia del usuario |
| Métricas personalizadas de servidor |[Seguimiento de llamadas en el código de servidor](app-insights-api-custom-events-metrics.md) |Business intelligence |

## <a name="why-are-hello-counts-in-search-and-metrics-charts-unequal"></a>¿Por qué Hola recuentos en los gráficos de búsqueda y las métricas de distintas?

[Muestreo](app-insights-sampling.md) reduce el número de Hola de elementos de telemetría (solicitudes, los eventos personalizados etc.) que realmente se envió desde el portal de toohello de aplicación. En la búsqueda, verá el número de Hola de elementos que se recibió realmente. En los gráficos de métricas que se muestran un recuento de eventos, verá el número de Hola de eventos originales que se ha producido. 

Cada elemento que se transmite lleva una propiedad `itemCount` que muestra cuántos elementos originales representa ese elemento. tooobserve de muestreo en la operación, puede ejecutar esta consulta en el análisis:

```
    requests | summarize original_events = sum(itemCount), transmitted_events = count()
```


## <a name="automation"></a>Automation

### <a name="configuring-application-insights"></a>Configuración de Application Insights

También puede [escribir scripts de PowerShell](app-insights-powershell.md) mediante el Monitor de recursos de Azure para:

* Crear y actualizar recursos de Application Insights
* Establecer plan de precios de Hola.
* Obtener clave de instrumentación de Hola.
* Agregar una alerta de métrica
* Agregar una prueba de disponibilidad.

No puede configurar un informe del Explorador de métricas ni configurar la exportación continua.

### <a name="querying-hello-telemetry"></a>Consultar la telemetría de Hola

Hola de uso [API de REST](https://dev.applicationinsights.io/) toorun [análisis](app-insights-analytics.md) consultas.

## <a name="how-can-i-set-an-alert-on-an-event"></a>¿Cómo puedo establecer una alerta sobre un evento?

Las alertas de Azure solo se establecen sobre métricas. Cree una métrica personalizada que cruce un umbral de valor cada vez que se produzca el evento. A continuación, establecer una alerta en la métrica de Hola. Tenga en cuenta que: recibirá una notificación cada vez que la métrica de hello cruza el umbral de Hola en cualquier dirección; no obtendrá una notificación hasta Hola cruce primero, con independencia de si el valor inicial de hello es alta o baja; siempre hay una latencia de unos minutos.

## <a name="are-there-data-transfer-charges-between-an-azure-web-app-and-application-insights"></a>¿Existen cargos por transferencia de datos entre una aplicación web de Azure y Application Insights?

* Si la aplicación web de Azure se hospeda en un centro de datos donde hay un punto de conexión de recopilación de Application Insights, no hay ningún cargo. 
* Si no hay ningún punto de conexión de recopilación en el centro de datos host, se le cobrarán los [cargos salientes de Azure](https://azure.microsoft.com/pricing/details/bandwidth/) de la telemetría de la aplicación.

Esto no depende de dónde se encuentre hospedado su recurso de Application Insights. Simplemente depende de distribución de Hola de nuestros puntos de conexión.

## <a name="can-i-send-telemetry-toohello-application-insights-portal"></a>¿Se pueden enviar portal de Application Insights de telemetría toohello?

Se recomienda usar nuestro SDK y usar hello API del SDK (app-insights-api-custom-events-metrics.md). Hay variantes de hello SDK para distintos [plataformas](app-insights-platforms.md). Estos SDK controlan el almacenamiento en búfer, la compresión, la limitación, los reintentos, etc. Sin embargo, Hola [esquema ingesta](https://github.com/Microsoft/ApplicationInsights-dotnet/tree/develop/Schema/PublicSchema) y [protocolo de extremo](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/ENDPOINT-PROTOCOL.md) son públicos.

## <a name="can-i-monitor-an-intranet-web-server"></a>¿Puedo supervisar un servidor web de una intranet?

Hay dos métodos:

### <a name="firewall-door"></a>Puerta de firewall

Permitir la web server toosend telemetría tooour extremos https://dc.services.visualstudio.com:443 y https://rt.services.visualstudio.com:443. 

### <a name="proxy"></a>Proxy

Enrutar el tráfico desde el servidor de puerta de enlace tooa en la intranet, por si se establece en ApplicationInsights.config:

```XML
<TelemetryChannel>
    <EndpointAddress>your gateway endpoint</EndpointAddress>
</TelemetryChannel>
```

La puerta de enlace debe enrutar Hola tráfico toohttps://dc.services.visualstudio.com:443/v2/pista

## <a name="can-i-run-availability-web-tests-on-an-intranet-server"></a>¿Puedo ejecutar pruebas web de disponibilidad en un servidor de intranet?

Nuestro [pruebas web](app-insights-monitor-web-app-availability.md) ejecutar en los puntos de presencia que están repartidos por todo el mundo Hola. Hay dos soluciones:

* Puerta de Firewall: permitir que las solicitudes de servidor tooyour de [agentes de prueba de hello larga y puede cambiar lista de web](app-insights-ip-addresses.md).
* Escribir su propio código toosend solicitudes periódicas tooyour servidor desde dentro de la intranet. Con este fin, puede ejecutar pruebas web de Visual Studio. evaluador de Hello podría enviar resultados Hola visión de tooApplication mediante hello TrackAvailability() API.

## <a name="more-answers"></a>Más respuestas
* [Foro de Application Insights](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

<!--Link references-->

[data]: app-insights-data-retention-privacy.md
[platforms]: app-insights-platforms.md
[start]: app-insights-overview.md
[windows]: app-insights-windows-get-started.md
