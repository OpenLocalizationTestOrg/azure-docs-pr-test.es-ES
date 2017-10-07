---
title: aplicaciones web de aaaAzure Application Insights para JavaScript | Documentos de Microsoft
description: "Obtenga recuentos de sesiones y vistas de página, además de datos de cliente web, y realice el seguimiento de los patrones de uso. Detecte problemas de rendimiento y excepciones en páginas web de JavaScript."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="52fc9-104">Application Insights para páginas web</span><span class="sxs-lookup"><span data-stu-id="52fc9-104">Application Insights for web pages</span></span>
<span data-ttu-id="52fc9-105">Obtenga información sobre el rendimiento de Hola y el uso de su aplicación o página web.</span><span class="sxs-lookup"><span data-stu-id="52fc9-105">Find out about hello performance and usage of your web page or app.</span></span> <span data-ttu-id="52fc9-106">Si agrega [Application Insights](app-insights-overview.md) tooyour secuencia de comandos de página, obtendrá los intervalos de carga de página y llamadas de AJAX, recuentos y detalles de excepciones de explorador y errores de AJAX, así como a los usuarios y los recuentos de sesión.</span><span class="sxs-lookup"><span data-stu-id="52fc9-106">If you add [Application Insights](app-insights-overview.md) tooyour page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="52fc9-107">Todos estos datos se pueden segmentar por página, sistema operativo del cliente y versión del explorador, geolocalización y otras dimensiones.</span><span class="sxs-lookup"><span data-stu-id="52fc9-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="52fc9-108">Puede establecer alertas sobre recuentos de errores o sobre cargas de página lentas.</span><span class="sxs-lookup"><span data-stu-id="52fc9-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="52fc9-109">Y mediante la inserción de llamadas de seguimiento en el código de JavaScript, puede realizar un seguimiento cómo se utilizan las diferentes características de saludo de la aplicación de la página web.</span><span class="sxs-lookup"><span data-stu-id="52fc9-109">And by inserting trace calls in your JavaScript code, you can track how hello different features of your web page application are used.</span></span>

<span data-ttu-id="52fc9-110">Puede utilizar Application Insights con cualquier página web, solo tiene que agregar un pequeño fragmento de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="52fc9-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="52fc9-111">Si su servicio web es [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md), puede integrar datos de telemetría desde el servidor y los clientes.</span><span class="sxs-lookup"><span data-stu-id="52fc9-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![En portal.azure.com, abra el recurso de la aplicación y haga clic en el Explorador.](./media/app-insights-javascript/03.png)

