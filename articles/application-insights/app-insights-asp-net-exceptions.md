---
title: aaaDiagnose errores y excepciones en aplicaciones con Azure Application Insights de web | Documentos de Microsoft
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
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a><span data-ttu-id="6d7ff-103">Diagnóstico de excepciones en aplicaciones web con Application Insights</span><span class="sxs-lookup"><span data-stu-id="6d7ff-103">Diagnose exceptions in your web apps with Application Insights</span></span>
<span data-ttu-id="6d7ff-104">Las excepciones en la aplicación web en directo se notifican mediante [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d7ff-104">Exceptions in your live web app are reported by [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="6d7ff-105">Puede correlacionar las solicitudes erróneas con excepciones y otros eventos en el cliente de Hola y el servidor, por lo que puede diagnosticar rápidamente Hola causas.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-105">You can correlate failed requests with exceptions and other events at both hello client and server, so that you can quickly diagnose hello causes.</span></span>

## <a name="set-up-exception-reporting"></a><span data-ttu-id="6d7ff-106">Configuración de informes de excepciones</span><span class="sxs-lookup"><span data-stu-id="6d7ff-106">Set up exception reporting</span></span>
* <span data-ttu-id="6d7ff-107">excepciones de toohave desde la aplicación de servidor:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-107">toohave exceptions reported from your server app:</span></span>
  * <span data-ttu-id="6d7ff-108">Instale el [SDK de Application Insights](app-insights-asp-net.md) en su código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-108">Install [Application Insights SDK](app-insights-asp-net.md) in your app code, or</span></span>
  * <span data-ttu-id="6d7ff-109">Servidores web de IIS: ejecute el [agente de Application Insights](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="6d7ff-109">IIS web servers: Run [Application Insights Agent](app-insights-monitor-performance-live-website-now.md); or</span></span>
  * <span data-ttu-id="6d7ff-110">Aplicaciones web de Azure: agregar hello [extensión de visión de la aplicación](app-insights-azure-web-apps.md)</span><span class="sxs-lookup"><span data-stu-id="6d7ff-110">Azure web apps: Add hello [Application Insights Extension](app-insights-azure-web-apps.md)</span></span>
  * <span data-ttu-id="6d7ff-111">Aplicaciones web de Java: Hola Install [agente Java](app-insights-java-agent.md)</span><span class="sxs-lookup"><span data-stu-id="6d7ff-111">Java web apps: Install hello [Java agent](app-insights-java-agent.md)</span></span>
* <span data-ttu-id="6d7ff-112">Instalar hello [fragmento de código de JavaScript](app-insights-javascript.md) en sus excepciones de explorador toocatch de páginas web.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-112">Install hello [JavaScript snippet](app-insights-javascript.md) in your web pages toocatch browser exceptions.</span></span>
* <span data-ttu-id="6d7ff-113">En algunos marcos de aplicaciones o con algunas opciones de configuración, deberá tootake algunos pasos adicionales toocatch más excepciones:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-113">In some application frameworks or with some settings, you need tootake some extra steps toocatch more exceptions:</span></span>
  * [<span data-ttu-id="6d7ff-114">Formularios web</span><span class="sxs-lookup"><span data-stu-id="6d7ff-114">Web forms</span></span>](#web-forms)
  * [<span data-ttu-id="6d7ff-115">MVC</span><span class="sxs-lookup"><span data-stu-id="6d7ff-115">MVC</span></span>](#mvc)
  * [<span data-ttu-id="6d7ff-116">API web 1.*</span><span class="sxs-lookup"><span data-stu-id="6d7ff-116">Web API 1.*</span></span>](#web-api-1)
  * [<span data-ttu-id="6d7ff-117">API web 2.*</span><span class="sxs-lookup"><span data-stu-id="6d7ff-117">Web API 2.*</span></span>](#web-api-2)
  * [<span data-ttu-id="6d7ff-118">WCF</span><span class="sxs-lookup"><span data-stu-id="6d7ff-118">WCF</span></span>](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a><span data-ttu-id="6d7ff-119">Diagnóstico de excepciones mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6d7ff-119">Diagnosing exceptions using Visual Studio</span></span>
<span data-ttu-id="6d7ff-120">Abra la solución de aplicación de hello en toohelp de Visual Studio con la depuración.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-120">Open hello app solution in Visual Studio toohelp with debugging.</span></span>

<span data-ttu-id="6d7ff-121">Ejecute la aplicación hello, ya sea en el servidor o en el equipo de desarrollo utilizando F5.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-121">Run hello app, either on your server or on your development machine by using F5.</span></span>

<span data-ttu-id="6d7ff-122">Abra la ventana de búsqueda de visión de la aplicación hello en Visual Studio y establézcalo toodisplay eventos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-122">Open hello Application Insights Search window in Visual Studio, and set it toodisplay events from your app.</span></span> <span data-ttu-id="6d7ff-123">Durante la depuración, puede hacerlo haciendo clic en el botón de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-123">While you're debugging, you can do this just by clicking hello Application Insights button.</span></span>

![Haga clic en proyecto de Hola y elija Application Insights, abrir.](./media/app-insights-asp-net-exceptions/34.png)

<span data-ttu-id="6d7ff-125">Tenga en cuenta que se pueden filtrar solo las excepciones Hola informe tooshow.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-125">Notice that you can filter hello report tooshow just exceptions.</span></span>

<span data-ttu-id="6d7ff-126">*¿No se muestra ninguna excepción? Consulte [Captura de excepciones](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="6d7ff-126">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>

<span data-ttu-id="6d7ff-127">Haga clic en un tooshow de informes de excepción su seguimiento de la pila.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-127">Click an exception report tooshow its stack trace.</span></span>
<span data-ttu-id="6d7ff-128">Haga clic en una referencia de la línea de seguimiento de la pila de hello, archivo de código relevante de hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-128">Click a line reference in hello stack trace, tooopen hello relevant code file.</span></span>  

<span data-ttu-id="6d7ff-129">En el código de hello, tenga en cuenta que CodeLens muestra datos sobre las excepciones de hello:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-129">In hello code, notice that CodeLens shows data about hello exceptions:</span></span>

![Notificación de CodeLens de excepciones.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a><span data-ttu-id="6d7ff-131">Diagnosticar errores mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6d7ff-131">Diagnosing failures using hello Azure portal</span></span>
<span data-ttu-id="6d7ff-132">De información general de Application Insights hello de la aplicación, iconos de errores de hello muestran los gráficos de excepciones y errores de solicitud HTTP, junto con una lista de hello solicitar direcciones URL que dar lugar a errores más frecuentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-132">From hello Application Insights overview of your app, hello Failures tile shows you charts of exceptions and failed HTTP requests, together with a list of hello request URLs that cause hello most frequent failures.</span></span>

![Selección de Configuración, Errores](./media/app-insights-asp-net-exceptions/012-start.png)

<span data-ttu-id="6d7ff-134">Haga clic en a través de uno de hello no se pudo tipos de excepciones en las repeticiones de hello lista tooget tooindividual de excepción de hello, donde puede ver los detalles de Hola y seguimiento de pila:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-134">Click through one of hello failed exception types in hello list tooget tooindividual occurrences of hello exception, where you can see hello details and stack trace:</span></span>

![Seleccione una instancia de una solicitud con error y en detalles de la excepción, obtener tooinstances de excepción de Hola.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

<span data-ttu-id="6d7ff-136">**O bien,** puede iniciar desde la lista de Hola de solicitudes y buscar excepciones relacionadas tooit.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-136">**Alternatively,** you can start from hello list of requests and find exceptions related tooit.</span></span>

<span data-ttu-id="6d7ff-137">*¿No se muestra ninguna excepción? Consulte [Captura de excepciones](#exceptions).*</span><span class="sxs-lookup"><span data-stu-id="6d7ff-137">*No exceptions showing? See [Capture exceptions](#exceptions).*</span></span>


## <a name="custom-tracing-and-log-data"></a><span data-ttu-id="6d7ff-138">Personalización del seguimiento y del registro de datos</span><span class="sxs-lookup"><span data-stu-id="6d7ff-138">Custom tracing and log data</span></span>
<span data-ttu-id="6d7ff-139">aplicación de tooyour específico de datos de diagnóstico de tooget, puede insertar código toosend sus propios datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-139">tooget diagnostic data specific tooyour app, you can insert code toosend your own telemetry data.</span></span> <span data-ttu-id="6d7ff-140">Esto se muestra en la búsqueda de diagnóstico junto con la solicitud de hello, vista de página y otros datos recopilados automáticamente.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-140">This displayed in diagnostic search alongside hello request, page view and other automatically-collected data.</span></span>

<span data-ttu-id="6d7ff-141">Tiene varias opciones:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-141">You have several options:</span></span>

* <span data-ttu-id="6d7ff-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) normalmente se usa para supervisar patrones de uso, pero Hola datos envía también aparecen en eventos personalizados en la búsqueda de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-142">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) is typically used for monitoring usage patterns, but hello data it sends also appears under Custom Events in diagnostic search.</span></span> <span data-ttu-id="6d7ff-143">Los eventos tienen nombre y pueden llevar propiedades de cadena y métricas numéricas en las que puede [filtrar las búsquedas de diagnósticos](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="6d7ff-143">Events are named, and can carry string properties and numeric metrics on which you can [filter your diagnostic searches](app-insights-diagnostic-search.md).</span></span>
* <span data-ttu-id="6d7ff-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) le permite enviar datos más grandes, como la información de POST.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-144">[TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) lets you send longer data such as POST information.</span></span>
* <span data-ttu-id="6d7ff-145">[TrackException()](#exceptions) envía seguimientos de la pila.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-145">[TrackException()](#exceptions) sends stack traces.</span></span> <span data-ttu-id="6d7ff-146">[Más información sobre excepciones](#exceptions).</span><span class="sxs-lookup"><span data-stu-id="6d7ff-146">[More about exceptions](#exceptions).</span></span>
* <span data-ttu-id="6d7ff-147">Si ya usa un marco de registro como Log4Net o NLog, puede [capturar aquellos registros](app-insights-asp-net-trace-logs.md) y verlos en la búsqueda de diagnósticos junto con datos de solicitud y excepción.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-147">If you already use a logging framework like Log4Net or NLog, you can [capture those logs](app-insights-asp-net-trace-logs.md) and see them in diagnostic search alongside request and exception data.</span></span>

<span data-ttu-id="6d7ff-148">estos eventos, abra a toosee [búsqueda](app-insights-diagnostic-search.md), Abrir filtro y, a continuación, elija Custom Event, seguimiento o excepción.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-148">toosee these events, open [Search](app-insights-diagnostic-search.md), open Filter, and then choose Custom Event, Trace, or Exception.</span></span>

![Obtener detalles](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> <span data-ttu-id="6d7ff-150">Si la aplicación genera una gran cantidad de telemetría, módulo de muestreo adaptativo de Hola reducirá automáticamente volumen Hola que se envía toohello portal enviando sólo una fracción representativa de eventos.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-150">If your app generates a lot of telemetry, hello adaptive sampling module will automatically reduce hello volume that is sent toohello portal by sending only a representative fraction of events.</span></span> <span data-ttu-id="6d7ff-151">Eventos que forman parte de hello misma operación se selecciona o anula la selección como un grupo, por lo que puede desplazarse entre los eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-151">Events that are part of hello same operation will be selected or deselected as a group, so that you can navigate between related events.</span></span> [<span data-ttu-id="6d7ff-152">Más información sobre el muestreo.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-152">Learn about sampling.</span></span>](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a><span data-ttu-id="6d7ff-153">¿Cómo toosee solicitar datos POST</span><span class="sxs-lookup"><span data-stu-id="6d7ff-153">How toosee request POST data</span></span>
<span data-ttu-id="6d7ff-154">Detalles de la solicitud no incluyen datos de hello enviados tooyour aplicación en una llamada a POST.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-154">Request details don't include hello data sent tooyour app in a POST call.</span></span> <span data-ttu-id="6d7ff-155">toohave notifican estos datos:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-155">toohave this data reported:</span></span>

* <span data-ttu-id="6d7ff-156">[Instalar SDK de hello](app-insights-asp-net.md) en el proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-156">[Install hello SDK](app-insights-asp-net.md) in your application project.</span></span>
* <span data-ttu-id="6d7ff-157">Inserte código en su aplicación toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span><span class="sxs-lookup"><span data-stu-id="6d7ff-157">Insert code in your application toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace).</span></span> <span data-ttu-id="6d7ff-158">Enviar datos POST de hello en el parámetro de mensaje de Hola.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-158">Send hello POST data in hello message parameter.</span></span> <span data-ttu-id="6d7ff-159">Hay un toohello permitida limitar el tamaño, por lo que debe intentar datos esenciales de toosend simplemente Hola.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-159">There is a limit toohello permitted size, so you should try toosend just hello essential data.</span></span>
* <span data-ttu-id="6d7ff-160">Cuando se investiga un solicitudes con error, encuentre ningún rastro de hello asociado.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-160">When you investigate a failed request, find hello associated traces.</span></span>  

![Obtener detalles](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <span data-ttu-id="6d7ff-162"><a name="exceptions"></a> Captura de excepciones y datos de diagnóstico relacionados</span><span class="sxs-lookup"><span data-stu-id="6d7ff-162"><a name="exceptions"></a> Capturing exceptions and related diagnostic data</span></span>
<span data-ttu-id="6d7ff-163">En primer lugar, no se mostrará en el portal de hello todas las excepciones de Hola que dar lugar a errores en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-163">At first, you won't see in hello portal all hello exceptions that cause failures in your app.</span></span> <span data-ttu-id="6d7ff-164">Podrá ver las excepciones de explorador (si usa hello [SDK de JavaScript](app-insights-javascript.md) en las páginas web).</span><span class="sxs-lookup"><span data-stu-id="6d7ff-164">You'll see any browser exceptions (if you're using hello [JavaScript SDK](app-insights-javascript.md) in your web pages).</span></span> <span data-ttu-id="6d7ff-165">Pero la mayoría de las excepciones de servidor capturada por IIS y tiene un poco de código toosee toowrite ellos.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-165">But most server exceptions are caught by IIS and you have toowrite a bit of code toosee them.</span></span>

<span data-ttu-id="6d7ff-166">Puede:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-166">You can:</span></span>

* <span data-ttu-id="6d7ff-167">**Registrar excepciones explícitamente** mediante la inserción de código en las excepciones Hola de tooreport de controladores de excepción.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-167">**Log exceptions explicitly** by inserting code in exception handlers tooreport hello exceptions.</span></span>
* <span data-ttu-id="6d7ff-168">**Capturar excepciones automáticamente** configurando su marco de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-168">**Capture exceptions automatically** by configuring your ASP.NET framework.</span></span> <span data-ttu-id="6d7ff-169">adiciones necesarias Hola son diferentes para distintos tipos de framework.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-169">hello necessary additions are different for different types of framework.</span></span>

## <a name="reporting-exceptions-explicitly"></a><span data-ttu-id="6d7ff-170">Notificación de excepciones explícitamente</span><span class="sxs-lookup"><span data-stu-id="6d7ff-170">Reporting exceptions explicitly</span></span>
<span data-ttu-id="6d7ff-171">Hello forma más sencilla es tooinsert un tooTrackException() de llamada en un controlador de excepciones.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-171">hello simplest way is tooinsert a call tooTrackException() in an exception handler.</span></span>

<span data-ttu-id="6d7ff-172">JavaScript</span><span class="sxs-lookup"><span data-stu-id="6d7ff-172">JavaScript</span></span>

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

<span data-ttu-id="6d7ff-173">C#</span><span class="sxs-lookup"><span data-stu-id="6d7ff-173">C#</span></span>

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

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

<span data-ttu-id="6d7ff-174">VB</span><span class="sxs-lookup"><span data-stu-id="6d7ff-174">VB</span></span>

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

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

<span data-ttu-id="6d7ff-175">Hello las medidas y las propiedades de parámetros son opcionales, pero son útiles para [filtrar y agregar](app-insights-diagnostic-search.md) información adicional.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-175">hello properties and measurements parameters are optional, but are useful for [filtering and adding](app-insights-diagnostic-search.md) extra information.</span></span> <span data-ttu-id="6d7ff-176">Por ejemplo, si tiene una aplicación que se puede ejecutar varios juegos, encontró todos los Hola excepción informes relacionados tooa juego determinado.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-176">For example, if you have an app that can run several games, you could find all hello exception reports related tooa particular game.</span></span> <span data-ttu-id="6d7ff-177">Puede agregar tantos elementos como como diccionario tooeach.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-177">You can add as many items as you like tooeach dictionary.</span></span>

## <a name="browser-exceptions"></a><span data-ttu-id="6d7ff-178">Excepciones de explorador</span><span class="sxs-lookup"><span data-stu-id="6d7ff-178">Browser exceptions</span></span>
<span data-ttu-id="6d7ff-179">Se notifican la mayoría de las excepciones de explorador.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-179">Most browser exceptions are reported.</span></span>

<span data-ttu-id="6d7ff-180">Si la página web incluye archivos de script de otros dominios o redes de entrega de contenido, asegúrese de que la etiqueta de script tiene el atributo de hello ```crossorigin="anonymous"```, y envía ese servidor hello [encabezados CORS](http://enable-cors.org/).</span><span class="sxs-lookup"><span data-stu-id="6d7ff-180">If your web page includes script files from content delivery networks or other domains, ensure your script tag has hello attribute ```crossorigin="anonymous"```,  and that hello server sends [CORS headers](http://enable-cors.org/).</span></span> <span data-ttu-id="6d7ff-181">Esto le permitirá tooget un seguimiento de pila y los detalles de las excepciones no controladas de JavaScript de estos recursos.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-181">This will allow you tooget a stack trace and detail for unhandled JavaScript exceptions from these resources.</span></span>

## <a name="web-forms"></a><span data-ttu-id="6d7ff-182">Formularios web</span><span class="sxs-lookup"><span data-stu-id="6d7ff-182">Web forms</span></span>
<span data-ttu-id="6d7ff-183">Para formularios web forms, Hola módulo HTTP será toocollect capaz de excepciones de hello cuando no hay ningún redirecciones configuradas con CustomErrors.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-183">For web forms, hello HTTP Module will be able toocollect hello exceptions when there are no redirects configured with CustomErrors.</span></span>

<span data-ttu-id="6d7ff-184">Pero si tiene activas redirecciones, agregar Hola siguen líneas toohello Application_Error función en Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-184">But if you have active redirects, add hello following lines toohello Application_Error function in Global.asax.cs.</span></span> <span data-ttu-id="6d7ff-185">(Agregue un archivo Global.asax si aún no tiene uno.)</span><span class="sxs-lookup"><span data-stu-id="6d7ff-185">(Add a Global.asax file if you don't already have one.)</span></span>

<span data-ttu-id="6d7ff-186">*C#*</span><span class="sxs-lookup"><span data-stu-id="6d7ff-186">*C#*</span></span>

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a><span data-ttu-id="6d7ff-187">MVC</span><span class="sxs-lookup"><span data-stu-id="6d7ff-187">MVC</span></span>
<span data-ttu-id="6d7ff-188">Si hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuración es `Off`, a continuación, las excepciones estarán disponibles para hello [módulo HTTP](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-188">If hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) configuration is `Off`, then exceptions will be available for hello [HTTP Module](https://msdn.microsoft.com/library/ms178468.aspx) toocollect.</span></span> <span data-ttu-id="6d7ff-189">Sin embargo, si es `RemoteOnly` (valor predeterminado), o `On`, a continuación, se borrará la excepción de hello y no está disponible para Application Insights tooautomatically recopilar.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-189">However, if it is `RemoteOnly` (default), or `On`, then hello exception will be cleared and not available for Application Insights tooautomatically collect.</span></span> <span data-ttu-id="6d7ff-190">Puede solucionar esto mediante la invalidación hello [System.Web.Mvc.HandleErrorAttribute clase](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)y aplicar clase hello se reemplaza, tal como se muestra de Hola diferentes MVC las versiones siguientes ([github origen](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span><span class="sxs-lookup"><span data-stu-id="6d7ff-190">You can fix that by overriding hello [System.Web.Mvc.HandleErrorAttribute class](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx), and applying hello overridden class as shown for hello different MVC versions below ([github source](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):</span></span>

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
                //If customError is Off, then AI HTTPModule will report hello exception
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

#### <a name="mvc-2"></a><span data-ttu-id="6d7ff-191">MVC 2</span><span class="sxs-lookup"><span data-stu-id="6d7ff-191">MVC 2</span></span>
<span data-ttu-id="6d7ff-192">Reemplace el atributo de HandleError de hello con el nuevo atributo en los controladores.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-192">Replace hello HandleError attribute with your new attribute in your controllers.</span></span>

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[<span data-ttu-id="6d7ff-193">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d7ff-193">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a><span data-ttu-id="6d7ff-194">MVC 3</span><span class="sxs-lookup"><span data-stu-id="6d7ff-194">MVC 3</span></span>
<span data-ttu-id="6d7ff-195">Registrar `AiHandleErrorAttribute` como filtro global de Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-195">Register `AiHandleErrorAttribute` as a global filter in Global.asax.cs:</span></span>

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[<span data-ttu-id="6d7ff-196">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d7ff-196">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a><span data-ttu-id="6d7ff-197">MVC 4, MVC5</span><span class="sxs-lookup"><span data-stu-id="6d7ff-197">MVC 4, MVC5</span></span>
<span data-ttu-id="6d7ff-198">Registrar AiHandleErrorAttribute como filtro global en FilterConfig.cs:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-198">Register AiHandleErrorAttribute as a global filter in FilterConfig.cs:</span></span>

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[<span data-ttu-id="6d7ff-199">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d7ff-199">Sample</span></span>](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a><span data-ttu-id="6d7ff-200">Web API 1.x</span><span class="sxs-lookup"><span data-stu-id="6d7ff-200">Web API 1.x</span></span>
<span data-ttu-id="6d7ff-201">Invalidar System.Web.Http.Filters.ExceptionFilterAttribute:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-201">Override System.Web.Http.Filters.ExceptionFilterAttribute:</span></span>

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

<span data-ttu-id="6d7ff-202">Puede agregar este atributo reemplazado los controladores de toospecific o agregar configuración de filtros globales toohello en la clase WebApiConfig de hello:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-202">You could add this overridden attribute toospecific controllers, or add it toohello global filter configuration in hello WebApiConfig class:</span></span>

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

[<span data-ttu-id="6d7ff-203">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d7ff-203">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

<span data-ttu-id="6d7ff-204">Hay una serie de casos que no pueden controlar los filtros de excepción Hola.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-204">There are a number of cases that hello exception filters cannot handle.</span></span> <span data-ttu-id="6d7ff-205">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-205">For example:</span></span>

* <span data-ttu-id="6d7ff-206">Excepciones iniciadas por constructores del controlador.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-206">Exceptions thrown from controller constructors.</span></span>
* <span data-ttu-id="6d7ff-207">Excepciones iniciadas por controladores de mensajes.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-207">Exceptions thrown from message handlers.</span></span>
* <span data-ttu-id="6d7ff-208">Excepciones iniciadas durante el enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-208">Exceptions thrown during routing.</span></span>
* <span data-ttu-id="6d7ff-209">Excepciones iniciadas durante la serialización del contenido de respuesta.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-209">Exceptions thrown during response content serialization.</span></span>

## <a name="web-api-2x"></a><span data-ttu-id="6d7ff-210">Web API 2.x</span><span class="sxs-lookup"><span data-stu-id="6d7ff-210">Web API 2.x</span></span>
<span data-ttu-id="6d7ff-211">Agregue una implementación de IExceptionLogger:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-211">Add an implementation of IExceptionLogger:</span></span>

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

<span data-ttu-id="6d7ff-212">Agregue este servicios toohello en WebApiConfig:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-212">Add this toohello services in WebApiConfig:</span></span>

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
  <span data-ttu-id="6d7ff-213">}</span><span class="sxs-lookup"><span data-stu-id="6d7ff-213">}</span></span>

[<span data-ttu-id="6d7ff-214">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d7ff-214">Sample</span></span>](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

<span data-ttu-id="6d7ff-215">Como alternativa, puede:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-215">As alternatives, you could:</span></span>

1. <span data-ttu-id="6d7ff-216">Reemplace Hola solo ExceptionHandler con una implementación personalizada de IExceptionHandler.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-216">Replace hello only ExceptionHandler with a custom implementation of IExceptionHandler.</span></span> <span data-ttu-id="6d7ff-217">Esto solo se llama cuando el marco de trabajo de hello es todavía puede toochoose qué respuesta mensaje toosend (no cuando Hola conexión anulada por ejemplo)</span><span class="sxs-lookup"><span data-stu-id="6d7ff-217">This is only called when hello framework is still able toochoose which response message toosend (not when hello connection is aborted for instance)</span></span>
2. <span data-ttu-id="6d7ff-218">Filtros de excepción (como se describe en la sección de hello en los controladores de API Web 1.x anteriores) - no se llama en todos los casos.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-218">Exception Filters (as described in hello section on Web API 1.x controllers above) - not called in all cases.</span></span>

## <a name="wcf"></a><span data-ttu-id="6d7ff-219">WCF</span><span class="sxs-lookup"><span data-stu-id="6d7ff-219">WCF</span></span>
<span data-ttu-id="6d7ff-220">Agregue una clase que extienda el atributo y que implemente IErrorHandler y IServiceBehavior.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-220">Add a class that extends Attribute and implements IErrorHandler and IServiceBehavior.</span></span>

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

<span data-ttu-id="6d7ff-221">Agregue las implementaciones del servicio Hola atributo toohello:</span><span class="sxs-lookup"><span data-stu-id="6d7ff-221">Add hello attribute toohello service implementations:</span></span>

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[<span data-ttu-id="6d7ff-222">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6d7ff-222">Sample</span></span>](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a><span data-ttu-id="6d7ff-223">Contadores de rendimiento de excepciones</span><span class="sxs-lookup"><span data-stu-id="6d7ff-223">Exception performance counters</span></span>
<span data-ttu-id="6d7ff-224">Si tiene [instalado el agente de visión de la aplicación hello](app-insights-monitor-performance-live-website-now.md) en el servidor, puede obtener un gráfico de velocidad de excepciones de hello, medido por. NET.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-224">If you have [installed hello Application Insights Agent](app-insights-monitor-performance-live-website-now.md) on your server, you can get a chart of hello exceptions rate, measured by .NET.</span></span> <span data-ttu-id="6d7ff-225">Esto incluye las excepciones de .NET, tanto controladas como no controladas.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-225">This includes both handled and unhandled .NET exceptions.</span></span>

<span data-ttu-id="6d7ff-226">Abra una hoja del Explorador de métricas, agregue un nuevo gráfico y seleccione **Tasa de excepciones**, que aparece debajo de Contadores de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-226">Open a Metric Explorer blade, add a new chart, and select **Exception rate**, listed under Performance Counters.</span></span>

<span data-ttu-id="6d7ff-227">.NET framework de Hello calcula la tasa de Hola Hola recuento de excepciones en un intervalo y dividiendo por longitud Hola de intervalo de saludo.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-227">hello .NET framework calculates hello rate by counting hello number of exceptions in an interval and dividing by hello length of hello interval.</span></span>

<span data-ttu-id="6d7ff-228">Tenga en cuenta que debe ser diferente del número de excepciones' hello' calculado por el portal de Application Insights Hola contando TrackException informes.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-228">Note that it will be different from hello 'Exceptions' count calculated by hello Application Insights portal by counting TrackException reports.</span></span> <span data-ttu-id="6d7ff-229">intervalos de muestreo de Hello son diferentes y Hola SDK no enviar informes de TrackException para todas las excepciones controladas y sin controlar.</span><span class="sxs-lookup"><span data-stu-id="6d7ff-229">hello sampling intervals are different, and hello SDK doesn't send TrackException reports for all handled and unhandled exceptions.</span></span>

## <a name="video"></a><span data-ttu-id="6d7ff-230">Vídeo</span><span class="sxs-lookup"><span data-stu-id="6d7ff-230">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a><span data-ttu-id="6d7ff-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6d7ff-231">Next steps</span></span>
* [<span data-ttu-id="6d7ff-232">Supervisar REST, SQL y otros toodependencies de llamadas</span><span class="sxs-lookup"><span data-stu-id="6d7ff-232">Monitor REST, SQL and other calls toodependencies</span></span>](app-insights-asp-net-dependencies.md)
* [<span data-ttu-id="6d7ff-233">Supervisar los tiempos de carga de página, las excepciones del explorador y las llamadas AJAX</span><span class="sxs-lookup"><span data-stu-id="6d7ff-233">Monitor page load times, browser exceptions, and AJAX calls</span></span>](app-insights-javascript.md)
* [<span data-ttu-id="6d7ff-234">Supervisar los contadores de rendimiento</span><span class="sxs-lookup"><span data-stu-id="6d7ff-234">Monitor performance counters</span></span>](app-insights-performance-counters.md)
