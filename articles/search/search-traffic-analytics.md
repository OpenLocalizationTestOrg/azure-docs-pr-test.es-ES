---
title: "Análisis de tráfico de búsqueda para Azure Search | Microsoft Docs"
description: "Habilite el análisis de tráfico de búsqueda para Búsqueda de Azure, un servicio de búsqueda hospedado en la nube en Microsoft Azure, para descubrir información acerca de los usuarios y los datos."
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
ms.openlocfilehash: 303ca5c820f573dc0b58f1910f258403c3baad2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-search-traffic-analytics"></a><span data-ttu-id="59caf-103">Análisis de tráfico de búsqueda</span><span class="sxs-lookup"><span data-stu-id="59caf-103">What is search traffic analytics</span></span>
<span data-ttu-id="59caf-104">Análisis de tráfico de búsqueda es un modelo de implementación de un bucle de comentarios para el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="59caf-104">Search traffic analytics is a pattern for implementing a feedback loop for your search service.</span></span> <span data-ttu-id="59caf-105">Este modelo describe los datos necesarios y cómo recopilarlos con Application Insights, el líder en el sector para la supervisión de servicios en varias plataformas.</span><span class="sxs-lookup"><span data-stu-id="59caf-105">This pattern describes the necessary data and how to collect it using Application Insights, an industry leader for monitoring services in multiple platforms.</span></span>

<span data-ttu-id="59caf-106">Análisis de tráfico de búsqueda le permite tener visibilidad en el servicio de búsqueda y descubrir información acerca de los usuarios y su comportamiento.</span><span class="sxs-lookup"><span data-stu-id="59caf-106">Search traffic analytics lets you gain visibility into your search service and unlock insights about your users and their behavior.</span></span> <span data-ttu-id="59caf-107">Si tiene datos sobre lo que eligen sus usuarios, es posible tomar decisiones que mejoren aún más su experiencia de búsqueda y retroceder cuando los resultados no son los esperados.</span><span class="sxs-lookup"><span data-stu-id="59caf-107">By having data about what your users choose, it's possible to make decisions that further improve your search experience, and to back off when the results are not what expected.</span></span>

<span data-ttu-id="59caf-108">Azure Search ofrece una solución de telemetría que integra Azure Application Insights y Power BI para proporcionar una supervisión y seguimiento detallados.</span><span class="sxs-lookup"><span data-stu-id="59caf-108">Azure Search offers a telemetry solution that integrates Azure Application Insights and Power BI to provide in-depth monitoring and tracking.</span></span> <span data-ttu-id="59caf-109">Puesto que la interacción con Azure Search es sólo a través de API, los desarrolladores deben implementar la telemetría mediante la búsqueda siguiendo las instrucciones de esta página.</span><span class="sxs-lookup"><span data-stu-id="59caf-109">Because interaction with Azure Search is only through APIs, the telemetry must be implemented by the developers using search, following the instructions in this page.</span></span>

## <a name="identify-the-relevant-search-data"></a><span data-ttu-id="59caf-110">Identificación de los datos de búsqueda relevantes</span><span class="sxs-lookup"><span data-stu-id="59caf-110">Identify the relevant search data</span></span>

<span data-ttu-id="59caf-111">Para hacer que las métricas de búsqueda sean útiles, es necesario registrar algunas de las señales de los usuarios de la aplicación de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="59caf-111">To have useful search metrics, it's necessary to log some signals from the users of the search application.</span></span> <span data-ttu-id="59caf-112">Estas señales indican el contenido en el que los usuarios están interesados y que consideran relevantes para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="59caf-112">These signals signify content that users are interested in and that they consider relevant to their needs.</span></span>

<span data-ttu-id="59caf-113">Hay dos señales que necesita Análisis de tráfico de búsqueda:</span><span class="sxs-lookup"><span data-stu-id="59caf-113">There are two signals Search Traffic Analytics needs:</span></span>

1. <span data-ttu-id="59caf-114">Eventos de búsqueda generados por el usuario: solo las consultas de búsqueda iniciadas por un usuario son interesantes.</span><span class="sxs-lookup"><span data-stu-id="59caf-114">User generated search events: only search queries initiated by a user are interesting.</span></span> <span data-ttu-id="59caf-115">Las solicitudes de búsqueda usadas para rellenar las facetas, el contenido adicional o cualquier información interna, no son importantes y sesgan y desvían los resultados.</span><span class="sxs-lookup"><span data-stu-id="59caf-115">Search requests used to populate facets, additional content or any internal information, are not important and they skew and bias your results.</span></span>

