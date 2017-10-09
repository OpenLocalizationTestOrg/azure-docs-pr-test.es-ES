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
# <a name="what-is-search-traffic-analytics"></a>Análisis de tráfico de búsqueda
Análisis de tráfico de búsqueda es un modelo de implementación de un bucle de comentarios para el servicio de búsqueda. Este patrón describe los datos necesarios de Hola y cómo toocollect con Application Insights, líder en la industria para la supervisión de servicios en varias plataformas.

Análisis de tráfico de búsqueda le permite tener visibilidad en el servicio de búsqueda y descubrir información acerca de los usuarios y su comportamiento. Si tiene datos sobre los usuarios que elegir, es toomake posibles decisiones que mejoran aún más su experiencia de búsqueda y tooback off cuando Hola resultados no son lo que esperaba.

Búsqueda de Azure ofrece una solución de telemetría que integra Azure Application Insights y Power BI tooprovide supervisión exhaustiva y seguimiento. Dado que interacción con búsqueda de Azure es sólo a través de API, telemetría Hola debe implementarse por los desarrolladores de hello utilizando la búsqueda, siga las instrucciones de hello en esta página.

## <a name="identify-hello-relevant-search-data"></a>Identificar los datos de búsqueda pertinente Hola

las métricas de búsqueda útiles de toohave, es necesario toolog algunas señales de los usuarios de Hola Hola aplicación de búsqueda. Estas señales indican el contenido que los usuarios están interesados en y que tienen en cuenta necesita tootheir relevante.

Hay dos señales que necesita Análisis de tráfico de búsqueda:

1. Eventos de búsqueda generados por el usuario: solo las consultas de búsqueda iniciadas por un usuario son interesantes. Las solicitudes que usan toopopulate facetas de búsqueda, contenido adicional o cualquier información interna, no son importantes y sesgar y desviar los resultados.

2. Click (eventos) generado por los usuarios: por clics en este documento, nos referimos tooa que el usuario seleccione un resultado de búsqueda determinada devuelto desde una consulta de búsqueda. Un clic generalmente significa que un documento es un resultado relevante para una consulta de búsqueda específica.

Mediante la vinculación de búsqueda y haga clic en eventos con un identificador de correlación, es posible tooanalyze comportamientos de Hola de usuarios en la aplicación. Estas informaciones de búsqueda son imposibles de tooobtain con solo los registros de tráfico de búsqueda.

## <a name="how-tooimplement-search-traffic-analytics"></a>Cómo buscar tooimplement en análisis de tráfico

Hola señales mencionan en hello anterior sección se debe recopilar de aplicación de búsqueda de hello como Hola usuario interactúa con él. Application Insights es una solución de supervisión extensible, disponible para varias plataformas, con opciones de instrumentación flexibles. Uso de Application Insights le permite aprovechar las ventajas de los informes de búsqueda de Power BI Hola creado por búsqueda de Azure toomake Hola un análisis de datos sea más fácil.

