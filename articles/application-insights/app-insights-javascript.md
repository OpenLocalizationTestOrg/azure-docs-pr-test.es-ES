---
title: Azure Application Insights para aplicaciones web de JavaScript | Microsoft Docs
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
ms.openlocfilehash: 4e8a77e3644bb726d1b8e2050dab61893ccfa3c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-web-pages"></a><span data-ttu-id="86873-104">Application Insights para páginas web</span><span class="sxs-lookup"><span data-stu-id="86873-104">Application Insights for web pages</span></span>
<span data-ttu-id="86873-105">Obtenga información sobre el rendimiento y la utilización de su página web o aplicación.</span><span class="sxs-lookup"><span data-stu-id="86873-105">Find out about the performance and usage of your web page or app.</span></span> <span data-ttu-id="86873-106">Si agrega [Application Insights](app-insights-overview.md) al script de la página, obtendrá los intervalos de carga de la página y de las llamadas AJAX, recuentos y detalles sobre las excepciones del explorador y los errores de AJAX, así como usuarios y recuentos de sesiones.</span><span class="sxs-lookup"><span data-stu-id="86873-106">If you add [Application Insights](app-insights-overview.md) to your page script, you get timings of page loads and AJAX calls, counts and details of browser exceptions and AJAX failures, as well as users and session counts.</span></span> <span data-ttu-id="86873-107">Todos estos datos se pueden segmentar por página, sistema operativo del cliente y versión del explorador, geolocalización y otras dimensiones.</span><span class="sxs-lookup"><span data-stu-id="86873-107">All these can be segmented by page, client OS and browser version, geo location, and other dimensions.</span></span> <span data-ttu-id="86873-108">Puede establecer alertas sobre recuentos de errores o sobre cargas de página lentas.</span><span class="sxs-lookup"><span data-stu-id="86873-108">You can set alerts on failure counts or slow page loading.</span></span> <span data-ttu-id="86873-109">Y mediante la inserción de llamadas de seguimiento en el código de JavaScript, puede controlar cómo se utilizan las distintas características de la aplicación de la página web.</span><span class="sxs-lookup"><span data-stu-id="86873-109">And by inserting trace calls in your JavaScript code, you can track how the different features of your web page application are used.</span></span>

<span data-ttu-id="86873-110">Puede utilizar Application Insights con cualquier página web, solo tiene que agregar un pequeño fragmento de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="86873-110">Application Insights can be used with any web pages - you just add a short piece of JavaScript.</span></span> <span data-ttu-id="86873-111">Si su servicio web es [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md), puede integrar datos de telemetría desde el servidor y los clientes.</span><span class="sxs-lookup"><span data-stu-id="86873-111">If your web service is [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md), you can integrate telemetry from your server and clients.</span></span>

![En portal.azure.com, abra el recurso de la aplicación y haga clic en el Explorador.](./media/app-insights-javascript/03.png)

