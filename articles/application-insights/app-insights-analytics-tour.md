---
title: Un paseo por Analytics de Azure Application Insights | Microsoft Docs
description: "Ejemplos breves de todas las principales consultas de Analytics, la potente herramienta de búsqueda de Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: f5650d212eb2f8c460f062b3c11ae14c1e026ba6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="578d0-103">Un paseo por Analytics de Application Insights</span><span class="sxs-lookup"><span data-stu-id="578d0-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="578d0-104">[Analytics](app-insights-analytics.md) es la eficaz característica de búsqueda de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="578d0-104">[Analytics](app-insights-analytics.md) is the powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="578d0-105">En estas páginas se describe el lenguaje de consulta de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="578d0-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="578d0-106">**[Vea el vídeo de introducción](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="578d0-106">**[Watch the introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="578d0-107">**[Use una versión de prueba de Analytics en nuestros datos simulados](https://analytics.applicationinsights.io/demo)** si su aplicación aún no envía datos a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="578d0-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data to Application Insights yet.</span></span>
* <span data-ttu-id="578d0-108">**[La hoja de referencia rápida de usuarios de SQL](https://aka.ms/sql-analytics)** traduce las expresiones más comunes.</span><span class="sxs-lookup"><span data-stu-id="578d0-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates the most common idioms.</span></span>

<span data-ttu-id="578d0-109">Recorramos algunas preguntas básicas para comenzar.</span><span class="sxs-lookup"><span data-stu-id="578d0-109">Let's take a walk through some basic queries to get you started.</span></span>

## <a name="connect-to-your-application-insights-data"></a><span data-ttu-id="578d0-110">Conexión a los datos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="578d0-110">Connect to your Application Insights data</span></span>
<span data-ttu-id="578d0-111">Abra Analytics desde la [hoja de información general](app-insights-dashboards.md) de su aplicación en Application Insights:</span><span class="sxs-lookup"><span data-stu-id="578d0-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![Abra portal.azure.com, abra su recurso de Application Insights y haga clic en Análisis.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="578d0-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): mostrarme n filas</span><span class="sxs-lookup"><span data-stu-id="578d0-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="578d0-114">Los puntos de datos que registran las operaciones de usuario (normalmente solicitudes HTTP recibidas mediante la aplicación web) se almacenan en una tabla denominada `requests`.</span><span class="sxs-lookup"><span data-stu-id="578d0-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="578d0-115">Cada fila es un punto de datos de telemetría procedente del SDK de Application Insights en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="578d0-115">Each row is a telemetry data point received from the Application Insights SDK in your app.</span></span>

<span data-ttu-id="578d0-116">Comencemos examinando algunas filas de ejemplo de la tabla:</span><span class="sxs-lookup"><span data-stu-id="578d0-116">Let's start by examining a few sample rows of the table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="578d0-118">Coloque el cursor en algún lugar de la instrucción antes de hacer clic en Go (Ir).</span><span class="sxs-lookup"><span data-stu-id="578d0-118">Put the cursor somewhere in the statement before you click Go.</span></span> <span data-ttu-id="578d0-119">Puede dividir una instrucción en varias líneas, pero no incluya líneas en blanco en una instrucción.</span><span class="sxs-lookup"><span data-stu-id="578d0-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="578d0-120">Las líneas en blanco son una forma práctica de tener varias consultas diferentes en la ventana.</span><span class="sxs-lookup"><span data-stu-id="578d0-120">Blank lines are a convenient way to keep several separate queries in the window.</span></span>
>
>

<span data-ttu-id="578d0-121">Elija columnas, arrástrelas, agrupe por columnas y filtre:</span><span class="sxs-lookup"><span data-stu-id="578d0-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Hacer clic en la selección de columna en la parte superior derecha de los resultados](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="578d0-123">Expanda cualquier elemento para ver los detalles:</span><span class="sxs-lookup"><span data-stu-id="578d0-123">Expand any item to see the detail:</span></span>

