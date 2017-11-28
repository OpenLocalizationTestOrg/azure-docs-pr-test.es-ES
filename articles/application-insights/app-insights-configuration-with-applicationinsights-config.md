---
title: 'Referencia de ApplicationInsights.config: Azure | Microsoft Docs'
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
ms.openlocfilehash: 7737f47d4181b5e920434f3a5372991efb58f63e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-the-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a><span data-ttu-id="aae65-103">Configuración del SDK de Application Insights con ApplicationInsights.config o .xml</span><span class="sxs-lookup"><span data-stu-id="aae65-103">Configuring the Application Insights SDK with ApplicationInsights.config or .xml</span></span>
<span data-ttu-id="aae65-104">El SDK de Application Insights para .NET consta de varios paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="aae65-104">The Application Insights .NET SDK consists of a number of NuGet packages.</span></span> <span data-ttu-id="aae65-105">El [paquete principal](http://www.nuget.org/packages/Microsoft.ApplicationInsights) proporciona la API para enviar telemetría a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aae65-105">The [core package](http://www.nuget.org/packages/Microsoft.ApplicationInsights) provides the API for sending telemetry to the Application Insights.</span></span> <span data-ttu-id="aae65-106">Los [paquetes adicionales](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) proporcionan *módulos* e *inicializadores* de telemetría para hacer un seguimiento automático de la aplicación y su contexto.</span><span class="sxs-lookup"><span data-stu-id="aae65-106">[Additional packages](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) provide telemetry *modules* and *initializers* for automatically tracking telemetry from your application and its context.</span></span> <span data-ttu-id="aae65-107">Si ajusta el archivo de configuración, puede habilitar o deshabilitar los módulos e inicializadores de telemetría, y establecer los parámetros para algunos de ellos.</span><span class="sxs-lookup"><span data-stu-id="aae65-107">By adjusting the configuration file, you can enable or disable telemetry modules and initializers, and set parameters for some of them.</span></span>

<span data-ttu-id="aae65-108">El archivo de configuración se denomina `ApplicationInsights.config` o `ApplicationInsights.xml`, dependiendo del tipo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="aae65-108">The configuration file is named `ApplicationInsights.config` or `ApplicationInsights.xml`, depending on the type of your application.</span></span> <span data-ttu-id="aae65-109">Se agrega automáticamente al proyecto cuando se [instalan la mayoría de las versiones del SDK][start].</span><span class="sxs-lookup"><span data-stu-id="aae65-109">It is automatically added to your project when you [install most versions of the SDK][start].</span></span> <span data-ttu-id="aae65-110">También se agrega a una aplicación web con el [Monitor de estado en un servidor IIS][redfield] o al seleccionar la [extensión de Application Insights para un sitio web o una máquina virtual de Azure](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="aae65-110">It is also added to a web app by [Status Monitor on an IIS server][redfield], or when you select the Appplication Insights [extension for an Azure website or VM](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="aae65-111">No hay un archivo equivalente para controlar el [SDK en una página web][client].</span><span class="sxs-lookup"><span data-stu-id="aae65-111">There isn't an equivalent file to control the [SDK in a web page][client].</span></span>

<span data-ttu-id="aae65-112">En este documento se describen las secciones que verá en el archivo de configuración, cómo controlan los componentes del SDK y qué paquetes NuGet cargan esos componentes.</span><span class="sxs-lookup"><span data-stu-id="aae65-112">This document describes the sections you see in the configuration file, how they control the components of the SDK, and which NuGet packages load those components.</span></span>

## <a name="telemetry-modules-aspnet"></a><span data-ttu-id="aae65-113">Módulos de telemetría (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="aae65-113">Telemetry Modules (ASP.NET)</span></span>
<span data-ttu-id="aae65-114">Cada módulo de telemetría recopila un tipo específico de datos y usa la API principal para enviar dichos datos.</span><span class="sxs-lookup"><span data-stu-id="aae65-114">Each telemetry module collects a specific type of data and uses the core API to send the data.</span></span> <span data-ttu-id="aae65-115">Los módulos los instalan diferentes paquetes NuGet, que también agregan las líneas necesarias al archivo .config.</span><span class="sxs-lookup"><span data-stu-id="aae65-115">The modules are installed by different NuGet packages, which also add the required lines to the .config file.</span></span>

<span data-ttu-id="aae65-116">Hay un nodo en el archivo de configuración para cada módulo.</span><span class="sxs-lookup"><span data-stu-id="aae65-116">There's a node in the configuration file for each module.</span></span> <span data-ttu-id="aae65-117">Para deshabilitar un módulo, elimine el nodo o conviértalo en comentario.</span><span class="sxs-lookup"><span data-stu-id="aae65-117">To disable a module, delete the node or comment it out.</span></span>

### <a name="dependency-tracking"></a><span data-ttu-id="aae65-118">Seguimiento de dependencia</span><span class="sxs-lookup"><span data-stu-id="aae65-118">Dependency Tracking</span></span>
<span data-ttu-id="aae65-119">[Dependency tracking](app-insights-asp-net-dependencies.md) recopila la telemetría sobre las llamadas que realiza la aplicación a bases de datos y a servicios y bases de datos externos.</span><span class="sxs-lookup"><span data-stu-id="aae65-119">[Dependency tracking](app-insights-asp-net-dependencies.md) collects telemetry about calls your app makes to databases and external services and databases.</span></span> <span data-ttu-id="aae65-120">Para permitir que este módulo funcione en un servidor IIS, deberá [instalar el Monitor de estado][redfield].</span><span class="sxs-lookup"><span data-stu-id="aae65-120">To allow this module to work in an IIS server, you need to [install Status Monitor][redfield].</span></span> <span data-ttu-id="aae65-121">Para utilizarlo en aplicaciones web o máquinas virtuales de Azure, [seleccione la extensión Application Insights](app-insights-azure-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="aae65-121">To use it in Azure web apps or VMs, [select the Application Insights extension](app-insights-azure-web-apps.md).</span></span>

<span data-ttu-id="aae65-122">También puede escribir su propio código de seguimiento de dependencias con la [API de TrackDependency](app-insights-api-custom-events-metrics.md#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="aae65-122">You can also write your own dependency tracking code using the [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).</span></span>

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* <span data-ttu-id="aae65-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .</span><span class="sxs-lookup"><span data-stu-id="aae65-123">[Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) NuGet package.</span></span>

### <a name="performance-collector"></a><span data-ttu-id="aae65-124">Recopilador de rendimiento</span><span class="sxs-lookup"><span data-stu-id="aae65-124">Performance collector</span></span>
<span data-ttu-id="aae65-125">[Recopila contadores de rendimiento del sistema](app-insights-performance-counters.md) como CPU, memoria y carga de la red desde instalaciones de IIS.</span><span class="sxs-lookup"><span data-stu-id="aae65-125">[Collects system performance counters](app-insights-performance-counters.md) such as CPU, memory and network load from IIS installations.</span></span> <span data-ttu-id="aae65-126">Puede especificar qué contadores recopilar, incluidos los contadores de rendimiento que ha configurado usted mismo.</span><span class="sxs-lookup"><span data-stu-id="aae65-126">You can specify which counters to collect, including performance counters you have set up yourself.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* <span data-ttu-id="aae65-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .</span><span class="sxs-lookup"><span data-stu-id="aae65-127">[Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) NuGet package.</span></span>

### <a name="application-insights-diagnostics-telemetry"></a><span data-ttu-id="aae65-128">Telemetría de diagnósticos de Application Insights</span><span class="sxs-lookup"><span data-stu-id="aae65-128">Application Insights Diagnostics Telemetry</span></span>
<span data-ttu-id="aae65-129">`DiagnosticsTelemetryModule` informa de errores en el propio código de instrumentación de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aae65-129">The `DiagnosticsTelemetryModule` reports errors in the Application Insights instrumentation code itself.</span></span> <span data-ttu-id="aae65-130">Por ejemplo, si el código no puede tener acceso a los contadores de rendimiento o si un `ITelemetryInitializer` inicia una excepción.</span><span class="sxs-lookup"><span data-stu-id="aae65-130">For example, if the code cannot access performance counters or if an `ITelemetryInitializer` throws an exception.</span></span> <span data-ttu-id="aae65-131">La telemetría de seguimiento que sigue este módulo aparece en la [Búsqueda de diagnóstico][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="aae65-131">Trace telemetry tracked by this module appears in the [Diagnostic Search][diagnostic].</span></span> <span data-ttu-id="aae65-132">Envía datos de diagnóstico a dc.services.vsallin.net.</span><span class="sxs-lookup"><span data-stu-id="aae65-132">Sends diagnostic data to dc.services.vsallin.net.</span></span>

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* <span data-ttu-id="aae65-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="aae65-133">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="aae65-134">Si solamente se instala este paquete, el archivo ApplicationInsights.config no se crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="aae65-134">If you only install this package, the ApplicationInsights.config file is not automatically created.</span></span>

### <a name="developer-mode"></a><span data-ttu-id="aae65-135">Modo de programador</span><span class="sxs-lookup"><span data-stu-id="aae65-135">Developer Mode</span></span>
<span data-ttu-id="aae65-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` fuerza al `TelemetryChannel` de Application Insights a enviar los datos inmediatamente, elemento de telemetría a elemento, cuando se adjunta un depurador al proceso de aplicación.</span><span class="sxs-lookup"><span data-stu-id="aae65-136">`DeveloperModeWithDebuggerAttachedTelemetryModule` forces the Application Insights `TelemetryChannel` to send data immediately, one telemetry item at a time, when a debugger is attached to the application process.</span></span> <span data-ttu-id="aae65-137">Esto reduce la cantidad de tiempo entre el momento en que la aplicación realiza un seguimiento de telemetría y el momento en que esta aparece en el portal de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aae65-137">This reduces the amount of time between the moment when your application tracks telemetry and when it appears on the Application Insights portal.</span></span> <span data-ttu-id="aae65-138">Esto provoca una sobrecarga considerable en la CPU y el ancho de banda.</span><span class="sxs-lookup"><span data-stu-id="aae65-138">It causes significant overhead in CPU and network bandwidth.</span></span>

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* <span data-ttu-id="aae65-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) </span><span class="sxs-lookup"><span data-stu-id="aae65-139">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package</span></span>

### <a name="web-request-tracking"></a><span data-ttu-id="aae65-140">Seguimiento de solicitud web</span><span class="sxs-lookup"><span data-stu-id="aae65-140">Web Request Tracking</span></span>
<span data-ttu-id="aae65-141">Informa del [tiempo de respuesta y del código del resultado](app-insights-asp-net.md) de solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="aae65-141">Reports the [response time and result code](app-insights-asp-net.md) of HTTP requests.</span></span>

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* <span data-ttu-id="aae65-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) </span><span class="sxs-lookup"><span data-stu-id="aae65-142">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>

### <a name="exception-tracking"></a><span data-ttu-id="aae65-143">Seguimiento de excepciones</span><span class="sxs-lookup"><span data-stu-id="aae65-143">Exception tracking</span></span>
<span data-ttu-id="aae65-144">`ExceptionTrackingTelemetryModule` realiza excepciones no controladas en la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="aae65-144">`ExceptionTrackingTelemetryModule` tracks unhandled exceptions in your web app.</span></span> <span data-ttu-id="aae65-145">Consulte [Errores y excepciones][exceptions].</span><span class="sxs-lookup"><span data-stu-id="aae65-145">See [Failures and exceptions][exceptions].</span></span>

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* <span data-ttu-id="aae65-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) </span><span class="sxs-lookup"><span data-stu-id="aae65-146">[Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) NuGet package</span></span>
* <span data-ttu-id="aae65-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - Realiza un seguimiento de [excepciones de tareas inadvertidas](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span><span class="sxs-lookup"><span data-stu-id="aae65-147">`Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` - tracks [unobserved task exceptions](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).</span></span>
* <span data-ttu-id="aae65-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - Realiza un seguimiento de excepciones no controladas para roles de trabajo, servicios de Windows y aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="aae65-148">`Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` - tracks unhandled exceptions for worker roles, windows services, and console applications.</span></span>
* <span data-ttu-id="aae65-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .</span><span class="sxs-lookup"><span data-stu-id="aae65-149">[Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) NuGet package.</span></span>

### <a name="eventsource-tracking"></a><span data-ttu-id="aae65-150">Seguimiento de EventSource</span><span class="sxs-lookup"><span data-stu-id="aae65-150">EventSource Tracking</span></span>
<span data-ttu-id="aae65-151">`EventSourceTelemetryModule` permite configurar eventos EventSource para enviarse a Application Insights como seguimientos.</span><span class="sxs-lookup"><span data-stu-id="aae65-151">`EventSourceTelemetryModule` allows you to configure EventSource events to be sent to Application Insights as traces.</span></span> <span data-ttu-id="aae65-152">Para obtener información sobre el seguimiento de eventos EventSource, vea [Uso de eventos EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span><span class="sxs-lookup"><span data-stu-id="aae65-152">For information on tracking EventSource events, see [Using EventSource Events](app-insights-asp-net-trace-logs.md#using-eventsource-events).</span></span>

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [<span data-ttu-id="aae65-153">Microsoft.ApplicationInsights.EventSourceListener</span><span class="sxs-lookup"><span data-stu-id="aae65-153">Microsoft.ApplicationInsights.EventSourceListener</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a><span data-ttu-id="aae65-154">Seguimiento de eventos ETW</span><span class="sxs-lookup"><span data-stu-id="aae65-154">ETW Event Tracking</span></span>
<span data-ttu-id="aae65-155">`EtwCollectorTelemetryModule` permite configurar eventos de proveedores ETW para enviarse a Application Insights como seguimientos.</span><span class="sxs-lookup"><span data-stu-id="aae65-155">`EtwCollectorTelemetryModule` allows you to configure events from ETW providers to be sent to Application Insights as traces.</span></span> <span data-ttu-id="aae65-156">Para obtener información sobre el seguimiento de eventos ETW de seguimiento, vea [Uso de eventos ETW](app-insights-asp-net-trace-logs.md#using-etw-events).</span><span class="sxs-lookup"><span data-stu-id="aae65-156">For information on tracking ETW events, see [Using ETW Events](app-insights-asp-net-trace-logs.md#using-etw-events).</span></span>

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [<span data-ttu-id="aae65-157">Microsoft.ApplicationInsights.EtwCollector</span><span class="sxs-lookup"><span data-stu-id="aae65-157">Microsoft.ApplicationInsights.EtwCollector</span></span>](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a><span data-ttu-id="aae65-158">Microsoft.ApplicationInsights</span><span class="sxs-lookup"><span data-stu-id="aae65-158">Microsoft.ApplicationInsights</span></span>
<span data-ttu-id="aae65-159">El paquete Microsoft.ApplicationInsights proporciona la [API principal](https://msdn.microsoft.com/library/mt420197.aspx) del SDK.</span><span class="sxs-lookup"><span data-stu-id="aae65-159">The Microsoft.ApplicationInsights package provides the [core API](https://msdn.microsoft.com/library/mt420197.aspx) of the SDK.</span></span> <span data-ttu-id="aae65-160">Los otros módulos de telemetría usan esto y también puede [usarlo usted mismo para definir su propia telemetría](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="aae65-160">The other telemetry modules use this, and you can also [use it to define your own telemetry](app-insights-api-custom-events-metrics.md).</span></span>

* <span data-ttu-id="aae65-161">No hay entrada en ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="aae65-161">No entry in ApplicationInsights.config.</span></span>
* <span data-ttu-id="aae65-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) .</span><span class="sxs-lookup"><span data-stu-id="aae65-162">[Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) NuGet package.</span></span> <span data-ttu-id="aae65-163">Si solamente instala este NuGet, no se genera ningún archivo .config.</span><span class="sxs-lookup"><span data-stu-id="aae65-163">If you just install this NuGet, no .config file is generated.</span></span>

## <a name="telemetry-channel"></a><span data-ttu-id="aae65-164">Canal de telemetría</span><span class="sxs-lookup"><span data-stu-id="aae65-164">Telemetry Channel</span></span>
<span data-ttu-id="aae65-165">El canal de telemetría administra el almacenamiento en búfer y la transmisión de telemetría al servicio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aae65-165">The telemetry channel manages buffering and transmission of telemetry to the Application Insights service.</span></span>

* <span data-ttu-id="aae65-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` es el canal predeterminado para servicios.</span><span class="sxs-lookup"><span data-stu-id="aae65-166">`Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel` is the default channel for services.</span></span> <span data-ttu-id="aae65-167">Almacena en búfer los datos de la memoria.</span><span class="sxs-lookup"><span data-stu-id="aae65-167">It buffers data in memory.</span></span>
* <span data-ttu-id="aae65-168">`Microsoft.ApplicationInsights.PersistenceChannel` es una alternativa para aplicaciones de consola.</span><span class="sxs-lookup"><span data-stu-id="aae65-168">`Microsoft.ApplicationInsights.PersistenceChannel` is an alternative for console applications.</span></span> <span data-ttu-id="aae65-169">Pueden guardar los datos no vaciados en almacenamiento persistente cuando la aplicación se cierre y se enviarán cuando la aplicación se inicie de nuevo.</span><span class="sxs-lookup"><span data-stu-id="aae65-169">It can save any unflushed data to persistent storage when your app closes down, and will send it when the app starts again.</span></span>

## <a name="telemetry-initializers-aspnet"></a><span data-ttu-id="aae65-170">Inicializadores de telemetría (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="aae65-170">Telemetry Initializers (ASP.NET)</span></span>
<span data-ttu-id="aae65-171">Los inicializadores de telemetría establecen propiedades de contexto que se envían junto con todos los elementos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="aae65-171">Telemetry initializers set context properties that are sent along with every item of telemetry.</span></span>

<span data-ttu-id="aae65-172">También puede [escribir sus propios inicializadores](app-insights-api-filtering-sampling.md#add-properties) para establecer propiedades de contexto.</span><span class="sxs-lookup"><span data-stu-id="aae65-172">You can [write your own initializers](app-insights-api-filtering-sampling.md#add-properties) to set context properties.</span></span>

<span data-ttu-id="aae65-173">Los inicializadores estándar están todos establecidos por los paquetes NuGet web o  WindowsServer:</span><span class="sxs-lookup"><span data-stu-id="aae65-173">The standard initializers are all set either by the Web or WindowsServer NuGet packages:</span></span>

* <span data-ttu-id="aae65-174">`AccountIdTelemetryInitializer` establece la propiedad AccountId.</span><span class="sxs-lookup"><span data-stu-id="aae65-174">`AccountIdTelemetryInitializer` sets the AccountId property.</span></span>
* <span data-ttu-id="aae65-175">`AuthenticatedUserIdTelemetryInitializer` establece la propiedad AuthenticatedUserId establecida por el SDK de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="aae65-175">`AuthenticatedUserIdTelemetryInitializer` sets the AuthenticatedUserId property as set by the JavaScript SDK.</span></span>
* <span data-ttu-id="aae65-176">`AzureRoleEnvironmentTelemetryInitializer` actualiza las propiedades `RoleName` y `RoleInstance` del contexto `Device` para todos los elementos de telemetría con información extraída del entorno de tiempo de ejecución de Azure.</span><span class="sxs-lookup"><span data-stu-id="aae65-176">`AzureRoleEnvironmentTelemetryInitializer` updates the `RoleName` and `RoleInstance` properties of the `Device` context for all telemetry items with information extracted from the Azure runtime environment.</span></span>
* <span data-ttu-id="aae65-177">`BuildInfoConfigComponentVersionTelemetryInitializer` actualiza la propiedad `Version` del contexto `Component` para todos los elementos de telemetría con el valor extraído del archivo `BuildInfo.config` que produce MS Build.</span><span class="sxs-lookup"><span data-stu-id="aae65-177">`BuildInfoConfigComponentVersionTelemetryInitializer` updates the `Version` property of the `Component` context for all telemetry items with the value extracted from the `BuildInfo.config` file produced by MS Build.</span></span>
* <span data-ttu-id="aae65-178">`ClientIpHeaderTelemetryInitializer` actualiza la propiedad `Ip` del contexto `Location` de todos los elementos de telemetría según el encabezado HTTP `X-Forwarded-For` de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="aae65-178">`ClientIpHeaderTelemetryInitializer` updates `Ip` property of the `Location` context of all telemetry items based on the `X-Forwarded-For` HTTP header of the request.</span></span>
* <span data-ttu-id="aae65-179">`DeviceTelemetryInitializer` actualiza las propiedades siguientes del contexto `Device` para todos los elementos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="aae65-179">`DeviceTelemetryInitializer` updates the following properties of the `Device` context for all telemetry items.</span></span>
  * <span data-ttu-id="aae65-180">`Type` se establece en "PC".</span><span class="sxs-lookup"><span data-stu-id="aae65-180">`Type` is set to "PC"</span></span>
  * <span data-ttu-id="aae65-181">`Id` se establece en el nombre de dominio del equipo donde se ejecuta la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="aae65-181">`Id` is set to the domain name of the computer where the web application is running.</span></span>
  * <span data-ttu-id="aae65-182">`OemName` se establece en el valor extraído del campo `Win32_ComputerSystem.Manufacturer` con WMI.</span><span class="sxs-lookup"><span data-stu-id="aae65-182">`OemName` is set to the value extracted from the `Win32_ComputerSystem.Manufacturer` field using WMI.</span></span>
  * <span data-ttu-id="aae65-183">`Model` se establece en el valor extraído del campo `Win32_ComputerSystem.Model` con WMI.</span><span class="sxs-lookup"><span data-stu-id="aae65-183">`Model` is set to the value extracted from the `Win32_ComputerSystem.Model` field using WMI.</span></span>
  * <span data-ttu-id="aae65-184">`NetworkType` se establece en el valor extraído de `NetworkInterface`.</span><span class="sxs-lookup"><span data-stu-id="aae65-184">`NetworkType` is set to the value extracted from the `NetworkInterface`.</span></span>
  * <span data-ttu-id="aae65-185">`Language` se establece en el nombre de `CurrentCulture`.</span><span class="sxs-lookup"><span data-stu-id="aae65-185">`Language` is set to the name of the `CurrentCulture`.</span></span>
* <span data-ttu-id="aae65-186">`DomainNameRoleInstanceTelemetryInitializer` actualiza la propiedad `RoleInstance` del contexto `Device` para todos los elementos de telemetría con el nombre de dominio del equipo donde se ejecuta la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="aae65-186">`DomainNameRoleInstanceTelemetryInitializer` updates the `RoleInstance` property of the `Device` context for all telemetry items with the domain name of the computer where the web application is running.</span></span>
* <span data-ttu-id="aae65-187">`OperationNameTelemetryInitializer` actualiza la propiedad `Name` de la propiedad `RequestTelemetry` y `Name` propiedad del contexto `Operation` de todos los elementos de telemetría según el método HTTP, así como los nombres del controlador MVC de ASP.NET y la acción que se invoca para procesar la solicitud.</span><span class="sxs-lookup"><span data-stu-id="aae65-187">`OperationNameTelemetryInitializer` updates the `Name` property of the `RequestTelemetry` and the `Name` property of the `Operation` context of all telemetry items based on the HTTP method, as well as names of ASP.NET MVC controller and action invoked to process the request.</span></span>
* <span data-ttu-id="aae65-188">`OperationIdTelemetryInitializer` o `OperationCorrelationTelemetryInitializer` actualizan la propiedad de contexto `Operation.Id` de todos los elementos de telemetría de los que se realiza un seguimiento mientras se controla una solicitud con el `RequestTelemetry.Id` que se genera.</span><span class="sxs-lookup"><span data-stu-id="aae65-188">`OperationIdTelemetryInitializer` or `OperationCorrelationTelemetryInitializer` updates the `Operation.Id` context property of all telemetry items tracked while handling a request with the automatically generated `RequestTelemetry.Id`.</span></span>
* <span data-ttu-id="aae65-189">`SessionTelemetryInitializer` actualiza la propiedad `Id` del contexto `Session` para todos los elementos de telemetría con valor extraído de la cookie `ai_session` que genera el código de instrumentación JavaScript de Application Insights que se ejecuta en el explorador del usuario.</span><span class="sxs-lookup"><span data-stu-id="aae65-189">`SessionTelemetryInitializer` updates the `Id` property of the `Session` context for all telemetry items with value extracted from the `ai_session` cookie generated by the ApplicationInsights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="aae65-190">`SyntheticTelemetryInitializer` o `SyntheticUserAgentTelemetryInitializer` actualizan las propiedades de los contextos `User`, `Session` y `Operation` de todos los elementos de telemetría de los que se realiza un seguimiento al tratar una solicitud de un origen sintético, como una prueba de disponibilidad o un bot de motor de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="aae65-190">`SyntheticTelemetryInitializer` or `SyntheticUserAgentTelemetryInitializer` updates the `User`, `Session` and `Operation` contexts properties of all telemetry items tracked when handling a request from a synthetic source, such as an availability test or search engine bot.</span></span> <span data-ttu-id="aae65-191">De forma predeterminada, [Explorador de métricas](app-insights-metrics-explorer.md) no muestra telemetría sintética.</span><span class="sxs-lookup"><span data-stu-id="aae65-191">By default, [Metrics Explorer](app-insights-metrics-explorer.md) does not display synthetic telemetry.</span></span>

    <span data-ttu-id="aae65-192">Conjunto de `<Filters>` que identifica las propiedades de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="aae65-192">The `<Filters>` set identifying properties of the requests.</span></span>
* <span data-ttu-id="aae65-193">`UserAgentTelemetryInitializer` actualiza la propiedad `UserAgent` del contexto `User` de todos los elementos de telemetría según el encabezado HTTP `User-Agent` de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="aae65-193">`UserAgentTelemetryInitializer` updates the `UserAgent` property of the `User` context of all telemetry items based on the `User-Agent` HTTP header of the request.</span></span>
* <span data-ttu-id="aae65-194">`UserTelemetryInitializer` actualiza las propiedades `Id` y `AcquisitionDate` del contexto `User` para todos los elementos de telemetría con valores extraídos de la cookie `ai_user` que genera el código de instrumentación JavaScript de Application Insights que se ejecuta en el explorador del usuario.</span><span class="sxs-lookup"><span data-stu-id="aae65-194">`UserTelemetryInitializer` updates the `Id` and `AcquisitionDate` properties of `User` context for all telemetry items with values extracted from the `ai_user` cookie generated by the Application Insights JavaScript instrumentation code running in the user's browser.</span></span>
* <span data-ttu-id="aae65-195">`WebTestTelemetryInitializer` establece el identificador de usuario, el identificador de sesión y las propiedades de origen sintético de las solicitudes HTTP que proceden de [pruebas de disponibilidad](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="aae65-195">`WebTestTelemetryInitializer` sets the user id, session id and synthetic source properties for HTTP requests that come from [availability tests](app-insights-monitor-web-app-availability.md).</span></span>
  <span data-ttu-id="aae65-196">Conjunto de `<Filters>` que identifica las propiedades de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="aae65-196">The `<Filters>` set identifying properties of the requests.</span></span>

<span data-ttu-id="aae65-197">Para aplicaciones de .NET que se ejecutan en Service Fabric, puede incluir el paquete de NuGet `Microsoft.ApplicationInsights.ServiceFabric`.</span><span class="sxs-lookup"><span data-stu-id="aae65-197">For .NET applications running in Service Fabric, you can include the `Microsoft.ApplicationInsights.ServiceFabric` NuGet package.</span></span> <span data-ttu-id="aae65-198">Este paquete incluye `FabricTelemetryInitializer`, que agrega propiedades de Service Fabric a elementos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="aae65-198">This package includes a `FabricTelemetryInitializer`, which adds Service Fabric properties to telemetry items.</span></span> <span data-ttu-id="aae65-199">Para obtener más información, consulte la [página de GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sobre las propiedades que agrega este paquete de NuGet.</span><span class="sxs-lookup"><span data-stu-id="aae65-199">For more information, see the [GitHub page](https://go.microsoft.com/fwlink/?linkid=848457) about the properties added by this NuGet package.</span></span>

## <a name="telemetry-processors-aspnet"></a><span data-ttu-id="aae65-200">Procesadores de telemetría (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="aae65-200">Telemetry Processors (ASP.NET)</span></span>
<span data-ttu-id="aae65-201">Los procesadores de telemetría pueden filtrar y modificar cada elemento de telemetría justo antes de que se envíe desde el SDK al portal.</span><span class="sxs-lookup"><span data-stu-id="aae65-201">Telemetry processors can filter and modify each telemetry item just before it is sent from the SDK to the portal.</span></span>

<span data-ttu-id="aae65-202">También puede [escribir sus propios procesadores de telemetría](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="aae65-202">You can [write your own telemetry processors](app-insights-api-filtering-sampling.md#filtering).</span></span>

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a><span data-ttu-id="aae65-203">Procesador de telemetría de muestreo adaptivo (desde 2.0.0-beta3)</span><span class="sxs-lookup"><span data-stu-id="aae65-203">Adaptive sampling telemetry processor (from 2.0.0-beta3)</span></span>
<span data-ttu-id="aae65-204">Esta opción está habilitada de manera predeterminada.</span><span class="sxs-lookup"><span data-stu-id="aae65-204">This is enabled by default.</span></span> <span data-ttu-id="aae65-205">Si la aplicación envía una gran cantidad de datos de telemetría, este procesador quita algunos de ellos.</span><span class="sxs-lookup"><span data-stu-id="aae65-205">If your app sends a lot of telemetry, this processor removes some of it.</span></span>

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="aae65-206">El parámetro proporciona el destino que el algoritmo intenta alcanzar.</span><span class="sxs-lookup"><span data-stu-id="aae65-206">The parameter provides the target that the algorithm tries to achieve.</span></span> <span data-ttu-id="aae65-207">Cada instancia del SDK funciona de forma independiente, por lo que si el servidor es un clúster de varios equipos, se multiplicará el volumen real de telemetría en consonancia.</span><span class="sxs-lookup"><span data-stu-id="aae65-207">Each instance of the SDK works independently, so if your server is a cluster of several machines, the actual volume of telemetry will be multiplied accordingly.</span></span>

<span data-ttu-id="aae65-208">[Obtenga más información sobre el muestreo](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="aae65-208">[Learn more about sampling](app-insights-sampling.md).</span></span>

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a><span data-ttu-id="aae65-209">Procesador de telemetría de muestreo de tasa fija (desde 2.0.0-beta1)</span><span class="sxs-lookup"><span data-stu-id="aae65-209">Fixed-rate sampling telemetry processor (from 2.0.0-beta1)</span></span>
<span data-ttu-id="aae65-210">También hay un [procesador de telemetría de muestreo](app-insights-api-filtering-sampling.md) estándar (desde 2.0.1):</span><span class="sxs-lookup"><span data-stu-id="aae65-210">There is also a standard [sampling telemetry processor](app-insights-api-filtering-sampling.md) (from 2.0.1):</span></span>

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close to 100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a><span data-ttu-id="aae65-211">Parámetros de canal (Java)</span><span class="sxs-lookup"><span data-stu-id="aae65-211">Channel parameters (Java)</span></span>
<span data-ttu-id="aae65-212">Estos parámetros afectan al modo en que el SDK de Java debe almacenar y vaciar los datos de telemetría que recopila.</span><span class="sxs-lookup"><span data-stu-id="aae65-212">These parameters affect how the Java SDK should store and flush the telemetry data that it collects.</span></span>

#### <a name="maxtelemetrybuffercapacity"></a><span data-ttu-id="aae65-213">MaxTelemetryBufferCapacity</span><span class="sxs-lookup"><span data-stu-id="aae65-213">MaxTelemetryBufferCapacity</span></span>
<span data-ttu-id="aae65-214">El número de elementos de telemetría que pueden almacenarse en el almacenamiento del SDK en memoria.</span><span class="sxs-lookup"><span data-stu-id="aae65-214">The number of telemetry items that can be stored in the SDK's in-memory storage.</span></span> <span data-ttu-id="aae65-215">Cuando se alcanza este número, se vacía el búfer de telemetría; es decir, los elementos de telemetría se envían al servidor de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aae65-215">When this number is reached, the telemetry buffer is flushed - that is, the telemetry items are sent to the Application Insights server.</span></span>

* <span data-ttu-id="aae65-216">Mín: 1</span><span class="sxs-lookup"><span data-stu-id="aae65-216">Min: 1</span></span>
* <span data-ttu-id="aae65-217">Máx: 1000</span><span class="sxs-lookup"><span data-stu-id="aae65-217">Max: 1000</span></span>
* <span data-ttu-id="aae65-218">Valor predeterminado: 500</span><span class="sxs-lookup"><span data-stu-id="aae65-218">Default: 500</span></span>

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a><span data-ttu-id="aae65-219">FlushIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="aae65-219">FlushIntervalInSeconds</span></span>
<span data-ttu-id="aae65-220">Determina la frecuencia con que los datos almacenados en el almacenamiento en memoria deben vaciarse (enviarse a Application Insights).</span><span class="sxs-lookup"><span data-stu-id="aae65-220">Determines how often the data that is stored in the in-memory storage should be flushed (sent to Application Insights).</span></span>

* <span data-ttu-id="aae65-221">Mín: 1</span><span class="sxs-lookup"><span data-stu-id="aae65-221">Min: 1</span></span>
* <span data-ttu-id="aae65-222">Máx: 300</span><span class="sxs-lookup"><span data-stu-id="aae65-222">Max: 300</span></span>
* <span data-ttu-id="aae65-223">Valor predeterminado: 5</span><span class="sxs-lookup"><span data-stu-id="aae65-223">Default: 5</span></span>

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a><span data-ttu-id="aae65-224">MaxTransmissionStorageCapacityInMB</span><span class="sxs-lookup"><span data-stu-id="aae65-224">MaxTransmissionStorageCapacityInMB</span></span>
<span data-ttu-id="aae65-225">Determina el tamaño máximo en MB que se asigna al almacenamiento persistente en el disco local.</span><span class="sxs-lookup"><span data-stu-id="aae65-225">Determines the maximum size in MB that is allotted to the persistent storage on the local disk.</span></span> <span data-ttu-id="aae65-226">Este almacenamiento se utiliza para conservar los elementos de telemetría que no pudieron transmitirse al extremo de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="aae65-226">This storage is used for persisting telemetry items that failed to be transmitted to the Application Insights endpoint.</span></span> <span data-ttu-id="aae65-227">Cuando se ha alcanzado el tamaño de almacenamiento, se descartarán los nuevos elementos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="aae65-227">When the storage size has been met, new telemetry items will be discarded.</span></span>

* <span data-ttu-id="aae65-228">Mín: 1</span><span class="sxs-lookup"><span data-stu-id="aae65-228">Min: 1</span></span>
* <span data-ttu-id="aae65-229">Máx: 100</span><span class="sxs-lookup"><span data-stu-id="aae65-229">Max: 100</span></span>
* <span data-ttu-id="aae65-230">Valor predeterminado: 10</span><span class="sxs-lookup"><span data-stu-id="aae65-230">Default: 10</span></span>

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a><span data-ttu-id="aae65-231">InstrumentationKey</span><span class="sxs-lookup"><span data-stu-id="aae65-231">InstrumentationKey</span></span>
<span data-ttu-id="aae65-232">Esto determina el recurso de Application Insights en el que aparecen los datos.</span><span class="sxs-lookup"><span data-stu-id="aae65-232">This determines the Application Insights resource in which your data appears.</span></span> <span data-ttu-id="aae65-233">Normalmente se crea un recurso independiente, con una clave independiente, para cada una de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="aae65-233">Typically you create a separate resource, with a separate key, for each of your applications.</span></span>

<span data-ttu-id="aae65-234">Si desea establecer la clave de forma dinámica (por ejemplo, si desea enviar los resultados de su aplicación a distintos recursos) puede omitir la clave del archivo de configuración y establecerla en el código.</span><span class="sxs-lookup"><span data-stu-id="aae65-234">If you want to set the key dynamically - for example if you want to send results from your application to different resources - you can omit the key from the configuration file, and set it in code instead.</span></span>

<span data-ttu-id="aae65-235">Para establecer la clave de todas las instancias de TelemetryClient, incluidos los módulos de telemetría estándar, establezca la clave en TelemetryConfiguration.Active.</span><span class="sxs-lookup"><span data-stu-id="aae65-235">To set the key for all instances of TelemetryClient, including standard telemetry modules, set the key in TelemetryConfiguration.Active.</span></span> <span data-ttu-id="aae65-236">Hágalo en un método de inicialización, como global.aspx.cs, en un servicio de ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="aae65-236">Do this in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

<span data-ttu-id="aae65-237">Si solo desea enviar un conjunto específico de eventos a un recurso diferente, puede establecer la clave para un TelemetryClient específico:</span><span class="sxs-lookup"><span data-stu-id="aae65-237">If you just want to send a specific set of events to a different resource, you can set the key for a specific TelemetryClient:</span></span>

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

<span data-ttu-id="aae65-238">Para obtener una nueva clave, [cree un nuevo recurso en el portal de Application Insights][new].</span><span class="sxs-lookup"><span data-stu-id="aae65-238">To get a new key, [create a new resource in the Application Insights portal][new].</span></span>

## <a name="next-steps"></a><span data-ttu-id="aae65-239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aae65-239">Next steps</span></span>
<span data-ttu-id="aae65-240">[Más información acerca de la API][api].</span><span class="sxs-lookup"><span data-stu-id="aae65-240">[Learn more about the API][api].</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
