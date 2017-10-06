---
title: "datos de aaaFind con búsquedas de registros de análisis de registros de Azure | Documentos de Microsoft"
description: "Búsquedas de registros permiten toocombine y correlacionan datos de varios orígenes en el entorno del equipo."
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
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a><span data-ttu-id="f58a9-103">Descripción de las búsquedas de registros en Log Analytics</span><span class="sxs-lookup"><span data-stu-id="f58a9-103">Find data using log searches in Log Analytics</span></span>

>[!NOTE]
> <span data-ttu-id="f58a9-104">Este artículo describen las búsquedas de registros usando el lenguaje de consulta actual de hello en análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="f58a9-104">This article describes log searches using hello current query language in Log Analytics.</span></span>  <span data-ttu-id="f58a9-105">Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, debe hacer referencia demasiado[busca en el registro de descripción en análisis de registros (nuevo)](log-analytics-log-search-new.md).</span><span class="sxs-lookup"><span data-stu-id="f58a9-105">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should refer too[Understanding log searches in Log Analytics (new)](log-analytics-log-search-new.md).</span></span>


<span data-ttu-id="f58a9-106">Núcleo de Hola de análisis de registros es característica de búsqueda de registros de Hola que permite toocombine y correlacionar datos de varios orígenes en el entorno del equipo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-106">At hello core of Log Analytics is hello log search feature which allows you toocombine and correlate any machine data from multiple sources within your environment.</span></span> <span data-ttu-id="f58a9-107">Las soluciones también se basan en toobring de búsqueda de registro se métricas dinamizadas en torno a un área problemática concreta.</span><span class="sxs-lookup"><span data-stu-id="f58a9-107">Solutions are also powered by log search toobring you metrics pivoted around a particular problem area.</span></span>

<span data-ttu-id="f58a9-108">En la página de búsqueda de hello, puede crear una consulta y, a continuación, al realizar una búsqueda, puede filtrar los resultados de hello mediante el uso de controles de faceta.</span><span class="sxs-lookup"><span data-stu-id="f58a9-108">On hello Search page, you can create a query, and then when you search, you can filter hello results by using facet controls.</span></span> <span data-ttu-id="f58a9-109">También puede crear consultas avanzadas tootransform, filtrar e informar sobre sus resultados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-109">You can also create advanced queries tootransform, filter, and report on your results.</span></span>

<span data-ttu-id="f58a9-110">En la mayoría de las páginas de soluciones aparecen consultas de búsqueda comunes.</span><span class="sxs-lookup"><span data-stu-id="f58a9-110">Common log search queries appear on most solution pages.</span></span> <span data-ttu-id="f58a9-111">A lo largo de la consola de OMS de hello, puede hacer clic iconos o profundizar en los elementos de tooother tooview detalles sobre el elemento de hello mediante la búsqueda de registro.</span><span class="sxs-lookup"><span data-stu-id="f58a9-111">Throughout hello OMS console, you can click tiles or drill in tooother items tooview details about hello item by using log search.</span></span>

<span data-ttu-id="f58a9-112">En este tutorial, usaremos ejemplos toocover todos los aspectos básicos de hello cuando se utiliza la búsqueda de registros.</span><span class="sxs-lookup"><span data-stu-id="f58a9-112">In this tutorial, we'll walk through examples toocover all hello basics when you use log search.</span></span>

<span data-ttu-id="f58a9-113">Se comenzaremos con ejemplos sencillos y prácticos y luego construiremos sobre ellos para que se pueda comprender los casos de uso prácticos sobre cómo visión de toouse Hola sintaxis tooextract Hola desea partir de los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-113">We'll start with simple, practical examples and then build on them so that you can get an understanding of practical use cases about how toouse hello syntax tooextract hello insights you want from hello data.</span></span>