![Seleccione Table (Tabla) y use Configure Columns (Configurar columnas).](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="578d0-125">Haga clic en el encabezado de una columna para cambiar el orden de los resultados disponibles en el explorador web.</span><span class="sxs-lookup"><span data-stu-id="578d0-125">Click the head of a column to re-order the results available in the web browser.</span></span> <span data-ttu-id="578d0-126">Tenga en cuenta que, para un conjunto grande de resultados, el número de filas que se descargan en el explorador es limitado.</span><span class="sxs-lookup"><span data-stu-id="578d0-126">But be aware that for a large result set, the number of rows downloaded to the browser is limited.</span></span> <span data-ttu-id="578d0-127">Esta forma de ordenación no siempre muestra los elementos mayores o menores reales.</span><span class="sxs-lookup"><span data-stu-id="578d0-127">Sorting this way doesn't always show you the actual highest or lowest items.</span></span> <span data-ttu-id="578d0-128">Para ordenar los elementos de forma confiable, use el operador `top` o `sort`.</span><span class="sxs-lookup"><span data-stu-id="578d0-128">To sort items reliably, use the `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="578d0-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) y [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="578d0-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="578d0-130">`take` resulta útil para obtener un ejemplo rápido de un resultado, pero muestra filas de la tabla sin ningún orden determinado.</span><span class="sxs-lookup"><span data-stu-id="578d0-130">`take` is useful to get a quick sample of a result, but it shows rows from the table in no particular order.</span></span> <span data-ttu-id="578d0-131">Para obtener una vista ordenada, use `top` (para un ejemplo) o `sort` (toda la tabla).</span><span class="sxs-lookup"><span data-stu-id="578d0-131">To get an ordered view, use `top` (for a sample) or `sort` (over the whole table).</span></span>

<span data-ttu-id="578d0-132">Muéstrame las primeras n filas, ordenadas por una columna en particular:</span><span class="sxs-lookup"><span data-stu-id="578d0-132">Show me the first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="578d0-133">*Sintaxis*: la mayoría de los operadores tienen parámetros de palabra clave como `by`.</span><span class="sxs-lookup"><span data-stu-id="578d0-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="578d0-134">`desc` = orden descendente, `asc` = orden ascendente.</span><span class="sxs-lookup"><span data-stu-id="578d0-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="578d0-135">`top...` es una manera más eficiente de decir `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="578d0-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="578d0-136">Podríamos haber escrito:</span><span class="sxs-lookup"><span data-stu-id="578d0-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="578d0-137">El resultado sería el mismo, pero se ejecutaría un poco más lento.</span><span class="sxs-lookup"><span data-stu-id="578d0-137">The result would be the same, but it would run a bit more slowly.</span></span> <span data-ttu-id="578d0-138">(También podría escribir `order`, que es un alias de `sort`).</span><span class="sxs-lookup"><span data-stu-id="578d0-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="578d0-139">Los encabezados de columna en la vista de tabla también pueden utilizarse para ordenar los resultados en la pantalla.</span><span class="sxs-lookup"><span data-stu-id="578d0-139">The column headers in the table view can also be used to sort the results on the screen.</span></span> <span data-ttu-id="578d0-140">Pero por supuesto, si ha usado `take` o `top` para recuperar solo parte de una tabla, solamente reordenará los registros que ha recuperado.</span><span class="sxs-lookup"><span data-stu-id="578d0-140">But of course, if you've used `take` or `top` to retrieve just part of a table, you'll only re-order the records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="578d0-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrado de una condición.</span><span class="sxs-lookup"><span data-stu-id="578d0-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="578d0-142">Veamos las solicitudes que devuelven un código de resultado determinado:</span><span class="sxs-lookup"><span data-stu-id="578d0-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="578d0-143">El operador `where` acepta una expresión booleana.</span><span class="sxs-lookup"><span data-stu-id="578d0-143">The `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="578d0-144">He aquí algunos puntos clave:</span><span class="sxs-lookup"><span data-stu-id="578d0-144">Here are some key points about them:</span></span>

* <span data-ttu-id="578d0-145">`and`, `or`: Operadores booleanos</span><span class="sxs-lookup"><span data-stu-id="578d0-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="578d0-146">`==`, `<>`, `!=`: igual que y no igual que</span><span class="sxs-lookup"><span data-stu-id="578d0-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="578d0-147">`=~`, `!~`: cadena que no distingue entre mayúsculas y minúsculas igual que y no igual que.</span><span class="sxs-lookup"><span data-stu-id="578d0-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="578d0-148">Hay muchos más operadores de comparación de cadenas.</span><span class="sxs-lookup"><span data-stu-id="578d0-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-the-right-type"></a><span data-ttu-id="578d0-149">Obtención del tipo correcto</span><span class="sxs-lookup"><span data-stu-id="578d0-149">Getting the right type</span></span>
<span data-ttu-id="578d0-150">Buscar solicitudes incorrectas:</span><span class="sxs-lookup"><span data-stu-id="578d0-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="578d0-151">Hora</span><span class="sxs-lookup"><span data-stu-id="578d0-151">Time</span></span>

<span data-ttu-id="578d0-152">De forma predeterminada, las consultas se restringen a las últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="578d0-152">By default, your queries are restricted to the last 24 hours.</span></span> <span data-ttu-id="578d0-153">Pero puede cambiar este intervalo:</span><span class="sxs-lookup"><span data-stu-id="578d0-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="578d0-154">Reemplace el intervalo de tiempo mediante la escritura de cualquier consulta que mencione `timestamp` en una cláusula where.</span><span class="sxs-lookup"><span data-stu-id="578d0-154">Override the time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="578d0-155">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="578d0-155">For example:</span></span>

```AIQL

    // What were the slowest requests over the past 3 days?
    requests
    | where timestamp > ago(3d)  // Override the time range
    | top 5 by duration
```

<span data-ttu-id="578d0-156">La característica de intervalo de tiempo es equivalente a una cláusula "where" insertada después de cada mención de una de las tablas de origen.</span><span class="sxs-lookup"><span data-stu-id="578d0-156">The time range feature is equivalent to a 'where' clause inserted after each mention of one of the source tables.</span></span>

<span data-ttu-id="578d0-157">`ago(3d)` significa "hace tres días".</span><span class="sxs-lookup"><span data-stu-id="578d0-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="578d0-158">Otras unidades de tiempo son horas (`2h`, `2.5h`), minutos (`25m`) y segundos (`10s`).</span><span class="sxs-lookup"><span data-stu-id="578d0-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="578d0-159">Otros ejemplos:</span><span class="sxs-lookup"><span data-stu-id="578d0-159">Other examples:</span></span>

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

<span data-ttu-id="578d0-160">[Referencia de fechas y horas](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="578d0-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="578d0-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): seleccionar, cambiar nombre y calcular columnas</span><span class="sxs-lookup"><span data-stu-id="578d0-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="578d0-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) para seleccionar solamente las columnas que desea:</span><span class="sxs-lookup"><span data-stu-id="578d0-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) to pick out just the columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="578d0-163">También puede cambiar el nombre de las columnas y definir otras nuevas:</span><span class="sxs-lookup"><span data-stu-id="578d0-163">You can also rename columns and define new ones:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![result](./media/app-insights-analytics-tour/270.png)

* <span data-ttu-id="578d0-165">Los nombres de columna pueden incluir espacios o símbolos si están entre corchetes, tal como se muestra: `['...']` o `["..."]`</span><span class="sxs-lookup"><span data-stu-id="578d0-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="578d0-166">`%` es el operador de módulo habitual.</span><span class="sxs-lookup"><span data-stu-id="578d0-166">`%` is the usual modulo operator.</span></span>
* <span data-ttu-id="578d0-167">`1d` (es decir, el dígito uno y luego una "d") es un literal de intervalo de tiempo que significa un día.</span><span class="sxs-lookup"><span data-stu-id="578d0-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="578d0-168">Aquí se indican otros literales de intervalo de tiempo: `12h`, `30m`, `10s` y `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="578d0-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="578d0-169">`floor` (alias `bin`) redondea un valor a la baja al múltiplo más cercano del valor base que proporciona.</span><span class="sxs-lookup"><span data-stu-id="578d0-169">`floor` (alias `bin`) rounds a value down to the nearest multiple of the base value you provide.</span></span> <span data-ttu-id="578d0-170">Por lo tanto, `floor(aTime, 1s)` redondea un tiempo a la baja al segundo más cercano.</span><span class="sxs-lookup"><span data-stu-id="578d0-170">So `floor(aTime, 1s)` rounds a time down to the nearest second.</span></span>

