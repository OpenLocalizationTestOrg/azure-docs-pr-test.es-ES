---
title: "Uso del portal de búsqueda de registros en Azure Log Analytics | Microsoft Docs"
description: "Este artículo incluye un tutorial que describe cómo crear búsquedas de registros y analizar los datos almacenados en el área de trabajo de Log Analytics mediante el portal de búsqueda de registros.  El tutorial incluye la ejecución de algunas consultas sencillas que devuelven distintos tipos de datos y el análisis de los resultados."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 6fc556ceb34cde26d5f3789a2397cdaa34b0b84d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-the-log-search-portal"></a><span data-ttu-id="19dc6-104">Creación de búsquedas de registros en Azure Log Analytics mediante el portal correspondiente</span><span class="sxs-lookup"><span data-stu-id="19dc6-104">Create log searches in Azure Log Analytics using the Log Search portal</span></span>

> [!NOTE]
> <span data-ttu-id="19dc6-105">Este artículo describe el portal de búsqueda de registros de Azure Log Analytics mediante el nuevo lenguaje de consulta.</span><span class="sxs-lookup"><span data-stu-id="19dc6-105">This article describes the Log Search portal in Azure Log Analytics using the new query language.</span></span>  <span data-ttu-id="19dc6-106">Puede obtener más información sobre el nuevo lenguaje y conocer el procedimiento para actualizar el área de trabajo en [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md) (Actualización del área de trabajo de Azure Log Analytics al nuevo registro de búsquedas)///.</span><span class="sxs-lookup"><span data-stu-id="19dc6-106">You can learn more about the new language and get the procedure to upgrade your workspace at [Upgrade your Azure Log Analytics workspace to new log search](log-analytics-log-search-upgrade.md).</span></span>  
>
> <span data-ttu-id="19dc6-107">Si todavía no se ha actualizado el área de trabajo al nuevo lenguaje de consulta, vaya a [Búsqueda de datos mediante búsquedas de registros en Log Analytics](log-analytics-log-searches.md) para obtener información sobre la versión actual del portal de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="19dc6-107">If your workspace hasn't been upgraded to the new query language, you should refer to [Find data using log searches in Log Analytics](log-analytics-log-searches.md) for information on the current version of the Log Search portal.</span></span>

