---
title: "Secuencia de métricas con métricas personalizadas y diagnósticos en Azure Application Insights aaaLive | Documentos de Microsoft"
description: "Supervise la aplicación web en tiempo real con métricas personalizadas y diagnostique problemas con una fuente directa de errores, seguimientos y eventos."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 1f471176-38f3-40b3-bc6d-3f47d0cbaaa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: bwren
ms.openlocfilehash: 68ddfbf387379ea778c20280c4ec96baa06d3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="live-metrics-stream-monitor--diagnose-with-1-second-latency"></a><span data-ttu-id="8e392-103">Live Metrics Stream: supervisión y diagnóstico con una latencia de 1 segundo</span><span class="sxs-lookup"><span data-stu-id="8e392-103">Live Metrics Stream: Monitor & Diagnose with 1-second latency</span></span> 

<span data-ttu-id="8e392-104">Sondeo de núcleo de latidos de hello de la aplicación web en directo, en producción mediante el uso de la secuencia en directo de las métricas de [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e392-104">Probe hello beating heart of your live, in-production web application by using Live Metrics Stream from [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="8e392-105">Seleccionar y filtrar las métricas y rendimiento toowatch de contadores en tiempo real, sin ningún servicio de tooyour alteraciones.</span><span class="sxs-lookup"><span data-stu-id="8e392-105">Select and filter metrics and performance counters toowatch in real time, without any disturbance tooyour service.</span></span> <span data-ttu-id="8e392-106">Inspeccione seguimientos de la pila procedentes de ejemplos de errores de solicitudes y excepciones.</span><span class="sxs-lookup"><span data-stu-id="8e392-106">Inspect stack traces from sample failed requests and exceptions.</span></span> <span data-ttu-id="8e392-107">Junto con [Profiler](app-insights-profiler.md), el [depurador de instantáneas](app-insights-snapshot-debugger.md) y la [prueba de rendimiento](app-insights-monitor-web-app-availability.md#performance-tests), Live Metrics Stream proporciona una herramienta de diagnóstico eficaz y no invasiva para sitios web activos.</span><span class="sxs-lookup"><span data-stu-id="8e392-107">Together with [Profiler](app-insights-profiler.md), [Snapshot debugger](app-insights-snapshot-debugger.md), and [performance testing](app-insights-monitor-web-app-availability.md#performance-tests),  Live Metrics Stream provides a powerful and non-invasive diagnostic tool for your live web site.</span></span>

<span data-ttu-id="8e392-108">Con Live Metrics Stream, puede:</span><span class="sxs-lookup"><span data-stu-id="8e392-108">With Live Metrics Stream, you can:</span></span>

* <span data-ttu-id="8e392-109">Inspeccionar el rendimiento y los recuentos de errores mientras se publica una solución para validarla.</span><span class="sxs-lookup"><span data-stu-id="8e392-109">Validate a fix while it is released, by watching performance and failure counts.</span></span>
* <span data-ttu-id="8e392-110">Ver el efecto de Hola de probar las cargas máximas y diagnosticar problemas en vivo.</span><span class="sxs-lookup"><span data-stu-id="8e392-110">Watch hello effect of test loads, and diagnose issues live.</span></span> 
* <span data-ttu-id="8e392-111">Centrarse en las sesiones de pruebas determinado o filtrar los problemas conocidos, seleccionar y filtrar las métricas de hello desea toowatch.</span><span class="sxs-lookup"><span data-stu-id="8e392-111">Focus on particular test sessions or filter out known issues, by selecting and filtering hello metrics you want toowatch.</span></span>
* <span data-ttu-id="8e392-112">Obtener seguimientos de las excepciones cuando se produzcan.</span><span class="sxs-lookup"><span data-stu-id="8e392-112">Get exception traces as they happen.</span></span>
* <span data-ttu-id="8e392-113">Experimente con filtros toofind Hola KPI más relevantes.</span><span class="sxs-lookup"><span data-stu-id="8e392-113">Experiment with filters toofind hello most relevant KPIs.</span></span>
* <span data-ttu-id="8e392-114">Supervisar cualquier contador de rendimiento de Windows en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="8e392-114">Monitor any Windows performance counter live.</span></span>
* <span data-ttu-id="8e392-115">Fácilmente identificar un servidor que tiene problemas y filtrar Hola todos los KPI/live toojust fuente ese servidor.</span><span class="sxs-lookup"><span data-stu-id="8e392-115">Easily identify a server that is having issues, and filter all hello KPI/live feed toojust that server.</span></span>

<span data-ttu-id="8e392-116">[![Vídeo de Live Metrics Stream](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span><span class="sxs-lookup"><span data-stu-id="8e392-116">[![Live Metrics Stream video](./media/app-insights-live-stream/youtube.png)](https://www.youtube.com/watch?v=zqfHf1Oi5PY)</span></span>

<span data-ttu-id="8e392-117">Secuencia en directo de métricas está actualmente disponible en aplicaciones ASP.NET que se ejecutan en local o en hello en la nube.</span><span class="sxs-lookup"><span data-stu-id="8e392-117">Live Metrics Stream is currently available on ASP.NET apps running on-premises or in hello Cloud.</span></span> 

## <a name="get-started"></a><span data-ttu-id="8e392-118">Primeros pasos</span><span class="sxs-lookup"><span data-stu-id="8e392-118">Get started</span></span>

1. <span data-ttu-id="8e392-119">Si aún no ha [instalado Application Insights](app-insights-asp-net.md) en la aplicación web de ASP.NET o la [aplicación de Windows Server](app-insights-windows-services.md), hágalo ahora.</span><span class="sxs-lookup"><span data-stu-id="8e392-119">If you haven't yet [installed Application Insights](app-insights-asp-net.md) in your ASP.NET web app or [Windows server app](app-insights-windows-services.md), do that now.</span></span> 
2. <span data-ttu-id="8e392-120">**Una versión más reciente de actualización toohello** del paquete de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="8e392-120">**Update toohello latest version** of hello Application Insights package.</span></span> <span data-ttu-id="8e392-121">En Visual Studio, haga clic con el botón derecho en el proyecto y elija **Administrar paquetes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8e392-121">In Visual Studio, right-click your project and choose **Manage Nuget packages**.</span></span> <span data-ttu-id="8e392-122">Hola abierto **actualizaciones** ficha, verificación **incluir versión preliminar**y seleccione todos los paquetes de Microsoft.ApplicationInsights.* Hola.</span><span class="sxs-lookup"><span data-stu-id="8e392-122">Open hello **Updates** tab, check **Include prerelease**, and select all hello Microsoft.ApplicationInsights.* packages.</span></span>

    <span data-ttu-id="8e392-123">Vuelva a implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8e392-123">Redeploy your app.</span></span>

3. <span data-ttu-id="8e392-124">Hola [portal de Azure](https://portal.azure.com), abra el recurso de Application Insights de hello para la aplicación y, a continuación, abra la secuencia en directo.</span><span class="sxs-lookup"><span data-stu-id="8e392-124">In hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open Live Stream.</span></span>

4. <span data-ttu-id="8e392-125">[Canal de control seguro hello](#secure-the-control-channel) si puede usar los datos confidenciales como nombres de cliente en los filtros.</span><span class="sxs-lookup"><span data-stu-id="8e392-125">[Secure hello control channel](#secure-the-control-channel) if you might use sensitive data such as customer names in your filters.</span></span>


![En la hoja de información general de hello, haga clic en secuencia en directo](./media/app-insights-live-stream/live-stream-2.png)

### <a name="no-data-check-your-server-firewall"></a><span data-ttu-id="8e392-127">¿No hay datos?</span><span class="sxs-lookup"><span data-stu-id="8e392-127">No data?</span></span> <span data-ttu-id="8e392-128">Comprobación del firewall del servidor</span><span class="sxs-lookup"><span data-stu-id="8e392-128">Check your server firewall</span></span>

<span data-ttu-id="8e392-129">Comprobar hello [puertos de salida de la secuencia en directo de métricas](app-insights-ip-addresses.md#outgoing-ports) están abiertos en firewall de Hola de los servidores.</span><span class="sxs-lookup"><span data-stu-id="8e392-129">Check hello [outgoing ports for Live Metrics Stream](app-insights-ip-addresses.md#outgoing-ports) are open in hello firewall of your servers.</span></span> 


## <a name="how-does-live-metrics-stream-differ-from-metrics-explorer-and-analytics"></a><span data-ttu-id="8e392-130">¿En qué se diferencia Live Metrics Stream de Explorador de métricas y Analytics?</span><span class="sxs-lookup"><span data-stu-id="8e392-130">How does Live Metrics Stream differ from Metrics Explorer and Analytics?</span></span>

| |<span data-ttu-id="8e392-131">Live Stream</span><span class="sxs-lookup"><span data-stu-id="8e392-131">Live Stream</span></span> | <span data-ttu-id="8e392-132">Explorador de métricas y Analytics</span><span class="sxs-lookup"><span data-stu-id="8e392-132">Metrics Explorer and Analytics</span></span> |
|---|---|---|
|<span data-ttu-id="8e392-133">Latency</span><span class="sxs-lookup"><span data-stu-id="8e392-133">Latency</span></span>|<span data-ttu-id="8e392-134">Los datos se muestran en un segundo.</span><span class="sxs-lookup"><span data-stu-id="8e392-134">Data displayed within one second</span></span>|<span data-ttu-id="8e392-135">La agregación se realiza en minutos.</span><span class="sxs-lookup"><span data-stu-id="8e392-135">Aggregated over minutes</span></span>|
|<span data-ttu-id="8e392-136">Sin retención</span><span class="sxs-lookup"><span data-stu-id="8e392-136">No retention</span></span>|<span data-ttu-id="8e392-137">Datos que se conservan mientras se está en el gráfico de hello y, a continuación, se descartan</span><span class="sxs-lookup"><span data-stu-id="8e392-137">Data persists while it's on hello chart, and is then discarded</span></span>|[<span data-ttu-id="8e392-138">Los datos se conservan durante 90 días.</span><span class="sxs-lookup"><span data-stu-id="8e392-138">Data retained for 90 days</span></span>](app-insights-data-retention-privacy.md#how-long-is-the-data-kept)|
|<span data-ttu-id="8e392-139">A petición</span><span class="sxs-lookup"><span data-stu-id="8e392-139">On demand</span></span>|<span data-ttu-id="8e392-140">Se transmiten datos mientras se abre Live Metrics.</span><span class="sxs-lookup"><span data-stu-id="8e392-140">Data is streamed while you open Live Metrics</span></span>|<span data-ttu-id="8e392-141">Los datos se envían cuando Hola SDK está instalado y habilitado</span><span class="sxs-lookup"><span data-stu-id="8e392-141">Data is sent whenever hello SDK is installed and enabled</span></span>|
|<span data-ttu-id="8e392-142">Gratuito</span><span class="sxs-lookup"><span data-stu-id="8e392-142">Free</span></span>|<span data-ttu-id="8e392-143">No se efectúa ningún cargo por los datos de Live Stream.</span><span class="sxs-lookup"><span data-stu-id="8e392-143">There is no charge for Live Stream data</span></span>|<span data-ttu-id="8e392-144">Asunto demasiado[precios](app-insights-pricing.md)</span><span class="sxs-lookup"><span data-stu-id="8e392-144">Subject too[pricing](app-insights-pricing.md)</span></span>
|<span data-ttu-id="8e392-145">muestreo</span><span class="sxs-lookup"><span data-stu-id="8e392-145">Sampling</span></span>|<span data-ttu-id="8e392-146">Se transmiten todas las métricas y los contadores seleccionados.</span><span class="sxs-lookup"><span data-stu-id="8e392-146">All selected metrics and counters are transmitted.</span></span> <span data-ttu-id="8e392-147">Se muestrean los errores y seguimientos de la pila.</span><span class="sxs-lookup"><span data-stu-id="8e392-147">Failures and stack traces are sampled.</span></span> <span data-ttu-id="8e392-148">No se aplican elementos TelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="8e392-148">TelemetryProcessors are not applied.</span></span>|<span data-ttu-id="8e392-149">Se pueden [muestrear](app-insights-api-filtering-sampling.md) eventos.</span><span class="sxs-lookup"><span data-stu-id="8e392-149">Events may be [sampled](app-insights-api-filtering-sampling.md)</span></span>|
|<span data-ttu-id="8e392-150">Canal de control</span><span class="sxs-lookup"><span data-stu-id="8e392-150">Control channel</span></span>|<span data-ttu-id="8e392-151">Las señales de control de filtro se envían toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="8e392-151">Filter control signals are sent toohello SDK.</span></span> <span data-ttu-id="8e392-152">Se recomienda [proteger este canal](#secure-channel).</span><span class="sxs-lookup"><span data-stu-id="8e392-152">We recommend you [secure this channel](#secure-channel).</span></span>|<span data-ttu-id="8e392-153">La comunicación es unidireccional, toohello portal</span><span class="sxs-lookup"><span data-stu-id="8e392-153">Communication is one-way, toohello portal</span></span>|


## <a name="select-and-filter-your-metrics"></a><span data-ttu-id="8e392-154">Selección y filtrado de métricas</span><span class="sxs-lookup"><span data-stu-id="8e392-154">Select and filter your metrics</span></span>

<span data-ttu-id="8e392-155">(Disponible en clásico aplicaciones ASP.NET con Hola SDK más reciente.)</span><span class="sxs-lookup"><span data-stu-id="8e392-155">(Available on classic ASP.NET apps with hello latest SDK.)</span></span>

<span data-ttu-id="8e392-156">Puede supervisar KPI personalizado en vivo aplicando filtros arbitrarios en cualquier telemetría de Application Insights desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e392-156">You can monitor custom KPI live by applying arbitrary filters on any Application Insights telemetry from hello portal.</span></span> <span data-ttu-id="8e392-157">Haga clic en el control de filtro de Hola que muestra al pasar el mouse cualquiera de los gráficos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e392-157">Click hello filter control that shows when you mouse-over any of hello charts.</span></span> <span data-ttu-id="8e392-158">Hola después de gráfico es trazar un número de solicitudes personalizado KPI con filtros en atributos de dirección URL y la duración.</span><span class="sxs-lookup"><span data-stu-id="8e392-158">hello following chart is plotting a custom Request count KPI with filters on URL and Duration attributes.</span></span> <span data-ttu-id="8e392-159">Validar los filtros con hello sección de vista previa de flujo que muestra una fuente directa de telemetría que coincida con los criterios de Hola que ha especificado en cualquier momento en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="8e392-159">Validate your filters with hello Stream Preview section that shows a live feed of telemetry that matches hello criteria you have specified at any point in time.</span></span> 

![KPI personalizado de solicitudes](./media/app-insights-live-stream/live-stream-filteredMetric.png)

<span data-ttu-id="8e392-161">Puede supervisar un valor que no sea el de recuento.</span><span class="sxs-lookup"><span data-stu-id="8e392-161">You can monitor a value different from Count.</span></span> <span data-ttu-id="8e392-162">Opciones de Hello dependen de tipo hello de secuencia, que puede ser cualquier telemetría de Application Insights: solicitudes, dependencias, excepciones, seguimientos, eventos o las métricas.</span><span class="sxs-lookup"><span data-stu-id="8e392-162">hello options depend on hello type of stream, which could be any Application Insights telemetry: requests, dependencies, exceptions, traces, events, or metrics.</span></span> <span data-ttu-id="8e392-163">Puede ser su propia [medida personalizada](app-insights-api-custom-events-metrics.md#properties):</span><span class="sxs-lookup"><span data-stu-id="8e392-163">It can be your own [custom measurement](app-insights-api-custom-events-metrics.md#properties):</span></span>

![Opciones de valor](./media/app-insights-live-stream/live-stream-valueoptions.png)

<span data-ttu-id="8e392-165">Además tooApplication telemetría de visión, también puede supervisar cualquier contador de rendimiento de Windows seleccionando de opciones de flujo de Hola y proporcionar nombre Hola Hola del contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="8e392-165">In addition tooApplication Insights telemetry, you can also monitor any Windows performance counter by selecting that from hello stream options, and providing hello name of hello performance counter.</span></span>

<span data-ttu-id="8e392-166">Las métricas activas se agregan en dos puntos: localmente en cada servidor y, a continuación, en todos los servidores.</span><span class="sxs-lookup"><span data-stu-id="8e392-166">Live metrics are aggregated at two points: locally on each server, and then across all servers.</span></span> <span data-ttu-id="8e392-167">Puede cambiar predeterminado de hello en seleccionando otras opciones en hello respectivos listas desplegables.</span><span class="sxs-lookup"><span data-stu-id="8e392-167">You can change hello default at either by selecting other options in hello respective drop-downs.</span></span>

## <a name="sample-telemetry-custom-live-diagnostic-events"></a><span data-ttu-id="8e392-168">Telemetría de ejemplo: eventos personalizados de diagnóstico en vivo</span><span class="sxs-lookup"><span data-stu-id="8e392-168">Sample Telemetry: Custom Live Diagnostic Events</span></span>
<span data-ttu-id="8e392-169">De forma predeterminada, fuente directa de Hola de eventos muestra ejemplos de solicitudes con error y llamadas de dependencia, excepciones, eventos y seguimientos.</span><span class="sxs-lookup"><span data-stu-id="8e392-169">By default, hello live feed of events shows samples of failed requests and dependency calls, exceptions, events, and traces.</span></span> <span data-ttu-id="8e392-170">Haga clic en criterios Hola aplica toosee de icono de filtro de Hola en cualquier momento en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="8e392-170">Click hello filter icon toosee hello applied criteria at any point in time.</span></span> 

![Fuente directa predeterminada](./media/app-insights-live-stream/live-stream-eventsdefault.png)

<span data-ttu-id="8e392-172">Como con métricas, puede especificar cualquier tooany criterios arbitrarios de tipos de telemetría de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="8e392-172">As with metrics, you can specify any arbitrary criteria tooany of hello Application Insights telemetry types.</span></span> <span data-ttu-id="8e392-173">En este ejemplo, seleccionaremos los eventos, seguimientos y errores de solicitud específicos.</span><span class="sxs-lookup"><span data-stu-id="8e392-173">In this example, we are selecting specific request failures, traces, and events.</span></span> <span data-ttu-id="8e392-174">También se han seleccionado todas las excepciones y errores de dependencia.</span><span class="sxs-lookup"><span data-stu-id="8e392-174">We are also selecting all exceptions and dependency failures.</span></span>

![Fuente personalizada en vivo](./media/app-insights-live-stream/live-stream-events.png)

<span data-ttu-id="8e392-176">Nota: Actualmente, por criterios basada en mensajes de excepción, use mensaje de excepción de extremo de saludo.</span><span class="sxs-lookup"><span data-stu-id="8e392-176">Note: Currently, for Exception message-based criteria, use hello outermost exception message.</span></span> <span data-ttu-id="8e392-177">Hola anterior ejemplo, toofilter out excepción supone un riesgo de hello con mensaje de excepción interna (sigue Hola "<--" delimitador) ""Hola cliente desconectado.</span><span class="sxs-lookup"><span data-stu-id="8e392-177">In hello preceding example, toofilter out hello benign exception with inner exception message (follows hello "<--" delimiter) "hello client disconnected."</span></span> <span data-ttu-id="8e392-178">Use un mensaje que no contenga criterios de error al leer el contenido de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="8e392-178">use a message not-contains "Error reading request content" criteria.</span></span>

<span data-ttu-id="8e392-179">Ver detalles de Hola de un elemento de hello live fuente haciendo clic en él.</span><span class="sxs-lookup"><span data-stu-id="8e392-179">See hello details of an item in hello live feed by clicking it.</span></span> <span data-ttu-id="8e392-180">Puede pausar Hola fuente haciendo clic en **pausar** simplemente desplazarse hacia abajo o haga clic en un elemento.</span><span class="sxs-lookup"><span data-stu-id="8e392-180">You can pause hello feed either by clicking **Pause** or simply scrolling down, or clicking an item.</span></span> <span data-ttu-id="8e392-181">Fuente directa se reanudará una vez que se desplaza toohello Atrás arriba, o haciendo clic en el contador de Hola de elementos recopilados mientras estaba en pausa.</span><span class="sxs-lookup"><span data-stu-id="8e392-181">Live feed will resume after you scroll back toohello top, or by clicking hello counter of items collected while it was paused.</span></span>

![Errores de muestreo de Live](./media/app-insights-live-stream/live-metrics-eventdetail.png)

## <a name="filter-by-server-instance"></a><span data-ttu-id="8e392-183">Filtrado por instancia de servidor</span><span class="sxs-lookup"><span data-stu-id="8e392-183">Filter by server instance</span></span>

<span data-ttu-id="8e392-184">Si desea toomonitor una instancia de rol de servidor en particular, puede filtrar por servidor.</span><span class="sxs-lookup"><span data-stu-id="8e392-184">If you want toomonitor a particular server role instance, you can filter by server.</span></span>

![Errores de muestreo de Live](./media/app-insights-live-stream/live-stream-filter.png)

## <a name="sdk-requirements"></a><span data-ttu-id="8e392-186">Requisitos de SDK</span><span class="sxs-lookup"><span data-stu-id="8e392-186">SDK Requirements</span></span>
<span data-ttu-id="8e392-187">Las secuencias personalizadas de Live Metrics Stream están disponibles con la versión 2.4.0-beta2 o la más reciente del [SDK de Application Insights para la web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span><span class="sxs-lookup"><span data-stu-id="8e392-187">Custom Live Metrics Stream is available with version 2.4.0-beta2 or newer of [Application Insights SDK for web](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/).</span></span> <span data-ttu-id="8e392-188">Recuerde la opción de "Incluye versión preliminar" tooselect desde el Administrador de paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="8e392-188">Remember tooselect "Include Prerelease" option from NuGet package manager.</span></span>

## <a name="secure-hello-control-channel"></a><span data-ttu-id="8e392-189">Proteger el canal de control de Hola</span><span class="sxs-lookup"><span data-stu-id="8e392-189">Secure hello control channel</span></span>
<span data-ttu-id="8e392-190">criterios de filtros personalizados de Hola que especifique se envían componente de métricas de Live toohello atrás en hello Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="8e392-190">hello custom filters criteria you specify are sent back toohello Live Metrics component in hello Application Insights SDK.</span></span> <span data-ttu-id="8e392-191">filtros de Hello podrían contener información confidencial, como customerIDs.</span><span class="sxs-lookup"><span data-stu-id="8e392-191">hello filters could potentially contain sensitive information such as customerIDs.</span></span> <span data-ttu-id="8e392-192">Puede hacer canal Hola seguro con una clave secreta de API además toohello clave de instrumentación.</span><span class="sxs-lookup"><span data-stu-id="8e392-192">You can make hello channel secure with a secret API key in addition toohello instrumentation key.</span></span>
### <a name="create-an-api-key"></a><span data-ttu-id="8e392-193">Creación de una clave de API</span><span class="sxs-lookup"><span data-stu-id="8e392-193">Create an API Key</span></span>

![Creación de una clave de API](./media/app-insights-live-stream/live-metrics-apikeycreate.png)

### <a name="add-api-key-tooconfiguration"></a><span data-ttu-id="8e392-195">Agregar tooConfiguration clave de API</span><span class="sxs-lookup"><span data-stu-id="8e392-195">Add API key tooConfiguration</span></span>
<span data-ttu-id="8e392-196">En el archivo applicationinsights.config de hello, agregue hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="8e392-196">In hello applicationinsights.config file, add hello AuthenticationApiKey toohello QuickPulseTelemetryModule:</span></span>
``` XML

<Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.QuickPulse.QuickPulseTelemetryModule, Microsoft.AI.PerfCounterCollector">
      <AuthenticationApiKey>YOUR-API-KEY-HERE</AuthenticationApiKey>
</Add> 

```
<span data-ttu-id="8e392-197">O bien, en el código, establezca esta opción en Hola QuickPulseTelemetryModule:</span><span class="sxs-lookup"><span data-stu-id="8e392-197">Or in code, set it on hello QuickPulseTelemetryModule:</span></span>

``` C#

    module.AuthenticationApiKey = "YOUR-API-KEY-HERE";

```

<span data-ttu-id="8e392-198">Sin embargo, si lo reconoce y confía que Hola a todos los servidores conectados, puede intentar filtros personalizados de hello sin canal Hola autenticado.</span><span class="sxs-lookup"><span data-stu-id="8e392-198">However, if you recognize and trust all hello connected servers, you can try hello custom filters without hello authenticated channel.</span></span> <span data-ttu-id="8e392-199">Esta opción está disponible durante seis meses.</span><span class="sxs-lookup"><span data-stu-id="8e392-199">This option is available for six months.</span></span> <span data-ttu-id="8e392-200">Esta invalidación se requiere una vez cada nueva sesión, o cuando se pone en línea un nuevo servidor.</span><span class="sxs-lookup"><span data-stu-id="8e392-200">This override is required once every new session, or when a new server comes online.</span></span>

![Opciones de autenticación de Live Metrics](./media/app-insights-live-stream/live-stream-auth.png)

>[!NOTE]
><span data-ttu-id="8e392-202">Se recomienda que configure canal Hola autenticado antes de introducir información potencialmente confidencial, como CustomerID en criterios de filtro de Hola.</span><span class="sxs-lookup"><span data-stu-id="8e392-202">We strongly recommend that you set up hello authenticated channel before entering potentially sensitive information like CustomerID in hello filter criteria.</span></span>
>

## <a name="generating-a-performance-test-load"></a><span data-ttu-id="8e392-203">Generación de una carga de prueba de rendimiento</span><span class="sxs-lookup"><span data-stu-id="8e392-203">Generating a performance test load</span></span>

<span data-ttu-id="8e392-204">Si desea aumentar toowatch efecto de Hola de una carga, hoja de prueba de rendimiento de uso Hola.</span><span class="sxs-lookup"><span data-stu-id="8e392-204">If you want toowatch hello effect of a load increase, use hello Performance Test blade.</span></span> <span data-ttu-id="8e392-205">Simula solicitudes de varios usuarios simultáneos.</span><span class="sxs-lookup"><span data-stu-id="8e392-205">It simulates requests from a number of simultaneous users.</span></span> <span data-ttu-id="8e392-206">Se pueden ejecutar cualquier "pruebas manuales" (ping pruebas) de una sola dirección URL, o puede ejecutarse un [prueba de rendimiento web de varios pasos](app-insights-monitor-web-app-availability.md#multi-step-web-tests) que se carga (de Hola de igual forma que una disponibilidad de prueba).</span><span class="sxs-lookup"><span data-stu-id="8e392-206">It can run either "manual tests" (ping tests) of a single URL, or it can run a [multi-step web performance test](app-insights-monitor-web-app-availability.md#multi-step-web-tests) that you upload (in hello same way as an availability test).</span></span>

> [!TIP]
> <span data-ttu-id="8e392-207">Después de crear la prueba de rendimiento de hello, abra la prueba de Hola y Hola hoja de secuencia en directo en ventanas independientes.</span><span class="sxs-lookup"><span data-stu-id="8e392-207">After you create hello performance test, open hello test and hello Live Stream blade in separate windows.</span></span> <span data-ttu-id="8e392-208">Puede ver al hello en cola inicia de prueba de rendimiento y la secuencia en directo de inspección en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="8e392-208">You can see when hello queued performance test starts, and watch live stream at hello same time.</span></span>
>


## <a name="troubleshooting"></a><span data-ttu-id="8e392-209">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="8e392-209">Troubleshooting</span></span>

<span data-ttu-id="8e392-210">¿No hay datos?</span><span class="sxs-lookup"><span data-stu-id="8e392-210">No data?</span></span> <span data-ttu-id="8e392-211">Si la aplicación está en una red protegida, Live Metrics Stream usará una dirección IP diferente que otra telemetría de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8e392-211">If your application is in a protected network: Live Metrics Stream uses a different IP addresses than other Application Insights telemetry.</span></span> <span data-ttu-id="8e392-212">Asegúrese de que [esas direcciones IP](app-insights-ip-addresses.md) están abiertos en el firewall.</span><span class="sxs-lookup"><span data-stu-id="8e392-212">Make sure [those IP addresses](app-insights-ip-addresses.md) are open in your firewall.</span></span>



## <a name="next-steps"></a><span data-ttu-id="8e392-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8e392-213">Next steps</span></span>
* [<span data-ttu-id="8e392-214">Supervisión del uso con Application Insights</span><span class="sxs-lookup"><span data-stu-id="8e392-214">Monitoring usage with Application Insights</span></span>](app-insights-web-track-usage.md)
* [<span data-ttu-id="8e392-215">Uso de la Búsqueda de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="8e392-215">Using Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="8e392-216">Generador de perfiles</span><span class="sxs-lookup"><span data-stu-id="8e392-216">Profiler</span></span>](app-insights-profiler.md)
* [<span data-ttu-id="8e392-217">Depurador de instantáneas</span><span class="sxs-lookup"><span data-stu-id="8e392-217">Snapshot debugger</span></span>](app-insights-snapshot-debugger.md)
