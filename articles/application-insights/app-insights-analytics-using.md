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
# <a name="using-analytics-in-application-insights"></a>Uso de Analytics en Application Insights
[Análisis de](app-insights-analytics.md) es característica de búsqueda eficaces Hola de [Application Insights](app-insights-overview.md). En estas páginas se describe el lenguaje de consulta de Log Analytics.

* **[Ver vídeo de introducción de hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Análisis de prueba con nuestros datos simulados](https://analytics.applicationinsights.io/demo)**  si la aplicación no envía datos tooApplication visión todavía.

## <a name="open-analytics"></a>Apertura de Analytics
En el recurso de inicio de la aplicación de Application Insights, haga clic en Analytics.

![Abra portal.azure.com, abra su recurso de Application Insights y haga clic en Análisis.](./media/app-insights-analytics-using/001.png)

tutorial de Hello en línea le ofrece algunas ideas sobre lo que puede hacer.

Puede encontrar un [paseo más amplio aquí](app-insights-analytics-tour.md).

## <a name="query-your-telemetry"></a>Consulta de la telemetría
### <a name="write-a-query"></a>Escriba una consulta.
![Pantalla del esquema](./media/app-insights-analytics-using/150.png)

Comenzar con nombres Hola de cualquiera de las tablas de Hola que aparecen a la izquierda de hello (o hello [intervalo](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) o [union](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operadores). Use `|` toocreate una canalización de [operadores](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html). 

IntelliSense le indicará con operadores de Hola y elementos de la expresión de Hola que puede usar. Haga clic en el icono de información de hello (o presione CTRL+BARRA ESPACIADORA) tooget una descripción más detallada y ejemplos de cómo toouse cada elemento.

Vea hello [paseo por el lenguaje análisis](app-insights-analytics-tour.md) y [referencia del lenguaje](app-insights-analytics-reference.md).

### <a name="run-a-query"></a>Ejecución de una consulta
![Ejecución de una consulta](./media/app-insights-analytics-using/130.png)

1. Puede utilizar saltos de línea sencillos en las consultas.
2. Coloque Hola cursor dentro o al final de Hola de consulta de Hola que desee toorun.
3. Compruebe el intervalo de tiempo de saludo de la consulta. (puede cambiarla o invalidarla; para ello, debe incluir su propia cláusula [`where...timestamp...`](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) en la consulta).
3. Haga clic en la consulta de Go toorun Hola.
4. No ponga líneas en blanco en la consulta. Puede mantener varias consultas separadas en una pestaña de consulta; para ello, sepárelas con líneas en blanco. Solo consulta Hola con cursor Hola se ejecuta.

### <a name="save-a-query"></a>Almacenamiento de una consulta
![Almacenamiento de una consulta](./media/app-insights-analytics-using/140.png)

1. Guardar archivo de consulta actual de Hola.
2. Abra un archivo de consulta guardado.
3. Cree un archivo de consulta.

## <a name="see-hello-details"></a>Ver detalles de Hola
Expanda cualquier fila de hello resultados toosee su lista de propiedades completa. Se puede expandir cualquier propiedad que es un valor estructurado: por ejemplo, dimensiones personalizadas o pila Hola enumerar en una excepción.

![Expansión de una fila](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a>Organizar resultados de Hola
Puede ordenar, filtrar, paginar y agrupar los resultados de hello devueltos por la consulta.

> [!NOTE]
> Ordenar, agrupar y filtrar en el Explorador de hello vuelva a no ejecutan la consulta. Solo reorganizar los resultados de Hola que ha sido devuelto por la última consulta. 
> 
> tooperform estas tareas en el servidor hello antes de que se devuelven resultados de hello, escribir la consulta con hello [ordenación](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [resumir](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) y [donde](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operadores.
> 
> 

Elegir columnas de hello haría como toosee, arrastre y cambio de tamaño de columnas toorearrange de encabezados de columna arrastrando sus bordes.

![Organización de columnas](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a>Ordenación y filtrado de elementos
Ordenar los resultados, haga clic en el encabezado de Hola de una columna. Haga clic en nuevo toosort Hola otra manera, y haga clic en una tercera vez toorevert toohello ordenación original devuelto por la consulta.

Utilice toonarrow de icono de filtro de hello en la búsqueda.

![Ordenación y filtrado de columnas](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a>Agrupación de elementos
toosort por más de una columna, utilizan la agrupación. Primero habilite dicha opción y, a continuación, arrastre los encabezados de columna en el espacio de Hola por encima de la tabla de Hola.

![Grupo](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a>¿Faltan algunos resultados?

Si cree que no puede ver todos los resultados de Hola que esperaba, hay un par de razones posibles.

* **Filtro de intervalo de tiempo**. De forma predeterminada, solo verá los resultados de hello últimas 24 horas. Hay un filtro automático que limita el intervalo de Hola de resultados que se recuperan de las tablas de origen Hola. 

    Sin embargo, puede cambiar el intervalo de tiempo de hello el filtro con el menú desplegable de Hola.

    O puede invalidar el intervalo automático de hello mediante la inclusión de su propio [ `where  ... timestamp ...` cláusula](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) en la consulta. Por ejemplo:

    `requests | where timestamp > ago('2d')`

* **Límite de resultados**. Hay un límite de unos 10 filas k en resultados de hello devueltos desde el portal de Hola. Se muestra una advertencia si sobrepasar el límite de Hola. Si esto sucede, ordenar los resultados en la tabla de hello no siempre mostrarle todas Hola real primeros o últimos resultados. 

    Es recomendable tooavoid posicionamiento Hola límite. Use el filtro de intervalo de tiempo de Hola o usar operadores como:

  * [top 100 by timestamp](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [take 100](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [summarize ](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [where timestamp &gt; ago(3d)](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

(¿Desea más de 10 000 filas? Considere el uso de [Exportación continua](app-insights-export-telemetry.md). Analytics está diseñado para el análisis, no para la recuperación de datos sin procesar.)

## <a name="diagrams"></a>Diagramas
Seleccione el tipo de Hola de diagrama que le gustaría:

![Seleccione un tipo de diagrama](./media/app-insights-analytics-using/230.png)

Si tiene varias columnas de tipos de derecho de hello, puede elegir Hola x y ejes y y una columna de resultados de hello toosplit de dimensiones por.

De forma predeterminada, resultados se muestran inicialmente como una tabla y seleccione diagrama Hola manualmente. Pero puede usar hello [representar directiva](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) final Hola de un tooselect consulta un diagrama.

### <a name="analytics-diagnostics"></a>Analytics Diagnostics


En un timechart, si se produce un pico súbito o el paso de los datos, es posible que contenga un punto de resaltado en la línea de saludo. Esto indica que diagnósticos de análisis se ha identificado una combinación de propiedades que filtrar los cambios repentinos Hola. Haga clic en hello punto tooget información más detallada acerca de filtro de Hola y versión filtrada de toosee Hola. Esto puede ayudar a identificar qué cambio Hola iniciadas. 

[Más información sobre Analytics Diagnostics](app-insights-analytics-diagnostics.md)


![Analytics Diagnostics](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a>Toodashboard de PIN
Puede anclar un tooone diagrama o una tabla de la [compartido paneles](app-insights-dashboards.md) -simplemente haga clic en Anclar Hola. (Puede que tenga demasiado[actualización de paquete de precios de la aplicación](app-insights-pricing.md) tooturn acerca de esta característica.) 

![Haga clic en Anclar Hola](./media/app-insights-analytics-using/pin-01.png)

Esto significa que, al reunir un toohelp panel supervisar el rendimiento de Hola o el uso de los servicios web, puede incluir un análisis bastante complejo junto con hello otras métricas. 

Puede anclar un panel de toohello tabla, si tiene cuatro o menos columnas. Se muestran solo Hola siete filas superiores.

### <a name="dashboard-refresh"></a>Actualización del panel
Hola gráfico anclado toohello panel se actualiza automáticamente volviendo a ejecutar consulta Hola cada horas aproximadamente. También puede hacer clic en botón de actualización de Hola.

### <a name="automatic-simplifications"></a>Simplificaciones automáticas

Ciertas medidas de simplificación son gráfico tooa aplicada al anclar el panel de tooa.

**Restricción de tiempo:** las consultas son toohello limitan de manera automática últimos 14 días. Hello efecto es Hola igual que si la consulta incluye `where timestamp > ago(14d)`.

**Restricción de recuento de ubicación:** si se muestra un gráfico que tiene muchas ubicaciones discretas (normalmente en un gráfico de barras), Hola menos bins rellenadas automáticamente se agrupan en un único "otros" bin. Por ejemplo, esta consulta:

    requests | summarize count_search = count() by client_CountryOrRegion

tiene esta apariencia en Analytics:

![Gráfico con cola larga](./media/app-insights-analytics-using/pin-07.png)

pero, al anclar el panel de tooa, el siguiente aspecto:

![Gráfico con intervalos limitados](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a>Exportar tooExcel
Una vez que haya ejecutado una consulta, puede descargar un archivo .csv. Haga clic en **Exportar, Excel**.

## <a name="export-toopower-bi"></a>Exportar tooPower BI
Coloque el cursor de hello en una consulta y elija **exportar, Power BI**.

![Exportar desde análisis tooPower BI](./media/app-insights-analytics-using/240.png)

Ejecutar consulta de hello en Power BI. Puede establecerlo toorefresh según una programación.

Con Power BI, puede crear paneles que reúnan datos de una gran variedad de orígenes.

[Obtener más información sobre la exportación tooPower BI](app-insights-export-power-bi.md)

## <a name="deep-link"></a>Vínculo profundo

Obtener un vínculo bajo **exportación, el vínculo compartido** que se puede enviar al usuario tooanother. Proporcionado por el usuario de hello tiene [grupo de recursos de acceso tooyour](app-insights-resources-roles-access-control.md), consulta Hola se abrirá en hello análisis de interfaz de usuario.

(En el vínculo de hello, texto de consulta de hello aparece después de "? q =", comprimido gzip y codificado en base 64. Si escribes vínculos profundos de código toogenerate que proporcione toousers. Sin embargo, Hola recomienda forma toorun análisis de código es usar hello [API de REST](https://dev.applicationinsights.io/).)


## <a name="automation"></a>Automation

Hola de uso [API de REST de acceso a datos](https://dev.applicationinsights.io/) toorun consultas de análisis. [Por ejemplo](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (con PowerShell):

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

A diferencia de hello interfaz de usuario de análisis, Hola API de REST no agrega automáticamente las consultas de tooyour de limitación de marca de tiempo. Recuerde tooadd su propia cláusula where, tooavoid obtener las respuestas muy grandes.



## <a name="import-data"></a>Importar datos

Los datos se pueden importar desde un archivo CSV. Un uso típico es tooimport datos estáticos que se pueden afiliar con tablas de la telemetría. 

Por ejemplo, si los usuarios autenticados se identifican en la telemetría mediante un alias o un identificador confuso, puede importar una tabla que asigna nombres de alias tooreal. Al realizar una combinación de telemetría de solicitud de hello, puede identificar a los usuarios por sus nombres en los informes de análisis de hello reales.

### <a name="define-your-data-schema"></a>Definición de un esquema de datos

1. Haga clic en **Configuración** (en la parte superior izquierda) y, luego, en **Orígenes de datos**. 
2. Agregar un origen de datos, siga las instrucciones de Hola. Es más frecuentes toosupply una muestra de datos de hello, que deben incluir al menos diez filas. A continuación, corrija el esquema de Hola.

Esto define un origen de datos, a continuación, puede utilizar tablas individuales tooimport.

### <a name="import-a-table"></a>Importación de una tabla

1. Abra la definición de origen de datos de lista de Hola.
2. Haga clic en "Cargar" y siga la tabla de hello instrucciones tooupload Hola. Esto implica un tooa llamada API de REST y, por lo que resulta fácil tooautomate. 

La tabla ya está disponible para usarla en las consultas de Analytics. Aparecerá en Analytics 

### <a name="use-hello-table"></a>Utilice tabla Hola

Supongamos que la definición del origen de datos se denomina `usermap` y que tiene dos campos, `realName` y `user_AuthenticatedId`. Hola `requests` tabla también tiene un campo denominado `user_AuthenticatedId`, por lo que resulta fácil toojoin ellos:

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
la tabla resultante de las solicitudes de Hello tiene una columna adicional, `realName`.

### <a name="import-from-logstash"></a>Importación desde LogStash

Si usa [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), puede usar los registros de análisis tooquery. Hola de uso [complemento que canaliza datos en análisis](https://github.com/Microsoft/logstash-output-application-insights). 

## <a name="video"></a>Vídeo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

