---
title: "Uso de Analytics: la eficaz herramienta de búsqueda de Azure Application Insights | Microsoft Docs"
description: "Uso de Analytics, la eficaz herramienta de búsqueda de Application Insights. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9f7c1744db52b1c2f374fd5655e2c66b5f61bacf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="346e0-103">Uso de Analytics en Application Insights</span><span class="sxs-lookup"><span data-stu-id="346e0-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="346e0-104">[Analytics](app-insights-analytics.md) es la eficaz característica de búsqueda de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="346e0-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="346e0-105">En estas páginas se describe el lenguaje de consulta de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="346e0-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="346e0-106">**[Vea el vídeo de introducción](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="346e0-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="346e0-107">**[Use una versión de prueba de Analytics en nuestros datos simulados](https://analytics.applicationinsights.io/demo)** si su aplicación aún no envía datos a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="346e0-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="346e0-108">Apertura de Analytics</span><span class="sxs-lookup"><span data-stu-id="346e0-108">Open Analytics</span></span>
<span data-ttu-id="346e0-109">En el recurso de inicio de la aplicación de Application Insights, haga clic en Analytics.</span><span class="sxs-lookup"><span data-stu-id="346e0-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Abra portal.azure.com, abra su recurso de Application Insights y haga clic en Análisis.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="346e0-111">El tutorial en línea le proporciona algunas ideas sobre lo que puede hacer.</span><span class="sxs-lookup"><span data-stu-id="346e0-111">The inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="346e0-112">Puede encontrar un [paseo más amplio aquí](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="346e0-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="346e0-113">Consulta de la telemetría</span><span class="sxs-lookup"><span data-stu-id="346e0-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="346e0-114">Escriba una consulta.</span><span class="sxs-lookup"><span data-stu-id="346e0-114">Write a query</span></span>
![Pantalla del esquema](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="346e0-116">Comience con los nombres de cualquiera de las tablas que aparecen a la izquierda (o los operadores [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) o [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html)).</span><span class="sxs-lookup"><span data-stu-id="346e0-116">Begin with the names of any of the tables listed on the left (or the [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="346e0-117">Use `|` para crear una canalización de [operadores](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="346e0-117">Use `|` to create a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="346e0-118">IntelliSense le indicará tanto los operadores como los elementos de la expresión que se pueden utilizar.</span><span class="sxs-lookup"><span data-stu-id="346e0-118">IntelliSense prompts you with the operators and the expression elements that you can use.</span></span> <span data-ttu-id="346e0-119">Haga clic en el icono de información (o presione Ctrl+Espacio) para obtener una descripción más larga de cada elemento y ejemplos de cómo usarlos.</span><span class="sxs-lookup"><span data-stu-id="346e0-119">Click the information icon (or press CTRL+Space) to get a longer description and examples of how to use each element.</span></span>

<span data-ttu-id="346e0-120">Consulte [Un paseo por Analytics de Application Insights](app-insights-analytics-tour.md) y [Referencia para Analytics](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="346e0-120">See the [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="346e0-121">Ejecución de una consulta</span><span class="sxs-lookup"><span data-stu-id="346e0-121">Run a query</span></span>
![Ejecución de una consulta](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="346e0-123">Puede utilizar saltos de línea sencillos en las consultas.</span><span class="sxs-lookup"><span data-stu-id="346e0-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="346e0-124">Coloque el cursor dentro o al final de la consulta que desea ejecutar.</span><span class="sxs-lookup"><span data-stu-id="346e0-124">Put the cursor inside or at the end of the query you want to run.</span></span>
3. <span data-ttu-id="346e0-125">Compruebe el intervalo de tiempo de la consulta</span><span class="sxs-lookup"><span data-stu-id="346e0-125">Check the time range of your query.</span></span> <span data-ttu-id="346e0-126">(puede cambiarla o invalidarla; para ello, debe incluir su propia cláusula [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) en la consulta).</span><span class="sxs-lookup"><span data-stu-id="346e0-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="346e0-127">Haga clic en Ir para ejecutar la consulta.</span><span class="sxs-lookup"><span data-stu-id="346e0-127">Click Go to run the query.</span></span>
4. <span data-ttu-id="346e0-128">No ponga líneas en blanco en la consulta.</span><span class="sxs-lookup"><span data-stu-id="346e0-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="346e0-129">Puede mantener varias consultas separadas en una pestaña de consulta; para ello, sepárelas con líneas en blanco.</span><span class="sxs-lookup"><span data-stu-id="346e0-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="346e0-130">Se ejecuta solo la consulta que tiene el cursor.</span><span class="sxs-lookup"><span data-stu-id="346e0-130">Only the query that has the cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="346e0-131">Almacenamiento de una consulta</span><span class="sxs-lookup"><span data-stu-id="346e0-131">Save a query</span></span>
![Almacenamiento de una consulta](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="346e0-133">Guarde el archivo de consulta actual.</span><span class="sxs-lookup"><span data-stu-id="346e0-133">Save the current query file.</span></span>
2. <span data-ttu-id="346e0-134">Abra un archivo de consulta guardado.</span><span class="sxs-lookup"><span data-stu-id="346e0-134">Open a saved query file.</span></span>
3. <span data-ttu-id="346e0-135">Cree un archivo de consulta.</span><span class="sxs-lookup"><span data-stu-id="346e0-135">Create a new query file.</span></span>

## <a name="see-the-details"></a><span data-ttu-id="346e0-136">Visualización de los detalles</span><span class="sxs-lookup"><span data-stu-id="346e0-136">See the details</span></span>
<span data-ttu-id="346e0-137">Expanda cualquier fila de los resultados para ver la lista completa de sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="346e0-137">Expand any row in the results to see its complete list of properties.</span></span> <span data-ttu-id="346e0-138">Puede expandir más cualquier propiedad que tenga un valor estructurado: por ejemplo, las dimensiones personalizadas o la pila indicada en una excepción.</span><span class="sxs-lookup"><span data-stu-id="346e0-138">You can further expand any property that is a structured value - for example, custom dimensions, or the stack listing in an exception.</span></span>

![Expansión de una fila](./media/app-insights-analytics-using/070.png)

## <a name="arrange-the-results"></a><span data-ttu-id="346e0-140">Disposición de los resultados</span><span class="sxs-lookup"><span data-stu-id="346e0-140">Arrange the results</span></span>
<span data-ttu-id="346e0-141">Puede ordenar, filtrar, paginar y agrupar los resultados devueltos desde la consulta.</span><span class="sxs-lookup"><span data-stu-id="346e0-141">You can sort, filter, paginate, and group the results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="346e0-142">Ordenar, agrupar y filtrar en el explorador no vuelve a ejecutar la consulta.</span><span class="sxs-lookup"><span data-stu-id="346e0-142">Sorting, grouping, and filtering in the browser don't re-run your query.</span></span> <span data-ttu-id="346e0-143">Solo vuelve a ordenar los resultados devueltos por la última consulta.</span><span class="sxs-lookup"><span data-stu-id="346e0-143">They only rearrange the results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="346e0-144">Para realizar estas tareas en el servidor antes de que se devuelvan los resultados, escriba la consulta con los operadores [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) y [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html).</span><span class="sxs-lookup"><span data-stu-id="346e0-144">To perform these tasks in the server before the results are returned, write your query with the [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="346e0-145">Elija las columnas que desea ver, arrastre los encabezados de columna para reorganizarlos y cambie el tamaño de las columnas arrastrando sus bordes.</span><span class="sxs-lookup"><span data-stu-id="346e0-145">Pick the columns you'd like to see, drag column headers to rearrange them, and resize columns by dragging their borders.</span></span>

![Organización de columnas](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="346e0-147">Ordenación y filtrado de elementos</span><span class="sxs-lookup"><span data-stu-id="346e0-147">Sort and filter items</span></span>
<span data-ttu-id="346e0-148">Haga clic en el encabezado de una columna para ordenar los resultados.</span><span class="sxs-lookup"><span data-stu-id="346e0-148">Sort your results by clicking the head of a column.</span></span> <span data-ttu-id="346e0-149">Vuelva a hacer clic para ordenar de otra manera, y haga clic una tercera vez para volver a la ordenación original devuelta por la consulta.</span><span class="sxs-lookup"><span data-stu-id="346e0-149">Click again to sort the other way, and click a third time to revert to the original ordering returned by your query.</span></span>

<span data-ttu-id="346e0-150">Utilice el icono de filtro para restringir la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="346e0-150">Use the filter icon to narrow your search.</span></span>

![Ordenación y filtrado de columnas](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="346e0-152">Agrupación de elementos</span><span class="sxs-lookup"><span data-stu-id="346e0-152">Group items</span></span>
<span data-ttu-id="346e0-153">Para ordenar por más de una columna, use la agrupación.</span><span class="sxs-lookup"><span data-stu-id="346e0-153">To sort by more than one column, use grouping.</span></span> <span data-ttu-id="346e0-154">Primero, habilítela y, después, arrastre los encabezados de columna en el espacio por encima de la tabla.</span><span class="sxs-lookup"><span data-stu-id="346e0-154">First enable it, and then drag column headers into the space above the table.</span></span>

![Grupo](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="346e0-156">¿Faltan algunos resultados?</span><span class="sxs-lookup"><span data-stu-id="346e0-156">Missing some results?</span></span>

<span data-ttu-id="346e0-157">Si cree que no ve todos los resultados que esperaba, puede deberse a los motivos siguientes.</span><span class="sxs-lookup"><span data-stu-id="346e0-157">If you think you're not seeing all the results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="346e0-158">**Filtro de intervalo de tiempo**.</span><span class="sxs-lookup"><span data-stu-id="346e0-158">**Time range filter**.</span></span> <span data-ttu-id="346e0-159">De forma predeterminada, solo verá los resultados de las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="346e0-159">By default, you will only see results from the last 24 hours.</span></span> <span data-ttu-id="346e0-160">Hay un filtro automático que limita el intervalo de resultados que se recuperan de las tablas de origen.</span><span class="sxs-lookup"><span data-stu-id="346e0-160">There is an automatic filter that limits the range of results that are retrieved from the source tables.</span></span> 

    <span data-ttu-id="346e0-161">Sin embargo, dicho filtro se puede cambiar desde el menú desplegable.</span><span class="sxs-lookup"><span data-stu-id="346e0-161">However, you can change the time range filter by using the drop-down menu.</span></span>

    <span data-ttu-id="346e0-162">O bien, puede invalidar el intervalo automático mediante la inclusión de su propia [`where  ... timestamp ...` cláusula](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) en la consulta.</span><span class="sxs-lookup"><span data-stu-id="346e0-162">Or you can override the automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="346e0-163">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="346e0-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="346e0-164">**Límite de resultados**.</span><span class="sxs-lookup"><span data-stu-id="346e0-164">**Results limit**.</span></span> <span data-ttu-id="346e0-165">Hay un límite de 10 000 filas en los resultados devueltos desde el portal.</span><span class="sxs-lookup"><span data-stu-id="346e0-165">There's a limit of about 10k rows on the results returned from the portal.</span></span> <span data-ttu-id="346e0-166">Se muestra una advertencia si se sobrepasa el límite.</span><span class="sxs-lookup"><span data-stu-id="346e0-166">A warning shows if you go over the limit.</span></span> <span data-ttu-id="346e0-167">Si esto sucede, al ordenar los resultados de la tabla no siempre mostrará todos los resultados primeros o últimos reales.</span><span class="sxs-lookup"><span data-stu-id="346e0-167">If that happens, sorting your results in the table won't always show you all the actual first or last results.</span></span> 

    <span data-ttu-id="346e0-168">Es recomendable evitar llegar al límite.</span><span class="sxs-lookup"><span data-stu-id="346e0-168">It's good practice to avoid hitting the limit.</span></span> <span data-ttu-id="346e0-169">Utilice el filtro de intervalo de tiempo u operadores como:</span><span class="sxs-lookup"><span data-stu-id="346e0-169">Use the time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="346e0-170">top 100 by timestamp</span><span class="sxs-lookup"><span data-stu-id="346e0-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="346e0-171">take 100</span><span class="sxs-lookup"><span data-stu-id="346e0-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="346e0-172">summarize </span><span class="sxs-lookup"><span data-stu-id="346e0-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="346e0-173">where timestamp > ago(3d)</span><span class="sxs-lookup"><span data-stu-id="346e0-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="346e0-174">(¿Desea más de 10 000 filas?</span><span class="sxs-lookup"><span data-stu-id="346e0-174">(Want more than 10k rows?</span></span> <span data-ttu-id="346e0-175">Considere el uso de [Exportación continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="346e0-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="346e0-176">Analytics está diseñado para el análisis, no para la recuperación de datos sin procesar.)</span><span class="sxs-lookup"><span data-stu-id="346e0-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="346e0-177">Diagramas</span><span class="sxs-lookup"><span data-stu-id="346e0-177">Diagrams</span></span>
<span data-ttu-id="346e0-178">Seleccione el tipo de diagrama que desea:</span><span class="sxs-lookup"><span data-stu-id="346e0-178">Select the type of diagram you'd like:</span></span>

![Seleccione un tipo de diagrama](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="346e0-180">Si tiene varias columnas de los tipos correctos, puede elegir los ejes X e Y, así como una columna de dimensiones para dividir los resultados.</span><span class="sxs-lookup"><span data-stu-id="346e0-180">If you have several columns of the right types, you can choose the x and y axes, and a column of dimensions to split the results by.</span></span>

<span data-ttu-id="346e0-181">De manera predeterminada, los resultados se muestran en un principio en forma de tabla y el diagrama se selecciona manualmente.</span><span class="sxs-lookup"><span data-stu-id="346e0-181">By default, results are initially displayed as a table, and you select the diagram manually.</span></span> <span data-ttu-id="346e0-182">Sin embargo, para seleccionar un diagrama se puede usar la [directiva render](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) al final de una consulta.</span><span class="sxs-lookup"><span data-stu-id="346e0-182">But you can use the [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at the end of a query to select a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="346e0-183">Analytics Diagnostics</span><span class="sxs-lookup"><span data-stu-id="346e0-183">Analytics diagnostics</span></span>


<span data-ttu-id="346e0-184">En un gráfico de tiempo, si se produce un pico o salto repentino en los datos, es posible que vea un punto en la línea resaltado.</span><span class="sxs-lookup"><span data-stu-id="346e0-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on the line.</span></span> <span data-ttu-id="346e0-185">Esto indica que Analytics Diagnostics ha identificado una combinación de propiedades que filtran los cambios repentinos.</span><span class="sxs-lookup"><span data-stu-id="346e0-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out the sudden change.</span></span> <span data-ttu-id="346e0-186">Haga clic en el punto para obtener más detalles del filtro y para ver la versión filtrada.</span><span class="sxs-lookup"><span data-stu-id="346e0-186">Click the point to get more detail on the filter, and to see the filtered version.</span></span> <span data-ttu-id="346e0-187">Esto puede ayudar a identificar lo que ha causado el cambio.</span><span class="sxs-lookup"><span data-stu-id="346e0-187">This may help you identify what caused the change.</span></span> 

[<span data-ttu-id="346e0-188">Más información sobre Analytics Diagnostics</span><span class="sxs-lookup"><span data-stu-id="346e0-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Analytics Diagnostics](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-to-dashboard"></a><span data-ttu-id="346e0-190">Anclar al panel</span><span class="sxs-lookup"><span data-stu-id="346e0-190">Pin to dashboard</span></span>
<span data-ttu-id="346e0-191">Puede anclar un diagrama o una tabla a uno de sus [paneles compartidos](app-insights-dashboards.md) ; simplemente haga clic en la chincheta.</span><span class="sxs-lookup"><span data-stu-id="346e0-191">You can pin a diagram or table to one of your [shared dashboards](app-insights-dashboards.md) - just click the pin.</span></span> <span data-ttu-id="346e0-192">(Es posible que necesite [actualizar el paquete de precios de la aplicación](app-insights-pricing.md) para activar esta característica).</span><span class="sxs-lookup"><span data-stu-id="346e0-192">(You might need to [upgrade your app's pricing package](app-insights-pricing.md) to turn on this feature.)</span></span> 

![Haga clic en la chincheta](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="346e0-194">Esto significa que, cuando elabora un panel que le ayude a supervisar el rendimiento o el uso de los servicios web, puede incluir un análisis bastante complejo junto con las demás métricas.</span><span class="sxs-lookup"><span data-stu-id="346e0-194">This means that, when you put together a dashboard to help you monitor the performance or usage of your web services, you can include quite complex analysis alongside the other metrics.</span></span> 

<span data-ttu-id="346e0-195">Puede anclar una tabla al panel, si tiene cuatro o menos columnas.</span><span class="sxs-lookup"><span data-stu-id="346e0-195">You can pin a table to the dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="346e0-196">Se muestran solo las siete filas superiores.</span><span class="sxs-lookup"><span data-stu-id="346e0-196">Only the top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="346e0-197">Actualización del panel</span><span class="sxs-lookup"><span data-stu-id="346e0-197">Dashboard refresh</span></span>
<span data-ttu-id="346e0-198">El gráfico anclado al panel se actualiza automáticamente al volver a ejecutar la consulta aproximadamente cada dos horas.</span><span class="sxs-lookup"><span data-stu-id="346e0-198">The chart pinned to the dashboard is refreshed automatically by re-running the query approximately every hours.</span></span> <span data-ttu-id="346e0-199">También puede hacer clic en el botón Actualizar.</span><span class="sxs-lookup"><span data-stu-id="346e0-199">You can also click the Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="346e0-200">Simplificaciones automáticas</span><span class="sxs-lookup"><span data-stu-id="346e0-200">Automatic simplifications</span></span>

<span data-ttu-id="346e0-201">Determinadas simplificaciones se aplican a un gráfico cuando se ancla a un panel.</span><span class="sxs-lookup"><span data-stu-id="346e0-201">Certain simplifications are applied to a chart when you pin it to a dashboard.</span></span>

<span data-ttu-id="346e0-202">**Restricción de tiempo:** las consultas se limitan de manera automática a los últimos 14 días.</span><span class="sxs-lookup"><span data-stu-id="346e0-202">**Time restriction:** Queries are automatically limited to the past 14 days.</span></span> <span data-ttu-id="346e0-203">El efecto es el mismo que si la consulta incluye `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="346e0-203">The effect is the same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="346e0-204">**Restricción de recuento de intervalos:** si se muestra un gráfico que muestra muchos intervalos discretos (normalmente un gráfico de barras), los intervalos menos poblados se agrupan en un solo intervalo "otros".</span><span class="sxs-lookup"><span data-stu-id="346e0-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), the less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="346e0-205">Por ejemplo, esta consulta:</span><span class="sxs-lookup"><span data-stu-id="346e0-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="346e0-206">tiene esta apariencia en Analytics:</span><span class="sxs-lookup"><span data-stu-id="346e0-206">looks like this in Analytics:</span></span>

![Gráfico con cola larga](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="346e0-208">pero cuando se ancla a un panel, la siguiente apariencia:</span><span class="sxs-lookup"><span data-stu-id="346e0-208">but when you pin it to a dashboard, it looks like this:</span></span>

![Gráfico con intervalos limitados](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-to-excel"></a><span data-ttu-id="346e0-210">Exportación a Excel</span><span class="sxs-lookup"><span data-stu-id="346e0-210">Export to Excel</span></span>
<span data-ttu-id="346e0-211">Una vez que haya ejecutado una consulta, puede descargar un archivo .csv.</span><span class="sxs-lookup"><span data-stu-id="346e0-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="346e0-212">Haga clic en **Exportar, Excel**.</span><span class="sxs-lookup"><span data-stu-id="346e0-212">Click **Export,  Excel**.</span></span>

## <a name="export-to-power-bi"></a><span data-ttu-id="346e0-213">Exportación a Power BI</span><span class="sxs-lookup"><span data-stu-id="346e0-213">Export to Power BI</span></span>
<span data-ttu-id="346e0-214">Coloque el cursor en una consulta y elija **Exportar, Power BI**.</span><span class="sxs-lookup"><span data-stu-id="346e0-214">Put the cursor in a query and choose **Export, Power BI**.</span></span>

![Exportación de Analytics a Power BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="346e0-216">Ejecute la consulta en Power BI.</span><span class="sxs-lookup"><span data-stu-id="346e0-216">You run the query in Power BI.</span></span> <span data-ttu-id="346e0-217">Puede establecerla para que se actualice según una programación.</span><span class="sxs-lookup"><span data-stu-id="346e0-217">You can set it to refresh on a schedule.</span></span>

<span data-ttu-id="346e0-218">Con Power BI, puede crear paneles que reúnan datos de una gran variedad de orígenes.</span><span class="sxs-lookup"><span data-stu-id="346e0-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="346e0-219">Más información acerca de la exportación a Power BI</span><span class="sxs-lookup"><span data-stu-id="346e0-219">Learn more about export to Power BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="346e0-220">Vínculo profundo</span><span class="sxs-lookup"><span data-stu-id="346e0-220">Deep link</span></span>

<span data-ttu-id="346e0-221">Obtenga un vínculo en **Export, Share link** (Exportar, compartir vínculo) que puede enviar a otro usuario.</span><span class="sxs-lookup"><span data-stu-id="346e0-221">Get a link under **Export, Share link** that you can send to another user.</span></span> <span data-ttu-id="346e0-222">Siempre que el usuario tenga [acceso a su grupo de recursos](app-insights-resources-roles-access-control.md), la consulta se abrirá en la interfaz de usuario de Analytics.</span><span class="sxs-lookup"><span data-stu-id="346e0-222">Provided the user has [access to your resource group](app-insights-resources-roles-access-control.md), the query will open in the Analytics UI.</span></span>

<span data-ttu-id="346e0-223">(En el vínculo, aparece el texto de consulta después de "?q=", comprimido en gzip y codificado en base 64.</span><span class="sxs-lookup"><span data-stu-id="346e0-223">(In the link, the query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="346e0-224">Puede escribir código para generar vínculos profundos que se proporcionan a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="346e0-224">You could write code to generate deep links that you provide to users.</span></span> <span data-ttu-id="346e0-225">Sin embargo, el método recomendado para ejecutar Analytics desde código es mediante la [API de REST](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="346e0-225">However, the recommended way to run Analytics from code is by using the [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="346e0-226">Automatización</span><span class="sxs-lookup"><span data-stu-id="346e0-226">Automation</span></span>

<span data-ttu-id="346e0-227">Use la [API de REST de acceso a datos](https://dev.applicationinsights.io/) para ejecutar las consultas de Analytics.</span><span class="sxs-lookup"><span data-stu-id="346e0-227">Use the  [Data Access REST API](https://dev.applicationinsights.io/) to run Analytics queries.</span></span> <span data-ttu-id="346e0-228">[Por ejemplo](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (con PowerShell):</span><span class="sxs-lookup"><span data-stu-id="346e0-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="346e0-229">A diferencia de la interfaz de usuario de Analytics, la API de REST no agrega automáticamente ninguna limitación de marca de tiempo a las consultas.</span><span class="sxs-lookup"><span data-stu-id="346e0-229">Unlike the Analytics UI, the REST API does not automatically add any timestamp limitation to your queries.</span></span> <span data-ttu-id="346e0-230">No olvide agregar su propia cláusula de where para evitar la obtención de respuestas muy grandes.</span><span class="sxs-lookup"><span data-stu-id="346e0-230">Remember to add your own where-clause, to avoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="346e0-231">Importar datos</span><span class="sxs-lookup"><span data-stu-id="346e0-231">Import data</span></span>

<span data-ttu-id="346e0-232">Los datos se pueden importar desde un archivo CSV.</span><span class="sxs-lookup"><span data-stu-id="346e0-232">You can import data from a CSV file.</span></span> <span data-ttu-id="346e0-233">Un uso habitual consiste en importar datos estáticos que se pueden combinar con tablas de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="346e0-233">A typical usage is to import static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="346e0-234">Por ejemplo, si los usuarios autenticados se identifican en la telemetría mediante un alias o un identificador confuso, puede importar una tabla que asigne alias a los nombres reales.</span><span class="sxs-lookup"><span data-stu-id="346e0-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases to real names.</span></span> <span data-ttu-id="346e0-235">Si realiza una combinación en la telemetría de la solicitud, puede identificar a los usuarios por sus nombres reales en los informes de Analytics.</span><span class="sxs-lookup"><span data-stu-id="346e0-235">By performing a join on the request telemetry, you can identify users by their real names in the Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="346e0-236">Definición de un esquema de datos</span><span class="sxs-lookup"><span data-stu-id="346e0-236">Define your data schema</span></span>

1. <span data-ttu-id="346e0-237">Haga clic en **Configuración** (en la parte superior izquierda) y, luego, en **Orígenes de datos**.</span><span class="sxs-lookup"><span data-stu-id="346e0-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="346e0-238">Agregue un origen de datos siguiendo las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="346e0-238">Add a data source, following the instructions.</span></span> <span data-ttu-id="346e0-239">Se le solicita que proporcione una muestra de los datos, que se deben incluir al menos diez filas.</span><span class="sxs-lookup"><span data-stu-id="346e0-239">You are asked to supply a sample of the data, which should include at least ten rows.</span></span> <span data-ttu-id="346e0-240">A continuación, corrija el esquema.</span><span class="sxs-lookup"><span data-stu-id="346e0-240">You then correct the schema.</span></span>

<span data-ttu-id="346e0-241">Así se define un origen de datos, que, posteriormente, se puede usar para importar tablas individuales.</span><span class="sxs-lookup"><span data-stu-id="346e0-241">This defines a data source, which you can then use to import individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="346e0-242">Importación de una tabla</span><span class="sxs-lookup"><span data-stu-id="346e0-242">Import a table</span></span>

1. <span data-ttu-id="346e0-243">Abra la definición del origen de datos de la lista.</span><span class="sxs-lookup"><span data-stu-id="346e0-243">Open your data source definition from the list.</span></span>
2. <span data-ttu-id="346e0-244">Haga clic en "Cargar" y siga las instrucciones para cargar la tabla.</span><span class="sxs-lookup"><span data-stu-id="346e0-244">Click "Upload" and follow the instructions to upload the table.</span></span> <span data-ttu-id="346e0-245">Esto implica una llamada a una API de REST, por lo que es fácil de automatizar.</span><span class="sxs-lookup"><span data-stu-id="346e0-245">This involves a call to a REST API, and so it is easy to automate.</span></span> 

<span data-ttu-id="346e0-246">La tabla ya está disponible para usarla en las consultas de Analytics.</span><span class="sxs-lookup"><span data-stu-id="346e0-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="346e0-247">Aparecerá en Analytics</span><span class="sxs-lookup"><span data-stu-id="346e0-247">It will appear in Analytics</span></span> 

### <a name="use-the-table"></a><span data-ttu-id="346e0-248">Uso de la tabla</span><span class="sxs-lookup"><span data-stu-id="346e0-248">Use the table</span></span>

<span data-ttu-id="346e0-249">Supongamos que la definición del origen de datos se denomina `usermap` y que tiene dos campos, `realName` y `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="346e0-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="346e0-250">La tabla `requests` también tiene un campo denominado `user_AuthenticatedId`, por lo que resulta sencillo combinarlos:</span><span class="sxs-lookup"><span data-stu-id="346e0-250">The `requests` table also has a field named `user_AuthenticatedId`, so it's easy to join them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="346e0-251">La tabla de solicitudes resultante tiene una columna adicional, `realName`.</span><span class="sxs-lookup"><span data-stu-id="346e0-251">The resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="346e0-252">Importación desde LogStash</span><span class="sxs-lookup"><span data-stu-id="346e0-252">Import from LogStash</span></span>

<span data-ttu-id="346e0-253">Si usa [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), puede utilizar Analytics para consultar los registros.</span><span class="sxs-lookup"><span data-stu-id="346e0-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics to query your logs.</span></span> <span data-ttu-id="346e0-254">Use el [complemento que canaliza los datos a Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="346e0-254">Use the [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="346e0-255">Vídeo</span><span class="sxs-lookup"><span data-stu-id="346e0-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

