---
title: "aaaSearch análisis de tráfico de búsqueda de Azure | Documentos de Microsoft"
description: "Habilitar el análisis de tráfico de búsqueda para búsqueda de Azure, un servicio de búsqueda en la nube hospedado en Microsoft Azure, toounlock información acerca de los usuarios y los datos."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="cd907-103">Análisis de tráfico de búsqueda</span><span class="sxs-lookup"><span data-stu-id="cd907-103">What is search traffic analytics</span></span>
<span data-ttu-id="cd907-104">Análisis de tráfico de búsqueda es un modelo de implementación de un bucle de comentarios para el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cd907-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="cd907-105">Este patrón describe los datos necesarios de Hola y cómo toocollect con Application Insights, líder en la industria para la supervisión de servicios en varias plataformas.</span><span class="sxs-lookup"><span data-stu-id="cd907-105">This pattern describes hello necessary data and how toocollect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="cd907-106">Análisis de tráfico de búsqueda le permite tener visibilidad en el servicio de búsqueda y descubrir información acerca de los usuarios y su comportamiento.</span><span class="sxs-lookup"><span data-stu-id="cd907-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="cd907-107">Si tiene datos sobre los usuarios que elegir, es toomake posibles decisiones que mejoran aún más su experiencia de búsqueda y tooback off cuando Hola resultados no son lo que esperaba.</span><span class="sxs-lookup"><span data-stu-id="cd907-107">By having data about what your users choose, it's possible toomake decisions that further improve your search experience, and tooback off when hello results are not what expected.</span></span>

<span data-ttu-id="cd907-108">Búsqueda de Azure ofrece una solución de telemetría que integra Azure Application Insights y Power BI tooprovide supervisión exhaustiva y seguimiento.</span><span class="sxs-lookup"><span data-stu-id="cd907-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI tooprovide in-depth monitoring and tracking.</span></span> <span data-ttu-id="cd907-109">Dado que interacción con búsqueda de Azure es sólo a través de API, telemetría Hola debe implementarse por los desarrolladores de hello utilizando la búsqueda, siga las instrucciones de hello en esta página.</span><span class="sxs-lookup"><span data-stu-id="cd907-109">Because interaction with Azure Search is only through APIs, hello telemetry must be implemented by hello developers using search, following hello instructions in this page.</span></span>

## <a name="identify-hello-relevant-search-data"></a><span data-ttu-id="cd907-110">Identificar los datos de búsqueda pertinente Hola</span><span class="sxs-lookup"><span data-stu-id="cd907-110">Identify hello relevant search data</span></span>

<span data-ttu-id="cd907-111">las métricas de búsqueda útiles de toohave, es necesario toolog algunas señales de los usuarios de Hola Hola aplicación de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cd907-111">toohave useful search metrics, it's necessary toolog some signals from hello users of hello search application.</span></span> <span data-ttu-id="cd907-112">Estas señales indican el contenido que los usuarios están interesados en y que tienen en cuenta necesita tootheir relevante.</span><span class="sxs-lookup"><span data-stu-id="cd907-112">These signals signify content that users are interested in and that they consider relevant tootheir needs.</span></span>

<span data-ttu-id="cd907-113">Hay dos señales que necesita Análisis de tráfico de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="cd907-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="cd907-114">Eventos de búsqueda generados por el usuario: solo las consultas de búsqueda iniciadas por un usuario son interesantes.</span><span class="sxs-lookup"><span data-stu-id="cd907-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="cd907-115">Las solicitudes que usan toopopulate facetas de búsqueda, contenido adicional o cualquier información interna, no son importantes y sesgar y desviar los resultados.</span><span class="sxs-lookup"><span data-stu-id="cd907-115">Search requests used toopopulate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="cd907-116">Click (eventos) generado por los usuarios: por clics en este documento, nos referimos tooa que el usuario seleccione un resultado de búsqueda determinada devuelto desde una consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cd907-116">User generated click events: By clicks in this document, we refer tooa user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="cd907-117">Un clic generalmente significa que un documento es un resultado relevante para una consulta de búsqueda específica.</span><span class="sxs-lookup"><span data-stu-id="cd907-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="cd907-118">Mediante la vinculación de búsqueda y haga clic en eventos con un identificador de correlación, es posible tooanalyze comportamientos de Hola de usuarios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cd907-118">By linking search and click events with a correlation id, it's possible tooanalyze hello behaviors of users on your application.</span></span> <span data-ttu-id="cd907-119">Estas informaciones de búsqueda son imposibles de tooobtain con solo los registros de tráfico de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cd907-119">These search insights are impossible tooobtain with only search traffic logs.</span></span>

