---
title: "Modelo de datos de telemetría de aplicación visión aaaAzure | Documentos de Microsoft"
description: "Información general del modelo de datos de Application Insights"
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
ms.openlocfilehash: 5610519c3db8ec68d6cf787639204fb79724f511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-data-model"></a>Modelo de datos de telemetría de Application Insights

[Azure Application Insights](app-insights-overview.md) envía telemetría desde su toohello de aplicación web portal de Azure, por lo que puede analizar el rendimiento de Hola y el uso de la aplicación. modelo de telemetría de Hello está normalizado para que sea posible toocreate plataforma y supervisión independientes del lenguaje. 

Los datos recopilados por Application Insights modelan este patrón de ejecución de aplicaciones típico:

![Modelo de aplicación de Application Insights](./media/application-insights-data-model/application-insights-data-model.png)

Hello tipos de telemetría siguientes son utilizados toomonitor Hola ejecución de la aplicación. Hello tres tipos siguientes son normalmente recopila automáticamente Hola Application Insights SDK de marco de aplicación web de hello:

* [**Solicitud** ](application-insights-data-model-request-telemetry.md) -genera toolog una solicitud recibida por la aplicación. Por ejemplo, hello web Application Insights que SDK genera automáticamente un elemento de telemetría de solicitud para cada solicitud HTTP que recibe la aplicación web. 

    Un **operación** es Hola de subprocesos de ejecución que se procesa una solicitud. También puede [escribir código](app-insights-api-custom-events-metrics.md#trackrequest) toomonitor otros tipos de operación, como una "reactive" en un sitio web de trabajo o la función que periódicamente procesa los datos.  Cada operación tiene un identificador. Este identificador que puede ser utilizados too[group]((application-insights-correlation.md) telemetría todos los genera mientras la aplicación está procesando la solicitud de saludo. Cada operación se realiza correctamente o produce un error y tiene una duración de tiempo.
* [**Excepción** ](application-insights-data-model-exception-telemetry.md) -normalmente representa una excepción que hace que una operación toofail.
* [**Dependencia** ](application-insights-data-model-dependency-telemetry.md) -representa una llamada desde el servicio de aplicación tooan externo o almacenamiento como una API de REST o SQL. En ASP.NET, tooSQL de llamadas de dependencia se definen mediante `System.Data`. Llamadas tooHTTP extremos se definen mediante `System.Net`. 

Application Insights proporciona tres tipos de datos adicionales para telemetría personalizada:

* [Seguimiento](application-insights-data-model-trace-telemetry.md) : usar directamente o a través de un registro de diagnósticos de adaptador tooimplement mediante un marco de instrumentación que tooyou familiarizado, como `Log4Net` o `System.Diagnostics`.
* [Evento](application-insights-data-model-event-telemetry.md) -suelen usar toocapture interacción del usuario con el servicio, los patrones de uso de tooanalyze.
* [Métrica](application-insights-data-model-metric-telemetry.md) -usa tooreport mediciones escalar periódicas.

Cada elemento de telemetría puede definir hello [información de contexto](application-insights-data-model-context.md) como identificador de sesión de usuario o la versión de aplicación. El contexto es un conjunto de campos fuertemente tipados que desbloquean ciertos escenarios. Cuando la versión de la aplicación se haya inicializado correctamente, Application Insights puede detectar nuevos patrones de comportamiento de la aplicación correlacionados con la reimplementación. Id. de sesión puede ser usado toocalculate Hola interrupción o un problema de impacto en los usuarios. Calcular recuentos distintivos de valores de identificador de sesión para ciertos errores de dependencia, seguimientos de errores o excepciones críticas proporciona información valiosa sobre impactos.

Modelo de telemetría define una manera de Application Insights demasiado[correlacionar](application-insights-correlation.md) operación toohello de telemetría de los cuales es una parte. Por ejemplo, una solicitud puede realizar llamadas de SQL Database y registrar información de diagnóstico. Puede establecer contexto de correlación de Hola para esos elementos de telemetría que ocupan telemetría de solicitud toohello atrás.

## <a name="schema-improvements"></a>Mejoras de esquema

Modelo de datos de información de aplicación es un toomodel de manera sencilla y básicos pero eficaz la telemetría de aplicación. Se tookeep escenarios esenciales de hello modelo simple y delgado toosupport se esfuerzan por y permite el esquema de hello tooextend para uso avanzado.

problemas de esquema o modelo de datos de tooreport y sugerencias usan GitHub [ApplicationInsights principal](https://github.com/Microsoft/ApplicationInsights-Home/labels/schema) repositorio.

## <a name="next-steps"></a>Pasos siguientes

- [Escritura de telemetría personalizada](app-insights-api-custom-events-metrics.md)
- Obtenga información acerca de cómo demasiado[ampliar y filtrar telemetría](app-insights-api-filtering-sampling.md).
- Use [muestreo](app-insights-sampling.md) cantidad de toominimize de telemetría en función de modelo de datos.
- Consulte las [plataformas](app-insights-platforms.md) compatibles con Application Insights.