2. <span data-ttu-id="59caf-116">Eventos de clic generados por el usuario: mediante los clics en este documento, nos referimos a la selección por parte del usuario de un resultado de búsqueda determinado devuelto a partir de una consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="59caf-116">User generated click events: By clicks in this document, we refer to a user selecting a particular search result returned from a search query.</span></span> <span data-ttu-id="59caf-117">Un clic generalmente significa que un documento es un resultado relevante para una consulta de búsqueda específica.</span><span class="sxs-lookup"><span data-stu-id="59caf-117">A click generally means that a document is a relevant result for a specific search query.</span></span>

<span data-ttu-id="59caf-118">Si vincula la búsqueda y eventos de clic con un identificador de correlación, es posible analizar los comportamientos de los usuarios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="59caf-118">By linking search and click events with a correlation id, it's possible to analyze the behaviors of users on your application.</span></span> <span data-ttu-id="59caf-119">Estas informaciones de búsqueda son imposibles de obtener con solo los registros de tráfico de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="59caf-119">These search insights are impossible to obtain with only search traffic logs.</span></span>

## <a name="how-to-implement-search-traffic-analytics"></a><span data-ttu-id="59caf-120">Implementación de Análisis de tráfico de búsqueda</span><span class="sxs-lookup"><span data-stu-id="59caf-120">How to implement search traffic analytics</span></span>

<span data-ttu-id="59caf-121">Las señales que se mencionan en la sección anterior se deben recopilar a partir de la aplicación de búsqueda a medida que el usuario interactúa con ella.</span><span class="sxs-lookup"><span data-stu-id="59caf-121">The signals mentioned in the preceding section must be gathered from the search application as the user interacts with it.</span></span> <span data-ttu-id="59caf-122">Application Insights es una solución de supervisión extensible, disponible para varias plataformas, con opciones de instrumentación flexibles.</span><span class="sxs-lookup"><span data-stu-id="59caf-122">Application Insights is an extensible monitoring solution, available for multiple platforms, with flexible instrumentation options.</span></span> <span data-ttu-id="59caf-123">El uso de Application Insights le permite aprovechar las ventajas de los informes de búsqueda de Power BI creados por Azure Search para facilitar el análisis de datos.</span><span class="sxs-lookup"><span data-stu-id="59caf-123">Usage of Application Insights lets you take advantage of the Power BI search reports created by Azure Search to make the analysis of data easier.</span></span>

