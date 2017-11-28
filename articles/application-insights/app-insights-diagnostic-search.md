---
title: "Búsqueda de Azure Application Insights aaaUsing | Documentos de Microsoft"
description: "Busque y filtre los datos de telemetría sin procesar que envía la aplicación web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a><span data-ttu-id="9ae0c-103">Uso de Búsqueda en Application Insights</span><span class="sxs-lookup"><span data-stu-id="9ae0c-103">Using Search in Application Insights</span></span>
<span data-ttu-id="9ae0c-104">Búsqueda es una característica de [Application Insights](app-insights-overview.md) usar toofind y explorar los elementos de telemetría individuales, como las vistas de página, excepciones o solicitudes web.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-104">Search is a feature of [Application Insights](app-insights-overview.md) that you use toofind and explore individual telemetry items, such as page views, exceptions, or web requests.</span></span> <span data-ttu-id="9ae0c-105">Y puede ver los seguimientos de registros y eventos que haya codificado.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-105">And you can view log traces and events that you have coded.</span></span>

<span data-ttu-id="9ae0c-106">(Para consultas más complejas sobre los datos, use [Analytics](app-insights-analytics-tour.md)).</span><span class="sxs-lookup"><span data-stu-id="9ae0c-106">(For more complex queries over your data, use [Analytics](app-insights-analytics-tour.md).)</span></span>

## <a name="where-do-you-see-search"></a><span data-ttu-id="9ae0c-107">¿Dónde verá Búsqueda?</span><span class="sxs-lookup"><span data-stu-id="9ae0c-107">Where do you see Search?</span></span>
### <a name="in-hello-azure-portal"></a><span data-ttu-id="9ae0c-108">Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9ae0c-108">In hello Azure portal</span></span>
<span data-ttu-id="9ae0c-109">Puede abrir búsqueda diagnóstico explícitamente desde la hoja de información general de visión de aplicación Hola de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="9ae0c-109">You can open diagnostic search explicitly from hello Application Insights Overview blade of your application:</span></span>

