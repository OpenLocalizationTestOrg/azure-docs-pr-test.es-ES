---
title: referencia de aaaApplicationInsights.config - Azure | Documentos de Microsoft
description: "Habilitación o deshabilitación de los módulos de recopilación de datos e incorporación de contadores de rendimiento y otros parámetros."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="106c9-103">Configurar Hola Application Insights SDK con ApplicationInsights.config o .xml</span><span class="sxs-lookup"><span data-stu-id="106c9-103">Configuring hello Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="106c9-104">Hola Application Insights .NET SDK está formado por un número de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="106c9-104">hello Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="106c9-105">El [paquete core](http://www.nuget.org/packages/Microsoft.ApplicationInsights) proporciona API de Hola para enviar telemetría a saludos Application Insights.</span><span class="sxs-lookup"><span data-stu-id="106c9-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides hello API for sending telemetry to hello Application Insights.</span></span> <span data-ttu-id="106c9-106">Los [paquetes adicionales](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) proporcionan *módulos* e *inicializadores* de telemetría para hacer un seguimiento automático de la aplicación y su contexto.</span><span class="sxs-lookup"><span data-stu-id="106c9-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="106c9-107">Ajustando el archivo de configuración de hello, puede habilitar o deshabilitar inicializadores y módulos de telemetría y establecer los parámetros para algunos de ellos.</span><span class="sxs-lookup"><span data-stu-id="106c9-107">By adjusting hello configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="106c9-108">se denomina archivo de configuración de Hello `ApplicationInsights.config` o `ApplicationInsights.xml`, según el tipo de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="106c9-108">hello configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on hello type of your application.</span></span> <span data-ttu-id="106c9-109">Se agrega automáticamente tooyour proyecto cuando se [instalar la mayoría de las versiones de SDK de hello][start].</span><span class="sxs-lookup"><span data-stu-id="106c9-109">It is automatically added tooyour project when you [install most versions of hello SDK][start].</span></span> <span data-ttu-id="106c9-110">También se agrega tooa aplicación web [Monitor de estado en un servidor IIS][redfield], o cuando se selecciona la visión de la aplicación de hello [extensión para un sitio Web de Azure o la máquina virtual](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="106c9-110">It is also added tooa web app by [Status Monitor on an IIS server][redfield], or when you select hello Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="106c9-111">No hay un Hola de toocontrol archivo equivalente [SDK en una página web][client].</span><span class="sxs-lookup"><span data-stu-id="106c9-111">There isn't an equivalent file toocontrol hello [SDK in a web page][client].</span></span>

<span data-ttu-id="106c9-112">Este documento describe secciones Hola que verá en la configuración de Hola de archivos, cómo controlan los componentes de Hola de hello SDK, y los paquetes de NuGet cargar esos componentes.</span><span class="sxs-lookup"><span data-stu-id="106c9-112">This document describes hello sections you see in hello configuration file, how they control hello components of hello SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="106c9-113">Módulos de telemetría (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="106c9-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="106c9-114">Cada módulo de telemetría recopila un tipo específico de datos y la usa core Hola datos de API toosend Hola.</span><span class="sxs-lookup"><span data-stu-id="106c9-114">Each telemetry module collects a specific type of data and uses hello core API toosend hello data.</span></span> <span data-ttu-id="106c9-115">Hola módulos se instalan diferentes paquetes de NuGet, que también agrega el archivo .config de hello líneas requeridas toohello.</span><span class="sxs-lookup"><span data-stu-id="106c9-115">hello modules are installed by different NuGet packages, which also add hello required lines toohello .config file.</span></span>

<span data-ttu-id="106c9-116">Hay un nodo en el archivo de configuración de Hola para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="106c9-116">There's a node in hello configuration file for each module.</span></span> <span data-ttu-id="106c9-117">toodisable un módulo, eliminar nodo de Hola o márquelo como comentario fuera.</span><span class="sxs-lookup"><span data-stu-id="106c9-117">toodisable a module, delete hello node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="106c9-118">Seguimiento de dependencia</span><span class="sxs-lookup"><span data-stu-id="106c9-118">Dependency Tracking</span></span>
<span data-ttu-id="106c9-119">[Seguimiento de dependencias](app-insights-asp-net-dependencies.md) recopila telemetría acerca de las llamadas que la aplicación realiza toodatabases y servicios externos y las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="106c9-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes toodatabases and external services and databases.</span></span> <span data-ttu-id="106c9-120">tooallow toowork de este módulo en un servidor IIS, necesita demasiado[instalar el Monitor de estado][redfield].</span><span class="sxs-lookup"><span data-stu-id="106c9-120">tooallow this module toowork in an IIS server, you need too[install Status Monitor][redfield].</span></span> <span data-ttu-id="106c9-121">toouse en aplicaciones web de Azure o máquinas virtuales, [Seleccionar extensión de Application Insights hello](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="106c9-121">toouse it in Azure web apps or VMs, [select hello Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="106c9-122">También puede escribir su propio código utilizando Hola de seguimiento de dependencias [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="106c9-122">You can also write your own dependency tracking code using hello [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="106c9-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .</span><span class="sxs-lookup"><span data-stu-id="106c9-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="106c9-124">Recopilador de rendimiento</span><span class="sxs-lookup"><span data-stu-id="106c9-124">Performance collector</span></span>
<span data-ttu-id="106c9-125">[Recopila contadores de rendimiento del sistema](app-insights-performance-counters.md) como CPU, memoria y carga de la red desde instalaciones de IIS.</span><span class="sxs-lookup"><span data-stu-id="106c9-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="106c9-126">Puede especificar qué toocollect contadores, incluidos los contadores de rendimiento que se ha configurado manualmente.</span><span class="sxs-lookup"><span data-stu-id="106c9-126">You can specify which counters toocollect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="106c9-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .</span><span class="sxs-lookup"><span data-stu-id="106c9-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="106c9-128">Telemetría de diagnósticos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="106c9-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="106c9-129">Hola `DiagnosticsTelemetryModule` informa de errores en el propio código de instrumentación Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="106c9-129">hello `DiagnosticsTelemetryModule` reports errors in hello Application Insights instrumentation code itself.</span></span> <span data-ttu-id="106c9-130">Por ejemplo, si el código de hello no puede tener acceso a los contadores de rendimiento o un `ITelemetryInitializer` produce una excepción.</span><span class="sxs-lookup"><span data-stu-id="106c9-130">For example, if hello code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="106c9-131">Realiza un seguimiento por este módulo de telemetría de seguimiento aparece en hello [búsqueda diagnóstico][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="106c9-131">Trace telemetry tracked by this module appears in hello [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="106c9-132">Envía datos de diagnóstico toodc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="106c9-132">Sends diagnostic data toodc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="106c9-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="106c9-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="106c9-134">Si instala solo este paquete, archivo de hello ApplicationInsights.config no se crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="106c9-134">If you only install this package, hello ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="106c9-135">Modo de programador</span><span class="sxs-lookup"><span data-stu-id="106c9-135">Developer Mode</span></span>
<span data-ttu-id="106c9-136">`DeveloperModeWithDebuggerAttachedTelemetryModule`fuerza Hola Application Insights `TelemetryChannel` toosend datos inmediatamente, elemento de telemetría de uno a la vez, cuando un depurador adjuntarán toohello proceso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="106c9-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces hello Application Insights `TelemetryChannel` toosend data immediately, one telemetry item at a time, when a debugger is attached toohello application process.</span></span> <span data-ttu-id="106c9-137">Esto reduce la cantidad de Hola de tiempo entre el momento de hello cuando la aplicación realiza un seguimiento de telemetría y cuando aparece en el portal de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="106c9-137">This reduces hello amount of time between hello moment when your application tracks telemetry and when it appears on hello Application Insights portal.</span></span> <span data-ttu-id="106c9-138">Esto provoca una sobrecarga considerable en la CPU y el ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="106c9-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="106c9-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/)</span><span class="sxs-lookup"><span data-stu-id="106c9-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="106c9-140">Seguimiento de solicitud web</span><span class="sxs-lookup"><span data-stu-id="106c9-140">Web Request Tracking</span></span>
<span data-ttu-id="106c9-141">Hola informes [código de tiempo y el resultado de la respuesta](app-insights-asp-net.md) de solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="106c9-141">Reports hello [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="106c9-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)</span><span class="sxs-lookup"><span data-stu-id="106c9-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="106c9-143">Seguimiento de excepciones</span><span class="sxs-lookup"><span data-stu-id="106c9-143">Exception tracking</span></span>
<span data-ttu-id="106c9-144">`ExceptionTrackingTelemetryModule` realiza excepciones no controladas en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="106c9-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="106c9-145">Consulte [Errores y excepciones][exceptions].</span><span class="sxs-lookup"><span data-stu-id="106c9-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="106c9-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web)</span><span class="sxs-lookup"><span data-stu-id="106c9-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="106c9-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - Realiza un seguimiento de [excepciones de tareas inadvertidas](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="106c9-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="106c9-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - Realiza un seguimiento de excepciones no controladas para roles de trabajo, servicios de Windows y aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="106c9-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="106c9-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .</span><span class="sxs-lookup"><span data-stu-id="106c9-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="106c9-150">Seguimiento de EventSource</span><span class="sxs-lookup"><span data-stu-id="106c9-150">EventSource Tracking</span></span>
<span data-ttu-id="106c9-151">`EventSourceTelemetryModule`le permite tooconfigure EventSource eventos toobe enviado tooApplication visión como seguimientos.</span><span class="sxs-lookup"><span data-stu-id="106c9-151">`EventSourceTelemetryModule` allows you tooconfigure EventSource events toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="106c9-152">Para obtener información sobre el seguimiento de eventos EventSource, vea [Uso de eventos EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="106c9-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="106c9-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="106c9-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="106c9-154">Seguimiento de eventos ETW</span><span class="sxs-lookup"><span data-stu-id="106c9-154">ETW Event Tracking</span></span>
<span data-ttu-id="106c9-155">`EtwCollectorTelemetryModule`le permite tooconfigure eventos de ETW proveedores toobe enviado tooApplication visión como seguimientos.</span><span class="sxs-lookup"><span data-stu-id="106c9-155">`EtwCollectorTelemetryModule` allows you tooconfigure events from ETW providers toobe sent tooApplication Insights as traces.</span></span> <span data-ttu-id="106c9-156">Para obtener información sobre el seguimiento de eventos ETW de seguimiento, vea [Uso de eventos ETW](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="106c9-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="106c9-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="106c9-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="106c9-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="106c9-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="106c9-159">paquete de Hola a Microsoft.ApplicationInsights proporciona hello [principales API](https://msdn.microsoft.com/library/mt420197.aspx) de hello SDK.</span><span class="sxs-lookup"><span data-stu-id="106c9-159">hello Microsoft.ApplicationInsights package provides hello [core API](https://msdn.microsoft.com/library/mt420197.aspx) of hello SDK.</span></span> <span data-ttu-id="106c9-160">Hello otros módulos de telemetría utilizan y también puede [usar toodefine su propio telemetría](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="106c9-160">hello other telemetry modules use this, and you can also [use it toodefine your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="106c9-161">No hay entrada en ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="106c9-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="106c9-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="106c9-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="106c9-163">Si solamente instala este NuGet, no se genera ningún archivo .config.</span><span class="sxs-lookup"><span data-stu-id="106c9-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="106c9-164">Canal de telemetría</span><span class="sxs-lookup"><span data-stu-id="106c9-164">Telemetry Channel</span></span>
<span data-ttu-id="106c9-165">canal de telemetría de Hello administra el almacenamiento en búfer y transmisión de telemetría toohello servicio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="106c9-165">hello telemetry channel manages buffering and transmission of telemetry toohello Application Insights service.</span></span>

* <span data-ttu-id="106c9-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`es el canal de hello predeterminado para los servicios.</span><span class="sxs-lookup"><span data-stu-id="106c9-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is hello default channel for services.</span></span> <span data-ttu-id="106c9-167">Almacena en búfer los datos de la memoria.</span><span class="sxs-lookup"><span data-stu-id="106c9-167">It buffers data in memory.</span></span>
* <span data-ttu-id="106c9-168">`Microsoft.ApplicationInsights.PersistenceChannel` es una alternativa para aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="106c9-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="106c9-169">Puede guardar cualquier almacenamiento de datos unflushed toopersistent cuando la aplicación cierra y enviará cuando la aplicación hello se inicia de nuevo.</span><span class="sxs-lookup"><span data-stu-id="106c9-169">It can save any unflushed data toopersistent storage when your app closes down, and will send it when hello app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="106c9-170">Inicializadores de telemetría (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="106c9-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="106c9-171">Los inicializadores de telemetría establecen propiedades de contexto que se envían junto con todos los elementos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="106c9-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="106c9-172">También puede [escribir sus propios inicializadores](app-insights-api-filtering-sampling.md#add-properties) tooset las propiedades de contexto.</span><span class="sxs-lookup"><span data-stu-id="106c9-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) tooset context properties.</span></span>

<span data-ttu-id="106c9-173">inicializadores de Hello estándar se configuraron todos haciendo hello Web o WindowsServer NuGet paquetes:</span><span class="sxs-lookup"><span data-stu-id="106c9-173">hello standard initializers are all set either by hello Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="106c9-174">`AccountIdTelemetryInitializer`establece la propiedad de identificador de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="106c9-174">`AccountIdTelemetryInitializer` sets hello AccountId property.</span></span>
* <span data-ttu-id="106c9-175">`AuthenticatedUserIdTelemetryInitializer`establece hello AuthenticatedUserId propiedad como conjunto Hola SDK de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="106c9-175">`AuthenticatedUserIdTelemetryInitializer` sets hello AuthenticatedUserId property as set by hello JavaScript SDK.</span></span>
* <span data-ttu-id="106c9-176">`AzureRoleEnvironmentTelemetryInitializer`Hola actualizaciones `RoleName` y `RoleInstance` propiedades de hello `Device` contexto para todos los elementos de telemetría con la información extraída del entorno de Azure en tiempo de ejecución de Hola.</span><span class="sxs-lookup"><span data-stu-id="106c9-176">`AzureRoleEnvironmentTelemetryInitializer` updates hello `RoleName` and `RoleInstance` properties of hello `Device` context for all telemetry items with information extracted from hello Azure runtime environment.</span></span>
* <span data-ttu-id="106c9-177">`BuildInfoConfigComponentVersionTelemetryInitializer`Hola actualizaciones `Version` propiedad de hello `Component` contexto para todos los elementos de telemetría con valor de hello extraído de hello `BuildInfo.config` archivo generado por MS Build.</span><span class="sxs-lookup"><span data-stu-id="106c9-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates hello `Version` property of hello `Component` context for all telemetry items with hello value extracted from hello `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="106c9-178">`ClientIpHeaderTelemetryInitializer`actualizaciones `Ip` propiedad de hello `Location` según el contexto de todos los elementos de telemetría hello `X-Forwarded-For` encabezado HTTP de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="106c9-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of hello `Location` context of all telemetry items based on hello `X-Forwarded-For` HTTP header of hello request.</span></span>
* <span data-ttu-id="106c9-179">`DeviceTelemetryInitializer`Hola de las actualizaciones siguientes propiedades de hello `Device` contexto para todos los elementos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="106c9-179">`DeviceTelemetryInitializer` updates hello following properties of hello `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="106c9-180">`Type`se establece demasiado "PC"</span><span class="sxs-lookup"><span data-stu-id="106c9-180">`Type` is set too"PC"</span></span>
  * <span data-ttu-id="106c9-181">`Id`se establece toohello nombre de dominio Hola equipo donde se ejecuta la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="106c9-181">`Id` is set toohello domain name of hello computer where hello web application is running.</span></span>
  * <span data-ttu-id="106c9-182">`OemName`está establecido el valor de toohello extraído de hello `Win32_ComputerSystem.Manufacturer` campo mediante WMI.</span><span class="sxs-lookup"><span data-stu-id="106c9-182">`OemName` is set toohello value extracted from hello `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="106c9-183">`Model`está establecido el valor de toohello extraído de hello `Win32_ComputerSystem.Model` campo mediante WMI.</span><span class="sxs-lookup"><span data-stu-id="106c9-183">`Model` is set toohello value extracted from hello `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="106c9-184">`NetworkType`está establecido el valor de toohello extraído de hello `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="106c9-184">`NetworkType` is set toohello value extracted from hello `NetworkInterface`.</span></span>
  * <span data-ttu-id="106c9-185">`Language`se establece el nombre toohello de hello `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="106c9-185">`Language` is set toohello name of hello `CurrentCulture`.</span></span>
* <span data-ttu-id="106c9-186">`DomainNameRoleInstanceTelemetryInitializer`Hola actualizaciones `RoleInstance` propiedad de hello `Device` contexto para todos los elementos de telemetría con el nombre de dominio de hello del equipo de Hola donde se ejecuta la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="106c9-186">`DomainNameRoleInstanceTelemetryInitializer` updates hello `RoleInstance` property of hello `Device` context for all telemetry items with hello domain name of hello computer where hello web application is running.</span></span>
* <span data-ttu-id="106c9-187">`OperationNameTelemetryInitializer`Hola actualizaciones `Name` propiedad de hello `RequestTelemetry` hello y `Name` propiedad de hello `Operation` contexto de todos los elementos de telemetría basado en método hello HTTP, así como nombres de Hola de tooprocess invocado de acción y controlador de MVC de ASP.NET solicitud.</span><span class="sxs-lookup"><span data-stu-id="106c9-187">`OperationNameTelemetryInitializer` updates hello `Name` property of hello `RequestTelemetry` and hello `Name` property of hello `Operation` context of all telemetry items based on hello HTTP method, as well as names of ASP.NET MVC controller and action invoked tooprocess hello request.</span></span>
* <span data-ttu-id="106c9-188">`OperationIdTelemetryInitializer`o `OperationCorrelationTelemetryInitializer` Hola actualizaciones `Operation.Id` realiza el seguimiento de propiedad de contexto de todos los elementos de telemetría al controlar una solicitud con hello generada automáticamente `RequestTelemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="106c9-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates hello `Operation.Id` context property of all telemetry items tracked while handling a request with hello automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="106c9-189">`SessionTelemetryInitializer`Hola actualizaciones `Id` propiedad de hello `Session` contexto para todos los elementos de telemetría con valor extraído de hello `ai_session` cookie generados por hello código de instrumentación ApplicationInsights JavaScript ejecuta en el explorador del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="106c9-189">`SessionTelemetryInitializer` updates hello `Id` property of hello `Session` context for all telemetry items with value extracted from hello `ai_session` cookie generated by hello ApplicationInsights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="106c9-190">`SyntheticTelemetryInitializer`o `SyntheticUserAgentTelemetryInitializer` Hola actualizaciones `User`, `Session` y `Operation` realiza el seguimiento de propiedades de contextos de todos los elementos de telemetría cuando controla una solicitud de una fuente sintética, como una disponibilidad de prueba o bot de motor de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="106c9-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates hello `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="106c9-191">De forma predeterminada, [Explorador de métricas](app-insights-metrics-explorer.md) no muestra telemetría sintética.</span><span class="sxs-lookup"><span data-stu-id="106c9-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="106c9-192">Hola `<Filters>` establece la identificación de propiedades de las solicitudes de Hola.</span><span class="sxs-lookup"><span data-stu-id="106c9-192">hello `<Filters>` set identifying properties of hello requests.</span></span>
* <span data-ttu-id="106c9-193">`UserAgentTelemetryInitializer`Hola actualizaciones `UserAgent` propiedad de hello `User` según el contexto de todos los elementos de telemetría hello `User-Agent` encabezado HTTP de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="106c9-193">`UserAgentTelemetryInitializer` updates hello `UserAgent` property of hello `User` context of all telemetry items based on hello `User-Agent` HTTP header of hello request.</span></span>
* <span data-ttu-id="106c9-194">`UserTelemetryInitializer`Hola actualizaciones `Id` y `AcquisitionDate` propiedades de `User` contexto para todos los elementos de telemetría con los valores extraídos de hello `ai_user` cookie generada por código de instrumentación de Application Insights JavaScript Hola ejecutando Hola explorador del usuario.</span><span class="sxs-lookup"><span data-stu-id="106c9-194">`UserTelemetryInitializer` updates hello `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from hello `ai_user` cookie generated by hello Application Insights JavaScript instrumentation code running in hello user's browser.</span></span>
* <span data-ttu-id="106c9-195">`WebTestTelemetryInitializer`conjuntos de Hola Id. de usuario, Id. de sesión y propiedades de origen sintético para solicitudes HTTP que vienen de [pruebas de disponibilidad](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="106c9-195">`WebTestTelemetryInitializer` sets hello user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="106c9-196">Hola `<Filters>` establece la identificación de propiedades de las solicitudes de Hola.</span><span class="sxs-lookup"><span data-stu-id="106c9-196">hello `<Filters>` set identifying properties of hello requests.</span></span>

<span data-ttu-id="106c9-197">Para aplicaciones de .NET que se ejecutan en el tejido de servicio, puede incluir hello `Microsoft.ApplicationInsights.ServiceFabric` paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="106c9-197">For .NET applications running in Service Fabric, you can include hello `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="106c9-198">Este paquete incluye un `FabricTelemetryInitializer`, que agrega elementos de tootelemetry de propiedades de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="106c9-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties tootelemetry items.</span></span> <span data-ttu-id="106c9-199">Para obtener más información, vea hello [página de GitHub](https://go.microsoft.com/fwlink/?linkid=848457) acerca de las propiedades de hello agregadas por este paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="106c9-199">For more information, see hello [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about hello properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="106c9-200">Procesadores de telemetría (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="106c9-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="106c9-201">Pueden filtrar y modificar cada elemento de telemetría justo antes de que se envía desde el portal de hello SDK toohello procesadores de telemetría.</span><span class="sxs-lookup"><span data-stu-id="106c9-201">Telemetry processors can filter and modify each telemetry item just before it is sent from hello SDK toohello portal.</span></span>

<span data-ttu-id="106c9-202">También puede [escribir sus propios procesadores de telemetría](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="106c9-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="106c9-203">Procesador de telemetría de muestreo adaptivo (desde 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="106c9-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="106c9-204">Esta opción está habilitada de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="106c9-204">This is enabled by default.</span></span> <span data-ttu-id="106c9-205">Si la aplicación envía una gran cantidad de datos de telemetría, este procesador quita algunos de ellos.</span><span class="sxs-lookup"><span data-stu-id="106c9-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="106c9-206">parámetro Hello proporciona destino Hola Hola algoritmo intenta tooachieve.</span><span class="sxs-lookup"><span data-stu-id="106c9-206">hello parameter provides hello target that hello algorithm tries tooachieve.</span></span> <span data-ttu-id="106c9-207">Cada instancia de hello SDK funciona de forma independiente, por lo que si el servidor es un clúster de varios equipos, el volumen real de Hola de telemetría se multiplicará según corresponda.</span><span class="sxs-lookup"><span data-stu-id="106c9-207">Each instance of hello SDK works independently, so if your server is a cluster of several machines, hello actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="106c9-208">[Obtenga más información sobre el muestreo](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="106c9-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="106c9-209">Procesador de telemetría de muestreo de tasa fija (desde 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="106c9-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="106c9-210">También hay un [procesador de telemetría de muestreo](app-insights-api-filtering-sampling.md) estándar (desde 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="106c9-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="106c9-211">Parámetros de canal (Java)</span><span class="sxs-lookup"><span data-stu-id="106c9-211">Channel parameters (Java)</span></span>
<span data-ttu-id="106c9-212">Estos parámetros afectan a cómo debe almacenar y vaciar los datos de telemetría de Hola que recopila Hola SDK de Java.</span><span class="sxs-lookup"><span data-stu-id="106c9-212">These parameters affect how hello Java SDK should store and flush hello telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="106c9-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="106c9-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="106c9-214">número de Hola de elementos de telemetría que pueden almacenarse en el almacenamiento en memoria del SDK de Hola.</span><span class="sxs-lookup"><span data-stu-id="106c9-214">hello number of telemetry items that can be stored in hello SDK's in-memory storage.</span></span> <span data-ttu-id="106c9-215">Cuando se alcanza este número, se vacía el búfer de telemetría de hello: es decir, los elementos de telemetría de Hola se envían toohello servidor de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="106c9-215">When this number is reached, hello telemetry buffer is flushed - that is, hello telemetry items are sent toohello Application Insights server.</span></span>

* <span data-ttu-id="106c9-216">Mín: 1</span><span class="sxs-lookup"><span data-stu-id="106c9-216">Min: 1</span></span>
* <span data-ttu-id="106c9-217">Máx: 1000</span><span class="sxs-lookup"><span data-stu-id="106c9-217">Max: 1000</span></span>
* <span data-ttu-id="106c9-218">Valor predeterminado: 500</span><span class="sxs-lookup"><span data-stu-id="106c9-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="106c9-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="106c9-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="106c9-220">Determina la frecuencia con hello datos que están almacenados en el almacenamiento en memoria de Hola deberían estar vació (enviado tooApplication visión).</span><span class="sxs-lookup"><span data-stu-id="106c9-220">Determines how often hello data that is stored in hello in-memory storage should be flushed (sent tooApplication Insights).</span></span>

* <span data-ttu-id="106c9-221">Mín: 1</span><span class="sxs-lookup"><span data-stu-id="106c9-221">Min: 1</span></span>
* <span data-ttu-id="106c9-222">Máx: 300</span><span class="sxs-lookup"><span data-stu-id="106c9-222">Max: 300</span></span>
* <span data-ttu-id="106c9-223">Valor predeterminado: 5</span><span class="sxs-lookup"><span data-stu-id="106c9-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="106c9-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="106c9-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="106c9-225">Determina el tamaño máximo de hello en MB que se asigna a un almacenamiento persistente en el disco local de hello toohello.</span><span class="sxs-lookup"><span data-stu-id="106c9-225">Determines hello maximum size in MB that is allotted toohello persistent storage on hello local disk.</span></span> <span data-ttu-id="106c9-226">Este almacenamiento se utiliza para almacenar elementos de telemetría que dieron error toobe transmitida toohello Application Insights extremo.</span><span class="sxs-lookup"><span data-stu-id="106c9-226">This storage is used for persisting telemetry items that failed toobe transmitted toohello Application Insights endpoint.</span></span> <span data-ttu-id="106c9-227">Cuando se ha cumplido el tamaño de almacenamiento de hello, se descartarán los nuevos elementos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="106c9-227">When hello storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="106c9-228">Mín: 1</span><span class="sxs-lookup"><span data-stu-id="106c9-228">Min: 1</span></span>
* <span data-ttu-id="106c9-229">Máx: 100</span><span class="sxs-lookup"><span data-stu-id="106c9-229">Max: 100</span></span>
* <span data-ttu-id="106c9-230">Valor predeterminado: 10</span><span class="sxs-lookup"><span data-stu-id="106c9-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="106c9-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="106c9-231">InstrumentationKey</span></span>
<span data-ttu-id="106c9-232">Esto determina los recursos de Application Insights de hello en el que aparecen los datos.</span><span class="sxs-lookup"><span data-stu-id="106c9-232">This determines hello Application Insights resource in which your data appears.</span></span> <span data-ttu-id="106c9-233">Normalmente se crea un recurso independiente, con una clave independiente, para cada una de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="106c9-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="106c9-234">Si desea tooset Hola clave dinámicamente: por ejemplo, si desea que los resultados de toosend de sus recursos de aplicación toodifferent - puede omitir clave Hola Hola del archivo de configuración y establecer en el código.</span><span class="sxs-lookup"><span data-stu-id="106c9-234">If you want tooset hello key dynamically - for example if you want toosend results from your application toodifferent resources - you can omit hello key from hello configuration file, and set it in code instead.</span></span>

<span data-ttu-id="106c9-235">clave de hello tooset para todas las instancias de TelemetryClient, incluidos los módulos de telemetría estándar, Establece clave hello en TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="106c9-235">tooset hello key for all instances of TelemetryClient, including standard telemetry modules, set hello key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="106c9-236">Hágalo en un método de inicialización, como global.aspx.cs, en un servicio de ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="106c9-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="106c9-237">Si su intención es toosend un conjunto específico de recursos distinto de tooa de eventos, puede establecer clave Hola para un TelemetryClient específica:</span><span class="sxs-lookup"><span data-stu-id="106c9-237">If you just want toosend a specific set of events tooa different resource, you can set hello key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="106c9-238">una nueva clave, tooget [crear un nuevo recurso en el portal de Application Insights hello][new].</span><span class="sxs-lookup"><span data-stu-id="106c9-238">tooget a new key, [create a new resource in hello Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="106c9-239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="106c9-239">Next steps</span></span>
<span data-ttu-id="106c9-240">[Obtener más información sobre la API de hello][api].</span><span class="sxs-lookup"><span data-stu-id="106c9-240">[Learn more about hello API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
