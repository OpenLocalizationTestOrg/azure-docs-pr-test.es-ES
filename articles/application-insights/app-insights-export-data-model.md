---
title: "aaaAzure modelo de datos de aplicación visión | Documentos de Microsoft"
description: "Describe las propiedades exportadas con la exportación continua de JSON y usadas como filtros."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a>Modelo de exportación de datos de Application Insights
Esta tabla enumeran las propiedades de Hola de telemetría enviados desde hello [Application Insights](app-insights-overview.md) SDK toohello portal.
Verá estas propiedades en el resultado de datos de [Exportación continua](app-insights-export-telemetry.md).
También aparecen en los filtros de propiedad de [Explorador de métricas](app-insights-metrics-explorer.md) y [Búsqueda de diagnóstico](app-insights-diagnostic-search.md).

Toonote puntos:

* `[0]`en estas tablas denota un punto en la ruta de acceso de Hola donde haya tooinsert un índice; pero no siempre es 0.
* Los períodos de tiempo se indican en décimas de microsegundo, así que 10000000 = 1 segundo.
* Las fechas y horas son del tipo UTC y se proporcionan en formato ISO de Hola`yyyy-MM-DDThh:mm:ss.sssZ`


## <a name="example"></a>Ejemplo
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  }

## <a name="context"></a>Context
Una sección de contexto acompaña a todos los tipos de telemetría. No todos estos campos se transmiten con cada punto de datos.