## <a name="how-tooimplement-search-traffic-analytics"></a><span data-ttu-id="cd907-120">Cómo buscar tooimplement en análisis de tráfico</span><span class="sxs-lookup"><span data-stu-id="cd907-120">How tooimplement search traffic analytics</span></span>

<span data-ttu-id="cd907-121">Hola señales mencionan en hello anterior sección se debe recopilar de aplicación de búsqueda de hello como Hola usuario interactúa con él.</span><span class="sxs-lookup"><span data-stu-id="cd907-121">hello signals mentioned in hello preceding section must be gathered from hello search application as hello user interacts with it.</span></span> <span data-ttu-id="cd907-122">Application Insights es una solución de supervisión extensible, disponible para varias plataformas, con opciones de instrumentación flexibles.</span><span class="sxs-lookup"><span data-stu-id="cd907-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="cd907-123">Uso de Application Insights le permite aprovechar las ventajas de los informes de búsqueda de Power BI Hola creado por búsqueda de Azure toomake Hola un análisis de datos sea más fácil.</span><span class="sxs-lookup"><span data-stu-id="cd907-123">Usage of Application Insights lets you take advantage of hello Power BI search reports created by Azure Search toomake hello analysis of data easier.</span></span>

<span data-ttu-id="cd907-124">Hola [portal](https://portal.azure.com) página para el servicio de búsqueda de Azure, hoja de análisis de tráfico de búsqueda de hello contiene una hoja de referencia para seguir este patrón de telemetría.</span><span class="sxs-lookup"><span data-stu-id="cd907-124">In hello [portal](https://portal.azure.com) page for your Azure Search service, hello Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="cd907-125">También puede seleccionar o crear un recurso de Application Insights y ver los datos necesarios hello, en un mismo lugar.</span><span class="sxs-lookup"><span data-stu-id="cd907-125">You can also select or create an Application Insights resource, and see hello necessary data, all in one place.</span></span>

![Instrucciones de Análisis de tráfico de búsqueda][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="cd907-127">1. Selección de un recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="cd907-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="cd907-128">Necesita tooselect un toouse de recursos de Application Insights o cree uno si aún no tiene uno.</span><span class="sxs-lookup"><span data-stu-id="cd907-128">You need tooselect an Application Insights resource toouse or create one if you don't have one already.</span></span> <span data-ttu-id="cd907-129">Puede utilizar un recurso ya en uso toolog Hola necesario eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="cd907-129">You can use a resource that's already in use toolog hello required custom events.</span></span>

<span data-ttu-id="cd907-130">Al crear un nuevo recurso de Application Insights, todos los tipos de aplicación son válidos para este escenario.</span><span class="sxs-lookup"><span data-stu-id="cd907-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="cd907-131">Seleccione Hola uno que mejor se adapte a plataforma Hola que usa.</span><span class="sxs-lookup"><span data-stu-id="cd907-131">Select hello one that best fits hello platform you are using.</span></span>

<span data-ttu-id="cd907-132">Se necesita la clave de instrumentación de hello para la creación de cliente de telemetría de hello para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cd907-132">You need hello instrumentation key for creating hello telemetry client for your application.</span></span> <span data-ttu-id="cd907-133">Puede obtenerlo de panel de portal de Application Insights de Hola o se puede obtener desde página de análisis de tráfico de búsqueda de hello, selección de instancia de Hola que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="cd907-133">You can get it from hello Application Insights portal dashboard, or you can get it from hello Search Traffic Analytics page, selecting hello instance you want toouse.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="cd907-134">2. Instrumentación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="cd907-134">2. Instrument your application</span></span>

<span data-ttu-id="cd907-135">Esta fase es donde instrumentar su propia aplicación de búsqueda, utilizando su Hola creado en el paso por encima de hello Application Insights recurso.</span><span class="sxs-lookup"><span data-stu-id="cd907-135">This phase is where you instrument your own search application, using hello Application Insights resource your created in hello step above.</span></span> <span data-ttu-id="cd907-136">Hay cuatro pasos toothis proceso:</span><span class="sxs-lookup"><span data-stu-id="cd907-136">There are four steps toothis process:</span></span>

<span data-ttu-id="cd907-137">**I. Crear un cliente de telemetría** es objeto de Hola que envía eventos toohello recurso de información de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cd907-137">**I. Create a telemetry client** This is hello object that sends events toohello Application Insights Resource.</span></span>

<span data-ttu-id="cd907-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="cd907-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="cd907-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="cd907-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="cd907-140">Para otros lenguajes y plataformas, vea Hola completa [lista](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span><span class="sxs-lookup"><span data-stu-id="cd907-140">For other languages and platforms, see hello complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="cd907-141">**II. Un Id. de búsqueda para la correlación de solicitud** toocorrelate búsqueda solicita con clics, es necesario toohave un identificador de correlación que relaciona estos dos eventos distintos.</span><span class="sxs-lookup"><span data-stu-id="cd907-141">**II. Request a Search ID for correlation** toocorrelate search requests with clicks, it's necessary toohave a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="cd907-142">Azure Search proporciona un identificador de búsqueda cuando lo solicita con un encabezado:</span><span class="sxs-lookup"><span data-stu-id="cd907-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="cd907-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="cd907-143">*C#*</span></span>

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="cd907-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="cd907-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="cd907-145">**III. Eventos de búsqueda de registros**</span><span class="sxs-lookup"><span data-stu-id="cd907-145">**III. Log Search events**</span></span>

<span data-ttu-id="cd907-146">Cada vez que un usuario emite una solicitud de búsqueda debe registrar como un evento de búsqueda con hello después de esquema en un evento personalizado de Application Insights:</span><span class="sxs-lookup"><span data-stu-id="cd907-146">Every time that a search request is issued by a user, you should log that as a search event with hello following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="cd907-147">**ServiceName**: nombre de servicio de búsqueda (cadena) **el identificador de búsqueda**: identificador único (guid) de consulta de búsqueda de hello (se incluye en la respuesta de la búsqueda de hello) **IndexName**: índice de servicio de búsqueda (cadena) toobe consultada **QueryTerms**: términos de búsqueda (cadena) especificados por el usuario de hello **ResultCount**: (int) número de documentos que se devolvieron (se incluye en la respuesta de la búsqueda de hello)  **ScoringProfile**: nombre de Hola la puntuación del perfil que se usa, si existe (cadena)</span><span class="sxs-lookup"><span data-stu-id="cd907-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello search query (comes in hello search response) **IndexName**: (string) search service index toobe queried **QueryTerms**: (string) search terms entered by hello user **ResultCount**: (int) number of documents that were returned (comes in hello search response) **ScoringProfile**: (string) name of hello scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="cd907-148">Número de solicitudes en las consultas de usuario generado mediante la adición de $count = true tooyour consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cd907-148">Request count on user generated queries by adding $count=true tooyour search query.</span></span> <span data-ttu-id="cd907-149">Puede obtener más información [aquí](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="cd907-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="cd907-150">Recuerde que las consultas de búsqueda de registro tooonly generadas por los usuarios.</span><span class="sxs-lookup"><span data-stu-id="cd907-150">Remember tooonly log search queries that are generated by users.</span></span>
>

<span data-ttu-id="cd907-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="cd907-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="cd907-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="cd907-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="cd907-153">**IV. Registro de eventos de clic**</span><span class="sxs-lookup"><span data-stu-id="cd907-153">**IV. Log Click events**</span></span>

<span data-ttu-id="cd907-154">Cada vez que un usuario hace clic en un documento, es una señal de que debe registrarse para fines de análisis de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cd907-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="cd907-155">Use Application Insights eventos personalizados toolog estos eventos con hello después de esquema:</span><span class="sxs-lookup"><span data-stu-id="cd907-155">Use Application Insights custom events toolog these events with hello following schema:</span></span>

<span data-ttu-id="cd907-156">**ServiceName**: nombre de servicio de búsqueda (cadena) **el identificador de búsqueda**: identificador único (guid) de consulta de búsqueda relacionada de hello **DocId**: identificador de documento (cadena) **posición** : página de resultados de rango (int) del documento de hello en búsqueda de Hola</span><span class="sxs-lookup"><span data-stu-id="cd907-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of hello related search query **DocId**: (string) document identifier **Position**: (int) rank of hello document in hello search results page</span></span>

> [!NOTE]
> <span data-ttu-id="cd907-157">Posición hace referencia toohello cardinal orden en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cd907-157">Position refers toohello cardinal order in your application.</span></span> <span data-ttu-id="cd907-158">Son tooset libre este número, siempre se siempre Hola iguales, tooallow para la comparación.</span><span class="sxs-lookup"><span data-stu-id="cd907-158">You are free tooset this number, as long as it's always hello same, tooallow for comparison.</span></span>
>

<span data-ttu-id="cd907-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="cd907-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="cd907-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="cd907-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="cd907-161">3. Análisis con Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="cd907-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="cd907-162">Una vez haya instrumentar la aplicación y comprobar que la aplicación está correctamente conectado tooApplication visión, puede usar una plantilla predefinida creada por búsqueda de Azure para Power BI desktop.</span><span class="sxs-lookup"><span data-stu-id="cd907-162">After you have instrumented your app and verified your application is correctly connected tooApplication Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="cd907-163">Esta plantilla contiene gráficos y tablas que le ayudarán a realizar tooimprove de las decisiones más informada el rendimiento de la búsqueda y la relevancia.</span><span class="sxs-lookup"><span data-stu-id="cd907-163">This template contains charts and tables that help you make more informed decisions tooimprove your search performance and relevance.</span></span>

<span data-ttu-id="cd907-164">plantilla de escritorio de tooinstantiate Hola Power BI, necesita tres fragmentos de información acerca de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="cd907-164">tooinstantiate hello Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="cd907-165">Estos datos pueden encontrarse en la página de análisis de tráfico de búsqueda de hello, cuando se selecciona Hola recursos toouse</span><span class="sxs-lookup"><span data-stu-id="cd907-165">This data can be found in hello Search Traffic Analytics page, when you select hello resource toouse</span></span>

![Datos de visión de la aplicación en la hoja de análisis de tráfico de búsqueda de Hola][2]

<span data-ttu-id="cd907-167">Métricas incluidas en la plantilla de escritorio de Power BI de hello:</span><span class="sxs-lookup"><span data-stu-id="cd907-167">Metrics included in hello Power BI desktop template:</span></span>

*   <span data-ttu-id="cd907-168">Haga clic en a través de velocidad (CTR): proporción de usuarios que hacen clic en un número de documento específico toohello del número total de búsquedas.</span><span class="sxs-lookup"><span data-stu-id="cd907-168">Click through Rate (CTR): ratio of users who click on a specific document toohello number of total searches.</span></span>
*   <span data-ttu-id="cd907-169">Búsquedas sin clics: términos de las consultas principales que no registran ningún clic</span><span class="sxs-lookup"><span data-stu-id="cd907-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="cd907-170">Más hace clic en documentos: hacer clic en documentos con el identificador de hello más últimas 24 horas, 7 días y 30 días.</span><span class="sxs-lookup"><span data-stu-id="cd907-170">Most clicked documents: most clicked documents by ID in hello last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="cd907-171">Pares de documentos de término populares: términos que son el resultado de hello hace clic en el mismo documento, ordenados por clics.</span><span class="sxs-lookup"><span data-stu-id="cd907-171">Popular term-document pairs: terms that result in hello same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="cd907-172">Tiempo tooclick: clics dividido por tiempo transcurrido desde la consulta de búsqueda de Hola</span><span class="sxs-lookup"><span data-stu-id="cd907-172">Time tooclick: clicks bucketed by time since hello search query</span></span>

![Plantilla de Power BI para la lectura desde Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="cd907-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd907-174">Next Steps</span></span>
<span data-ttu-id="cd907-175">Instrumentar búsqueda tooget eficaz y reveladora datos de su aplicación sobre el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="cd907-175">Instrument your search application tooget powerful and insightful data about your search service.</span></span>

<span data-ttu-id="cd907-176">Puede encontrar más información sobre Application Insights [aquí](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="cd907-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="cd907-177">Visite Application Insights [página de precios](https://azure.microsoft.com/pricing/details/application-insights/) toolearn más información acerca de los distintos niveles de servicio.</span><span class="sxs-lookup"><span data-stu-id="cd907-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) toolearn more about their different service tiers.</span></span>

<span data-ttu-id="cd907-178">Obtenga más información sobre cómo crear informes increíbles.</span><span class="sxs-lookup"><span data-stu-id="cd907-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="cd907-179">Consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) para obtener más información</span><span class="sxs-lookup"><span data-stu-id="cd907-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
