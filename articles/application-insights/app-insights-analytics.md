---
title: "Analytics: la eficaz herramienta de búsqueda de Azure Application Insights | Microsoft Docs"
description: "Información general de Analytics, la eficaz herramienta de búsqueda de Application Insights. "
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
ms.openlocfilehash: 8174745a00a107eea648b223a00466b6a7f37331
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="analytics-in-application-insights"></a><span data-ttu-id="a6d86-103">Analytics de Application Insights</span><span class="sxs-lookup"><span data-stu-id="a6d86-103">Analytics in Application Insights</span></span>
<span data-ttu-id="a6d86-104">[Analytics](app-insights-analytics.md) es la eficaz característica de búsqueda de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a6d86-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="a6d86-105">En estas páginas se describe el lenguaje de consulta de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a6d86-105">These pages describe the Log Analytics query language.</span></span> 

* <span data-ttu-id="a6d86-106">**[Vea el vídeo de introducción](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="a6d86-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="a6d86-107">**[Use una versión de prueba de Analytics en nuestros datos simulados](https://analytics.applicationinsights.io/demo)** si su aplicación aún no envía datos a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a6d86-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="a6d86-108">**[La hoja de referencia rápida de usuarios de SQL](https://aka.ms/sql-analytics)** traduce las expresiones más comunes.</span><span class="sxs-lookup"><span data-stu-id="a6d86-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>
* <span data-ttu-id="a6d86-109">**[Referencia de lenguaje](app-insights-analytics-reference.md)** Aprenda a utilizar las eficaces características del lenguaje de consulta de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a6d86-109">**[Language Reference](app-insights-analytics-reference.md)** Learn how to use all the powerful features of the Log Analytics query language.</span></span>


## <a name="queries-in-analytics"></a><span data-ttu-id="a6d86-110">Funciones de consultas de Analytics</span><span class="sxs-lookup"><span data-stu-id="a6d86-110">Queries in Analytics</span></span>
<span data-ttu-id="a6d86-111">Una consulta típica consta de una tabla de *origen* seguida de una serie de *operadores* separados por `|`.</span><span class="sxs-lookup"><span data-stu-id="a6d86-111">A typical query is a *source* table followed by a series of *operators* separated by `|`.</span></span> 

<span data-ttu-id="a6d86-112">Por ejemplo, vamos a averiguar a qué hora del día prueban los ciudadanos de Hyderabad nuestra aplicación web.</span><span class="sxs-lookup"><span data-stu-id="a6d86-112">For example, let's find out what time of day the citizens of Hyderabad try our web app.</span></span> <span data-ttu-id="a6d86-113">Y ya puestos, veamos qué códigos de resultados se devuelven a sus solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="a6d86-113">And while we're there, let's see what result codes are returned to their HTTP requests.</span></span> 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

<span data-ttu-id="a6d86-114">Contamos direcciones IP de cliente únicas agrupándolas por la hora del día durante los últimos 7 días.</span><span class="sxs-lookup"><span data-stu-id="a6d86-114">We count distinct client IP addresses, grouping them by the hour of the day over the past 7 days.</span></span> 

> [!NOTE]
> <span data-ttu-id="a6d86-115">Para obtener resultados más allá de las 24 horas anteriores, puede incluir explícitamente "timestamp" en la consulta, o bien usar el menú desplegable de intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="a6d86-115">To get results outside the previous 24h, either include 'timestamp' explicitly in your query, or use the time range drop-down menu.</span></span>
>

<span data-ttu-id="a6d86-116">Vamos a mostrar los resultados con la presentación de gráficos de barras y con la opción de apilar los resultados de distintos códigos de respuesta:</span><span class="sxs-lookup"><span data-stu-id="a6d86-116">Let's display the results with the bar chart presentation, choosing to stack the results from different response codes:</span></span>

![Elija el gráfico de barras, los ejes x e y, por último, la segmentación.](./media/app-insights-analytics/020.png)

<span data-ttu-id="a6d86-118">Parece que nuestra aplicación es más popular en Hyderabad a la hora del almuerzo y de acostarse.</span><span class="sxs-lookup"><span data-stu-id="a6d86-118">Looks like our app is most popular at lunchtime and bed-time in Hyderabad.</span></span> <span data-ttu-id="a6d86-119">(Y debemos investigar esos 500 códigos).</span><span class="sxs-lookup"><span data-stu-id="a6d86-119">(And we should investigate those 500 codes.)</span></span>

<span data-ttu-id="a6d86-120">También hay operaciones estadísticas potentes:</span><span class="sxs-lookup"><span data-stu-id="a6d86-120">There are also powerful statistical operations:</span></span>

![Resultados de consulta estadística](./media/app-insights-analytics/025.png)

<span data-ttu-id="a6d86-122">El lenguaje tiene muchas características atractivas:</span><span class="sxs-lookup"><span data-stu-id="a6d86-122">The language has many attractive features:</span></span>


* <span data-ttu-id="a6d86-123">[Filtre](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) la telemetría de la aplicación sin procesar por cualquier campo, incluidas sus métricas y propiedades personalizadas.</span><span class="sxs-lookup"><span data-stu-id="a6d86-123">[Filter](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) your raw app telemetry by any fields, including your custom properties and metrics.</span></span>
* <span data-ttu-id="a6d86-124">[Una](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) varias tablas: ponga en correlación las solicitudes con vistas de página, llamadas de dependencia, excepciones y seguimiento de registros.</span><span class="sxs-lookup"><span data-stu-id="a6d86-124">[Join](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) multiple tables – correlate requests with page views, dependency calls, exceptions and log traces.</span></span>
* <span data-ttu-id="a6d86-125">[Agregaciones](https://docs.loganalytics.io/learn/tutorials/aggregations.html)estadísticas de gran eficacia.</span><span class="sxs-lookup"><span data-stu-id="a6d86-125">Powerful statistical [aggregations](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>
* <span data-ttu-id="a6d86-126">Son tan eficaces como SQL, pero mucho más fáciles de usar para las consultas complejas: en lugar de anidar instrucciones, canaliza los datos de una operación básica a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="a6d86-126">Just as powerful as SQL, but much easier for complex queries: instead of nesting statements, you pipe the data from one elementary operation to the next.</span></span>
* <span data-ttu-id="a6d86-127">Visualizaciones inmediatas y potentes.</span><span class="sxs-lookup"><span data-stu-id="a6d86-127">Immediate and powerful visualizations.</span></span>
* <span data-ttu-id="a6d86-128">[Ancle gráficos a los paneles de Azure](app-insights-analytics-using.md#pin-to-dashboard).</span><span class="sxs-lookup"><span data-stu-id="a6d86-128">[Pin charts to Azure dashboards](app-insights-analytics-using.md#pin-to-dashboard).</span></span>
* <span data-ttu-id="a6d86-129">[Exporte consultas a Power BI](app-insights-analytics-using.md#export-to-power-bi).</span><span class="sxs-lookup"><span data-stu-id="a6d86-129">[Export queries to Power BI](app-insights-analytics-using.md#export-to-power-bi).</span></span>
* <span data-ttu-id="a6d86-130">Hay una [API de REST](https://dev.applicationinsights.io/) que puede usar para ejecutar consultas mediante programación, por ejemplo de Powershell.</span><span class="sxs-lookup"><span data-stu-id="a6d86-130">There's a [REST API](https://dev.applicationinsights.io/) that you can use to run queries programmatically, for example from Powershell.</span></span>


## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="a6d86-131">Conexión a los datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="a6d86-131">Connect to your Application Insights data</span></span>
<span data-ttu-id="a6d86-132">Abra Analytics desde la [hoja de información general](app-insights-dashboards.md) de su aplicación en Application Insights:</span><span class="sxs-lookup"><span data-stu-id="a6d86-132">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span> 

![Abra portal.azure.com, abra su recurso de Application Insights y haga clic en Análisis.](./media/app-insights-analytics/001.png)


## <a name="video"></a><span data-ttu-id="a6d86-134">Vídeo</span><span class="sxs-lookup"><span data-stu-id="a6d86-134">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a><span data-ttu-id="a6d86-135">Ejemplos de consultas</span><span class="sxs-lookup"><span data-stu-id="a6d86-135">Query examples</span></span>

<span data-ttu-id="a6d86-136">Pruebe estos tutoriales para ilustrar la eficacia del uso de Analytics:</span><span class="sxs-lookup"><span data-stu-id="a6d86-136">Try these walkthroughs to illustrate the power of using Analytics:</span></span>

 *  [<span data-ttu-id="a6d86-137">Diagnóstico automático de picos y saltos escalonados en duraciones de solicitudes</span><span class="sxs-lookup"><span data-stu-id="a6d86-137">Automatic diagnostics of spikes and step jumps in requests durations</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [<span data-ttu-id="a6d86-138">Análisis de las degradaciones de rendimiento con análisis de series temporales</span><span class="sxs-lookup"><span data-stu-id="a6d86-138">Analyzing performance degradations with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="a6d86-139">Análisis de los errores de aplicaciones con autocluster y diffpatterns</span><span class="sxs-lookup"><span data-stu-id="a6d86-139">Analyzing application failures with autocluster and diffpatterns</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [<span data-ttu-id="a6d86-140">Detecciones de formas avanzadas con análisis de series temporales</span><span class="sxs-lookup"><span data-stu-id="a6d86-140">Advanced shape detections with time series analysis</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [<span data-ttu-id="a6d86-141">Uso de operaciones de ventana deslizante para analizar el uso de aplicaciones (MAU/DAU acumulados, etc.)</span><span class="sxs-lookup"><span data-stu-id="a6d86-141">Using sliding window operations to analyze application usage (rolling MAU/DAU etc)</span></span>](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  <span data-ttu-id="a6d86-142">[Detección de interrupciones del servicio en función del análisis de registros de depuración](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) y la entrada de blog correspondiente [aquí](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics)</span><span class="sxs-lookup"><span data-stu-id="a6d86-142">[Detection of service disruptions based on analysis of debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) and a matching blog post [here](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).</span></span>
 *  <span data-ttu-id="a6d86-143">[Generación de perfiles de rendimiento de las aplicaciones mediante registros de depuración simples](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) y la entrada de blog correspondiente [aquí](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span><span class="sxs-lookup"><span data-stu-id="a6d86-143">[Profiling applications’ performance using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)</span></span>
 *  <span data-ttu-id="a6d86-144">[Medición de la duración de cada paso en el flujo de código mediante registros de depuración simples](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) y la entrada de blog correspondiente [aquí](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="a6d86-144">[Measuring the duration for each step in your code flow using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)</span></span>
 *  <span data-ttu-id="a6d86-145">[Análisis de la simultaneidad mediante registros de depuración simples](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) y la entrada de blog correspondiente [aquí](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span><span class="sxs-lookup"><span data-stu-id="a6d86-145">[Analyzing concurrency using simple debug logs](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) and a matching blog post [here](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)</span></span>



## <a name="next-steps"></a><span data-ttu-id="a6d86-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a6d86-146">Next steps</span></span>
* <span data-ttu-id="a6d86-147">Se recomienda empezar por el [paseo por el lenguaje](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="a6d86-147">We recommend you start with the [language tour](app-insights-analytics-tour.md).</span></span> 
* <span data-ttu-id="a6d86-148">Más información acerca del [uso de Analytics](app-insights-analytics-using.md).</span><span class="sxs-lookup"><span data-stu-id="a6d86-148">More about [using Analytics](app-insights-analytics-using.md).</span></span> 
* <span data-ttu-id="a6d86-149">[Referencia de lenguaje](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a6d86-149">[Language reference](app-insights-analytics-reference.md).</span></span> 
