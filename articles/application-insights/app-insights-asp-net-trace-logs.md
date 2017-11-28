---
title: los registros de seguimiento de .NET de aaaExplore en Application Insights
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
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a><span data-ttu-id="46834-103">Exploración de registros de seguimiento de .NET en Application Insights</span><span class="sxs-lookup"><span data-stu-id="46834-103">Explore .NET trace logs in Application Insights</span></span>
<span data-ttu-id="46834-104">Si usa NLog, log4Net o System.Diagnostics.Trace para el seguimiento de diagnóstico en la aplicación de ASP.NET, puede que los registros que se envían demasiado[Azure Application Insights][start], donde puede explorar y buscar ellos.</span><span class="sxs-lookup"><span data-stu-id="46834-104">If you use NLog, log4Net or System.Diagnostics.Trace for diagnostic tracing in your ASP.NET application, you can have your logs sent too[Azure Application Insights][start], where you can explore and search them.</span></span> <span data-ttu-id="46834-105">Los registros se combinará con hello otro telemetría procedentes de la aplicación, para que pueda identificar Hola seguimientos asociados con cada solicitud del usuario de mantenimiento y ponerlos en correlación con eventos e informes de excepción.</span><span class="sxs-lookup"><span data-stu-id="46834-105">Your logs will be merged with hello other telemetry coming from your application, so that you can identify hello traces associated with servicing each user request, and correlate them with other events and exception reports.</span></span>

> [!NOTE]
> <span data-ttu-id="46834-106">¿Necesita que el módulo de captura de registro de hello?</span><span class="sxs-lookup"><span data-stu-id="46834-106">Do you need hello log capture module?</span></span> <span data-ttu-id="46834-107">Es un adaptador útil para registradores de terceros, pero si aún no está usando NLog, log4Net o System.Diagnostics.Trace, considere la posibilidad de llamar directamente a [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) .</span><span class="sxs-lookup"><span data-stu-id="46834-107">It's a useful adapter for 3rd-party loggers, but if you aren't already using NLog, log4Net or System.Diagnostics.Trace, consider just calling [Application Insights TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) directly.</span></span>
>
>

## <a name="install-logging-on-your-app"></a><span data-ttu-id="46834-108">Instalación del registro en la aplicación</span><span class="sxs-lookup"><span data-stu-id="46834-108">Install logging on your app</span></span>
<span data-ttu-id="46834-109">Instale el marco de registro elegido en su proyecto.</span><span class="sxs-lookup"><span data-stu-id="46834-109">Install your chosen logging framework in your project.</span></span> <span data-ttu-id="46834-110">Esto debería producir una entrada en app.config o web.config.</span><span class="sxs-lookup"><span data-stu-id="46834-110">This should result in an entry in app.config or web.config.</span></span>

<span data-ttu-id="46834-111">Si usas System.Diagnostics.Trace, deberá tooadd un tooweb.config de entrada:</span><span class="sxs-lookup"><span data-stu-id="46834-111">If you're using System.Diagnostics.Trace, you need tooadd an entry tooweb.config:</span></span>

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
## <a name="configure-application-insights-toocollect-logs"></a><span data-ttu-id="46834-112">Configurar registros de toocollect Application Insights</span><span class="sxs-lookup"><span data-stu-id="46834-112">Configure Application Insights toocollect logs</span></span>
<span data-ttu-id="46834-113">**[Agregar proyecto de Application Insights tooyour](app-insights-asp-net.md)**  si aún no lo ha hecho todavía.</span><span class="sxs-lookup"><span data-stu-id="46834-113">**[Add Application Insights tooyour project](app-insights-asp-net.md)** if you haven't done that yet.</span></span> <span data-ttu-id="46834-114">Verá un compilador de registros de opción tooinclude Hola.</span><span class="sxs-lookup"><span data-stu-id="46834-114">You'll see an option tooinclude hello log collector.</span></span>

<span data-ttu-id="46834-115">O **configure Application Insights** haciendo clic con el botón derecho en el proyecto en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="46834-115">Or **Configure Application Insights** by right-clicking your project in Solution Explorer.</span></span> <span data-ttu-id="46834-116">Seleccione la opción de hello demasiado**configurar la recopilación de seguimiento**.</span><span class="sxs-lookup"><span data-stu-id="46834-116">Select hello option too**Configure trace collection**.</span></span>

