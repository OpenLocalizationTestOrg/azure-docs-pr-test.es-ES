---
title: "aaaUsing análisis - Hola eficaz herramienta de búsqueda de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Uso de hello análisis, herramienta de búsqueda eficaces de diagnóstico de Hola de Application Insights. "
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
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a><span data-ttu-id="75141-103">Uso de Analytics en Application Insights</span><span class="sxs-lookup"><span data-stu-id="75141-103">Using Analytics in Application Insights</span></span>
<span data-ttu-id="75141-104">[Análisis de](app-insights-analytics.md) es característica de búsqueda eficaces Hola de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="75141-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="75141-105">En estas páginas se describe el lenguaje de consulta de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="75141-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="75141-106">**[Ver vídeo de introducción de hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="75141-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="75141-107">**[Análisis de prueba con nuestros datos simulados](https://analytics.applicationinsights.io/demo)**  si la aplicación no envía datos tooApplication visión todavía.</span><span class="sxs-lookup"><span data-stu-id="75141-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>

## <a name="open-analytics"></a><span data-ttu-id="75141-108">Apertura de Analytics</span><span class="sxs-lookup"><span data-stu-id="75141-108">Open Analytics</span></span>
<span data-ttu-id="75141-109">En el recurso de inicio de la aplicación de Application Insights, haga clic en Analytics.</span><span class="sxs-lookup"><span data-stu-id="75141-109">From your app's home resource in Application Insights, click Analytics.</span></span>

![Abra portal.azure.com, abra su recurso de Application Insights y haga clic en Análisis.](./media/app-insights-analytics-using/001.png)

<span data-ttu-id="75141-111">tutorial de Hello en línea le ofrece algunas ideas sobre lo que puede hacer.</span><span class="sxs-lookup"><span data-stu-id="75141-111">hello inline tutorial gives you some ideas about what you can do.</span></span>

<span data-ttu-id="75141-112">Puede encontrar un [paseo más amplio aquí](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="75141-112">There's a [more extensive tour here](app-insights-analytics-tour.md).</span></span>

## <a name="query-your-telemetry"></a><span data-ttu-id="75141-113">Consulta de la telemetría</span><span class="sxs-lookup"><span data-stu-id="75141-113">Query your telemetry</span></span>
### <a name="write-a-query"></a><span data-ttu-id="75141-114">Escriba una consulta.</span><span class="sxs-lookup"><span data-stu-id="75141-114">Write a query</span></span>
![Pantalla del esquema](./media/app-insights-analytics-using/150.png)

<span data-ttu-id="75141-116">Comenzar con nombres Hola de cualquiera de las tablas de Hola que aparecen a la izquierda de hello (o hello [intervalo](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) o [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operadores).</span><span class="sxs-lookup"><span data-stu-id="75141-116">Begin with hello names of any of hello tables listed on hello left (or hello [range](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) or [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operators).</span></span> <span data-ttu-id="75141-117">Use `|` toocreate una canalización de [operadores](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span><span class="sxs-lookup"><span data-stu-id="75141-117">Use `|` toocreate a pipeline of [operators](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html).</span></span> 

<span data-ttu-id="75141-118">IntelliSense le indicará con operadores de Hola y elementos de la expresión de Hola que puede usar.</span><span class="sxs-lookup"><span data-stu-id="75141-118">IntelliSense prompts you with hello operators and hello expression elements that you can use.</span></span> <span data-ttu-id="75141-119">Haga clic en el icono de información de hello (o presione CTRL+BARRA ESPACIADORA) tooget una descripción más detallada y ejemplos de cómo toouse cada elemento.</span><span class="sxs-lookup"><span data-stu-id="75141-119">Click hello information icon (or press CTRL+Space) tooget a longer description and examples of how toouse each element.</span></span>

<span data-ttu-id="75141-120">Vea hello [paseo por el lenguaje análisis](app-insights-analytics-tour.md) y [referencia del lenguaje](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="75141-120">See hello [Analytics language tour](app-insights-analytics-tour.md) and [language reference](app-insights-analytics-reference.md).</span></span>

### <a name="run-a-query"></a><span data-ttu-id="75141-121">Ejecución de una consulta</span><span class="sxs-lookup"><span data-stu-id="75141-121">Run a query</span></span>
![Ejecución de una consulta](./media/app-insights-analytics-using/130.png)

1. <span data-ttu-id="75141-123">Puede utilizar saltos de línea sencillos en las consultas.</span><span class="sxs-lookup"><span data-stu-id="75141-123">You can use single line breaks in a query.</span></span>
2. <span data-ttu-id="75141-124">Coloque Hola cursor dentro o al final de Hola de consulta de Hola que desee toorun.</span><span class="sxs-lookup"><span data-stu-id="75141-124">Put hello cursor inside or at hello end of hello query you want toorun.</span></span>
3. <span data-ttu-id="75141-125">Compruebe el intervalo de tiempo de saludo de la consulta.</span><span class="sxs-lookup"><span data-stu-id="75141-125">Check hello time range of your query.</span></span> <span data-ttu-id="75141-126">(puede cambiarla o invalidarla; para ello, debe incluir su propia cláusula [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) en la consulta).</span><span class="sxs-lookup"><span data-stu-id="75141-126">(You can change it, or override it by including your own [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) clause in your query.)</span></span>
3. <span data-ttu-id="75141-127">Haga clic en la consulta de Go toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-127">Click Go toorun hello query.</span></span>
4. <span data-ttu-id="75141-128">No ponga líneas en blanco en la consulta.</span><span class="sxs-lookup"><span data-stu-id="75141-128">Don't put blank lines in your query.</span></span> <span data-ttu-id="75141-129">Puede mantener varias consultas separadas en una pestaña de consulta; para ello, sepárelas con líneas en blanco.</span><span class="sxs-lookup"><span data-stu-id="75141-129">You can keep several separated queries in one query tab by separating them with blank lines.</span></span> <span data-ttu-id="75141-130">Solo consulta Hola con cursor Hola se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="75141-130">Only hello query that has hello cursor runs.</span></span>

### <a name="save-a-query"></a><span data-ttu-id="75141-131">Almacenamiento de una consulta</span><span class="sxs-lookup"><span data-stu-id="75141-131">Save a query</span></span>
![Almacenamiento de una consulta](./media/app-insights-analytics-using/140.png)

1. <span data-ttu-id="75141-133">Guardar archivo de consulta actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-133">Save hello current query file.</span></span>
2. <span data-ttu-id="75141-134">Abra un archivo de consulta guardado.</span><span class="sxs-lookup"><span data-stu-id="75141-134">Open a saved query file.</span></span>
3. <span data-ttu-id="75141-135">Cree un archivo de consulta.</span><span class="sxs-lookup"><span data-stu-id="75141-135">Create a new query file.</span></span>

## <a name="see-hello-details"></a><span data-ttu-id="75141-136">Ver detalles de Hola</span><span class="sxs-lookup"><span data-stu-id="75141-136">See hello details</span></span>
<span data-ttu-id="75141-137">Expanda cualquier fila de hello resultados toosee su lista de propiedades completa.</span><span class="sxs-lookup"><span data-stu-id="75141-137">Expand any row in hello results toosee its complete list of properties.</span></span> <span data-ttu-id="75141-138">Se puede expandir cualquier propiedad que es un valor estructurado: por ejemplo, dimensiones personalizadas o pila Hola enumerar en una excepción.</span><span class="sxs-lookup"><span data-stu-id="75141-138">You can further expand any property that is a structured value - for example, custom dimensions, or hello stack listing in an exception.</span></span>

![Expansión de una fila](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a><span data-ttu-id="75141-140">Organizar resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="75141-140">Arrange hello results</span></span>
<span data-ttu-id="75141-141">Puede ordenar, filtrar, paginar y agrupar los resultados de hello devueltos por la consulta.</span><span class="sxs-lookup"><span data-stu-id="75141-141">You can sort, filter, paginate, and group hello results returned from your query.</span></span>

> [!NOTE]
> <span data-ttu-id="75141-142">Ordenar, agrupar y filtrar en el Explorador de hello vuelva a no ejecutan la consulta.</span><span class="sxs-lookup"><span data-stu-id="75141-142">Sorting, grouping, and filtering in hello browser don't re-run your query.</span></span> <span data-ttu-id="75141-143">Solo reorganizar los resultados de Hola que ha sido devuelto por la última consulta.</span><span class="sxs-lookup"><span data-stu-id="75141-143">They only rearrange hello results that were returned by your last query.</span></span> 
> 
> <span data-ttu-id="75141-144">tooperform estas tareas en el servidor hello antes de que se devuelven resultados de hello, escribir la consulta con hello [ordenación](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [resumir](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) y [donde](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operadores.</span><span class="sxs-lookup"><span data-stu-id="75141-144">tooperform these tasks in hello server before hello results are returned, write your query with hello [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) and [where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operators.</span></span>
> 
> 

<span data-ttu-id="75141-145">Elegir columnas de hello haría como toosee, arrastre y cambio de tamaño de columnas toorearrange de encabezados de columna arrastrando sus bordes.</span><span class="sxs-lookup"><span data-stu-id="75141-145">Pick hello columns you'd like toosee, drag column headers toorearrange them, and resize columns by dragging their borders.</span></span>

![Organización de columnas](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a><span data-ttu-id="75141-147">Ordenación y filtrado de elementos</span><span class="sxs-lookup"><span data-stu-id="75141-147">Sort and filter items</span></span>
<span data-ttu-id="75141-148">Ordenar los resultados, haga clic en el encabezado de Hola de una columna.</span><span class="sxs-lookup"><span data-stu-id="75141-148">Sort your results by clicking hello head of a column.</span></span> <span data-ttu-id="75141-149">Haga clic en nuevo toosort Hola otra manera, y haga clic en una tercera vez toorevert toohello ordenación original devuelto por la consulta.</span><span class="sxs-lookup"><span data-stu-id="75141-149">Click again toosort hello other way, and click a third time toorevert toohello original ordering returned by your query.</span></span>

<span data-ttu-id="75141-150">Utilice toonarrow de icono de filtro de hello en la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="75141-150">Use hello filter icon toonarrow your search.</span></span>

![Ordenación y filtrado de columnas](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a><span data-ttu-id="75141-152">Agrupación de elementos</span><span class="sxs-lookup"><span data-stu-id="75141-152">Group items</span></span>
<span data-ttu-id="75141-153">toosort por más de una columna, utilizan la agrupación.</span><span class="sxs-lookup"><span data-stu-id="75141-153">toosort by more than one column, use grouping.</span></span> <span data-ttu-id="75141-154">Primero habilite dicha opción y, a continuación, arrastre los encabezados de columna en el espacio de Hola por encima de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-154">First enable it, and then drag column headers into hello space above hello table.</span></span>

![Grupo](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a><span data-ttu-id="75141-156">¿Faltan algunos resultados?</span><span class="sxs-lookup"><span data-stu-id="75141-156">Missing some results?</span></span>

<span data-ttu-id="75141-157">Si cree que no puede ver todos los resultados de Hola que esperaba, hay un par de razones posibles.</span><span class="sxs-lookup"><span data-stu-id="75141-157">If you think you're not seeing all hello results you expected, there are a couple of possible reasons.</span></span>

* <span data-ttu-id="75141-158">**Filtro de intervalo de tiempo**.</span><span class="sxs-lookup"><span data-stu-id="75141-158">**Time range filter**.</span></span> <span data-ttu-id="75141-159">De forma predeterminada, solo verá los resultados de hello últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="75141-159">By default, you will only see results from hello last 24 hours.</span></span> <span data-ttu-id="75141-160">Hay un filtro automático que limita el intervalo de Hola de resultados que se recuperan de las tablas de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-160">There is an automatic filter that limits hello range of results that are retrieved from hello source tables.</span></span> 

    <span data-ttu-id="75141-161">Sin embargo, puede cambiar el intervalo de tiempo de hello el filtro con el menú desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-161">However, you can change hello time range filter by using hello drop-down menu.</span></span>

    <span data-ttu-id="75141-162">O puede invalidar el intervalo automático de hello mediante la inclusión de su propio [ `where  ... timestamp ...` cláusula](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) en la consulta.</span><span class="sxs-lookup"><span data-stu-id="75141-162">Or you can override hello automatic range by including your own [`where  ... timestamp ...` clause](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) into your query.</span></span> <span data-ttu-id="75141-163">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="75141-163">For example:</span></span>

    `requests | where timestamp > ago('2d')`

* <span data-ttu-id="75141-164">**Límite de resultados**.</span><span class="sxs-lookup"><span data-stu-id="75141-164">**Results limit**.</span></span> <span data-ttu-id="75141-165">Hay un límite de unos 10 filas k en resultados de hello devueltos desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-165">There's a limit of about 10k rows on hello results returned from hello portal.</span></span> <span data-ttu-id="75141-166">Se muestra una advertencia si sobrepasar el límite de Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-166">A warning shows if you go over hello limit.</span></span> <span data-ttu-id="75141-167">Si esto sucede, ordenar los resultados en la tabla de hello no siempre mostrarle todas Hola real primeros o últimos resultados.</span><span class="sxs-lookup"><span data-stu-id="75141-167">If that happens, sorting your results in hello table won't always show you all hello actual first or last results.</span></span> 

    <span data-ttu-id="75141-168">Es recomendable tooavoid posicionamiento Hola límite.</span><span class="sxs-lookup"><span data-stu-id="75141-168">It's good practice tooavoid hitting hello limit.</span></span> <span data-ttu-id="75141-169">Use el filtro de intervalo de tiempo de Hola o usar operadores como:</span><span class="sxs-lookup"><span data-stu-id="75141-169">Use hello time range filter, or use operators such as:</span></span>

  * [<span data-ttu-id="75141-170">top 100 by timestamp</span><span class="sxs-lookup"><span data-stu-id="75141-170">top 100 by timestamp</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [<span data-ttu-id="75141-171">take 100</span><span class="sxs-lookup"><span data-stu-id="75141-171">take 100</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [<span data-ttu-id="75141-172">summarize </span><span class="sxs-lookup"><span data-stu-id="75141-172">summarize </span></span>](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [<span data-ttu-id="75141-173">where timestamp &gt; ago(3d)</span><span class="sxs-lookup"><span data-stu-id="75141-173">where timestamp > ago(3d)</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

<span data-ttu-id="75141-174">(¿Desea más de 10 000 filas?</span><span class="sxs-lookup"><span data-stu-id="75141-174">(Want more than 10k rows?</span></span> <span data-ttu-id="75141-175">Considere el uso de [Exportación continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="75141-175">Consider using [Continuous Export](app-insights-export-telemetry.md) instead.</span></span> <span data-ttu-id="75141-176">Analytics está diseñado para el análisis, no para la recuperación de datos sin procesar.)</span><span class="sxs-lookup"><span data-stu-id="75141-176">Analytics is designed for analysis, rather than retrieving raw data.)</span></span>

## <a name="diagrams"></a><span data-ttu-id="75141-177">Diagramas</span><span class="sxs-lookup"><span data-stu-id="75141-177">Diagrams</span></span>
<span data-ttu-id="75141-178">Seleccione el tipo de Hola de diagrama que le gustaría:</span><span class="sxs-lookup"><span data-stu-id="75141-178">Select hello type of diagram you'd like:</span></span>

![Seleccione un tipo de diagrama](./media/app-insights-analytics-using/230.png)

<span data-ttu-id="75141-180">Si tiene varias columnas de tipos de derecho de hello, puede elegir Hola x y ejes y y una columna de resultados de hello toosplit de dimensiones por.</span><span class="sxs-lookup"><span data-stu-id="75141-180">If you have several columns of hello right types, you can choose hello x and y axes, and a column of dimensions toosplit hello results by.</span></span>

<span data-ttu-id="75141-181">De forma predeterminada, resultados se muestran inicialmente como una tabla y seleccione diagrama Hola manualmente.</span><span class="sxs-lookup"><span data-stu-id="75141-181">By default, results are initially displayed as a table, and you select hello diagram manually.</span></span> <span data-ttu-id="75141-182">Pero puede usar hello [representar directiva](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) final Hola de un tooselect consulta un diagrama.</span><span class="sxs-lookup"><span data-stu-id="75141-182">But you can use hello [render directive](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) at hello end of a query tooselect a diagram.</span></span>

### <a name="analytics-diagnostics"></a><span data-ttu-id="75141-183">Analytics Diagnostics</span><span class="sxs-lookup"><span data-stu-id="75141-183">Analytics diagnostics</span></span>


<span data-ttu-id="75141-184">En un timechart, si se produce un pico súbito o el paso de los datos, es posible que contenga un punto de resaltado en la línea de saludo.</span><span class="sxs-lookup"><span data-stu-id="75141-184">On a timechart, if there is a sudden spike or step in your data, you may see a highlighted point on hello line.</span></span> <span data-ttu-id="75141-185">Esto indica que diagnósticos de análisis se ha identificado una combinación de propiedades que filtrar los cambios repentinos Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-185">This indicates that Analytics Diagnostics has identified a combination of properties that filter out hello sudden change.</span></span> <span data-ttu-id="75141-186">Haga clic en hello punto tooget información más detallada acerca de filtro de Hola y versión filtrada de toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-186">Click hello point tooget more detail on hello filter, and toosee hello filtered version.</span></span> <span data-ttu-id="75141-187">Esto puede ayudar a identificar qué cambio Hola iniciadas.</span><span class="sxs-lookup"><span data-stu-id="75141-187">This may help you identify what caused hello change.</span></span> 

[<span data-ttu-id="75141-188">Más información sobre Analytics Diagnostics</span><span class="sxs-lookup"><span data-stu-id="75141-188">Learn more about Analytics Diagnostics</span></span>](app-insights-analytics-diagnostics.md)


![Analytics Diagnostics](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a><span data-ttu-id="75141-190">Toodashboard de PIN</span><span class="sxs-lookup"><span data-stu-id="75141-190">Pin toodashboard</span></span>
<span data-ttu-id="75141-191">Puede anclar un tooone diagrama o una tabla de la [compartido paneles](app-insights-dashboards.md) -simplemente haga clic en Anclar Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-191">You can pin a diagram or table tooone of your [shared dashboards](app-insights-dashboards.md) - just click hello pin.</span></span> <span data-ttu-id="75141-192">(Puede que tenga demasiado[actualización de paquete de precios de la aplicación](app-insights-pricing.md) tooturn acerca de esta característica.)</span><span class="sxs-lookup"><span data-stu-id="75141-192">(You might need too[upgrade your app's pricing package](app-insights-pricing.md) tooturn on this feature.)</span></span> 

![Haga clic en Anclar Hola](./media/app-insights-analytics-using/pin-01.png)

<span data-ttu-id="75141-194">Esto significa que, al reunir un toohelp panel supervisar el rendimiento de Hola o el uso de los servicios web, puede incluir un análisis bastante complejo junto con hello otras métricas.</span><span class="sxs-lookup"><span data-stu-id="75141-194">This means that, when you put together a dashboard toohelp you monitor hello performance or usage of your web services, you can include quite complex analysis alongside hello other metrics.</span></span> 

<span data-ttu-id="75141-195">Puede anclar un panel de toohello tabla, si tiene cuatro o menos columnas.</span><span class="sxs-lookup"><span data-stu-id="75141-195">You can pin a table toohello dashboard, if it has four or fewer columns.</span></span> <span data-ttu-id="75141-196">Se muestran solo Hola siete filas superiores.</span><span class="sxs-lookup"><span data-stu-id="75141-196">Only hello top seven rows are displayed.</span></span>

### <a name="dashboard-refresh"></a><span data-ttu-id="75141-197">Actualización del panel</span><span class="sxs-lookup"><span data-stu-id="75141-197">Dashboard refresh</span></span>
<span data-ttu-id="75141-198">Hola gráfico anclado toohello panel se actualiza automáticamente volviendo a ejecutar consulta Hola cada horas aproximadamente.</span><span class="sxs-lookup"><span data-stu-id="75141-198">hello chart pinned toohello dashboard is refreshed automatically by re-running hello query approximately every hours.</span></span> <span data-ttu-id="75141-199">También puede hacer clic en botón de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-199">You can also click hello Refresh button.</span></span>

### <a name="automatic-simplifications"></a><span data-ttu-id="75141-200">Simplificaciones automáticas</span><span class="sxs-lookup"><span data-stu-id="75141-200">Automatic simplifications</span></span>

<span data-ttu-id="75141-201">Ciertas medidas de simplificación son gráfico tooa aplicada al anclar el panel de tooa.</span><span class="sxs-lookup"><span data-stu-id="75141-201">Certain simplifications are applied tooa chart when you pin it tooa dashboard.</span></span>

<span data-ttu-id="75141-202">**Restricción de tiempo:** las consultas son toohello limitan de manera automática últimos 14 días.</span><span class="sxs-lookup"><span data-stu-id="75141-202">**Time restriction:** Queries are automatically limited toohello past 14 days.</span></span> <span data-ttu-id="75141-203">Hello efecto es Hola igual que si la consulta incluye `where timestamp > ago(14d)`.</span><span class="sxs-lookup"><span data-stu-id="75141-203">hello effect is hello same as if your query includes `where timestamp > ago(14d)`.</span></span>

<span data-ttu-id="75141-204">**Restricción de recuento de ubicación:** si se muestra un gráfico que tiene muchas ubicaciones discretas (normalmente en un gráfico de barras), Hola menos bins rellenadas automáticamente se agrupan en un único "otros" bin.</span><span class="sxs-lookup"><span data-stu-id="75141-204">**Bin count restriction:** If you display a chart that has a lot of discrete bins (typically a bar chart), hello less populated bins are automatically grouped into a single "others" bin.</span></span> <span data-ttu-id="75141-205">Por ejemplo, esta consulta:</span><span class="sxs-lookup"><span data-stu-id="75141-205">For example, this query:</span></span>

    requests | summarize count_search = count() by client_CountryOrRegion

<span data-ttu-id="75141-206">tiene esta apariencia en Analytics:</span><span class="sxs-lookup"><span data-stu-id="75141-206">looks like this in Analytics:</span></span>

![Gráfico con cola larga](./media/app-insights-analytics-using/pin-07.png)

<span data-ttu-id="75141-208">pero, al anclar el panel de tooa, el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="75141-208">but when you pin it tooa dashboard, it looks like this:</span></span>

![Gráfico con intervalos limitados](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a><span data-ttu-id="75141-210">Exportar tooExcel</span><span class="sxs-lookup"><span data-stu-id="75141-210">Export tooExcel</span></span>
<span data-ttu-id="75141-211">Una vez que haya ejecutado una consulta, puede descargar un archivo .csv.</span><span class="sxs-lookup"><span data-stu-id="75141-211">After you've run a query, you can download a .csv file.</span></span> <span data-ttu-id="75141-212">Haga clic en **Exportar, Excel**.</span><span class="sxs-lookup"><span data-stu-id="75141-212">Click **Export,  Excel**.</span></span>

## <a name="export-toopower-bi"></a><span data-ttu-id="75141-213">Exportar tooPower BI</span><span class="sxs-lookup"><span data-stu-id="75141-213">Export tooPower BI</span></span>
<span data-ttu-id="75141-214">Coloque el cursor de hello en una consulta y elija **exportar, Power BI**.</span><span class="sxs-lookup"><span data-stu-id="75141-214">Put hello cursor in a query and choose **Export, Power BI**.</span></span>

![Exportar desde análisis tooPower BI](./media/app-insights-analytics-using/240.png)

<span data-ttu-id="75141-216">Ejecutar consulta de hello en Power BI.</span><span class="sxs-lookup"><span data-stu-id="75141-216">You run hello query in Power BI.</span></span> <span data-ttu-id="75141-217">Puede establecerlo toorefresh según una programación.</span><span class="sxs-lookup"><span data-stu-id="75141-217">You can set it toorefresh on a schedule.</span></span>

<span data-ttu-id="75141-218">Con Power BI, puede crear paneles que reúnan datos de una gran variedad de orígenes.</span><span class="sxs-lookup"><span data-stu-id="75141-218">With Power BI, you can create dashboards that bring together data from a wide variety of sources.</span></span>

[<span data-ttu-id="75141-219">Obtener más información sobre la exportación tooPower BI</span><span class="sxs-lookup"><span data-stu-id="75141-219">Learn more about export tooPower BI</span></span>](app-insights-export-power-bi.md)

## <a name="deep-link"></a><span data-ttu-id="75141-220">Vínculo profundo</span><span class="sxs-lookup"><span data-stu-id="75141-220">Deep link</span></span>

<span data-ttu-id="75141-221">Obtener un vínculo bajo **exportación, el vínculo compartido** que se puede enviar al usuario tooanother.</span><span class="sxs-lookup"><span data-stu-id="75141-221">Get a link under **Export, Share link** that you can send tooanother user.</span></span> <span data-ttu-id="75141-222">Proporcionado por el usuario de hello tiene [grupo de recursos de acceso tooyour](app-insights-resources-roles-access-control.md), consulta Hola se abrirá en hello análisis de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="75141-222">Provided hello user has [access tooyour resource group](app-insights-resources-roles-access-control.md), hello query will open in hello Analytics UI.</span></span>

<span data-ttu-id="75141-223">(En el vínculo de hello, texto de consulta de hello aparece después de "? q =", comprimido gzip y codificado en base 64.</span><span class="sxs-lookup"><span data-stu-id="75141-223">(In hello link, hello query text appears after "?q=", gzip compressed and base-64 encoded.</span></span> <span data-ttu-id="75141-224">Si escribes vínculos profundos de código toogenerate que proporcione toousers.</span><span class="sxs-lookup"><span data-stu-id="75141-224">You could write code toogenerate deep links that you provide toousers.</span></span> <span data-ttu-id="75141-225">Sin embargo, Hola recomienda forma toorun análisis de código es usar hello [API de REST](https://dev.applicationinsights.io/).)</span><span class="sxs-lookup"><span data-stu-id="75141-225">However, hello recommended way toorun Analytics from code is by using hello [REST API](https://dev.applicationinsights.io/).)</span></span>


## <a name="automation"></a><span data-ttu-id="75141-226">Automation</span><span class="sxs-lookup"><span data-stu-id="75141-226">Automation</span></span>

<span data-ttu-id="75141-227">Hola de uso [API de REST de acceso a datos](https://dev.applicationinsights.io/) toorun consultas de análisis.</span><span class="sxs-lookup"><span data-stu-id="75141-227">Use hello  [Data Access REST API](https://dev.applicationinsights.io/) toorun Analytics queries.</span></span> <span data-ttu-id="75141-228">[Por ejemplo](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (con PowerShell):</span><span class="sxs-lookup"><span data-stu-id="75141-228">[For example](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (using PowerShell):</span></span>

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

<span data-ttu-id="75141-229">A diferencia de hello interfaz de usuario de análisis, Hola API de REST no agrega automáticamente las consultas de tooyour de limitación de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="75141-229">Unlike hello Analytics UI, hello REST API does not automatically add any timestamp limitation tooyour queries.</span></span> <span data-ttu-id="75141-230">Recuerde tooadd su propia cláusula where, tooavoid obtener las respuestas muy grandes.</span><span class="sxs-lookup"><span data-stu-id="75141-230">Remember tooadd your own where-clause, tooavoid getting huge responses.</span></span>



## <a name="import-data"></a><span data-ttu-id="75141-231">Importar datos</span><span class="sxs-lookup"><span data-stu-id="75141-231">Import data</span></span>

<span data-ttu-id="75141-232">Los datos se pueden importar desde un archivo CSV.</span><span class="sxs-lookup"><span data-stu-id="75141-232">You can import data from a CSV file.</span></span> <span data-ttu-id="75141-233">Un uso típico es tooimport datos estáticos que se pueden afiliar con tablas de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="75141-233">A typical usage is tooimport static data that you can join with tables from your telemetry.</span></span> 

<span data-ttu-id="75141-234">Por ejemplo, si los usuarios autenticados se identifican en la telemetría mediante un alias o un identificador confuso, puede importar una tabla que asigna nombres de alias tooreal.</span><span class="sxs-lookup"><span data-stu-id="75141-234">For example, if authenticated users are identified in your telemetry by an alias or obfuscated id, you could import a table that maps aliases tooreal names.</span></span> <span data-ttu-id="75141-235">Al realizar una combinación de telemetría de solicitud de hello, puede identificar a los usuarios por sus nombres en los informes de análisis de hello reales.</span><span class="sxs-lookup"><span data-stu-id="75141-235">By performing a join on hello request telemetry, you can identify users by their real names in hello Analytics reports.</span></span>

### <a name="define-your-data-schema"></a><span data-ttu-id="75141-236">Definición de un esquema de datos</span><span class="sxs-lookup"><span data-stu-id="75141-236">Define your data schema</span></span>

1. <span data-ttu-id="75141-237">Haga clic en **Configuración** (en la parte superior izquierda) y, luego, en **Orígenes de datos**.</span><span class="sxs-lookup"><span data-stu-id="75141-237">Click **Settings** (at top left) and then **Data Sources**.</span></span> 
2. <span data-ttu-id="75141-238">Agregar un origen de datos, siga las instrucciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-238">Add a data source, following hello instructions.</span></span> <span data-ttu-id="75141-239">Es más frecuentes toosupply una muestra de datos de hello, que deben incluir al menos diez filas.</span><span class="sxs-lookup"><span data-stu-id="75141-239">You are asked toosupply a sample of hello data, which should include at least ten rows.</span></span> <span data-ttu-id="75141-240">A continuación, corrija el esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-240">You then correct hello schema.</span></span>

<span data-ttu-id="75141-241">Esto define un origen de datos, a continuación, puede utilizar tablas individuales tooimport.</span><span class="sxs-lookup"><span data-stu-id="75141-241">This defines a data source, which you can then use tooimport individual tables.</span></span>

### <a name="import-a-table"></a><span data-ttu-id="75141-242">Importación de una tabla</span><span class="sxs-lookup"><span data-stu-id="75141-242">Import a table</span></span>

1. <span data-ttu-id="75141-243">Abra la definición de origen de datos de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-243">Open your data source definition from hello list.</span></span>
2. <span data-ttu-id="75141-244">Haga clic en "Cargar" y siga la tabla de hello instrucciones tooupload Hola.</span><span class="sxs-lookup"><span data-stu-id="75141-244">Click "Upload" and follow hello instructions tooupload hello table.</span></span> <span data-ttu-id="75141-245">Esto implica un tooa llamada API de REST y, por lo que resulta fácil tooautomate.</span><span class="sxs-lookup"><span data-stu-id="75141-245">This involves a call tooa REST API, and so it is easy tooautomate.</span></span> 

<span data-ttu-id="75141-246">La tabla ya está disponible para usarla en las consultas de Analytics.</span><span class="sxs-lookup"><span data-stu-id="75141-246">Your table is now available for use in Analytics queries.</span></span> <span data-ttu-id="75141-247">Aparecerá en Analytics</span><span class="sxs-lookup"><span data-stu-id="75141-247">It will appear in Analytics</span></span> 

### <a name="use-hello-table"></a><span data-ttu-id="75141-248">Utilice tabla Hola</span><span class="sxs-lookup"><span data-stu-id="75141-248">Use hello table</span></span>

<span data-ttu-id="75141-249">Supongamos que la definición del origen de datos se denomina `usermap` y que tiene dos campos, `realName` y `user_AuthenticatedId`.</span><span class="sxs-lookup"><span data-stu-id="75141-249">Let's suppose your data source definition is called `usermap`, and that it has two fields, `realName` and `user_AuthenticatedId`.</span></span> <span data-ttu-id="75141-250">Hola `requests` tabla también tiene un campo denominado `user_AuthenticatedId`, por lo que resulta fácil toojoin ellos:</span><span class="sxs-lookup"><span data-stu-id="75141-250">hello `requests` table also has a field named `user_AuthenticatedId`, so it's easy toojoin them:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
<span data-ttu-id="75141-251">la tabla resultante de las solicitudes de Hello tiene una columna adicional, `realName`.</span><span class="sxs-lookup"><span data-stu-id="75141-251">hello resulting table of requests has an additional column, `realName`.</span></span>

### <a name="import-from-logstash"></a><span data-ttu-id="75141-252">Importación desde LogStash</span><span class="sxs-lookup"><span data-stu-id="75141-252">Import from LogStash</span></span>

<span data-ttu-id="75141-253">Si usa [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), puede usar los registros de análisis tooquery.</span><span class="sxs-lookup"><span data-stu-id="75141-253">If you use [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), you can use Analytics tooquery your logs.</span></span> <span data-ttu-id="75141-254">Hola de uso [complemento que canaliza datos en análisis](https://github.com/Microsoft/logstash-output-application-insights).</span><span class="sxs-lookup"><span data-stu-id="75141-254">Use hello [plugin that pipes data into Analytics](https://github.com/Microsoft/logstash-output-application-insights).</span></span> 

## <a name="video"></a><span data-ttu-id="75141-255">Vídeo</span><span class="sxs-lookup"><span data-stu-id="75141-255">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