| Ruta de acceso | Tipo | Notas |
| --- | --- | --- |
| context.custom.dimensions [0] |objeto [ ] |Pares de cadenas de clave-valor establecidos por el parámetro de propiedades personalizadas. Longitud máxima de clave: 100, longitud máxima de valores: 1024. Más de 100 valores únicos, propiedad Hola se pueden buscar, pero no se puede usar para la segmentación. Máximo de 200 claves por ikey. |
| context.custom.metrics [0] |objeto [ ] |Los pares de clave-valor se establecen mediante el parámetro de medidas personalizado y mediante TrackMetrics. Longitud máxima de clave: 100, los valores pueden ser numéricos. |
| context.data.eventTime |cadena |UTC |
| context.data.isSynthetic |boolean |Solicitud aparece toocome de una prueba web o bot. |
| context.data.samplingRate |número |Porcentaje de telemetría generado por hello SDK que se envía tooportal. Intervalo 0,0 a 100,0. |
| context.device |objeto |Dispositivo de cliente |
| context.device.browser |cadena |IE, Chrome,… |
| context.device.browserVersion |cadena |Chrome 48.0,… |
| context.device.deviceModel |cadena | |
| context.device.deviceName |cadena | |
| context.device.id |cadena | |
| context.device.locale |cadena |en-GB, de-DE,… |
| context.device.network |cadena | |
| context.device.oemName |cadena | |
| context.device.osVersion |cadena |Sistema operativo del host |
| context.device.roleInstance |cadena |Identificador del host del servidor |
| context.device.roleName |cadena | |
| context.device.type |cadena |PC, explorador,… |
| context.location |objeto |Derivado de clientip. |
| context.location.city |cadena |Derivado de clientip, si se conoce. |
| context.location.clientip |cadena |Último octágono es too0 anonimizados. |
| context.location.continent |cadena | |
| context.location.country |cadena | |
| context.location.province |cadena |Estado o provincia |
| context.operation.id |cadena |Elementos que tienen el mismo Id. de operación se muestran como elementos relacionados en el portal de Hola de Hola. Normalmente Hola Id. de solicitud. |
| context.operation.name |cadena |Nombre de solicitud o dirección URL |
| context.operation.parentId |cadena |Permite elementos relacionados anidados. |
| context.session.id |cadena |Identificador de un grupo de operaciones de hello mismo origen. Un período de 30 minutos sin un final de Hola de señales de operación de una sesión. |
| context.session.isFirst |boolean | |
| context.user.accountAcquisitionDate |cadena | |
| context.user.anonAcquisitionDate |cadena | |
| context.user.anonId |cadena | |
| context.user.authAcquisitionDate |cadena |[Usuario autenticado](app-insights-api-custom-events-metrics.md#authenticated-users) |
| context.user.isAuthenticated |boolean | |
| internal.data.documentVersion |cadena | |
| internal.data.id |cadena | |

## <a name="events"></a>Eventos
Eventos personalizados generados por [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).

| Ruta de acceso | Tipo | Notas |
| --- | --- | --- |
| event [0] count |integer |100/(frecuencia de[muestreo](app-insights-sampling.md) ). Por ejemplo, 4 =&gt; 25 %. |
| event [0] name |cadena |Nombre del evento.  Longitud máxima: 250. |
| event [0] url |cadena | |
| event [0] urlData.base |cadena | |
| event [0] urlData.host |cadena | |

## <a name="exceptions"></a>Excepciones
Informes [excepciones](app-insights-asp-net-exceptions.md) en servidor hello y en el Explorador de Hola.

| Ruta de acceso | Tipo | Notas |
| --- | --- | --- |
| basicException [0] assembly |cadena | |
| basicException [0] count |integer |100/(frecuencia de[muestreo](app-insights-sampling.md) ). Por ejemplo, 4 =&gt; 25 %. |
| basicException [0] exceptionGroup |cadena | |
| basicException [0] exceptionType |string | |
| basicException [0] failedUserCodeMethod |cadena | |
| basicException [0] failedUserCodeAssembly |cadena | |
| basicException [0] handledAt |cadena | |
| basicException [0] hasFullStack |boolean | |
| basicException [0] id |cadena | |
| basicException [0] method |cadena | |
| basicException [0] message |cadena |Mensaje de excepción. Longitud máxima: 10 000. |
| basicException [0] outerExceptionMessage |cadena | |
| basicException [0] outerExceptionThrownAtAssembly |cadena | |
| basicException [0] outerExceptionThrownAtMethod |cadena | |
| basicException [0] outerExceptionType |cadena | |
| basicException [0] outerId |cadena | |
| basicException [0] parsedStack [0] assembly |cadena | |
| basicException [0] parsedStack [0] fileName |cadena | |
| basicException [0] parsedStack [0] level |integer | |
| basicException [0] parsedStack [0] line |integer | |
| basicException [0] parsedStack [0] method |cadena | |
| basicException [0] stack |cadena |Longitud máxima: 10 000. |
| basicException [0] typeName |cadena | |

## <a name="trace-messages"></a>Mensajes de seguimiento
Enviado por [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace)y por hello [registro adaptadores](app-insights-asp-net-trace-logs.md).

| Ruta de acceso | Tipo | Notas |
| --- | --- | --- |
| message [0] loggerName |cadena | |
| message [0] parameters |cadena | |
| message [0] raw |cadena |mensaje de registro de Hello, longitud máxima de 10k. |
| message [0] severityLevel |cadena | |

## <a name="remote-dependency"></a>Dependencia remota
Enviado por TrackDependency. Usar tooreport rendimiento y el uso de [llama toodependencies](app-insights-asp-net-dependencies.md) en servidor hello y llamadas de AJAX en el Explorador de Hola.

| Ruta de acceso | Tipo | Notas |
| --- | --- | --- |
| remoteDependency [0] async |boolean | |
| remoteDependency [0] baseName |cadena | |
| remoteDependency [0] commandName |cadena |Por ejemplo, "home/index". |
| remoteDependency [0] count |integer |100/(frecuencia de[muestreo](app-insights-sampling.md) ). Por ejemplo, 4 =&gt; 25 %. |
| remoteDependency [0] dependencyTypeName |cadena |HTTP, SQL... |
| remoteDependency [0] durationMetric.value |número |Tiempo de toocompletion de llamada de respuesta de dependencia |
| remoteDependency [0] id |cadena | |
| remoteDependency [0] name |string |URL Longitud máxima: 250. |
| remoteDependency [0] resultCode |cadena |de la dependencia de HTTP |
| remoteDependency [0] success |boolean | |
| remoteDependency [0] type |cadena |Http, Sql,... |
| remoteDependency [0] url |cadena |Longitud máxima: 2000 |
| remoteDependency [0] urlData.base |cadena |Longitud máxima: 2000 |
| remoteDependency [0] urlData.hashTag |cadena | |
| remoteDependency [0] urlData.host |cadena |Longitud máxima: 200 |

## <a name="requests"></a>Solicitudes
Enviado por [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest). módulos estándar de Hello usan este tiempo de respuesta del servidor tooreports, medido en el servidor de Hola.

| Ruta de acceso | Tipo | Notas |
| --- | --- | --- |
| request [0] count |integer |100/(frecuencia de[muestreo](app-insights-sampling.md) ). Por ejemplo: 4 =&gt; 25 %. |
| request [0] durationMetric.value |número |Tiempo de solicitud que llegan tarde tooresponse. 1e7 = 1 s |
| request [0] id |cadena |Identificador de operación |
| request [0] name |cadena |GET y POST + dirección url base.  Longitud máxima: 250 |
| request [0] responseCode |integer |Tooclient de respuesta enviado de HTTP |
| request [0] success |boolean |Predeterminado == (responseCode &lt; 400) |
| request [0] url |cadena |No incluye el host |
| request [0] urlData.base |cadena | |
| request [0] urlData.hashTag |cadena | |
| request [0] urlData.host |cadena | |

## <a name="page-view-performance"></a>Rendimiento de la vista de página
Explorador de hello envía. Medidas Hola tiempo tooprocess una página, de usuario iniciador Hola solicitud toodisplay completa (se excluyen las llamadas de AJAX asincrónicas).

Los valores de contexto muestran el sistema operativo del cliente y la versión del explorador.

| Ruta de acceso | Tipo | Notas |
| --- | --- | --- |
| clientPerformance [0] clientProcess.value |integer |Tiempo desde el final de la recepción de toodisplaying de la página de Hola Hola HTML. |
| clientPerformance [0] name |cadena | |
| clientPerformance [0] networkConnection.value |integer |Tooestablish de tiempo que tarda una conexión de red. |
| clientPerformance [0] receiveRequest.value |integer |Hora de fin de enviar hello tooreceiving de solicitud Hola HTML en la respuesta. |
| clientPerformance [0] sendRequest.value |integer |Tiempo de solicitud de hello HTTP toosend tomada. |
| clientPerformance [0] total.value |integer |Hora de toosend Hola solicitud toodisplaying Hola página de inicio. |
| clientPerformance [0] url |cadena |Dirección URL de esta solicitud |
| clientPerformance [0] urlData.base |cadena | |
| clientPerformance [0] urlData.hashTag |cadena | |
| clientPerformance [0] urlData.host |cadena | |
| clientPerformance [0] urlData.protocol |cadena | |

## <a name="page-views"></a>Vistas de página
Enviado por trackPageView() o [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)

| Ruta de acceso | Tipo | Notas |
| --- | --- | --- |
| view [0] count |integer |100/(frecuencia de[muestreo](app-insights-sampling.md) ). Por ejemplo, 4 =&gt; 25 %. |
| view [0] durationMetric.value |integer |Valor establecido opcionalmente en trackPageView() o mediante startTrackPage() - stopTrackPage(). No igual Hola como valores de clientPerformance. |
| view [0] name |cadena |Título de la página.  Longitud máxima: 250 |
| view [0] url |cadena | |
| view [0] urlData.base |cadena | |
| view [0] urlData.hashTag |cadena | |
| view [0] urlData.host |cadena | |

## <a name="availability"></a>Disponibilidad
Notifica sobre [pruebas web de disponibilidad](app-insights-monitor-web-app-availability.md).

| Ruta de acceso | Tipo | Notas |
| --- | --- | --- |
| availability [0] availabilityMetric.name |cadena |Disponibilidad |
| availability [0] availabilityMetric.value |número |1,0 o 0,0 |
| availability [0] count |integer |100/(frecuencia de[muestreo](app-insights-sampling.md) ). Por ejemplo, 4 =&gt; 25 %. |
| availability [0] dataSizeMetric.name |cadena | |
| availability [0] dataSizeMetric.value |integer | |
| availability [0] durationMetric.name |cadena | |
| availability [0] durationMetric.value |número |Duración de la prueba. 1e7 = 1 s |
| availability [0] message |cadena |Diagnóstico de errores |
| availability [0] result |cadena |Sin errores/Error |
| availability [0] runLocation |cadena |Origen geográfica de la solicitud http |
| availability [0] testName |cadena | |
| availability [0] testRunId |cadena | |
| availability [0] testTimestamp |cadena | |

## <a name="metrics"></a>Métricas
Generado por TrackMetric().

valor de métrica de Hola se encuentra en context.custom.metrics[0]

Por ejemplo:

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a>Acerca de los valores de métrica
Los valores de métrica, tanto en los informes de métrica como en otros lugares, se notifican con una estructura de objeto estándar. Por ejemplo:

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

Actualmente - aunque esto podría variar en hello futura - en todos los valores notificados de módulos SDK estándar hello, `count==1` y solo Hola `name` y `value` los campos son útiles. Hello único caso donde podría ser diferentes sería si escribir sus propias llamadas TrackMetric en que se establecen los Hola otros parámetros.

Hola propósito de hello otros campos es tooallow métricas toobe agregan Hola SDK, portal de tooreduce tráfico toohello. Por ejemplo, podría hacer el promedio de varias lecturas sucesivas antes de enviar cada informe métrica. A continuación, calcular Hola min, max, desviación estándar y un valor agregado (suma o promedio) y establecer toohello número de lecturas representado por informe de Hola.

En tablas de hello anteriores, omitimos Hola rara vez utilizadas campos count, min, max, stdDev y sampledValue.

En lugar de las métricas de la agregación previa, puede usar [muestreo](app-insights-sampling.md) si necesita el volumen de hello tooreduce de telemetría.

### <a name="durations"></a>Duraciones
Excepto donde se indique lo contrario, las duraciones se representan en décimas de microsegundo, por lo que 10000000,0 equivalen a 1 segundo.

## <a name="see-also"></a>Consulte también
* [Application Insights](app-insights-overview.md)
* [Exportación continua](app-insights-export-telemetry.md)
* [Ejemplos de código](app-insights-export-telemetry.md#code-samples)