<span data-ttu-id="46834-117">*¿No aparece ningún menú de Application Insights ni una opción de compilador de registros?*</span><span class="sxs-lookup"><span data-stu-id="46834-117">*No Application Insights menu or log collector option?*</span></span> <span data-ttu-id="46834-118">Pruebe la [solución de problemas](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="46834-118">Try [Troubleshooting](#troubleshooting).</span></span>

## <a name="manual-installation"></a><span data-ttu-id="46834-119">Instalación manual</span><span class="sxs-lookup"><span data-stu-id="46834-119">Manual installation</span></span>
<span data-ttu-id="46834-120">Utilice este método si el tipo de proyecto no es compatible con el instalador de Application Insights hello (por ejemplo un proyecto escritorio de Windows).</span><span class="sxs-lookup"><span data-stu-id="46834-120">Use this method if your project type isn't supported by hello Application Insights installer (for example a Windows desktop project).</span></span>

1. <span data-ttu-id="46834-121">Si tiene previsto toouse log4Net o NLog, instálelo en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="46834-121">If you plan toouse log4Net or NLog, install it in your project.</span></span>
2. <span data-ttu-id="46834-122">En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y seleccione **Administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="46834-122">In Solution Explorer, right-click your project and choose **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="46834-123">Busque "Application Insights"</span><span class="sxs-lookup"><span data-stu-id="46834-123">Search for "Application Insights"</span></span>
4. <span data-ttu-id="46834-124">Seleccione el paquete adecuado de hello - uno de:</span><span class="sxs-lookup"><span data-stu-id="46834-124">Select hello appropriate package - one of:</span></span>

   * <span data-ttu-id="46834-125">Microsoft.ApplicationInsights.TraceListener (llamadas a System.Diagnostics.Trace toocapture)</span><span class="sxs-lookup"><span data-stu-id="46834-125">Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace calls)</span></span>
   * <span data-ttu-id="46834-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource eventos)</span><span class="sxs-lookup"><span data-stu-id="46834-126">Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource events)</span></span>
   * <span data-ttu-id="46834-127">Microsoft.ApplicationInsights.EtwListener (toocapture los eventos ETW)</span><span class="sxs-lookup"><span data-stu-id="46834-127">Microsoft.ApplicationInsights.EtwListener (toocapture ETW events)</span></span>
   * <span data-ttu-id="46834-128">Microsoft.ApplicationInsights.NLogTarget</span><span class="sxs-lookup"><span data-stu-id="46834-128">Microsoft.ApplicationInsights.NLogTarget</span></span>
   * <span data-ttu-id="46834-129">Microsoft.ApplicationInsights.Log4NetAppender</span><span class="sxs-lookup"><span data-stu-id="46834-129">Microsoft.ApplicationInsights.Log4NetAppender</span></span>

<span data-ttu-id="46834-130">paquete de NuGet Hola instala a los ensamblados necesarios de Hola y también modifica el archivo web.config o app.config.</span><span class="sxs-lookup"><span data-stu-id="46834-130">hello NuGet package installs hello necessary assemblies, and also modifies web.config or app.config.</span></span>

## <a name="insert-diagnostic-log-calls"></a><span data-ttu-id="46834-131">Insertar llamadas de registro de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="46834-131">Insert diagnostic log calls</span></span>
<span data-ttu-id="46834-132">Si usa System.Diagnostics.Trace, una llamada típica sería:</span><span class="sxs-lookup"><span data-stu-id="46834-132">If you use System.Diagnostics.Trace, a typical call would be:</span></span>

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

<span data-ttu-id="46834-133">Si prefiere log4net o NLog:</span><span class="sxs-lookup"><span data-stu-id="46834-133">If you prefer log4net or NLog:</span></span>

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a><span data-ttu-id="46834-134">Uso de eventos EventSource</span><span class="sxs-lookup"><span data-stu-id="46834-134">Using EventSource events</span></span>
<span data-ttu-id="46834-135">Puede configurar [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) tooApplication de toobe enviado eventos visión como seguimientos.</span><span class="sxs-lookup"><span data-stu-id="46834-135">You can configure [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="46834-136">En primer lugar, instale hello `Microsoft.ApplicationInsights.EventSourceListener` paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="46834-136">First, install hello `Microsoft.ApplicationInsights.EventSourceListener` NuGet package.</span></span> <span data-ttu-id="46834-137">A continuación, edite `TelemetryModules` sección de hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) archivo.</span><span class="sxs-lookup"><span data-stu-id="46834-137">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="46834-138">Para cada origen, puede establecer Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="46834-138">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="46834-139">`Name`Especifica el nombre de Hola de hello EventSource toocollect.</span><span class="sxs-lookup"><span data-stu-id="46834-139">`Name` specifies hello name of hello EventSource toocollect.</span></span>
 * <span data-ttu-id="46834-140">`Level`Especifica hello toocollect de nivel de registro.</span><span class="sxs-lookup"><span data-stu-id="46834-140">`Level` specifies hello logging level toocollect.</span></span> <span data-ttu-id="46834-141">Puede ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` o `Warning`.</span><span class="sxs-lookup"><span data-stu-id="46834-141">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="46834-142">`Keywords`(Opcional) especifica el valor entero hello toouse de combinaciones de palabras clave.</span><span class="sxs-lookup"><span data-stu-id="46834-142">`Keywords` (Optional) specifies hello integer value of keywords combinations toouse.</span></span>

## <a name="using-diagnosticsource-events"></a><span data-ttu-id="46834-143">Uso de eventos de DiagnosticSource</span><span class="sxs-lookup"><span data-stu-id="46834-143">Using DiagnosticSource events</span></span>
<span data-ttu-id="46834-144">Puede configurar [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) tooApplication de toobe enviado eventos visión como seguimientos.</span><span class="sxs-lookup"><span data-stu-id="46834-144">You can configure [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="46834-145">En primer lugar, instale hello [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="46834-145">First, install hello [`Microsoft.ApplicationInsights.DiagnosticSourceListener`](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet package.</span></span> <span data-ttu-id="46834-146">A continuación, edite hello `TelemetryModules` sección de hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) archivo.</span><span class="sxs-lookup"><span data-stu-id="46834-146">Then edit hello `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

<span data-ttu-id="46834-147">Para cada DiagnosticSource desea tootrace, agregue una entrada con hello `Name` toohello nombre de su DiagnosticSource del conjunto de atributos.</span><span class="sxs-lookup"><span data-stu-id="46834-147">For each DiagnosticSource you want tootrace, add an entry with hello `Name` attribute  set toohello name of your DiagnosticSource.</span></span>

## <a name="using-etw-events"></a><span data-ttu-id="46834-148">Uso de eventos ETW</span><span class="sxs-lookup"><span data-stu-id="46834-148">Using ETW events</span></span>
<span data-ttu-id="46834-149">Puede configurar toobe de eventos ETW enviado tooApplication visión como seguimientos.</span><span class="sxs-lookup"><span data-stu-id="46834-149">You can configure ETW events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="46834-150">En primer lugar, instale hello `Microsoft.ApplicationInsights.EtwCollector` paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="46834-150">First, install hello `Microsoft.ApplicationInsights.EtwCollector` NuGet package.</span></span> <span data-ttu-id="46834-151">A continuación, edite `TelemetryModules` sección de hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) archivo.</span><span class="sxs-lookup"><span data-stu-id="46834-151">Then edit `TelemetryModules` section of hello [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) file.</span></span>

