---
title: "aaaAnalytics - Hola eficaz herramienta de búsqueda de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Información general de análisis de la herramienta de búsqueda eficaces de diagnóstico de Hola de Application Insights. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a>Analytics de Application Insights
[Análisis de](app-insights-analytics.md) es característica de búsqueda eficaces Hola de [Application Insights](app-insights-overview.md). En estas páginas se describe el lenguaje de consulta de Log Analytics. 

* **[Ver vídeo de introducción de hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Análisis de prueba con nuestros datos simulados](https://analytics.applicationinsights.io/demo)**  si la aplicación no envía datos tooApplication visión todavía.
* **[Hoja de referencia rápida de SQL-usuarios](https://aka.ms/sql-analytics)**  traduce giros de hello más comunes.
* **[Referencia del lenguaje](app-insights-analytics-reference.md)**  Obtenga información acerca de cómo toouse todos Hola eficaces características de lenguaje de consulta de análisis de registros de Hola.


## <a name="queries-in-analytics"></a>Funciones de consultas de Analytics
Una consulta típica consta de una tabla de *origen* seguida de una serie de *operadores* separados por `|`. 

Por ejemplo, vamos a averiguar en qué momento del ciudadanos de Hola de día de Hyderabad pruebe nuestra aplicación web. Y mientras se esté allí, veamos qué códigos de resultado se devuelven las solicitudes de tootheir HTTP. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

Contamos con direcciones IP de cliente distinto, agrupándolos según la hora de hello del día de hello sobre Hola últimos 7 días. 

> [!NOTE]
> resultados de tooget fuera Hola 24 horas anteriores, incluir 'timestamp' explícitamente en la consulta, o bien menú de lista desplegable de rango de tiempo de Hola.
>

Vamos a mostrar los resultados de hello con hello barra presentación de gráfico, si elige toostack Hola de códigos de respuesta diferentes:

![Elija el gráfico de barras, los ejes x e y, por último, la segmentación.](./media/app-insights-analytics/020.png)

Parece que nuestra aplicación es más popular en Hyderabad a la hora del almuerzo y de acostarse. (Y debemos investigar esos 500 códigos).

También hay operaciones estadísticas potentes:

![Resultados de consulta estadística](./media/app-insights-analytics/025.png)

lenguaje de Hello tiene muchas características atractivas:


* [Filtre](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) la telemetría de la aplicación sin procesar por cualquier campo, incluidas sus métricas y propiedades personalizadas.
* [Una](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) varias tablas: ponga en correlación las solicitudes con vistas de página, llamadas de dependencia, excepciones y seguimiento de registros.
* [Agregaciones](https://docs.loganalytics.io/learn/tutorials/aggregations.html)estadísticas de gran eficacia.
* Tan eficaces como SQL, pero es mucho más fácil para consultas complejas: en lugar de anidamiento de instrucciones, canalizar datos Hola de toohello de una operación elemental a continuación.
* Visualizaciones inmediatas y potentes.
* [Gráficos de PIN tooAzure paneles](app-insights-analytics-using.md#pin-to-dashboard).
* [Exportar consultas tooPower BI](app-insights-analytics-using.md#export-to-power-bi).
* Hay un [API de REST](https://dev.applicationinsights.io/) que puede usar las consultas de toorun mediante programación, por ejemplo de Powershell.


## <a name="connect-tooyour-application-insights-data"></a>Conexión de datos de Application Insights tooyour
Abra Analytics desde la [hoja de información general](app-insights-dashboards.md) de su aplicación en Application Insights: 

![Abra portal.azure.com, abra su recurso de Application Insights y haga clic en Análisis.](./media/app-insights-analytics/001.png)


## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>Ejemplos de consultas

Pruebe estos tutoriales tooillustrate Hola gran ventaja de usar análisis:

 *  [Diagnóstico automático de picos y saltos escalonados en duraciones de solicitudes](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [Análisis de las degradaciones de rendimiento con análisis de series temporales](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [Análisis de los errores de aplicaciones con autocluster y diffpatterns](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [Detecciones de formas avanzadas con análisis de series temporales](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [Usar deslizante ventana operaciones tooanalyze uso de la aplicación (lo que revertir MAU/DAU etcetera)](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [Detección de interrupciones del servicio en función del análisis de registros de depuración](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) y la entrada de blog correspondiente [aquí](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics)
 *  [Generación de perfiles de rendimiento de las aplicaciones mediante registros de depuración simples](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) y la entrada de blog correspondiente [aquí](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)
 *  [Medir la duración de Hola para cada paso en el flujo de código usando los registros de depuración simple](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) y una entrada de blog coincidente [aquí](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [Análisis de la simultaneidad mediante registros de depuración simples](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) y la entrada de blog correspondiente [aquí](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)



## <a name="next-steps"></a>Pasos siguientes
* Es recomendable que comience con hello [paseo por el lenguaje](app-insights-analytics-tour.md). 
* Más información acerca del [uso de Analytics](app-insights-analytics-using.md). 
* [Referencia de lenguaje](app-insights-analytics-reference.md). 
