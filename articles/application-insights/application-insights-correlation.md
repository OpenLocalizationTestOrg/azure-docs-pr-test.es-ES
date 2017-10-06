---
title: "aaaAzure aplicación visión telemetría correlación | Documentos de Microsoft"
description: "Correlación de Telemetría de Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 3ed8c589d237cac5daceac939ca893b7d81a2967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>Correlación de Telemetría en Application Insights

En Hola a todos de micro servicios, cada operación lógica requiere trabajo realizado en los distintos componentes del servicio de Hola. Cada uno de estos componentes puede supervisarse por separado mediante [Application Insights](app-insights-overview.md). componente de aplicación de Hello web se comunica con credenciales de usuario de toovalidate de componente de proveedor de autenticación y con datos de tooget de componente de API de hello para la visualización. componente de API de Hola a su vez puede consultar los datos de otros servicios y utilizar los componentes de proveedor de caché y notificar al componente de facturación de hello sobre esta llamada. Application Insights admite la correlación de telemetría distribuida. Permite toodetect qué componente es responsable de errores o degradación del rendimiento.

Este artículo se explica el modelo de datos de hello utilizado por la telemetría de Application Insights toocorrelate enviados por varios componentes. Incluye técnicas de propagación de contexto de Hola y protocolos. También cubre la implementación de Hola de conceptos de correlación de hello en lenguajes diferentes y plataformas.

## <a name="telemetry-correlation-data-model"></a>Modelo de datos de correlación de telemetría

Application Insights define el [modelo de datos](application-insights-data-model.md) para la correlación de telemetría distribuida. telemetría tooassociate con operación lógica de hello, cada elemento de telemetría tiene un campo de contexto denominado `operation_Id`. Este identificador es compartido por todos los elementos telemetría en seguimiento de hello distribuida. De este modo, aun con la pérdida de telemetría de una sola capa, todavía puede asociar la telemetría notificada por otros componentes.

Operación lógica distribuida normalmente consta de un conjunto de operaciones más pequeñas - solicitudes procesadas por uno de los componentes de Hola. La [telemetría de solicitudes](application-insights-data-model-request-telemetry.md) define esas operaciones. Cada telemetría de solicitudes cuenta con su propio `id`, que la identifica global y exclusivamente. Y todos los telemetría - seguimientos, excepciones, etc. asociados a esta solicitud debe establecer hello `operation_parentId` toohello valor de solicitud de hello `id`.

Cada operación de salida como componente de http llamada tooanother representado por [telemetría dependencia](application-insights-data-model-dependency-telemetry.md). La telemetría de dependencia también define su propio `id`, que es globalmente único. La telemetría de solicitudes, iniciada por esta llamada de dependencia, la usa como `operation_parentId`.

Puede crear vista de Hola de operación lógica distribuida mediante `operation_Id`, `operation_parentId`, y `request.id` con `dependency.id`. Esos campos también definen el orden de causalidad de Hola de las llamadas de telemetría.

En el entorno de servicios micro, seguimientos de componentes pueden enviarse toohello diferentes almacenamientos. Cada componente puede tener su propia clave de instrumentación en Application Insights. tooget telemetría para la operación lógica de hello, deberá tooquery datos desde el almacenamiento de cada. Cuando el número de almacenamiento es muy grande, debe toohave una sugerencia sobre dónde toolook siguiente.

Application Insights modelo de datos define dos campos toosolve este problema: `request.source` y `dependency.target`. primer campo de Hello identifica el componente de Hola que inició la solicitud de la dependencia de Hola y hello en segundo lugar identifica qué componente devolvió una respuesta de llamada de la dependencia de Hola Hola.


## <a name="example"></a>Ejemplo

Veamos un ejemplo de una aplicación COTIZACIONES mostrando Hola precio actual de mercado de un material utilizando API externa Hola denominado API de COTIZACIONES. Hola aplicación COTIZACIONES tiene una página `Stock page` abre Hola cliente web explorador utilizando `GET /Home/Stock`. las consultas de aplicación Hola Hola existencias API con una llamada HTTP `GET /api/stock/value`.

Puede analizar la telemetría resultante mediante la ejecución de una consulta:

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

En la nota de la vista de resultado Hola que todos los elementos de telemetría compartan la raíz de hello `operation_Id`. Cuando llama ajax realizadas desde la página de hello - nuevo identificador único `qJSXU` es toohello asignado dependencia telemetría e Id. de la vista de página se utiliza como `operation_ParentId`. A su vez, la solicitud de servidor utiliza el id. de ajax como `operation_ParentId`, etc.

| itemType   | name                      | id           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| pageView   | Stock page                |              | STYz               | STYz         |
| dependency | GET /Home/Stock           | qJSXU        | STYz               | STYz         |
| request    | GET Home/Stock            | KqKwlrSt9PA= | qJSXU              | STYz         |
| dependency | GET /api/stock/value      | bBrf2L7mm2g= | KqKwlrSt9PA=       | STYz         |