<span data-ttu-id="f58a9-114">Cuando se haya familiarizado con las técnicas de búsqueda, puede revisar hello [referencia de búsqueda de registro de análisis de registros](log-analytics-search-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f58a9-114">After you've familiar with search techniques, you can review hello [Log Analytics log search reference](log-analytics-search-reference.md).</span></span>

## <a name="use-basic-filters"></a><span data-ttu-id="f58a9-115">Uso de filtros básicos</span><span class="sxs-lookup"><span data-stu-id="f58a9-115">Use basic filters</span></span>
<span data-ttu-id="f58a9-116">Hello lo primero que tooknow es que Hola primera parte de una consulta de búsqueda, antes de cualquier "|" carácter de barra vertical, es siempre un *filtro*.</span><span class="sxs-lookup"><span data-stu-id="f58a9-116">hello first thing tooknow is that hello first part of a search query, before any "|" vertical pipe character, is always a *filter*.</span></span> <span data-ttu-id="f58a9-117">Se puede considerar como una cláusula WHERE de TSQL--en determina *qué* subconjunto de datos toopull fuera del almacén de datos OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-117">You can think of it as a WHERE clause in TSQL--it determines *what* subset of data toopull out of hello OMS data store.</span></span> <span data-ttu-id="f58a9-118">Buscar en el almacén de datos de hello es en gran medida sobre la especificación de las características de Hola de datos de Hola que desea tooextract, por lo que es natural que una consulta comience con hello cláusula WHERE.</span><span class="sxs-lookup"><span data-stu-id="f58a9-118">Searching in hello data store is largely about specifying hello characteristics of hello data that you want tooextract, so it is natural that a query would start with hello WHERE clause.</span></span>

<span data-ttu-id="f58a9-119">Hello filtros más básicos que puede usar son *palabras clave*, como 'error' o "tiempo de espera" o un nombre de equipo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-119">hello most basic filters you can use are *keywords*, such as ‘error’ or ‘timeout’, or a computer name.</span></span> <span data-ttu-id="f58a9-120">Estos tipos de consultas sencillas generalmente devuelven diversas formas de datos dentro de hello mismo conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-120">These types of simple queries generally return diverse shapes of data within hello same result set.</span></span> <span data-ttu-id="f58a9-121">Esto es porque el análisis de registro tiene diferentes *tipos* de datos en el sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-121">This is because Log Analytics has different *types* of data in hello system.</span></span>

### <a name="tooconduct-a-simple-search"></a><span data-ttu-id="f58a9-122">tooconduct una búsqueda simple</span><span class="sxs-lookup"><span data-stu-id="f58a9-122">tooconduct a simple search</span></span>
1. <span data-ttu-id="f58a9-123">En el portal de OMS de hello, haga clic en **búsqueda de registros**.</span><span class="sxs-lookup"><span data-stu-id="f58a9-123">In hello OMS portal, click **Log Search**.</span></span>  
    <span data-ttu-id="f58a9-124">![icono de búsqueda](./media/log-analytics-log-searches/oms-overview-log-search.png)</span><span class="sxs-lookup"><span data-stu-id="f58a9-124">![search tile](./media/log-analytics-log-searches/oms-overview-log-search.png)</span></span>
2. <span data-ttu-id="f58a9-125">En el campo de consulta de hello, escriba `error` y, a continuación, haga clic en **búsqueda**.</span><span class="sxs-lookup"><span data-stu-id="f58a9-125">In hello query field, type `error` and then click **Search**.</span></span>  
    <span data-ttu-id="f58a9-126">![error de búsqueda](./media/log-analytics-log-searches/oms-search-error.png)</span><span class="sxs-lookup"><span data-stu-id="f58a9-126">![search error](./media/log-analytics-log-searches/oms-search-error.png)</span></span>  
    <span data-ttu-id="f58a9-127">Por ejemplo, la consulta de Hola para `error` en hello siguiente imagen devolvió 100 000 **eventos** registros (recopilados por la administración de registros), 18 **ConfigurationAlert** (generados por la configuración de registros Evaluación) y 12 **ConfigurationChange** registros (capturados por seguimiento de cambios de hello).</span><span class="sxs-lookup"><span data-stu-id="f58a9-127">For example, hello query for `error` in hello following image returned 100,000 **Event** records (collected by Log Management), 18 **ConfigurationAlert** records (generated by Configuration Assessment) and 12 **ConfigurationChange** records (captured by hello Change Tracking).</span></span>   
    <span data-ttu-id="f58a9-128">![resultados de la búsqueda](./media/log-analytics-log-searches/oms-search-results01.png)</span><span class="sxs-lookup"><span data-stu-id="f58a9-128">![search results](./media/log-analytics-log-searches/oms-search-results01.png)</span></span>  

<span data-ttu-id="f58a9-129">Estos filtros no son en realidad clases o tipos de objeto.</span><span class="sxs-lookup"><span data-stu-id="f58a9-129">These filters are not really object types/classes.</span></span> <span data-ttu-id="f58a9-130">*Tipo* es una etiqueta o una propiedad o una cadena/nombre/categoría, que está adjunta tooa parte de los datos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-130">*Type* is just a tag, or a property, or a string/name/category, that is attached tooa piece of data.</span></span> <span data-ttu-id="f58a9-131">Algunos documentos Hola sistema están etiquetados como **Type: ConfigurationAlert** y algunas se etiquetan como **tipo: rendimiento**, o **Type: Event**, y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="f58a9-131">Some documents in hello system are tagged as **Type:ConfigurationAlert** and some are tagged as **Type:Perf**, or **Type:Event**, and so on.</span></span> <span data-ttu-id="f58a9-132">Cada resultado de búsqueda, documento, registro o entrada muestra todas las propiedades sin procesar de Hola y sus valores para cada una de estas partes de los datos, y se puede usar esos toospecify de nombres de campo de filtro de hello cuando desee tooretrieve sólo los registros de Hola donde hello campo tiene que da valor.</span><span class="sxs-lookup"><span data-stu-id="f58a9-132">Each search result, document, record, or entry displays all hello raw properties and their values for each of those pieces of data, and you can use those field names toospecify in hello filter when you want tooretrieve only hello records where hello field has that given value.</span></span>

<span data-ttu-id="f58a9-133">*Type* es simplemente un campo que todos los registros tienen, no es diferente de ningún otro campo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-133">*Type* is really just a field that all records have, it is not different from any other field.</span></span> <span data-ttu-id="f58a9-134">Esto se estableció en función de valor de hello del campo de tipo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-134">This was established based on hello value of hello Type field.</span></span> <span data-ttu-id="f58a9-135">Ese registro tendrá una forma diferente.</span><span class="sxs-lookup"><span data-stu-id="f58a9-135">That record will have a different shape or form.</span></span> <span data-ttu-id="f58a9-136">A propósito, **tipo = Perf**, o **tipo = Event** también son sintaxis Hola necesita toolearn tooquery de los datos de rendimiento o eventos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-136">Incidentally, **Type=Perf**, or **Type=Event** is also hello syntax that you need toolearn tooquery for performance data or events.</span></span>

<span data-ttu-id="f58a9-137">Puede usar un signo de dos puntos (:) o un signo igual (=) después de nombre de campo de Hola y antes del valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-137">You can use either a colon (:) or an equal sign (=) after hello field name and before hello value.</span></span> <span data-ttu-id="f58a9-138">**Type: Event** y **tipo = Event** son equivalentes en significado, puede elegir Hola estilo que prefiera.</span><span class="sxs-lookup"><span data-stu-id="f58a9-138">**Type:Event** and **Type=Event** are equivalent in meaning, you can choose hello style you prefer.</span></span>

<span data-ttu-id="f58a9-139">Por lo tanto, si hello escriba = Perf registros tienen un campo llamado 'CounterName', a continuación, puede escribir una consulta parecida a `Type=Perf CounterName="% Processor Time"`.</span><span class="sxs-lookup"><span data-stu-id="f58a9-139">So, if hello Type=Perf records have a field called 'CounterName', then you can write a query resembling `Type=Perf CounterName="% Processor Time"`.</span></span>

<span data-ttu-id="f58a9-140">Esto le dará solamente de los datos de rendimiento de Hola donde el nombre de contador de rendimiento de hello es "% Processor Time".</span><span class="sxs-lookup"><span data-stu-id="f58a9-140">This will give you only hello performance data where hello performance counter name is "% Processor Time".</span></span>

### <a name="toosearch-for-processor-time-performance-data"></a><span data-ttu-id="f58a9-141">toosearch para datos de rendimiento de tiempo de procesador</span><span class="sxs-lookup"><span data-stu-id="f58a9-141">toosearch for processor time performance data</span></span>
* <span data-ttu-id="f58a9-142">En el campo de consulta de búsqueda de hello, escriba`Type=Perf CounterName="% Processor Time"`</span><span class="sxs-lookup"><span data-stu-id="f58a9-142">In hello search query field, type `Type=Perf CounterName="% Processor Time"`</span></span>

<span data-ttu-id="f58a9-143">También puede ser más específico y usar **InstanceName = _ 'Total'** en consultas de hello, que es un contador de rendimiento de Windows.</span><span class="sxs-lookup"><span data-stu-id="f58a9-143">You can also be more specific and use **InstanceName=_'Total'** in hello query, which is a Windows performance counter.</span></span> <span data-ttu-id="f58a9-144">También puede seleccionar una faceta y otro **field:value**.</span><span class="sxs-lookup"><span data-stu-id="f58a9-144">You can also select a facet and another **field:value**.</span></span> <span data-ttu-id="f58a9-145">filtro de Hola se agrega automáticamente tooyour filtro en la barra de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-145">hello filter is automatically added tooyour filter in hello query bar.</span></span> <span data-ttu-id="f58a9-146">Puede ver esto en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="f58a9-146">You can see this in hello following image.</span></span> <span data-ttu-id="f58a9-147">Muestra dónde tooclick tooadd **InstanceName: '_Total'** toohello consulta sin escribir nada.</span><span class="sxs-lookup"><span data-stu-id="f58a9-147">It shows you where tooclick tooadd **InstanceName:’_Total’** toohello query without typing anything.</span></span>

![search facet](./media/log-analytics-log-searches/oms-search-facet.png)

<span data-ttu-id="f58a9-149">La consulta ahora se convierte en `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span><span class="sxs-lookup"><span data-stu-id="f58a9-149">Your query now becomes `Type=Perf CounterName="% Processor Time" InstanceName="_Total"`</span></span>

<span data-ttu-id="f58a9-150">En este ejemplo, no es necesario toospecify **tipo = Perf** tooget toothis resultado.</span><span class="sxs-lookup"><span data-stu-id="f58a9-150">In this example, you don't have toospecify **Type=Perf** tooget toothis result.</span></span> <span data-ttu-id="f58a9-151">Porque Hola campos CounterName y InstanceName solo existen para los registros de tipo = Perf, consulta hello es lo suficientemente específica como tooreturn Hola mismos resultados como Hola anterior, más larga:</span><span class="sxs-lookup"><span data-stu-id="f58a9-151">Because hello fields CounterName and InstanceName only exist for records of Type=Perf, hello query is specific enough tooreturn hello same results as hello longer, previous one:</span></span>

```
CounterName="% Processor Time" InstanceName="_Total"
```

<span data-ttu-id="f58a9-152">Esto es porque todos los filtros de hello en consulta Hola se evalúan como perteneciente a *AND* entre sí.</span><span class="sxs-lookup"><span data-stu-id="f58a9-152">This is because all hello filters in hello query are evaluated as being in *AND* with each other.</span></span> <span data-ttu-id="f58a9-153">De hecho, hello más campos agregue toohello criterios, obtendrá menos resultados más específicos y refinados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-153">Effectively, hello more fields you add toohello criteria, you get less, more specific and refined results.</span></span>

<span data-ttu-id="f58a9-154">Por ejemplo, las consultas de hello `Type=Event EventLog="Windows PowerShell"` es idéntico demasiado`Type=Event AND EventLog="Windows PowerShell"`.</span><span class="sxs-lookup"><span data-stu-id="f58a9-154">For example, hello query `Type=Event EventLog="Windows PowerShell"` is identical too`Type=Event AND EventLog="Windows PowerShell"`.</span></span> <span data-ttu-id="f58a9-155">Devuelve todos los eventos que se registraron y recopilados de registro de eventos de Windows PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-155">It returns all events that were logged in and collected from hello Windows PowerShell event log.</span></span> <span data-ttu-id="f58a9-156">Si agrega un filtro varias veces seleccionando de manera repetida Hola misma faceta, a continuación, problema de hello es meramente cosmético; podría desordenar la barra de búsqueda de hello, pero seguiría devolviendo Hola mismos resultados porque el operador AND implícito de hello siempre está ahí.</span><span class="sxs-lookup"><span data-stu-id="f58a9-156">If you add a filter multiple times by repeatedly selecting hello same facet, then hello issue is purely cosmetic--it might clutter hello Search bar, but it still returns hello same results because hello implicit AND operator is always there.</span></span>

<span data-ttu-id="f58a9-157">Puede invertir fácilmente el operador AND implícito de hello usando un operador NOT explícitamente.</span><span class="sxs-lookup"><span data-stu-id="f58a9-157">You can easily reverse hello implicit AND operator by using a NOT operator explicitly.</span></span> <span data-ttu-id="f58a9-158">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-158">For example:</span></span>

<span data-ttu-id="f58a9-159">`Type:Event NOT(EventLog:"Windows PowerShell")`o su equivalente `Type=Event EventLog!="Windows PowerShell"` devuelven todos los eventos de todos los demás registros que no son Hola registro de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f58a9-159">`Type:Event NOT(EventLog:"Windows PowerShell")` or its equivalent `Type=Event EventLog!="Windows PowerShell"` return all events from all other logs that are NOT hello Windows PowerShell log.</span></span>

<span data-ttu-id="f58a9-160">O bien, puede usar otro operador booleano como 'OR'.</span><span class="sxs-lookup"><span data-stu-id="f58a9-160">Or, you can use other Boolean operator such as ‘OR’.</span></span> <span data-ttu-id="f58a9-161">siguiente de Hello consulta devuelve los registros en los que Hola EventLog es Application OR System.</span><span class="sxs-lookup"><span data-stu-id="f58a9-161">hello following query returns records for which hello EventLog is either Application OR System.</span></span>

```
EventLog=Application OR EventLog=System
```

<span data-ttu-id="f58a9-162">Con hello por encima de la consulta, obtendrá entradas para ambos registros en hello mismo conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-162">Using hello above query, you’ll get entries for both logs in hello same result set.</span></span>

<span data-ttu-id="f58a9-163">Sin embargo, si quita hello o dejando hello AND implícito en su lugar, a continuación, hello siguiente consulta no producirá ningún resultado porque no hay una entrada de registro de eventos que pertenezca tooBOTH registros.</span><span class="sxs-lookup"><span data-stu-id="f58a9-163">However, if you remove hello OR by leaving hello implicit AND in place, then hello following query will not produce any results because there isn’t an event log entry that belongs tooBOTH logs.</span></span> <span data-ttu-id="f58a9-164">Cada entrada de registro de eventos se escribió tooonly uno de dos registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-164">Each event log entry was written tooonly one of hello two logs.</span></span>

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a><span data-ttu-id="f58a9-165">Uso de filtros adicionales</span><span class="sxs-lookup"><span data-stu-id="f58a9-165">Use additional filters</span></span>
<span data-ttu-id="f58a9-166">Hello siguiente consulta devuelve entradas de 2 registros de eventos para todos los equipos de Hola que han enviado datos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-166">hello following query returns entries for 2 event logs for all hello computers that have sent data.</span></span>

```
EventLog=Application OR EventLog=System
```

![search results](./media/log-analytics-log-searches/oms-search-results03.png)

<span data-ttu-id="f58a9-168">Al seleccionar uno de los campos de Hola o filtros se limitará Hola consulta tooa equipo específico, sin incluir todas las demás.</span><span class="sxs-lookup"><span data-stu-id="f58a9-168">Selecting one of hello fields or filters will narrow hello query tooa specific computer, excluding all other ones.</span></span> <span data-ttu-id="f58a9-169">consulta resultante Hola se parecería al siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-169">hello resulting query would resemble hello following.</span></span>

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

<span data-ttu-id="f58a9-170">Que es equivalente toohello siguientes, debido a hello and implícito.</span><span class="sxs-lookup"><span data-stu-id="f58a9-170">Which is equivalent toohello following, because of hello implicit AND.</span></span>

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="f58a9-171">Cada consulta se evalúa en hello siguiendo el orden explícito.</span><span class="sxs-lookup"><span data-stu-id="f58a9-171">Each query is evaluated in hello following explicit order.</span></span> <span data-ttu-id="f58a9-172">Paréntesis de Hola de nota.</span><span class="sxs-lookup"><span data-stu-id="f58a9-172">Note hello parenthesis.</span></span>

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

<span data-ttu-id="f58a9-173">Como campo de registro de eventos de hello, puede recuperar datos únicamente de un conjunto de equipos específicos agregando o.</span><span class="sxs-lookup"><span data-stu-id="f58a9-173">Just like hello event log field, you can retrieve data only for a set of specific computers by adding OR.</span></span> <span data-ttu-id="f58a9-174">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-174">For example:</span></span>

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

<span data-ttu-id="f58a9-175">De forma similar, esta Hola después de valor devuelto de la consulta **% de tiempo de CPU** Hola selecciona sólo los dos equipos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-175">Similarly, this hello following query return **% CPU Time** for hello selected two computers only.</span></span>

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a><span data-ttu-id="f58a9-176">Tipos de campo</span><span class="sxs-lookup"><span data-stu-id="f58a9-176">Field types</span></span>
<span data-ttu-id="f58a9-177">Al crear filtros, debe comprender las diferencias de hello en trabajar con diferentes tipos de los campos devueltos por las búsquedas de registros.</span><span class="sxs-lookup"><span data-stu-id="f58a9-177">When creating filters, you should understand hello differences in working with different types of fields returned by log searches.</span></span>

<span data-ttu-id="f58a9-178">Los **campos de búsqueda** se muestran en azul en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f58a9-178">**Searchable fields** show in blue in search results.</span></span>  <span data-ttu-id="f58a9-179">Puede usar campos de búsqueda en campo de toohello específico de condiciones de búsqueda como siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="f58a9-179">You can use searchable fields in search conditions specific toohello field such as hello following:</span></span>

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

<span data-ttu-id="f58a9-180">Los **campos de búsqueda de texto libre** se muestran en gris en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f58a9-180">**Free text searchable fields** are shown in grey in search results.</span></span>  <span data-ttu-id="f58a9-181">No se utilizaron con campo de toohello específico de condiciones de búsqueda como campos de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f58a9-181">They cannot be used with search conditions specific toohello field like searchable fields.</span></span>  <span data-ttu-id="f58a9-182">Se busca solo en al realizar una consulta en todos los campos como siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-182">They are only searched when performing a query across all fields such as hello following.</span></span>

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a><span data-ttu-id="f58a9-183">Operadores booleanos</span><span class="sxs-lookup"><span data-stu-id="f58a9-183">Boolean operators</span></span>
<span data-ttu-id="f58a9-184">Con los campos de fecha y hora, y numéricos, puede buscar valores mediante *mayor que*, *menor que* y *menor o igual que*.</span><span class="sxs-lookup"><span data-stu-id="f58a9-184">With datetime and numeric fields, you can search for values using *greater than*, *lesser than*, and *lesser than or equal*.</span></span> <span data-ttu-id="f58a9-185">Puede usar operadores simples como >, <>, =, < =,! = en la barra de búsqueda de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-185">You can use simple operators such as >, < , >=, <= , != in hello query search bar.</span></span>

<span data-ttu-id="f58a9-186">Puede consultar un registro de eventos específico para un período de tiempo específico.</span><span class="sxs-lookup"><span data-stu-id="f58a9-186">You can query a specific event log for a specific period of time.</span></span> <span data-ttu-id="f58a9-187">Por ejemplo, hello últimas 24 horas se expresa con hello siguiente expresión mnemotécnica.</span><span class="sxs-lookup"><span data-stu-id="f58a9-187">For example, hello last 24 hours is expressed with hello following mnemonic expression.</span></span>

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a><span data-ttu-id="f58a9-188">toosearch mediante un operador booleano</span><span class="sxs-lookup"><span data-stu-id="f58a9-188">toosearch using a boolean operator</span></span>
* <span data-ttu-id="f58a9-189">En el campo de consulta de búsqueda de hello, escriba`EventLog=System TimeGenerated>NOW-24HOURS`</span><span class="sxs-lookup"><span data-stu-id="f58a9-189">In hello search query field, type `EventLog=System TimeGenerated>NOW-24HOURS`</span></span>  
    <span data-ttu-id="f58a9-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span><span class="sxs-lookup"><span data-stu-id="f58a9-190">![search with boolean](./media/log-analytics-log-searches/oms-search-boolean.png)</span></span>

<span data-ttu-id="f58a9-191">Aunque puede controlar Hola intervalo de tiempo gráficamente, y casi siempre es recomendable toodo que, hay ventajas tooincluding un filtro de tiempo directamente en la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-191">Although you can control hello time interval graphically, and most times you might want toodo that, there are advantages tooincluding a time filter directly into hello query.</span></span> <span data-ttu-id="f58a9-192">Por ejemplo, esto funciona bien con paneles donde puede reemplazar tiempo Hola de cada icono, con independencia de hello *global* selector de tiempo en la página del panel Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-192">For example, this works great with dashboards where you can override hello time for each tile, regardless of hello *global* time selector on hello dashboard page.</span></span> <span data-ttu-id="f58a9-193">Para obtener más información, consulte [Cuestiones sobre el tiempo en el panel](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span><span class="sxs-lookup"><span data-stu-id="f58a9-193">For more information, see [Time Matters in Dashboard](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).</span></span>

<span data-ttu-id="f58a9-194">Si desea filtrar por tiempo, tenga en cuenta que se obtienen resultados para hello *intersección* de hello dos períodos de tiempo: Hola especificada en el portal de OMS (S1) de Hola y Hola especificada en la consulta de hello (S2).</span><span class="sxs-lookup"><span data-stu-id="f58a9-194">When filtering by time, keep in mind that you get results for hello *intersection* of hello two time periods: hello one specified in hello OMS portal (S1) and hello one specified in hello query (S2).</span></span>

![intersección](./media/log-analytics-log-searches/oms-search-intersection.png)

<span data-ttu-id="f58a9-196">Esto significa que, si hello períodos de tiempo no forman una intersección, por ejemplo en el portal de OMS Hola donde elegir **esta semana** y en la consulta de hello define **última semana**, a continuación, no hay ninguna intersección y no recibirá ningún resultado.</span><span class="sxs-lookup"><span data-stu-id="f58a9-196">This means, if hello time periods don’t intersect, for example in hello OMS portal where you choose **This week** and in hello query where you define **last week**, then there is no intersection and you won't receive any results.</span></span>

<span data-ttu-id="f58a9-197">Operadores de comparación usados con campo de hello TimeGenerated también son útiles en otras situaciones.</span><span class="sxs-lookup"><span data-stu-id="f58a9-197">Comparison operators used for hello TimeGenerated field are also useful in other situations.</span></span> <span data-ttu-id="f58a9-198">Por ejemplo, con los campos numéricos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-198">For example, with numeric fields.</span></span>

<span data-ttu-id="f58a9-199">Por ejemplo, dado que las alertas de evaluación de configuración tienen Hola después de los valores de gravedad:</span><span class="sxs-lookup"><span data-stu-id="f58a9-199">For example, given that Configuration Assessment’s alerts have hello following severity values:</span></span>

* <span data-ttu-id="f58a9-200">0 = Información</span><span class="sxs-lookup"><span data-stu-id="f58a9-200">0 = Information</span></span>
* <span data-ttu-id="f58a9-201">1= Advertencia</span><span class="sxs-lookup"><span data-stu-id="f58a9-201">1 = Warning</span></span>
* <span data-ttu-id="f58a9-202">2 = Crítico</span><span class="sxs-lookup"><span data-stu-id="f58a9-202">2 = Critical</span></span>

<span data-ttu-id="f58a9-203">Puede consultar alertas de advertencia y críticas y también excluir las informativas con hello después de consulta:</span><span class="sxs-lookup"><span data-stu-id="f58a9-203">You can query for both warning and critical alerts and also exclude informational ones with hello following query:</span></span>

```
Type=ConfigurationAlert  Severity>=1
```


<span data-ttu-id="f58a9-204">También puede usar consultas por rango.</span><span class="sxs-lookup"><span data-stu-id="f58a9-204">You can also use range queries.</span></span> <span data-ttu-id="f58a9-205">Esto significa que puede proporcionar el intervalo de saludo inicial y final de los valores de una secuencia.</span><span class="sxs-lookup"><span data-stu-id="f58a9-205">This means that you can provide hello beginning and end range of values in a sequence.</span></span> <span data-ttu-id="f58a9-206">Por ejemplo, si desea eventos del registro de eventos de Operations Manager de Hola donde hello EventID es igual o mayor que too2100 pero no superior a 2199, a continuación, Hola después consulta devolvería estos valores.</span><span class="sxs-lookup"><span data-stu-id="f58a9-206">For example, if you want events from hello Operations Manager event log where hello EventID is greater than or equal too2100 but not greater than 2199, then hello following query would return them.</span></span>

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> <span data-ttu-id="f58a9-207">sintaxis de intervalo de Hola que debe usar es el separador de hello dos puntos (:) field: value y *no* Hola signo de igual (=).</span><span class="sxs-lookup"><span data-stu-id="f58a9-207">hello range syntax you must use is hello colon (:) field:value separator and *not* hello equal sign (=).</span></span> <span data-ttu-id="f58a9-208">Incluya el extremo de hello inferior y superior del intervalo de hello corchetes y sepárelos con dos puntos (..).</span><span class="sxs-lookup"><span data-stu-id="f58a9-208">Enclose hello lower and upper end of hello range in square brackets and separate them with two periods (..).</span></span>
>
>

## <a name="manipulate-search-results"></a><span data-ttu-id="f58a9-209">Manipulación de los resultados de búsqueda</span><span class="sxs-lookup"><span data-stu-id="f58a9-209">Manipulate search results</span></span>
<span data-ttu-id="f58a9-210">Cuando está buscando datos, podrá desea toorefine la consulta de búsqueda y tener un buen nivel de control sobre los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-210">When you're searching for data, you'll want toorefine your search query and have a good level of control over hello results.</span></span> <span data-ttu-id="f58a9-211">Cuando se recuperan los resultados, puede aplicar comandos tootransform ellos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-211">When results are retrieved, you can apply commands tootransform them.</span></span>

<span data-ttu-id="f58a9-212">Comandos en las búsquedas de análisis de registros *debe* seguir Hola carácter de barra vertical (|).</span><span class="sxs-lookup"><span data-stu-id="f58a9-212">Commands in Log Analytics searches *must* follow after hello vertical pipe character (|).</span></span> <span data-ttu-id="f58a9-213">Un filtro siempre debe ser la primera parte de una cadena de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-213">A filter must always be hello first part of a query string.</span></span> <span data-ttu-id="f58a9-214">Define el conjunto de datos de hello con que trabaja y luego "canaliza" esos resultados en un comando.</span><span class="sxs-lookup"><span data-stu-id="f58a9-214">It defines hello data set you're working with and then "pipes" those results into a command.</span></span> <span data-ttu-id="f58a9-215">A continuación, puede usar comandos adicionales de hello canalización tooadd.</span><span class="sxs-lookup"><span data-stu-id="f58a9-215">You can then use hello pipe tooadd additional commands.</span></span> <span data-ttu-id="f58a9-216">Esto es parecido a grandes rasgos canalización de Windows PowerShell toohello.</span><span class="sxs-lookup"><span data-stu-id="f58a9-216">This is loosely similar toohello Windows PowerShell pipeline.</span></span>

<span data-ttu-id="f58a9-217">En general, Hola lenguaje de búsqueda de análisis de registros intente toomake de estilo y los criterios de PowerShell toofollow toohello similar de TI TI los profesionales de TI y tooease Hola una curva de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="f58a9-217">In general, hello Log Analytics search language tries toofollow PowerShell style and guidelines toomake it similar toohello IT pros, and tooease hello learning curve.</span></span>

<span data-ttu-id="f58a9-218">Los comandos tienen nombres de verbos para que pueda saber fácilmente lo que hacen.</span><span class="sxs-lookup"><span data-stu-id="f58a9-218">Commands have names of verbs so you can easily tell what they do.</span></span>  

### <a name="sort"></a><span data-ttu-id="f58a9-219">Sort</span><span class="sxs-lookup"><span data-stu-id="f58a9-219">Sort</span></span>
<span data-ttu-id="f58a9-220">comando de ordenación de Hello permite hello toodefine ordenación por uno o varios campos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-220">hello sort command allows you toodefine hello sorting order by one or multiple fields.</span></span> <span data-ttu-id="f58a9-221">Aunque no lo use, se aplica de forma predeterminada un tiempo en orden descendente.</span><span class="sxs-lookup"><span data-stu-id="f58a9-221">Even if you don’t use it, by default, a time descending order is enforced.</span></span> <span data-ttu-id="f58a9-222">los resultados más recientes de Hello siempre están en parte superior de Hola de resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f58a9-222">hello most recent results are always at hello top of search results.</span></span> <span data-ttu-id="f58a9-223">Esto significa que cuando ejecuta una búsqueda con `Type=Event EventID=1234` , lo que realmente se ejecuta es:</span><span class="sxs-lookup"><span data-stu-id="f58a9-223">This means that when you run a search, with `Type=Event EventID=1234` what really is executed for you is:</span></span>

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

<span data-ttu-id="f58a9-224">Eso es porque es de tipo hello de experiencia con el que está familiarizado en los registros.</span><span class="sxs-lookup"><span data-stu-id="f58a9-224">That's because it is hello type of experience you are familiar with in logs.</span></span> <span data-ttu-id="f58a9-225">Por ejemplo, en el Visor de eventos de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f58a9-225">For example, in hello Windows Event Viewer.</span></span>

<span data-ttu-id="f58a9-226">Puede usar a ordenación toochange Hola forma resultados se devuelven.</span><span class="sxs-lookup"><span data-stu-id="f58a9-226">You can use Sort toochange hello way results are returned.</span></span> <span data-ttu-id="f58a9-227">Hello en los ejemplos siguientes muestran cómo funciona.</span><span class="sxs-lookup"><span data-stu-id="f58a9-227">hello following examples show how this works.</span></span>

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


<span data-ttu-id="f58a9-228">Hello sencillos ejemplos anteriores muestran cómo funcionan los comandos; estos cambian forma Hola de resultados de Hola Hola filtro devuelve.</span><span class="sxs-lookup"><span data-stu-id="f58a9-228">hello simple examples above show you how commands work--they change hello shape of hello results that hello filter returned.</span></span>

### <a name="limit-and-top"></a><span data-ttu-id="f58a9-229">Limit y Top</span><span class="sxs-lookup"><span data-stu-id="f58a9-229">Limit and top</span></span>
<span data-ttu-id="f58a9-230">Otro comando menos conocido es LIMIT.</span><span class="sxs-lookup"><span data-stu-id="f58a9-230">Another less known command is LIMIT.</span></span> <span data-ttu-id="f58a9-231">Limit es un verbo al estilo de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f58a9-231">Limit is a PowerShell-like verb.</span></span> <span data-ttu-id="f58a9-232">Límite es de comando TOP toohello funcionalmente idénticas.</span><span class="sxs-lookup"><span data-stu-id="f58a9-232">Limit is functionally identical toohello TOP command.</span></span> <span data-ttu-id="f58a9-233">Hello consultas siguientes devuelven Hola mismos resultados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-233">hello following queries return hello same results.</span></span>

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a><span data-ttu-id="f58a9-234">toosearch con top</span><span class="sxs-lookup"><span data-stu-id="f58a9-234">toosearch using top</span></span>
* <span data-ttu-id="f58a9-235">En el campo de consulta de búsqueda de hello, escriba`Type=Event EventID=600 | Top 1` </span><span class="sxs-lookup"><span data-stu-id="f58a9-235">In hello search query field, type `Type=Event EventID=600 | Top 1` </span></span>  
    <span data-ttu-id="f58a9-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span><span class="sxs-lookup"><span data-stu-id="f58a9-236">![search top](./media/log-analytics-log-searches/oms-search-top.png)</span></span>

<span data-ttu-id="f58a9-237">En la imagen de hello anterior, hay miles de 358 registros con EventID = 600.</span><span class="sxs-lookup"><span data-stu-id="f58a9-237">In hello image above, there are 358 thousand records with EventID=600.</span></span> <span data-ttu-id="f58a9-238">Hola campos, las facetas y filtros en hello siempre dejado de mostrar información sobre los resultados de hello devueltos *por parte de filtro de hello* de consulta de hello, que forma parte de hello delante de cualquier carácter de canalización.</span><span class="sxs-lookup"><span data-stu-id="f58a9-238">hello fields, facets, and filters on hello left always show information about hello results returned *by hello filter portion* of hello query, which is hello part before any pipe character.</span></span> <span data-ttu-id="f58a9-239">Hola **resultados** panel solo devuelve el resultado de hello 1 más reciente, porque comando de ejemplo de Hola en forma y transforma los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-239">hello **Results** pane only returns hello most recent 1 result, because hello example command shaped and transformed hello results.</span></span>

### <a name="select"></a><span data-ttu-id="f58a9-240">Seleccionar</span><span class="sxs-lookup"><span data-stu-id="f58a9-240">Select</span></span>
<span data-ttu-id="f58a9-241">comando SELECT Hola se comporta como Select-Object en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f58a9-241">hello SELECT command behaves like Select-Object in PowerShell.</span></span> <span data-ttu-id="f58a9-242">Devuelve los resultados filtrados que no tienen todas sus propiedades originales.</span><span class="sxs-lookup"><span data-stu-id="f58a9-242">It returns filtered results that do not have all of their original properties.</span></span> <span data-ttu-id="f58a9-243">En su lugar, selecciona sólo las propiedades de Hola que especifique.</span><span class="sxs-lookup"><span data-stu-id="f58a9-243">Instead, it selects only hello properties that you specify.</span></span>

#### <a name="toorun-a-search-using-hello-select-command"></a><span data-ttu-id="f58a9-244">toorun una búsqueda con el comando select Hola</span><span class="sxs-lookup"><span data-stu-id="f58a9-244">toorun a search using hello select command</span></span>
1. <span data-ttu-id="f58a9-245">En el campo de búsqueda, escriba `Type=Event` y luego haga clic en **Buscar**.</span><span class="sxs-lookup"><span data-stu-id="f58a9-245">In Search, type `Type=Event` and then click **Search**.</span></span>
2. <span data-ttu-id="f58a9-246">Haga clic en **+ mostrar más** en uno de hello resultados tooview tienen todas las propiedades de Hola Hola resultados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-246">Click **+ show more** in one of hello results tooview all hello properties that hello results have.</span></span>
3. <span data-ttu-id="f58a9-247">Seleccione algunas de ellas explícitamente y hello cambios de consulta demasiado`Type=Event | Select Computer,EventID,RenderedDescription`.</span><span class="sxs-lookup"><span data-stu-id="f58a9-247">Select some of those explicitly, and hello query changes too`Type=Event | Select Computer,EventID,RenderedDescription`.</span></span>  
    <span data-ttu-id="f58a9-248">![Búsqueda con Select](./media/log-analytics-log-searches/oms-search-select.png)</span><span class="sxs-lookup"><span data-stu-id="f58a9-248">![search select](./media/log-analytics-log-searches/oms-search-select.png)</span></span>

<span data-ttu-id="f58a9-249">Este comando es especialmente útil cuando desea que los resultados de búsqueda de toocontrol y elegir solo un Hola partes de datos que realmente importan para la exploración, que a menudo no registro completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-249">This command is particularly useful when you want toocontrol search output and choose only hello portions of data that really matter for your exploration, which often isn’t hello full record.</span></span> <span data-ttu-id="f58a9-250">También es útil cuando registros de diferentes tipos tienen *algunas* propiedades en común, pero no *todas*.</span><span class="sxs-lookup"><span data-stu-id="f58a9-250">This is also useful when records of different types have *some* common properties, but not *all* of their properties are common.</span></span> <span data-ttu-id="f58a9-251">Puede generar resultados con apariencia natural de una tabla o funcionan bien cuando se exportó el archivo CSV de tooa y, a continuación, se transforman en Excel.</span><span class="sxs-lookup"><span data-stu-id="f58a9-251">The, you can generate output that looks more naturally like a table, or work well when exported tooa CSV file and then massaged in Excel.</span></span>

## <a name="use-hello-measure-command"></a><span data-ttu-id="f58a9-252">Use el comando measure de Hola</span><span class="sxs-lookup"><span data-stu-id="f58a9-252">Use hello measure command</span></span>
<span data-ttu-id="f58a9-253">MEASURE es uno de los comandos más versátiles de hello en las búsquedas de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="f58a9-253">MEASURE is one of hello most versatile commands in Log Analytics searches.</span></span> <span data-ttu-id="f58a9-254">Le permite tooapply estadística *funciones* tooyour datos y agregar los resultados agrupados por un campo determinado.</span><span class="sxs-lookup"><span data-stu-id="f58a9-254">It allows you tooapply statistical *functions* tooyour data and aggregate results grouped by a given field.</span></span> <span data-ttu-id="f58a9-255">Son muchas las funciones estadísticas que admite este comando.</span><span class="sxs-lookup"><span data-stu-id="f58a9-255">There are multiple statistical functions that Measure supports.</span></span>

### <a name="measure-count"></a><span data-ttu-id="f58a9-256">Measure count()</span><span class="sxs-lookup"><span data-stu-id="f58a9-256">Measure count()</span></span>
<span data-ttu-id="f58a9-257">Hola toowork primera función estadística con y el otro toounderstand más sencilla de Hola Hola *count()* función.</span><span class="sxs-lookup"><span data-stu-id="f58a9-257">hello first statistical function toowork with, and one of hello simplest toounderstand is hello *count()* function.</span></span>

<span data-ttu-id="f58a9-258">Resultados de cualquier consulta de búsqueda como `Type=Event`, muestran filtros también llamados facetas en hello parte izquierda de los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f58a9-258">Results from any search query such as `Type=Event`, show filters also called facets on hello left side of search results.</span></span> <span data-ttu-id="f58a9-259">filtros de Hello muestran una distribución de valores por un campo dado de resultados de hello en búsqueda de hello realizada.</span><span class="sxs-lookup"><span data-stu-id="f58a9-259">hello filters show a distribution of values by a given field for hello results in hello search executed.</span></span>

![search measure count](./media/log-analytics-log-searches/oms-search-measure-count01.png)

<span data-ttu-id="f58a9-261">Por ejemplo, en hello imagen anterior se verá hello **equipo** campo y se muestra que dentro de los eventos de casi 739 miles de hello en los resultados de hello, hay 68 valores únicos y distintos para hello **equipo** campo de esos registros.</span><span class="sxs-lookup"><span data-stu-id="f58a9-261">For example, in hello image above you'll see hello **Computer** field and it shows that within hello almost 739 thousand events in hello results, there are 68 unique and distinct values for hello **Computer** field in those records.</span></span> <span data-ttu-id="f58a9-262">icono de Hello solo muestra hello 5 principales, que son Hola 5 valores más comunes que se escriben en hello **equipo** campos), ordenados por número de Hola de documentos que contienen ese valor específico en ese campo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-262">hello tile only shows hello top 5, which are hello most common 5 values that are written in hello **Computer** fields), sorted by hello number of documents that contain that specific value in that field.</span></span> <span data-ttu-id="f58a9-263">En la imagen de hello puede ver que, entre esos casi 369 miles de eventos, 90 mil proceden hello OpsInsights04.contoso.com equipo, 83 mil del equipo de hello DB03.contoso.com y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="f58a9-263">In hello image you can see that – among those almost 369 thousand events – 90 thousand come from hello OpsInsights04.contoso.com computer, 83 thousand from hello DB03.contoso.com computer, and so on.</span></span>

<span data-ttu-id="f58a9-264">¿Qué ocurre si desea que toosee todos los valores, ya que el icono de Hola solo muestra hello solo top 5?</span><span class="sxs-lookup"><span data-stu-id="f58a9-264">What if you want toosee all values, since hello tile only shows only hello top 5?</span></span>

<span data-ttu-id="f58a9-265">Que es qué medida Hola comando puede hacer con la función count() de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-265">That’s what hello measure command can do with hello count() function.</span></span> <span data-ttu-id="f58a9-266">Esta función no usa ningún parámetro.</span><span class="sxs-lookup"><span data-stu-id="f58a9-266">This function doesn't use any parameters.</span></span> <span data-ttu-id="f58a9-267">Solo debe especificar campo hello mediante el cual desea toogroup: Hola **equipo** en este caso:</span><span class="sxs-lookup"><span data-stu-id="f58a9-267">You just specify hello field by which you want toogroup by – hello **Computer** field in this case:</span></span>

`Type=Event | Measure count() by Computer`

![search measure count](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

<span data-ttu-id="f58a9-269">Sin embargo, **Computer** es simplemente un campo usado *en* cada dato; no hay ninguna base de datos relacional implicada y no hay ningún objeto **Computer** independiente en ninguna parte.</span><span class="sxs-lookup"><span data-stu-id="f58a9-269">However, **Computer** is just a field used *in* each piece of data – there are no relational databases involved and there is no separate **Computer** object anywhere.</span></span> <span data-ttu-id="f58a9-270">Hola simplemente valores *en* Hola datos pueden describir la entidad que ha generado y otras características y aspectos de los datos de hello; por lo tanto, Hola término *faceta*.</span><span class="sxs-lookup"><span data-stu-id="f58a9-270">Just hello values *in* hello data can describe which entity generated them, and a number of other characteristics and aspects of hello data – hence hello term *facet*.</span></span> <span data-ttu-id="f58a9-271">Sin embargo, también puede agrupar por otros campos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-271">However, you can just as well group by other fields.</span></span> <span data-ttu-id="f58a9-272">Dado que resultados originales de hello casi 739 miles de eventos de que se canalizan Hola medida comando también tienen un campo denominado **EventID**, puede aplicar Hola mismo toogroup técnica por ese campo y obtener un recuento de eventos por EventID:</span><span class="sxs-lookup"><span data-stu-id="f58a9-272">Because hello original results of almost 739 thousand events that are piped into hello measure command also have a field called **EventID**, you can apply hello same technique toogroup by that field and get a count of events by EventID:</span></span>

```
Type=Event | Measure count() by EventID
```

<span data-ttu-id="f58a9-273">Si no está interesado en número de registros real de Hola que contienen un valor específico, pero en su lugar, si desea obtener una lista de hello valores por sí mismos, puede agregar un *seleccione* comando final hello y primera columna de hello simplemente seleccione:</span><span class="sxs-lookup"><span data-stu-id="f58a9-273">If you're not interested in hello actual record count that contain a specific value, but instead if you only want a list of hello values themselves, you can add a *Select* command at hello end of it and just select hello first column:</span></span>

```
Type=Event | Measure count() by EventID | Select EventID
```

<span data-ttu-id="f58a9-274">A continuación, puede obtener más intrincados y previamente ordenar resultados de hello en consultas de Hola o puede hacer clic columnas hello en cuadrícula de hello, demasiado.</span><span class="sxs-lookup"><span data-stu-id="f58a9-274">Then you can get more intricate and pre-sort hello results in hello query, or you can just click hello columns in hello grid, too.</span></span>

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a><span data-ttu-id="f58a9-275">toosearch mediante measure count</span><span class="sxs-lookup"><span data-stu-id="f58a9-275">toosearch using measure count</span></span>
* <span data-ttu-id="f58a9-276">En el campo de consulta de búsqueda de hello, escriba`Type=Event | Measure count() by EventID`</span><span class="sxs-lookup"><span data-stu-id="f58a9-276">In hello search query field, type `Type=Event | Measure count() by EventID`</span></span>
* <span data-ttu-id="f58a9-277">Anexar `| Select EventID` toohello final de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-277">Append `| Select EventID` toohello end of hello query.</span></span>
* <span data-ttu-id="f58a9-278">Por último, anexe `| Sort EventID asc` toohello final de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-278">Finally, append `| Sort EventID asc` toohello end of hello query.</span></span>

<span data-ttu-id="f58a9-279">Hay un par de cuestiones importantes de toonotice y resaltar:</span><span class="sxs-lookup"><span data-stu-id="f58a9-279">There are a couple important points toonotice and emphasize:</span></span>

<span data-ttu-id="f58a9-280">En primer lugar, los resultados de Hola que ve ya no son Hola original sin procesar resultados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-280">First, hello results you see are not hello original raw results anymore.</span></span> <span data-ttu-id="f58a9-281">Son los resultados de agregado, básicamente grupos de resultados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-281">Instead, they are aggregated results – essentially groups of results.</span></span> <span data-ttu-id="f58a9-282">Esto no supone un problema, pero debe comprender que está interactuando con una forma muy diferente de datos que difieren de forma sin formato original Hola que se crea sobre la marcha hello como resultado de la función estadística o de agregación de hello.</span><span class="sxs-lookup"><span data-stu-id="f58a9-282">This isn't a problem, but you should understand that you're interacting with a very different shape of data that differs from hello original raw shape that gets created on hello fly as a result of hello aggregation/statistical function.</span></span>

<span data-ttu-id="f58a9-283">Segundo, **medir recuento** actualmente devuelve solo Hola top 100 primeros resultados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-283">Second, **Measure count** currently returns only hello top 100 distinct results.</span></span> <span data-ttu-id="f58a9-284">Este límite no aplica toohello otras funciones estadísticas.</span><span class="sxs-lookup"><span data-stu-id="f58a9-284">This limit does not apply toohello other statistical functions.</span></span> <span data-ttu-id="f58a9-285">Por lo tanto, normalmente deberá toouse un toosearch de primer filtro más preciso para elementos específicos antes de aplicar measure count().</span><span class="sxs-lookup"><span data-stu-id="f58a9-285">So, you'll usually need toouse a more precise filter first toosearch for specific items before you apply measure count().</span></span>

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a><span data-ttu-id="f58a9-286">Usar funciones max y min de Hola con comandos de medida de Hola</span><span class="sxs-lookup"><span data-stu-id="f58a9-286">Use hello max and min functions with hello measure command</span></span>
<span data-ttu-id="f58a9-287">Son varias las situaciones en las que **Measure Max()** y **Measure Min()** son útiles.</span><span class="sxs-lookup"><span data-stu-id="f58a9-287">There are various scenarios where **Measure Max()** and **Measure Min()** are useful.</span></span> <span data-ttu-id="f58a9-288">Sin embargo, puesto que cada función es opuesta entre sí, ilustraremos Max() y usted puede experimentar con Min() por su cuenta.</span><span class="sxs-lookup"><span data-stu-id="f58a9-288">However, since each function is opposite of each other, we'll illustrate Max() and you can experiment with Min() on your own.</span></span>

<span data-ttu-id="f58a9-289">Si busca eventos de seguridad, tienen una propiedad **Level** que puede variar.</span><span class="sxs-lookup"><span data-stu-id="f58a9-289">If you query for security events, they have a **Level** property that can vary.</span></span> <span data-ttu-id="f58a9-290">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-290">For example:</span></span>

```
Type=SecurityEvent
```

![search measure count start](./media/log-analytics-log-searches/oms-search-measure-max01.png)

<span data-ttu-id="f58a9-292">Si desea que tooview Hola mayor valor de seguridad de hello todos eventos dados un equipo común, Hola campo Agrupar por, puede usar</span><span class="sxs-lookup"><span data-stu-id="f58a9-292">If you want tooview hello highest value for all of hello security events given a common Computer, hello group by field, you can use</span></span>

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![search measure max computer](./media/log-analytics-log-searches/oms-search-measure-max02.png)

<span data-ttu-id="f58a9-294">Se mostrará que para los equipos de Hola que tenían **nivel** registros, la mayoría de ellos tiene al menos 8, el nivel muchas tenían un nivel de 16.</span><span class="sxs-lookup"><span data-stu-id="f58a9-294">It will display that for hello computers that had **Level** records, most of them have at least level 8, many had a level of 16.</span></span>

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![search measure max time generated computer](./media/log-analytics-log-searches/oms-search-measure-max03.png)

<span data-ttu-id="f58a9-296">Esta función es muy adecuada para números, pero también para campos de fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="f58a9-296">This function works well with numbers, but it also works with DateTime fields.</span></span> <span data-ttu-id="f58a9-297">Resulta útil toocheck para hello última o marca de hora más reciente de cualquier parte de los datos indexados para cada equipo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-297">It is useful toocheck for hello last or most recent time stamp for any piece of data indexed for each computer.</span></span> <span data-ttu-id="f58a9-298">¿Por ejemplo: cuándo se notifican los eventos de seguridad más reciente de Hola para cada máquina?</span><span class="sxs-lookup"><span data-stu-id="f58a9-298">For example: When was hello most recent security event reported for each machine?</span></span>

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="f58a9-299">Usar avg, función hello con comandos de medida de Hola</span><span class="sxs-lookup"><span data-stu-id="f58a9-299">Use hello avg function with hello measure command</span></span>
<span data-ttu-id="f58a9-300">Hola función estadística Avg() usada con measure le permite el valor medio de hello toocalculate de algún campo y los resultados de grupo por hello mismo u otro campo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-300">hello Avg() statistical function used with measure allows you toocalculate hello average value for some field, and group results by hello same or other field.</span></span> <span data-ttu-id="f58a9-301">Esto resulta útil en muchos casos, por ejemplo, con los datos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="f58a9-301">This is useful in a variety of cases, such as performance data.</span></span>

<span data-ttu-id="f58a9-302">Comenzaremos con los datos de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="f58a9-302">We'll start with performance data.</span></span> <span data-ttu-id="f58a9-303">Tenga en cuenta que OMS actualmente recopila contadores de rendimiento tanto para equipos Windows como Linux.</span><span class="sxs-lookup"><span data-stu-id="f58a9-303">Note that OMS currently collects performance counters for both Windows and Linux machines.</span></span>

<span data-ttu-id="f58a9-304">toosearch para *todos los* datos de rendimiento, consulta más básica de hello es:</span><span class="sxs-lookup"><span data-stu-id="f58a9-304">toosearch for *all* performance data, hello most basic query is:</span></span>

```
Type=Perf
```

![search avg start](./media/log-analytics-log-searches/oms-search-avg01.png)

<span data-ttu-id="f58a9-306">Hola primero que notará es que el análisis de registros muestra tres perspectivas: lista, que se muestra en los que se muestran los registros reales de hello detrás de los gráficos de hello; Tabla, que muestra una vista tabular de datos del contador de rendimiento; y las métricas, que se muestran los contadores de rendimiento de gráficos para saludo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-306">hello first thing you'll notice is that Log Analytics shows you three perspectives: List, which shows you which shows hello actual records behind hello charts; Table, which shows a tabular view of performance counter data; and Metrics, which shows charts for hello performance counters.</span></span>

<span data-ttu-id="f58a9-307">En la imagen de hello anterior, hay dos conjuntos de campos marcados que indican Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="f58a9-307">In hello image above, there are two sets of fields marked that indicate hello following:</span></span>

* <span data-ttu-id="f58a9-308">Hola primer conjunto identifica el nombre de contador de rendimiento de Windows, el nombre del objeto y el nombre de instancia en el filtro de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-308">hello first set identifies Windows Performance Counter Name, Object Name, and Instance Name in hello query filter.</span></span> <span data-ttu-id="f58a9-309">Estos son los campos de Hola que probablemente usará normalmente como facetas o filtros:</span><span class="sxs-lookup"><span data-stu-id="f58a9-309">These are hello fields you probably will most commonly use as facets/filters</span></span>
* <span data-ttu-id="f58a9-310">**CounterValue** es Hola valor real del contador de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-310">**CounterValue** is hello actual value of hello counter.</span></span> <span data-ttu-id="f58a9-311">En este ejemplo, es el valor de hello *75*.</span><span class="sxs-lookup"><span data-stu-id="f58a9-311">In this example, hello value is *75*.</span></span>
* <span data-ttu-id="f58a9-312">**TimeGenerated** es 12:51, en formato de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="f58a9-312">**TimeGenerated** is 12:51, in 24-hour time format.</span></span>

<span data-ttu-id="f58a9-313">Ésta es una vista de las métricas de hello en un gráfico.</span><span class="sxs-lookup"><span data-stu-id="f58a9-313">Here's a view of hello metrics in a graph.</span></span>

![search avg start](./media/log-analytics-log-searches/oms-search-avg02.png)

<span data-ttu-id="f58a9-315">Después de leer sobre la forma de registro de rendimiento de Hola y de haber leído sobre otras técnicas de búsqueda, puede usar medida Avg() tooaggregate este tipo de datos numéricos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-315">After reading about hello Perf record shape, and having read about other search techniques, you can use measure Avg() tooaggregate this type of numerical data.</span></span>

<span data-ttu-id="f58a9-316">A continuación se muestra un sencillo ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-316">Here's a simple example:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![search avg samplevalue](./media/log-analytics-log-searches/oms-search-avg03.png)

<span data-ttu-id="f58a9-318">En este ejemplo, seleccionar contador de rendimiento de tiempo Total de CPU de Hola y el promedio por equipo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-318">In this example, you select hello CPU Total Time performance counter and average by Computer.</span></span> <span data-ttu-id="f58a9-319">Si desea toonarrow hacia abajo el saludo de tooonly resultados últimos 6 horas, puede usar el control de filtro de tiempo de Hola o especifique en la consulta del siguiente modo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-319">If you want toonarrow down your results tooonly hello last 6 hours, you can either use hello time filter control or specify in your query as follows:</span></span>

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a><span data-ttu-id="f58a9-320">toosearch con avg, función hello comando measure de Hola</span><span class="sxs-lookup"><span data-stu-id="f58a9-320">toosearch using hello avg function with hello measure command</span></span>
* <span data-ttu-id="f58a9-321">En el cuadro de consulta de búsqueda de hello, escriba `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span><span class="sxs-lookup"><span data-stu-id="f58a9-321">In hello Search query box, type `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.</span></span>

<span data-ttu-id="f58a9-322">Puede agregar y correlacionar los datos *entre* equipos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-322">You can aggregate and correlate data *across* computers.</span></span> <span data-ttu-id="f58a9-323">Por ejemplo, imagine que tiene un conjunto de hosts en algún tipo de granja de servidores donde cada nodo es igual tooany otro y solo lo hacen Hola todos los mismo tipo de trabajo y la carga se debe equilibrar de manera aproximada.</span><span class="sxs-lookup"><span data-stu-id="f58a9-323">For example, imagine that you have a set of hosts in some sort of farm where each node is equal tooany other one and they just do all hello same type of work and load should be roughly balanced.</span></span> <span data-ttu-id="f58a9-324">Podría obtener sus contadores en un solo paso con hello siguiente consulta y conseguir los promedios para toda granja de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-324">You could get their counters all in one go with hello following query and get averages for hello entire farm.</span></span> <span data-ttu-id="f58a9-325">Puede comenzar eligiendo los equipos de hello con hello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-325">You can start by choosing hello computers with hello following example:</span></span>

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="f58a9-326">Ahora que tiene equipos de hello, también desea tooselect dos indicadores de rendimiento clave (KPI): % de uso de CPU y % espacio libre en disco.</span><span class="sxs-lookup"><span data-stu-id="f58a9-326">Now that you have hello computers, you also only want tooselect two key performance indicators (KPIs): % CPU Usage and % Free Disk Space.</span></span> <span data-ttu-id="f58a9-327">Por lo tanto, se convierte en parte de la consulta de hello:</span><span class="sxs-lookup"><span data-stu-id="f58a9-327">So, that part of hello query becomes:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

<span data-ttu-id="f58a9-328">Ahora puede agregar equipos y contadores con el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="f58a9-328">Now you can add computers and counters with hello following example:</span></span>

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

<span data-ttu-id="f58a9-329">Hola porque tiene una selección muy específica, **medir Avg()** comando puede devolver Hola Media no por equipo, sino en la granja de servidores de hello, simplemente Agrupar por CounterName.</span><span class="sxs-lookup"><span data-stu-id="f58a9-329">Because you have a very specific selection, hello **measure Avg()** command can return hello average not by computer, but across hello farm, simply by grouping by CounterName.</span></span> <span data-ttu-id="f58a9-330">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-330">For example:</span></span>

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

<span data-ttu-id="f58a9-331">Esto proporciona una vista útil compacta de un par de KPI de su entorno.</span><span class="sxs-lookup"><span data-stu-id="f58a9-331">This gives you a useful compact view of a couple of your environment's KPIs.</span></span>

![search avg grouping](./media/log-analytics-log-searches/oms-search-avg04.png)

<span data-ttu-id="f58a9-333">Puede usar fácilmente consultas de búsqueda de hello en un panel.</span><span class="sxs-lookup"><span data-stu-id="f58a9-333">You can easily use hello search query in a dashboard.</span></span> <span data-ttu-id="f58a9-334">Por ejemplo, puede guardar la consulta de búsqueda de Hola y crear un panel de llamado *KPI de granja de servidores Web*.</span><span class="sxs-lookup"><span data-stu-id="f58a9-334">For example, you could save hello search query and create a dashboard from it named *Web Farm KPIs*.</span></span> <span data-ttu-id="f58a9-335">toolearn más información acerca de los paneles, consulte [crear un panel personalizado en el análisis de registros](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="f58a9-335">toolearn more about using dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span>

![search avg dashboard](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a><span data-ttu-id="f58a9-337">Utilice la función de suma de hello con el comando measure de Hola</span><span class="sxs-lookup"><span data-stu-id="f58a9-337">Use hello sum function with hello measure command</span></span>
<span data-ttu-id="f58a9-338">función de suma de Hello es funciones similares de tooother del comando de medida de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-338">hello sum function is similar tooother functions of hello measure command.</span></span> <span data-ttu-id="f58a9-339">Puede ver un ejemplo sobre cómo toouse Hola función sum en [búsqueda de registros de IIS W3C en Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="f58a9-339">You can see an example about how toouse hello sum function at [W3C IIS Logs Search in Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).</span></span>

<span data-ttu-id="f58a9-340">Puede usar Max() y Min() con cadenas de texto, números, fechas y horas.</span><span class="sxs-lookup"><span data-stu-id="f58a9-340">You can use Max() and Min() with numbers, date times and text strings.</span></span> <span data-ttu-id="f58a9-341">Con cadenas de texto, se ordenan alfabéticamente y obtiene la primera y la última.</span><span class="sxs-lookup"><span data-stu-id="f58a9-341">With text strings, they are sorted alphabetically and you get first and last.</span></span>

<span data-ttu-id="f58a9-342">Sin embargo, no puede usar Sum() con campos que no sean numéricos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-342">However, you cannot use Sum() with anything other than numerical fields.</span></span> <span data-ttu-id="f58a9-343">Esto también aplica tooAvg().</span><span class="sxs-lookup"><span data-stu-id="f58a9-343">This also applies tooAvg().</span></span>

### <a name="use-hello-percentile-function-with-hello-measure-command"></a><span data-ttu-id="f58a9-344">Use la función de percentil de hello con el comando measure de Hola</span><span class="sxs-lookup"><span data-stu-id="f58a9-344">Use hello percentile function with hello measure command</span></span>
<span data-ttu-id="f58a9-345">función de percentil de Hello es tooAvg() y Sum() similares que sólo se puede utilizar para campos numéricos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-345">hello percentile function is similar tooAvg() and Sum() in that you can only use it for numerical fields.</span></span> <span data-ttu-id="f58a9-346">Puede usar cualquier percentil entre 1 too99 en un campo numérico.</span><span class="sxs-lookup"><span data-stu-id="f58a9-346">You can use any percentile between 1 too99 on a numeric field.</span></span> <span data-ttu-id="f58a9-347">También puede usar ambos comandos, **percentile** y **pct**.</span><span class="sxs-lookup"><span data-stu-id="f58a9-347">You can also use both **percentile** and **pct** commands.</span></span> <span data-ttu-id="f58a9-348">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="f58a9-348">Here are few examples:</span></span>  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a><span data-ttu-id="f58a9-349">Utilice Hola donde comando</span><span class="sxs-lookup"><span data-stu-id="f58a9-349">Use hello where command</span></span>
<span data-ttu-id="f58a9-350">Hola donde comando funciona como un filtro, pero se puede aplicar en el filtro de hello canalización toofurther agrega los resultados producidos por un comando de medida, como los resultados de tooraw lugar que se filtran al principio de Hola de una consulta.</span><span class="sxs-lookup"><span data-stu-id="f58a9-350">hello where command works like a filter, but it can be applied in hello pipeline toofurther filter aggregated results that have been produced by a Measure command – as opposed tooraw results that are filtered at hello beginning of a query.</span></span>

<span data-ttu-id="f58a9-351">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-351">For example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

<span data-ttu-id="f58a9-352">Puede agregar otra barra vertical "|" carácter hello y dónde tooonly comando obtener equipos cuyo promedio de CPU es superior al 80%, con Hola después ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-352">You can add another pipe "|" character and hello Where command tooonly get computers whose average CPU is above 80%, with hello following example:</span></span>

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

<span data-ttu-id="f58a9-353">Si está familiarizado con Microsoft System Center Operations Manager, se puede considerar Hola donde en términos de módulo de administración.</span><span class="sxs-lookup"><span data-stu-id="f58a9-353">If you're familiar with Microsoft System Center - Operations Manager, you can think of hello where command in management pack terms.</span></span> <span data-ttu-id="f58a9-354">Si el ejemplo de Hola fuera una regla, Hola primera parte de consulta de hello sería Hola y origen de datos de Hola donde comando sería la detección de condición de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-354">If hello example were a rule, hello first part of hello query would be hello data source and hello where command would be hello condition detection.</span></span>

<span data-ttu-id="f58a9-355">Puede utilizar consultas de Hola como un icono en **Mi panel**, como un monitor de ordenaciones, toosee cuando CPU de los equipos están sobreutilizados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-355">You can use hello query as a tile in **My Dashboard**, as a monitor of sorts, toosee when computer CPUs are over-utilized.</span></span> <span data-ttu-id="f58a9-356">toolearn más información acerca de los paneles, consulte [crear un panel personalizado en el análisis de registros](log-analytics-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="f58a9-356">toolearn more about dashboards, see [Create a custom dashboard in Log Analytics](log-analytics-dashboards.md).</span></span> <span data-ttu-id="f58a9-357">También puede crear y usar paneles mediante aplicación móvil de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-357">You can also create and use dashboards using hello mobile app.</span></span> <span data-ttu-id="f58a9-358">Para más información, consulte la [aplicación móvil de OMS](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span><span class="sxs-lookup"><span data-stu-id="f58a9-358">For more information, see [OMS Mobile App ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865).</span></span> <span data-ttu-id="f58a9-359">En hello dos iconos inferiores de hello después de la imagen, puede ver Hola monitor muestra una lista y como un número.</span><span class="sxs-lookup"><span data-stu-id="f58a9-359">In hello bottom two tiles of hello following image, you can see hello monitor displayed a list and as a number.</span></span> <span data-ttu-id="f58a9-360">En esencia, que siempre desee Hola número toobe cero y Hola toobe lista vacía.</span><span class="sxs-lookup"><span data-stu-id="f58a9-360">Essentially, you always want hello number toobe zero and hello list toobe empty.</span></span> <span data-ttu-id="f58a9-361">De lo contrario, indica una condición de alerta.</span><span class="sxs-lookup"><span data-stu-id="f58a9-361">Otherwise, it indicates an alert condition.</span></span> <span data-ttu-id="f58a9-362">Si es necesario, puede usarlo tootake un vistazo qué máquinas están bajo presión.</span><span class="sxs-lookup"><span data-stu-id="f58a9-362">If needed, you can use it tootake a look at which machines are under pressure.</span></span>

![mobile dashboard](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a><span data-ttu-id="f58a9-364">Usar hello in (operador)</span><span class="sxs-lookup"><span data-stu-id="f58a9-364">Use hello in operator</span></span>
<span data-ttu-id="f58a9-365">Hola *IN* (operador), junto con *NOT IN* permite toouse las búsquedas secundarias, que son las búsquedas que incluyen otra búsqueda como argumento.</span><span class="sxs-lookup"><span data-stu-id="f58a9-365">hello *IN* operator, along with *NOT IN* allows you toouse subsearches, which are searches that include another search as an argument.</span></span> <span data-ttu-id="f58a9-366">Se encierran entre llaves {} dentro de otra búsqueda *principal* o *exterior*.</span><span class="sxs-lookup"><span data-stu-id="f58a9-366">They are contained in braces {} within another *primary* or *outer* search.</span></span> <span data-ttu-id="f58a9-367">Hola resultado de una búsqueda secundaria, a menudo una lista de resultados diferentes, se usa como argumento en su búsqueda principal.</span><span class="sxs-lookup"><span data-stu-id="f58a9-367">hello result of a subsearch, often a list of distinct results, is then used as an argument in its primary search.</span></span>

<span data-ttu-id="f58a9-368">Puede usar las búsquedas secundarias toomatch subconjuntos de datos que no se pueden describir directamente en una expresión de búsqueda, pero que pueden generarse a partir de una búsqueda.</span><span class="sxs-lookup"><span data-stu-id="f58a9-368">You can use subsearches toomatch subsets of your data that you cannot describe directly in a search expression, but which can be generated from a search.</span></span> <span data-ttu-id="f58a9-369">Por ejemplo, si está interesado en usar un toofind de búsqueda de todos los eventos de *que les faltan actualizaciones de seguridad de equipos*, deberá toodesign una búsqueda secundaria que primero identifique esos *que les faltan actualizaciones de seguridad de equipos*  antes de buscar los eventos que pertenecen toothose hosts.</span><span class="sxs-lookup"><span data-stu-id="f58a9-369">For example, if you’re interested in using one search toofind all events from *computers missing security updates*, then you need toodesign a subsearch that first identifies that *computers missing security updates* before it finds events belonging toothose hosts.</span></span>

<span data-ttu-id="f58a9-370">Por lo tanto, puede expresar *necesitan de equipos que les faltan actualmente actualizaciones de seguridad* con hello después de consulta:</span><span class="sxs-lookup"><span data-stu-id="f58a9-370">So, you could express *computers currently missing required security updates* with hello following query:</span></span>

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![Ejemplo de búsqueda con IN](./media/log-analytics-log-searches/oms-search-in01-revised.png)

<span data-ttu-id="f58a9-372">Una vez que tenga la lista de hello, puede usar búsqueda de hello como una lista de búsqueda interna toofeed Hola de equipos en una búsqueda externa (principal) que buscará eventos de esos equipos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-372">Once you have hello list, you can use hello search as an inner search toofeed hello list of computers into an outer (primary) search that will look for events for those computers.</span></span> <span data-ttu-id="f58a9-373">Para ello escriba búsqueda interna Hola entre llaves e incorpore sus resultados como valores posibles de un campo o filtro en búsqueda externa hello mediante operador IN de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-373">You do this by enclosing hello inner search in braces and feeding its results as possible values for a filter/field in hello outer search using hello IN operator.</span></span> <span data-ttu-id="f58a9-374">consulta de Hello sería algo parecido a:</span><span class="sxs-lookup"><span data-stu-id="f58a9-374">hello query would resemble:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![Ejemplo de búsqueda con IN](./media/log-analytics-log-searches/oms-search-in02-revised.png)

<span data-ttu-id="f58a9-376">También tiempo de Hola de aviso de filtro que se utiliza en la búsqueda interna Hola porque Hola evaluación de actualización del sistema toma una instantánea de todos los equipos cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="f58a9-376">Also notice hello time filter used in hello inner search because hello System Update Assessment takes a snapshot of all computers every 24 hours.</span></span> <span data-ttu-id="f58a9-377">Puede realizar la consulta interna de hello más ligera y precisa si solo busca un día.</span><span class="sxs-lookup"><span data-stu-id="f58a9-377">You can make hello inner query more lightweight and precise by only searching for a day.</span></span> <span data-ttu-id="f58a9-378">búsqueda externa Hello en su lugar usa selección de tiempo de hello en la interfaz de usuario de hello, recupera eventos de hello últimos 7 días.</span><span class="sxs-lookup"><span data-stu-id="f58a9-378">hello outer search instead uses hello time selection in hello user interface, retrieving events from hello last 7 days.</span></span> <span data-ttu-id="f58a9-379">Consulte [Operadores booleanos](#boolean-operators) para más información acerca de los operadores de tiempo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-379">See [Boolean operators](#boolean-operators) for more information about time operators.</span></span>

<span data-ttu-id="f58a9-380">Dado que realmente solo Hola usar los resultados de búsqueda interna de Hola como un valor de filtro para Hola externa, puede aplicar comandos en búsqueda externa Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-380">Because you really only use hello results of hello inner search as a filter value for hello outer one, you can still apply commands in hello outer search.</span></span> <span data-ttu-id="f58a9-381">Por ejemplo, todavía puede Hola de grupo por encima de los eventos con otro comando measure:</span><span class="sxs-lookup"><span data-stu-id="f58a9-381">For example, you can still group hello above events with another measure command:</span></span>

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![Ejemplo de búsqueda con IN](./media/log-analytics-log-searches/oms-search-in03-revised.png)

<span data-ttu-id="f58a9-383">Por lo general, desea que la consulta interna tooexecute rápidamente porque el análisis de registro tiene tiempos de espera del servicio para y también tooreturn una pequeña cantidad de resultados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-383">Generally, you want your inner query tooexecute quickly because Log Analytics has service-side timeouts for it and also tooreturn a small amount of results.</span></span> <span data-ttu-id="f58a9-384">Si la consulta interna de hello devuelve más resultados, se trunca lista de resultados de Hola Hola búsqueda externa tooreturn potencialmente que podría producir resultados incorrectos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-384">If hello inner query returns more results, hello result list gets truncated, which could potentially cause hello outer search tooreturn incorrect results.</span></span>

<span data-ttu-id="f58a9-385">Otra regla es que la búsqueda interna de hello necesita actualmente tooprovide *agregados* resultados.</span><span class="sxs-lookup"><span data-stu-id="f58a9-385">Another rule is that hello inner search currently needs tooprovide *aggregated* results.</span></span> <span data-ttu-id="f58a9-386">Es decir, debe contener un comando *measure* ; actualmente no se pueden proporcionar resultados sin procesar a una búsqueda externa.</span><span class="sxs-lookup"><span data-stu-id="f58a9-386">In other words, it must contain a *measure* command; you cannot currently feed raw results into an outer search.</span></span>

<span data-ttu-id="f58a9-387">Además, puede haber solo un operador IN y este debe ser Hola último filtro de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f58a9-387">Also, there can be only one IN operator and it must be hello last filter in hello query.</span></span> <span data-ttu-id="f58a9-388">No pueden tener varios operadores IN o haría: Esto se evita básicamente ejecuta varias búsquedas secundarias;: Hola importante punto es que solo una búsqueda secundaria o interna es posible para cada búsqueda externa.</span><span class="sxs-lookup"><span data-stu-id="f58a9-388">Multiple IN operators cannot be OR’d – this essentially prevents running multiple subsearches: hello important point is that only one sub/inner search is possible for each outer search.</span></span>

<span data-ttu-id="f58a9-389">Incluso con estos límites, IN permite realizar muchos tipos de búsquedas correlacionadas y le permite toodefine toogroups algo similar como equipos, usuarios o archivos: los campos de hello en los datos contienen.</span><span class="sxs-lookup"><span data-stu-id="f58a9-389">Even with these limits, IN enables many kinds of correlated searches, and allows you toodefine something similar toogroups such as computers, users, or files – whatever hello fields in your data contain.</span></span> <span data-ttu-id="f58a9-390">Estos son otros ejemplos:</span><span class="sxs-lookup"><span data-stu-id="f58a9-390">Here are more examples:</span></span>

<span data-ttu-id="f58a9-391">**Todas las actualizaciones que faltan en equipos donde se deshabilitó la configuración Actualización automática**</span><span class="sxs-lookup"><span data-stu-id="f58a9-391">**All updates missing from computers where Automatic Update setting is disabled**</span></span>

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

<span data-ttu-id="f58a9-392">**Todos los eventos de error de equipos que ejecutan SQL Server (=donde se ejecutó la evaluación de SQL)**</span><span class="sxs-lookup"><span data-stu-id="f58a9-392">**All error events from computers running SQL Server (=where SQL Assessment has run)**</span></span>

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

<span data-ttu-id="f58a9-393">**Todos los eventos de seguridad de equipos que son controladores de dominio (=donde se ejecutó la evaluación de AD)**</span><span class="sxs-lookup"><span data-stu-id="f58a9-393">**All security events from computers that are Domain Controllers (=where AD Assessment has run)**</span></span>

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

<span data-ttu-id="f58a9-394">**¿Qué otras cuentas han iniciado sesión en toohello mismos equipos que cuenta BACONLAND\jochan ha iniciado sesión?**</span><span class="sxs-lookup"><span data-stu-id="f58a9-394">**Which other accounts have logged on toohello same computers where account BACONLAND\jochan has logged on?**</span></span>

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a><span data-ttu-id="f58a9-395">Use el comando distinct de Hola</span><span class="sxs-lookup"><span data-stu-id="f58a9-395">Use hello distinct command</span></span>
<span data-ttu-id="f58a9-396">Como sugiere su nombre hello, este comando proporciona una lista de valores distintos para un campo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-396">As hello name suggests, this command provides a list of distinct values for a field.</span></span> <span data-ttu-id="f58a9-397">Es sorprendentemente sencillo pero muy útil.</span><span class="sxs-lookup"><span data-stu-id="f58a9-397">It's surprisingly simple but quite useful.</span></span> <span data-ttu-id="f58a9-398">Hola que se puede lograr mismo con el comando measure count() así, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="f58a9-398">hello same could be achieved with measure count() command as well, as shown below.</span></span>

```
Type=Event | Measure count() by Computer
```

![Ejemplo del comando de búsqueda DISTINCT](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

<span data-ttu-id="f58a9-400">Sin embargo, si todo lo que le interesa es una lista de valores distintos y no Hola número de documentos que tengan que los valores, a continuación, DISTINCT puede proporcionar tooread más limpio y más fácil de salida y una sintaxis más corta, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="f58a9-400">However, if all you're interested in is just a list of distinct values and not hello count of documents that have that values, then DISTINCT can provide cleaner and easier tooread output, and shorter syntax, as shown below.</span></span>

```
Type=Event | Distinct Computer
```
![Ejemplo del comando de búsqueda DISTINCT](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a><span data-ttu-id="f58a9-402">Usar función countdistinct de hello con comandos de medida de Hola</span><span class="sxs-lookup"><span data-stu-id="f58a9-402">Use hello countdistinct function with hello measure command</span></span>
<span data-ttu-id="f58a9-403">función countdistinct de Hello cuenta número Hola de valores distintos dentro de cada grupo.</span><span class="sxs-lookup"><span data-stu-id="f58a9-403">hello countdistinct function counts hello number of distinct values within each group.</span></span> <span data-ttu-id="f58a9-404">Por ejemplo, es posible usar toocount Hola un número de equipos únicos reporting para cada tipo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-404">For example, it could be used toocount hello number of unique computers reporting for each Type:</span></span>

```
* | measure countdistinct(Computer) by Type
```

![Countdistinct de OMS](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a><span data-ttu-id="f58a9-406">Usar comandos de intervalo de medida de Hola</span><span class="sxs-lookup"><span data-stu-id="f58a9-406">Use hello measure interval command</span></span>
<span data-ttu-id="f58a9-407">Con una recopilación de datos de rendimiento prácticamente en tiempo real, puede recopilar y visualizar cualquier contador de rendimiento en Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="f58a9-407">With near real-time performance data collection, you can collect and visualize any performance counter in Log Analytics.</span></span> <span data-ttu-id="f58a9-408">Basta con escribir consultas de hello **tipo: rendimiento** devolverá miles de métricas gráficos según el número de Hola de contadores y los servidores en su entorno de análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="f58a9-408">Simply entering hello query **Type:Perf** will return thousands of metric graphs based on hello number of counters and servers in your Log Analytics environment.</span></span> <span data-ttu-id="f58a9-409">Con la agregación de métricas a petición, puede mirar Hola métricas generales en su entorno en un nivel alto y profundización en los datos más pormenorizados que necesite.</span><span class="sxs-lookup"><span data-stu-id="f58a9-409">With on-demand metric aggregation, you can look at hello overall metrics in your environment at a high level, and deep dive into more granular data as you need to.</span></span>

<span data-ttu-id="f58a9-410">Supongamos que desea tooknow ¿qué es el promedio de CPU de hello en todos los equipos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-410">Let’s say that you want tooknow what is hello average CPU across all your computers.</span></span> <span data-ttu-id="f58a9-411">Examinando Hola CPU promedio para cada equipo podría no ser útil porque pueden obtener atenuados resultados. toolook con mayor detalle, puede agrupar el resultado en un momento más pequeño fragmentos de ventana y buscar en una serie de tiempo en distintas dimensiones.</span><span class="sxs-lookup"><span data-stu-id="f58a9-411">Looking at hello average CPU for every computer might not be helpful because results may get smoothed out. toolook into more details, you can aggregate your result in a smaller time window chunks, and look into a time series across different dimensions.</span></span> <span data-ttu-id="f58a9-412">Por ejemplo, puede realizar por hora media de hello del uso de CPU a través de todos los equipos como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="f58a9-412">For example, you can perform hello hourly average of CPU usage across all your computers as follows:</span></span>

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![Medida de promedios en un intervalo](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

<span data-ttu-id="f58a9-414">De forma predeterminada, estos resultados se mostrarán en un gráfico de líneas interactivo con varias series.</span><span class="sxs-lookup"><span data-stu-id="f58a9-414">By default these results will be displayed in a multi-series interactive line chart.</span></span>  <span data-ttu-id="f58a9-415">Este gráfico admite alternar entre series (con el cambio de escala del eje Y), usar el zoom y mantener el mouse sobre elementos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-415">This chart supports series toggling (with y-axis rescaling), zooming, and hovering.</span></span>  <span data-ttu-id="f58a9-416">opción de visualización de tabla Hola está todavía disponible para ver los datos sin procesar de hello si es necesario.</span><span class="sxs-lookup"><span data-stu-id="f58a9-416">hello table display option is still available for viewing hello raw data if necessary.</span></span>

<span data-ttu-id="f58a9-417">También puede agrupar por otros campos.</span><span class="sxs-lookup"><span data-stu-id="f58a9-417">You can also group by other fields.</span></span> <span data-ttu-id="f58a9-418">En este ejemplo, que me interesa en todos los contadores % de Hola para un equipo específico y deseo tooknow: ¿qué es cada hora 70 percentiles de Hola de cada contador:</span><span class="sxs-lookup"><span data-stu-id="f58a9-418">In this example, I am looking at all hello % counters for one specific computer, and I want tooknow what is hello hourly 70 percentiles of every counter:</span></span>

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
<span data-ttu-id="f58a9-419">Una toonote lo es que estas consultas no son contadores tooperformance limitado.</span><span class="sxs-lookup"><span data-stu-id="f58a9-419">One thing toonote is that these queries are not limited tooperformance counters.</span></span> <span data-ttu-id="f58a9-420">Se puede aplicar tooany métrica.</span><span class="sxs-lookup"><span data-stu-id="f58a9-420">You can apply them tooany metric.</span></span> <span data-ttu-id="f58a9-421">En este ejemplo, estoy consultando los registros de IIS para W3C.</span><span class="sxs-lookup"><span data-stu-id="f58a9-421">In this example, I’m looking at W3C IIS logs.</span></span> <span data-ttu-id="f58a9-422">Deseo tooknow ¿qué es el tiempo máximo de hello necesario en un intervalo de 5 minutos para procesar cada solicitud:</span><span class="sxs-lookup"><span data-stu-id="f58a9-422">I want tooknow what is hello maximum time it takes over a 5-minute interval for processing each request:</span></span>

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a><span data-ttu-id="f58a9-423">Uso de varios agregados en una consulta</span><span class="sxs-lookup"><span data-stu-id="f58a9-423">Use multiple aggregates in one query</span></span>
<span data-ttu-id="f58a9-424">Puede especificar varias cláusulas de agregado en un comando measure.</span><span class="sxs-lookup"><span data-stu-id="f58a9-424">You can specify multiple aggregate clauses in a measure command.</span></span>  <span data-ttu-id="f58a9-425">A cada una se le puede asignar un alias de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="f58a9-425">Each one can be aliased independently.</span></span>  <span data-ttu-id="f58a9-426">Si no se proporciona un alias resultante de hello nombre del campo será la función de agregado de Hola que usó (es decir, "avg(CounterValue)" para avg(CounterValue)).</span><span class="sxs-lookup"><span data-stu-id="f58a9-426">If it is not given an alias hello resulting field name will be hello aggregate function that was used (i.e. "avg(CounterValue)" for avg(CounterValue)).</span></span>

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![Varios agregados en OMS 1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

<span data-ttu-id="f58a9-428">Este es otro ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f58a9-428">Here is another example:</span></span>

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a><span data-ttu-id="f58a9-429">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f58a9-429">Next steps</span></span>
<span data-ttu-id="f58a9-430">Para más información acerca de las búsquedas de registros, consulte:</span><span class="sxs-lookup"><span data-stu-id="f58a9-430">For additional information about log searches, see:</span></span>

* <span data-ttu-id="f58a9-431">Use [campos personalizados en el análisis de registros](log-analytics-custom-fields.md) tooextend búsquedas de registros.</span><span class="sxs-lookup"><span data-stu-id="f58a9-431">Use [Custom fields in Log Analytics](log-analytics-custom-fields.md) tooextend log searches.</span></span>
* <span data-ttu-id="f58a9-432">Hola de revisión [referencia de búsqueda de registro de análisis de registros](log-analytics-search-reference.md) tooview todos Hola buscar campos y facetas disponibles en el análisis de registros.</span><span class="sxs-lookup"><span data-stu-id="f58a9-432">Review hello [Log Analytics log search reference](log-analytics-search-reference.md) tooview all of hello search fields and facets available in Log Analytics.</span></span>