<span data-ttu-id="578d0-171">Las expresiones pueden incluir todos los operadores habituales (`+`, `-`, etc.) y hay una amplia gama de funciones útiles.</span><span class="sxs-lookup"><span data-stu-id="578d0-171">Expressions can include all the usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="578d0-172">Extend</span><span class="sxs-lookup"><span data-stu-id="578d0-172">Extend</span></span>
<span data-ttu-id="578d0-173">Si solo desea agregar columnas a las ya existentes, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="578d0-173">If you just want to add columns to the existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="578d0-174">El uso de [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) es menos detallado que [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) si desea conservar todas las columnas existentes.</span><span class="sxs-lookup"><span data-stu-id="578d0-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want to keep all the existing columns.</span></span>

### <a name="convert-to-local-time"></a><span data-ttu-id="578d0-175">Conversión a la hora local</span><span class="sxs-lookup"><span data-stu-id="578d0-175">Convert to local time</span></span>

<span data-ttu-id="578d0-176">Las marcas de tiempo siempre se expresan en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="578d0-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="578d0-177">Por lo que si se encuentra en la costa Pacífico y es temporada de invierno, sería de esta forma:</span><span class="sxs-lookup"><span data-stu-id="578d0-177">So if you're on the US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="578d0-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): adición de grupos de filas</span><span class="sxs-lookup"><span data-stu-id="578d0-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="578d0-179">`Summarize` aplica una *función de agregación* específica sobre grupos de filas.</span><span class="sxs-lookup"><span data-stu-id="578d0-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="578d0-180">Por ejemplo, el tiempo que su aplicación web tarda en responder a una solicitud se notifica en el campo `duration`.</span><span class="sxs-lookup"><span data-stu-id="578d0-180">For example, the time your web app takes to respond to a request is reported in the field `duration`.</span></span> <span data-ttu-id="578d0-181">Veamos el tiempo medio de respuesta de todas las solicitudes:</span><span class="sxs-lookup"><span data-stu-id="578d0-181">Let's see the average response time to all requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="578d0-182">O bien, podríamos separar el resultado en solicitudes de nombres diferentes:</span><span class="sxs-lookup"><span data-stu-id="578d0-182">Or we could separate the result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="578d0-183">`Summarize` recopila los puntos de datos de la transmisión en grupos que la cláusula `by` calcula por igual.</span><span class="sxs-lookup"><span data-stu-id="578d0-183">`Summarize` collects the data points in the stream into groups for which the `by` clause evaluates equally.</span></span> <span data-ttu-id="578d0-184">Cada valor de la expresión `by` (cada nombre de la operación en el ejemplo anterior) da como resultado una fila de la tabla de resultados.</span><span class="sxs-lookup"><span data-stu-id="578d0-184">Each value in the `by` expression - each operation name in the above example - results in a row in the result table.</span></span>

<span data-ttu-id="578d0-185">O bien, podríamos agrupar los resultados en función de la hora del día:</span><span class="sxs-lookup"><span data-stu-id="578d0-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="578d0-186">Observe cómo usamos la función `bin` (también conocida como "`floor`").</span><span class="sxs-lookup"><span data-stu-id="578d0-186">Notice how we're using the `bin` function (aka `floor`).</span></span> <span data-ttu-id="578d0-187">Si solo usáramos `by timestamp`, cada fila de entrada terminaría en su pequeño grupo.</span><span class="sxs-lookup"><span data-stu-id="578d0-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="578d0-188">Para cualquier escalar continuo, como horas o números, tenemos que dividir el intervalo continuo en un número de valores discretos fácil de administrar.</span><span class="sxs-lookup"><span data-stu-id="578d0-188">For any continuous scalar like times or numbers, we have to break the continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="578d0-189">`bin`, que es simplemente la conocida función de redondeo `floor`, es la manera más sencilla de hacerlo.</span><span class="sxs-lookup"><span data-stu-id="578d0-189">`bin` - which is just the familiar rounding-down `floor` function - is the easiest way to do that.</span></span>

<span data-ttu-id="578d0-190">Podemos usar la misma técnica para reducir los intervalos de cadenas:</span><span class="sxs-lookup"><span data-stu-id="578d0-190">We can use the same technique to reduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="578d0-191">Tenga en cuenta que puede usar `name=` para establecer el nombre de una columna de resultados, en las expresiones de agregación o mediante la cláusula by.</span><span class="sxs-lookup"><span data-stu-id="578d0-191">Notice that you can use `name=` to set the name of a result column, either in the aggregation expressions or the by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="578d0-192">Recuento de datos muestreados</span><span class="sxs-lookup"><span data-stu-id="578d0-192">Counting sampled data</span></span>
<span data-ttu-id="578d0-193">`sum(itemCount)` es la agregación recomendada para contar eventos.</span><span class="sxs-lookup"><span data-stu-id="578d0-193">`sum(itemCount)` is the recommended aggregation to count events.</span></span> <span data-ttu-id="578d0-194">En muchos casos, itemCount == 1, por lo que la función simplemente cuenta el número de filas del grupo.</span><span class="sxs-lookup"><span data-stu-id="578d0-194">In many cases, itemCount==1, so the function simply counts up the number of rows in the group.</span></span> <span data-ttu-id="578d0-195">Pero cuando el [muestreo](app-insights-sampling.md) está en funcionamiento, solo se conserva una fracción de los eventos originales como puntos de datos en Application Insights, de modo que por cada punto de datos que vea, haya eventos `itemCount`.</span><span class="sxs-lookup"><span data-stu-id="578d0-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of the original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="578d0-196">Por ejemplo, si el muestreo descarta el 75 % de los eventos originales, itemCount ==4 en los registros retenidos; es decir, para cada registro retenido, había cuatro registros originales.</span><span class="sxs-lookup"><span data-stu-id="578d0-196">For example, if sampling discards 75% of the original events, then itemCount==4 in the retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="578d0-197">El muestreo adaptable hace que itemCount sea mayor durante los períodos en que la aplicación se utiliza más.</span><span class="sxs-lookup"><span data-stu-id="578d0-197">Adaptive sampling causes itemCount to be higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="578d0-198">Por lo tanto, resumir itemCount proporciona una buena estimación del número original de eventos.</span><span class="sxs-lookup"><span data-stu-id="578d0-198">Summing up itemCount therefore gives a good estimate of the original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="578d0-199">También existe una agregación `count()` (y una operación de recuento) para los casos en los que realmente desea contar el número de filas de un grupo.</span><span class="sxs-lookup"><span data-stu-id="578d0-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want to count the number of rows in a group.</span></span>

