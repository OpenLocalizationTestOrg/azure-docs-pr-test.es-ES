---
title: "Paseo aaaA a través del análisis de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Breves ejemplos de todas las consultas principales de hello en el análisis, Hola eficaz herramienta de búsqueda de Application Insights."
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
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a><span data-ttu-id="46498-103">Un paseo por Analytics de Application Insights</span><span class="sxs-lookup"><span data-stu-id="46498-103">A tour of Analytics in Application Insights</span></span>
<span data-ttu-id="46498-104">[Análisis de](app-insights-analytics.md) es característica de búsqueda eficaces Hola de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46498-104">[Analytics](app-insights-analytics.md) is hello powerful search feature of [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="46498-105">En estas páginas se describe el lenguaje de consulta de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="46498-105">These pages describe the Log Analytics query language.</span></span>

* <span data-ttu-id="46498-106">**[Ver vídeo de introducción de hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span><span class="sxs-lookup"><span data-stu-id="46498-106">**[Watch hello introductory video](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.</span></span>
* <span data-ttu-id="46498-107">**[Análisis de prueba con nuestros datos simulados](https://analytics.applicationinsights.io/demo)**  si la aplicación no envía datos tooApplication visión todavía.</span><span class="sxs-lookup"><span data-stu-id="46498-107">**[Test drive Analytics on our simulated data](https://analytics.applicationinsights.io/demo)** if your app isn't sending data tooApplication Insights yet.</span></span>
* <span data-ttu-id="46498-108">**[Hoja de referencia rápida de SQL-usuarios](https://aka.ms/sql-analytics)**  traduce giros de hello más comunes.</span><span class="sxs-lookup"><span data-stu-id="46498-108">**[SQL-users' cheat sheet](https://aka.ms/sql-analytics)** translates hello most common idioms.</span></span>

<span data-ttu-id="46498-109">¡Eche un recorrido a través de algunas tooget consultas básicas que se inició.</span><span class="sxs-lookup"><span data-stu-id="46498-109">Let's take a walk through some basic queries tooget you started.</span></span>

## <a name="connect-tooyour-application-insights-data"></a><span data-ttu-id="46498-110">Conexión de datos de Application Insights tooyour</span><span class="sxs-lookup"><span data-stu-id="46498-110">Connect tooyour Application Insights data</span></span>
<span data-ttu-id="46498-111">Abra Analytics desde la [hoja de información general](app-insights-dashboards.md) de su aplicación en Application Insights:</span><span class="sxs-lookup"><span data-stu-id="46498-111">Open Analytics from your app's [overview blade](app-insights-dashboards.md) in Application Insights:</span></span>

![Abra portal.azure.com, abra su recurso de Application Insights y haga clic en Análisis.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a><span data-ttu-id="46498-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): mostrarme n filas</span><span class="sxs-lookup"><span data-stu-id="46498-113">[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): show me n rows</span></span>
<span data-ttu-id="46498-114">Los puntos de datos que registran las operaciones de usuario (normalmente solicitudes HTTP recibidas mediante la aplicación web) se almacenan en una tabla denominada `requests`.</span><span class="sxs-lookup"><span data-stu-id="46498-114">Data points that log user operations (typically HTTP requests received by your web app) are stored in a table called `requests`.</span></span> <span data-ttu-id="46498-115">Cada fila tiene un punto de datos de telemetría recibido de hello Application Insights SDK en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="46498-115">Each row is a telemetry data point received from hello Application Insights SDK in your app.</span></span>

<span data-ttu-id="46498-116">Empecemos examinando algunas filas de ejemplo de tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="46498-116">Let's start by examining a few sample rows of hello table:</span></span>

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> <span data-ttu-id="46498-118">Coloque el cursor de hello en alguna parte en la instrucción de hello antes de hacer clic en Ir.</span><span class="sxs-lookup"><span data-stu-id="46498-118">Put hello cursor somewhere in hello statement before you click Go.</span></span> <span data-ttu-id="46498-119">Puede dividir una instrucción en varias líneas, pero no incluya líneas en blanco en una instrucción.</span><span class="sxs-lookup"><span data-stu-id="46498-119">You can split a statement over more than one line, but don't put blank lines in a statement.</span></span> <span data-ttu-id="46498-120">Líneas en blanco son una manera cómoda de tookeep varios separan las consultas en la ventana hello.</span><span class="sxs-lookup"><span data-stu-id="46498-120">Blank lines are a convenient way tookeep several separate queries in hello window.</span></span>
>
>

<span data-ttu-id="46498-121">Elija columnas, arrástrelas, agrupe por columnas y filtre:</span><span class="sxs-lookup"><span data-stu-id="46498-121">Choose columns, drag them, group by columns, and filter:</span></span>

![Hacer clic en la selección de columna en la parte superior derecha de los resultados](./media/app-insights-analytics-tour/030.png)

<span data-ttu-id="46498-123">Expanda cualquier detalle de hello toosee de elemento:</span><span class="sxs-lookup"><span data-stu-id="46498-123">Expand any item toosee hello detail:</span></span>

![Seleccione Table (Tabla) y use Configure Columns (Configurar columnas).](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> <span data-ttu-id="46498-125">Haga clic en el encabezado de Hola de una columna toore-ordenar Hola los resultados disponibles en el Explorador de web Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-125">Click hello head of a column toore-order hello results available in hello web browser.</span></span> <span data-ttu-id="46498-126">Pero tenga en cuenta que para un conjunto de resultados grandes, se limita Hola número de filas descargadas toohello explorador.</span><span class="sxs-lookup"><span data-stu-id="46498-126">But be aware that for a large result set, hello number of rows downloaded toohello browser is limited.</span></span> <span data-ttu-id="46498-127">Este modo de ordenación no siempre puede mostrar Hola real mayor o menor de elementos.</span><span class="sxs-lookup"><span data-stu-id="46498-127">Sorting this way doesn't always show you hello actual highest or lowest items.</span></span> <span data-ttu-id="46498-128">elementos toosort usan de forma confiable, hello `top` o `sort` operador.</span><span class="sxs-lookup"><span data-stu-id="46498-128">toosort items reliably, use hello `top` or `sort` operator.</span></span>
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a><span data-ttu-id="46498-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) y [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span><span class="sxs-lookup"><span data-stu-id="46498-129">[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) and [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)</span></span>
<span data-ttu-id="46498-130">`take`es un ejemplo rápido de un resultado de tooget útil, pero muestra filas de tabla de hello en ningún orden concreto.</span><span class="sxs-lookup"><span data-stu-id="46498-130">`take` is useful tooget a quick sample of a result, but it shows rows from hello table in no particular order.</span></span> <span data-ttu-id="46498-131">usar una vista ordenada, tooget `top` (para obtener un ejemplo) o `sort` (a través de hello toda la tabla).</span><span class="sxs-lookup"><span data-stu-id="46498-131">tooget an ordered view, use `top` (for a sample) or `sort` (over hello whole table).</span></span>

<span data-ttu-id="46498-132">Mostrarme Hola n primeras filas, ordenadas por una columna concreta:</span><span class="sxs-lookup"><span data-stu-id="46498-132">Show me hello first n rows, ordered by a particular column:</span></span>

```AIQL

    requests | top 10 by timestamp desc
```

* <span data-ttu-id="46498-133">*Sintaxis*: la mayoría de los operadores tienen parámetros de palabra clave como `by`.</span><span class="sxs-lookup"><span data-stu-id="46498-133">*Syntax:* Most operators have keyword parameters such as `by`.</span></span>
* <span data-ttu-id="46498-134">`desc` = orden descendente, `asc` = orden ascendente.</span><span class="sxs-lookup"><span data-stu-id="46498-134">`desc` = descending order, `asc` = ascending.</span></span>

![](./media/app-insights-analytics-tour/260.png)

<span data-ttu-id="46498-135">`top...` es una manera más eficiente de decir `sort ... | take...`.</span><span class="sxs-lookup"><span data-stu-id="46498-135">`top...` is a more performant way of saying `sort ... | take...`.</span></span> <span data-ttu-id="46498-136">Podríamos haber escrito:</span><span class="sxs-lookup"><span data-stu-id="46498-136">We could have written:</span></span>

```AIQL

    requests | sort by timestamp desc | take 10
```

<span data-ttu-id="46498-137">resultado de Hello sería Hola mismo, pero se ejecutaría un poco más lentamente.</span><span class="sxs-lookup"><span data-stu-id="46498-137">hello result would be hello same, but it would run a bit more slowly.</span></span> <span data-ttu-id="46498-138">(También podría escribir `order`, que es un alias de `sort`).</span><span class="sxs-lookup"><span data-stu-id="46498-138">(You could also write `order`, which is an alias of `sort`.)</span></span>

<span data-ttu-id="46498-139">encabezados de columna de Hello en la vista de tabla de hello también pueden ser utilizados toosort Hola resultados en pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="46498-139">hello column headers in hello table view can also be used toosort hello results on hello screen.</span></span> <span data-ttu-id="46498-140">Pero, por supuesto, si ha usado `take` o `top` tooretrieve parte de una tabla, verá solo reordenar Hola registros que se han recuperado.</span><span class="sxs-lookup"><span data-stu-id="46498-140">But of course, if you've used `take` or `top` tooretrieve just part of a table, you'll only re-order hello records you've retrieved.</span></span>

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a><span data-ttu-id="46498-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrado de una condición.</span><span class="sxs-lookup"><span data-stu-id="46498-141">[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtering on a condition</span></span>

<span data-ttu-id="46498-142">Veamos las solicitudes que devuelven un código de resultado determinado:</span><span class="sxs-lookup"><span data-stu-id="46498-142">Let's see just requests that returned a particular result code:</span></span>

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

<span data-ttu-id="46498-143">Hola `where` operador toma una expresión booleana.</span><span class="sxs-lookup"><span data-stu-id="46498-143">hello `where` operator takes a Boolean expression.</span></span> <span data-ttu-id="46498-144">He aquí algunos puntos clave:</span><span class="sxs-lookup"><span data-stu-id="46498-144">Here are some key points about them:</span></span>

* <span data-ttu-id="46498-145">`and`, `or`: Operadores booleanos</span><span class="sxs-lookup"><span data-stu-id="46498-145">`and`, `or`: Boolean operators</span></span>
* <span data-ttu-id="46498-146">`==`, `<>`, `!=`: igual que y no igual que</span><span class="sxs-lookup"><span data-stu-id="46498-146">`==`, `<>`, `!=` : equal and not equal</span></span>
* <span data-ttu-id="46498-147">`=~`, `!~`: cadena que no distingue entre mayúsculas y minúsculas igual que y no igual que.</span><span class="sxs-lookup"><span data-stu-id="46498-147">`=~`, `!~` : case-insensitive string equal and not equal.</span></span> <span data-ttu-id="46498-148">Hay muchos más operadores de comparación de cadenas.</span><span class="sxs-lookup"><span data-stu-id="46498-148">There are lots more string comparison operators.</span></span>

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a><span data-ttu-id="46498-149">Introducción al tipo correcto de Hola</span><span class="sxs-lookup"><span data-stu-id="46498-149">Getting hello right type</span></span>
<span data-ttu-id="46498-150">Buscar solicitudes incorrectas:</span><span class="sxs-lookup"><span data-stu-id="46498-150">Find unsuccessful requests:</span></span>

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a><span data-ttu-id="46498-151">Hora</span><span class="sxs-lookup"><span data-stu-id="46498-151">Time</span></span>

<span data-ttu-id="46498-152">De forma predeterminada, las consultas son toohello restringido últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="46498-152">By default, your queries are restricted toohello last 24 hours.</span></span> <span data-ttu-id="46498-153">Pero puede cambiar este intervalo:</span><span class="sxs-lookup"><span data-stu-id="46498-153">But you can change this range:</span></span>

![](./media/app-insights-analytics-tour/change-time-range.png)

<span data-ttu-id="46498-154">Invalidar el intervalo de tiempo de hello escribiendo cualquier consulta que se mencionan `timestamp` en una cláusula where.</span><span class="sxs-lookup"><span data-stu-id="46498-154">Override hello time range by writing any query that mentions `timestamp` in a where-clause.</span></span> <span data-ttu-id="46498-155">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="46498-155">For example:</span></span>

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

<span data-ttu-id="46498-156">característica de intervalo de tiempo de Hello es equivalente tooa 'where' inserta cláusula después de cada mención de una de las tablas de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-156">hello time range feature is equivalent tooa 'where' clause inserted after each mention of one of hello source tables.</span></span>

<span data-ttu-id="46498-157">`ago(3d)` significa "hace tres días".</span><span class="sxs-lookup"><span data-stu-id="46498-157">`ago(3d)` means 'three days ago'.</span></span> <span data-ttu-id="46498-158">Otras unidades de tiempo son horas (`2h`, `2.5h`), minutos (`25m`) y segundos (`10s`).</span><span class="sxs-lookup"><span data-stu-id="46498-158">Other units of time include hours (`2h`, `2.5h`), minutes (`25m`), and seconds (`10s`).</span></span>

<span data-ttu-id="46498-159">Otros ejemplos:</span><span class="sxs-lookup"><span data-stu-id="46498-159">Other examples:</span></span>

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

<span data-ttu-id="46498-160">[Referencia de fechas y horas](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span><span class="sxs-lookup"><span data-stu-id="46498-160">[Dates and times reference](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).</span></span>


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a><span data-ttu-id="46498-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): seleccionar, cambiar nombre y calcular columnas</span><span class="sxs-lookup"><span data-stu-id="46498-161">[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): select, rename, and compute columns</span></span>
<span data-ttu-id="46498-162">Use [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick solo las columnas de Hola que desee:</span><span class="sxs-lookup"><span data-stu-id="46498-162">Use [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick out just hello columns you want:</span></span>

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

<span data-ttu-id="46498-163">También puede cambiar el nombre de las columnas y definir otras nuevas:</span><span class="sxs-lookup"><span data-stu-id="46498-163">You can also rename columns and define new ones:</span></span>

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

* <span data-ttu-id="46498-165">Los nombres de columna pueden incluir espacios o símbolos si están entre corchetes, tal como se muestra: `['...']` o `["..."]`</span><span class="sxs-lookup"><span data-stu-id="46498-165">Column names can include spaces or symbols if they are bracketed like this: `['...']` or `["..."]`</span></span>
* <span data-ttu-id="46498-166">`%`es habitual operador de módulo hello.</span><span class="sxs-lookup"><span data-stu-id="46498-166">`%` is hello usual modulo operator.</span></span>
* <span data-ttu-id="46498-167">`1d` (es decir, el dígito uno y luego una "d") es un literal de intervalo de tiempo que significa un día.</span><span class="sxs-lookup"><span data-stu-id="46498-167">`1d` (that's a digit one, then a 'd') is a timespan literal meaning one day.</span></span> <span data-ttu-id="46498-168">Aquí se indican otros literales de intervalo de tiempo: `12h`, `30m`, `10s` y `0.01s`.</span><span class="sxs-lookup"><span data-stu-id="46498-168">Here are some more timespan literals: `12h`, `30m`, `10s`, `0.01s`.</span></span>
* <span data-ttu-id="46498-169">`floor`(alias `bin`) Redondea un valor de profundidad toohello múltiplo más cercano de valor base Hola que proporcione.</span><span class="sxs-lookup"><span data-stu-id="46498-169">`floor` (alias `bin`) rounds a value down toohello nearest multiple of hello base value you provide.</span></span> <span data-ttu-id="46498-170">Por lo que `floor(aTime, 1s)` redondea una hora hacia abajo toohello más cercano de segundo.</span><span class="sxs-lookup"><span data-stu-id="46498-170">So `floor(aTime, 1s)` rounds a time down toohello nearest second.</span></span>

<span data-ttu-id="46498-171">Las expresiones pueden incluir todos los operadores habituales de hello (`+`, `-`,...), y no hay una gama de funciones útiles.</span><span class="sxs-lookup"><span data-stu-id="46498-171">Expressions can include all hello usual operators (`+`, `-`, ...), and there's a range of useful functions.</span></span>

## <a name="extend"></a><span data-ttu-id="46498-172">Extend</span><span class="sxs-lookup"><span data-stu-id="46498-172">Extend</span></span>
<span data-ttu-id="46498-173">Si solo desea tooadd toohello de las columnas existentes, utilice [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span><span class="sxs-lookup"><span data-stu-id="46498-173">If you just want tooadd columns toohello existing ones, use [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

<span data-ttu-id="46498-174">Usar [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) es menos detallado [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) si desea tookeep Hola a todas las columnas existentes.</span><span class="sxs-lookup"><span data-stu-id="46498-174">Using [`extend`](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) is less verbose than [`project`](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) if you want tookeep all hello existing columns.</span></span>

### <a name="convert-toolocal-time"></a><span data-ttu-id="46498-175">Convertir la hora de toolocal</span><span class="sxs-lookup"><span data-stu-id="46498-175">Convert toolocal time</span></span>

<span data-ttu-id="46498-176">Las marcas de tiempo siempre se expresan en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="46498-176">Timestamps are always in UTC.</span></span> <span data-ttu-id="46498-177">Por lo que si se encuentra en hello nos suroeste y es temporada de invierno, podría como esta:</span><span class="sxs-lookup"><span data-stu-id="46498-177">So if you're on hello US Pacific coast and it's winter, you might like this:</span></span>

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a><span data-ttu-id="46498-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): adición de grupos de filas</span><span class="sxs-lookup"><span data-stu-id="46498-178">[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): aggregate groups of rows</span></span>
<span data-ttu-id="46498-179">`Summarize` aplica una *función de agregación* específica sobre grupos de filas.</span><span class="sxs-lookup"><span data-stu-id="46498-179">`Summarize` applies a specified *aggregation function* over groups of rows.</span></span>

<span data-ttu-id="46498-180">Por ejemplo, hello tarda la aplicación web toorespond tooa solicitud se notifica en el campo de hello `duration`.</span><span class="sxs-lookup"><span data-stu-id="46498-180">For example, hello time your web app takes toorespond tooa request is reported in hello field `duration`.</span></span> <span data-ttu-id="46498-181">Veamos medio de respuesta de hello tooall solicitudes de tiempo:</span><span class="sxs-lookup"><span data-stu-id="46498-181">Let's see hello average response time tooall requests:</span></span>

![](./media/app-insights-analytics-tour/410.png)

<span data-ttu-id="46498-182">O se puede separar resultado de hello en las solicitudes de nombres diferentes:</span><span class="sxs-lookup"><span data-stu-id="46498-182">Or we could separate hello result into requests of different names:</span></span>

![](./media/app-insights-analytics-tour/420.png)

<span data-ttu-id="46498-183">`Summarize`recopila Hola puntos de datos de flujo de hello en grupos para qué hello `by` cláusula evalúa igualmente.</span><span class="sxs-lookup"><span data-stu-id="46498-183">`Summarize` collects hello data points in hello stream into groups for which hello `by` clause evaluates equally.</span></span> <span data-ttu-id="46498-184">Cada valor de hello `by` expresión - cada nombre de la operación en hello ejemplo anterior - da como resultado de una fila en la tabla de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-184">Each value in hello `by` expression - each operation name in hello above example - results in a row in hello result table.</span></span>

<span data-ttu-id="46498-185">O bien, podríamos agrupar los resultados en función de la hora del día:</span><span class="sxs-lookup"><span data-stu-id="46498-185">Or we could group results by time of day:</span></span>

![](./media/app-insights-analytics-tour/430.png)

<span data-ttu-id="46498-186">Tenga en cuenta cómo usamos hello `bin` (función) (también conocido como `floor`).</span><span class="sxs-lookup"><span data-stu-id="46498-186">Notice how we're using hello `bin` function (aka `floor`).</span></span> <span data-ttu-id="46498-187">Si solo usáramos `by timestamp`, cada fila de entrada terminaría en su pequeño grupo.</span><span class="sxs-lookup"><span data-stu-id="46498-187">If we just used `by timestamp`, every input row would end up in its own little group.</span></span> <span data-ttu-id="46498-188">Para cualquier valor escalar continua veces like o números, tenemos intervalo continuo de hello toobreak en un número de valores discretos fáciles de administrar.</span><span class="sxs-lookup"><span data-stu-id="46498-188">For any continuous scalar like times or numbers, we have toobreak hello continuous range into a manageable number of discrete values.</span></span> <span data-ttu-id="46498-189">`bin`-que es simplemente Hola familiarizado redondeo en profundidad `floor` función; es toodo de manera más fácil de Hola que.</span><span class="sxs-lookup"><span data-stu-id="46498-189">`bin` - which is just hello familiar rounding-down `floor` function - is hello easiest way toodo that.</span></span>

<span data-ttu-id="46498-190">Podemos usar Hola mismos intervalos de tooreduce técnica de cadenas:</span><span class="sxs-lookup"><span data-stu-id="46498-190">We can use hello same technique tooreduce ranges of strings:</span></span>

![](./media/app-insights-analytics-tour/440.png)

<span data-ttu-id="46498-191">Tenga en cuenta que puede usar `name=` tooset nombre de Hola de una columna de resultados, en las expresiones de agregado de Hola o por la cláusula de Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-191">Notice that you can use `name=` tooset hello name of a result column, either in hello aggregation expressions or hello by-clause.</span></span>

## <a name="counting-sampled-data"></a><span data-ttu-id="46498-192">Recuento de datos muestreados</span><span class="sxs-lookup"><span data-stu-id="46498-192">Counting sampled data</span></span>
<span data-ttu-id="46498-193">`sum(itemCount)`es recomendable de hello agregación toocount eventos.</span><span class="sxs-lookup"><span data-stu-id="46498-193">`sum(itemCount)` is hello recommended aggregation toocount events.</span></span> <span data-ttu-id="46498-194">En muchos casos, itemCount == 1, por lo que la función de hello simplemente cuenta el número de Hola de filas en un grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-194">In many cases, itemCount==1, so hello function simply counts up hello number of rows in hello group.</span></span> <span data-ttu-id="46498-195">Pero cuando [muestreo](app-insights-sampling.md) está en funcionamiento, sólo una fracción de eventos de hello original se conservan como puntos de datos de Application Insights, por lo que para cada punto de datos que se ven, hay `itemCount` eventos.</span><span class="sxs-lookup"><span data-stu-id="46498-195">But when [sampling](app-insights-sampling.md) is in operation, only a fraction of hello original events are retained as data points in Application Insights, so that for each data point you see, there are `itemCount` events.</span></span>

<span data-ttu-id="46498-196">Por ejemplo, si el muestreo descarta el 75% de los eventos originales de hello y, a continuación, itemCount == 4 en registros de hello conservan: es decir, para cada registro retenido, había cuatro registros originales.</span><span class="sxs-lookup"><span data-stu-id="46498-196">For example, if sampling discards 75% of hello original events, then itemCount==4 in hello retained records - that is, for every retained record, there were four original records.</span></span>

<span data-ttu-id="46498-197">Muestreo adaptativo hace itemCount toobe superior durante los períodos de la aplicación cuando se utilice con un alto grado.</span><span class="sxs-lookup"><span data-stu-id="46498-197">Adaptive sampling causes itemCount toobe higher during periods when your application is being heavily used.</span></span>

<span data-ttu-id="46498-198">Por lo tanto, se suma de itemCount ofrece una buena estimación del número original de Hola de eventos.</span><span class="sxs-lookup"><span data-stu-id="46498-198">Summing up itemCount therefore gives a good estimate of hello original number of events.</span></span>

![](./media/app-insights-analytics-tour/510.png)

<span data-ttu-id="46498-199">También hay un `count()` agregación (y una operación de recuento), para los casos donde realmente desea toocount Hola número de filas de un grupo.</span><span class="sxs-lookup"><span data-stu-id="46498-199">There's also a `count()` aggregation (and a count operation), for cases where you really do want toocount hello number of rows in a group.</span></span>

<span data-ttu-id="46498-200">Existe una gama de [funciones de agregación](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span><span class="sxs-lookup"><span data-stu-id="46498-200">There's a range of [aggregation functions](https://docs.loganalytics.io/learn/tutorials/aggregations.html).</span></span>

## <a name="charting-hello-results"></a><span data-ttu-id="46498-201">Gráficos de resultados de Hola</span><span class="sxs-lookup"><span data-stu-id="46498-201">Charting hello results</span></span>
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

<span data-ttu-id="46498-202">De forma predeterminada, los resultados se muestran como una tabla:</span><span class="sxs-lookup"><span data-stu-id="46498-202">By default, results display as a table:</span></span>

![](./media/app-insights-analytics-tour/225.png)

<span data-ttu-id="46498-203">Podemos hacer un mejor rendimiento que la vista de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-203">We can do better than hello table view.</span></span> <span data-ttu-id="46498-204">Echemos un vistazo a los resultados de hello en la vista de gráfico de hello con la opción de barra vertical de hello:</span><span class="sxs-lookup"><span data-stu-id="46498-204">Let's look at hello results in hello chart view with hello vertical bar option:</span></span>

![Haga clic Chart (Gráfico) y después elija Vertical bar chart (Gráfico de barras verticales) y asigne los ejes x e y.](./media/app-insights-analytics-tour/230.png)

<span data-ttu-id="46498-206">Tenga en cuenta que, aunque se no ordenación resultados de Hola por hora (como puede ver en la visualización de la tabla de hello), Hola gráfico siempre muestran fechas y horas en el orden correcto.</span><span class="sxs-lookup"><span data-stu-id="46498-206">Notice that although we didn't sort hello results by time (as you can see in hello table display), hello chart display always shows datetimes in correct order.</span></span>


## <a name="timecharts"></a><span data-ttu-id="46498-207">Gráficos de tiempo</span><span class="sxs-lookup"><span data-stu-id="46498-207">Timecharts</span></span>
<span data-ttu-id="46498-208">Mostrar cuántos eventos hay cada hora:</span><span class="sxs-lookup"><span data-stu-id="46498-208">Show how many events there are each hour:</span></span>

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

<span data-ttu-id="46498-209">Seleccione la opción de visualización del gráfico de hello:</span><span class="sxs-lookup"><span data-stu-id="46498-209">Select hello Chart display option:</span></span>

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a><span data-ttu-id="46498-211">Varias series</span><span class="sxs-lookup"><span data-stu-id="46498-211">Multiple series</span></span>
<span data-ttu-id="46498-212">Varias expresiones en hello `summarize` cláusula crea varias columnas.</span><span class="sxs-lookup"><span data-stu-id="46498-212">Multiple expressions in hello `summarize` clause creates multiple columns.</span></span>

<span data-ttu-id="46498-213">Varias expresiones en hello `by` cláusula crea varias filas, una para cada combinación de valores.</span><span class="sxs-lookup"><span data-stu-id="46498-213">Multiple expressions in hello `by` clause creates multiple rows, one for each combination of values.</span></span>

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabla de solicitudes por hora y ubicación](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a><span data-ttu-id="46498-215">Segmentación de un gráfico por dimensiones</span><span class="sxs-lookup"><span data-stu-id="46498-215">Segment a chart by dimensions</span></span>
<span data-ttu-id="46498-216">Si se pueden toosplit usado Hola datos numéricos en series independientes de los puntos de gráfico una tabla que tiene una columna de cadenas y una columna numérica, cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-216">If you chart a table that has a string column and a numeric column, hello string can be used toosplit hello numeric data into separate series of points.</span></span> <span data-ttu-id="46498-217">Si hay más de una columna de cadena, puede elegir qué toouse de columna como discriminador Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-217">If there's more than one string column, you can choose which column toouse as hello discriminator.</span></span>

![Segmentación de un gráfico de análisis](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a><span data-ttu-id="46498-219">Tasa de devolución</span><span class="sxs-lookup"><span data-stu-id="46498-219">Bounce rate</span></span>

<span data-ttu-id="46498-220">Convertir una toouse de cadena booleano tooa como un discriminador:</span><span class="sxs-lookup"><span data-stu-id="46498-220">Convert a boolean tooa string toouse it as a discriminator:</span></span>

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

### <a name="display-multiple-metrics"></a><span data-ttu-id="46498-221">Muestra de varias métricas</span><span class="sxs-lookup"><span data-stu-id="46498-221">Display multiple metrics</span></span>
<span data-ttu-id="46498-222">Si el gráfico de una tabla que tiene más de una columna numérica, en la marca de tiempo de suma toohello, puede mostrar cualquier combinación de ellos.</span><span class="sxs-lookup"><span data-stu-id="46498-222">If you chart a table that has more than one numeric column, in addition toohello timestamp, you can display any combination of them.</span></span>

![Segmentación de un gráfico de análisis](./media/app-insights-analytics-tour/110.png)

<span data-ttu-id="46498-224">Debe seleccionar **Don't Split** (No dividir) para poder seleccionar varias columnas numéricas.</span><span class="sxs-lookup"><span data-stu-id="46498-224">You must select **Don't Split** before you can select multiple numeric columns.</span></span> <span data-ttu-id="46498-225">No se divide por una columna de cadenas en hello mismo tiempo como mostrar más de una columna numérica.</span><span class="sxs-lookup"><span data-stu-id="46498-225">You can't split by a string column at hello same time as displaying more than one numeric column.</span></span>

## <a name="daily-average-cycle"></a><span data-ttu-id="46498-226">Ciclo medio diario</span><span class="sxs-lookup"><span data-stu-id="46498-226">Daily average cycle</span></span>
<span data-ttu-id="46498-227">¿Cómo varía en uso en día promedio Hola?</span><span class="sxs-lookup"><span data-stu-id="46498-227">How does usage vary over hello average day?</span></span>

<span data-ttu-id="46498-228">Solicitudes de recuento por tiempo Hola módulo un día, segmentan en horas:</span><span class="sxs-lookup"><span data-stu-id="46498-228">Count requests by hello time modulo one day, binned into hours:</span></span>

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
> <span data-ttu-id="46498-230">Tenga en cuenta que actualmente tenemos tooconvert tiempo duraciones toodatetimes en orden toodisplay en un gráfico de líneas.</span><span class="sxs-lookup"><span data-stu-id="46498-230">Notice that we currently have tooconvert time durations toodatetimes in order toodisplay on a line chart.</span></span>
>
>

## <a name="compare-multiple-daily-series"></a><span data-ttu-id="46498-231">Comparación de varias series diarias</span><span class="sxs-lookup"><span data-stu-id="46498-231">Compare multiple daily series</span></span>
<span data-ttu-id="46498-232">¿Cómo varía en uso con el tiempo de hello del día en distintos países?</span><span class="sxs-lookup"><span data-stu-id="46498-232">How does usage vary over hello time of day in different countries?</span></span>

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

## <a name="plot-a-distribution"></a><span data-ttu-id="46498-234">Trazado de una distribución</span><span class="sxs-lookup"><span data-stu-id="46498-234">Plot a distribution</span></span>
<span data-ttu-id="46498-235">¿Cuántas sesiones existen de longitudes diferentes?</span><span class="sxs-lookup"><span data-stu-id="46498-235">How many sessions are there of different lengths?</span></span>

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

<span data-ttu-id="46498-236">Hola la última línea es necesario tooconvert toodatetime.</span><span class="sxs-lookup"><span data-stu-id="46498-236">hello last line is required tooconvert toodatetime.</span></span> <span data-ttu-id="46498-237">Actualmente Hola x eje de un gráfico se muestra como un valor escalar solo si es una fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="46498-237">Currently hello x axis of a chart is displayed as a scalar only if it is a datetime.</span></span>

<span data-ttu-id="46498-238">Hola `where` cláusula excluye las sesiones Monoestable (sessionDuration == 0) y conjuntos de Hola longitud del eje x de Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-238">hello `where` clause excludes one-shot sessions (sessionDuration==0) and sets hello length of hello x-axis.</span></span>

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[<span data-ttu-id="46498-239">Percentiles</span><span class="sxs-lookup"><span data-stu-id="46498-239">Percentiles</span></span>](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
<span data-ttu-id="46498-240">¿Qué intervalos de duraciones cubren diferentes porcentajes de sesiones?</span><span class="sxs-lookup"><span data-stu-id="46498-240">What ranges of durations cover different percentages of sessions?</span></span>

<span data-ttu-id="46498-241">Usar hello por encima de la consulta, pero reemplace Hola última línea:</span><span class="sxs-lookup"><span data-stu-id="46498-241">Use hello above query, but replace hello last line:</span></span>

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

<span data-ttu-id="46498-242">Eliminamos límite superior de Hola Hola donde cláusula, en orden tooget corregir cifras incluidas todas las sesiones con más de una solicitud:</span><span class="sxs-lookup"><span data-stu-id="46498-242">We also removed hello upper limit in hello where clause, in order tooget correct figures including all sessions with more than one request:</span></span>

![result](./media/app-insights-analytics-tour/180.png)

<span data-ttu-id="46498-244">De lo que podemos ver que:</span><span class="sxs-lookup"><span data-stu-id="46498-244">From which we can see that:</span></span>

* <span data-ttu-id="46498-245">El 5 % de las sesiones tienen una duración de menos de 3 minutos 34 s;</span><span class="sxs-lookup"><span data-stu-id="46498-245">5% of sessions have a duration of less than 3 minutes 34s;</span></span>
* <span data-ttu-id="46498-246">El 50 % de las sesiones dura menos de 36 minutos;</span><span class="sxs-lookup"><span data-stu-id="46498-246">50% of sessions last less than 36 minutes;</span></span>
* <span data-ttu-id="46498-247">El 5 % de las sesiones dura más de 7 días.</span><span class="sxs-lookup"><span data-stu-id="46498-247">5% of sessions last more than 7 days</span></span>

<span data-ttu-id="46498-248">tooget un desglose independiente para cada país, solo tenemos toobring hello client_CountryOrRegion columna por separado a través de los operadores de resumen:</span><span class="sxs-lookup"><span data-stu-id="46498-248">tooget a separate breakdown for each country, we just have toobring hello client_CountryOrRegion column separately through both summarize operators:</span></span>

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

## <a name="join"></a><span data-ttu-id="46498-249">Unión</span><span class="sxs-lookup"><span data-stu-id="46498-249">Join</span></span>
<span data-ttu-id="46498-250">Tenemos que tooseveral acceso a tablas, incluidas las excepciones y las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="46498-250">We have access tooseveral tables, including requests and exceptions.</span></span>

<span data-ttu-id="46498-251">toofind Hola excepciones relacionadas tooa solicitud que devuelve una respuesta de error, se pueden combinar tablas de hello en `session_Id`:</span><span class="sxs-lookup"><span data-stu-id="46498-251">toofind hello exceptions related tooa request that returned a failure response, we can join hello tables on `session_Id`:</span></span>

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


<span data-ttu-id="46498-252">Es recomendable toouse `project` tooselect columnas de hello solo es necesario antes de realizar Hola combinación.</span><span class="sxs-lookup"><span data-stu-id="46498-252">It's good practice toouse `project` tooselect just hello columns we need before performing hello join.</span></span>
<span data-ttu-id="46498-253">Hola mismas cláusulas, cambiamos el nombre de columna de marca de tiempo de Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-253">In hello same clauses, we rename hello timestamp column.</span></span>

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a><span data-ttu-id="46498-254">[Permiten](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): asignar una variable de resultado tooa</span><span class="sxs-lookup"><span data-stu-id="46498-254">[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): Assign a result tooa variable</span></span>

<span data-ttu-id="46498-255">Use `let` tooseparate partes de saludo de la expresión anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-255">Use `let` tooseparate out hello parts of hello previous expression.</span></span> <span data-ttu-id="46498-256">resultados de Hello son iguales:</span><span class="sxs-lookup"><span data-stu-id="46498-256">hello results are unchanged:</span></span>

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> <span data-ttu-id="46498-257">En el cliente de análisis de hello, no incluya líneas en blanco entre las partes de Hola de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-257">In hello Analytics client, don't put blank lines between hello parts of hello query.</span></span> <span data-ttu-id="46498-258">Asegúrese de tooexecute seguro todos del mismo.</span><span class="sxs-lookup"><span data-stu-id="46498-258">Make sure tooexecute all of it.</span></span>
>

<span data-ttu-id="46498-259">Use `toscalar` tooconvert un valor de tooa de celda de tabla única:</span><span class="sxs-lookup"><span data-stu-id="46498-259">Use `toscalar` tooconvert a single table cell tooa value:</span></span>

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


### <a name="functions"></a><span data-ttu-id="46498-260">Functions</span><span class="sxs-lookup"><span data-stu-id="46498-260">Functions</span></span>

<span data-ttu-id="46498-261">Use *permiten* toodefine una función:</span><span class="sxs-lookup"><span data-stu-id="46498-261">Use *Let* toodefine a function:</span></span>

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a><span data-ttu-id="46498-262">Acceso a objetos anidados</span><span class="sxs-lookup"><span data-stu-id="46498-262">Accessing nested objects</span></span>
<span data-ttu-id="46498-263">Se puede acceder fácilmente a los objetos anidados.</span><span class="sxs-lookup"><span data-stu-id="46498-263">Nested objects can be accessed easily.</span></span> <span data-ttu-id="46498-264">Por ejemplo, en la secuencia de excepciones de hello, puede ver objetos estructurados similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="46498-264">For example, in hello exceptions stream you can see structured objects like this:</span></span>

![result](./media/app-insights-analytics-tour/520.png)

<span data-ttu-id="46498-266">Es posible simplificar eligiendo Propiedades Hola que le interesa:</span><span class="sxs-lookup"><span data-stu-id="46498-266">You can flatten it by choosing hello properties you're interested in:</span></span>

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="46498-267">Tenga en cuenta que necesita el tipo adecuado de toocast Hola resultado toohello.</span><span class="sxs-lookup"><span data-stu-id="46498-267">Note that you need toocast hello result toohello appropriate type.</span></span>


## <a name="custom-properties-and-measurements"></a><span data-ttu-id="46498-268">Propiedades y medidas personalizadas</span><span class="sxs-lookup"><span data-stu-id="46498-268">Custom properties and measurements</span></span>
<span data-ttu-id="46498-269">Si la aplicación se asocia [dimensiones personalizadas (propiedades) y las medidas personalizadas](app-insights-api-custom-events-metrics.md#properties) tooevents, a continuación, se verán en hello `customDimensions` y `customMeasurements` objetos.</span><span class="sxs-lookup"><span data-stu-id="46498-269">If your application attaches [custom dimensions (properties) and custom measurements](app-insights-api-custom-events-metrics.md#properties) tooevents, then you will see them in hello `customDimensions` and `customMeasurements` objects.</span></span>

<span data-ttu-id="46498-270">Por ejemplo, si la aplicación incluye:</span><span class="sxs-lookup"><span data-stu-id="46498-270">For example, if your app includes:</span></span>

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

<span data-ttu-id="46498-271">tooextract estos valores en el análisis:</span><span class="sxs-lookup"><span data-stu-id="46498-271">tooextract these values in Analytics:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

<span data-ttu-id="46498-272">tooverify si es una dimensión personalizada de un tipo determinado:</span><span class="sxs-lookup"><span data-stu-id="46498-272">tooverify whether a custom dimension is of a particular type:</span></span>

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a><span data-ttu-id="46498-273">Paneles</span><span class="sxs-lookup"><span data-stu-id="46498-273">Dashboards</span></span>
<span data-ttu-id="46498-274">Puede anclar el panel de resultados tooa en orden toobring juntos todos los gráficos y sus tablas más importantes.</span><span class="sxs-lookup"><span data-stu-id="46498-274">You can pin your results tooa dashboard in order toobring together all your most important charts and tables.</span></span>

* <span data-ttu-id="46498-275">[Panel compartido Azure](app-insights-dashboards.md#share-dashboards): haga clic en el icono de alfiler Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-275">[Azure shared dashboard](app-insights-dashboards.md#share-dashboards): Click hello pin icon.</span></span> <span data-ttu-id="46498-276">Antes de hacerlo, debe tener un panel compartido.</span><span class="sxs-lookup"><span data-stu-id="46498-276">Before you do this, you must have a shared dashboard.</span></span> <span data-ttu-id="46498-277">Hola portal de Azure, abrir o crear un panel y haga clic en compartir.</span><span class="sxs-lookup"><span data-stu-id="46498-277">In hello Azure portal, open or create a dashboard and click Share.</span></span>
* <span data-ttu-id="46498-278">[Panel de Power BI](app-insights-export-power-bi.md): haga clic en Exportar, Consulta de Power BI.</span><span class="sxs-lookup"><span data-stu-id="46498-278">[Power BI dashboard](app-insights-export-power-bi.md): Click Export, Power BI Query.</span></span> <span data-ttu-id="46498-279">Una ventaja de esta alternativa es que puede mostrar la consulta junto con otros resultados procedentes de una gran variedad de orígenes.</span><span class="sxs-lookup"><span data-stu-id="46498-279">An advantage of this alternative is that you can display your query alongside other results from a wide range of sources.</span></span>

## <a name="combine-with-imported-data"></a><span data-ttu-id="46498-280">Combinación con datos importados</span><span class="sxs-lookup"><span data-stu-id="46498-280">Combine with imported data</span></span>

<span data-ttu-id="46498-281">Informes de análisis un aspecto excelentes en el panel de hello, pero a veces desea tootranslate Hola datos tooa forma por más.</span><span class="sxs-lookup"><span data-stu-id="46498-281">Analytics reports look great on hello dashboard, but sometimes you want tootranslate hello data tooa more digestible form.</span></span> <span data-ttu-id="46498-282">Por ejemplo, suponga que los usuarios autenticados se identifican en la telemetría de hello mediante un alias.</span><span class="sxs-lookup"><span data-stu-id="46498-282">For example, suppose your authenticated users are identified in hello telemetry by an alias.</span></span> <span data-ttu-id="46498-283">Le gustaría tooshow nombres su real en los resultados.</span><span class="sxs-lookup"><span data-stu-id="46498-283">You'd like tooshow their real names in your results.</span></span> <span data-ttu-id="46498-284">toodo, necesita un archivo CSV que se asigna desde los nombres reales de hello alias toohello.</span><span class="sxs-lookup"><span data-stu-id="46498-284">toodo this, you need a CSV file that maps from hello aliases toohello real names.</span></span>

<span data-ttu-id="46498-285">Puede importar un archivo de datos y usarla como cualquiera de las tablas estándar hello (solicitudes, excepciones etc.).</span><span class="sxs-lookup"><span data-stu-id="46498-285">You can import a data file and use it just like any of hello standard tables (requests, exceptions, and so on).</span></span> <span data-ttu-id="46498-286">Puede consultarla por sí sola o combinarla con otras tablas.</span><span class="sxs-lookup"><span data-stu-id="46498-286">Either query it on its own, or join it with other tables.</span></span> <span data-ttu-id="46498-287">Por ejemplo, si tiene una tabla denominada usermap y tiene columnas `realName` y `userId`, puede usar tootranslate hello `user_AuthenticatedId` campo telemetría de solicitud de hello:</span><span class="sxs-lookup"><span data-stu-id="46498-287">For example, if you have a table named usermap, and it has columns `realName` and `userId`, then you can use it tootranslate hello `user_AuthenticatedId` field in hello request telemetry:</span></span>

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

<span data-ttu-id="46498-288">tooimport una tabla, en la hoja de esquema de hello, en **otros orígenes de datos**, siga Hola instrucciones tooadd un nuevo origen de datos, mediante la carga de una muestra de los datos.</span><span class="sxs-lookup"><span data-stu-id="46498-288">tooimport a table, in hello Schema blade, under **Other Data Sources**, follow hello instructions tooadd a new data source, by uploading a sample of your data.</span></span> <span data-ttu-id="46498-289">A continuación, puede utilizar estas tablas de tooupload de definición.</span><span class="sxs-lookup"><span data-stu-id="46498-289">Then you can use this definition tooupload tables.</span></span>

<span data-ttu-id="46498-290">la característica de importación de Hello está actualmente en vista previa, por lo que inicialmente se verá un vínculo "Póngase en contacto con nosotros" bajo "Otros orígenes de datos."</span><span class="sxs-lookup"><span data-stu-id="46498-290">hello import feature is currently in preview, so you will initially see a "Contact us" link under "Other data sources."</span></span> <span data-ttu-id="46498-291">Utilice este toosign toohello programa de vista previa y vínculo de hello, a continuación, se reemplazará por un botón "Agregar nuevo origen de datos".</span><span class="sxs-lookup"><span data-stu-id="46498-291">Use this toosign up toohello preview program, and hello link will then be replaced by an "Add new data source" button.</span></span>


## <a name="tables"></a><span data-ttu-id="46498-292">Tablas</span><span class="sxs-lookup"><span data-stu-id="46498-292">Tables</span></span>
<span data-ttu-id="46498-293">secuencia de Hola de telemetría recibido de la aplicación sea accesible a través de varias tablas.</span><span class="sxs-lookup"><span data-stu-id="46498-293">hello stream of telemetry received from your app is accessible through several tables.</span></span> <span data-ttu-id="46498-294">esquema de Hola de propiedades disponibles para cada tabla es visible a la izquierda de Hola de ventana hello.</span><span class="sxs-lookup"><span data-stu-id="46498-294">hello schema of properties available for each table is visible at hello left of hello window.</span></span>

### <a name="requests-table"></a><span data-ttu-id="46498-295">Tabla de solicitudes</span><span class="sxs-lookup"><span data-stu-id="46498-295">Requests table</span></span>
<span data-ttu-id="46498-296">Recuento de las solicitudes HTTP tooyour web app y segmento por nombre de página:</span><span class="sxs-lookup"><span data-stu-id="46498-296">Count HTTP requests tooyour web app and segment by page name:</span></span>

![Contar solicitudes segmentadas por nombre](./media/app-insights-analytics-tour/analytics-count-requests.png)

<span data-ttu-id="46498-298">Busque solicitudes de Hola que producirá un error en la mayoría:</span><span class="sxs-lookup"><span data-stu-id="46498-298">Find hello requests that fail most:</span></span>

![Contar solicitudes segmentadas por nombre](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a><span data-ttu-id="46498-300">Tabla de eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="46498-300">Custom events table</span></span>
<span data-ttu-id="46498-301">Si usa [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend sus propios eventos, puede leerlos desde esta tabla.</span><span class="sxs-lookup"><span data-stu-id="46498-301">If you use [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend your own events, you can read them from this table.</span></span>

<span data-ttu-id="46498-302">Veamos un ejemplo en el que el código de aplicación contiene estas líneas:</span><span class="sxs-lookup"><span data-stu-id="46498-302">Let's take an example where your app code contains these lines:</span></span>

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

<span data-ttu-id="46498-303">Muestra la frecuencia de Hola de estos eventos:</span><span class="sxs-lookup"><span data-stu-id="46498-303">Display hello frequency of these events:</span></span>

![Mostrar la tasa de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

<span data-ttu-id="46498-305">Extraer las medidas y dimensiones de eventos de hello:</span><span class="sxs-lookup"><span data-stu-id="46498-305">Extract measurements and dimensions from hello events:</span></span>

![Mostrar la tasa de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a><span data-ttu-id="46498-307">Tabla de métricas personalizadas</span><span class="sxs-lookup"><span data-stu-id="46498-307">Custom metrics table</span></span>
<span data-ttu-id="46498-308">Si utilizas [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend sus propios valores de métrica, encontrará sus resultados en hello **customMetrics** secuencia.</span><span class="sxs-lookup"><span data-stu-id="46498-308">If you are using [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend your own metric values, you’ll find its results in hello **customMetrics** stream.</span></span> <span data-ttu-id="46498-309">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="46498-309">For example:</span></span>  

![Métricas personalizadas en Application Insights Analytics](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> <span data-ttu-id="46498-311">En [Explorer métricas](app-insights-metrics-explorer.md), todas las medidas personalizadas de tipo tooany adjunto de telemetría aparecen juntas en la hoja de métricas de hello junto con las métricas que se envían con `TrackMetric()`.</span><span class="sxs-lookup"><span data-stu-id="46498-311">In [Metrics Explorer](app-insights-metrics-explorer.md), all custom measurements attached tooany type of telemetry appear together in hello metrics blade along with metrics sent using `TrackMetric()`.</span></span> <span data-ttu-id="46498-312">Pero en el análisis, las medidas personalizadas siguen siendo adjunta toowhichever tipo de telemetría que se llevaron a en - eventos o las solicitudes etc. - mientras métricas enviadas por TrackMetric aparecen en su propia secuencia.</span><span class="sxs-lookup"><span data-stu-id="46498-312">But in Analytics, custom measurements are still attached toowhichever type of telemetry they were carried on - events or requests, and so on - while metrics sent by TrackMetric appear in their own stream.</span></span>
>
>

### <a name="performance-counters-table"></a><span data-ttu-id="46498-313">Tabla de contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="46498-313">Performance counters table</span></span>
<span data-ttu-id="46498-314">Los [contadores de rendimiento](app-insights-performance-counters.md) muestran métricas del sistema básico de la aplicación, como CPU, memoria y la utilización de la red.</span><span class="sxs-lookup"><span data-stu-id="46498-314">[Performance counters](app-insights-performance-counters.md) show you basic system metrics for your app, such as CPU, memory, and network utilization.</span></span> <span data-ttu-id="46498-315">Puede configurar Hola SDK toosend adicionales, incluidos sus propios contadores.</span><span class="sxs-lookup"><span data-stu-id="46498-315">You can configure hello SDK toosend additional counters, including your own custom counters.</span></span>

<span data-ttu-id="46498-316">Hola **performanceCounters** esquema expone hello `category`, `counter` nombre, y `instance` nombre de cada contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="46498-316">hello **performanceCounters** schema exposes hello `category`, `counter` name, and `instance` name of each performance counter.</span></span> <span data-ttu-id="46498-317">Nombres de instancia de contador son solo los contadores de rendimiento de toosome aplicables y suelen indican nombre Hola de hello proceso toowhich Hola recuento está relacionada con.</span><span class="sxs-lookup"><span data-stu-id="46498-317">Counter instance names are only applicable toosome performance counters, and typically indicate hello name of hello process toowhich hello count relates.</span></span> <span data-ttu-id="46498-318">En la telemetría de Hola para cada aplicación, verá solo los contadores de Hola para esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="46498-318">In hello telemetry for each application, you’ll see only hello counters for that application.</span></span> <span data-ttu-id="46498-319">Por ejemplo, toosee qué contadores están disponibles:</span><span class="sxs-lookup"><span data-stu-id="46498-319">For example, toosee what counters are available:</span></span>

![Contadores de rendimiento en Application Insights Analytics](./media/app-insights-analytics-tour/analytics-performance-counters.png)

<span data-ttu-id="46498-321">un gráfico de memoria disponible a través de hello tooget periodo seleccionado:</span><span class="sxs-lookup"><span data-stu-id="46498-321">tooget a chart of available memory over hello selected period:</span></span>

![Gráfico de tiempo de la memoria in Application Insights Analytics](./media/app-insights-analytics-tour/analytics-available-memory.png)

<span data-ttu-id="46498-323">Al igual que otros telemetría **performanceCounters** también tiene una columna `cloud_RoleInstance` que indica la identidad de Hola de máquina de host de hello en el que se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="46498-323">Like other telemetry, **performanceCounters** also has a column `cloud_RoleInstance` that indicates hello identity of hello host machine on which your app is running.</span></span> <span data-ttu-id="46498-324">Por ejemplo, toocompare Hola rendimiento de la aplicación en equipos diferentes de hello:</span><span class="sxs-lookup"><span data-stu-id="46498-324">For example, toocompare hello performance of your app on hello different machines:</span></span>

![Rendimiento segmentado por instancia de rol en Application Insights Analytics](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a><span data-ttu-id="46498-326">Tabla de excepciones</span><span class="sxs-lookup"><span data-stu-id="46498-326">Exceptions table</span></span>
<span data-ttu-id="46498-327">[Las excepciones que notifica la aplicación](app-insights-asp-net-exceptions.md) están disponibles en esta tabla.</span><span class="sxs-lookup"><span data-stu-id="46498-327">[Exceptions reported by your app](app-insights-asp-net-exceptions.md) are available in this table.</span></span>

<span data-ttu-id="46498-328">toofind Hola solicitud HTTP que estaba controlando la aplicación cuando se produce la excepción de hello, combine operation_Id:</span><span class="sxs-lookup"><span data-stu-id="46498-328">toofind hello HTTP request that your app was handling when hello exception was raised, join on operation_Id:</span></span>

![Combinar excepciones con solicitudes en operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a><span data-ttu-id="46498-330">Tabla de intervalos de explorador</span><span class="sxs-lookup"><span data-stu-id="46498-330">Browser timings table</span></span>
<span data-ttu-id="46498-331">`browserTimings` muestra los datos de carga de las páginas recopilados en los exploradores de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="46498-331">`browserTimings` shows page load data collected in your users' browsers.</span></span>

<span data-ttu-id="46498-332">[Configurar la aplicación para telemetría de cliente](app-insights-javascript.md) en orden toosee estas métricas.</span><span class="sxs-lookup"><span data-stu-id="46498-332">[Set up your app for client-side telemetry](app-insights-javascript.md) in order toosee these metrics.</span></span>

<span data-ttu-id="46498-333">esquema de Hello incluye [métricas que indica la longitud de Hola de distintas fases del proceso de carga de página de hello](app-insights-javascript.md#page-load-performance).</span><span class="sxs-lookup"><span data-stu-id="46498-333">hello schema includes [metrics indicating hello lengths of different stages of hello page loading process](app-insights-javascript.md#page-load-performance).</span></span> <span data-ttu-id="46498-334">(No indican longitud Hola de tiempo a los usuarios leen una página.)</span><span class="sxs-lookup"><span data-stu-id="46498-334">(They don’t indicate hello length of time your users read a page.)</span></span>  

<span data-ttu-id="46498-335">Mostrar popularities Hola de diferentes páginas y tiempos de cada página de carga:</span><span class="sxs-lookup"><span data-stu-id="46498-335">Show hello popularities of different pages, and load times for each page:</span></span>

![Tiempos de carga de páginas en Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a><span data-ttu-id="46498-337">Tabla de resultados de la disponibilidad</span><span class="sxs-lookup"><span data-stu-id="46498-337">Availability results table</span></span>
<span data-ttu-id="46498-338">`availabilityResults`Muestra Hola resultados de la [pruebas web](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="46498-338">`availabilityResults` shows hello results of your [web tests](app-insights-monitor-web-app-availability.md).</span></span> <span data-ttu-id="46498-339">Cada ejecución de las pruebas en cada una de las ubicaciones se notifica por separado.</span><span class="sxs-lookup"><span data-stu-id="46498-339">Each run of your tests from each test location is reported separately.</span></span>

![Tiempos de carga de páginas en Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a><span data-ttu-id="46498-341">Tabla de dependencias</span><span class="sxs-lookup"><span data-stu-id="46498-341">Dependencies table</span></span>
<span data-ttu-id="46498-342">Contiene los resultados de las llamadas que la aplicación hace toodatabases y las API de REST y otros llama tooTrackDependency().</span><span class="sxs-lookup"><span data-stu-id="46498-342">Contains results of calls that your app makes toodatabases and REST APIs, and other calls tooTrackDependency().</span></span> <span data-ttu-id="46498-343">También incluye las llamadas AJAX realizadas desde el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="46498-343">Also includes AJAX calls made from hello browser.</span></span>

<span data-ttu-id="46498-344">Llamadas AJAX desde el Explorador de hello:</span><span class="sxs-lookup"><span data-stu-id="46498-344">AJAX calls from hello browser:</span></span>

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

<span data-ttu-id="46498-345">Llamadas de dependencia del servidor hello:</span><span class="sxs-lookup"><span data-stu-id="46498-345">Dependency calls from hello server:</span></span>

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

<span data-ttu-id="46498-346">Resultados de la dependencia de servidor siempre muestran `success==False` si hello no está instalado el agente de visión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="46498-346">Server-side dependency results always show `success==False` if hello Application Insights Agent is not installed.</span></span> <span data-ttu-id="46498-347">Sin embargo, hello otros datos son correctos.</span><span class="sxs-lookup"><span data-stu-id="46498-347">However, hello other data are correct.</span></span>

### <a name="traces-table"></a><span data-ttu-id="46498-348">Tabla de seguimientos</span><span class="sxs-lookup"><span data-stu-id="46498-348">Traces table</span></span>
<span data-ttu-id="46498-349">Contiene la telemetría de hello enviado por una aplicación que use TrackTrace(), o [otros marcos de registro](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="46498-349">Contains hello telemetry sent by your app using TrackTrace(), or [other logging frameworks](app-insights-asp-net-trace-logs.md).</span></span>

## <a name="video"></a><span data-ttu-id="46498-350">Vídeo</span><span class="sxs-lookup"><span data-stu-id="46498-350">Video</span></span> 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

<span data-ttu-id="46498-351">Consultas avanzadas:</span><span class="sxs-lookup"><span data-stu-id="46498-351">Advanced queries:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a><span data-ttu-id="46498-352">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46498-352">Next steps</span></span>
* [<span data-ttu-id="46498-353">Referencia de idioma de Analytics</span><span class="sxs-lookup"><span data-stu-id="46498-353">Analytics language reference</span></span>](app-insights-analytics-reference.md)
* <span data-ttu-id="46498-354">[Hoja de referencia rápida de SQL-usuarios](https://aka.ms/sql-analytics) traduce giros de hello más comunes.</span><span class="sxs-lookup"><span data-stu-id="46498-354">[SQL-users' cheat sheet](https://aka.ms/sql-analytics) translates hello most common idioms.</span></span>

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