> [!NOTE] 
> <span data-ttu-id="46834-152">Solo se pueden recopilar eventos ETW si Hola Hola de hospedaje de proceso SDK se está ejecutando bajo una identidad que sea miembro de "Usuarios del registro de rendimiento" o los administradores.</span><span class="sxs-lookup"><span data-stu-id="46834-152">ETW events can only be collected if hello process hosting hello SDK is running under an identity that is a member of "Performance Log Users" or Administrators.</span></span>

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

<span data-ttu-id="46834-153">Para cada origen, puede establecer Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="46834-153">For each source, you can set hello following parameters:</span></span>
 * <span data-ttu-id="46834-154">`ProviderName`es el nombre de Hola de toocollect de proveedor ETW de Hola.</span><span class="sxs-lookup"><span data-stu-id="46834-154">`ProviderName` is hello name of hello ETW provider toocollect.</span></span>
 * <span data-ttu-id="46834-155">`ProviderGuid`Especifica Hola GUID de hello toocollect de proveedor ETW, se puede utilizar en lugar de `ProviderName`.</span><span class="sxs-lookup"><span data-stu-id="46834-155">`ProviderGuid` specifies hello GUID of hello ETW provider toocollect, can be used instead of `ProviderName`.</span></span>
 * <span data-ttu-id="46834-156">`Level`establece hello toocollect de nivel de registro.</span><span class="sxs-lookup"><span data-stu-id="46834-156">`Level` sets hello logging level toocollect.</span></span> <span data-ttu-id="46834-157">Puede ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` o `Warning`.</span><span class="sxs-lookup"><span data-stu-id="46834-157">Can be one of `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.</span></span>
 * <span data-ttu-id="46834-158">`Keywords`Valor entero de la palabra clave combinaciones toouse Hola a conjuntos (opcionales).</span><span class="sxs-lookup"><span data-stu-id="46834-158">`Keywords` (Optional) sets hello integer value of keyword combinations toouse.</span></span>