<span data-ttu-id="59caf-124">En la página del [portal](https://portal.azure.com) para el servicio Azure Search, la hoja de Análisis de tráfico de búsqueda contiene una hoja de referencia para seguir este modelo de telemetría.</span><span class="sxs-lookup"><span data-stu-id="59caf-124">In the [portal](https://portal.azure.com) page for your Azure Search service, the Search Traffic Analytics blade contains a cheat sheet for following this telemetry pattern.</span></span> <span data-ttu-id="59caf-125">También puede seleccionar o crear un recurso de Application Insights y ver los datos necesarios, todo en el mismo lugar.</span><span class="sxs-lookup"><span data-stu-id="59caf-125">You can also select or create an Application Insights resource, and see the necessary data, all in one place.</span></span>

![Instrucciones de Análisis de tráfico de búsqueda][1]

### <a name="1-select-an-application-insights-resource"></a><span data-ttu-id="59caf-127">1. Selección de un recurso de Application Insights</span><span class="sxs-lookup"><span data-stu-id="59caf-127">1. Select an Application Insights resource</span></span>

<span data-ttu-id="59caf-128">Tiene que seleccionar un recurso de Application Insights para usar o crear uno si aún no lo tiene.</span><span class="sxs-lookup"><span data-stu-id="59caf-128">You need to select an Application Insights resource to use or create one if you don't have one already.</span></span> <span data-ttu-id="59caf-129">Puede utilizar un recurso que ya esté en uso para registrar los eventos personalizados necesarios.</span><span class="sxs-lookup"><span data-stu-id="59caf-129">You can use a resource that's already in use to log the required custom events.</span></span>

<span data-ttu-id="59caf-130">Al crear un nuevo recurso de Application Insights, todos los tipos de aplicación son válidos para este escenario.</span><span class="sxs-lookup"><span data-stu-id="59caf-130">When creating a new Application Insights resource, all application types are valid for this scenario.</span></span> <span data-ttu-id="59caf-131">Seleccione el que mejor se adapte a la plataforma que usa.</span><span class="sxs-lookup"><span data-stu-id="59caf-131">Select the one that best fits the platform you are using.</span></span>

<span data-ttu-id="59caf-132">Necesita la clave de instrumentación para crear el cliente de telemetría para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="59caf-132">You need the instrumentation key for creating the telemetry client for your application.</span></span> <span data-ttu-id="59caf-133">Puede obtenerlo desde el panel del portal de Application Insights o desde la página de Análisis de tráfico de búsqueda seleccionando la instancia que desee usar.</span><span class="sxs-lookup"><span data-stu-id="59caf-133">You can get it from the Application Insights portal dashboard, or you can get it from the Search Traffic Analytics page, selecting the instance you want to use.</span></span>

### <a name="2-instrument-your-application"></a><span data-ttu-id="59caf-134">2. Instrumentación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="59caf-134">2. Instrument your application</span></span>

<span data-ttu-id="59caf-135">En esta fase se instrumenta su propia aplicación de búsqueda con el recurso de Application Insights creado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="59caf-135">This phase is where you instrument your own search application, using the Application Insights resource your created in the step above.</span></span> <span data-ttu-id="59caf-136">Existen cuatro pasos para este proceso:</span><span class="sxs-lookup"><span data-stu-id="59caf-136">There are four steps to this process:</span></span>

<span data-ttu-id="59caf-137">**I. Creación de un cliente de telemetría** Este es el objeto que envía eventos al recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="59caf-137">**I. Create a telemetry client** This is the object that sends events to the Application Insights Resource.</span></span>

<span data-ttu-id="59caf-138">*C#*</span><span class="sxs-lookup"><span data-stu-id="59caf-138">*C#*</span></span>

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

<span data-ttu-id="59caf-139">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="59caf-139">*JavaScript*</span></span>

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

<span data-ttu-id="59caf-140">Para otros lenguajes y plataformas, vea la [lista](https://docs.microsoft.com/azure/application-insights/app-insights-platforms) completa.</span><span class="sxs-lookup"><span data-stu-id="59caf-140">For other languages and platforms, see the complete [list](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).</span></span>

<span data-ttu-id="59caf-141">**II. Solicitud de un identificador de búsqueda para la correlación** Para correlacionar las solicitudes de búsqueda con clics, es necesario tener un identificador de correlación que relacione estos dos eventos distintos.</span><span class="sxs-lookup"><span data-stu-id="59caf-141">**II. Request a Search ID for correlation** To correlate search requests with clicks, it's necessary to have a correlation id that relates these two distinct events.</span></span> <span data-ttu-id="59caf-142">Azure Search proporciona un identificador de búsqueda cuando lo solicita con un encabezado:</span><span class="sxs-lookup"><span data-stu-id="59caf-142">Azure Search provides you with a Search Id when you request it with a header:</span></span>

<span data-ttu-id="59caf-143">*C#*</span><span class="sxs-lookup"><span data-stu-id="59caf-143">*C#*</span></span>

    // This sample uses the Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

<span data-ttu-id="59caf-144">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="59caf-144">*JavaScript*</span></span>

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

<span data-ttu-id="59caf-145">**III. Eventos de búsqueda de registros**</span><span class="sxs-lookup"><span data-stu-id="59caf-145">**III. Log Search events**</span></span>

<span data-ttu-id="59caf-146">Cada vez que un usuario emite una solicitud de búsqueda, debe registrarla como un evento de búsqueda con el esquema siguiente en un evento personalizado de Application Insights:</span><span class="sxs-lookup"><span data-stu-id="59caf-146">Every time that a search request is issued by a user, you should log that as a search event with the following schema on an Application Insights custom event:</span></span>

<span data-ttu-id="59caf-147">**ServiceName**: (cadena) nombre de servicio de búsqueda **SearchId**: (guid) identificador único de una consulta de búsqueda (viene con la respuesta de búsqueda) **IndexName**: (cadena) índice de servicio que se va a consultar **QueryTerms**: (cadena) términos de búsqueda especificados por el usuario **ResultCount**: (int) número de documentos devueltos (viene en la respuesta de búsqueda) **ScoringProfile**: (cadena) nombre del perfil de puntuación usado, si lo hubiera</span><span class="sxs-lookup"><span data-stu-id="59caf-147">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the search query (comes in the search response) **IndexName**: (string) search service index to be queried **QueryTerms**: (string) search terms entered by the user **ResultCount**: (int) number of documents that were returned (comes in the search response) **ScoringProfile**: (string) name of the scoring profile used, if any</span></span>

> [!NOTE]
> <span data-ttu-id="59caf-148">Solicite el recuento de consultas generadas por el usuario agregando $count=true a la consulta de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="59caf-148">Request count on user generated queries by adding $count=true to your search query.</span></span> <span data-ttu-id="59caf-149">Puede obtener más información [aquí](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span><span class="sxs-lookup"><span data-stu-id="59caf-149">See more information [here](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)</span></span>
>

> [!NOTE]
> <span data-ttu-id="59caf-150">Recuerde registrar solo consultas de búsqueda generadas por usuarios.</span><span class="sxs-lookup"><span data-stu-id="59caf-150">Remember to only log search queries that are generated by users.</span></span>
>

<span data-ttu-id="59caf-151">*C#*</span><span class="sxs-lookup"><span data-stu-id="59caf-151">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

<span data-ttu-id="59caf-152">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="59caf-152">*JavaScript*</span></span>

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

<span data-ttu-id="59caf-153">**IV. Registro de eventos de clic**</span><span class="sxs-lookup"><span data-stu-id="59caf-153">**IV. Log Click events**</span></span>

<span data-ttu-id="59caf-154">Cada vez que un usuario hace clic en un documento, es una señal de que debe registrarse para fines de análisis de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="59caf-154">Every time that a user clicks on a document, that's a signal that must be logged for search analysis purposes.</span></span> <span data-ttu-id="59caf-155">Utilice eventos personalizados de Application Insights para registrar estos eventos con el siguiente esquema:</span><span class="sxs-lookup"><span data-stu-id="59caf-155">Use Application Insights custom events to log these events with the following schema:</span></span>

<span data-ttu-id="59caf-156">**ServiceName**: (cadena) nombre de servicio de búsqueda **SearchId**: (guid) identificador único de la consulta de búsqueda relacionada **DocId**: (cadena) identificador del documento **Position**: (int) posición del documento en la página de resultados de búsqueda</span><span class="sxs-lookup"><span data-stu-id="59caf-156">**ServiceName**: (string) search service name **SearchId**: (guid) unique identifier of the related search query **DocId**: (string) document identifier **Position**: (int) rank of the document in the search results page</span></span>

> [!NOTE]
> <span data-ttu-id="59caf-157">La posición hace referencia al orden cardinal en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="59caf-157">Position refers to the cardinal order in your application.</span></span> <span data-ttu-id="59caf-158">Puede establecer este número, siempre que en todo momento sea el mismo, para permitir la comparación.</span><span class="sxs-lookup"><span data-stu-id="59caf-158">You are free to set this number, as long as it's always the same, to allow for comparison.</span></span>
>

<span data-ttu-id="59caf-159">*C#*</span><span class="sxs-lookup"><span data-stu-id="59caf-159">*C#*</span></span>

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

<span data-ttu-id="59caf-160">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="59caf-160">*JavaScript*</span></span>

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a><span data-ttu-id="59caf-161">3. Análisis con Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="59caf-161">3. Analyze with Power BI Desktop</span></span>

<span data-ttu-id="59caf-162">Una vez que haya instrumentado la aplicación y comprobado que la aplicación se ha conectado correctamente a Application Insights, puede usar una plantilla predefinida creada por Azure Search para Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="59caf-162">After you have instrumented your app and verified your application is correctly connected to Application Insights, you can use a predefined template created by Azure Search for Power BI desktop.</span></span>
<span data-ttu-id="59caf-163">Esta plantilla contiene gráficos y tablas que le ayudarán a tomar decisiones más informadas para mejorar la relevancia y el rendimiento de las búsquedas.</span><span class="sxs-lookup"><span data-stu-id="59caf-163">This template contains charts and tables that help you make more informed decisions to improve your search performance and relevance.</span></span>

<span data-ttu-id="59caf-164">Para crear una instancia de la plantilla de Power BI Desktop, necesita tres fragmentos de información sobre Application Insights.</span><span class="sxs-lookup"><span data-stu-id="59caf-164">To instantiate the Power BI desktop template, you need three pieces of information about Application Insights.</span></span> <span data-ttu-id="59caf-165">Estos datos pueden encontrarse en la página de Análisis de tráfico de búsqueda, cuando seleccione el recurso que utilizar</span><span class="sxs-lookup"><span data-stu-id="59caf-165">This data can be found in the Search Traffic Analytics page, when you select the resource to use</span></span>

![Datos de Application Insights en la hoja de Análisis de tráfico de búsqueda][2]

<span data-ttu-id="59caf-167">Métricas incluidas en la plantilla de PowerBI Desktop:</span><span class="sxs-lookup"><span data-stu-id="59caf-167">Metrics included in the Power BI desktop template:</span></span>

*   <span data-ttu-id="59caf-168">Haga clic para valorar (CTR): proporción de usuarios que hacen clic en un documento específico para el número de número total de búsquedas.</span><span class="sxs-lookup"><span data-stu-id="59caf-168">Click through Rate (CTR): ratio of users who click on a specific document to the number of total searches.</span></span>
*   <span data-ttu-id="59caf-169">Búsquedas sin clics: términos de las consultas principales que no registran ningún clic</span><span class="sxs-lookup"><span data-stu-id="59caf-169">Searches without clicks: terms for top queries that register no clicks</span></span>
*   <span data-ttu-id="59caf-170">Documentos con más clics: documentos con más clics por identificador en las últimas 24 horas, 7 días y 30 días.</span><span class="sxs-lookup"><span data-stu-id="59caf-170">Most clicked documents: most clicked documents by ID in the last 24 hours, 7 days, and 30 days.</span></span>
*   <span data-ttu-id="59caf-171">Pares de documentos de términos populares: términos resultantes en el mismo documento en el que se hizo clic, ordenados por clics.</span><span class="sxs-lookup"><span data-stu-id="59caf-171">Popular term-document pairs: terms that result in the same document clicked, ordered by clicks.</span></span>
*   <span data-ttu-id="59caf-172">Tiempo para hacer clic : clics divididos por tiempo transcurrido desde la consulta de búsqueda</span><span class="sxs-lookup"><span data-stu-id="59caf-172">Time to click: clicks bucketed by time since the search query</span></span>

![Plantilla de Power BI para la lectura desde Application Insights][3]


## <a name="next-steps"></a><span data-ttu-id="59caf-174">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="59caf-174">Next Steps</span></span>
<span data-ttu-id="59caf-175">Instrumente la aplicación de búsqueda para obtener datos eficaces y reveladores sobre el servicio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="59caf-175">Instrument your search application to get powerful and insightful data about your search service.</span></span>

<span data-ttu-id="59caf-176">Puede encontrar más información sobre Application Insights [aquí](https://go.microsoft.com/fwlink/?linkid=842905).</span><span class="sxs-lookup"><span data-stu-id="59caf-176">You can find more information on Application Insights [here](https://go.microsoft.com/fwlink/?linkid=842905).</span></span> <span data-ttu-id="59caf-177">Visite la [página de precios](https://azure.microsoft.com/pricing/details/application-insights/) de Application Insights para obtener más información sobre los distintos niveles de servicio.</span><span class="sxs-lookup"><span data-stu-id="59caf-177">Visit Application Insights [pricing page](https://azure.microsoft.com/pricing/details/application-insights/) to learn more about their different service tiers.</span></span>

<span data-ttu-id="59caf-178">Obtenga más información sobre cómo crear informes increíbles.</span><span class="sxs-lookup"><span data-stu-id="59caf-178">Learn more about creating amazing reports.</span></span> <span data-ttu-id="59caf-179">Consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) para obtener más información</span><span class="sxs-lookup"><span data-stu-id="59caf-179">See [Getting started with Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) for details</span></span>

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