<span data-ttu-id="52fc9-113">Necesita una suscripción demasiado[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="52fc9-113">You need a subscription too[Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="52fc9-114">Si su equipo tiene una suscripción de la organización, pida Hola propietario tooadd su tooit Account de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="52fc9-114">If your team has an organizational subscription, ask hello owner tooadd your Microsoft Account tooit.</span></span> <span data-ttu-id="52fc9-115">El desarrollo y la utilización a pequeña escala no implica ningún costo.</span><span class="sxs-lookup"><span data-stu-id="52fc9-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="52fc9-116">Configuración de Application Insights para su página Web</span><span class="sxs-lookup"><span data-stu-id="52fc9-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="52fc9-117">Agregue tooyour las páginas Web Hola cargador código fragmento de código, como sigue.</span><span class="sxs-lookup"><span data-stu-id="52fc9-117">Add hello loader code snippet tooyour web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="52fc9-118">Apertura o creación de recurso en Application Insights</span><span class="sxs-lookup"><span data-stu-id="52fc9-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="52fc9-119">Hola recursos de Application Insights es donde se muestran los datos sobre rendimiento y el uso de la página.</span><span class="sxs-lookup"><span data-stu-id="52fc9-119">hello Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="52fc9-120">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="52fc9-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="52fc9-121">Si ya ha configurado para el servidor de saludo de la aplicación de supervisión, ya dispone de un recurso:</span><span class="sxs-lookup"><span data-stu-id="52fc9-121">If you already set up monitoring for hello server side of your app, you already have a resource:</span></span>

![Seleccione Examinar, Servicios para desarrolladores, Application Insights.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="52fc9-123">Si no tiene uno, créelo:</span><span class="sxs-lookup"><span data-stu-id="52fc9-123">If you don't have one, create it:</span></span>

![Seleccione Nuevo, Servicios para desarrolladores, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="52fc9-125">*¿Tiene ya alguna pregunta?*</span><span class="sxs-lookup"><span data-stu-id="52fc9-125">*Questions already?*</span></span> <span data-ttu-id="52fc9-126">[Creación de recursos en Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="52fc9-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a><span data-ttu-id="52fc9-127">Agregar script tooyour aplicación de hello SDK o las páginas web</span><span class="sxs-lookup"><span data-stu-id="52fc9-127">Add hello SDK script tooyour app or web pages</span></span>
<span data-ttu-id="52fc9-128">En Inicio rápido, obtener script de Hola para páginas web:</span><span class="sxs-lookup"><span data-stu-id="52fc9-128">In Quick Start, get hello script for web pages:</span></span>

![En la hoja de información general sobre la aplicación, elija Inicio rápido, obtener código toomonitor las páginas web.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="52fc9-131">Insertar el script de Hola justo antes de hello `</head>` etiqueta de cada página que desee tootrack.</span><span class="sxs-lookup"><span data-stu-id="52fc9-131">Insert hello script just before hello `</head>` tag of every page you want tootrack.</span></span> <span data-ttu-id="52fc9-132">Si su sitio Web tiene una página maestra, puede colocar el script de Hola no existe.</span><span class="sxs-lookup"><span data-stu-id="52fc9-132">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="52fc9-133">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="52fc9-133">For example:</span></span>

* <span data-ttu-id="52fc9-134">En un proyecto de ASP.NET MVC, lo colocaría en `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="52fc9-134">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="52fc9-135">En un sitio de SharePoint, en el panel de control hello, abra [configuración del sitio o página maestra](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="52fc9-135">In a SharePoint site, on hello control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="52fc9-136">script de Hola contiene la clave de instrumentación de Hola que dirige el recurso de Application Insights de hello datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="52fc9-136">hello script contains hello instrumentation key that directs hello data tooyour Application Insights resource.</span></span> 

<span data-ttu-id="52fc9-137">([Una explicación más detallada del script de Hola. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="52fc9-137">([Deeper explanation of hello script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="52fc9-138">*(Si está usando un marco de página web conocido, mire a ver si encuentra adaptadores de Application Insights). Por ejemplo, hay [un módulo AngularJS](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="52fc9-138">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="52fc9-139">Configuración detallada</span><span class="sxs-lookup"><span data-stu-id="52fc9-139">Detailed configuration</span></span>
<span data-ttu-id="52fc9-140">Hay varios [parámetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) que puede establecer, aunque en la mayoría de los casos, no es necesario.</span><span class="sxs-lookup"><span data-stu-id="52fc9-140">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="52fc9-141">Por ejemplo, puede deshabilitar o limitar número de Hola de llamadas Ajax notificados por la vista de página (tooreduce tráfico).</span><span class="sxs-lookup"><span data-stu-id="52fc9-141">For example, you can disable or limit hello number of Ajax calls reported per page view (tooreduce traffic).</span></span> <span data-ttu-id="52fc9-142">O bien puede establecer depuración modo toohave telemetría mover rápidamente a través de la canalización de hello sin que se va a procesar por lotes.</span><span class="sxs-lookup"><span data-stu-id="52fc9-142">Or you can set debug mode toohave telemetry move rapidly through hello pipeline without being batched.</span></span>

<span data-ttu-id="52fc9-143">tooset estos parámetros, busque esta línea en el fragmento de código de hello y agregar más elementos separados por comas después de él:</span><span class="sxs-lookup"><span data-stu-id="52fc9-143">tooset these parameters, look for this line in hello code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="52fc9-144">Hola [parámetros disponibles](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) incluyen:</span><span class="sxs-lookup"><span data-stu-id="52fc9-144">hello [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="52fc9-145"><a name="run"></a>Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="52fc9-145"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="52fc9-146">Ejecutar la aplicación web, usar un mientras toogenerate telemetría y espera una cuestión de segundos.</span><span class="sxs-lookup"><span data-stu-id="52fc9-146">Run your web app, use it a while toogenerate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="52fc9-147">Puede ejecutar mediante hello **F5** clave en el equipo de desarrollo, o publicarlo y que los usuarios puedan trabajar con él.</span><span class="sxs-lookup"><span data-stu-id="52fc9-147">You can either run it using hello **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="52fc9-148">Si desea toocheck telemetría de Hola que una aplicación web está enviando información de tooApplication, use herramientas de depuración de su explorador (**F12** en muchos exploradores).</span><span class="sxs-lookup"><span data-stu-id="52fc9-148">If you want toocheck hello telemetry that a web app is sending tooApplication Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="52fc9-149">Los datos se envían toodc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="52fc9-149">Data is sent toodc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="52fc9-150">Exploración de los datos de rendimiento del explorador</span><span class="sxs-lookup"><span data-stu-id="52fc9-150">Explore your browser performance data</span></span>
<span data-ttu-id="52fc9-151">Hola abra Explorador hoja tooshow agrega los datos de rendimiento desde los exploradores de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="52fc9-151">Open hello Browser blade tooshow aggregated performance data from your users' browsers.</span></span>

![En portal.azure.com, abra el recurso de la aplicación y haga clic en Configuración, Explorador](./media/app-insights-javascript/03.png)

<span data-ttu-id="52fc9-153">*¿Aún no hay datos? Haga clic en **actualizar** al principio de Hola de página de Hola. ¿Todavía nada? Consulte [Solución de problemas](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="52fc9-153">*No data yet? Click **Refresh** at hello top of hello page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="52fc9-154">Hola explorador hoja es un [hoja de métricas explorador](app-insights-metrics-explorer.md) con filtros predefinidos y elementos a un gráfico.</span><span class="sxs-lookup"><span data-stu-id="52fc9-154">hello Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="52fc9-155">Puede editar intervalo de tiempo de hello, filtros y la configuración de gráfico si desea y guardar el resultado de hello como favorito.</span><span class="sxs-lookup"><span data-stu-id="52fc9-155">You can edit hello time range, filters, and chart configuration if you want, and save hello result as a favorite.</span></span> <span data-ttu-id="52fc9-156">Haga clic en **Restaurar valores predeterminados** tooget toohello atrás configuración original de hoja.</span><span class="sxs-lookup"><span data-stu-id="52fc9-156">Click **Restore defaults** tooget back toohello original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="52fc9-157">Rendimiento de carga de la página</span><span class="sxs-lookup"><span data-stu-id="52fc9-157">Page load performance</span></span>
<span data-ttu-id="52fc9-158">En hello superior es un gráfico segmentado de tiempos de carga de página.</span><span class="sxs-lookup"><span data-stu-id="52fc9-158">At hello top is a segmented chart of page load times.</span></span> <span data-ttu-id="52fc9-159">alto total de Hola de gráfico de Hola representa páginas de tooload y la presentación de tiempo medio de Hola desde la aplicación en los exploradores de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="52fc9-159">hello total height of hello chart represents hello average time tooload and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="52fc9-160">tiempo de Hola se mide desde al explorador de hello envía la solicitud HTTP inicial de hello hasta que la carga sincrónica todos los eventos se han procesado, incluido el diseño y la ejecución de scripts.</span><span class="sxs-lookup"><span data-stu-id="52fc9-160">hello time is measured from when hello browser sends hello initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="52fc9-161">No incluye las tareas asincrónicas, como la carga de elementos web de las llamadas AJAX.</span><span class="sxs-lookup"><span data-stu-id="52fc9-161">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="52fc9-162">gráfico de Hello segmentos de tiempo de carga de página total de hello en hello [estándares intervalos definidos por W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="52fc9-162">hello chart segments hello total page load time into hello [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="52fc9-163">Tenga en cuenta que hello *conectado a la red* tiempo suele ser más lenta de lo que cabría esperar, porque es un promedio a través de todas las solicitudes de servidor de hello explorador toohello.</span><span class="sxs-lookup"><span data-stu-id="52fc9-163">Note that hello *network connect* time is often lower than you might expect, because it's an average over all requests from hello browser toohello server.</span></span> <span data-ttu-id="52fc9-164">Muchas de las solicitudes individuales tienen un tiempo de conexión de 0 porque ya hay un servidor de toohello conexión activa.</span><span class="sxs-lookup"><span data-stu-id="52fc9-164">Many individual requests have a connect time of 0 because there is already an active connection toohello server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="52fc9-165">¿La carga es lenta?</span><span class="sxs-lookup"><span data-stu-id="52fc9-165">Slow loading?</span></span>
<span data-ttu-id="52fc9-166">Una carga de página lenta es una importante fuente de insatisfacción para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="52fc9-166">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="52fc9-167">Gráfico de hello indica la carga de página lenta, resulta fácil toodo cierta investigación de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="52fc9-167">If hello chart indicates slow page loads, it's easy toodo some diagnostic research.</span></span>

<span data-ttu-id="52fc9-168">gráfico de Hello muestra promedio de Hola de todas las cargas de página en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="52fc9-168">hello chart shows hello average of all page loads in your app.</span></span> <span data-ttu-id="52fc9-169">toosee si el problema de Hola limita tooparticular páginas, buscar más hacia abajo de la hoja de hello, donde hay una cuadrícula segmentada por página dirección URL:</span><span class="sxs-lookup"><span data-stu-id="52fc9-169">toosee if hello problem is confined tooparticular pages, look further down hello blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="52fc9-170">Observe el recuento de vistas de página de Hola y la desviación estándar.</span><span class="sxs-lookup"><span data-stu-id="52fc9-170">Notice hello page view count and standard deviation.</span></span> <span data-ttu-id="52fc9-171">Si el recuento de páginas de hello es muy baja, a continuación, Hola problema no está afectando a los usuarios mucho.</span><span class="sxs-lookup"><span data-stu-id="52fc9-171">If hello page count is very low, then hello issue isn't affecting users much.</span></span> <span data-ttu-id="52fc9-172">Una desviación estándar alta (promedio de toohello comparables propio) indica una gran cantidad de la variación entre las mediciones individuales.</span><span class="sxs-lookup"><span data-stu-id="52fc9-172">A high standard deviation (comparable toohello average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="52fc9-173">**Amplíe la información de una dirección URL y una vista de página.**</span><span class="sxs-lookup"><span data-stu-id="52fc9-173">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="52fc9-174">Haga clic en cualquier toosee de nombre de página una hoja de dirección URL del explorador gráficos filtrados toothat simplemente; y, a continuación, en una instancia de una vista de página.</span><span class="sxs-lookup"><span data-stu-id="52fc9-174">Click any page name toosee a blade of browser charts filtered just toothat URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="52fc9-175">Haga clic en `...` para obtener una lista completa de propiedades para ese evento, o bien inspeccionar llamadas de Ajax de Hola y eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="52fc9-175">Click `...` for a full list of properties for that event, or inspect hello Ajax calls and related events.</span></span> <span data-ttu-id="52fc9-176">Llamadas Ajax lentas afectan a Hola tiempo de carga de página global si son sincrónicas.</span><span class="sxs-lookup"><span data-stu-id="52fc9-176">Slow Ajax calls affect hello overall page load time if they are synchronous.</span></span> <span data-ttu-id="52fc9-177">Relacionados con los eventos incluyen solicitudes de servidor para hello misma dirección URL (si ha configurado visión de la aplicación en el servidor web).</span><span class="sxs-lookup"><span data-stu-id="52fc9-177">Related events include server requests for hello same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="52fc9-178">**Evolución del rendimiento de la página en el tiempo.**</span><span class="sxs-lookup"><span data-stu-id="52fc9-178">**Page performance over time.**</span></span> <span data-ttu-id="52fc9-179">Volver a la hoja de exploradores de hello, cambiar la cuadrícula de tiempo de carga de vista de página de hello en un toosee de gráfico de línea si hubiera picos en momentos concretos:</span><span class="sxs-lookup"><span data-stu-id="52fc9-179">Back at hello Browsers blade, change hello Page View Load Time grid into a line chart toosee if there were peaks at particular times:</span></span>

![Haga clic en el encabezado de Hola de cuadrícula de Hola y seleccione un nuevo tipo de gráfico](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="52fc9-181">**Segmentación mediante otras dimensiones.**</span><span class="sxs-lookup"><span data-stu-id="52fc9-181">**Segment by other dimensions.**</span></span> <span data-ttu-id="52fc9-182">¿Quizás las páginas son tooload más lento en una situación determinada de explorador, el sistema operativo cliente o usuario?</span><span class="sxs-lookup"><span data-stu-id="52fc9-182">Maybe your pages are slower tooload on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="52fc9-183">Agregar un nuevo gráfico y experimentar con hello **Group by** dimensión.</span><span class="sxs-lookup"><span data-stu-id="52fc9-183">Add a new chart and experiment with hello **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="52fc9-184">Rendimiento AJAX</span><span class="sxs-lookup"><span data-stu-id="52fc9-184">AJAX Performance</span></span>
<span data-ttu-id="52fc9-185">Asegúrese de que las llamadas AJAX en sus páginas web funcionan correctamente.</span><span class="sxs-lookup"><span data-stu-id="52fc9-185">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="52fc9-186">Suelen ser usado toofill partes de la página de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="52fc9-186">They are often used toofill parts of your page asynchronously.</span></span> <span data-ttu-id="52fc9-187">Aunque hello página general podría cargar rápidamente, los usuarios podrían frustrados por comenzar en elementos web en blanco, esperando datos tooappear en ellos.</span><span class="sxs-lookup"><span data-stu-id="52fc9-187">Although hello overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data tooappear in them.</span></span>

<span data-ttu-id="52fc9-188">Llamadas AJAX realizadas desde la página web se muestran en la hoja de exploradores de hello como dependencias.</span><span class="sxs-lookup"><span data-stu-id="52fc9-188">AJAX calls made from your web page are shown on hello Browsers blade as dependencies.</span></span>

<span data-ttu-id="52fc9-189">Hay gráficos de resumen en la parte superior de Hola de hoja de hello:</span><span class="sxs-lookup"><span data-stu-id="52fc9-189">There are summary charts in hello upper part of hello blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="52fc9-190">y cuadrículas detalladas más abajo:</span><span class="sxs-lookup"><span data-stu-id="52fc9-190">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="52fc9-191">Haga clic en cualquier fila para obtener detalles concretos.</span><span class="sxs-lookup"><span data-stu-id="52fc9-191">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="52fc9-192">Si elimina el filtro de exploradores de hello en hoja hello, servidor y las dependencias de AJAX se incluyen en estos gráficos.</span><span class="sxs-lookup"><span data-stu-id="52fc9-192">If you delete hello Browsers filter on hello blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="52fc9-193">Haga clic en Restaurar valores predeterminados tooreconfigure Hola filtro.</span><span class="sxs-lookup"><span data-stu-id="52fc9-193">Click Restore Defaults tooreconfigure hello filter.</span></span>
> 
> 

<span data-ttu-id="52fc9-194">**toodrill en llamadas Ajax error** desplácese hacia abajo de la cuadrícula de errores de dependencia de toohello y, a continuación, haga clic en una instancia específica de toosee de fila.</span><span class="sxs-lookup"><span data-stu-id="52fc9-194">**toodrill into failed Ajax calls** scroll down toohello Dependency failures grid, and then click a row toosee specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="52fc9-195">Haga clic en `...` para telemetría completa de Hola para una llamada de Ajax.</span><span class="sxs-lookup"><span data-stu-id="52fc9-195">Click `...` for hello full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="52fc9-196">¿No se han notificado llamadas Ajax?</span><span class="sxs-lookup"><span data-stu-id="52fc9-196">No Ajax calls reported?</span></span>
<span data-ttu-id="52fc9-197">Llamadas AJAX incluyen las llamadas HTTP/HTTPS realizadas desde script de Hola de la página web.</span><span class="sxs-lookup"><span data-stu-id="52fc9-197">Ajax calls include any HTTP/HTTPS  calls made from hello script of your web page.</span></span> <span data-ttu-id="52fc9-198">Si no se ven notificado, comprobar ese fragmento de código de hello no ha establecido hello `disableAjaxTracking` o `maxAjaxCallsPerView` [parámetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="52fc9-198">If you don't see them reported, check that hello code snippet doesn't set hello `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="52fc9-199">Excepciones de explorador</span><span class="sxs-lookup"><span data-stu-id="52fc9-199">Browser exceptions</span></span>
<span data-ttu-id="52fc9-200">En la hoja de exploradores de hello, hay un gráfico de resumen de las excepciones y una cuadrícula de tipos de excepción más hacia abajo de la hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="52fc9-200">On hello Browsers blade, there's an exceptions summary chart, and a grid of exception types further down hello blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="52fc9-201">Si no ve las excepciones de explorador notificadas, comprobar ese fragmento de código de hello no ha establecido hello `disableExceptionTracking` [parámetro](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span><span class="sxs-lookup"><span data-stu-id="52fc9-201">If you don't see browser exceptions reported, check that hello code snippet doesn't set hello `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="52fc9-202">Inspección de eventos de vista de página individuales</span><span class="sxs-lookup"><span data-stu-id="52fc9-202">Inspect individual page view events</span></span>

<span data-ttu-id="52fc9-203">Por lo general, Application Insights analiza la telemetría de vista de página y usted solo verá informes acumulativos, cuya media se ha calculado en función de todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="52fc9-203">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="52fc9-204">Pero a efectos de depuración, también puede ver eventos de vista de página individuales.</span><span class="sxs-lookup"><span data-stu-id="52fc9-204">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="52fc9-205">En la hoja de búsqueda de diagnóstico de hello, establezca filtros tooPage vista.</span><span class="sxs-lookup"><span data-stu-id="52fc9-205">In hello Diagnostic Search blade, set Filters tooPage View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="52fc9-206">Seleccione cualquier toosee de eventos más detallados.</span><span class="sxs-lookup"><span data-stu-id="52fc9-206">Select any event toosee more detail.</span></span> <span data-ttu-id="52fc9-207">En la página de detalles de hello, haga clic en "..." toosee todavía con más detalle.</span><span class="sxs-lookup"><span data-stu-id="52fc9-207">In hello details page, click "..." toosee even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="52fc9-208">Si usa [búsqueda](app-insights-diagnostic-search.md), observe que tiene palabras completas toomatch: "Iene" y "má" no coincide con "About".</span><span class="sxs-lookup"><span data-stu-id="52fc9-208">If you use [Search](app-insights-diagnostic-search.md), notice that you have toomatch whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="52fc9-209">También puede usar hello eficaz [lenguaje de consulta de análisis de registros](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch las vistas de página.</span><span class="sxs-lookup"><span data-stu-id="52fc9-209">You can also use hello powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="52fc9-210">Propiedades de la vista de página</span><span class="sxs-lookup"><span data-stu-id="52fc9-210">Page view properties</span></span>
* <span data-ttu-id="52fc9-211">**Duración de vista de página**</span><span class="sxs-lookup"><span data-stu-id="52fc9-211">**Page view duration**</span></span> 
  
  * <span data-ttu-id="52fc9-212">De forma predeterminada, Hola tiempo toma tooload Hola página, de toofull de solicitud de cliente cargue (incluidos los archivos auxiliares pero excluidas las tareas asincrónicas como las llamadas de Ajax).</span><span class="sxs-lookup"><span data-stu-id="52fc9-212">By default, hello time it takes tooload hello page, from client request toofull load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="52fc9-213">Si establece `overridePageViewDuration` en hello [configuración de la página](#detailed-configuration), Hola intervalo entre tooexecution de solicitud de cliente de hello primero `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="52fc9-213">If you set `overridePageViewDuration` in hello [page configuration](#detailed-configuration), hello interval between client request tooexecution of hello first `trackPageView`.</span></span> <span data-ttu-id="52fc9-214">Si mueve trackPageView desde su posición normal después de la inicialización de Hola de secuencia de comandos de hello, refleja un valor diferente.</span><span class="sxs-lookup"><span data-stu-id="52fc9-214">If you moved trackPageView from its usual position after hello initialization of hello script, it will reflect a different value.</span></span>
  * <span data-ttu-id="52fc9-215">Si `overridePageViewDuration` establecido y una duración se proporciona un argumento de hello `trackPageView()` llamar, a continuación, el valor del argumento Hola se utiliza en su lugar.</span><span class="sxs-lookup"><span data-stu-id="52fc9-215">If `overridePageViewDuration` is set and a duration argument is provided in hello `trackPageView()` call, then hello argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="52fc9-216">Recuentos de página personalizados</span><span class="sxs-lookup"><span data-stu-id="52fc9-216">Custom page counts</span></span>
<span data-ttu-id="52fc9-217">De forma predeterminada, un recuento de páginas se produce cada vez que se carga una página nueva en el explorador del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="52fc9-217">By default, a page count occurs each time a new page loads into hello client browser.</span></span>  <span data-ttu-id="52fc9-218">Sin embargo, podrían desear toocount vistas de página adicionales.</span><span class="sxs-lookup"><span data-stu-id="52fc9-218">But you might want toocount additional page views.</span></span> <span data-ttu-id="52fc9-219">Por ejemplo, una página puede mostrar su contenido en las pestañas y desea toocount una página al usuario de hello cambia pestañas.</span><span class="sxs-lookup"><span data-stu-id="52fc9-219">For example, a page might display its content in tabs and you want toocount a page when hello user switches tabs.</span></span> <span data-ttu-id="52fc9-220">O código JavaScript en la página de hello podría cargar contenido nuevo sin cambiar la dirección URL del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="52fc9-220">Or JavaScript code in hello page might load new content without changing hello browser's URL.</span></span>

<span data-ttu-id="52fc9-221">Inserte una llamada de JavaScript similar al siguiente en el punto adecuado de hello en el código de cliente:</span><span class="sxs-lookup"><span data-stu-id="52fc9-221">Insert a JavaScript call like this at hello appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="52fc9-222">nombre de la página de Hello puede contener Hola mismo caracteres como una dirección URL, pero nada después de "#" o "?" se omite.</span><span class="sxs-lookup"><span data-stu-id="52fc9-222">hello page name can contain hello same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="52fc9-223">Seguimiento de uso</span><span class="sxs-lookup"><span data-stu-id="52fc9-223">Usage tracking</span></span>
<span data-ttu-id="52fc9-224">¿Desea toofind lo que hacer los usuarios con la aplicación?</span><span class="sxs-lookup"><span data-stu-id="52fc9-224">Want toofind out what your users do with your app?</span></span>

* [<span data-ttu-id="52fc9-225">Obtenga información sobre el seguimiento de uso</span><span class="sxs-lookup"><span data-stu-id="52fc9-225">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="52fc9-226">[Más información sobre las API para eventos y métricas personalizados](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="52fc9-226">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="52fc9-227"><a name="video"></a> Vídeo</span><span class="sxs-lookup"><span data-stu-id="52fc9-227"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="52fc9-228"><a name="next"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52fc9-228"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="52fc9-229">Seguir el uso</span><span class="sxs-lookup"><span data-stu-id="52fc9-229">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="52fc9-230">Eventos y métricas personalizados</span><span class="sxs-lookup"><span data-stu-id="52fc9-230">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="52fc9-231">Compilación - Métrica - Aprendizaje</span><span class="sxs-lookup"><span data-stu-id="52fc9-231">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