Ahora cuando Hola llamada `GET /api/stock/value` realizados servicio externo tooan desea tooknow Hola identidad de ese servidor. De este modo, puede establecer el campo `dependency.target` adecuadamente. Cuando el servicio externo de hello no admite la supervisión - `target` se establece toohello el nombre de host de servicio de hello como `stock-prices-api.com`. Sin embargo si ese servicio se identifica a sí mismo devolviendo predefinido encabezado HTTP - `target` contiene la identidad de servicio de Hola que permite el seguimiento de toobuild distribuida Application Insights consultando la telemetría de dicho servicio. 

## <a name="correlation-headers"></a>Encabezados de correlación

Estamos trabajando en una propuesta de RFC para hello [correlación protocolo HTTP](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md). Esta propuesta define dos encabezados:

- `Request-Id`llevar el identificador único global de hello de la llamada de Hola
- `Correlation-Context`-llevar la colección de pares de valor de nombre de Hola de propiedades de la traza de hello distribuida

Hola estándar también define dos esquemas de `Request-Id` generación - jerárquico y plano. Con un esquema plano hello, hay un conocido `Id` clave definida para hello `Correlation-Context` colección.

Visión de la aplicación define hello [extensión](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md) para la correlación de hello protocolo HTTP. Usa `Request-Context` asignar nombre a pares de valor de colección de hello toopropagate de propiedades utilizados por el llamador inmediato de Hola o destinatario. Application Insights SDK utiliza este encabezado tooset `dependency.target` y `request.source` campos.

## <a name="open-tracing-and-application-insights"></a>Open Tracing y Application Insights

Aspecto de los modelos de datos de [Open Tracing](http://opentracing.io/) y Application Insights 

- `request`, `pageView` asigna demasiado**intervalo** con`span.kind = server`
- `dependency`se asigna demasiado**intervalo** con`span.kind = client`
- `id`de un `request` y `dependency` asigna demasiado**Span.Id**
- `operation_Id`se asigna demasiado**TraceId**
- `operation_ParentId`se asigna demasiado**referencia** de tipo`ChileOf`

Consulte [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.

Consulte [specification](https://github.com/opentracing/specification/blob/master/specification.md) (especificación) y [semantic_conventions](https://github.com/opentracing/specification/blob/master/semantic_conventions.md) (convenciones_semánticas) para obtener definiciones de los conceptos de Open Tracing.


## <a name="telemetry-correlation-in-net"></a>Correlación de telemetría en .NET

Con el tiempo .NET define el número de formas toocorrelate telemetría y diagnósticos registros. No hay `System.Diagnostics.CorrelationManager` permitir tootrack [LogicalOperationStack y ActivityId](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx). `System.Diagnostics.Tracing.EventSource`y Windows ETW definir método hello [SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx). `ILogger` usa [ámbitos de registro](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes). WCF y HTTP conectan la propagación del contexto "actual".

Sin embargo, esos métodos no han habilitado la compatibilidad con el seguimiento distribuido automático. `DiagnosticsSource`es un toosupport de forma automática entre la correlación de la máquina. Bibliotecas de .NET admiten el origen de diagnóstico y permiten la propagación automática entre equipos del contexto de la correlación de Hola a través de transporte de hello como http.

Hola [guía tooActivities](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) en origen de diagnóstico se explican conceptos básicos de Hola de seguimiento de actividades. 

Núcleo de ASP.NET 2.0 admite la extracción de encabezados Http y a partir de Hola nueva actividad. 

`System.Net.HttpClient`versión inicial `<fill in>` admite la inserción automática de correlación Hola encabezados Http y llamada de hello http como una actividad de seguimiento.

Hay un nuevo módulo Http [Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/) para hello clásico de ASP.NET. En este módulo se implementa la correlación de telemetría mediante DiagnosticsSource (Origen de diagnóstico). Inicia la actividad en función de los encabezados de solicitud entrantes.  También correlaciona telemetría de las distintas fases de Hola de procesamiento de la solicitud. Incluso en los casos Hola cada fase de procesamiento de IIS se ejecuta en los subprocesos de administrar distintos.

Versión inicial de aplicación visión SDK `2.4.0-beta1` usa telemetría toocollect DiagnosticsSource y la actividad y asociarla a la actividad actual de hello. 

## <a name="next-steps"></a>Pasos siguientes

- [Escritura de telemetría personalizada](app-insights-api-custom-events-metrics.md)
- Incorpore todos los componentes del microservicio en Application Insights. Consulte las [plataformas compatibles](app-insights-platforms.md).
- Consulte [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.
- Obtenga información acerca de cómo demasiado[ampliar y filtrar telemetría](app-insights-api-filtering-sampling.md).