<span data-ttu-id="86873-113">Necesita una suscripción a [Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="86873-113">You need a subscription to [Microsoft Azure](https://azure.com).</span></span> <span data-ttu-id="86873-114">Si su equipo tiene una suscripción organizativa, pida al propietario que le agregue su cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="86873-114">If your team has an organizational subscription, ask the owner to add your Microsoft Account to it.</span></span> <span data-ttu-id="86873-115">El desarrollo y la utilización a pequeña escala no implica ningún costo.</span><span class="sxs-lookup"><span data-stu-id="86873-115">Development and small-scale use won't cost anything.</span></span>

## <a name="set-up-application-insights-for-your-web-page"></a><span data-ttu-id="86873-116">Configuración de Application Insights para su página Web</span><span class="sxs-lookup"><span data-stu-id="86873-116">Set up Application Insights for your web page</span></span>
<span data-ttu-id="86873-117">Agregue el fragmento de código del cargador a las páginas web, como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="86873-117">Add the loader code snippet to your web pages, as follows.</span></span>

### <a name="open-or-create-application-insights-resource"></a><span data-ttu-id="86873-118">Apertura o creación de recurso en Application Insights</span><span class="sxs-lookup"><span data-stu-id="86873-118">Open or create Application Insights resource</span></span>
<span data-ttu-id="86873-119">El recurso de Application Insights es donde se muestran los datos sobre el rendimiento y el uso de la página.</span><span class="sxs-lookup"><span data-stu-id="86873-119">The Application Insights resource is where data about your page's performance and usage is displayed.</span></span> 

<span data-ttu-id="86873-120">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="86873-120">Sign into [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="86873-121">Si ya ha configurado la supervisión del lado del servidor de su aplicación, ya tiene un recurso:</span><span class="sxs-lookup"><span data-stu-id="86873-121">If you already set up monitoring for the server side of your app, you already have a resource:</span></span>

![Seleccione Examinar, Servicios para desarrolladores, Application Insights.](./media/app-insights-javascript/01-find.png)

<span data-ttu-id="86873-123">Si no tiene uno, créelo:</span><span class="sxs-lookup"><span data-stu-id="86873-123">If you don't have one, create it:</span></span>

![Seleccione Nuevo, Servicios para desarrolladores, Application Insights.](./media/app-insights-javascript/01-create.png)

<span data-ttu-id="86873-125">*¿Tiene ya alguna pregunta?*</span><span class="sxs-lookup"><span data-stu-id="86873-125">*Questions already?*</span></span> <span data-ttu-id="86873-126">[Creación de recursos en Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="86873-126">[More about creating a resource](app-insights-create-new-resource.md).</span></span>

### <a name="add-the-sdk-script-to-your-app-or-web-pages"></a><span data-ttu-id="86873-127">Agregar el script de SDK a la aplicación o la página web</span><span class="sxs-lookup"><span data-stu-id="86873-127">Add the SDK script to your app or web pages</span></span>
<span data-ttu-id="86873-128">En Inicio rápido, obtenga el script para páginas web:</span><span class="sxs-lookup"><span data-stu-id="86873-128">In Quick Start, get the script for web pages:</span></span>

![En la hoja de información general de su aplicación, elija Inicio rápido, Obtener código para supervisar mis páginas web.](./media/app-insights-javascript/02-monitor-web-page.png)

<span data-ttu-id="86873-131">Inserte el script justo antes de la etiqueta `</head>` de cada página que desea seguir. Si su sitio web tiene una página maestra, puede colocar el script allí.</span><span class="sxs-lookup"><span data-stu-id="86873-131">Insert the script just before the `</head>` tag of every page you want to track. If your website has a master page, you can put the script there.</span></span> <span data-ttu-id="86873-132">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="86873-132">For example:</span></span>

* <span data-ttu-id="86873-133">En un proyecto de ASP.NET MVC, lo colocaría en `View\Shared\_Layout.cshtml`</span><span class="sxs-lookup"><span data-stu-id="86873-133">In an ASP.NET MVC project, you'd put it in `View\Shared\_Layout.cshtml`</span></span>
* <span data-ttu-id="86873-134">En un sitio de SharePoint, en el panel de control, abra [Configuración del sitio/Página maestra](app-insights-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="86873-134">In a SharePoint site, on the control panel, open [Site Settings / Master Page](app-insights-sharepoint.md).</span></span>

<span data-ttu-id="86873-135">El script contiene la clave de instrumentación que dirige los datos al recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="86873-135">The script contains the instrumentation key that directs the data to your Application Insights resource.</span></span> 

<span data-ttu-id="86873-136">([Una explicación más profunda del script](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span><span class="sxs-lookup"><span data-stu-id="86873-136">([Deeper explanation of the script.](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))</span></span>

<span data-ttu-id="86873-137">*(Si está usando un marco de página web conocido, mire a ver si encuentra adaptadores de Application Insights). Por ejemplo, hay [un módulo AngularJS](http://ngmodules.org/modules/angular-appinsights).)*</span><span class="sxs-lookup"><span data-stu-id="86873-137">*(If you're using a well-known web page framework, look around for Application Insights adaptors. For example, there's [an AngularJS module](http://ngmodules.org/modules/angular-appinsights).)*</span></span>

## <a name="detailed-configuration"></a><span data-ttu-id="86873-138">Configuración detallada</span><span class="sxs-lookup"><span data-stu-id="86873-138">Detailed configuration</span></span>
<span data-ttu-id="86873-139">Hay varios [parámetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) que puede establecer, aunque en la mayoría de los casos, no es necesario.</span><span class="sxs-lookup"><span data-stu-id="86873-139">There are several [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) you can set, though in most cases, you shouldn't need to.</span></span> <span data-ttu-id="86873-140">Por ejemplo, puede deshabilitar o limitar el número de llamadas Ajax notificadas por vista de página (para reducir el tráfico).</span><span class="sxs-lookup"><span data-stu-id="86873-140">For example, you can disable or limit the number of Ajax calls reported per page view (to reduce traffic).</span></span> <span data-ttu-id="86873-141">O bien, puede establecer el modo de depuración para que los datos de telemetría se muevan rápidamente a través de la canalización sin que se procese por lotes.</span><span class="sxs-lookup"><span data-stu-id="86873-141">Or you can set debug mode to have telemetry move rapidly through the pipeline without being batched.</span></span>

<span data-ttu-id="86873-142">Para establecer estos parámetros, busque esta línea en el fragmento de código y agregue más elementos delimitados por comas a continuación:</span><span class="sxs-lookup"><span data-stu-id="86873-142">To set these parameters, look for this line in the code snippet, and add more comma-separated items after it:</span></span>

    })({
      instrumentationKey: "..."
      // Insert here
    });

<span data-ttu-id="86873-143">Entre los [parámetros disponibles](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) se incluyen:</span><span class="sxs-lookup"><span data-stu-id="86873-143">The [available parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) include:</span></span>

    // Send telemetry immediately without batching.
    // Remember to remove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, to reduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up to execution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <span data-ttu-id="86873-144"><a name="run"></a>Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="86873-144"><a name="run"></a>Run your app</span></span>
<span data-ttu-id="86873-145">Ejecute la aplicación web, úsela un rato para generar datos de telemetría y espere unos segundos.</span><span class="sxs-lookup"><span data-stu-id="86873-145">Run your web app, use it a while to generate telemetry, and wait a few seconds.</span></span> <span data-ttu-id="86873-146">Puede ejecutarla con la tecla **F5** en la máquina de desarrollo, o publicarla y dejar que los usuarios jueguen con ella.</span><span class="sxs-lookup"><span data-stu-id="86873-146">You can either run it using the **F5** key on your development machine, or publish it and let users play with it.</span></span>

<span data-ttu-id="86873-147">Si quiere comprobar la telemetría que envía una aplicación web a Application Insights, use las herramientas de depuración del explorador (**F12** en muchos exploradores).</span><span class="sxs-lookup"><span data-stu-id="86873-147">If you want to check the telemetry that a web app is sending to Application Insights, use your browser's debugging tools (**F12** on many browsers).</span></span> <span data-ttu-id="86873-148">Los datos se envían a dc.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="86873-148">Data is sent to dc.services.visualstudio.com.</span></span>

## <a name="explore-your-browser-performance-data"></a><span data-ttu-id="86873-149">Exploración de los datos de rendimiento del explorador</span><span class="sxs-lookup"><span data-stu-id="86873-149">Explore your browser performance data</span></span>
<span data-ttu-id="86873-150">Abra la hoja del Explorador para mostrar los datos de rendimiento agregados de los exploradores de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="86873-150">Open the Browser blade to show aggregated performance data from your users' browsers.</span></span>

![En portal.azure.com, abra el recurso de la aplicación y haga clic en Configuración, Explorador](./media/app-insights-javascript/03.png)

<span data-ttu-id="86873-152">*¿Aún no hay datos? Haga clic en **Actualizar** en la parte superior de la página. ¿Todavía nada? Consulte [Solución de problemas](app-insights-troubleshoot-faq.md).*</span><span class="sxs-lookup"><span data-stu-id="86873-152">*No data yet? Click **Refresh** at the top of the page. Still nothing? See [Troubleshooting](app-insights-troubleshoot-faq.md).*</span></span>

<span data-ttu-id="86873-153">La hoja Explorador es una [hoja del Explorador de métricas](app-insights-metrics-explorer.md) con filtros y selecciones de gráfico preestablecidos.</span><span class="sxs-lookup"><span data-stu-id="86873-153">The Browser blade is a [Metrics Explorer blade](app-insights-metrics-explorer.md) with preset filters and chart selections.</span></span> <span data-ttu-id="86873-154">Si lo desea, puede editar el intervalo de tiempo, los filtros y la configuración de los gráficos y guardar el resultado como favorito.</span><span class="sxs-lookup"><span data-stu-id="86873-154">You can edit the time range, filters, and chart configuration if you want, and save the result as a favorite.</span></span> <span data-ttu-id="86873-155">Haga clic en **Restaurar valores predeterminados** para volver a la configuración original de la hoja.</span><span class="sxs-lookup"><span data-stu-id="86873-155">Click **Restore defaults** to get back to the original blade configuration.</span></span>

## <a name="page-load-performance"></a><span data-ttu-id="86873-156">Rendimiento de carga de la página</span><span class="sxs-lookup"><span data-stu-id="86873-156">Page load performance</span></span>
<span data-ttu-id="86873-157">En la parte superior hay un gráfico segmentado de tiempos de carga de la página.</span><span class="sxs-lookup"><span data-stu-id="86873-157">At the top is a segmented chart of page load times.</span></span> <span data-ttu-id="86873-158">La altura total del gráfico representa el tiempo promedio para cargar y mostrar las páginas desde la aplicación en los exploradores de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="86873-158">The total height of the chart represents the average time to load and display pages from your app in your users' browsers.</span></span> <span data-ttu-id="86873-159">El tiempo se mide desde el momento en que el explorador envía la solicitud HTTP inicial hasta que todos los eventos de la carga sincrónica se han procesado, incluido el diseño y la ejecución de scripts.</span><span class="sxs-lookup"><span data-stu-id="86873-159">The time is measured from when the browser sends the initial HTTP request until all synchronous load events have been processed, including layout and running scripts.</span></span> <span data-ttu-id="86873-160">No incluye las tareas asincrónicas, como la carga de elementos web de las llamadas AJAX.</span><span class="sxs-lookup"><span data-stu-id="86873-160">It doesn't include asynchronous tasks such as loading web parts from AJAX calls.</span></span>

<span data-ttu-id="86873-161">El gráfico divide el tiempo total de carga de las páginas en los [intervalos estándar definidos por W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span><span class="sxs-lookup"><span data-stu-id="86873-161">The chart segments the total page load time into the [standard timings defined by W3C](http://www.w3.org/TR/navigation-timing/#processing-model).</span></span> 

![](./media/app-insights-javascript/08-client-split.png)

<span data-ttu-id="86873-162">Tenga en cuenta que el tiempo de *conexión de red* suele ser menor de lo esperable, ya que es una media de todas las solicitudes del explorador al servidor.</span><span class="sxs-lookup"><span data-stu-id="86873-162">Note that the *network connect* time is often lower than you might expect, because it's an average over all requests from the browser to the server.</span></span> <span data-ttu-id="86873-163">Muchas de las solicitudes individuales tienen un tiempo de conexión de 0 porque ya hay una conexión activa con el servidor.</span><span class="sxs-lookup"><span data-stu-id="86873-163">Many individual requests have a connect time of 0 because there is already an active connection to the server.</span></span>

### <a name="slow-loading"></a><span data-ttu-id="86873-164">¿La carga es lenta?</span><span class="sxs-lookup"><span data-stu-id="86873-164">Slow loading?</span></span>
<span data-ttu-id="86873-165">Una carga de página lenta es una importante fuente de insatisfacción para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="86873-165">Slow page loads are a major source of dissatisfaction for your users.</span></span> <span data-ttu-id="86873-166">Si el gráfico indica una carga de página lenta, es fácil realizar una investigación de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="86873-166">If the chart indicates slow page loads, it's easy to do some diagnostic research.</span></span>

<span data-ttu-id="86873-167">El gráfico muestra el promedio de todas las cargas de páginas en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="86873-167">The chart shows the average of all page loads in your app.</span></span> <span data-ttu-id="86873-168">Para ver si el problema se limita a páginas concretas, consulte más abajo en la hoja, donde hay una cuadrícula dividida por dirección URL de la página:</span><span class="sxs-lookup"><span data-stu-id="86873-168">To see if the problem is confined to particular pages, look further down the blade, where there's a grid segmented by page URL:</span></span>

![](./media/app-insights-javascript/09-page-perf.png)

<span data-ttu-id="86873-169">Observe que el recuento de vistas de página y la desviación estándar.</span><span class="sxs-lookup"><span data-stu-id="86873-169">Notice the page view count and standard deviation.</span></span> <span data-ttu-id="86873-170">Si el número de páginas es muy bajo, el problema no afecta mucho a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="86873-170">If the page count is very low, then the issue isn't affecting users much.</span></span> <span data-ttu-id="86873-171">Una desviación estándar alta (en comparación con el mismo promedio) indica mucha variación entre las mediciones individuales.</span><span class="sxs-lookup"><span data-stu-id="86873-171">A high standard deviation (comparable to the average itself) indicates a lot of variation between individual measurements.</span></span>

<span data-ttu-id="86873-172">**Amplíe la información de una dirección URL y una vista de página.**</span><span class="sxs-lookup"><span data-stu-id="86873-172">**Zoom in on one URL and one page view.**</span></span> <span data-ttu-id="86873-173">Haga clic en cualquier nombre de página para ver una hoja de gráficos de explorador filtrada solo para esa dirección URL y, a continuación, en una instancia de una vista de página.</span><span class="sxs-lookup"><span data-stu-id="86873-173">Click any page name to see a blade of browser charts filtered just to that URL; and then on an instance of a page view.</span></span>

![](./media/app-insights-javascript/35.png)

<span data-ttu-id="86873-174">Haga clic en `...` para obtener una lista completa de las propiedades del evento, o bien inspeccione las llamadas Ajax y los eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="86873-174">Click `...` for a full list of properties for that event, or inspect the Ajax calls and related events.</span></span> <span data-ttu-id="86873-175">Las llamadas Ajax lentas afectan al tiempo total de carga de la página si son sincrónicas.</span><span class="sxs-lookup"><span data-stu-id="86873-175">Slow Ajax calls affect the overall page load time if they are synchronous.</span></span> <span data-ttu-id="86873-176">Entre los eventos relacionados se incluyen las solicitudes del servidor para la misma dirección URL (si ha configurado Application Insights en el servidor web).</span><span class="sxs-lookup"><span data-stu-id="86873-176">Related events include server requests for the same URL (if you've set up Application Insights on your web server).</span></span>

<span data-ttu-id="86873-177">**Evolución del rendimiento de la página en el tiempo.**</span><span class="sxs-lookup"><span data-stu-id="86873-177">**Page performance over time.**</span></span> <span data-ttu-id="86873-178">De nuevo en la hoja de exploradores, cambie la cuadrícula de tiempo de carga de la vista de página en un gráfico de líneas para ver si hay picos en momentos concretos:</span><span class="sxs-lookup"><span data-stu-id="86873-178">Back at the Browsers blade, change the Page View Load Time grid into a line chart to see if there were peaks at particular times:</span></span>

![Haga clic en el encabezado de la cuadrícula y seleccione un nuevo tipo de gráfico](./media/app-insights-javascript/10-page-perf-area.png)

<span data-ttu-id="86873-180">**Segmentación mediante otras dimensiones.**</span><span class="sxs-lookup"><span data-stu-id="86873-180">**Segment by other dimensions.**</span></span> <span data-ttu-id="86873-181">¿Puede que las páginas sean más lentas a la hora de cargarse en un determinado explorador, sistema operativo del cliente o ubicación del usuario?</span><span class="sxs-lookup"><span data-stu-id="86873-181">Maybe your pages are slower to load on a particular browser, client OS, or user locality?</span></span> <span data-ttu-id="86873-182">Agregue un nuevo gráfico y experimente con la dimensión **Group-by** (Agrupar por).</span><span class="sxs-lookup"><span data-stu-id="86873-182">Add a new chart and experiment with the **Group-by** dimension.</span></span>

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a><span data-ttu-id="86873-183">Rendimiento AJAX</span><span class="sxs-lookup"><span data-stu-id="86873-183">AJAX Performance</span></span>
<span data-ttu-id="86873-184">Asegúrese de que las llamadas AJAX en sus páginas web funcionan correctamente.</span><span class="sxs-lookup"><span data-stu-id="86873-184">Make sure any AJAX calls in your web pages are performing well.</span></span> <span data-ttu-id="86873-185">A menudo se utilizan para rellenar los elementos de la página de manera asincrónica.</span><span class="sxs-lookup"><span data-stu-id="86873-185">They are often used to fill parts of your page asynchronously.</span></span> <span data-ttu-id="86873-186">Aunque los elementos principales de la página se carguen rápidamente, los usuarios se frustran al ver elementos web en blanco, esperando hasta que los datos aparezcan.</span><span class="sxs-lookup"><span data-stu-id="86873-186">Although the overall page might load promptly, your users could be frustrated by staring at blank web parts, waiting for data to appear in them.</span></span>

<span data-ttu-id="86873-187">Las llamadas AJAX realizadas desde la página web aparecen en la hoja de exploradores como dependencias.</span><span class="sxs-lookup"><span data-stu-id="86873-187">AJAX calls made from your web page are shown on the Browsers blade as dependencies.</span></span>

<span data-ttu-id="86873-188">Hay gráficos de resumen en la parte superior de la hoja:</span><span class="sxs-lookup"><span data-stu-id="86873-188">There are summary charts in the upper part of the blade:</span></span>

![](./media/app-insights-javascript/31.png)

<span data-ttu-id="86873-189">y cuadrículas detalladas más abajo:</span><span class="sxs-lookup"><span data-stu-id="86873-189">and detailed grids lower down:</span></span>

![](./media/app-insights-javascript/33.png)

<span data-ttu-id="86873-190">Haga clic en cualquier fila para obtener detalles concretos.</span><span class="sxs-lookup"><span data-stu-id="86873-190">Click any row for specific details.</span></span>

> [!NOTE]
> <span data-ttu-id="86873-191">Si elimina el filtro Exploradores de la hoja, tanto el servidor como las dependencias AJAX se incluirán en estos gráficos.</span><span class="sxs-lookup"><span data-stu-id="86873-191">If you delete the Browsers filter on the blade, both server and AJAX dependencies are included in these charts.</span></span> <span data-ttu-id="86873-192">Haga clic en Restaurar valores predeterminados para volver a configurar el filtro.</span><span class="sxs-lookup"><span data-stu-id="86873-192">Click Restore Defaults to reconfigure the filter.</span></span>
> 
> 

<span data-ttu-id="86873-193">**Para profundizar en las llamadas Ajax con errores** , desplácese hacia abajo hasta la cuadrícula de errores de Dependencia y haga clic en cualquiera de las filas para ver las instancias concretas.</span><span class="sxs-lookup"><span data-stu-id="86873-193">**To drill into failed Ajax calls** scroll down to the Dependency failures grid, and then click a row to see specific instances.</span></span>

![](./media/app-insights-javascript/37.png)


<span data-ttu-id="86873-194">Haga clic en `...` para obtener la telemetría completa de una llamada Ajax.</span><span class="sxs-lookup"><span data-stu-id="86873-194">Click `...` for the full telemetry for an Ajax call.</span></span>

### <a name="no-ajax-calls-reported"></a><span data-ttu-id="86873-195">¿No se han notificado llamadas Ajax?</span><span class="sxs-lookup"><span data-stu-id="86873-195">No Ajax calls reported?</span></span>
<span data-ttu-id="86873-196">Las llamadas Ajax incluyen todas las llamadas HTTP/HTTPS realizadas desde el script de una página web.</span><span class="sxs-lookup"><span data-stu-id="86873-196">Ajax calls include any HTTP/HTTPS  calls made from the script of your web page.</span></span> <span data-ttu-id="86873-197">Si no se han notificado, compruebe que el fragmento de código no establece los [parámetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableAjaxTracking` o `maxAjaxCallsPerView`.</span><span class="sxs-lookup"><span data-stu-id="86873-197">If you don't see them reported, check that the code snippet doesn't set the `disableAjaxTracking` or `maxAjaxCallsPerView` [parameters](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="86873-198">Excepciones de explorador</span><span class="sxs-lookup"><span data-stu-id="86873-198">Browser exceptions</span></span>
<span data-ttu-id="86873-199">En la hoja de exploradores, hay un gráfico de resumen de excepciones y una cuadrícula de tipos de excepción más abajo en la hoja.</span><span class="sxs-lookup"><span data-stu-id="86873-199">On the Browsers blade, there's an exceptions summary chart, and a grid of exception types further down the blade.</span></span>

![](./media/app-insights-javascript/39.png)

<span data-ttu-id="86873-200">Si no ve que se hayan notificado las excepciones del explorador, compruebe que el fragmento de código no establezca el [parámetro](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) `disableExceptionTracking`.</span><span class="sxs-lookup"><span data-stu-id="86873-200">If you don't see browser exceptions reported, check that the code snippet doesn't set the `disableExceptionTracking` [parameter](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).</span></span>

## <a name="inspect-individual-page-view-events"></a><span data-ttu-id="86873-201">Inspección de eventos de vista de página individuales</span><span class="sxs-lookup"><span data-stu-id="86873-201">Inspect individual page view events</span></span>

<span data-ttu-id="86873-202">Por lo general, Application Insights analiza la telemetría de vista de página y usted solo verá informes acumulativos, cuya media se ha calculado en función de todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="86873-202">Usually page view telemetry is analyzed by Application Insights and you see only cumulative reports, averaged over all your users.</span></span> <span data-ttu-id="86873-203">Pero a efectos de depuración, también puede ver eventos de vista de página individuales.</span><span class="sxs-lookup"><span data-stu-id="86873-203">But for debugging purposes, you can also look at individual page view events.</span></span>

<span data-ttu-id="86873-204">En la hoja Búsqueda de diagnóstico, establezca Filtros en Vista de página.</span><span class="sxs-lookup"><span data-stu-id="86873-204">In the Diagnostic Search blade, set Filters to Page View.</span></span>

![](./media/app-insights-javascript/12-search-pages.png)

<span data-ttu-id="86873-205">Seleccione el evento que desea ver con mayor detalle.</span><span class="sxs-lookup"><span data-stu-id="86873-205">Select any event to see more detail.</span></span> <span data-ttu-id="86873-206">En la página de detalles, haga clic en "..." para ver aún más detalles.</span><span class="sxs-lookup"><span data-stu-id="86873-206">In the details page, click "..." to see even more detail.</span></span>

> [!NOTE]
> <span data-ttu-id="86873-207">Si usa [Buscar](app-insights-diagnostic-search.md), tenga en cuenta que tiene que hacer coincidir palabras completas: "Acerc" y "cerca de" no coinciden con "Acerca de".</span><span class="sxs-lookup"><span data-stu-id="86873-207">If you use [Search](app-insights-diagnostic-search.md), notice that you have to match whole words: "Abou" and "bout" do not match "About".</span></span>
> 
> 

<span data-ttu-id="86873-208">También puede usar el potente [lenguaje de consulta de Log Analytics](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) para buscar vistas de página.</span><span class="sxs-lookup"><span data-stu-id="86873-208">You can also use the powerful [Log Analytics query language](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) to search page views.</span></span>

### <a name="page-view-properties"></a><span data-ttu-id="86873-209">Propiedades de la vista de página</span><span class="sxs-lookup"><span data-stu-id="86873-209">Page view properties</span></span>
* <span data-ttu-id="86873-210">**Duración de vista de página**</span><span class="sxs-lookup"><span data-stu-id="86873-210">**Page view duration**</span></span> 
  
  * <span data-ttu-id="86873-211">De forma predeterminada, el tiempo necesario para cargar la página, desde la solicitud del cliente hasta la carga completa (incluidos los archivos auxiliares, aunque no las tareas asincrónicas, como las llamadas de Ajax).</span><span class="sxs-lookup"><span data-stu-id="86873-211">By default, the time it takes to load the page, from client request to full load (including auxiliary files but excluding asynchronous tasks such as Ajax calls).</span></span> 
  * <span data-ttu-id="86873-212">Si establece `overridePageViewDuration` en la [configuración de la página](#detailed-configuration), el intervalo entre la solicitud del cliente y la ejecución del primer `trackPageView`.</span><span class="sxs-lookup"><span data-stu-id="86873-212">If you set `overridePageViewDuration` in the [page configuration](#detailed-configuration), the interval between client request to execution of the first `trackPageView`.</span></span> <span data-ttu-id="86873-213">Si mueve trackPageView desde su posición habitual después de la inicialización del script, reflejará un valor diferente.</span><span class="sxs-lookup"><span data-stu-id="86873-213">If you moved trackPageView from its usual position after the initialization of the script, it will reflect a different value.</span></span>
  * <span data-ttu-id="86873-214">Si se ha establecido `overridePageViewDuration` y se proporciona un argumento de duración en la llamada a `trackPageView()`, se usará el valor del argumento.</span><span class="sxs-lookup"><span data-stu-id="86873-214">If `overridePageViewDuration` is set and a duration argument is provided in the `trackPageView()` call, then the argument value is used instead.</span></span> 

## <a name="custom-page-counts"></a><span data-ttu-id="86873-215">Recuentos de página personalizados</span><span class="sxs-lookup"><span data-stu-id="86873-215">Custom page counts</span></span>
<span data-ttu-id="86873-216">De forma predeterminada, se realiza un recuento de página cada vez que se carga una página nueva en el explorador del cliente.</span><span class="sxs-lookup"><span data-stu-id="86873-216">By default, a page count occurs each time a new page loads into the client browser.</span></span>  <span data-ttu-id="86873-217">Sin embargo, tal vez quiera realizar un recuento de otras vistas de página.</span><span class="sxs-lookup"><span data-stu-id="86873-217">But you might want to count additional page views.</span></span> <span data-ttu-id="86873-218">Por ejemplo, una página puede mostrar su contenido en pestañas y a usted puede interesarle realizar el recuento de una página cuando el usuario cambia de pestaña.</span><span class="sxs-lookup"><span data-stu-id="86873-218">For example, a page might display its content in tabs and you want to count a page when the user switches tabs.</span></span> <span data-ttu-id="86873-219">O el código JavaScript de la página puede cargar contenido nuevo sin cambiar la URL del explorador.</span><span class="sxs-lookup"><span data-stu-id="86873-219">Or JavaScript code in the page might load new content without changing the browser's URL.</span></span>

<span data-ttu-id="86873-220">Inserte una llamada de JavaScript como esta en el lugar adecuado del código de cliente:</span><span class="sxs-lookup"><span data-stu-id="86873-220">Insert a JavaScript call like this at the appropriate point in your client code:</span></span>

    appInsights.trackPageView(myPageName);

<span data-ttu-id="86873-221">El nombre de la página puede contener los mismos caracteres que una dirección URL, aunque se ignorará todo aquello que haya después de "#" o "?".</span><span class="sxs-lookup"><span data-stu-id="86873-221">The page name can contain the same characters as a URL, but anything after "#" or "?" is ignored.</span></span>

## <a name="usage-tracking"></a><span data-ttu-id="86873-222">Seguimiento de uso</span><span class="sxs-lookup"><span data-stu-id="86873-222">Usage tracking</span></span>
<span data-ttu-id="86873-223">¿Desea averiguar qué hacen los usuarios con su aplicación?</span><span class="sxs-lookup"><span data-stu-id="86873-223">Want to find out what your users do with your app?</span></span>

* [<span data-ttu-id="86873-224">Obtenga información sobre el seguimiento de uso</span><span class="sxs-lookup"><span data-stu-id="86873-224">Learn about usage tracking</span></span>](app-insights-web-track-usage.md)
* <span data-ttu-id="86873-225">[Más información sobre las API para eventos y métricas personalizados](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="86873-225">[Learn about custom events and metrics API](app-insights-api-custom-events-metrics.md).</span></span>

## <span data-ttu-id="86873-226"><a name="video"></a> Vídeo</span><span class="sxs-lookup"><span data-stu-id="86873-226"><a name="video"></a> Video</span></span>


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <span data-ttu-id="86873-227"><a name="next"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="86873-227"><a name="next"></a> Next steps</span></span>
* [<span data-ttu-id="86873-228">Seguir el uso</span><span class="sxs-lookup"><span data-stu-id="86873-228">Track usage</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="86873-229">Eventos y métricas personalizados</span><span class="sxs-lookup"><span data-stu-id="86873-229">Custom events and metrics</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="86873-230">Compilación - Métrica - Aprendizaje</span><span class="sxs-lookup"><span data-stu-id="86873-230">Build-measure-learn</span></span>](app-insights-web-track-usage.md)

