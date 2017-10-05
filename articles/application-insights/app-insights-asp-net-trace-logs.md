---
title: "Exploración de registros de seguimiento de .NET en Application Insights"
description: Busque registros generados con Seguimiento, NLog o Log4Net.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 68e03bf10167ecde675d62782de7063aea9e81d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="09279-103">Exploración de registros de seguimiento de .NET en Application Insights</span><span class="sxs-lookup"><span data-stu-id="09279-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="09279-104">Si usa NLog, log4Net o System.Diagnostics.Trace para realizar el seguimiento de diagnósticos en la aplicación ASP.NET, sus registros se pueden enviar a [Azure Application Insights][start], donde puede explorarlos y buscarlos.</span><span class="sxs-lookup"><span data-stu-id="09279-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent to [Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="09279-105">Los registros se combinarán con los otros informes de telemetría procedente de su aplicación, y así podrá identificar los seguimientos asociados con el mantenimiento de cada solicitud de usuario y correlacionarlos con otros eventos e informes de excepciones.</span><span class="sxs-lookup"><span data-stu-id="09279-105">Your logs will be merged with the other telemetry coming from your application, so that you can identify the traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="09279-106">¿Necesita el módulo de captura de registros?</span><span class="sxs-lookup"><span data-stu-id="09279-106">Do you need the log capture module?</span></span> <span data-ttu-id="09279-107">Es un adaptador útil para registradores de terceros, pero si aún no está usando NLog, log4Net o System.Diagnostics.Trace, considere la posibilidad de llamar directamente a [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) .</span><span class="sxs-lookup"><span data-stu-id="09279-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="09279-108">Instalación del registro en la aplicación</span><span class="sxs-lookup"><span data-stu-id="09279-108">Install logging on your app</span></span>
<span data-ttu-id="09279-109">Instale el marco de registro elegido en su proyecto.</span><span class="sxs-lookup"><span data-stu-id="09279-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="09279-110">Esto debería producir una entrada en app.config o web.config.</span><span class="sxs-lookup"><span data-stu-id="09279-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="09279-111">Si usa System.Diagnostics.Trace, debe agregar una entrada a web.config:</span><span class="sxs-lookup"><span data-stu-id="09279-111">If you're using System.Diagnostics.Trace, you need to add an entry to web.config:</span></span>

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-to-collect-logs"></a><span data-ttu-id="09279-112">Configuración de Application Insights para recopilar registros</span><span class="sxs-lookup"><span data-stu-id="09279-112">Configure Application Insights to collect logs</span></span>
<span data-ttu-id="09279-113">Si todavía no lo ha hecho, **[agregue Application Insights a su proyecto](app-insights-asp-net.md)**.</span><span class="sxs-lookup"><span data-stu-id="09279-113">**[Add Application Insights to your project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="09279-114">Verá una opción para incluir el compilador de registros.</span><span class="sxs-lookup"><span data-stu-id="09279-114">You'll see an option to include the log collector.</span></span>

<span data-ttu-id="09279-115">O **configure Application Insights** haciendo clic con el botón derecho en el proyecto en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="09279-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="09279-116">Seleccione la opción de **Configurar recolección de seguimientos**.</span><span class="sxs-lookup"><span data-stu-id="09279-116">Select the option to **Configure trace collection**.</span></span>

<span data-ttu-id="09279-117">*¿No aparece ningún menú de Application Insights ni una opción de compilador de registros?*</span><span class="sxs-lookup"><span data-stu-id="09279-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="09279-118">Pruebe la [solución de problemas](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="09279-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="09279-119">Instalación manual</span><span class="sxs-lookup"><span data-stu-id="09279-119">Manual installation</span></span>
<span data-ttu-id="09279-120">Utilice este método si el tipo de proyecto no es compatible con el programa de instalación de Application Insights (por ejemplo, un proyecto de escritorio de Windows).</span><span class="sxs-lookup"><span data-stu-id="09279-120">Use this method if your project type isn't supported by the Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="09279-121">Si planea usar log4Net o NLog, instálelo en su proyecto.</span><span class="sxs-lookup"><span data-stu-id="09279-121">If you plan to use log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="09279-122">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y seleccione **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="09279-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="09279-123">Busque "Application Insights"</span><span class="sxs-lookup"><span data-stu-id="09279-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="09279-124">Seleccione el paquete adecuado entre los siguientes:</span><span class="sxs-lookup"><span data-stu-id="09279-124">Select the appropriate package - one of:</span></span>

   * <span data-ttu-id="09279-125">Microsoft.ApplicationInsights.TraceListener (para capturar las llamadas de System.Diagnostics.Trace)</span><span class="sxs-lookup"><span data-stu-id="09279-125">Microsoft.ApplicationInsights.TraceListener (to capture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="09279-126">Microsoft.ApplicationInsights.EventSourceListener (para capturar eventos EventSource)</span><span class="sxs-lookup"><span data-stu-id="09279-126">Microsoft.ApplicationInsights.EventSourceListener (to capture EventSource events)</span></span>
   * <span data-ttu-id="09279-127">Microsoft.ApplicationInsights.EtwListener (para capturar eventos ETW)</span><span class="sxs-lookup"><span data-stu-id="09279-127">Microsoft.ApplicationInsights.EtwListener (to capture ETW events)</span></span>
   * <span data-ttu-id="09279-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="09279-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="09279-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="09279-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="09279-130">El paquete de NuGet instala los ensamblados necesarios y también modifica el archivo web.config o app.config.</span><span class="sxs-lookup"><span data-stu-id="09279-130">The NuGet package installs the necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="09279-131">Insertar llamadas de registro de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="09279-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="09279-132">Si usa System.Diagnostics.Trace, una llamada típica sería:</span><span class="sxs-lookup"><span data-stu-id="09279-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="09279-133">Si prefiere log4net o NLog:</span><span class="sxs-lookup"><span data-stu-id="09279-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="09279-134">Uso de eventos EventSource</span><span class="sxs-lookup"><span data-stu-id="09279-134">Using EventSource events</span></span>
<span data-ttu-id="09279-135">Puede configurar eventos [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) para enviarse a Application Insights como seguimientos.</span><span class="sxs-lookup"><span data-stu-id="09279-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="09279-136">Primero, instale el paquete de NuGet `Microsoft.ApplicationInsights.EventSourceListener`.</span><span class="sxs-lookup"><span data-stu-id="09279-136">First, install the `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="09279-137">Luego, edite la sección `TelemetryModules` del archivo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="09279-137">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="09279-138">En cada origen, puede establecer los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="09279-138">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="09279-139">`Name` especifica el nombre del evento EventSource que se recopilará.</span><span class="sxs-lookup"><span data-stu-id="09279-139">`Name` specifies the name of the EventSource to collect.</span></span>
 * <span data-ttu-id="09279-140">`Level` especifica el nivel de registro que se recopilará.</span><span class="sxs-lookup"><span data-stu-id="09279-140">`Level` specifies the logging level to collect.</span></span> <span data-ttu-id="09279-141">Puede ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` o `Warning`.</span><span class="sxs-lookup"><span data-stu-id="09279-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="09279-142">`Keywords` especifica el valor del entero de combinaciones de palabras clave que se usará (opcional).</span><span class="sxs-lookup"><span data-stu-id="09279-142">`Keywords` (Optional) specifies the integer value of keywords combinations to use.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="09279-143">Uso de eventos de DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="09279-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="09279-144">Puede configurar eventos [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) para enviarlos a Application Insights como seguimientos.</span><span class="sxs-lookup"><span data-stu-id="09279-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="09279-145">Primero, instale el paquete de NuGet [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener).</span><span class="sxs-lookup"><span data-stu-id="09279-145">First, install the [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="09279-146">Seguidamente, edite la sección `TelemetryModules` del archivo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="09279-146">Then edit the `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="09279-147">Para cada instancia de DiagnosticSource que quiera seguir, agregue una entrada con el atributo `Name` establecido con el nombre de la instancia DiagnosticSource.</span><span class="sxs-lookup"><span data-stu-id="09279-147">For each DiagnosticSource you want to trace, add an entry with the `Name` attribute  set to the name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="09279-148">Uso de eventos ETW</span><span class="sxs-lookup"><span data-stu-id="09279-148">Using ETW events</span></span>
<span data-ttu-id="09279-149">Puede configurar eventos ETW para enviarse a Application Insights como seguimientos.</span><span class="sxs-lookup"><span data-stu-id="09279-149">You can configure ETW events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="09279-150">Primero, instale el paquete de NuGet `Microsoft.ApplicationInsights.EtwCollector`.</span><span class="sxs-lookup"><span data-stu-id="09279-150">First, install the `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="09279-151">Luego, edite la sección `TelemetryModules` del archivo [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md).</span><span class="sxs-lookup"><span data-stu-id="09279-151">Then edit `TelemetryModules` section of the [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="09279-152">Solo se pueden recopilar eventos ETW si el proceso que hospeda el SDK se ejecuta bajo una identidad que sea miembro de "Usuarios del registro de rendimiento" o los administradores.</span><span class="sxs-lookup"><span data-stu-id="09279-152">ETW events can only be collected if the process hosting the SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="09279-153">En cada origen, puede establecer los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="09279-153">For each source, you can set the following parameters:</span></span>
 * <span data-ttu-id="09279-154">`ProviderName` es el nombre del proveedor ETW que se recopilará.</span><span class="sxs-lookup"><span data-stu-id="09279-154">`ProviderName` is the name of the ETW provider to collect.</span></span>
 * <span data-ttu-id="09279-155">`ProviderGuid` especifica el GUID del proveedor ETW que se recopilará, que puede usarse en lugar de `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="09279-155">`ProviderGuid` specifies the GUID of the ETW provider to collect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="09279-156">`Level` establece el nivel de registro que se recopilará.</span><span class="sxs-lookup"><span data-stu-id="09279-156">`Level` sets the logging level to collect.</span></span> <span data-ttu-id="09279-157">Puede ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` o `Warning`.</span><span class="sxs-lookup"><span data-stu-id="09279-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="09279-158">`Keywords` establece el valor del entero de combinaciones de palabras clave que se usará (opcional).</span><span class="sxs-lookup"><span data-stu-id="09279-158">`Keywords` (Optional) sets the integer value of keyword combinations to use.</span></span>

## <a name="using-the-trace-api-directly"></a><span data-ttu-id="09279-159">Uso de la API de seguimiento directamente</span><span class="sxs-lookup"><span data-stu-id="09279-159">Using the Trace API directly</span></span>
<span data-ttu-id="09279-160">Puede llamar directamente a la API de seguimiento de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="09279-160">You can call the Application Insights trace API directly.</span></span> <span data-ttu-id="09279-161">Los adaptadores de registro usan esta API.</span><span class="sxs-lookup"><span data-stu-id="09279-161">The logging adapters use this API.</span></span>

<span data-ttu-id="09279-162">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="09279-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="09279-163">Una ventaja de TrackTrace es que puede colocar datos relativamente largos en el mensaje.</span><span class="sxs-lookup"><span data-stu-id="09279-163">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="09279-164">Por ejemplo, aquí podría codificar datos POST.</span><span class="sxs-lookup"><span data-stu-id="09279-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="09279-165">Además, puede agregar un nivel de gravedad al mensaje.</span><span class="sxs-lookup"><span data-stu-id="09279-165">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="09279-166">Y, al igual que con otra telemetría, puede agregar valores de propiedad que puede usar para ayudar a filtrar o buscar distintos conjuntos de seguimientos.</span><span class="sxs-lookup"><span data-stu-id="09279-166">And, like other telemetry, you can add property values that you can use to help filter or search for different sets of traces.</span></span> <span data-ttu-id="09279-167">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="09279-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="09279-168">Esto permitiría filtrar fácilmente en [Búsqueda][diagnostic] todos los mensajes de un determinado nivel de gravedad relativos a una determinada base de datos.</span><span class="sxs-lookup"><span data-stu-id="09279-168">This would enable you, in [Search][diagnostic], to easily filter out all the messages of a particular severity level relating to a particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="09279-169">Explorar los registros</span><span class="sxs-lookup"><span data-stu-id="09279-169">Explore your logs</span></span>
<span data-ttu-id="09279-170">Ejecute la aplicación, ya sea en modo de depuración o mediante su implementación para que esté activa.</span><span class="sxs-lookup"><span data-stu-id="09279-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="09279-171">En la hoja de información general de su aplicación del [portal de Application Insights][portal], elija [Buscar][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="09279-171">In your app's overview blade in [the Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![En Application Insights, elija Buscar.](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Búsqueda](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="09279-174">Por ejemplo, puede:</span><span class="sxs-lookup"><span data-stu-id="09279-174">You can, for example:</span></span>

* <span data-ttu-id="09279-175">Filtrar por seguimientos de registro, o por elementos con determinadas propiedades</span><span class="sxs-lookup"><span data-stu-id="09279-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="09279-176">Inspeccionar un elemento específico en detalle</span><span class="sxs-lookup"><span data-stu-id="09279-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="09279-177">Encontrar otros informes de telemetría relacionados con la misma solicitud de usuario (es decir, con el mismo OperationId)</span><span class="sxs-lookup"><span data-stu-id="09279-177">Find other telemetry relating to the same user request (that is, with the same OperationId)</span></span>
* <span data-ttu-id="09279-178">Guardar la configuración de esta página como favorita</span><span class="sxs-lookup"><span data-stu-id="09279-178">Save the configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="09279-179">**Muestreo.**</span><span class="sxs-lookup"><span data-stu-id="09279-179">**Sampling.**</span></span> <span data-ttu-id="09279-180">Si la aplicación envía una gran cantidad de datos y usa el SDK de Application Insights para ASP.NET versión 2.0.0-beta3 o posterior, la característica de muestreo adaptativo puede operar y enviar solamente un porcentaje de los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="09279-180">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="09279-181">Obtenga más información sobre el muestreo.</span><span class="sxs-lookup"><span data-stu-id="09279-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="09279-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09279-182">Next steps</span></span>
<span data-ttu-id="09279-183">[Diagnóstico de errores y excepciones en ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="09279-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="09279-184">[Aprenda más sobre la búsqueda][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="09279-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="09279-185">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="09279-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="09279-186">¿Cómo se puede hacer para Java?</span><span class="sxs-lookup"><span data-stu-id="09279-186">How do I do this for Java?</span></span>
<span data-ttu-id="09279-187">Utilice los [adaptadores de registro de Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="09279-187">Use the [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-the-project-context-menu"></a><span data-ttu-id="09279-188">No aparece la opción de Application Insights en el menú contextual del proyecto</span><span class="sxs-lookup"><span data-stu-id="09279-188">There's no Application Insights option on the project context menu</span></span>
* <span data-ttu-id="09279-189">Compruebe si las herramientas de Application Insights están instaladas en este equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="09279-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="09279-190">En el menú Herramientas de Visual Studio, en Extensiones y actualizaciones, busque Herramientas de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="09279-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="09279-191">Si no se encuentran en la pestaña Instalado, abra la pestaña En línea e instálelas.</span><span class="sxs-lookup"><span data-stu-id="09279-191">If it isn't in the Installed tab, open the Online tab and install it.</span></span>
* <span data-ttu-id="09279-192">Podría tratarse de un tipo de proyecto no admitido por las herramientas de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="09279-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="09279-193">Use la [instalación manual](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="09279-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-the-configuration-tool"></a><span data-ttu-id="09279-194">No aparece la opción de adaptador en la herramienta de configuración</span><span class="sxs-lookup"><span data-stu-id="09279-194">No log adapter option in the configuration tool</span></span>
* <span data-ttu-id="09279-195">Debe instalar primero el marco de registro.</span><span class="sxs-lookup"><span data-stu-id="09279-195">You need to install the logging framework first.</span></span>
* <span data-ttu-id="09279-196">Si usa System.Diagnostics.Trace, asegúrese de que lo ha [configurado en `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="09279-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="09279-197">¿Tiene la versión más reciente de Application Insights?</span><span class="sxs-lookup"><span data-stu-id="09279-197">Have you got the latest version of Application Insights?</span></span> <span data-ttu-id="09279-198">En el menú **Herramientas** de Visual Studio, elija **Extensiones y actualizaciones** y abra la pestaña **Actualizaciones**. Si Developer Analytics Tools está instalado, haga clic para actualizarlo.</span><span class="sxs-lookup"><span data-stu-id="09279-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open the **Updates** tab. If Developer Analytics tools is there, click to update it.</span></span>

### <span data-ttu-id="09279-199"><a name="emptykey"></a>Aparece el mensaje de error "La clave de instrumentación no puede estar vacía".</span><span class="sxs-lookup"><span data-stu-id="09279-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="09279-200">Parece que ha instalado el paquete de NuGet del adaptador de registro sin tener que instalar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="09279-200">Looks like you installed the logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="09279-201">En el Explorador de soluciones, haga clic con el botón derecho en `ApplicationInsights.config` y elija **Actualizar Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="09279-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="09279-202">Aparecerá un cuadro de diálogo que le invita a iniciar sesión en Azure y a crear un recurso de Application Insights, o a volver a utilizar uno existente.</span><span class="sxs-lookup"><span data-stu-id="09279-202">You'll get a dialog that invites you to sign in to Azure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="09279-203">Esto debería solucionarlo.</span><span class="sxs-lookup"><span data-stu-id="09279-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-the-other-events"></a><span data-ttu-id="09279-204">Puedo ver seguimientos en Búsqueda de diagnóstico, pero no los otros eventos.</span><span class="sxs-lookup"><span data-stu-id="09279-204">I can see traces in diagnostic search, but not the other events</span></span>
<span data-ttu-id="09279-205">A veces, el paso de todos los eventos y solicitudes por la canalización puede llevar un rato.</span><span class="sxs-lookup"><span data-stu-id="09279-205">It can sometimes take a while for all the events and requests to get through the pipeline.</span></span>

### <span data-ttu-id="09279-206"><a name="limits"></a>¿Qué cantidad de datos se conserva?</span><span class="sxs-lookup"><span data-stu-id="09279-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="09279-207">Hay varios factores que afectan a la cantidad de datos que se conservan.</span><span class="sxs-lookup"><span data-stu-id="09279-207">Several factors impact the amount of data retained.</span></span> <span data-ttu-id="09279-208">Consulte la sección [Límites](app-insights-api-custom-events-metrics.md#limits) de la página de métricas de eventos de cliente para más información.</span><span class="sxs-lookup"><span data-stu-id="09279-208">See the [limits](app-insights-api-custom-events-metrics.md#limits) section of the customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-the-log-entries-that-i-expect"></a><span data-ttu-id="09279-209">No veo algunas de las entradas del registro que esperaba</span><span class="sxs-lookup"><span data-stu-id="09279-209">I'm not seeing some of the log entries that I expect</span></span>
<span data-ttu-id="09279-210">Si la aplicación envía una gran cantidad de datos y usa el SDK de Application Insights para ASP.NET versión 2.0.0-beta3 o posterior, la característica de muestreo adaptativo puede operar y enviar solamente un porcentaje de los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="09279-210">If your application sends a lot of data and you are using the Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="09279-211">Obtenga más información sobre el muestreo.</span><span class="sxs-lookup"><span data-stu-id="09279-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="09279-212"><a name="add"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09279-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="09279-213">[Configuración de pruebas de disponibilidad y de capacidad de respuesta][availability]</span><span class="sxs-lookup"><span data-stu-id="09279-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="09279-214">[Solución de problemas][qna]</span><span class="sxs-lookup"><span data-stu-id="09279-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