<span data-ttu-id="19dc6-108">Este artículo incluye un tutorial que describe cómo crear búsquedas de registros y analizar los datos almacenados en el área de trabajo de Log Analytics mediante el portal de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="19dc6-108">This article includes a tutorial that describes how to create log searches and analyze data stored in your Log Analytics workspace using the Log Search portal.</span></span>  <span data-ttu-id="19dc6-109">El tutorial incluye la ejecución de algunas consultas sencillas que devuelven distintos tipos de datos y el análisis de los resultados.</span><span class="sxs-lookup"><span data-stu-id="19dc6-109">The tutorial includes running some simple queries to return different types of data and analyzing results.</span></span>  <span data-ttu-id="19dc6-110">Se centra en las características del portal de búsqueda de registros que permiten modificar la consulta en lugar de hacerlo directamente.</span><span class="sxs-lookup"><span data-stu-id="19dc6-110">It focuses on features in the Log Search portal for modifying the query rather than modifying it directly.</span></span>  <span data-ttu-id="19dc6-111">Para más información sobre cómo editar directamente la consulta, vaya a la [referencia del lenguaje de consulta](https://go.microsoft.com/fwlink/?linkid=856079).</span><span class="sxs-lookup"><span data-stu-id="19dc6-111">For details on directly editing the query, see the [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>

<span data-ttu-id="19dc6-112">Para crear búsquedas en el portal de análisis avanzado en lugar de en el portal de búsqueda de registros, consulte [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587) (Introducción al portal de análisis).</span><span class="sxs-lookup"><span data-stu-id="19dc6-112">To create searches in the Advanced Analytics portal instead of the Log Search portal, see [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856587).</span></span>  <span data-ttu-id="19dc6-113">Ambos portales usan el mismo lenguaje de consulta para acceder a los mismos datos en el área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="19dc6-113">Both portals use the same query language to access the same data in the Log Analytics workspace.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19dc6-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="19dc6-114">Prerequisites</span></span>
<span data-ttu-id="19dc6-115">En este tutorial se da por supuesto que ya tiene un área de trabajo de Log Analytics con al menos un origen conectado que genera los datos para que las consultas los analicen.</span><span class="sxs-lookup"><span data-stu-id="19dc6-115">This tutorial assumes that you already have a Log Analytics workspace with at least one connected source that generates data for the queries to analyze.</span></span>  

- <span data-ttu-id="19dc6-116">Si no tiene un área de trabajo, puede crear una gratis mediante el procedimiento descrito en [Introducción a un área de trabajo de Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="19dc6-116">If you don't have a workspace, you can create a free one using the procedure at [Get started with a Log Analytics workspace](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="19dc6-117">Conecte al menos un [agente de Windows](log-analytics-windows-agents.md) o un [agente de Linux](log-analytics-linux-agents.md) al área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="19dc6-117">Connect least one [Windows agent](log-analytics-windows-agents.md) or one [Linux agent](log-analytics-linux-agents.md) to the workspace.</span></span>  

## <a name="open-the-log-search-portal"></a><span data-ttu-id="19dc6-118">Abrir el portal de búsqueda de registros</span><span class="sxs-lookup"><span data-stu-id="19dc6-118">Open the Log Search portal</span></span>
<span data-ttu-id="19dc6-119">En primer lugar, abra el portal de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="19dc6-119">Start by opening the Log Search portal.</span></span>  <span data-ttu-id="19dc6-120">Puede acceder a él en Azure Portal o en el portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="19dc6-120">You can access it in either the Azure portal or the OMS portal.</span></span>

1. <span data-ttu-id="19dc6-121">Abra Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="19dc6-121">Open the Azure portal.</span></span>
2. <span data-ttu-id="19dc6-122">Vaya a Log Analytics y seleccione su área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="19dc6-122">Navigate to Log Analytics and select your workspace.</span></span>
3. <span data-ttu-id="19dc6-123">Seleccione la opción **búsqueda de registros** para permanecer en Azure Portal o inicie el portal de OMS seleccionando **Portal de OMS** y, a continuación, haga clic en el botón de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="19dc6-123">Either select **Log Search** to stay in the Azure portal or launch the OMS portal by selecting **OMS Portal** and then clicking the Log Search button.</span></span>

![Botón Log Search (Búsqueda de registros)](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a><span data-ttu-id="19dc6-125">Creación de una búsqueda simple</span><span class="sxs-lookup"><span data-stu-id="19dc6-125">Create a simple search</span></span>
<span data-ttu-id="19dc6-126">La forma más rápida de recuperar algunos datos con los que trabajar es con una consulta simple que devuelve todos los registros en una tabla.</span><span class="sxs-lookup"><span data-stu-id="19dc6-126">The quickest way to retrieve some data to work with is a simple query that returns all records in table.</span></span>  <span data-ttu-id="19dc6-127">Si tiene clientes de Windows o Linux conectados al área de trabajo, tendrá datos en las tablas Event (Windows) o Syslog (Linux).</span><span class="sxs-lookup"><span data-stu-id="19dc6-127">If you have any Windows or Linux clients connected to your workspace, then you'll have data in either the Event (Windows) or Syslog (Linux) table.</span></span>

<span data-ttu-id="19dc6-128">Escriba una de las consultas siguientes en el cuadro de búsqueda y haga clic en el botón de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="19dc6-128">Type one the following queries in the search box and click the search button.</span></span>  

```
Event
```
```
Syslog
```

<span data-ttu-id="19dc6-129">Se devuelven los datos en la vista de lista predeterminada y puede ver el número total de registros que se han devuelto.</span><span class="sxs-lookup"><span data-stu-id="19dc6-129">Data is returned in the default list view, and you can see how many total records were returned.</span></span>

![Consulta sencilla](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

<span data-ttu-id="19dc6-131">Se muestran solo las primeras propiedades de cada registro.</span><span class="sxs-lookup"><span data-stu-id="19dc6-131">Only the first few properties of each record are displayed.</span></span>  <span data-ttu-id="19dc6-132">Haga clic en **Mostrar más** para ver todas las propiedades de un registro concreto.</span><span class="sxs-lookup"><span data-stu-id="19dc6-132">Click **show more** to display all properties for a particular record.</span></span>

![Detalles del registro](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-the-time-scope"></a><span data-ttu-id="19dc6-134">Establecimiento del ámbito de tiempo</span><span class="sxs-lookup"><span data-stu-id="19dc6-134">Set the time scope</span></span>
<span data-ttu-id="19dc6-135">Cada registro recopilado por Log Analytics tiene una propiedad **TimeGenerated** que contiene la fecha y hora en que se creó el registro.</span><span class="sxs-lookup"><span data-stu-id="19dc6-135">Every record collected by Log Analytics has a **TimeGenerated** property that contains the date and time that the record was created.</span></span>  <span data-ttu-id="19dc6-136">Una consulta en el portal de búsqueda de registros solo devuelve registros con una propiedad **TimeGenerated** dentro del ámbito de tiempo que aparece en el lado izquierdo de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="19dc6-136">A query in the Log Search portal only returns records with a **TimeGenerated** within the time scope that's displayed on the left side of the screen.</span></span>  

<span data-ttu-id="19dc6-137">Puede cambiar el filtro de tiempo seleccionando la lista desplegable o modificando el control deslizante.</span><span class="sxs-lookup"><span data-stu-id="19dc6-137">You can change the time filter either by selecting the dropdown or by modifying the slider.</span></span>  <span data-ttu-id="19dc6-138">El control deslizante muestra un gráfico de barras que muestra el número relativo de registros para cada segmento de tiempo dentro del rango.</span><span class="sxs-lookup"><span data-stu-id="19dc6-138">The slider displays a bar graph that shows the relative number of records for each time segment within the range.</span></span>  <span data-ttu-id="19dc6-139">Este segmento variará según el rango.</span><span class="sxs-lookup"><span data-stu-id="19dc6-139">This segment will vary depending on the range.</span></span>

<span data-ttu-id="19dc6-140">El ámbito de tiempo predeterminado es **1 día**.</span><span class="sxs-lookup"><span data-stu-id="19dc6-140">The default time scope is **1 day**.</span></span>  <span data-ttu-id="19dc6-141">Cambie este valor a **7 días** y el número total de registros aumentará.</span><span class="sxs-lookup"><span data-stu-id="19dc6-141">Change this value to **7 days**, and the total number of records should increase.</span></span>

![Ámbito de tiempo y fecha](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-the-query"></a><span data-ttu-id="19dc6-143">Filtrado de los resultados de la consulta</span><span class="sxs-lookup"><span data-stu-id="19dc6-143">Filter results of the query</span></span>
<span data-ttu-id="19dc6-144">En el lado izquierdo de la pantalla está el panel de filtros que le permite agregar filtros a la consulta sin necesidad de modificarla directamente.</span><span class="sxs-lookup"><span data-stu-id="19dc6-144">On the left side of the screen is the filter pane which allows you to add filtering to the query without modifying it directly.</span></span>  <span data-ttu-id="19dc6-145">Varias propiedades de los registros devueltos aparecen con sus diez valores principales junto con su recuento de registros.</span><span class="sxs-lookup"><span data-stu-id="19dc6-145">Several properties of the records returned are displayed with their top ten values with their record count.</span></span>

<span data-ttu-id="19dc6-146">Si está trabajando con **Event**, active la casilla junto a **Error** en **EVENTLEVELNAME**.</span><span class="sxs-lookup"><span data-stu-id="19dc6-146">If you're working with **Event**, select the checkbox next to **Error** under **EVENTLEVELNAME**.</span></span>   <span data-ttu-id="19dc6-147">Si está trabajando con **Syslog**, active la casilla junto a **Error** en **SEVERITYLEVEL**.</span><span class="sxs-lookup"><span data-stu-id="19dc6-147">If you're working with **Syslog**, select the checkbox next to **err** under **SEVERITYLEVEL**.</span></span>  <span data-ttu-id="19dc6-148">Esto cambia la consulta a una de las siguientes para limitar los resultados a los eventos de error.</span><span class="sxs-lookup"><span data-stu-id="19dc6-148">This changes the query to one of the following to limit the results to error events.</span></span>

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtrar](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

<span data-ttu-id="19dc6-150">Agregue propiedades al panel de filtros seleccionando **Agregar a filtros** en el menú de propiedades de uno de los registros.</span><span class="sxs-lookup"><span data-stu-id="19dc6-150">Add properties to the filter pane by selecting **Add to filters** from the property menu on one of the records.</span></span>

![Menú Agregar a filtros](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

<span data-ttu-id="19dc6-152">Puede establecer el mismo filtro seleccionando **Filtrar** desde el menú de propiedades de un registro con el valor que desea filtrar.</span><span class="sxs-lookup"><span data-stu-id="19dc6-152">You can set the same filter by selecting **Filter** from the property menu for a record with the value you want to filter.</span></span>  

<span data-ttu-id="19dc6-153">Solo aquellas propiedades que tienen el nombre en azul tienen la opción **Filtrar**.</span><span class="sxs-lookup"><span data-stu-id="19dc6-153">You only have the **Filter** option for properties with their name in blue.</span></span>  <span data-ttu-id="19dc6-154">Se trata de campos que permiten *búsquedas* que se indexan para las condiciones de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="19dc6-154">These are *searchable* fields which are indexed for search conditions.</span></span>  <span data-ttu-id="19dc6-155">Los campos en gris son campos que *permiten realizar búsquedas de texto libre* que solo tienen la opción **Mostrar referencias**.</span><span class="sxs-lookup"><span data-stu-id="19dc6-155">Fields in grey are *free text searchable* fields which only have the **Show references** option.</span></span>  <span data-ttu-id="19dc6-156">Esta opción devuelve los registros que contienen ese valor en cualquier propiedad.</span><span class="sxs-lookup"><span data-stu-id="19dc6-156">This option returns records that have that value in any property.</span></span>

![Menú Filtrar](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

<span data-ttu-id="19dc6-158">Puede agrupar los resultados de una sola propiedad seleccionando la opción **Agrupar por** en el menú de registro.</span><span class="sxs-lookup"><span data-stu-id="19dc6-158">You can group the results on a single property by selecting the **Group by** option in the record menu.</span></span>  <span data-ttu-id="19dc6-159">Esto agregará un operador [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) a la consulta que muestra los resultados en un gráfico.</span><span class="sxs-lookup"><span data-stu-id="19dc6-159">This will add a [summarize](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator to your query that displays the results in a chart.</span></span>  <span data-ttu-id="19dc6-160">Puede agrupar por más de una propiedad, pero deberá editar la consulta directamente.</span><span class="sxs-lookup"><span data-stu-id="19dc6-160">You can group on more than one property, but you would need to edit the query directly.</span></span>  <span data-ttu-id="19dc6-161">Seleccione el menú de registro situado junto a la propiedad **Computer** y seleccione **Agrupar por "Computer"**.</span><span class="sxs-lookup"><span data-stu-id="19dc6-161">Select the record menu next the the **Computer** property and select **Group by 'Computer'**.</span></span>  

![Agrupar por equipo](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a><span data-ttu-id="19dc6-163">Trabajo con resultados</span><span class="sxs-lookup"><span data-stu-id="19dc6-163">Work with results</span></span>
<span data-ttu-id="19dc6-164">El portal de búsqueda de registros tiene una variedad de características para trabajar con los resultados de una consulta.</span><span class="sxs-lookup"><span data-stu-id="19dc6-164">The Log Search portal has a variety of features for working with the results of a query.</span></span>  <span data-ttu-id="19dc6-165">Puede ordenar, filtrar y agrupar los resultados para analizar los datos sin modificar la consulta real.</span><span class="sxs-lookup"><span data-stu-id="19dc6-165">You can sort, filter, and group results to analyze the data without modifying the actual query.</span></span>  <span data-ttu-id="19dc6-166">Los resultados de una consulta no se ordenan de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="19dc6-166">Results of a query are not sorted by default.</span></span>

<span data-ttu-id="19dc6-167">Para ver los datos en un formato de tabla que proporciona opciones adicionales para filtrar y ordenar, haga clic en **Tabla**.</span><span class="sxs-lookup"><span data-stu-id="19dc6-167">To view the data in table form which provides additional options for filtering and sorting, click **Table**.</span></span>  

![Vista Tabla](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

<span data-ttu-id="19dc6-169">Haga clic en la flecha junto a un registro para ver los detalles de ese registro.</span><span class="sxs-lookup"><span data-stu-id="19dc6-169">Click the arrow by a record to view the details for that record.</span></span>

![Ordenar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

<span data-ttu-id="19dc6-171">Ordene cualquier campo haciendo clic en el encabezado de la columna.</span><span class="sxs-lookup"><span data-stu-id="19dc6-171">Sort on any field by clicking on its column header.</span></span>

![Ordenar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

<span data-ttu-id="19dc6-173">Filtre los resultados en un valor específico de la columna haciendo clic en el botón de filtro y proporcionando una condición de filtro.</span><span class="sxs-lookup"><span data-stu-id="19dc6-173">Filter the results on a specific value in the column by clicking the filter button and providing a filter condition.</span></span>

![Filtrar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

<span data-ttu-id="19dc6-175">Agrupe por una columna arrastrando el encabezado a la parte superior de los resultados.</span><span class="sxs-lookup"><span data-stu-id="19dc6-175">Group on a column by dragging its column header to the top of the results.</span></span>  <span data-ttu-id="19dc6-176">Puede agrupar por varios campos arrastrando varias columnas a la parte superior.</span><span class="sxs-lookup"><span data-stu-id="19dc6-176">You can group on multiple fields by dragging multiple columns to the top.</span></span>

![Agrupar resultados](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a><span data-ttu-id="19dc6-178">Trabajo con datos de rendimiento</span><span class="sxs-lookup"><span data-stu-id="19dc6-178">Work with performance data</span></span>
<span data-ttu-id="19dc6-179">Los datos de rendimiento de los agentes de Windows y Linux se almacenan en el área de trabajo de Log Analytics en la tabla **Perf**.</span><span class="sxs-lookup"><span data-stu-id="19dc6-179">Performance data for both Windows and Linux agents is stored in the Log Analytics workspace in the **Perf** table.</span></span>  <span data-ttu-id="19dc6-180">Los registros de rendimiento tienen la misma apariencia que cualquier otro registro y puede escribir una consulta sencilla que devuelva todos los datos de rendimiento igual que se hace con los eventos.</span><span class="sxs-lookup"><span data-stu-id="19dc6-180">Performance records look just like any other record, and we can write a simple query that returns all performance records just like with events.</span></span>

```
Perf
```

![Datos de rendimiento](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

<span data-ttu-id="19dc6-182">La devolución de millones de registros para todos los objetos y contadores de rendimiento no resulta muy útil.</span><span class="sxs-lookup"><span data-stu-id="19dc6-182">Returning millions of records for all performance objects and counters though isn't very useful.</span></span>  <span data-ttu-id="19dc6-183">Puede usar los mismos métodos empleados anteriormente para filtrar los datos o simplemente escribir la siguiente consulta directamente en el cuadro de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="19dc6-183">You can use the same methods you used above to filter the data or just type the following query directly into the log search box.</span></span>  <span data-ttu-id="19dc6-184">Esta devolverá únicamente los registros de utilización del procesador para los equipos con Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="19dc6-184">This returns only processor utilization records for both Windows and Linux computers.</span></span>

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Utilización del procesador](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

<span data-ttu-id="19dc6-186">Esto limita los datos a un contador determinado, pero aún no están en un formato que resulte especialmente útil.</span><span class="sxs-lookup"><span data-stu-id="19dc6-186">This limits the data to a particular counter, but it still doesn't put it in a form that's particularly useful.</span></span>  <span data-ttu-id="19dc6-187">Puede mostrar los datos en un gráfico de líneas, pero primero debe agruparlos por las propiedades Computer y TimeGenerated.</span><span class="sxs-lookup"><span data-stu-id="19dc6-187">You can display the data in a line chart, but first need to group it by Computer and TimeGenerated.</span></span>  <span data-ttu-id="19dc6-188">Para agrupar por varios campos, debe modificar la consulta directamente, así que modifíquela de la siguiente manera.</span><span class="sxs-lookup"><span data-stu-id="19dc6-188">To group on multiple fields, you need to modify the query directly, so modify the query to the following.</span></span>  <span data-ttu-id="19dc6-189">Esta utiliza la función [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) de la propiedad **CounterValue** para calcular el valor medio durante cada hora.</span><span class="sxs-lookup"><span data-stu-id="19dc6-189">This uses the [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) function on the **CounterValue** property to calculate the average value over each hour.</span></span>

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Gráfico con datos de rendimiento](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

<span data-ttu-id="19dc6-191">Ahora que los datos están agrupados adecuadamente, puede mostrarlos en un gráfico visual agregando el operador [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator).</span><span class="sxs-lookup"><span data-stu-id="19dc6-191">Now that the data is suitably grouped, you can display it in a visual chart by adding the [render](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operator.</span></span>  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Gráfico de líneas](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a><span data-ttu-id="19dc6-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19dc6-193">Next steps</span></span>

- <span data-ttu-id="19dc6-194">Obtenga más información sobre el lenguaje de consultas de Log Analytics en [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079) (Introducción al portal de análisis).</span><span class="sxs-lookup"><span data-stu-id="19dc6-194">Learn more about the Log Analytics query language at [Getting Started with the Analytics Portal](https://go.microsoft.com/fwlink/?linkid=856079).</span></span>
- <span data-ttu-id="19dc6-195">Realice un tutorial en el [portal avanzado de análisis](https://go.microsoft.com/fwlink/?linkid=856587) que le permita ejecutar las mismas consultas y acceder a los mismos datos que el portal de búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="19dc6-195">Walk through a tutorial using the [Advanced Analytics portal](https://go.microsoft.com/fwlink/?linkid=856587) which allows you to run the same queries and access the same data as the Log Search portal.</span></span>