![Open diagnostic search](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

<span data-ttu-id="9ae0c-111">También se abre al hacer clic a través de algunos gráficos y elementos de la cuadrícula.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-111">It also opens when you click through some charts and grid items.</span></span> <span data-ttu-id="9ae0c-112">En este caso, sus filtros están establecidos previamente toofocus en el tipo de saludo del elemento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-112">In this case, its filters are pre-set toofocus on hello type of item you selected.</span></span> 

<span data-ttu-id="9ae0c-113">Por ejemplo, en la hoja de información general de hello, es un gráfico de barras de solicitudes clasificados por tiempo de respuesta.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-113">For example, on hello Overview blade, there's a bar chart of requests classified by response time.</span></span> <span data-ttu-id="9ae0c-114">Haga clic en un toosee de intervalo de rendimiento una lista de las solicitudes individuales en ese intervalo de tiempo de respuesta:</span><span class="sxs-lookup"><span data-stu-id="9ae0c-114">Click through a performance range toosee a list of individual requests in that response time range:</span></span>

![Recorrido mediante clic del rendimiento de la solicitud](./media/app-insights-diagnostic-search/07-open-from-filters.png)

<span data-ttu-id="9ae0c-116">Hola cuerpo principal de búsqueda de diagnóstico es una lista de elementos de telemetría - solicitudes de servidor, la página vistas, los eventos personalizados que ha incluido y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-116">hello main body of Diagnostic Search is a list of telemetry items - server requests, page views, custom events that you have coded, and so on.</span></span> <span data-ttu-id="9ae0c-117">En hello parte superior de la lista de hello es un gráfico de resumen que muestran recuentos de eventos con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-117">At hello top of hello list is a summary chart showing counts of events over time.</span></span>

<span data-ttu-id="9ae0c-118">Haga clic en actualización tooget nuevos eventos.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-118">Click Refresh tooget new events.</span></span>

### <a name="in-visual-studio"></a><span data-ttu-id="9ae0c-119">En Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9ae0c-119">In Visual Studio</span></span>

<span data-ttu-id="9ae0c-120">En Visual Studio, también hay una ventana de Búsqueda de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-120">In Visual Studio, there's also an Application Insights Search window.</span></span> <span data-ttu-id="9ae0c-121">Es muy útil para mostrar eventos de telemetría generados por aplicación hello que está depurando.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-121">It's most useful for displaying telemetry events generated by hello application that you're debugging.</span></span> <span data-ttu-id="9ae0c-122">Pero también puede mostrar los eventos de hello recopilados desde la aplicación publicada en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-122">But it can also show hello events collected from your published app at hello Azure portal.</span></span>

<span data-ttu-id="9ae0c-123">Abra la ventana de búsqueda de hello en Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="9ae0c-123">Open hello Search window in Visual Studio:</span></span>

![Búsqueda de Application Insights abierta en Visual Studio](./media/app-insights-diagnostic-search/32.png)

<span data-ttu-id="9ae0c-125">ventana de búsqueda de Hello tiene portal de características similares toohello web:</span><span class="sxs-lookup"><span data-stu-id="9ae0c-125">hello Search window has features similar toohello web portal:</span></span>

![Ventana de búsqueda de Application Insights en Visual Studio](./media/app-insights-diagnostic-search/34.png)

<span data-ttu-id="9ae0c-127">pestaña de la operación de seguimiento de Hello está disponible al abrir una solicitud o una vista de página.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-127">hello Track Operation tab is available when you open a request or a page view.</span></span> <span data-ttu-id="9ae0c-128">Una "operación" es una secuencia de eventos que está asociada a la vista única de solicitud o la página tooa.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-128">An 'operation' is a sequence of events that is associated with tooa single request or page view.</span></span> <span data-ttu-id="9ae0c-129">Por ejemplo, llamadas de dependencia, excepciones, registros de seguimiento y eventos personalizados pueden ser parte de una única operación.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-129">For example, dependency calls, exceptions, trace logs, and custom events might be part of a single operation.</span></span> <span data-ttu-id="9ae0c-130">Hola operación de seguimiento ficha muestra gráficamente Hola tiempo y la duración de estos eventos en la vista de solicitud o la página de toohello de relación.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-130">hello Track Operation tab shows graphically hello timing and duration of these events in relation toohello request or page view.</span></span> 

## <a name="inspect-individual-items"></a><span data-ttu-id="9ae0c-131">Inspección de elementos individuales</span><span class="sxs-lookup"><span data-stu-id="9ae0c-131">Inspect individual items</span></span>
<span data-ttu-id="9ae0c-132">Seleccione los campos de clave de telemetría elemento toosee y elementos relacionados.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-132">Select any telemetry item toosee key fields and related items.</span></span> <span data-ttu-id="9ae0c-133">Si desea que el conjunto completo de hello toosee de campos, haga clic en "...".</span><span class="sxs-lookup"><span data-stu-id="9ae0c-133">If you want toosee hello full set of fields, click "...".</span></span> 

![Haga clic en nuevo elemento de trabajo, editar los campos de hello y, a continuación, haga clic en Aceptar.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a><span data-ttu-id="9ae0c-135">Filtro de los tipos de evento</span><span class="sxs-lookup"><span data-stu-id="9ae0c-135">Filter event types</span></span>
<span data-ttu-id="9ae0c-136">Abra la hoja de filtro de Hola y elegir tipos de evento de Hola desea toosee.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-136">Open hello Filter blade and choose hello event types you want toosee.</span></span> <span data-ttu-id="9ae0c-137">(Si, más adelante, desea que los filtros de hello toorestore con el que se abrió hoja hello, haga clic en Restablecer).</span><span class="sxs-lookup"><span data-stu-id="9ae0c-137">(If, later, you want toorestore hello filters with which you opened hello blade, click Reset.)</span></span>

![Elija Filtrar y seleccione los tipos de telemetría](./media/app-insights-diagnostic-search/02-filter-req.png)

<span data-ttu-id="9ae0c-139">los tipos de evento de Hello son:</span><span class="sxs-lookup"><span data-stu-id="9ae0c-139">hello event types are:</span></span>

* <span data-ttu-id="9ae0c-140">**Seguimiento** - [registros de diagnóstico](app-insights-asp-net-trace-logs.md), como llamadas a TrackTrace, log4Net, NLog y System.Diagnostic.Trace.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-140">**Trace** - [Diagnostic logs](app-insights-asp-net-trace-logs.md) including TrackTrace, log4Net, NLog, and System.Diagnostic.Trace calls.</span></span>
* <span data-ttu-id="9ae0c-141">**Solicitud** - solicitudes HTTP recibidas por la aplicación de servidor, como páginas, scripts, imágenes, archivos de estilo y datos.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-141">**Request** - HTTP requests received by your server application, including pages, scripts, images, style files, and data.</span></span> <span data-ttu-id="9ae0c-142">Estos eventos son gráficos de información general de solicitud y respuesta para la Hola de toocreate usado.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-142">These events are used toocreate hello request and response overview charts.</span></span>
* <span data-ttu-id="9ae0c-143">**Vista de página** - [telemetría enviados por el cliente web de hello](app-insights-javascript.md), usa toocreate página Ver informes.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-143">**Page View** - [Telemetry sent by hello web client](app-insights-javascript.md), used toocreate page view reports.</span></span> 
* <span data-ttu-id="9ae0c-144">**Evento personalizado** : si se insertan llamadas tooTrackEvent() en orden demasiado[supervisar el uso de](app-insights-api-custom-events-metrics.md), puede buscar aquí.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-144">**Custom Event** - If you inserted calls tooTrackEvent() in order too[monitor usage](app-insights-api-custom-events-metrics.md), you can search them here.</span></span>
* <span data-ttu-id="9ae0c-145">**Excepción** - no detectada [las excepciones producidas en el servidor de hello](app-insights-asp-net-exceptions.md)y los que inicie sesión con TrackException().</span><span class="sxs-lookup"><span data-stu-id="9ae0c-145">**Exception** - Uncaught [exceptions in hello server](app-insights-asp-net-exceptions.md), and those that you log by using TrackException().</span></span>
* <span data-ttu-id="9ae0c-146">**Dependencia** - [llamadas desde una aplicación de servidor](app-insights-asp-net-dependencies.md) tooother servicios, tales como las API de REST o bases de datos y llamadas de AJAX desde su [código de cliente](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="9ae0c-146">**Dependency** - [Calls from your server application](app-insights-asp-net-dependencies.md) tooother services such as REST APIs or databases, and AJAX calls from your [client code](app-insights-javascript.md).</span></span>
* <span data-ttu-id="9ae0c-147">**Disponibilidad**: resultados de [pruebas de disponibilidad](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="9ae0c-147">**Availability** - Results of [availability tests](app-insights-monitor-web-app-availability.md).</span></span>

## <a name="filter-on-property-values"></a><span data-ttu-id="9ae0c-148">Filtro de los valores de propiedad</span><span class="sxs-lookup"><span data-stu-id="9ae0c-148">Filter on property values</span></span>
<span data-ttu-id="9ae0c-149">Puede filtrar eventos en los valores de hello de sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-149">You can filter events on hello values of their properties.</span></span> <span data-ttu-id="9ae0c-150">propiedades disponibles de Hello dependen de los tipos de evento de Hola que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-150">hello available properties depend on hello event types you selected.</span></span> 

<span data-ttu-id="9ae0c-151">Por ejemplo, seleccione solicitudes con un código de respuesta específico.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-151">For example, pick out requests with a specific response code.</span></span> 

![Expanda una propiedad y elija un valor](./media/app-insights-diagnostic-search/03-response500.png)

<span data-ttu-id="9ae0c-153">No elegir ningún valor de una propiedad determinada tiene el mismo efecto que elegir todos los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-153">Choosing no values of a particular property has hello same effect as choosing all values.</span></span> <span data-ttu-id="9ae0c-154">Se desactiva el filtrado en esa propiedad.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-154">It switches off filtering on that property.</span></span>

### <a name="narrow-your-search"></a><span data-ttu-id="9ae0c-155">Acotación de la búsqueda</span><span class="sxs-lookup"><span data-stu-id="9ae0c-155">Narrow your search</span></span>
<span data-ttu-id="9ae0c-156">Observe que Hola cuenta toohello derecha de los valores de filtro de Hola muestran cuántas repeticiones no existe están en conjunto filtrado de hello actual.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-156">Notice that hello counts toohello right of hello filter values show how many occurrences there are in hello current filtered set.</span></span> 

<span data-ttu-id="9ae0c-157">En este ejemplo, es evidente de que esa solicitud de ' Rpt/empleados' hello hace que la mayoría de los errores de hello '500':</span><span class="sxs-lookup"><span data-stu-id="9ae0c-157">In this example, it's clear that hello 'Rpt/Employees' request results in most of hello '500' errors:</span></span>

![Expanda una propiedad y elija un valor](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a><span data-ttu-id="9ae0c-159">Buscar eventos con hello misma propiedad</span><span class="sxs-lookup"><span data-stu-id="9ae0c-159">Find events with hello same property</span></span>
<span data-ttu-id="9ae0c-160">Buscar Hola a todos los elementos con hello mismo valor de propiedad:</span><span class="sxs-lookup"><span data-stu-id="9ae0c-160">Find all hello items with hello same property value:</span></span>

![Haga clic con el botón secundario en una propiedad](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a><span data-ttu-id="9ae0c-162">Datos de saludo de búsqueda</span><span class="sxs-lookup"><span data-stu-id="9ae0c-162">Search hello data</span></span>

> [!NOTE]
> <span data-ttu-id="9ae0c-163">toowrite consultas más complejas, abra [ **análisis** ](app-insights-analytics-tour.md) de arriba Hola de hoja de la búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-163">toowrite more complex queries, open [**Analytics**](app-insights-analytics-tour.md) from hello top of hello Search blade.</span></span>
> 

<span data-ttu-id="9ae0c-164">Puede buscar términos en cualquiera de los valores de propiedad de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-164">You can search for terms in any of hello property values.</span></span> <span data-ttu-id="9ae0c-165">Esto es especialmente útil si ha escrito [eventos personalizados](app-insights-api-custom-events-metrics.md) con valores de propiedad.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-165">This is particularly useful if you have written [custom events](app-insights-api-custom-events-metrics.md) with property values.</span></span> 

<span data-ttu-id="9ae0c-166">Puede ser conveniente tooset un intervalo de tiempo, como búsquedas en un intervalo más corto son más rápidos.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-166">You might want tooset a time range, as searches over a shorter range are faster.</span></span> 

![Open diagnostic search](./media/app-insights-diagnostic-search/appinsights-311search.png)

<span data-ttu-id="9ae0c-168">Busque palabras completas, no subcadenas.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-168">Search for complete words, not substrings.</span></span> <span data-ttu-id="9ae0c-169">Usar caracteres especiales de tooenclose entre comillas.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-169">Use quotation marks tooenclose special characters.</span></span>

| <span data-ttu-id="9ae0c-170">cadena</span><span class="sxs-lookup"><span data-stu-id="9ae0c-170">string</span></span> | <span data-ttu-id="9ae0c-171">is *not* found by</span><span class="sxs-lookup"><span data-stu-id="9ae0c-171">is *not* found by</span></span> | <span data-ttu-id="9ae0c-172">but these do find it</span><span class="sxs-lookup"><span data-stu-id="9ae0c-172">but these do find it</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9ae0c-173">HomeController.About</span><span class="sxs-lookup"><span data-stu-id="9ae0c-173">HomeController.About</span></span> |<span data-ttu-id="9ae0c-174">home</span><span class="sxs-lookup"><span data-stu-id="9ae0c-174">home</span></span><br/><span data-ttu-id="9ae0c-175">controller</span><span class="sxs-lookup"><span data-stu-id="9ae0c-175">controller</span></span><br/><span data-ttu-id="9ae0c-176">out</span><span class="sxs-lookup"><span data-stu-id="9ae0c-176">out</span></span> | <span data-ttu-id="9ae0c-177">homecontroller</span><span class="sxs-lookup"><span data-stu-id="9ae0c-177">homecontroller</span></span><br/><span data-ttu-id="9ae0c-178">about</span><span class="sxs-lookup"><span data-stu-id="9ae0c-178">about</span></span><br/><span data-ttu-id="9ae0c-179">"homecontroller.about"</span><span class="sxs-lookup"><span data-stu-id="9ae0c-179">"homecontroller.about"</span></span>|
|<span data-ttu-id="9ae0c-180">Estados Unidos</span><span class="sxs-lookup"><span data-stu-id="9ae0c-180">United States</span></span>|<span data-ttu-id="9ae0c-181">Uni</span><span class="sxs-lookup"><span data-stu-id="9ae0c-181">Uni</span></span><br/><span data-ttu-id="9ae0c-182">ted</span><span class="sxs-lookup"><span data-stu-id="9ae0c-182">ted</span></span>|<span data-ttu-id="9ae0c-183">united</span><span class="sxs-lookup"><span data-stu-id="9ae0c-183">united</span></span><br/><span data-ttu-id="9ae0c-184">states</span><span class="sxs-lookup"><span data-stu-id="9ae0c-184">states</span></span><br/><span data-ttu-id="9ae0c-185">united AND states</span><span class="sxs-lookup"><span data-stu-id="9ae0c-185">united AND states</span></span><br/><span data-ttu-id="9ae0c-186">"united states"</span><span class="sxs-lookup"><span data-stu-id="9ae0c-186">"united states"</span></span>

<span data-ttu-id="9ae0c-187">Estos son expresiones de búsqueda de Hola que puede utilizar:</span><span class="sxs-lookup"><span data-stu-id="9ae0c-187">Here are hello search expressions you can use:</span></span>

| <span data-ttu-id="9ae0c-188">Consulta de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9ae0c-188">Sample query</span></span> | <span data-ttu-id="9ae0c-189">Efecto</span><span class="sxs-lookup"><span data-stu-id="9ae0c-189">Effect</span></span> |
| --- | --- |
| `apple` |<span data-ttu-id="9ae0c-190">Buscar todos los eventos en intervalo de tiempo de hello cuyos campos incluyen hello palabra "apple"</span><span class="sxs-lookup"><span data-stu-id="9ae0c-190">Find all events in hello time range whose fields include hello word "apple"</span></span> |
| `apple AND banana` |<span data-ttu-id="9ae0c-191">Busca eventos que contienen ambos términos.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-191">Find events that contain both words.</span></span> <span data-ttu-id="9ae0c-192">Utilizar "AND" en mayúsculas, no "and".</span><span class="sxs-lookup"><span data-stu-id="9ae0c-192">Use capital "AND", not "and".</span></span> |
| `apple OR banana`<br/>`apple banana` |<span data-ttu-id="9ae0c-193">Buscar eventos que contengan cualquiera de los dos términos.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-193">Find events that contain either word.</span></span> <span data-ttu-id="9ae0c-194">Usar "OR" no "or".</span><span class="sxs-lookup"><span data-stu-id="9ae0c-194">Use "OR", not "or".</span></span><br/><span data-ttu-id="9ae0c-195">Forma abreviada.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-195">Short form.</span></span> |
| `apple NOT banana` |<span data-ttu-id="9ae0c-196">Buscar eventos que contienen una palabra pero no Hola otro.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-196">Find events that contain one word but not hello other.</span></span> |



## <a name="sampling"></a><span data-ttu-id="9ae0c-197">muestreo</span><span class="sxs-lookup"><span data-stu-id="9ae0c-197">Sampling</span></span>
<span data-ttu-id="9ae0c-198">Si la aplicación genera una gran cantidad de telemetría (y el uso de hello 2.0.0-beta3 de versión de SDK de ASP.NET o una versión posterior), módulo de muestreo adaptativo de hello automáticamente reduce el volumen de Hola que se envía toohello portal enviando sólo una fracción representativa de eventos.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-198">If your app generates a lot of telemetry (and you are using hello ASP.NET SDK version 2.0.0-beta3 or later), hello adaptive sampling module automatically reduces hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="9ae0c-199">Sin embargo, eventos que están relacionado toohello misma solicitud se selecciona o anula la selección como un grupo, por lo que puede desplazarse entre los eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-199">However, events that are related toohello same request are selected or deselected as a group, so that you can navigate between related events.</span></span> 

<span data-ttu-id="9ae0c-200">[Más información sobre el muestreo](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9ae0c-200">[Learn about sampling](app-insights-sampling.md).</span></span>



## <a name="create-work-item"></a><span data-ttu-id="9ae0c-201">Creación de elemento de trabajo</span><span class="sxs-lookup"><span data-stu-id="9ae0c-201">Create work item</span></span>
<span data-ttu-id="9ae0c-202">Puede crear un error en GitHub o Visual Studio Team Services con detalles de Hola desde cualquier elemento de telemetría.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-202">You can create a bug in GitHub or Visual Studio Team Services with hello details from any telemetry item.</span></span> 

![Haga clic en nuevo elemento de trabajo, editar los campos de hello y, a continuación, haga clic en Aceptar.](./media/app-insights-diagnostic-search/42.png)

<span data-ttu-id="9ae0c-204">Hello primera vez para ello, deberá tooconfigure un tooyour vínculo Team Services cuenta y del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-204">hello first time you do this, you are asked tooconfigure a link tooyour Team Services account and project.</span></span>

![Rellenar Hola URL del servidor de Team Services y el nombre del proyecto de Hola y haga clic en autorizar](./media/app-insights-diagnostic-search/41.png)

<span data-ttu-id="9ae0c-206">(También puede configurar vínculo hello en la hoja de elementos de trabajo de Hola.)</span><span class="sxs-lookup"><span data-stu-id="9ae0c-206">(You can also configure hello link on hello Work Items blade.)</span></span>

## <a name="save-your-search"></a><span data-ttu-id="9ae0c-207">Guardado de la búsqueda</span><span class="sxs-lookup"><span data-stu-id="9ae0c-207">Save your search</span></span>
<span data-ttu-id="9ae0c-208">Cuando haya establecido todos los filtros de Hola que desee, puede guardar búsqueda hello como favorito.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-208">When you've set all hello filters you want, you can save hello search as a favorite.</span></span> <span data-ttu-id="9ae0c-209">Si trabaja en una cuenta profesional, puede elegir si tooshare con otros miembros del equipo.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-209">If you work in an organizational account, you can choose whether tooshare it with other team members.</span></span>

![Haga clic en favorito, establezca nombre de Hola y haga clic en Guardar](./media/app-insights-diagnostic-search/08-favorite-save.png)

<span data-ttu-id="9ae0c-211">de nuevo, la búsqueda de Hola de toosee **hoja de información general de toohello vaya** y abrir favoritos:</span><span class="sxs-lookup"><span data-stu-id="9ae0c-211">toosee hello search again, **go toohello overview blade** and open Favorites:</span></span>

![Favoritos](./media/app-insights-diagnostic-search/09-favorite-get.png)

<span data-ttu-id="9ae0c-213">Si ha guardado con el intervalo de tiempo relativo, hoja de volver a abrir hello tiene los datos más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-213">If you saved with Relative time range, hello re-opened blade has hello latest data.</span></span> <span data-ttu-id="9ae0c-214">Si ha guardado con el intervalo de tiempo absoluto, vea Hola mismos datos cada vez.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-214">If you saved with Absolute time range, you see hello same data every time.</span></span> <span data-ttu-id="9ae0c-215">(Si 'Relative' no está disponible cuando se desea toosave un favorito, haga clic en el intervalo de tiempo en el encabezado de Hola y establecer un intervalo de tiempo que no es un intervalo personalizado).</span><span class="sxs-lookup"><span data-stu-id="9ae0c-215">(If 'Relative' isn't available when you want toosave a favorite, click Time Range in hello header, and set a time range that isn't a custom range.)</span></span>

## <a name="send-more-telemetry-tooapplication-insights"></a><span data-ttu-id="9ae0c-216">Enviar telemetría más tooApplication visión</span><span class="sxs-lookup"><span data-stu-id="9ae0c-216">Send more telemetry tooApplication Insights</span></span>
<span data-ttu-id="9ae0c-217">En la telemetría de suma toohello de cuadro enviado por Application Insights SDK, puede:</span><span class="sxs-lookup"><span data-stu-id="9ae0c-217">In addition toohello out-of-the-box telemetry sent by Application Insights SDK, you can:</span></span>

* <span data-ttu-id="9ae0c-218">Capturar seguimientos de registros de su plataforma de registro de favoritos en [.NET](app-insights-asp-net-trace-logs.md) o [Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="9ae0c-218">Capture log traces from your favorite logging framework in [.NET](app-insights-asp-net-trace-logs.md) or [Java](app-insights-java-trace-logs.md).</span></span> <span data-ttu-id="9ae0c-219">Esto significa que puede buscar en los seguimientos de registros y correlacionarlos con vistas de página, excepciones y otros eventos.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-219">This means you can search through your log traces and correlate them with page views, exceptions, and other events.</span></span> 
* <span data-ttu-id="9ae0c-220">[Escribir código](app-insights-api-custom-events-metrics.md) toosend excepciones, eventos personalizados y vistas de página.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-220">[Write code](app-insights-api-custom-events-metrics.md) toosend custom events, page views, and exceptions.</span></span> 

<span data-ttu-id="9ae0c-221">[Obtenga información acerca de cómo se registra toosend y telemetría personalizada tooApplication visión](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="9ae0c-221">[Learn how toosend logs and custom telemetry tooApplication Insights](app-insights-asp-net-trace-logs.md).</span></span>

## <span data-ttu-id="9ae0c-222"><a name="questions"></a>Preguntas y respuestas</span><span class="sxs-lookup"><span data-stu-id="9ae0c-222"><a name="questions"></a>Q & A</span></span>
### <span data-ttu-id="9ae0c-223"><a name="limits"></a>¿Qué cantidad de datos se conserva?</span><span class="sxs-lookup"><span data-stu-id="9ae0c-223"><a name="limits"></a>How much data is retained?</span></span>

<span data-ttu-id="9ae0c-224">Vea hello [resumen límites](app-insights-pricing.md#limits-summary).</span><span class="sxs-lookup"><span data-stu-id="9ae0c-224">See hello [Limits summary](app-insights-pricing.md#limits-summary).</span></span>

### <a name="how-can-i-see-post-data-in-my-server-requests"></a><span data-ttu-id="9ae0c-225">¿Cómo puedo ver datos POST en mis solicitudes de servidor?</span><span class="sxs-lookup"><span data-stu-id="9ae0c-225">How can I see POST data in my server requests?</span></span>
<span data-ttu-id="9ae0c-226">Automáticamente no registramos datos POST de hello, pero puede usar [TrackTrace o registro llamadas](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="9ae0c-226">We don't log hello POST data automatically, but you can use [TrackTrace or log calls](app-insights-asp-net-trace-logs.md).</span></span> <span data-ttu-id="9ae0c-227">Colocar los datos de entrada de hello en el parámetro de mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-227">Put hello POST data in hello message parameter.</span></span> <span data-ttu-id="9ae0c-228">No se puede filtrar en el mensaje de Hola Hola mismo forma puede filtrar según propiedades, pero el límite de tamaño de hello es más largo.</span><span class="sxs-lookup"><span data-stu-id="9ae0c-228">You can't filter on hello message in hello same way you can filter on properties, but hello size limit is longer.</span></span>

## <a name="video"></a><span data-ttu-id="9ae0c-229">Vídeo</span><span class="sxs-lookup"><span data-stu-id="9ae0c-229">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <span data-ttu-id="9ae0c-230"><a name="add"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9ae0c-230"><a name="add"></a>Next steps</span></span>
* [<span data-ttu-id="9ae0c-231">Escribir consultas complejas en Analytics</span><span class="sxs-lookup"><span data-stu-id="9ae0c-231">Write complex queries in Analytics</span></span>](app-insights-analytics-tour.md)
* [<span data-ttu-id="9ae0c-232">Enviar registros y telemetría personalizada tooApplication visión</span><span class="sxs-lookup"><span data-stu-id="9ae0c-232">Send logs and custom telemetry tooApplication Insights</span></span>](app-insights-asp-net-trace-logs.md)
* [<span data-ttu-id="9ae0c-233">Configuración de pruebas de disponibilidad y de capacidad de respuesta</span><span class="sxs-lookup"><span data-stu-id="9ae0c-233">Set up availability and responsiveness tests</span></span>](app-insights-monitor-web-app-availability.md)
* [<span data-ttu-id="9ae0c-234">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="9ae0c-234">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
