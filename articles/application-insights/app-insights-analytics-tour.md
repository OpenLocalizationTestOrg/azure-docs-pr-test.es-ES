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
# <a name="a-tour-of-analytics-in-application-insights"></a>Un paseo por Analytics de Application Insights
[Análisis de](app-insights-analytics.md) es característica de búsqueda eficaces Hola de [Application Insights](app-insights-overview.md). En estas páginas se describe el lenguaje de consulta de Log Analytics.

* **[Ver vídeo de introducción de hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Análisis de prueba con nuestros datos simulados](https://analytics.applicationinsights.io/demo)**  si la aplicación no envía datos tooApplication visión todavía.
* **[Hoja de referencia rápida de SQL-usuarios](https://aka.ms/sql-analytics)**  traduce giros de hello más comunes.

¡Eche un recorrido a través de algunas tooget consultas básicas que se inició.

## <a name="connect-tooyour-application-insights-data"></a>Conexión de datos de Application Insights tooyour
Abra Analytics desde la [hoja de información general](app-insights-dashboards.md) de su aplicación en Application Insights:

![Abra portal.azure.com, abra su recurso de Application Insights y haga clic en Análisis.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a>[Take](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): mostrarme n filas
Los puntos de datos que registran las operaciones de usuario (normalmente solicitudes HTTP recibidas mediante la aplicación web) se almacenan en una tabla denominada `requests`. Cada fila tiene un punto de datos de telemetría recibido de hello Application Insights SDK en la aplicación.

Empecemos examinando algunas filas de ejemplo de tabla de hello:

![results](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> Coloque el cursor de hello en alguna parte en la instrucción de hello antes de hacer clic en Ir. Puede dividir una instrucción en varias líneas, pero no incluya líneas en blanco en una instrucción. Líneas en blanco son una manera cómoda de tookeep varios separan las consultas en la ventana hello.
>
>

Elija columnas, arrástrelas, agrupe por columnas y filtre:

![Hacer clic en la selección de columna en la parte superior derecha de los resultados](./media/app-insights-analytics-tour/030.png)

Expanda cualquier detalle de hello toosee de elemento:

![Seleccione Table (Tabla) y use Configure Columns (Configurar columnas).](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> Haga clic en el encabezado de Hola de una columna toore-ordenar Hola los resultados disponibles en el Explorador de web Hola. Pero tenga en cuenta que para un conjunto de resultados grandes, se limita Hola número de filas descargadas toohello explorador. Este modo de ordenación no siempre puede mostrar Hola real mayor o menor de elementos. elementos toosort usan de forma confiable, hello `top` o `sort` operador.
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a>[Top](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) y [sort](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)
`take`es un ejemplo rápido de un resultado de tooget útil, pero muestra filas de tabla de hello en ningún orden concreto. usar una vista ordenada, tooget `top` (para obtener un ejemplo) o `sort` (a través de hello toda la tabla).

Mostrarme Hola n primeras filas, ordenadas por una columna concreta:

```AIQL

    requests | top 10 by timestamp desc
```

* *Sintaxis*: la mayoría de los operadores tienen parámetros de palabra clave como `by`.
* `desc` = orden descendente, `asc` = orden ascendente.

![](./media/app-insights-analytics-tour/260.png)

`top...` es una manera más eficiente de decir `sort ... | take...`. Podríamos haber escrito:

```AIQL

    requests | sort by timestamp desc | take 10
```

resultado de Hello sería Hola mismo, pero se ejecutaría un poco más lentamente. (También podría escribir `order`, que es un alias de `sort`).

encabezados de columna de Hello en la vista de tabla de hello también pueden ser utilizados toosort Hola resultados en pantalla de bienvenida. Pero, por supuesto, si ha usado `take` o `top` tooretrieve parte de una tabla, verá solo reordenar Hola registros que se han recuperado.

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a>[Where](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): filtrado de una condición.

Veamos las solicitudes que devuelven un código de resultado determinado:

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

Hola `where` operador toma una expresión booleana. He aquí algunos puntos clave:

* `and`, `or`: Operadores booleanos
* `==`, `<>`, `!=`: igual que y no igual que
* `=~`, `!~`: cadena que no distingue entre mayúsculas y minúsculas igual que y no igual que. Hay muchos más operadores de comparación de cadenas.

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a>Introducción al tipo correcto de Hola
Buscar solicitudes incorrectas:

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a>Hora

De forma predeterminada, las consultas son toohello restringido últimas 24 horas. Pero puede cambiar este intervalo:

![](./media/app-insights-analytics-tour/change-time-range.png)

Invalidar el intervalo de tiempo de hello escribiendo cualquier consulta que se mencionan `timestamp` en una cláusula where. Por ejemplo:

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

característica de intervalo de tiempo de Hello es equivalente tooa 'where' inserta cláusula después de cada mención de una de las tablas de origen Hola.

`ago(3d)` significa "hace tres días". Otras unidades de tiempo son horas (`2h`, `2.5h`), minutos (`25m`) y segundos (`10s`).

Otros ejemplos:

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

[Referencia de fechas y horas](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a>[Project](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): seleccionar, cambiar nombre y calcular columnas
Use [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick solo las columnas de Hola que desee:

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

También puede cambiar el nombre de las columnas y definir otras nuevas:

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

* Los nombres de columna pueden incluir espacios o símbolos si están entre corchetes, tal como se muestra: `['...']` o `["..."]`
* `%`es habitual operador de módulo hello.
* `1d` (es decir, el dígito uno y luego una "d") es un literal de intervalo de tiempo que significa un día. Aquí se indican otros literales de intervalo de tiempo: `12h`, `30m`, `10s` y `0.01s`.
* `floor`(alias `bin`) Redondea un valor de profundidad toohello múltiplo más cercano de valor base Hola que proporcione. Por lo que `floor(aTime, 1s)` redondea una hora hacia abajo toohello más cercano de segundo.

Las expresiones pueden incluir todos los operadores habituales de hello (`+`, `-`,...), y no hay una gama de funciones útiles.

## <a name="extend"></a>Extend
Si solo desea tooadd toohello de las columnas existentes, utilice [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

Usar [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) es menos detallado [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) si desea tookeep Hola a todas las columnas existentes.

### <a name="convert-toolocal-time"></a>Convertir la hora de toolocal

Las marcas de tiempo siempre se expresan en formato UTC. Por lo que si se encuentra en hello nos suroeste y es temporada de invierno, podría como esta:

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a>[Summarize](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): adición de grupos de filas
`Summarize` aplica una *función de agregación* específica sobre grupos de filas.

Por ejemplo, hello tarda la aplicación web toorespond tooa solicitud se notifica en el campo de hello `duration`. Veamos medio de respuesta de hello tooall solicitudes de tiempo:

![](./media/app-insights-analytics-tour/410.png)

O se puede separar resultado de hello en las solicitudes de nombres diferentes:

![](./media/app-insights-analytics-tour/420.png)

`Summarize`recopila Hola puntos de datos de flujo de hello en grupos para qué hello `by` cláusula evalúa igualmente. Cada valor de hello `by` expresión - cada nombre de la operación en hello ejemplo anterior - da como resultado de una fila en la tabla de resultados de Hola.

O bien, podríamos agrupar los resultados en función de la hora del día:

![](./media/app-insights-analytics-tour/430.png)

Tenga en cuenta cómo usamos hello `bin` (función) (también conocido como `floor`). Si solo usáramos `by timestamp`, cada fila de entrada terminaría en su pequeño grupo. Para cualquier valor escalar continua veces like o números, tenemos intervalo continuo de hello toobreak en un número de valores discretos fáciles de administrar. `bin`-que es simplemente Hola familiarizado redondeo en profundidad `floor` función; es toodo de manera más fácil de Hola que.

Podemos usar Hola mismos intervalos de tooreduce técnica de cadenas:

![](./media/app-insights-analytics-tour/440.png)

Tenga en cuenta que puede usar `name=` tooset nombre de Hola de una columna de resultados, en las expresiones de agregado de Hola o por la cláusula de Hola.

## <a name="counting-sampled-data"></a>Recuento de datos muestreados
`sum(itemCount)`es recomendable de hello agregación toocount eventos. En muchos casos, itemCount == 1, por lo que la función de hello simplemente cuenta el número de Hola de filas en un grupo de Hola. Pero cuando [muestreo](app-insights-sampling.md) está en funcionamiento, sólo una fracción de eventos de hello original se conservan como puntos de datos de Application Insights, por lo que para cada punto de datos que se ven, hay `itemCount` eventos.

Por ejemplo, si el muestreo descarta el 75% de los eventos originales de hello y, a continuación, itemCount == 4 en registros de hello conservan: es decir, para cada registro retenido, había cuatro registros originales.

Muestreo adaptativo hace itemCount toobe superior durante los períodos de la aplicación cuando se utilice con un alto grado.

Por lo tanto, se suma de itemCount ofrece una buena estimación del número original de Hola de eventos.

![](./media/app-insights-analytics-tour/510.png)

También hay un `count()` agregación (y una operación de recuento), para los casos donde realmente desea toocount Hola número de filas de un grupo.

Existe una gama de [funciones de agregación](https://docs.loganalytics.io/learn/tutorials/aggregations.html).

## <a name="charting-hello-results"></a>Gráficos de resultados de Hola
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

De forma predeterminada, los resultados se muestran como una tabla:

![](./media/app-insights-analytics-tour/225.png)

Podemos hacer un mejor rendimiento que la vista de tabla de Hola. Echemos un vistazo a los resultados de hello en la vista de gráfico de hello con la opción de barra vertical de hello:

![Haga clic Chart (Gráfico) y después elija Vertical bar chart (Gráfico de barras verticales) y asigne los ejes x e y.](./media/app-insights-analytics-tour/230.png)

Tenga en cuenta que, aunque se no ordenación resultados de Hola por hora (como puede ver en la visualización de la tabla de hello), Hola gráfico siempre muestran fechas y horas en el orden correcto.


## <a name="timecharts"></a>Gráficos de tiempo
Mostrar cuántos eventos hay cada hora:

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

Seleccione la opción de visualización del gráfico de hello:

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a>Varias series
Varias expresiones en hello `summarize` cláusula crea varias columnas.

Varias expresiones en hello `by` cláusula crea varias filas, una para cada combinación de valores.

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Tabla de solicitudes por hora y ubicación](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a>Segmentación de un gráfico por dimensiones
Si se pueden toosplit usado Hola datos numéricos en series independientes de los puntos de gráfico una tabla que tiene una columna de cadenas y una columna numérica, cadena de Hola. Si hay más de una columna de cadena, puede elegir qué toouse de columna como discriminador Hola.

![Segmentación de un gráfico de análisis](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a>Tasa de devolución

Convertir una toouse de cadena booleano tooa como un discriminador:

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

### <a name="display-multiple-metrics"></a>Muestra de varias métricas
Si el gráfico de una tabla que tiene más de una columna numérica, en la marca de tiempo de suma toohello, puede mostrar cualquier combinación de ellos.

![Segmentación de un gráfico de análisis](./media/app-insights-analytics-tour/110.png)

Debe seleccionar **Don't Split** (No dividir) para poder seleccionar varias columnas numéricas. No se divide por una columna de cadenas en hello mismo tiempo como mostrar más de una columna numérica.

## <a name="daily-average-cycle"></a>Ciclo medio diario
¿Cómo varía en uso en día promedio Hola?

Solicitudes de recuento por tiempo Hola módulo un día, segmentan en horas:

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
> Tenga en cuenta que actualmente tenemos tooconvert tiempo duraciones toodatetimes en orden toodisplay en un gráfico de líneas.
>
>

## <a name="compare-multiple-daily-series"></a>Comparación de varias series diarias
¿Cómo varía en uso con el tiempo de hello del día en distintos países?

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

## <a name="plot-a-distribution"></a>Trazado de una distribución
¿Cuántas sesiones existen de longitudes diferentes?

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

Hola la última línea es necesario tooconvert toodatetime. Actualmente Hola x eje de un gráfico se muestra como un valor escalar solo si es una fecha y hora.

Hola `where` cláusula excluye las sesiones Monoestable (sessionDuration == 0) y conjuntos de Hola longitud del eje x de Hola.

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[Percentiles](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
¿Qué intervalos de duraciones cubren diferentes porcentajes de sesiones?

Usar hello por encima de la consulta, pero reemplace Hola última línea:

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

Eliminamos límite superior de Hola Hola donde cláusula, en orden tooget corregir cifras incluidas todas las sesiones con más de una solicitud:

![result](./media/app-insights-analytics-tour/180.png)

De lo que podemos ver que:

* El 5 % de las sesiones tienen una duración de menos de 3 minutos 34 s;
* El 50 % de las sesiones dura menos de 36 minutos;
* El 5 % de las sesiones dura más de 7 días.

tooget un desglose independiente para cada país, solo tenemos toobring hello client_CountryOrRegion columna por separado a través de los operadores de resumen:

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

## <a name="join"></a>Unión
Tenemos que tooseveral acceso a tablas, incluidas las excepciones y las solicitudes.

toofind Hola excepciones relacionadas tooa solicitud que devuelve una respuesta de error, se pueden combinar tablas de hello en `session_Id`:

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


Es recomendable toouse `project` tooselect columnas de hello solo es necesario antes de realizar Hola combinación.
Hola mismas cláusulas, cambiamos el nombre de columna de marca de tiempo de Hola.

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a>[Permiten](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): asignar una variable de resultado tooa

Use `let` tooseparate partes de saludo de la expresión anterior Hola. resultados de Hello son iguales:

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> En el cliente de análisis de hello, no incluya líneas en blanco entre las partes de Hola de consulta de Hola. Asegúrese de tooexecute seguro todos del mismo.
>

Use `toscalar` tooconvert un valor de tooa de celda de tabla única:

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


### <a name="functions"></a>Functions

Use *permiten* toodefine una función:

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a>Acceso a objetos anidados
Se puede acceder fácilmente a los objetos anidados. Por ejemplo, en la secuencia de excepciones de hello, puede ver objetos estructurados similar al siguiente:

![result](./media/app-insights-analytics-tour/520.png)

Es posible simplificar eligiendo Propiedades Hola que le interesa:

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

Tenga en cuenta que necesita el tipo adecuado de toocast Hola resultado toohello.


## <a name="custom-properties-and-measurements"></a>Propiedades y medidas personalizadas
Si la aplicación se asocia [dimensiones personalizadas (propiedades) y las medidas personalizadas](app-insights-api-custom-events-metrics.md#properties) tooevents, a continuación, se verán en hello `customDimensions` y `customMeasurements` objetos.

Por ejemplo, si la aplicación incluye:

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

tooextract estos valores en el análisis:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

tooverify si es una dimensión personalizada de un tipo determinado:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a>Paneles
Puede anclar el panel de resultados tooa en orden toobring juntos todos los gráficos y sus tablas más importantes.

* [Panel compartido Azure](app-insights-dashboards.md#share-dashboards): haga clic en el icono de alfiler Hola. Antes de hacerlo, debe tener un panel compartido. Hola portal de Azure, abrir o crear un panel y haga clic en compartir.
* [Panel de Power BI](app-insights-export-power-bi.md): haga clic en Exportar, Consulta de Power BI. Una ventaja de esta alternativa es que puede mostrar la consulta junto con otros resultados procedentes de una gran variedad de orígenes.

## <a name="combine-with-imported-data"></a>Combinación con datos importados

Informes de análisis un aspecto excelentes en el panel de hello, pero a veces desea tootranslate Hola datos tooa forma por más. Por ejemplo, suponga que los usuarios autenticados se identifican en la telemetría de hello mediante un alias. Le gustaría tooshow nombres su real en los resultados. toodo, necesita un archivo CSV que se asigna desde los nombres reales de hello alias toohello.

Puede importar un archivo de datos y usarla como cualquiera de las tablas estándar hello (solicitudes, excepciones etc.). Puede consultarla por sí sola o combinarla con otras tablas. Por ejemplo, si tiene una tabla denominada usermap y tiene columnas `realName` y `userId`, puede usar tootranslate hello `user_AuthenticatedId` campo telemetría de solicitud de hello:

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

tooimport una tabla, en la hoja de esquema de hello, en **otros orígenes de datos**, siga Hola instrucciones tooadd un nuevo origen de datos, mediante la carga de una muestra de los datos. A continuación, puede utilizar estas tablas de tooupload de definición.

la característica de importación de Hello está actualmente en vista previa, por lo que inicialmente se verá un vínculo "Póngase en contacto con nosotros" bajo "Otros orígenes de datos." Utilice este toosign toohello programa de vista previa y vínculo de hello, a continuación, se reemplazará por un botón "Agregar nuevo origen de datos".


## <a name="tables"></a>Tablas
secuencia de Hola de telemetría recibido de la aplicación sea accesible a través de varias tablas. esquema de Hola de propiedades disponibles para cada tabla es visible a la izquierda de Hola de ventana hello.

### <a name="requests-table"></a>Tabla de solicitudes
Recuento de las solicitudes HTTP tooyour web app y segmento por nombre de página:

![Contar solicitudes segmentadas por nombre](./media/app-insights-analytics-tour/analytics-count-requests.png)

Busque solicitudes de Hola que producirá un error en la mayoría:

![Contar solicitudes segmentadas por nombre](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a>Tabla de eventos personalizados
Si usa [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend sus propios eventos, puede leerlos desde esta tabla.

Veamos un ejemplo en el que el código de aplicación contiene estas líneas:

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

Muestra la frecuencia de Hola de estos eventos:

![Mostrar la tasa de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

Extraer las medidas y dimensiones de eventos de hello:

![Mostrar la tasa de eventos personalizados](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a>Tabla de métricas personalizadas
Si utilizas [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend sus propios valores de métrica, encontrará sus resultados en hello **customMetrics** secuencia. Por ejemplo:  

![Métricas personalizadas en Application Insights Analytics](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> En [Explorer métricas](app-insights-metrics-explorer.md), todas las medidas personalizadas de tipo tooany adjunto de telemetría aparecen juntas en la hoja de métricas de hello junto con las métricas que se envían con `TrackMetric()`. Pero en el análisis, las medidas personalizadas siguen siendo adjunta toowhichever tipo de telemetría que se llevaron a en - eventos o las solicitudes etc. - mientras métricas enviadas por TrackMetric aparecen en su propia secuencia.
>
>

### <a name="performance-counters-table"></a>Tabla de contadores de rendimiento
Los [contadores de rendimiento](app-insights-performance-counters.md) muestran métricas del sistema básico de la aplicación, como CPU, memoria y la utilización de la red. Puede configurar Hola SDK toosend adicionales, incluidos sus propios contadores.

Hola **performanceCounters** esquema expone hello `category`, `counter` nombre, y `instance` nombre de cada contador de rendimiento. Nombres de instancia de contador son solo los contadores de rendimiento de toosome aplicables y suelen indican nombre Hola de hello proceso toowhich Hola recuento está relacionada con. En la telemetría de Hola para cada aplicación, verá solo los contadores de Hola para esa aplicación. Por ejemplo, toosee qué contadores están disponibles:

![Contadores de rendimiento en Application Insights Analytics](./media/app-insights-analytics-tour/analytics-performance-counters.png)

un gráfico de memoria disponible a través de hello tooget periodo seleccionado:

![Gráfico de tiempo de la memoria in Application Insights Analytics](./media/app-insights-analytics-tour/analytics-available-memory.png)

Al igual que otros telemetría **performanceCounters** también tiene una columna `cloud_RoleInstance` que indica la identidad de Hola de máquina de host de hello en el que se ejecuta la aplicación. Por ejemplo, toocompare Hola rendimiento de la aplicación en equipos diferentes de hello:

![Rendimiento segmentado por instancia de rol en Application Insights Analytics](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a>Tabla de excepciones
[Las excepciones que notifica la aplicación](app-insights-asp-net-exceptions.md) están disponibles en esta tabla.

toofind Hola solicitud HTTP que estaba controlando la aplicación cuando se produce la excepción de hello, combine operation_Id:

![Combinar excepciones con solicitudes en operation_Id](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a>Tabla de intervalos de explorador
`browserTimings` muestra los datos de carga de las páginas recopilados en los exploradores de los usuarios.

[Configurar la aplicación para telemetría de cliente](app-insights-javascript.md) en orden toosee estas métricas.

esquema de Hello incluye [métricas que indica la longitud de Hola de distintas fases del proceso de carga de página de hello](app-insights-javascript.md#page-load-performance). (No indican longitud Hola de tiempo a los usuarios leen una página.)  

Mostrar popularities Hola de diferentes páginas y tiempos de cada página de carga:

![Tiempos de carga de páginas en Analytics](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a>Tabla de resultados de la disponibilidad
`availabilityResults`Muestra Hola resultados de la [pruebas web](app-insights-monitor-web-app-availability.md). Cada ejecución de las pruebas en cada una de las ubicaciones se notifica por separado.

![Tiempos de carga de páginas en Analytics](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a>Tabla de dependencias
Contiene los resultados de las llamadas que la aplicación hace toodatabases y las API de REST y otros llama tooTrackDependency(). También incluye las llamadas AJAX realizadas desde el Explorador de Hola.

Llamadas AJAX desde el Explorador de hello:

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

Llamadas de dependencia del servidor hello:

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

Resultados de la dependencia de servidor siempre muestran `success==False` si hello no está instalado el agente de visión de la aplicación. Sin embargo, hello otros datos son correctos.

### <a name="traces-table"></a>Tabla de seguimientos
Contiene la telemetría de hello enviado por una aplicación que use TrackTrace(), o [otros marcos de registro](app-insights-asp-net-trace-logs.md).

## <a name="video"></a>Vídeo 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

Consultas avanzadas:

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a>Pasos siguientes
* [Referencia de idioma de Analytics](app-insights-analytics-reference.md)
* [Hoja de referencia rápida de SQL-usuarios](https://aka.ms/sql-analytics) traduce giros de hello más comunes.

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