## <a name="using-hello-trace-api-directly"></a><span data-ttu-id="46834-159">Directamente con la API de seguimiento de Hola</span><span class="sxs-lookup"><span data-stu-id="46834-159">Using hello Trace API directly</span></span>
<span data-ttu-id="46834-160">Puede llamar directamente a API de seguimiento de hello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="46834-160">You can call hello Application Insights trace API directly.</span></span> <span data-ttu-id="46834-161">los adaptadores de registro de Hello utilizan esta API.</span><span class="sxs-lookup"><span data-stu-id="46834-161">hello logging adapters use this API.</span></span>

<span data-ttu-id="46834-162">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="46834-162">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

<span data-ttu-id="46834-163">La ventaja de TrackTrace es que puede colocar datos relativamente largos en mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="46834-163">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="46834-164">Por ejemplo, aquí podría codificar datos POST.</span><span class="sxs-lookup"><span data-stu-id="46834-164">For example, you could encode POST data there.</span></span>

<span data-ttu-id="46834-165">Además, puede agregar un mensaje de tooyour de nivel de gravedad.</span><span class="sxs-lookup"><span data-stu-id="46834-165">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="46834-166">Y, al igual que otros telemetría, puede agregar valores de propiedad que se puede utilizar toohelp filtrar o buscar para diferentes conjuntos de seguimientos.</span><span class="sxs-lookup"><span data-stu-id="46834-166">And, like other telemetry, you can add property values that you can use toohelp filter or search for different sets of traces.</span></span> <span data-ttu-id="46834-167">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="46834-167">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="46834-168">Esto permitiría que, en [búsqueda][diagnostic], tooeasily filtrar todos los mensajes de saludo de un nivel de gravedad determinado relacionados con la base de datos determinada tooa.</span><span class="sxs-lookup"><span data-stu-id="46834-168">This would enable you, in [Search][diagnostic], tooeasily filter out all hello messages of a particular severity level relating tooa particular database.</span></span>

## <a name="explore-your-logs"></a><span data-ttu-id="46834-169">Explorar los registros</span><span class="sxs-lookup"><span data-stu-id="46834-169">Explore your logs</span></span>
<span data-ttu-id="46834-170">Ejecute la aplicación, ya sea en modo de depuración o mediante su implementación para que esté activa.</span><span class="sxs-lookup"><span data-stu-id="46834-170">Run your app, either in debug mode or deploy it live.</span></span>