<span data-ttu-id="578d0-200">Existe una gama de [funciones de agregación](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="578d0-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-the-results"></a><span data-ttu-id="578d0-201">Crear gráficos de los resultados</span><span class="sxs-lookup"><span data-stu-id="578d0-201">Charting the results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="578d0-202">De forma predeterminada, los resultados se muestran como una tabla:</span><span class="sxs-lookup"><span data-stu-id="578d0-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="578d0-203">Podemos hacerlo mejor que la vista de la tabla.</span><span class="sxs-lookup"><span data-stu-id="578d0-203">We can do better than the table view.</span></span> <span data-ttu-id="578d0-204">Echemos un vistazo a los resultados en la vista del gráfico con la opción de barra vertical:</span><span class="sxs-lookup"><span data-stu-id="578d0-204">Let's look at the results in the chart view with the vertical bar option:</span></span>

![Haga clic Chart (Gráfico) y después elija Vertical bar chart (Gráfico de barras verticales) y asigne los ejes x e y.](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="578d0-206">Tenga en cuenta que aunque no ordenamos los resultados por tiempo (como puede ver en la visualización de la tabla), la visualización del gráfico siempre muestra las fechas en el orden correcto.</span><span class="sxs-lookup"><span data-stu-id="578d0-206">Notice that although we didn't sort the results by time (as you can see in the table display), the chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="578d0-207">Gráficos de tiempo</span><span class="sxs-lookup"><span data-stu-id="578d0-207">Timecharts</span></span>
<span data-ttu-id="578d0-208">Mostrar cuántos eventos hay cada hora:</span><span class="sxs-lookup"><span data-stu-id="578d0-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="578d0-209">Seleccionar la opción de visualización de gráfico:</span><span class="sxs-lookup"><span data-stu-id="578d0-209">Select the Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="578d0-211">Varias series</span><span class="sxs-lookup"><span data-stu-id="578d0-211">Multiple series</span></span>
<span data-ttu-id="578d0-212">Varias expresiones en la cláusula `summarize` crean varias columnas.</span><span class="sxs-lookup"><span data-stu-id="578d0-212">Multiple expressions in the `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="578d0-213">Varias expresiones en la cláusula `by` crea varias filas, una para cada combinación de valores.</span><span class="sxs-lookup"><span data-stu-id="578d0-213">Multiple expressions in the `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabla de solicitudes por hora y ubicación](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="578d0-215">Segmentación de un gráfico por dimensiones</span><span class="sxs-lookup"><span data-stu-id="578d0-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="578d0-216">Si utiliza una tabla que tiene una columna de cadena y una columna numérica, la cadena puede utilizarse para dividir los datos numéricos en series independientes de puntos.</span><span class="sxs-lookup"><span data-stu-id="578d0-216">If you chart a table that has a string column and a numeric column, the string can be used to split the numeric data into separate series of points.</span></span> <span data-ttu-id="578d0-217">Si hay más de una columna de cadena, puede elegir qué columna debe utilizar como discriminador.</span><span class="sxs-lookup"><span data-stu-id="578d0-217">If there's more than one string column, you can choose which column to use as the discriminator.</span></span>

![Segmentación de un gráfico de análisis](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="578d0-219">Tasa de devolución</span><span class="sxs-lookup"><span data-stu-id="578d0-219">Bounce rate</span></span>

<span data-ttu-id="578d0-220">Convierte un valor booleano en una cadena que se utiliza como discriminador:</span><span class="sxs-lookup"><span data-stu-id="578d0-220">Convert a boolean to a string to use it as a discriminator:</span></span>

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a><span data-ttu-id="578d0-221">Muestra de varias métricas</span><span class="sxs-lookup"><span data-stu-id="578d0-221">Display multiple metrics</span></span>
<span data-ttu-id="578d0-222">Si utiliza una tabla con más de una columna numérica, además de la marca de tiempo, puede mostrar cualquier combinación de ellas.</span><span class="sxs-lookup"><span data-stu-id="578d0-222">If you chart a table that has more than one numeric column, in addition to the timestamp, you can display any combination of them.</span></span>

![Segmentación de un gráfico de análisis](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="578d0-224">Debe seleccionar **Don't Split** (No dividir) para poder seleccionar varias columnas numéricas.</span><span class="sxs-lookup"><span data-stu-id="578d0-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="578d0-225">No se puede dividir por una columna de cadena al mismo tiempo que se muestra más de una columna numérica.</span><span class="sxs-lookup"><span data-stu-id="578d0-225">You can't split by a string column at the same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="578d0-226">Ciclo medio diario</span><span class="sxs-lookup"><span data-stu-id="578d0-226">Daily average cycle</span></span>
<span data-ttu-id="578d0-227">¿Cómo varía el uso a lo largo del día normal?</span><span class="sxs-lookup"><span data-stu-id="578d0-227">How does usage vary over the average day?</span></span>

<span data-ttu-id="578d0-228">Contar solicitudes por el módulo de tiempo un día, discretizadas en horas:</span><span class="sxs-lookup"><span data-stu-id="578d0-228">Count requests by the time modulo one day, binned into hours:</span></span>

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Gráfico de líneas de horas en un día normal](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> <span data-ttu-id="578d0-230">Observe que actualmente tenemos convertir las duraciones de tiempo en fechas y horas para mostrar en el gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="578d0-230">Notice that we currently have to convert time durations to datetimes in order to display on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="578d0-231">Comparación de varias series diarias</span><span class="sxs-lookup"><span data-stu-id="578d0-231">Compare multiple daily series</span></span>
<span data-ttu-id="578d0-232">¿Cómo varía el uso a lo largo de la hora del día en distintos países?</span><span class="sxs-lookup"><span data-stu-id="578d0-232">How does usage vary over the time of day in different countries?</span></span>

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![División por client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a><span data-ttu-id="578d0-234">Trazado de una distribución</span><span class="sxs-lookup"><span data-stu-id="578d0-234">Plot a distribution</span></span>
<span data-ttu-id="578d0-235">¿Cuántas sesiones existen de longitudes diferentes?</span><span class="sxs-lookup"><span data-stu-id="578d0-235">How many sessions are there of different lengths?</span></span>

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

<span data-ttu-id="578d0-236">La última línea es necesaria para convertir a un valor datetime.</span><span class="sxs-lookup"><span data-stu-id="578d0-236">The last line is required to convert to datetime.</span></span> <span data-ttu-id="578d0-237">Actualmente el eje x de un gráfico se muestra como un valor escalar solo si es un valor datetime.</span><span class="sxs-lookup"><span data-stu-id="578d0-237">Currently the x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="578d0-238">La cláusula `where` excluye las sesiones únicas (sessionDuration==0) y establece la longitud del eje X.</span><span class="sxs-lookup"><span data-stu-id="578d0-238">The `where` clause excludes one-shot sessions (sessionDuration==0) and sets the length of the x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="578d0-239">Percentiles</span><span class="sxs-lookup"><span data-stu-id="578d0-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="578d0-240">¿Qué intervalos de duraciones cubren diferentes porcentajes de sesiones?</span><span class="sxs-lookup"><span data-stu-id="578d0-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="578d0-241">Utilice la consulta anterior, pero reemplace la última línea:</span><span class="sxs-lookup"><span data-stu-id="578d0-241">Use the above query, but replace the last line:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

<span data-ttu-id="578d0-242">También eliminamos el límite superior en la cláusula where con el fin de obtener cifras correctas, incluidas las sesiones con más de una solicitud:</span><span class="sxs-lookup"><span data-stu-id="578d0-242">We also removed the upper limit in the where clause, in order to get correct figures including all sessions with more than one request:</span></span>

![result](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="578d0-244">De lo que podemos ver que:</span><span class="sxs-lookup"><span data-stu-id="578d0-244">From which we can see that:</span></span>

* <span data-ttu-id="578d0-245">El 5 % de las sesiones tienen una duración de menos de 3 minutos 34 s;</span><span class="sxs-lookup"><span data-stu-id="578d0-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="578d0-246">El 50 % de las sesiones dura menos de 36 minutos;</span><span class="sxs-lookup"><span data-stu-id="578d0-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="578d0-247">El 5 % de las sesiones dura más de 7 días.</span><span class="sxs-lookup"><span data-stu-id="578d0-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="578d0-248">Para obtener un desglose independiente para cada país, simplemente tiene que conservar la columna client_CountryOrRegion por separado en ambos operadores de resumen:</span><span class="sxs-lookup"><span data-stu-id="578d0-248">To get a separate breakdown for each country, we just have to bring the client_CountryOrRegion column separately through both summarize operators:</span></span>

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a><span data-ttu-id="578d0-249">Unión</span><span class="sxs-lookup"><span data-stu-id="578d0-249">Join</span></span>
<span data-ttu-id="578d0-250">Tenemos acceso a varias tablas, incluidas las solicitudes y las excepciones.</span><span class="sxs-lookup"><span data-stu-id="578d0-250">We have access to several tables, including requests and exceptions.</span></span>

<span data-ttu-id="578d0-251">Para encontrar las excepciones relacionadas con una solicitud que devolvió una respuesta de error, podemos combinar las tablas en `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="578d0-251">To find the exceptions related to a request that returned a failure response, we can join the tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="578d0-252">Es recomendable usar `project` para seleccionar solo las columnas que se necesitan antes de realizar la combinación.</span><span class="sxs-lookup"><span data-stu-id="578d0-252">It's good practice to use `project` to select just the columns we need before performing the join.</span></span>
<span data-ttu-id="578d0-253">En las mismas cláusulas, cambiamos el nombre de la columna de marca de tiempo.</span><span class="sxs-lookup"><span data-stu-id="578d0-253">In the same clauses, we rename the timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-to-a-variable"></a><span data-ttu-id="578d0-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): asignación de un resultado a una variable</span><span class="sxs-lookup"><span data-stu-id="578d0-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result to a variable</span></span>

<span data-ttu-id="578d0-255">Use `let` para separar las partes de la expresión anterior.</span><span class="sxs-lookup"><span data-stu-id="578d0-255">Use `let` to separate out the parts of the previous expression.</span></span> <span data-ttu-id="578d0-256">Los resultados no cambian:</span><span class="sxs-lookup"><span data-stu-id="578d0-256">The results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="578d0-257">En el cliente de Analytics, no incluya líneas en blanco entre las partes de la consulta.</span><span class="sxs-lookup"><span data-stu-id="578d0-257">In the Analytics client, don't put blank lines between the parts of the query.</span></span> <span data-ttu-id="578d0-258">Asegúrese de ejecutar todo.</span><span class="sxs-lookup"><span data-stu-id="578d0-258">Make sure to execute all of it.</span></span>
>

<span data-ttu-id="578d0-259">Use `toscalar` para convertir una celda de tabla única en un valor:</span><span class="sxs-lookup"><span data-stu-id="578d0-259">Use `toscalar` to convert a single table cell to a value:</span></span>

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a><span data-ttu-id="578d0-260">Funciones</span><span class="sxs-lookup"><span data-stu-id="578d0-260">Functions</span></span>

<span data-ttu-id="578d0-261">Use *Let* para definir una función:</span><span class="sxs-lookup"><span data-stu-id="578d0-261">Use *Let* to define a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="578d0-262">Acceso a objetos anidados</span><span class="sxs-lookup"><span data-stu-id="578d0-262">Accessing nested objects</span></span>
<span data-ttu-id="578d0-263">Se puede acceder fácilmente a los objetos anidados.</span><span class="sxs-lookup"><span data-stu-id="578d0-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="578d0-264">Por ejemplo, en la transmisión de excepciones verá objetos estructurados así:</span><span class="sxs-lookup"><span data-stu-id="578d0-264">For example, in the exceptions stream you can see structured objects like this:</span></span>

![result](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="578d0-266">Es posible aplanarlo si selecciona las propiedades que le interesan:</span><span class="sxs-lookup"><span data-stu-id="578d0-266">You can flatten it by choosing the properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="578d0-267">Tenga en cuenta que debe utilizar una conversión al tipo adecuado.</span><span class="sxs-lookup"><span data-stu-id="578d0-267">Note that you need to cast the result to the appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="578d0-268">Propiedades y medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="578d0-268">Custom properties and measurements</span></span>
<span data-ttu-id="578d0-269">Si la aplicación adjunta [dimensiones personalizadas (propiedades) y medidas personalizadas](app-insights-api-custom-events-metrics.md#properties) a eventos, las verá en los objetos `customDimensions` y `customMeasurements`.</span><span class="sxs-lookup"><span data-stu-id="578d0-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) to events, then you will see them in the `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="578d0-270">Por ejemplo, si la aplicación incluye:</span><span class="sxs-lookup"><span data-stu-id="578d0-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="578d0-271">Para extraer estos valores en Analytics:</span><span class="sxs-lookup"><span data-stu-id="578d0-271">To extract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast to expected type

```

<span data-ttu-id="578d0-272">Para comprobar si una dimensión personalizada es de un tipo determinado:</span><span class="sxs-lookup"><span data-stu-id="578d0-272">To verify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="578d0-273">Paneles</span><span class="sxs-lookup"><span data-stu-id="578d0-273">Dashboards</span></span>
<span data-ttu-id="578d0-274">Puede anclar los resultados a un panel para reunir todos los gráficos y tablas más importantes.</span><span class="sxs-lookup"><span data-stu-id="578d0-274">You can pin your results to a dashboard in order to bring together all your most important charts and tables.</span></span>

* <span data-ttu-id="578d0-275">[Panel compartido de Azure](app-insights-dashboards.md#share-dashboards): haga clic en el icono de anclar.</span><span class="sxs-lookup"><span data-stu-id="578d0-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click the pin icon.</span></span> <span data-ttu-id="578d0-276">Antes de hacerlo, debe tener un panel compartido.</span><span class="sxs-lookup"><span data-stu-id="578d0-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="578d0-277">En Azure Portal, abra o cree un panel y haga clic en Compartir.</span><span class="sxs-lookup"><span data-stu-id="578d0-277">In the Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="578d0-278">[Panel de Power BI](app-insights-export-power-bi.md): haga clic en Exportar, Consulta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="578d0-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="578d0-279">Una ventaja de esta alternativa es que puede mostrar la consulta junto con otros resultados procedentes de una gran variedad de orígenes.</span><span class="sxs-lookup"><span data-stu-id="578d0-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="578d0-280">Combinación con datos importados</span><span class="sxs-lookup"><span data-stu-id="578d0-280">Combine with imported data</span></span>

<span data-ttu-id="578d0-281">Los informes de análisis se ven perfectos en el panel, pero a veces desea convertir los datos a una forma más simplificada.</span><span class="sxs-lookup"><span data-stu-id="578d0-281">Analytics reports look great on the dashboard, but sometimes you want to translate the data to a more digestible form.</span></span> <span data-ttu-id="578d0-282">Por ejemplo, suponga que los usuarios autenticados se identifican en la telemetría mediante un alias.</span><span class="sxs-lookup"><span data-stu-id="578d0-282">For example, suppose your authenticated users are identified in the telemetry by an alias.</span></span> <span data-ttu-id="578d0-283">Le gustaría mostrar sus nombres reales en los resultados.</span><span class="sxs-lookup"><span data-stu-id="578d0-283">You'd like to show their real names in your results.</span></span> <span data-ttu-id="578d0-284">Para ello, necesita un archivo CSV que asigna los nombres reales a partir de los alias.</span><span class="sxs-lookup"><span data-stu-id="578d0-284">To do this, you need a CSV file that maps from the aliases to the real names.</span></span>

<span data-ttu-id="578d0-285">Puede importar un archivo de datos y usarlo como cualquiera de las tablas estándares (solicitudes, excepciones, etc.).</span><span class="sxs-lookup"><span data-stu-id="578d0-285">You can import a data file and use it just like any of the standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="578d0-286">Puede consultarla por sí sola o combinarla con otras tablas.</span><span class="sxs-lookup"><span data-stu-id="578d0-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="578d0-287">Por ejemplo, si tiene una tabla denominada usermap y tiene las columnas `realName` y `userId`, se puede utilizar para traducir el campo `user_AuthenticatedId` en la telemetría de solicitud:</span><span class="sxs-lookup"><span data-stu-id="578d0-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it to translate the `user_AuthenticatedId` field in the request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get the realName field from the usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="578d0-288">Para importar una tabla, en la hoja de esquema, en **Other Data Sources** (Otros orígenes de datos), siga las instrucciones para agregar un nuevo origen de datos, mediante la carga de una muestra de los datos.</span><span class="sxs-lookup"><span data-stu-id="578d0-288">To import a table, in the Schema blade, under **Other Data Sources**, follow the instructions to add a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="578d0-289">Luego puede usar esta definición para cargar las tablas.</span><span class="sxs-lookup"><span data-stu-id="578d0-289">Then you can use this definition to upload tables.</span></span>

<span data-ttu-id="578d0-290">La característica de importación está actualmente en versión preliminar, por lo que verá inicialmente un vínculo "Póngase en contacto con nosotros" en "Other data sources" (Otros orígenes de datos).</span><span class="sxs-lookup"><span data-stu-id="578d0-290">The import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="578d0-291">Úselo para suscribirse al programa de versión preliminar y luego el vínculo se reemplazará por un botón "Add new data source" (Agregar nuevo origen de datos).</span><span class="sxs-lookup"><span data-stu-id="578d0-291">Use this to sign up to the preview program, and the link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="578d0-292">Tablas</span><span class="sxs-lookup"><span data-stu-id="578d0-292">Tables</span></span>
<span data-ttu-id="578d0-293">A la transmisión de datos de telemetría recibidos de la aplicación se puede acceder a través de varias tablas.</span><span class="sxs-lookup"><span data-stu-id="578d0-293">The stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="578d0-294">El esquema de propiedades disponibles para cada tabla se puede ver a la izquierda de la ventana.</span><span class="sxs-lookup"><span data-stu-id="578d0-294">The schema of properties available for each table is visible at the left of the window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="578d0-295">Tabla de solicitudes</span><span class="sxs-lookup"><span data-stu-id="578d0-295">Requests table</span></span>
<span data-ttu-id="578d0-296">Contar solicitudes HTTP para su aplicación web y segmento por nombre de página:</span><span class="sxs-lookup"><span data-stu-id="578d0-296">Count HTTP requests to your web app and segment by page name:</span></span>

![Contar solicitudes segmentadas por nombre](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="578d0-298">Buscar solicitudes con más errores:</span><span class="sxs-lookup"><span data-stu-id="578d0-298">Find the requests that fail most:</span></span>

![Contar solicitudes segmentadas por nombre](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="578d0-300">Tabla de eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="578d0-300">Custom events table</span></span>
<span data-ttu-id="578d0-301">Si utiliza [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) para enviar sus propios eventos, puede leerlo desde esta tabla.</span><span class="sxs-lookup"><span data-stu-id="578d0-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) to send your own events, you can read them from this table.</span></span>

<span data-ttu-id="578d0-302">Veamos un ejemplo en el que el código de aplicación contiene estas líneas:</span><span class="sxs-lookup"><span data-stu-id="578d0-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="578d0-303">Mostrar la frecuencia de estos eventos:</span><span class="sxs-lookup"><span data-stu-id="578d0-303">Display the frequency of these events:</span></span>

![Mostrar la tasa de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="578d0-305">Extraer las medidas y dimensiones de los eventos:</span><span class="sxs-lookup"><span data-stu-id="578d0-305">Extract measurements and dimensions from the events:</span></span>

![Mostrar la tasa de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="578d0-307">Tabla de métricas personalizadas</span><span class="sxs-lookup"><span data-stu-id="578d0-307">Custom metrics table</span></span>
<span data-ttu-id="578d0-308">Si utiliza [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) para enviar sus propios valores de métrica, encontrará los resultados en la transmisión **customMetrics**.</span><span class="sxs-lookup"><span data-stu-id="578d0-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to send your own metric values, you’ll find its results in the **customMetrics** stream.</span></span> <span data-ttu-id="578d0-309">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="578d0-309">For example:</span></span>  

![Métricas personalizadas en Application Insights Analytics](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="578d0-311">En el [Explorador de métricas](app-insights-metrics-explorer.md), todas las medidas personalizadas adjuntas a cualquier tipo de telemetría aparecen juntas en la hoja de métricas, junto con las métricas enviadas mediante `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="578d0-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached to any type of telemetry appear together in the metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="578d0-312">Sin embargo, en Analytics, las medidas personalizadas siguen adjuntas al tipo de telemetría en que se realizaron (eventos, solicitudes, etc.), mientras que las enviadas por TrackMetric aparecen en su propia transmisión.</span><span class="sxs-lookup"><span data-stu-id="578d0-312">But in Analytics, custom measurements are still attached to whichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="578d0-313">Tabla de contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="578d0-313">Performance counters table</span></span>
<span data-ttu-id="578d0-314">Los [contadores de rendimiento](app-insights-performance-counters.md) muestran métricas del sistema básico de la aplicación, como CPU, memoria y la utilización de la red.</span><span class="sxs-lookup"><span data-stu-id="578d0-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="578d0-315">Puede configurar el SDK para que envíe contadores adicionales, entre los que se incluyen sus propios contadores.</span><span class="sxs-lookup"><span data-stu-id="578d0-315">You can configure the SDK to send additional counters, including your own custom counters.</span></span>

<span data-ttu-id="578d0-316">El esquema **performanceCounters** expone `category`, el nombre de `counter` y el nombre de `instance` de cada contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="578d0-316">The **performanceCounters** schema exposes the `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="578d0-317">Los nombres de instancia de contador solo se pueden aplicar a algunos contadores de rendimiento y suele indicar el nombre del proceso con el que está relacionado el recuento.</span><span class="sxs-lookup"><span data-stu-id="578d0-317">Counter instance names are only applicable to some performance counters, and typically indicate the name of the process to which the count relates.</span></span> <span data-ttu-id="578d0-318">En la telemetría de cada aplicación, solo se ven los contadores de dicha aplicación.</span><span class="sxs-lookup"><span data-stu-id="578d0-318">In the telemetry for each application, you’ll see only the counters for that application.</span></span> <span data-ttu-id="578d0-319">Por ejemplo, para ver qué contadores están disponibles:</span><span class="sxs-lookup"><span data-stu-id="578d0-319">For example, to see what counters are available:</span></span>

![Contadores de rendimiento en Application Insights Analytics](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="578d0-321">Para obtener un gráfico de la memoria disponible en un período seleccionado:</span><span class="sxs-lookup"><span data-stu-id="578d0-321">To get a chart of available memory over the selected period:</span></span>

![Gráfico de tiempo de la memoria in Application Insights Analytics](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="578d0-323">Al igual que otros datos de telemetría, **performanceCounters** también tiene una columna `cloud_RoleInstance` que indica la identidad del equipo host en el que se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="578d0-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates the identity of the host machine on which your app is running.</span></span> <span data-ttu-id="578d0-324">Por ejemplo, para comparar el rendimiento de una aplicación en distintas máquinas:</span><span class="sxs-lookup"><span data-stu-id="578d0-324">For example, to compare the performance of your app on the different machines:</span></span>

![Rendimiento segmentado por instancia de rol en Application Insights Analytics](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="578d0-326">Tabla de excepciones</span><span class="sxs-lookup"><span data-stu-id="578d0-326">Exceptions table</span></span>
<span data-ttu-id="578d0-327">[Las excepciones que notifica la aplicación](app-insights-asp-net-exceptions.md) están disponibles en esta tabla.</span><span class="sxs-lookup"><span data-stu-id="578d0-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="578d0-328">Para buscar la solicitud HTTP que controlaba la aplicación cuando se produjo la excepción, combine operation_Id:</span><span class="sxs-lookup"><span data-stu-id="578d0-328">To find the HTTP request that your app was handling when the exception was raised, join on operation_Id:</span></span>

![Combinar excepciones con solicitudes en operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="578d0-330">Tabla de intervalos de explorador</span><span class="sxs-lookup"><span data-stu-id="578d0-330">Browser timings table</span></span>
<span data-ttu-id="578d0-331">`browserTimings` muestra los datos de carga de las páginas recopilados en los exploradores de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="578d0-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="578d0-332">[Configure su aplicación para la telemetría del lado cliente](app-insights-javascript.md) para ver estas métricas.</span><span class="sxs-lookup"><span data-stu-id="578d0-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order to see these metrics.</span></span>

<span data-ttu-id="578d0-333">El esquema incluye [métricas que indican las duraciones de las distintas fases del proceso de carga de las páginas](app-insights-javascript.md#page-load-performance)</span><span class="sxs-lookup"><span data-stu-id="578d0-333">The schema includes [metrics indicating the lengths of different stages of the page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="578d0-334">(no indican el periodo durante el que los usuarios leen una página).</span><span class="sxs-lookup"><span data-stu-id="578d0-334">(They don’t indicate the length of time your users read a page.)</span></span>  

<span data-ttu-id="578d0-335">Mostrar la popularidad de las distintas páginas y los tiempos de carga de cada página:</span><span class="sxs-lookup"><span data-stu-id="578d0-335">Show the popularities of different pages, and load times for each page:</span></span>

![Tiempos de carga de páginas en Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="578d0-337">Tabla de resultados de la disponibilidad</span><span class="sxs-lookup"><span data-stu-id="578d0-337">Availability results table</span></span>
<span data-ttu-id="578d0-338">`availabilityResults` muestra los resultados de sus [pruebas web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="578d0-338">`availabilityResults` shows the results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="578d0-339">Cada ejecución de las pruebas en cada una de las ubicaciones se notifica por separado.</span><span class="sxs-lookup"><span data-stu-id="578d0-339">Each run of your tests from each test location is reported separately.</span></span>

![Tiempos de carga de páginas en Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="578d0-341">Tabla de dependencias</span><span class="sxs-lookup"><span data-stu-id="578d0-341">Dependencies table</span></span>
<span data-ttu-id="578d0-342">Contiene los resultados de las llamadas que su aplicación realiza a las bases de datos y a las API de REST, así como de otras llamadas a TrackDependency().</span><span class="sxs-lookup"><span data-stu-id="578d0-342">Contains results of calls that your app makes to databases and REST APIs, and other calls to TrackDependency().</span></span> <span data-ttu-id="578d0-343">También incluye las llamadas AJAX realizadas desde el explorador.</span><span class="sxs-lookup"><span data-stu-id="578d0-343">Also includes AJAX calls made from the browser.</span></span>

<span data-ttu-id="578d0-344">Llamadas AJAX desde el explorador:</span><span class="sxs-lookup"><span data-stu-id="578d0-344">AJAX calls from the browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="578d0-345">Llamadas de dependencia desde el servidor:</span><span class="sxs-lookup"><span data-stu-id="578d0-345">Dependency calls from the server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="578d0-346">Los resultados de la dependencia de servidor siempre muestran `success==False` si no está instalado el agente de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="578d0-346">Server-side dependency results always show `success==False` if the Application Insights Agent is not installed.</span></span> <span data-ttu-id="578d0-347">Sin embargo, los demás datos son correctos.</span><span class="sxs-lookup"><span data-stu-id="578d0-347">However, the other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="578d0-348">Tabla de seguimientos</span><span class="sxs-lookup"><span data-stu-id="578d0-348">Traces table</span></span>
<span data-ttu-id="578d0-349">Contiene los datos de telemetría que ha enviado la aplicación mediante TrackTrace(), u [otras plataformas de registro](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="578d0-349">Contains the telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="578d0-350">Vídeo</span><span class="sxs-lookup"><span data-stu-id="578d0-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="578d0-351">Consultas avanzadas:</span><span class="sxs-lookup"><span data-stu-id="578d0-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="578d0-352">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="578d0-352">Next steps</span></span>
* [<span data-ttu-id="578d0-353">Referencia de idioma de Analytics</span><span class="sxs-lookup"><span data-stu-id="578d0-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="578d0-354">[La hoja de referencia rápida de usuarios de SQL](https://aka.ms/sql-analytics) traduce las expresiones más comunes.</span><span class="sxs-lookup"><span data-stu-id="578d0-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates the most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
