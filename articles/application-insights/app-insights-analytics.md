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
# <a name="analytics-in-application-insights"></a><span data-ttu-id="1ce6b-103">Analytics de Application Insights</span><span class="sxs-lookup"><span data-stu-id="1ce6b-103">Analytics in Application Insights</span></span>
<span data-ttu-id="1ce6b-104">[Análisis de](app-insights-analytics.md) es característica de búsqueda eficaces Hola de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ce6b-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="1ce6b-105">En estas páginas se describe el lenguaje de consulta de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="1ce6b-106">**[Ver vídeo de introducción de hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="1ce6b-107">**[Análisis de prueba con nuestros datos simulados](https://analytics.applicationinsights.io/demo)**  si la aplicación no envía datos tooApplication visión todavía.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="1ce6b-108">**[Hoja de referencia rápida de SQL-usuarios](https://aka.ms/sql-analytics)**  traduce giros de hello más comunes.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>
* <span data-ttu-id="1ce6b-109">**[Referencia del lenguaje](app-insights-analytics-reference.md)**  Obtenga información acerca de cómo toouse todos Hola eficaces características de lenguaje de consulta de análisis de registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how toouse all hello powerful features of hello Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="1ce6b-110">Funciones de consultas de Analytics</span><span class="sxs-lookup"><span data-stu-id="1ce6b-110">Queries in Analytics</span></span>
<span data-ttu-id="1ce6b-111">Una consulta típica consta de una tabla de *origen* seguida de una serie de *operadores* separados por `|`.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="1ce6b-112">Por ejemplo, vamos a averiguar en qué momento del ciudadanos de Hola de día de Hyderabad pruebe nuestra aplicación web.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-112">For example, let's find out what time of day hello citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="1ce6b-113">Y mientras se esté allí, veamos qué códigos de resultado se devuelven las solicitudes de tootheir HTTP.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-113">And while we're there, let's see what result codes are returned tootheir HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="1ce6b-114">Contamos con direcciones IP de cliente distinto, agrupándolos según la hora de hello del día de hello sobre Hola últimos 7 días.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-114">We count distinct client IP addresses, grouping them by hello hour of hello day over hello past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="1ce6b-115">resultados de tooget fuera Hola 24 horas anteriores, incluir 'timestamp' explícitamente en la consulta, o bien menú de lista desplegable de rango de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-115">tooget results outside hello previous 24h, either include 'timestamp' explicitly in your query, or use hello time range drop-down menu.</span></span>
>

<span data-ttu-id="1ce6b-116">Vamos a mostrar los resultados de hello con hello barra presentación de gráfico, si elige toostack Hola de códigos de respuesta diferentes:</span><span class="sxs-lookup"><span data-stu-id="1ce6b-116">Let's display hello results with hello bar chart presentation, choosing toostack hello results from different response codes:</span></span>

![Elija el gráfico de barras, los ejes x e y, por último, la segmentación.](./media/app-insights-analytics/020.png)

<span data-ttu-id="1ce6b-118">Parece que nuestra aplicación es más popular en Hyderabad a la hora del almuerzo y de acostarse.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="1ce6b-119">(Y debemos investigar esos 500 códigos).</span><span class="sxs-lookup"><span data-stu-id="1ce6b-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="1ce6b-120">También hay operaciones estadísticas potentes:</span><span class="sxs-lookup"><span data-stu-id="1ce6b-120">There are also powerful statistical operations:</span></span>

![Resultados de consulta estadística](./media/app-insights-analytics/025.png)

<span data-ttu-id="1ce6b-122">lenguaje de Hello tiene muchas características atractivas:</span><span class="sxs-lookup"><span data-stu-id="1ce6b-122">hello language has many attractive features:</span></span>


* <span data-ttu-id="1ce6b-123">[Filtre](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) la telemetría de la aplicación sin procesar por cualquier campo, incluidas sus métricas y propiedades personalizadas.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="1ce6b-124">[Una](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) varias tablas: ponga en correlación las solicitudes con vistas de página, llamadas de dependencia, excepciones y seguimiento de registros.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="1ce6b-125">[Agregaciones](https://docs.loganalytics.io/learn/tutorials/aggregations.html)estadísticas de gran eficacia.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="1ce6b-126">Tan eficaces como SQL, pero es mucho más fácil para consultas complejas: en lugar de anidamiento de instrucciones, canalizar datos Hola de toohello de una operación elemental a continuación.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe hello data from one elementary operation toohello next.</span></span>
* <span data-ttu-id="1ce6b-127">Visualizaciones inmediatas y potentes.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="1ce6b-128">[Gráficos de PIN tooAzure paneles](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="1ce6b-128">[Pin charts tooAzure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="1ce6b-129">[Exportar consultas tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="1ce6b-129">[Export queries tooPower BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="1ce6b-130">Hay un [API de REST](https://dev.applicationinsights.io/) que puede usar las consultas de toorun mediante programación, por ejemplo de Powershell.</span><span class="sxs-lookup"><span data-stu-id="1ce6b-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use toorun queries programmatically, for example from Powershell.</span></span>


## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="1ce6b-131">Conexión de datos de Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="1ce6b-131">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="1ce6b-132">Abra Analytics desde la [hoja de información general](app-insights-dashboards.md) de su aplicación en Application Insights:</span><span class="sxs-lookup"><span data-stu-id="1ce6b-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Abra portal.azure.com, abra su recurso de Application Insights y haga clic en Análisis.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="1ce6b-134">Vídeo</span><span class="sxs-lookup"><span data-stu-id="1ce6b-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="1ce6b-135">Ejemplos de consultas</span><span class="sxs-lookup"><span data-stu-id="1ce6b-135">Query examples</span></span>

<span data-ttu-id="1ce6b-136">Pruebe estos tutoriales tooillustrate Hola gran ventaja de usar análisis:</span><span class="sxs-lookup"><span data-stu-id="1ce6b-136">Try these walkthroughs tooillustrate hello power of using Analytics:</span></span>

 *  [<span data-ttu-id="1ce6b-137">Diagnóstico automático de picos y saltos escalonados en duraciones de solicitudes</span><span class="sxs-lookup"><span data-stu-id="1ce6b-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="1ce6b-138">Análisis de las degradaciones de rendimiento con análisis de series temporales</span><span class="sxs-lookup"><span data-stu-id="1ce6b-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="1ce6b-139">Análisis de los errores de aplicaciones con autocluster y diffpatterns</span><span class="sxs-lookup"><span data-stu-id="1ce6b-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="1ce6b-140">Detecciones de formas avanzadas con análisis de series temporales</span><span class="sxs-lookup"><span data-stu-id="1ce6b-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="1ce6b-141">Usar deslizante ventana operaciones tooanalyze uso de la aplicación (lo que revertir MAU/DAU etcetera)</span><span class="sxs-lookup"><span data-stu-id="1ce6b-141">Using sliding window operations tooanalyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="1ce6b-142">[Detección de interrupciones del servicio en función del análisis de registros de depuración](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) y la entrada de blog correspondiente [aquí](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics)</span><span class="sxs-lookup"><span data-stu-id="1ce6b-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="1ce6b-143">[Generación de perfiles de rendimiento de las aplicaciones mediante registros de depuración simples](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) y la entrada de blog correspondiente [aquí](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="1ce6b-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="1ce6b-144">[Medir la duración de Hola para cada paso en el flujo de código usando los registros de depuración simple](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) y una entrada de blog coincidente [aquí](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="1ce6b-144">[Measuring hello duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="1ce6b-145">[Análisis de la simultaneidad mediante registros de depuración simples](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) y la entrada de blog correspondiente [aquí](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="1ce6b-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="1ce6b-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1ce6b-146">Next steps</span></span>
* <span data-ttu-id="1ce6b-147">Es recomendable que comience con hello [paseo por el lenguaje](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="1ce6b-147">We recommend you start with hello [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="1ce6b-148">Más información acerca del [uso de Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="1ce6b-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="1ce6b-149">[Referencia de lenguaje](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1ce6b-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
