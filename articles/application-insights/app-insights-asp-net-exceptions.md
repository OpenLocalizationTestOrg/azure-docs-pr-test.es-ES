---
title: "Diagnóstico de errores y excepciones en aplicaciones web con Azure Application Insights | Microsoft Docs"
description: "Capture las excepciones de las aplicaciones ASP.NET junto con la telemetría de solicitudes."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 7eeacdc6677ccdebb1653e94a163ecb47090b7ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="642b3-103">Diagnóstico de excepciones en aplicaciones web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="642b3-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="642b3-104">Las excepciones en la aplicación web en directo se notifican mediante [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="642b3-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="642b3-105">Puede correlacionar las solicitudes con error con excepciones y otros eventos en el cliente y en el servidor, de modo que pueda diagnosticar rápidamente las causas.</span><span class="sxs-lookup"><span data-stu-id="642b3-105">You can correlate failed requests with exceptions and other events at both the client and server, so that you can quickly diagnose the causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="642b3-106">Configuración de informes de excepciones</span><span class="sxs-lookup"><span data-stu-id="642b3-106">Set up exception reporting</span></span>
* <span data-ttu-id="642b3-107">Para que se notifiquen excepciones desde su aplicación de servidor:</span><span class="sxs-lookup"><span data-stu-id="642b3-107">To have exceptions reported from your server app:</span></span>
  * <span data-ttu-id="642b3-108">Instale el [SDK de Application Insights](app-insights-asp-net.md) en su código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="642b3-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="642b3-109">Servidores web de IIS: ejecute el [agente de Application Insights](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="642b3-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="642b3-110">Aplicaciones web de Azure: agregue la [extensión de Application Insights](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="642b3-110">Azure web apps: Add the [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="642b3-111">Aplicaciones web de Java: instale el [agente de Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="642b3-111">Java web apps: Install the [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="642b3-112">Instale el [fragmento de código de JavaScript](app-insights-javascript.md) en las páginas web para capturar las excepciones del explorador.</span><span class="sxs-lookup"><span data-stu-id="642b3-112">Install the [JavaScript snippet](app-insights-javascript.md) in your web pages to catch browser exceptions.</span></span>
* <span data-ttu-id="642b3-113">En algunos marcos de aplicaciones o con algunas opciones de configuración, debe realizar algunos pasos adicionales para capturar más excepciones:</span><span class="sxs-lookup"><span data-stu-id="642b3-113">In some application frameworks or with some settings, you need to take some extra steps to catch more exceptions:</span></span>
  * [<span data-ttu-id="642b3-114">Formularios web</span><span class="sxs-lookup"><span data-stu-id="642b3-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="642b3-115">MVC</span><span class="sxs-lookup"><span data-stu-id="642b3-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="642b3-116">API web 1.*</span><span class="sxs-lookup"><span data-stu-id="642b3-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="642b3-117">API web 2.*</span><span class="sxs-lookup"><span data-stu-id="642b3-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="642b3-118">WCF</span><span class="sxs-lookup"><span data-stu-id="642b3-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="642b3-119">Diagnóstico de excepciones mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="642b3-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="642b3-120">Abra la solución de aplicación en Visual Studio para ayudar con la depuración.</span><span class="sxs-lookup"><span data-stu-id="642b3-120">Open the app solution in Visual Studio to help with debugging.</span></span>

<span data-ttu-id="642b3-121">Ejecute la aplicación, bien en el servidor o en el equipo de desarrollo mediante F5.</span><span class="sxs-lookup"><span data-stu-id="642b3-121">Run the app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="642b3-122">Abra la ventana Búsqueda de Application Insights en Visual Studio y configúrela para mostrar los eventos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="642b3-122">Open the Application Insights Search window in Visual Studio, and set it to display events from your app.</span></span> <span data-ttu-id="642b3-123">Durante la depuración, puede hacer esto haciendo clic simplemente en el botón de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="642b3-123">While you're debugging, you can do this just by clicking the Application Insights button.</span></span>

![Haga clic con el botón derecho en el proyecto y seleccione Application Insights, Abrir.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="642b3-125">Observe que puede filtrar el informe para mostrar solo excepciones.</span><span class="sxs-lookup"><span data-stu-id="642b3-125">Notice that you can filter the report to show just exceptions.</span></span>

<span data-ttu-id="642b3-126">*¿No se muestra ninguna excepción? Consulte [Captura de excepciones](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="642b3-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="642b3-127">Haga clic en un informe de excepciones para mostrar su seguimiento de la pila.</span><span class="sxs-lookup"><span data-stu-id="642b3-127">Click an exception report to show its stack trace.</span></span>
<span data-ttu-id="642b3-128">Haga clic en una referencia de línea en el seguimiento de la pila para abrir el archivo de código pertinente.</span><span class="sxs-lookup"><span data-stu-id="642b3-128">Click a line reference in the stack trace, to open the relevant code file.</span></span>  

<span data-ttu-id="642b3-129">En el código, tenga en cuenta que CodeLens muestra datos de las excepciones:</span><span class="sxs-lookup"><span data-stu-id="642b3-129">In the code, notice that CodeLens shows data about the exceptions:</span></span>

![Notificación de CodeLens de excepciones.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-the-azure-portal"></a><span data-ttu-id="642b3-131">Diagnóstico de errores mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="642b3-131">Diagnosing failures using the Azure portal</span></span>
<span data-ttu-id="642b3-132">En la hoja de información general de Application Insights de su aplicación, el icono Errores muestra los gráficos de excepciones y las solicitudes HTTP con error, junto con una lista de las direcciones URL de solicitudes que provocan los errores más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="642b3-132">From the Application Insights overview of your app, the Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of the request URLs that cause the most frequent failures.</span></span>

![Selección de Configuración, Errores](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="642b3-134">Haga clic en uno de los tipos de excepción con error en la lista para obtener las repeticiones individuales de la excepción, donde puede ver los detalles y el seguimiento de la pila:</span><span class="sxs-lookup"><span data-stu-id="642b3-134">Click through one of the failed exception types in the list to get to individual occurrences of the exception, where you can see the details and stack trace:</span></span>

![Seleccione una instancia de una solicitud con error y, en los detalles de la excepción, obtenga las instancias de la excepción.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="642b3-136">**También** puede hacerlo desde la lista de solicitudes y buscar excepciones relacionadas.</span><span class="sxs-lookup"><span data-stu-id="642b3-136">**Alternatively,** you can start from the list of requests and find exceptions related to it.</span></span>

<span data-ttu-id="642b3-137">*¿No se muestra ninguna excepción? Consulte [Captura de excepciones](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="642b3-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="642b3-138">Personalización del seguimiento y del registro de datos</span><span class="sxs-lookup"><span data-stu-id="642b3-138">Custom tracing and log data</span></span>
<span data-ttu-id="642b3-139">Para obtener datos de diagnóstico específicos de su aplicación, puede insertar código para enviar sus propios datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="642b3-139">To get diagnostic data specific to your app, you can insert code to send your own telemetry data.</span></span> <span data-ttu-id="642b3-140">Esto aparece en la búsqueda de diagnóstico junto con la solicitud, vista de página y otros datos que se recopilan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="642b3-140">This displayed in diagnostic search alongside the request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="642b3-141">Tiene varias opciones:</span><span class="sxs-lookup"><span data-stu-id="642b3-141">You have several options:</span></span>

* <span data-ttu-id="642b3-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) normalmente se usa para supervisar patrones de uso, pero los datos que envía también aparecen en Eventos personalizados en la búsqueda de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="642b3-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but the data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="642b3-143">Los eventos tienen nombre y pueden llevar propiedades de cadena y métricas numéricas en las que puede [filtrar las búsquedas de diagnósticos](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="642b3-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="642b3-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) le permite enviar datos más grandes, como la información de POST.</span><span class="sxs-lookup"><span data-stu-id="642b3-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="642b3-145">[TrackException()](#exceptions) envía seguimientos de la pila.</span><span class="sxs-lookup"><span data-stu-id="642b3-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="642b3-146">[Más información sobre excepciones](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="642b3-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="642b3-147">Si ya usa un marco de registro como Log4Net o NLog, puede [capturar aquellos registros](app-insights-asp-net-trace-logs.md) y verlos en la búsqueda de diagnósticos junto con datos de solicitud y excepción.</span><span class="sxs-lookup"><span data-stu-id="642b3-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="642b3-148">Para ver estos eventos, abra [Buscar](app-insights-diagnostic-search.md), abra Filtrar y luego elija Evento personalizado, Seguimiento o Excepción.</span><span class="sxs-lookup"><span data-stu-id="642b3-148">To see these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Obtener detalles](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="642b3-150">Si la aplicación genera mucha telemetría, el módulo de muestreo adaptable reducirá automáticamente el volumen que se envía al portal mediante el envío de únicamente una fracción representativa de eventos.</span><span class="sxs-lookup"><span data-stu-id="642b3-150">If your app generates a lot of telemetry, the adaptive sampling module will automatically reduce the volume that is sent to the portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="642b3-151">Los eventos que forman parte de la misma operación se seleccionarán o se anulará su selección como grupo, por lo que puede navegar entre los eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="642b3-151">Events that are part of the same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="642b3-152">Más información sobre el muestreo.</span><span class="sxs-lookup"><span data-stu-id="642b3-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-to-see-request-post-data"></a><span data-ttu-id="642b3-153">Visualización de los datos de solicitud POST</span><span class="sxs-lookup"><span data-stu-id="642b3-153">How to see request POST data</span></span>
<span data-ttu-id="642b3-154">Los detalles de la solicitud no incluyen los datos enviados a la aplicación en una llamada a POST.</span><span class="sxs-lookup"><span data-stu-id="642b3-154">Request details don't include the data sent to your app in a POST call.</span></span> <span data-ttu-id="642b3-155">Para que se notifiquen estos datos:</span><span class="sxs-lookup"><span data-stu-id="642b3-155">To have this data reported:</span></span>

* <span data-ttu-id="642b3-156">[Instale el SDK](app-insights-asp-net.md) en su proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="642b3-156">[Install the SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="642b3-157">Inserte código en la aplicación para llamar a [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="642b3-157">Insert code in your application to call [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="642b3-158">Envíe los datos de POST en el parámetro de mensaje.</span><span class="sxs-lookup"><span data-stu-id="642b3-158">Send the POST data in the message parameter.</span></span> <span data-ttu-id="642b3-159">Hay un límite en cuanto al tamaño permitido, así que debe intentar enviar únicamente los datos fundamentales.</span><span class="sxs-lookup"><span data-stu-id="642b3-159">There is a limit to the permitted size, so you should try to send just the essential data.</span></span>
* <span data-ttu-id="642b3-160">Cuando investigue una solicitud con error, busque los seguimientos asociados.</span><span class="sxs-lookup"><span data-stu-id="642b3-160">When you investigate a failed request, find the associated traces.</span></span>  

![Obtener detalles](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="642b3-162"><a name="exceptions"></a> Captura de excepciones y datos de diagnóstico relacionados</span><span class="sxs-lookup"><span data-stu-id="642b3-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="642b3-163">En primer lugar, no verá en el portal todas las excepciones que provocan errores en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="642b3-163">At first, you won't see in the portal all the exceptions that cause failures in your app.</span></span> <span data-ttu-id="642b3-164">Verá las excepciones del explorador (si usa el [SDK de JavaScript](app-insights-javascript.md) en sus páginas web).</span><span class="sxs-lookup"><span data-stu-id="642b3-164">You'll see any browser exceptions (if you're using the [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="642b3-165">Pero la mayoría de las excepciones de servidor las detecta IIS y debe escribir algo de código para verlas.</span><span class="sxs-lookup"><span data-stu-id="642b3-165">But most server exceptions are caught by IIS and you have to write a bit of code to see them.</span></span>

<span data-ttu-id="642b3-166">Puede:</span><span class="sxs-lookup"><span data-stu-id="642b3-166">You can:</span></span>

* <span data-ttu-id="642b3-167">**Registrar excepciones explícitamente** insertando código en los controladores de excepciones para notificar las excepciones.</span><span class="sxs-lookup"><span data-stu-id="642b3-167">**Log exceptions explicitly** by inserting code in exception handlers to report the exceptions.</span></span>
* <span data-ttu-id="642b3-168">**Capturar excepciones automáticamente** configurando su marco de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="642b3-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="642b3-169">Las adiciones necesarias son diferentes para los distintos tipos de marco.</span><span class="sxs-lookup"><span data-stu-id="642b3-169">The necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="642b3-170">Notificación de excepciones explícitamente</span><span class="sxs-lookup"><span data-stu-id="642b3-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="642b3-171">La manera más sencilla consiste en insertar una llamada a TrackException() en un controlador de excepciones.</span><span class="sxs-lookup"><span data-stu-id="642b3-171">The simplest way is to insert a call to TrackException() in an exception handler.</span></span>

<span data-ttu-id="642b3-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="642b3-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="642b3-173">C#</span><span class="sxs-lookup"><span data-stu-id="642b3-173">C#</span></span>

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send the exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="642b3-174">VB</span><span class="sxs-lookup"><span data-stu-id="642b3-174">VB</span></span>

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send the exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="642b3-175">Los parámetros de las propiedades y las medidas son opcionales, pero son útiles para [filtrar y agregar información](app-insights-diagnostic-search.md) adicional.</span><span class="sxs-lookup"><span data-stu-id="642b3-175">The properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="642b3-176">Por ejemplo, si tiene una aplicación que se puede ejecutar varios juegos, podría buscar todos los informes de excepción relacionados con un juego en particular.</span><span class="sxs-lookup"><span data-stu-id="642b3-176">For example, if you have an app that can run several games, you could find all the exception reports related to a particular game.</span></span> <span data-ttu-id="642b3-177">Puede agregar tantos elementos como desee para cada diccionario.</span><span class="sxs-lookup"><span data-stu-id="642b3-177">You can add as many items as you like to each dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="642b3-178">Excepciones de explorador</span><span class="sxs-lookup"><span data-stu-id="642b3-178">Browser exceptions</span></span>
<span data-ttu-id="642b3-179">Se notifican la mayoría de las excepciones de explorador.</span><span class="sxs-lookup"><span data-stu-id="642b3-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="642b3-180">Si la página web incluye archivos de script de redes de entrega de contenido o de otros dominios, asegúrese de que la etiqueta de script tenga el atributo ```crossorigin="anonymous"```, y que el servidor envíe [encabezados CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="642b3-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has the attribute ```crossorigin="anonymous"```,  and that the server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="642b3-181">Esto le permitirá obtener un seguimiento de pila y los detalles de las excepciones no controladas de JavaScript de estos recursos.</span><span class="sxs-lookup"><span data-stu-id="642b3-181">This will allow you to get a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="642b3-182">Formularios web</span><span class="sxs-lookup"><span data-stu-id="642b3-182">Web forms</span></span>
<span data-ttu-id="642b3-183">Para los formularios web, el módulo HTTP podrá recopilar las excepciones cuando no haya ningún redireccionamiento configurado con CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="642b3-183">For web forms, the HTTP Module will be able to collect the exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="642b3-184">Pero si tiene redireccionamientos activos, agregue las siguientes líneas a la función Application_Error en Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="642b3-184">But if you have active redirects, add the following lines to the Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="642b3-185">(Agregue un archivo Global.asax si aún no tiene uno.)</span><span class="sxs-lookup"><span data-stu-id="642b3-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="642b3-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="642b3-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="642b3-187">MVC</span><span class="sxs-lookup"><span data-stu-id="642b3-187">MVC</span></span>
<span data-ttu-id="642b3-188">Si la configuración de [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) es `Off`, entonces habrá excepciones disponibles para que las recopile el [módulo HTTP](https://msdn.microsoft.com/library/ms178468.aspx).</span><span class="sxs-lookup"><span data-stu-id="642b3-188">If the [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for the [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) to collect.</span></span> <span data-ttu-id="642b3-189">Sin embargo, si es `RemoteOnly` (valor predeterminado), o `On`, la excepción se desactivará y no estará disponible para que Application Insights la recopile automáticamente.</span><span class="sxs-lookup"><span data-stu-id="642b3-189">However, if it is `RemoteOnly` (default), or `On`, then the exception will be cleared and not available for Application Insights to automatically collect.</span></span> <span data-ttu-id="642b3-190">Para corregir este problema, invalide la [clase System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx) y aplique la clase invalidada como se muestra a continuación para las diferentes versiones de MVC ([origen de github](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="642b3-190">You can fix that by overriding the [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying the overridden class as shown for the different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report the exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a><span data-ttu-id="642b3-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="642b3-191">MVC 2</span></span>
<span data-ttu-id="642b3-192">Sustituya el atributo HandleError por el nuevo atributo en los controladores.</span><span class="sxs-lookup"><span data-stu-id="642b3-192">Replace the HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="642b3-193">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="642b3-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="642b3-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="642b3-194">MVC 3</span></span>
<span data-ttu-id="642b3-195">Registrar `AiHandleErrorAttribute` como filtro global de Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="642b3-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="642b3-196">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="642b3-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="642b3-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="642b3-197">MVC 4, MVC5</span></span>
<span data-ttu-id="642b3-198">Registrar AiHandleErrorAttribute como filtro global en FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="642b3-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with the override to track unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="642b3-199">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="642b3-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="642b3-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="642b3-200">Web API 1.x</span></span>
<span data-ttu-id="642b3-201">Invalidar System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="642b3-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

<span data-ttu-id="642b3-202">Podría agregar este atributo invalidado a controladores específicos o agregarlo a la configuración de filtros globales en la clase WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="642b3-202">You could add this overridden attribute to specific controllers, or add it to the global filter configuration in the WebApiConfig class:</span></span>

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[<span data-ttu-id="642b3-203">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="642b3-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="642b3-204">Hay un número de casos que los filtros de excepciones no pueden procesar.</span><span class="sxs-lookup"><span data-stu-id="642b3-204">There are a number of cases that the exception filters cannot handle.</span></span> <span data-ttu-id="642b3-205">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="642b3-205">For example:</span></span>

* <span data-ttu-id="642b3-206">Excepciones iniciadas por constructores del controlador.</span><span class="sxs-lookup"><span data-stu-id="642b3-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="642b3-207">Excepciones iniciadas por controladores de mensajes.</span><span class="sxs-lookup"><span data-stu-id="642b3-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="642b3-208">Excepciones iniciadas durante el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="642b3-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="642b3-209">Excepciones iniciadas durante la serialización del contenido de respuesta.</span><span class="sxs-lookup"><span data-stu-id="642b3-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="642b3-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="642b3-210">Web API 2.x</span></span>
<span data-ttu-id="642b3-211">Agregue una implementación de IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="642b3-211">Add an implementation of IExceptionLogger:</span></span>

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

<span data-ttu-id="642b3-212">Agregue lo siguiente a los servicios en WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="642b3-212">Add this to the services in WebApiConfig:</span></span>

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  <span data-ttu-id="642b3-213">}</span><span class="sxs-lookup"><span data-stu-id="642b3-213">}</span></span>

[<span data-ttu-id="642b3-214">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="642b3-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="642b3-215">Como alternativa, puede:</span><span class="sxs-lookup"><span data-stu-id="642b3-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="642b3-216">Sustituir el único ExceptionHandler por una implementación personalizada de IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="642b3-216">Replace the only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="642b3-217">Solo se llama a este controlador de excepciones cuando el marco es aún capaz de seleccionar el mensaje de respuesta que se enviará (no cuando se anula la conexión, por ejemplo)</span><span class="sxs-lookup"><span data-stu-id="642b3-217">This is only called when the framework is still able to choose which response message to send (not when the connection is aborted for instance)</span></span>
2. <span data-ttu-id="642b3-218">Los filtros de excepciones (como se describe en la sección sobre controladores de Web API 1.x anteriores) no se llaman en todos los casos.</span><span class="sxs-lookup"><span data-stu-id="642b3-218">Exception Filters (as described in the section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="642b3-219">WCF</span><span class="sxs-lookup"><span data-stu-id="642b3-219">WCF</span></span>
<span data-ttu-id="642b3-220">Agregue una clase que extienda el atributo y que implemente IErrorHandler y IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="642b3-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

<span data-ttu-id="642b3-221">Agregue el atributo a las implementaciones de servicio:</span><span class="sxs-lookup"><span data-stu-id="642b3-221">Add the attribute to the service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="642b3-222">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="642b3-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="642b3-223">Contadores de rendimiento de excepciones</span><span class="sxs-lookup"><span data-stu-id="642b3-223">Exception performance counters</span></span>
<span data-ttu-id="642b3-224">Si tiene [instalado el agente de Application Insights](app-insights-monitor-performance-live-website-now.md) en el servidor, puede obtener un gráfico de la tasa de excepciones, medida por .NET.</span><span class="sxs-lookup"><span data-stu-id="642b3-224">If you have [installed the Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of the exceptions rate, measured by .NET.</span></span> <span data-ttu-id="642b3-225">Esto incluye las excepciones de .NET, tanto controladas como no controladas.</span><span class="sxs-lookup"><span data-stu-id="642b3-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="642b3-226">Abra una hoja del Explorador de métricas, agregue un nuevo gráfico y seleccione **Tasa de excepciones**, que aparece debajo de Contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="642b3-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="642b3-227">.NET framework calcula la tasa contando el número de excepciones producidas en un intervalo y dividiéndolo por la duración del intervalo de tiempo.</span><span class="sxs-lookup"><span data-stu-id="642b3-227">The .NET framework calculates the rate by counting the number of exceptions in an interval and dividing by the length of the interval.</span></span>

<span data-ttu-id="642b3-228">Tenga en cuenta que será diferente del recuento de "Excepciones" calculado por el portal de Application Insights contando los informes de TrackException.</span><span class="sxs-lookup"><span data-stu-id="642b3-228">Note that it will be different from the 'Exceptions' count calculated by the Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="642b3-229">Los intervalos de muestreo son diferentes y el SDK no envía informes de TrackException para todas las excepciones, controladas y no controladas.</span><span class="sxs-lookup"><span data-stu-id="642b3-229">The sampling intervals are different, and the SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="642b3-230">Vídeo</span><span class="sxs-lookup"><span data-stu-id="642b3-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="642b3-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="642b3-231">Next steps</span></span>
* [<span data-ttu-id="642b3-232">Supervisar REST, SQL y otras llamadas a las dependencias</span><span class="sxs-lookup"><span data-stu-id="642b3-232">Monitor REST, SQL and other calls to dependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="642b3-233">Supervisar los tiempos de carga de página, las excepciones del explorador y las llamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="642b3-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="642b3-234">Supervisar los contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="642b3-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
