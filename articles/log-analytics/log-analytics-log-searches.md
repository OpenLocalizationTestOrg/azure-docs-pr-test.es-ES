---
title: "Búsqueda de datos con búsquedas de registros en Azure Log Analytics | Microsoft Docs"
description: "Las búsquedas de registros permiten combinar y correlacionar datos de equipo procedentes de varios orígenes dentro de su entorno."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bf237a837297cb8f1ab3a3340139133adcd2b244
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="9bc2e-103">Descripción de las búsquedas de registros en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9bc2e-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="9bc2e-104">En este artículo se describen las búsquedas de registros de Log Analytics mediante el lenguaje de consulta actual.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-104">This article describes log searches using the current query language in Log Analytics.</span></span>  <span data-ttu-id="9bc2e-105">Si el área de trabajo se ha actualizado al [nuevo lenguaje de consulta de Log Analytics](log-analytics-log-search-upgrade.md), debe consultar [Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md) (Descripción de las búsquedas de registros en Log Analytics [nuevo]).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-105">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer to [Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="9bc2e-106">La base de Log Analytics es la característica de búsqueda de registros que permite combinar y correlacionar datos de equipo procedentes de varios orígenes en el entorno.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-106">At the core of Log Analytics is the log search feature which allows you to combine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="9bc2e-107">Las soluciones también se basan en la búsqueda de registros con el objeto de proporcionarle métricas dinamizadas en torno a una área de problema determinada.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-107">Solutions are also powered by log search to bring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="9bc2e-108">En la página Buscar, puede crear una consulta y luego, al buscar, puede filtrar los resultados mediante controles de faceta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-108">On the Search page, you can create a query, and then when you search, you can filter the results by using facet controls.</span></span> <span data-ttu-id="9bc2e-109">También puede crear consultas avanzadas para transformar, filtrar y informar sobre sus resultados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-109">You can also create advanced queries to transform, filter, and report on your results.</span></span>

<span data-ttu-id="9bc2e-110">En la mayoría de las páginas de soluciones aparecen consultas de búsqueda comunes.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="9bc2e-111">En toda la consola de OMS, puede hacer clic en los iconos o explorar otros elementos para ver sus detalles mediante la búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-111">Throughout the OMS console, you can click tiles or drill in to other items to view details about the item by using log search.</span></span>

<span data-ttu-id="9bc2e-112">En este tutorial, usaremos ejemplos para cubrir todos los aspectos básicos del uso de la búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-112">In this tutorial, we'll walk through examples to cover all the basics when you use log search.</span></span>

<span data-ttu-id="9bc2e-113">Comenzaremos con ejemplos sencillos y prácticos y luego construiremos sobre ellos para que pueda comprender los casos de uso prácticos sobre cómo usar la sintaxis para extraer la información deseada de los datos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how to use the syntax to extract the insights you want from the data.</span></span>

<span data-ttu-id="9bc2e-114">Cuando se haya familiarizado con las técnicas de búsqueda, puede repasar la [Referencia sobre búsqueda de registros de Log Analytics](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-114">After you've familiar with search techniques, you can review the [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="9bc2e-115">Uso de filtros básicos</span><span class="sxs-lookup"><span data-stu-id="9bc2e-115">Use basic filters</span></span>
<span data-ttu-id="9bc2e-116">Lo primero que debe saber es que la primera parte de una consulta de búsqueda, antes de cualquier carácter de barra vertical "|", es siempre un *filtro*.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-116">The first thing to know is that the first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="9bc2e-117">Se puede considerar como una cláusula WHERE de TSQL en el sentido de que determina *qué* subconjunto de datos se va a extraer del almacén de datos de OMS.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data to pull out of the OMS data store.</span></span> <span data-ttu-id="9bc2e-118">La búsqueda en el almacén de datos consiste en gran medida en especificar las características de los datos que quiere extraer, por lo que es natural que una consulta comience con la cláusula WHERE.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-118">Searching in the data store is largely about specifying the characteristics of the data that you want to extract, so it is natural that a query would start with the WHERE clause.</span></span>

<span data-ttu-id="9bc2e-119">Los filtros más básicos que puede usar son *palabras clave*, como 'error' o 'tiempo de espera', o un nombre de equipo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-119">The most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="9bc2e-120">Estos tipos de consultas sencillas generalmente devuelven diversas formas de datos en el mismo conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-120">These types of simple queries generally return diverse shapes of data within the same result set.</span></span> <span data-ttu-id="9bc2e-121">Este es el motivo de que Log Analytics tenga distintos *tipos* de datos en el sistema.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-121">This is because Log Analytics has different *types* of data in the system.</span></span>

### <a name="to-conduct-a-simple-search"></a><span data-ttu-id="9bc2e-122">Para llevar a cabo una búsqueda simple</span><span class="sxs-lookup"><span data-stu-id="9bc2e-122">To conduct a simple search</span></span>
1. <span data-ttu-id="9bc2e-123">En el portal de OMS, haga clic en **Log Search**(Búsqueda de registros).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-123">In the OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="9bc2e-124">![icono de búsqueda](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="9bc2e-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="9bc2e-125">En el campo de consulta, escriba `error` y luego haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-125">In the query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="9bc2e-126">![error de búsqueda](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="9bc2e-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="9bc2e-127">Por ejemplo, la consulta de `error` en la siguiente imagen devolvió 100 000 registros de **Event** (recopilados por Administración del registro), 18 registros de **ConfigurationAlert** (generados por la evaluación de la configuración) y 12 registros de **ConfigurationChange** (capturados por el seguimiento de cambios).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-127">For example, the query for `error` in the following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by the Change Tracking).</span></span>   
    <span data-ttu-id="9bc2e-128">![resultados de la búsqueda](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="9bc2e-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="9bc2e-129">Estos filtros no son en realidad clases o tipos de objeto.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="9bc2e-130">*Type* es una etiqueta, una propiedad o una cadena/nombre/categoría, que se adjunta a una parte de los datos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-130">*Type* is just a tag, or a property, or a string/name/category, that is attached to a piece of data.</span></span> <span data-ttu-id="9bc2e-131">Algunos documentos del sistema están etiquetados como **Type:ConfigurationAlert** y otros como **Type:Perf** o **Type:Event**, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-131">Some documents in the system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="9bc2e-132">Cada resultado de búsqueda, documento, registro o entrada muestra todas las propiedades sin procesar y sus valores para cada uno de estas partes de los datos, y puede usar esos nombres de campo para especificar en el filtro cuándo quiere recuperar únicamente los registros donde el campo tiene ese valor dado.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-132">Each search result, document, record, or entry displays all the raw properties and their values for each of those pieces of data, and you can use those field names to specify in the filter when you want to retrieve only the records where the field has that given value.</span></span>

<span data-ttu-id="9bc2e-133">*Type* es simplemente un campo que todos los registros tienen, no es diferente de ningún otro campo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="9bc2e-134">Esto se estableció en función del valor del campo Type.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-134">This was established based on the value of the Type field.</span></span> <span data-ttu-id="9bc2e-135">Ese registro tendrá una forma diferente.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-135">That record will have a different shape or form.</span></span> <span data-ttu-id="9bc2e-136">Por cierto, **Type=Perf** o **Type=Event** es también la sintaxis que debe conocer para consultar datos o eventos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-136">Incidentally, **Type=Perf**, or **Type=Event** is also the syntax that you need to learn to query for performance data or events.</span></span>

<span data-ttu-id="9bc2e-137">Puede usar un signo de dos puntos (:) o un signo igual (=) después del nombre del campo y antes del valor.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-137">You can use either a colon (:) or an equal sign (=) after the field name and before the value.</span></span> <span data-ttu-id="9bc2e-138">**Type:Event** and **Type=Event** tienen un significado equivalente, así que puede elegir el estilo que prefiera.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose the style you prefer.</span></span>

<span data-ttu-id="9bc2e-139">Por lo tanto, si los registros Type=Perf tienen un campo llamado 'CounterName', puede escribir entonces una consulta parecida a `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-139">So, if the Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="9bc2e-140">Esta consulta solo le proporcionará los datos de rendimiento donde el nombre del contador de rendimiento sea "% de tiempo de procesador".</span><span class="sxs-lookup"><span data-stu-id="9bc2e-140">This will give you only the performance data where the performance counter name is "% Processor Time".</span></span>

### <a name="to-search-for-processor-time-performance-data"></a><span data-ttu-id="9bc2e-141">Para buscar datos de rendimiento de tiempo de procesador</span><span class="sxs-lookup"><span data-stu-id="9bc2e-141">To search for processor time performance data</span></span>
* <span data-ttu-id="9bc2e-142">En el campo de consulta de búsqueda, escriba `Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="9bc2e-142">In the search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="9bc2e-143">También puede ser más específico y usar **InstanceName=_'Total'** en la consulta, que es un contador de rendimiento de Windows.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-143">You can also be more specific and use **InstanceName=_'Total'** in the query, which is a Windows performance counter.</span></span> <span data-ttu-id="9bc2e-144">También puede seleccionar una faceta y otro **field:value**.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="9bc2e-145">El filtro se agrega automáticamente al filtro en la barra de consulta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-145">The filter is automatically added to your filter in the query bar.</span></span> <span data-ttu-id="9bc2e-146">Puede ver esto en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-146">You can see this in the following image.</span></span> <span data-ttu-id="9bc2e-147">Se muestra dónde hacer clic para agregar **InstanceName:’_Total’** a la consulta sin escribir nada.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-147">It shows you where to click to add **InstanceName:’_Total’** to the query without typing anything.</span></span>

![search facet](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="9bc2e-149">La consulta ahora se convierte en `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="9bc2e-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="9bc2e-150">En este ejemplo, no tiene que especificar **Type=Perf** para llegar a este resultado.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-150">In this example, you don't have to specify **Type=Perf** to get to this result.</span></span> <span data-ttu-id="9bc2e-151">Dado que los campos CounterName e InstanceName solo existen para los registros de Type=Perf, la consulta es lo suficientemente específica como para devolver los mismos resultados que la anterior, más larga:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-151">Because the fields CounterName and InstanceName only exist for records of Type=Perf, the query is specific enough to return the same results as the longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="9bc2e-152">Esto se debe a que todos los filtros de la consulta se evalúan como que están en *AND* con respecto al otro.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-152">This is because all the filters in the query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="9bc2e-153">Efectivamente, cuantos más campos agregue a los criterios, obtendrá resultados más o menos específicos y refinados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-153">Effectively, the more fields you add to the criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="9bc2e-154">Por ejemplo, la consulta `Type=Event EventLog="Windows PowerShell"` es idéntica a `Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-154">For example, the query `Type=Event EventLog="Windows PowerShell"` is identical to `Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="9bc2e-155">Devuelve todos los eventos que se registraron y se recopilaron del registro de eventos de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-155">It returns all events that were logged in and collected from the Windows PowerShell event log.</span></span> <span data-ttu-id="9bc2e-156">Si agrega un filtro varias veces seleccionando de manera repetida la misma faceta, entonces el problema es meramente cosmético; podría desordenar la barra de búsqueda, pero seguiría devolviendo los mismos resultados porque el operador AND implícito siempre está ahí.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-156">If you add a filter multiple times by repeatedly selecting the same facet, then the issue is purely cosmetic--it might clutter the Search bar, but it still returns the same results because the implicit AND operator is always there.</span></span>

<span data-ttu-id="9bc2e-157">Puede invertir fácilmente el operador AND implícito usando un operador NOT explícitamente.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-157">You can easily reverse the implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="9bc2e-158">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-158">For example:</span></span>

<span data-ttu-id="9bc2e-159">`Type:Event NOT(EventLog:"Windows PowerShell")` o su equivalente `Type=Event EventLog!="Windows PowerShell"` devuelven todos los eventos de todos los registros, EXCEPTO el registro de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT the Windows PowerShell log.</span></span>

<span data-ttu-id="9bc2e-160">O bien, puede usar otro operador booleano como 'OR'.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="9bc2e-161">La siguiente consulta devuelve registros en los que EventLog es Application OR System.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-161">The following query returns records for which the EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="9bc2e-162">Con la consulta anterior, obtendrá entradas para ambos registros en el mismo conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-162">Using the above query, you’ll get entries for both logs in the same result set.</span></span>

<span data-ttu-id="9bc2e-163">Sin embargo, si quita el operador OR dejando en su lugar el operador AND implícito, entonces la siguiente consulta no producirá ningún resultado porque no hay una entrada de registro de eventos que pertenezca a AMBOS registros.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-163">However, if you remove the OR by leaving the implicit AND in place, then the following query will not produce any results because there isn’t an event log entry that belongs to BOTH logs.</span></span> <span data-ttu-id="9bc2e-164">Cada entrada de registro de eventos se escribió para solo uno de los dos registros.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-164">Each event log entry was written to only one of the two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="9bc2e-165">Uso de filtros adicionales</span><span class="sxs-lookup"><span data-stu-id="9bc2e-165">Use additional filters</span></span>
<span data-ttu-id="9bc2e-166">La siguiente consulta devuelve entradas de dos registros de eventos para todos los equipos que han enviado datos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-166">The following query returns entries for 2 event logs for all the computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![search results](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="9bc2e-168">Al seleccionar uno de los campos o filtros se limitará la consulta a un equipo específico, sin incluir todos los demás.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-168">Selecting one of the fields or filters will narrow the query to a specific computer, excluding all other ones.</span></span> <span data-ttu-id="9bc2e-169">La consulta resultante podría parecerse a la siguiente.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-169">The resulting query would resemble the following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="9bc2e-170">La cual es equivalente a la siguiente debido al AND implícito.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-170">Which is equivalent to the following, because of the implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="9bc2e-171">Cada consulta se evalúa en el siguiente orden explícito.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-171">Each query is evaluated in the following explicit order.</span></span> <span data-ttu-id="9bc2e-172">Observe los paréntesis.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-172">Note the parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="9bc2e-173">Al igual que el campo de registro de eventos, solo puede recuperar datos de un conjunto de equipos específicos agregando OR.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-173">Just like the event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="9bc2e-174">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="9bc2e-175">Igualmente, la siguiente consulta devuelve el **% tiempo de CPU** solo para los dos equipos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-175">Similarly, this the following query return **% CPU Time** for the selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="9bc2e-176">Tipos de campo</span><span class="sxs-lookup"><span data-stu-id="9bc2e-176">Field types</span></span>
<span data-ttu-id="9bc2e-177">Cuando cree filtros, debe comprender las diferencias que existen al trabajar con los distintos tipos de campos que aparecen en las búsquedas de registros.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-177">When creating filters, you should understand the differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="9bc2e-178">Los **campos de búsqueda** se muestran en azul en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="9bc2e-179">Puede usar campos de búsqueda en condiciones de búsqueda específicas para el campo, como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-179">You can use searchable fields in search conditions specific to the field such as the following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="9bc2e-180">Los **campos de búsqueda de texto libre** se muestran en gris en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="9bc2e-181">No se pueden usar con condiciones de búsqueda específicas para el campo, como los campos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-181">They cannot be used with search conditions specific to the field like searchable fields.</span></span>  <span data-ttu-id="9bc2e-182">Se buscan solo al realizar una consulta en todos los campos, como la siguiente.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-182">They are only searched when performing a query across all fields such as the following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="9bc2e-183">Operadores booleanos</span><span class="sxs-lookup"><span data-stu-id="9bc2e-183">Boolean operators</span></span>
<span data-ttu-id="9bc2e-184">Con los campos de fecha y hora, y numéricos, puede buscar valores mediante *mayor que*, *menor que* y *menor o igual que*.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="9bc2e-185">Puede usar operadores simples como >, < , >=, <= , !=, en la barra de búsqueda de consulta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-185">You can use simple operators such as >, < , >=, <= , != in the query search bar.</span></span>

<span data-ttu-id="9bc2e-186">Puede consultar un registro de eventos específico para un período de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="9bc2e-187">Por ejemplo, las últimas 24 horas se expresan con la siguiente expresión mnemotécnica.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-187">For example, the last 24 hours is expressed with the following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="to-search-using-a-boolean-operator"></a><span data-ttu-id="9bc2e-188">Para realizar búsquedas mediante un operador booleano</span><span class="sxs-lookup"><span data-stu-id="9bc2e-188">To search using a boolean operator</span></span>
* <span data-ttu-id="9bc2e-189">En el campo de consulta de búsqueda, escriba `EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="9bc2e-189">In the search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="9bc2e-190">![búsqueda con booleano](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="9bc2e-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="9bc2e-191">Aunque puede controlar el intervalo de tiempo gráficamente, y casi siempre es recomendable hacerlo, resulta beneficioso incluir un filtro de tiempo directamente en la consulta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-191">Although you can control the time interval graphically, and most times you might want to do that, there are advantages to including a time filter directly into the query.</span></span> <span data-ttu-id="9bc2e-192">Por ejemplo, esto funciona bien con paneles donde puede invalidar el tiempo de cada icono, con independencia del selector de tiempo *global* de la página del panel.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-192">For example, this works great with dashboards where you can override the time for each tile, regardless of the *global* time selector on the dashboard page.</span></span> <span data-ttu-id="9bc2e-193">Para obtener más información, consulte [Cuestiones sobre el tiempo en el panel](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="9bc2e-194">Si desea filtrar por tiempo, tenga en cuenta que se obtienen resultados para la *intersección* de los dos períodos: el especificado en el portal de OMS (S1) y el especificado en la consulta (S2).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-194">When filtering by time, keep in mind that you get results for the *intersection* of the two time periods: the one specified in the OMS portal (S1) and the one specified in the query (S2).</span></span>

![intersección](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="9bc2e-196">Esto significa que, si los períodos no se cruzan, por ejemplo en el portal de OMS donde elige **esta semana** y en la consulta donde define **última semana**, entonces no hay ninguna intersección y no recibirá ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-196">This means, if the time periods don’t intersect, for example in the OMS portal where you choose **This week** and in the query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="9bc2e-197">Los operadores de comparación usados con el campo TimeGenerated también son útiles en otras situaciones.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-197">Comparison operators used for the TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="9bc2e-198">Por ejemplo, con los campos numéricos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-198">For example, with numeric fields.</span></span>

<span data-ttu-id="9bc2e-199">Por ejemplo, dado que las alertas de evaluación de la configuración tienen los siguientes valores de gravedad:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-199">For example, given that Configuration Assessment’s alerts have the following severity values:</span></span>

* <span data-ttu-id="9bc2e-200">0 = Información</span><span class="sxs-lookup"><span data-stu-id="9bc2e-200">0 = Information</span></span>
* <span data-ttu-id="9bc2e-201">1= Advertencia</span><span class="sxs-lookup"><span data-stu-id="9bc2e-201">1 = Warning</span></span>
* <span data-ttu-id="9bc2e-202">2 = Crítico</span><span class="sxs-lookup"><span data-stu-id="9bc2e-202">2 = Critical</span></span>

<span data-ttu-id="9bc2e-203">Puede consultar las alertas de advertencia y críticas y también excluir las informativas con la siguiente consulta:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-203">You can query for both warning and critical alerts and also exclude informational ones with the following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="9bc2e-204">También puede usar consultas por rango.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-204">You can also use range queries.</span></span> <span data-ttu-id="9bc2e-205">Esto significa que puede proporcionar el intervalo inicial y final de los valores de una secuencia.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-205">This means that you can provide the beginning and end range of values in a sequence.</span></span> <span data-ttu-id="9bc2e-206">Por ejemplo, si desea los eventos del registro de eventos de Operations Manager en los que EventID sea mayor o igual que 2100 pero no superior a 2199, la siguiente consulta devolvería estos valores.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-206">For example, if you want events from the Operations Manager event log where the EventID is greater than or equal to 2100 but not greater than 2199, then the following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="9bc2e-207">La sintaxis de intervalo que debe usar es el separador dos puntos (:) field:value y *no* el signo igual (=).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-207">The range syntax you must use is the colon (:) field:value separator and *not* the equal sign (=).</span></span> <span data-ttu-id="9bc2e-208">Incluya el extremo inferior y superior del intervalo entre corchetes y sepárelos con dos puntos (..).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-208">Enclose the lower and upper end of the range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="9bc2e-209">Manipulación de los resultados de búsqueda</span><span class="sxs-lookup"><span data-stu-id="9bc2e-209">Manipulate search results</span></span>
<span data-ttu-id="9bc2e-210">Al buscar datos, querrá refinar la consulta de búsqueda y tener un buen nivel de control sobre los resultados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-210">When you're searching for data, you'll want to refine your search query and have a good level of control over the results.</span></span> <span data-ttu-id="9bc2e-211">Cuando se recuperen los resultados, puede aplicar comandos para transformarlos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-211">When results are retrieved, you can apply commands to transform them.</span></span>

<span data-ttu-id="9bc2e-212">Los comandos de las búsquedas de Log Analytics *deben* seguir al carácter de barra vertical (|).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-212">Commands in Log Analytics searches *must* follow after the vertical pipe character (|).</span></span> <span data-ttu-id="9bc2e-213">Un filtro debe ser siempre la primera parte de una cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-213">A filter must always be the first part of a query string.</span></span> <span data-ttu-id="9bc2e-214">Define el conjunto de datos con el que trabaja y luego "canaliza" esos resultados en un comando.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-214">It defines the data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="9bc2e-215">Luego puede usar la canalización para agregar comandos adicionales.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-215">You can then use the pipe to add additional commands.</span></span> <span data-ttu-id="9bc2e-216">Es parecido a grandes rasgos a la canalización de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-216">This is loosely similar to the Windows PowerShell pipeline.</span></span>

<span data-ttu-id="9bc2e-217">En general, el lenguaje de búsqueda de Log Analytics intenta seguir el estilo y los criterios de PowerShell a fin de que sea familiar para los profesionales de TI y para facilitar la curva de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-217">In general, the Log Analytics search language tries to follow PowerShell style and guidelines to make it similar to the IT pros, and to ease the learning curve.</span></span>

<span data-ttu-id="9bc2e-218">Los comandos tienen nombres de verbos para que pueda saber fácilmente lo que hacen.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="9bc2e-219">Sort</span><span class="sxs-lookup"><span data-stu-id="9bc2e-219">Sort</span></span>
<span data-ttu-id="9bc2e-220">El comando sort permite definir el criterio de ordenación por uno o varios campos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-220">The sort command allows you to define the sorting order by one or multiple fields.</span></span> <span data-ttu-id="9bc2e-221">Aunque no lo use, se aplica de forma predeterminada un tiempo en orden descendente.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="9bc2e-222">Los resultados más recientes siempre están en la parte superior de los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-222">The most recent results are always at the top of search results.</span></span> <span data-ttu-id="9bc2e-223">Esto significa que cuando ejecuta una búsqueda con `Type=Event EventID=1234` , lo que realmente se ejecuta es:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="9bc2e-224">Esto se debe a que es el tipo de experiencia con el que está familiarizado en los registros.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-224">That's because it is the type of experience you are familiar with in logs.</span></span> <span data-ttu-id="9bc2e-225">Por ejemplo, en el Visor de eventos de Windows.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-225">For example, in the Windows Event Viewer.</span></span>

<span data-ttu-id="9bc2e-226">Puede usar el comando Sort para cambiar la forma en que se devuelven los resultados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-226">You can use Sort to change the way results are returned.</span></span> <span data-ttu-id="9bc2e-227">En los ejemplos siguientes se muestra cómo funciona este comando.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-227">The following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="9bc2e-228">Los sencillos ejemplos anteriores muestran cómo funcionan los comandos; estos cambian la forma de los resultados que devuelve el filtro.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-228">The simple examples above show you how commands work--they change the shape of the results that the filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="9bc2e-229">Limit y Top</span><span class="sxs-lookup"><span data-stu-id="9bc2e-229">Limit and top</span></span>
<span data-ttu-id="9bc2e-230">Otro comando menos conocido es LIMIT.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="9bc2e-231">Limit es un verbo al estilo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="9bc2e-232">Es funcionalmente idéntico al comando TOP.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-232">Limit is functionally identical to the TOP command.</span></span> <span data-ttu-id="9bc2e-233">Las consultas siguientes devuelven los mismos resultados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-233">The following queries return the same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="to-search-using-top"></a><span data-ttu-id="9bc2e-234">Para realizar búsquedas con TOP</span><span class="sxs-lookup"><span data-stu-id="9bc2e-234">To search using top</span></span>
* <span data-ttu-id="9bc2e-235">En el campo de consulta de búsqueda, escriba `Type=Event EventID=600 | Top 1` .</span><span class="sxs-lookup"><span data-stu-id="9bc2e-235">In the search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="9bc2e-236">![búsqueda con Top](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="9bc2e-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="9bc2e-237">En la imagen anterior, hay 358 000 registros con EventID=600.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-237">In the image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="9bc2e-238">Los campos, las facetas y los filtros de la izquierda siempre muestran información sobre los resultados devueltos *por la parte de filtro* de la consulta, que es la situada delante de cualquier carácter de barra vertical.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-238">The fields, facets, and filters on the left always show information about the results returned *by the filter portion* of the query, which is the part before any pipe character.</span></span> <span data-ttu-id="9bc2e-239">El panel **Resultados** solo devuelve el resultado más reciente (1), porque el comando de ejemplo ha dado forma a los resultados y los ha transformado.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-239">The **Results** pane only returns the most recent 1 result, because the example command shaped and transformed the results.</span></span>

### <a name="select"></a><span data-ttu-id="9bc2e-240">Seleccionar</span><span class="sxs-lookup"><span data-stu-id="9bc2e-240">Select</span></span>
<span data-ttu-id="9bc2e-241">El comando SELECT se comporta como Select-Object en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-241">The SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="9bc2e-242">Devuelve los resultados filtrados que no tienen todas sus propiedades originales.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="9bc2e-243">En su lugar, selecciona solo las propiedades que especifique.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-243">Instead, it selects only the properties that you specify.</span></span>

#### <a name="to-run-a-search-using-the-select-command"></a><span data-ttu-id="9bc2e-244">Para ejecutar una búsqueda con el comando Select</span><span class="sxs-lookup"><span data-stu-id="9bc2e-244">To run a search using the select command</span></span>
1. <span data-ttu-id="9bc2e-245">En el campo de búsqueda, escriba `Type=Event` y luego haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="9bc2e-246">Haga clic en **+ mostrar más** en uno de los resultados para ver todas las propiedades que tienen los resultados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-246">Click **+ show more** in one of the results to view all the properties that the results have.</span></span>
3. <span data-ttu-id="9bc2e-247">Seleccione algunas de ellas explícitamente y la consulta cambiará a `Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-247">Select some of those explicitly, and the query changes to `Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="9bc2e-248">![Búsqueda con Select](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="9bc2e-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="9bc2e-249">Se trata de un comando especialmente útil cuando desea controlar los resultados de búsqueda y elegir solo las partes de los datos que realmente importan para la exploración, que casi siempre no son el registro completo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-249">This command is particularly useful when you want to control search output and choose only the portions of data that really matter for your exploration, which often isn’t the full record.</span></span> <span data-ttu-id="9bc2e-250">También es útil cuando registros de diferentes tipos tienen *algunas* propiedades en común, pero no *todas*.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="9bc2e-251">Luego, puede generar resultados con la apariencia natural de una tabla, o que funcionan bien cuando se exportan a un archivo CSV y luego se transforman en Excel.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-251">The, you can generate output that looks more naturally like a table, or work well when exported to a CSV file and then massaged in Excel.</span></span>

## <a name="use-the-measure-command"></a><span data-ttu-id="9bc2e-252">Uso del comando measure</span><span class="sxs-lookup"><span data-stu-id="9bc2e-252">Use the measure command</span></span>
<span data-ttu-id="9bc2e-253">MEASURE es uno de los comandos más versátiles en las búsquedas de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-253">MEASURE is one of the most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="9bc2e-254">Permite aplicar *funciones* estadísticas a los datos y agregar los resultados agrupados por un campo dado.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-254">It allows you to apply statistical *functions* to your data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="9bc2e-255">Son muchas las funciones estadísticas que admite este comando.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="9bc2e-256">Measure count()</span><span class="sxs-lookup"><span data-stu-id="9bc2e-256">Measure count()</span></span>
<span data-ttu-id="9bc2e-257">La primera función estadística con la que se trabaja y una de las más fáciles de entender es la función *count()* .</span><span class="sxs-lookup"><span data-stu-id="9bc2e-257">The first statistical function to work with, and one of the simplest to understand is the *count()* function.</span></span>

<span data-ttu-id="9bc2e-258">Los resultados de cualquier consulta de búsqueda como `Type=Event`, muestran filtros también llamados facetas en el lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-258">Results from any search query such as `Type=Event`, show filters also called facets on the left side of search results.</span></span> <span data-ttu-id="9bc2e-259">Los filtros muestran una distribución de valores por un campo dado de los resultados de la búsqueda realizada.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-259">The filters show a distribution of values by a given field for the results in the search executed.</span></span>

![search measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="9bc2e-261">Por ejemplo, en la imagen anterior verá el campo **Computer**, y muestra que dentro de los casi 739 000 eventos de los resultados, hay 68 valores únicos y distintos para ese **Computer** campo en esos registros.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-261">For example, in the image above you'll see the **Computer** field and it shows that within the almost 739 thousand events in the results, there are 68 unique and distinct values for the **Computer** field in those records.</span></span> <span data-ttu-id="9bc2e-262">El icono solo muestra los cinco principales, que son los cinco valores más comunes que están escritos en el campo **Computer** , ordenados por el número de documentos que contienen ese valor específico en ese campo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-262">The tile only shows the top 5, which are the most common 5 values that are written in the **Computer** fields), sorted by the number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="9bc2e-263">En la imagen se ve que, entre esos eventos casi 369 000 eventos, 90 000 proceden del equipo OpsInsights04.contoso.com, 83 000 del equipo DB03.contoso.com y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-263">In the image you can see that – among those almost 369 thousand events – 90 thousand come from the OpsInsights04.contoso.com computer, 83 thousand from the DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="9bc2e-264">¿Y si quisiera ver todos los valores, ya que el icono solo muestra los cinco primeros?</span><span class="sxs-lookup"><span data-stu-id="9bc2e-264">What if you want to see all values, since the tile only shows only the top 5?</span></span>

<span data-ttu-id="9bc2e-265">Eso es lo que puede hacer el comando measure con la función count().</span><span class="sxs-lookup"><span data-stu-id="9bc2e-265">That’s what the measure command can do with the count() function.</span></span> <span data-ttu-id="9bc2e-266">Esta función no usa ningún parámetro.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="9bc2e-267">Usted solo especifica el campo por el que desea agrupar, en este caso, el campo **Computer** :</span><span class="sxs-lookup"><span data-stu-id="9bc2e-267">You just specify the field by which you want to group by – the **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![search measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="9bc2e-269">Sin embargo, **Computer** es simplemente un campo usado *en* cada dato; no hay ninguna base de datos relacional implicada y no hay ningún objeto **Computer** independiente en ninguna parte.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="9bc2e-270">Los valores *en* los datos bastan para describir la entidad que los ha generado, así como otras características y aspectos de los datos; de ahí el término *faceta*.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-270">Just the values *in* the data can describe which entity generated them, and a number of other characteristics and aspects of the data – hence the term *facet*.</span></span> <span data-ttu-id="9bc2e-271">Sin embargo, también puede agrupar por otros campos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="9bc2e-272">Dado que los resultados originales de casi 739 000 eventos que se canalizan al comando measure también tienen un campo denominado **EventID**, puede aplicar la misma técnica para agrupar por ese campo y obtener un recuento de eventos por EventID:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-272">Because the original results of almost 739 thousand events that are piped into the measure command also have a field called **EventID**, you can apply the same technique to group by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="9bc2e-273">Si no está interesado en el número de registros real que contiene un valor específico, sino que solo quiere una lista de valores propiamente dichos, puede agregar un comando *Select* al final de la misma y seleccionar la primera columna:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-273">If you're not interested in the actual record count that contain a specific value, but instead if you only want a list of the values themselves, you can add a *Select* command at the end of it and just select the first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="9bc2e-274">Así puede obtener resultados más intrincados y ordenarlos previamente en la consulta, o también puede hacer simplemente clic en las columnas de la cuadrícula.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-274">Then you can get more intricate and pre-sort the results in the query, or you can just click the columns in the grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="to-search-using-measure-count"></a><span data-ttu-id="9bc2e-275">Para buscar mediante measure count</span><span class="sxs-lookup"><span data-stu-id="9bc2e-275">To search using measure count</span></span>
* <span data-ttu-id="9bc2e-276">En el campo de consulta de búsqueda, escriba `Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="9bc2e-276">In the search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="9bc2e-277">Anexe `| Select EventID` al final de la consulta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-277">Append `| Select EventID` to the end of the query.</span></span>
* <span data-ttu-id="9bc2e-278">Finalmente, anexe `| Sort EventID asc` al final de la consulta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-278">Finally, append `| Sort EventID asc` to the end of the query.</span></span>

<span data-ttu-id="9bc2e-279">Hay un par de cuestiones importantes que es necesario observar y resaltar:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-279">There are a couple important points to notice and emphasize:</span></span>

<span data-ttu-id="9bc2e-280">En primer lugar, los resultados que ve ya no son los resultados sin formato originales.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-280">First, the results you see are not the original raw results anymore.</span></span> <span data-ttu-id="9bc2e-281">Son los resultados de agregado, básicamente grupos de resultados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="9bc2e-282">Esto no supone un problema, pero debe comprender que está interactuando con una forma muy diferente de los datos que difiere de la forma sin formato original que se crea sobre la marcha como resultado de la función estadística o de agregación.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from the original raw shape that gets created on the fly as a result of the aggregation/statistical function.</span></span>

<span data-ttu-id="9bc2e-283">En segundo lugar, **Measure count** solo devuelve actualmente los 100 primeros resultados diferentes.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-283">Second, **Measure count** currently returns only the top 100 distinct results.</span></span> <span data-ttu-id="9bc2e-284">Este límite no se aplica a las otras funciones estadísticas.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-284">This limit does not apply to the other statistical functions.</span></span> <span data-ttu-id="9bc2e-285">Por lo tanto, normalmente deberá usar primero un filtro más preciso para buscar elementos específicos antes de aplicar measure count().</span><span class="sxs-lookup"><span data-stu-id="9bc2e-285">So, you'll usually need to use a more precise filter first to search for specific items before you apply measure count().</span></span>

## <a name="use-the-max-and-min-functions-with-the-measure-command"></a><span data-ttu-id="9bc2e-286">Uso de las funciones max y min con el comando measure</span><span class="sxs-lookup"><span data-stu-id="9bc2e-286">Use the max and min functions with the measure command</span></span>
<span data-ttu-id="9bc2e-287">Son varias las situaciones en las que **Measure Max()** y **Measure Min()** son útiles.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="9bc2e-288">Sin embargo, puesto que cada función es opuesta entre sí, ilustraremos Max() y usted puede experimentar con Min() por su cuenta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="9bc2e-289">Si busca eventos de seguridad, tienen una propiedad **Level** que puede variar.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="9bc2e-290">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-290">For example:</span></span>

```
Type=SecurityEvent
```

![search measure count start](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="9bc2e-292">Si quiere ver el valor más alto de todos los eventos de seguridad dado un equipo común, puede usar agrupar por campo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-292">If you want to view the highest value for all of the security events given a common Computer, the group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![search measure max computer](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="9bc2e-294">Mostrará que, para los equipos con registros **Level**, la mayoría tiene al menos el nivel 8 y muchos, el nivel 16.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-294">It will display that for the computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![search measure max time generated computer](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="9bc2e-296">Esta función es muy adecuada para números, pero también para campos de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="9bc2e-297">Resulta útil para comprobar la última marca de tiempo o la más reciente en cualquier parte de los datos indexados para cada equipo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-297">It is useful to check for the last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="9bc2e-298">Por ejemplo: ¿cuándo se notificó el evento de seguridad más reciente para cada máquina?</span><span class="sxs-lookup"><span data-stu-id="9bc2e-298">For example: When was the most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-the-avg-function-with-the-measure-command"></a><span data-ttu-id="9bc2e-299">Uso de la función avg con el comando measure</span><span class="sxs-lookup"><span data-stu-id="9bc2e-299">Use the avg function with the measure command</span></span>
<span data-ttu-id="9bc2e-300">La función estadística Avg() usada con measure le permite calcular el valor medio de algún campo y agrupar los resultados por el mismo campo u otro diferente.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-300">The Avg() statistical function used with measure allows you to calculate the average value for some field, and group results by the same or other field.</span></span> <span data-ttu-id="9bc2e-301">Esto resulta útil en muchos casos, por ejemplo, con los datos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="9bc2e-302">Comenzaremos con los datos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-302">We'll start with performance data.</span></span> <span data-ttu-id="9bc2e-303">Tenga en cuenta que OMS actualmente recopila contadores de rendimiento tanto para equipos Windows como Linux.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="9bc2e-304">Para buscar *todos* los datos de rendimiento, la consulta más básica es:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-304">To search for *all* performance data, the most basic query is:</span></span>

```
Type=Perf
```

![search avg start](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="9bc2e-306">Lo primero que notará es que Log Analytics muestra tres perspectivas: Lista, que muestra los registros en los que se basan los gráficos; Tabla, que muestra una vista tabular de los datos de los contadores de rendimiento; y Métricas, que muestra gráficos para los contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-306">The first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows the actual records behind the charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for the performance counters.</span></span>

<span data-ttu-id="9bc2e-307">En la imagen anterior, hay dos conjuntos de campos marcados que indican lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-307">In the image above, there are two sets of fields marked that indicate the following:</span></span>

* <span data-ttu-id="9bc2e-308">El primer conjunto identifica el nombre del contador de rendimiento de Windows, el nombre del objeto y el nombre de instancia en el filtro de consulta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-308">The first set identifies Windows Performance Counter Name, Object Name, and Instance Name in the query filter.</span></span> <span data-ttu-id="9bc2e-309">Estos son los campos que usará probablemente como facetas o filtros:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-309">These are the fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="9bc2e-310">**CounterValue** es el valor real del contador.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-310">**CounterValue** is the actual value of the counter.</span></span> <span data-ttu-id="9bc2e-311">En este ejemplo, el valor es *75*.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-311">In this example, the value is *75*.</span></span>
* <span data-ttu-id="9bc2e-312">**TimeGenerated** es 12:51, en formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="9bc2e-313">Esta es una vista de las métricas en un gráfico.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-313">Here's a view of the metrics in a graph.</span></span>

![search avg start](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="9bc2e-315">Después de leer sobre la forma de los registros Perf y de haber leído sobre otras técnicas de búsqueda, puede usar measure Avg() para agregar este tipo de datos numéricos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-315">After reading about the Perf record shape, and having read about other search techniques, you can use measure Avg() to aggregate this type of numerical data.</span></span>

<span data-ttu-id="9bc2e-316">A continuación se muestra un sencillo ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![search avg samplevalue](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="9bc2e-318">En este ejemplo, selecciona el contador de rendimiento de tiempo total de la CPU y el promedio por equipo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-318">In this example, you select the CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="9bc2e-319">Si desea restringir los resultados a solo las últimas 6 horas, puede usar el control de filtro de tiempo o especificarlo en la consulta de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-319">If you want to narrow down your results to only the last 6 hours, you can either use the time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="to-search-using-the-avg-function-with-the-measure-command"></a><span data-ttu-id="9bc2e-320">Para buscar con la función avg con el comando measure</span><span class="sxs-lookup"><span data-stu-id="9bc2e-320">To search using the avg function with the measure command</span></span>
* <span data-ttu-id="9bc2e-321">En el campo de consulta de búsqueda, escriba `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-321">In the Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="9bc2e-322">Puede agregar y correlacionar los datos *entre* equipos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="9bc2e-323">Por ejemplo, imagine que tiene un conjunto de hosts en algún tipo de granja de servidores donde cada nodo es igual a otro y todos hacen el mismo tipo de trabajo, y la carga se debe equilibrar de manera aproximada.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal to any other one and they just do all the same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="9bc2e-324">Podría obtener sus contadores en un solo paso con la siguiente consulta y conseguir los promedios para toda la granja.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-324">You could get their counters all in one go with the following query and get averages for the entire farm.</span></span> <span data-ttu-id="9bc2e-325">Puede comenzar eligiendo los equipos con el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-325">You can start by choosing the computers with the following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="9bc2e-326">Ahora que tiene los equipos, solo quiere seleccionar dos indicadores clave de rendimiento (KPI): % de uso de la CPU y % de espacio libre en disco.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-326">Now that you have the computers, you also only want to select two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="9bc2e-327">Por lo tanto, esa parte de la consulta se convierte en:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-327">So, that part of the query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="9bc2e-328">Ahora puede agregar equipos y contadores con el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-328">Now you can add computers and counters with the following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="9bc2e-329">Como tiene una selección muy específica, el comando **measure Avg()** puede devolver el promedio no por equipo, sino en la granja de servidores, con solo agrupar por CounterName.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-329">Because you have a very specific selection, the **measure Avg()** command can return the average not by computer, but across the farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="9bc2e-330">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="9bc2e-331">Esto proporciona una vista útil compacta de un par de KPI de su entorno.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![search avg grouping](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="9bc2e-333">Puede usar fácilmente la consulta de búsqueda en un panel.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-333">You can easily use the search query in a dashboard.</span></span> <span data-ttu-id="9bc2e-334">Por ejemplo, puede guardar la consulta de búsqueda y crear un panel a partir de ella llamado *KPI de granja de servidores web*.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-334">For example, you could save the search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="9bc2e-335">Para aprender más acerca del uso de paneles, consulte [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md)(Creación de un panel personalizado en Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-335">To learn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![search avg dashboard](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-the-sum-function-with-the-measure-command"></a><span data-ttu-id="9bc2e-337">Uso de la función sum con el comando measure</span><span class="sxs-lookup"><span data-stu-id="9bc2e-337">Use the sum function with the measure command</span></span>
<span data-ttu-id="9bc2e-338">La función sum es similar a otras funciones del comando measure.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-338">The sum function is similar to other functions of the measure command.</span></span> <span data-ttu-id="9bc2e-339">Puede ver un ejemplo sobre cómo usar la función sum en [Búsqueda de registros de W3C IIS en Visión operativa de Microsoft Azure](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-339">You can see an example about how to use the sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="9bc2e-340">Puede usar Max() y Min() con cadenas de texto, números, fechas y horas.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="9bc2e-341">Con cadenas de texto, se ordenan alfabéticamente y obtiene la primera y la última.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="9bc2e-342">Sin embargo, no puede usar Sum() con campos que no sean numéricos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="9bc2e-343">Esto también se aplica a Avg().</span><span class="sxs-lookup"><span data-stu-id="9bc2e-343">This also applies to Avg().</span></span>

### <a name="use-the-percentile-function-with-the-measure-command"></a><span data-ttu-id="9bc2e-344">Uso de la función percentile con el comando measure</span><span class="sxs-lookup"><span data-stu-id="9bc2e-344">Use the percentile function with the measure command</span></span>
<span data-ttu-id="9bc2e-345">La función percentile se parece a Avg() y Sum() en que solo se puede usar para campos numéricos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-345">The percentile function is similar to Avg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="9bc2e-346">Puede utilizar cualquier percentil entre 1 y 99 en un campo numérico.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-346">You can use any percentile between 1 to 99 on a numeric field.</span></span> <span data-ttu-id="9bc2e-347">También puede usar ambos comandos, **percentile** y **pct**.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="9bc2e-348">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-the-where-command"></a><span data-ttu-id="9bc2e-349">Uso del comando where</span><span class="sxs-lookup"><span data-stu-id="9bc2e-349">Use the where command</span></span>
<span data-ttu-id="9bc2e-350">El comando where funciona como un filtro, pero se puede aplicar en la canalización para filtrar aún más los resultados agregados producidos por un comando measure, por oposición a los resultados sin formato que se filtran al principio de una consulta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-350">The where command works like a filter, but it can be applied in the pipeline to further filter aggregated results that have been produced by a Measure command – as opposed to raw results that are filtered at the beginning of a query.</span></span>

<span data-ttu-id="9bc2e-351">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="9bc2e-352">Puede agregar otro carácter de barra vertical "|" y el comando where para obtener solo los equipos cuyo promedio de CPU sea superior al 80 %, con el siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-352">You can add another pipe "|" character and the Where command to only get computers whose average CPU is above 80%, with the following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="9bc2e-353">Si está familiarizado con Microsoft System Center Operations Manager, puede considerar el comando where en términos de módulo de administración.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of the where command in management pack terms.</span></span> <span data-ttu-id="9bc2e-354">Si el ejemplo fuera una regla, la primera parte de la consulta sería el origen de datos y el comando where sería la detección de condición.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-354">If the example were a rule, the first part of the query would be the data source and the where command would be the condition detection.</span></span>

<span data-ttu-id="9bc2e-355">Puede usar la consulta como icono en **Mi panel**, como monitor de ordenaciones, para ver cuándo las CPU de equipo se sobreutilizan.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-355">You can use the query as a tile in **My Dashboard**, as a monitor of sorts, to see when computer CPUs are over-utilized.</span></span> <span data-ttu-id="9bc2e-356">Para aprender más acerca de los paneles, consulte [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md)(Creación de un panel personalizado en Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-356">To learn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="9bc2e-357">También puede crear y usar paneles mediante la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-357">You can also create and use dashboards using the mobile app.</span></span> <span data-ttu-id="9bc2e-358">Para más información, consulte la [aplicación móvil de OMS](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="9bc2e-359">En los dos iconos inferiores de la siguiente imagen, puede ver que el monitor se muestra como una lista y como un número.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-359">In the bottom two tiles of the following image, you can see the monitor displayed a list and as a number.</span></span> <span data-ttu-id="9bc2e-360">Básicamente, desea siempre que el número sea cero y la lista esté vacía.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-360">Essentially, you always want the number to be zero and the list to be empty.</span></span> <span data-ttu-id="9bc2e-361">De lo contrario, indica una condición de alerta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="9bc2e-362">Si es necesario, puede usarlo para ver qué máquinas están bajo presión.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-362">If needed, you can use it to take a look at which machines are under pressure.</span></span>

![mobile dashboard](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-the-in-operator"></a><span data-ttu-id="9bc2e-364">Uso del operador in</span><span class="sxs-lookup"><span data-stu-id="9bc2e-364">Use the in operator</span></span>
<span data-ttu-id="9bc2e-365">El operador *IN*, junto con *NOT IN*, permite usar subbúsquedas, que son búsquedas que incluyen otra búsqueda como argumento.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-365">The *IN* operator, along with *NOT IN* allows you to use subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="9bc2e-366">Se encierran entre llaves {} dentro de otra búsqueda *principal* o *exterior*.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="9bc2e-367">El resultado de una subbúsqueda, con frecuencia una lista de resultados distintos, se usa a continuación como argumento en su búsqueda principal.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-367">The result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="9bc2e-368">Puede usar subbúsquedas para hacer coincidir subconjuntos de los datos que no se puedan describir directamente en una expresión de búsqueda, pero que se puedan generar a partir de una búsqueda.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-368">You can use subsearches to match subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="9bc2e-369">Por ejemplo, si está interesado en usar una búsqueda para encontrar todos los eventos de *equipos donde faltan actualizaciones de seguridad*, debe diseñar una subbúsqueda que identifique esos *equipos donde faltan actualizaciones de seguridad* antes de buscar los eventos que pertenezcan a dichos hosts.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-369">For example, if you’re interested in using one search to find all events from *computers missing security updates*, then you need to design a subsearch that first identifies that *computers missing security updates* before it finds events belonging to those hosts.</span></span>

<span data-ttu-id="9bc2e-370">Por lo tanto, puede expresar *equipos donde actualmente faltan actualizaciones de seguridad* con la siguiente consulta:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-370">So, you could express *computers currently missing required security updates* with the following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![Ejemplo de búsqueda con IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="9bc2e-372">Una vez que tenga la lista, puede usar la búsqueda como búsqueda interna para proporcionar la lista de equipos a una búsqueda externa (principal) que buscará eventos para esos equipos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-372">Once you have the list, you can use the search as an inner search to feed the list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="9bc2e-373">Para ello, encierre la búsqueda interna entre llaves y proporcione sus resultados como valores posibles para un filtro o campo en la búsqueda externa mediante el operador IN.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-373">You do this by enclosing the inner search in braces and feeding its results as possible values for a filter/field in the outer search using the IN operator.</span></span> <span data-ttu-id="9bc2e-374">La consulta se parecería a:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-374">The query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![Ejemplo de búsqueda con IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="9bc2e-376">Observe también el filtro de tiempo que se usa en la búsqueda interna, porque la evaluación de la actualización del sistema toma una instantánea de todos los equipos cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-376">Also notice the time filter used in the inner search because the System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="9bc2e-377">También puede hacer la consulta interna más ligera y precisa si busca para un solo día.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-377">You can make the inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="9bc2e-378">En su lugar, la búsqueda externa usa la selección de tiempo en la interfaz de usuario y recupera eventos de los siete últimos días.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-378">The outer search instead uses the time selection in the user interface, retrieving events from the last 7 days.</span></span> <span data-ttu-id="9bc2e-379">Consulte [Operadores booleanos](#boolean-operators) para más información acerca de los operadores de tiempo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="9bc2e-380">Como realmente solo usa los resultados de la búsqueda interna como valor de filtro para la externa, todavía puede aplicar comandos en la búsqueda externa.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-380">Because you really only use the results of the inner search as a filter value for the outer one, you can still apply commands in the outer search.</span></span> <span data-ttu-id="9bc2e-381">Por ejemplo, puede agrupar los eventos anteriores con otro comando measure:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-381">For example, you can still group the above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![Ejemplo de búsqueda con IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="9bc2e-383">Por lo general, conviene que la consulta interna se ejecute rápidamente porque Log Analytics tiene tiempos de espera del servicio para ella y también para devolver una cantidad pequeña de resultados.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-383">Generally, you want your inner query to execute quickly because Log Analytics has service-side timeouts for it and also to return a small amount of results.</span></span> <span data-ttu-id="9bc2e-384">Si la consulta interna devuelve más resultados, se trunca la lista, lo que podría causar que la búsqueda externa devuelva resultados incorrectos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-384">If the inner query returns more results, the result list gets truncated, which could potentially cause the outer search to return incorrect results.</span></span>

<span data-ttu-id="9bc2e-385">Otra regla es que la búsqueda interna actualmente necesita proporcionar resultados *agregados* .</span><span class="sxs-lookup"><span data-stu-id="9bc2e-385">Another rule is that the inner search currently needs to provide *aggregated* results.</span></span> <span data-ttu-id="9bc2e-386">Es decir, debe contener un comando *measure* ; actualmente no se pueden proporcionar resultados sin procesar a una búsqueda externa.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="9bc2e-387">Además, solo puede haber un operador IN y debe ser el último filtro de la consulta.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-387">Also, there can be only one IN operator and it must be the last filter in the query.</span></span> <span data-ttu-id="9bc2e-388">No se pueden combinar varios operadores IN mediante OR; básicamente, esto impide que se ejecuten varias subbúsquedas. Lo importante es que solo es posible una subbúsqueda o búsqueda interna por cada búsqueda externa.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: the important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="9bc2e-389">Incluso con estos límites, IN permite muchos tipos de búsquedas correlacionadas y con él puede definir algo similar a los grupos, como equipos, usuarios o archivos, según los campos que contengan sus datos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-389">Even with these limits, IN enables many kinds of correlated searches, and allows you to define something similar to groups such as computers, users, or files – whatever the fields in your data contain.</span></span> <span data-ttu-id="9bc2e-390">Estos son otros ejemplos:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-390">Here are more examples:</span></span>

<span data-ttu-id="9bc2e-391">**Todas las actualizaciones que faltan en equipos donde se deshabilitó la configuración Actualización automática**</span><span class="sxs-lookup"><span data-stu-id="9bc2e-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="9bc2e-392">**Todos los eventos de error de equipos que ejecutan SQL Server (=donde se ejecutó la evaluación de SQL)**</span><span class="sxs-lookup"><span data-stu-id="9bc2e-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="9bc2e-393">**Todos los eventos de seguridad de equipos que son controladores de dominio (=donde se ejecutó la evaluación de AD)**</span><span class="sxs-lookup"><span data-stu-id="9bc2e-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="9bc2e-394">**¿Qué otras cuentas han iniciado sesión en los mismos equipos que la cuenta BACONLAND\jochan?**</span><span class="sxs-lookup"><span data-stu-id="9bc2e-394">**Which other accounts have logged on to the same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-the-distinct-command"></a><span data-ttu-id="9bc2e-395">Uso del comando distinct</span><span class="sxs-lookup"><span data-stu-id="9bc2e-395">Use the distinct command</span></span>
<span data-ttu-id="9bc2e-396">Como su nombre indica, este comando proporciona una lista de valores distintos para un campo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-396">As the name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="9bc2e-397">Es sorprendentemente sencillo pero muy útil.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="9bc2e-398">Se podría lograr lo mismo con el comando measure count(), como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-398">The same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![Ejemplo del comando de búsqueda DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="9bc2e-400">Sin embargo, si todo lo que le interesa es una simple lista de valores distintos y no el número de documentos que tengan esos valores, DISTINCT puede proporcionar una salida más limpia y fácil de leer, con una sintaxis más corta, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-400">However, if all you're interested in is just a list of distinct values and not the count of documents that have that values, then DISTINCT can provide cleaner and easier to read output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![Ejemplo del comando de búsqueda DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-the-countdistinct-function-with-the-measure-command"></a><span data-ttu-id="9bc2e-402">Uso de la función countdistinct con el comando measure</span><span class="sxs-lookup"><span data-stu-id="9bc2e-402">Use the countdistinct function with the measure command</span></span>
<span data-ttu-id="9bc2e-403">La función countdistinct cuenta el número de valores distintos dentro de cada grupo.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-403">The countdistinct function counts the number of distinct values within each group.</span></span> <span data-ttu-id="9bc2e-404">Por ejemplo, podría utilizarse para contar el número de equipos únicos que elaboran informes para cada tipo:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-404">For example, it could be used to count the number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![Countdistinct de OMS](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-the-measure-interval-command"></a><span data-ttu-id="9bc2e-406">Uso del comando measure interval</span><span class="sxs-lookup"><span data-stu-id="9bc2e-406">Use the measure interval command</span></span>
<span data-ttu-id="9bc2e-407">Con una recopilación de datos de rendimiento prácticamente en tiempo real, puede recopilar y visualizar cualquier contador de rendimiento en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="9bc2e-408">Basta con escribir la consulta **Type:Perf** para que se devuelvan miles de gráficos de métricas en función del número de contadores y los servidores en el entorno de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-408">Simply entering the query **Type:Perf** will return thousands of metric graphs based on the number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="9bc2e-409">Con la agregación de métricas a petición, puede consultar las métricas generales de alto nivel de su entorno y profundizar en los datos más granulares cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-409">With on-demand metric aggregation, you can look at the overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="9bc2e-410">Supongamos que desea saber cuál es el promedio de CPU entre todos los equipos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-410">Let’s say that you want to know what is the average CPU across all your computers.</span></span> <span data-ttu-id="9bc2e-411">Es posible que ver el promedio de CPU para cada equipo no resulte útil porque los resultados podrían uniformizarse.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-411">Looking at the average CPU for every computer might not be helpful because results may get smoothed out.</span></span> <span data-ttu-id="9bc2e-412">Para examinarlo con más detalle, puede agregar el resultado en intervalos de tiempo más reducidos y después observar una serie temporal en distintas dimensiones.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-412">To look into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="9bc2e-413">Por ejemplo, puede obtener el promedio de uso de CPU por hora en todos los equipos de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-413">For example, you can perform the hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![Medida de promedios en un intervalo](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="9bc2e-415">De forma predeterminada, estos resultados se mostrarán en un gráfico de líneas interactivo con varias series.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-415">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="9bc2e-416">Este gráfico admite alternar entre series (con el cambio de escala del eje Y), usar el zoom y mantener el mouse sobre elementos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-416">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="9bc2e-417">La opción de visualización de la tabla sigue disponible para ver los datos sin procesar si es necesario.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-417">The table display option is still available for viewing the raw data if necessary.</span></span>

<span data-ttu-id="9bc2e-418">También puede agrupar por otros campos.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-418">You can also group by other fields.</span></span> <span data-ttu-id="9bc2e-419">En este ejemplo, estoy mirando todos los contadores de porcentaje de un equipo específico y quiero saber cuál es el percentil 70 por hora de cada contador:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-419">In this example, I am looking at all the % counters for one specific computer, and I want to know what is the hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="9bc2e-420">Hay que destacar que estas consultas no se limitan a los contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-420">One thing to note is that these queries are not limited to performance counters.</span></span> <span data-ttu-id="9bc2e-421">Se pueden aplicar a cualquier métrica.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-421">You can apply them to any metric.</span></span> <span data-ttu-id="9bc2e-422">En este ejemplo, estoy consultando los registros de IIS para W3C.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-422">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="9bc2e-423">Quiero saber cuál es el tiempo máximo que se tarda en procesar cada solicitud a lo largo de un intervalo de 5 minutos:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-423">I want to know what is the maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="9bc2e-424">Uso de varios agregados en una consulta</span><span class="sxs-lookup"><span data-stu-id="9bc2e-424">Use multiple aggregates in one query</span></span>
<span data-ttu-id="9bc2e-425">Puede especificar varias cláusulas de agregado en un comando measure.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-425">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="9bc2e-426">A cada una se le puede asignar un alias de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-426">Each one can be aliased independently.</span></span>  <span data-ttu-id="9bc2e-427">Si no se le proporciona un alias, el nombre de campo resultante será la función de agregado que se usó (es decir, "avg(CounterValue)" para avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="9bc2e-427">If it is not given an alias the resulting field name will be the aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![Varios agregados en OMS 1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="9bc2e-429">Este es otro ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-429">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="9bc2e-430">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9bc2e-430">Next steps</span></span>
<span data-ttu-id="9bc2e-431">Para más información acerca de las búsquedas de registros, consulte:</span><span class="sxs-lookup"><span data-stu-id="9bc2e-431">For additional information about log searches, see:</span></span>

* <span data-ttu-id="9bc2e-432">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) (Campos personalizados en Log Analytics) para ampliar las búsquedas de registros.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-432">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) to extend log searches.</span></span>
* <span data-ttu-id="9bc2e-433">Revise la [Referencia sobre búsqueda de registros de Log Analytics](log-analytics-search-reference.md) para ver todos los campos de búsqueda y las facetas disponibles en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bc2e-433">Review the [Log Analytics log search reference](log-analytics-search-reference.md) to view all of the search fields and facets available in Log Analytics.</span></span>