Hola [portal](https://portal.azure.com) página para el servicio de búsqueda de Azure, hoja de análisis de tráfico de búsqueda de hello contiene una hoja de referencia para seguir este patrón de telemetría. También puede seleccionar o crear un recurso de Application Insights y ver los datos necesarios hello, en un mismo lugar.

![Instrucciones de Análisis de tráfico de búsqueda][1]

### <a name="1-select-an-application-insights-resource"></a>1. Selección de un recurso de Application Insights

Necesita tooselect un toouse de recursos de Application Insights o cree uno si aún no tiene uno. Puede utilizar un recurso ya en uso toolog Hola necesario eventos personalizados.

Al crear un nuevo recurso de Application Insights, todos los tipos de aplicación son válidos para este escenario. Seleccione Hola uno que mejor se adapte a plataforma Hola que usa.

Se necesita la clave de instrumentación de hello para la creación de cliente de telemetría de hello para la aplicación. Puede obtenerlo de panel de portal de Application Insights de Hola o se puede obtener desde página de análisis de tráfico de búsqueda de hello, selección de instancia de Hola que desee toouse.

### <a name="2-instrument-your-application"></a>2. Instrumentación de la aplicación

Esta fase es donde instrumentar su propia aplicación de búsqueda, utilizando su Hola creado en el paso por encima de hello Application Insights recurso. Hay cuatro pasos toothis proceso:

**I. Crear un cliente de telemetría** es objeto de Hola que envía eventos toohello recurso de información de la aplicación.

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

Para otros lenguajes y plataformas, vea Hola completa [lista](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).

**II. Un Id. de búsqueda para la correlación de solicitud** toocorrelate búsqueda solicita con clics, es necesario toohave un identificador de correlación que relaciona estos dos eventos distintos. Azure Search proporciona un identificador de búsqueda cuando lo solicita con un encabezado:

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III. Eventos de búsqueda de registros**

Cada vez que un usuario emite una solicitud de búsqueda debe registrar como un evento de búsqueda con hello después de esquema en un evento personalizado de Application Insights:

**ServiceName**: nombre de servicio de búsqueda (cadena) **el identificador de búsqueda**: identificador único (guid) de consulta de búsqueda de hello (se incluye en la respuesta de la búsqueda de hello) **IndexName**: índice de servicio de búsqueda (cadena) toobe consultada **QueryTerms**: términos de búsqueda (cadena) especificados por el usuario de hello **ResultCount**: (int) número de documentos que se devolvieron (se incluye en la respuesta de la búsqueda de hello)  **ScoringProfile**: nombre de Hola la puntuación del perfil que se usa, si existe (cadena)

> [!NOTE]
> Número de solicitudes en las consultas de usuario generado mediante la adición de $count = true tooyour consulta de búsqueda. Puede obtener más información [aquí](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)
>

> [!NOTE]
> Recuerde que las consultas de búsqueda de registro tooonly generadas por los usuarios.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV. Registro de eventos de clic**

Cada vez que un usuario hace clic en un documento, es una señal de que debe registrarse para fines de análisis de búsqueda. Use Application Insights eventos personalizados toolog estos eventos con hello después de esquema:

**ServiceName**: nombre de servicio de búsqueda (cadena) **el identificador de búsqueda**: identificador único (guid) de consulta de búsqueda relacionada de hello **DocId**: identificador de documento (cadena) **posición** : página de resultados de rango (int) del documento de hello en búsqueda de Hola

> [!NOTE]
> Posición hace referencia toohello cardinal orden en la aplicación. Son tooset libre este número, siempre se siempre Hola iguales, tooallow para la comparación.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3. Análisis con Power BI Desktop

Una vez haya instrumentar la aplicación y comprobar que la aplicación está correctamente conectado tooApplication visión, puede usar una plantilla predefinida creada por búsqueda de Azure para Power BI desktop.
Esta plantilla contiene gráficos y tablas que le ayudarán a realizar tooimprove de las decisiones más informada el rendimiento de la búsqueda y la relevancia.

plantilla de escritorio de tooinstantiate Hola Power BI, necesita tres fragmentos de información acerca de Application Insights. Estos datos pueden encontrarse en la página de análisis de tráfico de búsqueda de hello, cuando se selecciona Hola recursos toouse

![Datos de visión de la aplicación en la hoja de análisis de tráfico de búsqueda de Hola][2]

Métricas incluidas en la plantilla de escritorio de Power BI de hello:

*   Haga clic en a través de velocidad (CTR): proporción de usuarios que hacen clic en un número de documento específico toohello del número total de búsquedas.
*   Búsquedas sin clics: términos de las consultas principales que no registran ningún clic
*   Más hace clic en documentos: hacer clic en documentos con el identificador de hello más últimas 24 horas, 7 días y 30 días.
*   Pares de documentos de término populares: términos que son el resultado de hello hace clic en el mismo documento, ordenados por clics.
*   Tiempo tooclick: clics dividido por tiempo transcurrido desde la consulta de búsqueda de Hola

![Plantilla de Power BI para la lectura desde Application Insights][3]


## <a name="next-steps"></a>Pasos siguientes
Instrumentar búsqueda tooget eficaz y reveladora datos de su aplicación sobre el servicio de búsqueda.

Puede encontrar más información sobre Application Insights [aquí](https://go.microsoft.com/fwlink/?linkid=842905). Visite Application Insights [página de precios](https://azure.microsoft.com/pricing/details/application-insights/) toolearn más información acerca de los distintos niveles de servicio.

Obtenga más información sobre cómo crear informes increíbles. Consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) para obtener más información

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