<span data-ttu-id="46834-171">En la hoja de información general de la aplicación en [portal de Application Insights hello][portal], elija [búsqueda][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="46834-171">In your app's overview blade in [hello Application Insights portal][portal], choose [Search][diagnostic].</span></span>

![En Application Insights, elija Buscar.](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Búsqueda](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

<span data-ttu-id="46834-174">Por ejemplo, puede:</span><span class="sxs-lookup"><span data-stu-id="46834-174">You can, for example:</span></span>

* <span data-ttu-id="46834-175">Filtrar por seguimientos de registro, o por elementos con determinadas propiedades</span><span class="sxs-lookup"><span data-stu-id="46834-175">Filter on log traces, or on items with specific properties</span></span>
* <span data-ttu-id="46834-176">Inspeccionar un elemento específico en detalle</span><span class="sxs-lookup"><span data-stu-id="46834-176">Inspect a specific item in detail.</span></span>
* <span data-ttu-id="46834-177">Buscar otra telemetría relacionada con toohello misma solicitud de usuario (es decir, con Hola mismo OperationId)</span><span class="sxs-lookup"><span data-stu-id="46834-177">Find other telemetry relating toohello same user request (that is, with hello same OperationId)</span></span>
* <span data-ttu-id="46834-178">Guardar configuración de Hola de esta página como favorito</span><span class="sxs-lookup"><span data-stu-id="46834-178">Save hello configuration of this page as a Favorite</span></span>

> [!NOTE]
> <span data-ttu-id="46834-179">**Muestreo.**</span><span class="sxs-lookup"><span data-stu-id="46834-179">**Sampling.**</span></span> <span data-ttu-id="46834-180">Si la aplicación envía una gran cantidad de datos y utilizas Hola Application Insights SDK para ASP.NET versión 2.0.0-beta3 o posterior, característica de muestreo adaptativo de hello puede operar y enviar solamente un porcentaje de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="46834-180">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="46834-181">Aprenda más sobre el muestreo.</span><span class="sxs-lookup"><span data-stu-id="46834-181">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <a name="next-steps"></a><span data-ttu-id="46834-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46834-182">Next steps</span></span>
<span data-ttu-id="46834-183">[Diagnóstico de errores y excepciones en ASP.NET][exceptions]</span><span class="sxs-lookup"><span data-stu-id="46834-183">[Diagnose failures and exceptions in ASP.NET][exceptions]</span></span>

<span data-ttu-id="46834-184">[Aprenda más sobre la búsqueda][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="46834-184">[Learn more about Search][diagnostic].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="46834-185">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="46834-185">Troubleshooting</span></span>
### <a name="how-do-i-do-this-for-java"></a><span data-ttu-id="46834-186">¿Cómo se puede hacer para Java?</span><span class="sxs-lookup"><span data-stu-id="46834-186">How do I do this for Java?</span></span>
<span data-ttu-id="46834-187">Hola de uso [adaptadores de registro de Java](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="46834-187">Use hello [Java log adapters](app-insights-java-trace-logs.md).</span></span>

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a><span data-ttu-id="46834-188">No hay ninguna opción de Application Insights en el menú contextual del proyecto Hola</span><span class="sxs-lookup"><span data-stu-id="46834-188">There's no Application Insights option on hello project context menu</span></span>
* <span data-ttu-id="46834-189">Compruebe si las herramientas de Application Insights están instaladas en este equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="46834-189">Check Application Insights tools is installed on this development machine.</span></span> <span data-ttu-id="46834-190">En el menú Herramientas de Visual Studio, en Extensiones y actualizaciones, busque Herramientas de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="46834-190">In Visual Studio menu Tools, Extensions and Updates, look for Application Insights Tools.</span></span> <span data-ttu-id="46834-191">Si no se encuentra en la ficha de hello instalado, abra hello en línea pestaña e instálelo.</span><span class="sxs-lookup"><span data-stu-id="46834-191">If it isn't in hello Installed tab, open hello Online tab and install it.</span></span>
* <span data-ttu-id="46834-192">Podría tratarse de un tipo de proyecto no admitido por las herramientas de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="46834-192">This might be a type of project not supported by Application Insights tools.</span></span> <span data-ttu-id="46834-193">Use la [instalación manual](#manual-installation).</span><span class="sxs-lookup"><span data-stu-id="46834-193">Use [manual installation](#manual-installation).</span></span>

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a><span data-ttu-id="46834-194">Ninguna opción de adaptador de registro en la herramienta de configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="46834-194">No log adapter option in hello configuration tool</span></span>
* <span data-ttu-id="46834-195">En primer lugar debe marco de registro de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="46834-195">You need tooinstall hello logging framework first.</span></span>
* <span data-ttu-id="46834-196">Si usa System.Diagnostics.Trace, asegúrese de que lo ha [configurado en `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="46834-196">If you're using System.Diagnostics.Trace, make sure you [configured it in `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).</span></span>
* <span data-ttu-id="46834-197">¿Tengo versión más reciente de Hola de Application Insights?</span><span class="sxs-lookup"><span data-stu-id="46834-197">Have you got hello latest version of Application Insights?</span></span> <span data-ttu-id="46834-198">En Visual Studio **herramientas** menú, elija **extensiones y actualizaciones**, abra hello y **actualizaciones** ficha. Si hay herramientas de análisis de desarrollador, haga clic en tooupdate se.</span><span class="sxs-lookup"><span data-stu-id="46834-198">In Visual Studio **Tools** menu, choose **Extensions and Updates**, and open hello **Updates** tab. If Developer Analytics tools is there, click tooupdate it.</span></span>

### <span data-ttu-id="46834-199"><a name="emptykey"></a>Aparece el mensaje de error "La clave de instrumentación no puede estar vacía".</span><span class="sxs-lookup"><span data-stu-id="46834-199"><a name="emptykey"></a>I get an error "Instrumentation key cannot be empty"</span></span>
<span data-ttu-id="46834-200">Parece que instaló Hola registro paquete Nuget de adaptador sin tener que instalar Application Insights.</span><span class="sxs-lookup"><span data-stu-id="46834-200">Looks like you installed hello logging adapter Nuget package without installing Application Insights.</span></span>

<span data-ttu-id="46834-201">En el Explorador de soluciones, haga clic con el botón derecho en `ApplicationInsights.config` y elija **Actualizar Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="46834-201">In Solution Explorer, right-click `ApplicationInsights.config` and choose **Update Application Insights**.</span></span> <span data-ttu-id="46834-202">Obtendrá un cuadro de diálogo que le invita toosign en tooAzure y cree un recurso de Application Insights, o volver a utilizar uno existente.</span><span class="sxs-lookup"><span data-stu-id="46834-202">You'll get a dialog that invites you toosign in tooAzure and either create an Application Insights resource, or re-use an existing one.</span></span> <span data-ttu-id="46834-203">Esto debería solucionarlo.</span><span class="sxs-lookup"><span data-stu-id="46834-203">That should fix it.</span></span>

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a><span data-ttu-id="46834-204">Puedo ver seguimientos en la búsqueda de diagnóstico, pero no Hola otros eventos</span><span class="sxs-lookup"><span data-stu-id="46834-204">I can see traces in diagnostic search, but not hello other events</span></span>
<span data-ttu-id="46834-205">A veces puede tardar unos instantes para todos los tooget Hola de eventos y las solicitudes a través de la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="46834-205">It can sometimes take a while for all hello events and requests tooget through hello pipeline.</span></span>

### <span data-ttu-id="46834-206"><a name="limits"></a>¿Qué cantidad de datos se conserva?</span><span class="sxs-lookup"><span data-stu-id="46834-206"><a name="limits"></a>How much data is retained?</span></span>
<span data-ttu-id="46834-207">Varios factores afectan a cantidad Hola de los datos almacenados.</span><span class="sxs-lookup"><span data-stu-id="46834-207">Several factors impact hello amount of data retained.</span></span> <span data-ttu-id="46834-208">Vea hello [límites](app-insights-api-custom-events-metrics.md#limits) sección de página de las métricas de eventos de cliente de Hola para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="46834-208">See hello [limits](app-insights-api-custom-events-metrics.md#limits) section of hello customer event metrics page for more information.</span></span> 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a><span data-ttu-id="46834-209">No veo algunas entradas del registro de hello que espero</span><span class="sxs-lookup"><span data-stu-id="46834-209">I'm not seeing some of hello log entries that I expect</span></span>
<span data-ttu-id="46834-210">Si la aplicación envía una gran cantidad de datos y utilizas Hola Application Insights SDK para ASP.NET versión 2.0.0-beta3 o posterior, característica de muestreo adaptativo de hello puede operar y enviar solamente un porcentaje de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="46834-210">If your application sends a lot of data and you are using hello Application Insights SDK for ASP.NET version 2.0.0-beta3 or later, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> [<span data-ttu-id="46834-211">Aprenda más sobre el muestreo.</span><span class="sxs-lookup"><span data-stu-id="46834-211">Learn more about sampling.</span></span>](app-insights-sampling.md)

## <span data-ttu-id="46834-212"><a name="add"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="46834-212"><a name="add"></a>Next steps</span></span>
* <span data-ttu-id="46834-213">[Configuración de pruebas de disponibilidad y de capacidad de respuesta][availability]</span><span class="sxs-lookup"><span data-stu-id="46834-213">[Set up availability and responsiveness tests][availability]</span></span>
* <span data-ttu-id="46834-214">[Solución de problemas][qna]</span><span class="sxs-lookup"><span data-stu-id="46834-214">[Troubleshooting][qna]</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
