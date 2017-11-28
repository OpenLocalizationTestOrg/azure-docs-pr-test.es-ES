---
title: "aaaApplication API visión para eventos personalizados y las métricas | Documentos de Microsoft"
description: "Inserte unas pocas líneas de código en el uso de tootrack dispositivo o aplicación de escritorio, página Web o un servicio y diagnosticar problemas."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="9424b-103">API de Application Insights para eventos y métricas personalizados</span><span class="sxs-lookup"><span data-stu-id="9424b-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="9424b-104">Insertar unas pocas líneas de código en su toofind de aplicación a lo que hacen los usuarios con él o toohelp diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="9424b-104">Insert a few lines of code in your application toofind out what users are doing with it, or toohelp diagnose issues.</span></span> <span data-ttu-id="9424b-105">Puede enviar datos de telemetría desde aplicaciones de escritorio y de dispositivo y desde clientes y servidores web.</span><span class="sxs-lookup"><span data-stu-id="9424b-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="9424b-106">Hola de uso [Azure Application Insights](app-insights-overview.md) principales de eventos personalizados de telemetría API toosend y las métricas y las versiones de telemetría estándar.</span><span class="sxs-lookup"><span data-stu-id="9424b-106">Use hello [Azure Application Insights](app-insights-overview.md) core telemetry API toosend custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="9424b-107">Esta API es Hola misma API dicho estándar Hola usar recopiladores de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9424b-107">This API is hello same API that hello standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="9424b-108">API summary</span><span class="sxs-lookup"><span data-stu-id="9424b-108">API summary</span></span>
<span data-ttu-id="9424b-109">Hola API es uniforme en todas las plataformas, además de algunas pequeñas variaciones.</span><span class="sxs-lookup"><span data-stu-id="9424b-109">hello API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="9424b-110">Método</span><span class="sxs-lookup"><span data-stu-id="9424b-110">Method</span></span> | <span data-ttu-id="9424b-111">Usado para</span><span class="sxs-lookup"><span data-stu-id="9424b-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="9424b-112">Páginas, pantallas, hojas o formularios.</span><span class="sxs-lookup"><span data-stu-id="9424b-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="9424b-113">Acciones de usuario y otros eventos.</span><span class="sxs-lookup"><span data-stu-id="9424b-113">User actions and other events.</span></span> <span data-ttu-id="9424b-114">Rendimiento de comportamiento o toomonitor de usuario tootrack usado.</span><span class="sxs-lookup"><span data-stu-id="9424b-114">Used tootrack user behavior or toomonitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="9424b-115">Medidas de rendimiento, como la longitud de las colas no relacionados con eventos toospecific.</span><span class="sxs-lookup"><span data-stu-id="9424b-115">Performance measurements such as queue lengths not related toospecific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="9424b-116">Excepciones de registro para diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="9424b-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="9424b-117">Seguimiento donde se producen en los eventos de relación tooother y examinar los seguimientos de pila.</span><span class="sxs-lookup"><span data-stu-id="9424b-117">Trace where they occur in relation tooother events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="9424b-118">Registro de hello frecuencia y duración de las solicitudes de servidor para el análisis de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9424b-118">Logging hello frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="9424b-119">Mensajes de registro de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="9424b-119">Diagnostic log messages.</span></span> <span data-ttu-id="9424b-120">También puede capturar registros de terceros.</span><span class="sxs-lookup"><span data-stu-id="9424b-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="9424b-121">Registro de hello duración y frecuencia de los componentes de tooexternal de llamadas que depende de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9424b-121">Logging hello duration and frequency of calls tooexternal components that your app depends on.</span></span> |

<span data-ttu-id="9424b-122">También puede [adjuntar propiedades y las métricas de](#properties) toomost de estas llamadas de telemetría.</span><span class="sxs-lookup"><span data-stu-id="9424b-122">You can [attach properties and metrics](#properties) toomost of these telemetry calls.</span></span>

## <span data-ttu-id="9424b-123"><a name="prep"></a>Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="9424b-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="9424b-124">Si aún no tiene una referencia en el SDK de Application Insights:</span><span class="sxs-lookup"><span data-stu-id="9424b-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="9424b-125">Agregar proyecto de hello Application Insights SDK tooyour:</span><span class="sxs-lookup"><span data-stu-id="9424b-125">Add hello Application Insights SDK tooyour project:</span></span>

  * [<span data-ttu-id="9424b-126">Proyecto de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9424b-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="9424b-127">Proyecto de Java</span><span class="sxs-lookup"><span data-stu-id="9424b-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="9424b-128">JavaScript en cada página web</span><span class="sxs-lookup"><span data-stu-id="9424b-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="9424b-129">En el código de servidor web o de dispositivo, incluya:</span><span class="sxs-lookup"><span data-stu-id="9424b-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="9424b-130">*C#:*`using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="9424b-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="9424b-131">*Visual Basic:*`Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="9424b-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="9424b-132">*Java:*`import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="9424b-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="9424b-133">Construcción de una instancia de TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="9424b-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="9424b-134">Construcción de una instancia de `TelemetryClient` (excepto en JavaScript en páginas web):</span><span class="sxs-lookup"><span data-stu-id="9424b-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="9424b-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="9424b-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9424b-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="9424b-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="9424b-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="9424b-138">TelemetryClient es seguro para subprocesos.</span><span class="sxs-lookup"><span data-stu-id="9424b-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="9424b-139">Se recomienda que use una instancia de TelemetryClient para cada módulo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9424b-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="9424b-140">Por ejemplo, puede tener una instancia de TelemetryClient en las solicitudes de HTTP entrantes y tooreport con servicio web y otra en una eventos de lógica de negocios de middleware clase tooreport.</span><span class="sxs-lookup"><span data-stu-id="9424b-140">For instance, you may have one TelemetryClient instance in your web service tooreport incoming HTTP requests, and another in a middleware class tooreport business logic events.</span></span> <span data-ttu-id="9424b-141">Puede establecer las propiedades como `TelemetryClient.Context.User.Id` tootrack usuarios y sesiones, o `TelemetryClient.Context.Device.Id` máquina de hello tooidentify.</span><span class="sxs-lookup"><span data-stu-id="9424b-141">You can set properties such as `TelemetryClient.Context.User.Id` tootrack users and sessions, or `TelemetryClient.Context.Device.Id` tooidentify hello machine.</span></span> <span data-ttu-id="9424b-142">Esta información es eventos tooall adjunto que Hola envíos de instancia.</span><span class="sxs-lookup"><span data-stu-id="9424b-142">This information is attached tooall events that hello instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="9424b-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="9424b-143">TrackEvent</span></span>
<span data-ttu-id="9424b-144">En Application Insights, un *evento personalizado* es un punto de datos que se puede mostrar en el [Explorador de métricas](app-insights-metrics-explorer.md) como recuento agregado, y como repeticiones individuales en [Búsqueda de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="9424b-145">(No relacionado tooMVC u otros framework "eventos".)</span><span class="sxs-lookup"><span data-stu-id="9424b-145">(It isn't related tooMVC or other framework "events.")</span></span>

<span data-ttu-id="9424b-146">Insertar `TrackEvent` llama en su código toocount diversos eventos.</span><span class="sxs-lookup"><span data-stu-id="9424b-146">Insert `TrackEvent` calls in your code toocount various events.</span></span> <span data-ttu-id="9424b-147">la frecuencia con la que los usuarios eligen una determinada característica, con la que logran unos determinados objetivos o con la que cometen determinados tipos de errores.</span><span class="sxs-lookup"><span data-stu-id="9424b-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="9424b-148">Por ejemplo, en una aplicación de juego, enviar un evento cada vez que un usuario gana el juego de hello:</span><span class="sxs-lookup"><span data-stu-id="9424b-148">For example, in a game app, send an event whenever a user wins hello game:</span></span>

<span data-ttu-id="9424b-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9424b-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="9424b-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="9424b-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9424b-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="9424b-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="9424b-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a><span data-ttu-id="9424b-153">Ver los eventos en el portal de Microsoft Azure Hola</span><span class="sxs-lookup"><span data-stu-id="9424b-153">View your events in hello Microsoft Azure portal</span></span>
<span data-ttu-id="9424b-154">toosee un recuento de los eventos, abra un [Explorer métricas](app-insights-metrics-explorer.md) hoja, agregar un nuevo gráfico y seleccione **eventos**.</span><span class="sxs-lookup"><span data-stu-id="9424b-154">toosee a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Visualización de un recuento de eventos personalizados](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="9424b-156">recuentos de hello toocompare diversos eventos, establezca el tipo de gráfico de Hola de demasiado**cuadrícula**y de grupo por nombre de evento:</span><span class="sxs-lookup"><span data-stu-id="9424b-156">toocompare hello counts of different events, set hello chart type too**Grid**, and group by event name:</span></span>

![Establece el tipo de gráfico de Hola y de agrupación](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="9424b-158">En la cuadrícula de hello, haga clic en a través de un evento nombre toosee las repeticiones individuales de ese evento.</span><span class="sxs-lookup"><span data-stu-id="9424b-158">On hello grid, click through an event name toosee individual occurrences of that event.</span></span> <span data-ttu-id="9424b-159">toosee más detallada: haga clic en cualquier aparición en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-159">toosee more detail - click any occurrence in hello list.</span></span>

![Obtención de eventos de Hola](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="9424b-161">toofocus según determinados eventos en la búsqueda o en el Explorador de métricas, nombres de evento de toohello de filtro del conjunto Hola hoja que le interesa:</span><span class="sxs-lookup"><span data-stu-id="9424b-161">toofocus on specific events in either Search or Metrics Explorer, set hello blade's filter toohello event names that you're interested in:</span></span>

![Abre filtros, expanda el nombre del evento y seleccione uno o varios valores.](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="9424b-163">Eventos personalizados en Analytics</span><span class="sxs-lookup"><span data-stu-id="9424b-163">Custom events in Analytics</span></span>

<span data-ttu-id="9424b-164">telemetría Hola está disponible en hello `customEvents` tabla [el análisis de visión aplicaciones](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-164">hello telemetry is available in hello `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="9424b-165">Cada fila representa una llamada demasiado`trackEvent(..)` en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9424b-165">Each row represents a call too`trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="9424b-166">Si [muestreo](app-insights-sampling.md) está en funcionamiento, la propiedad itemCount de hello muestra un valor mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="9424b-166">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="9424b-167">Para el ejemplo itemCount == 10 significa que de 10 llamadas tootrackEvent(), proceso de muestreo de hello sólo transmite uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="9424b-167">For example itemCount==10 means that of 10 calls tootrackEvent(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="9424b-168">tooget un número correcto de eventos personalizados, debe utilizar, por tanto, use código como `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="9424b-168">tooget a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="9424b-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="9424b-169">TrackMetric</span></span>

<span data-ttu-id="9424b-170">Application Insights pueden gráfico de métricas que no son eventos tooparticular adjunto.</span><span class="sxs-lookup"><span data-stu-id="9424b-170">Application Insights can chart metrics that are not attached tooparticular events.</span></span> <span data-ttu-id="9424b-171">Por ejemplo, puede supervisar una longitud de cola a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="9424b-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="9424b-172">Con métricas, medidas individuales de hello son de menos interés que las variaciones de Hola y las tendencias y, por lo que estadística gráficos son útiles.</span><span class="sxs-lookup"><span data-stu-id="9424b-172">With metrics, hello individual measurements are of less interest than hello variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="9424b-173">En ordenar las métricas de toosend tooApplication visión, puede usar hello `TrackMetric(..)` API.</span><span class="sxs-lookup"><span data-stu-id="9424b-173">In order toosend metrics tooApplication Insights, you can use hello `TrackMetric(..)` API.</span></span> <span data-ttu-id="9424b-174">Una métrica no hay toosend de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="9424b-174">There are two ways toosend a metric:</span></span> 

* <span data-ttu-id="9424b-175">Valor único.</span><span class="sxs-lookup"><span data-stu-id="9424b-175">Single value.</span></span> <span data-ttu-id="9424b-176">Cada vez que realiza una medida en la aplicación, debe enviar valor correspondiente de hello tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="9424b-176">Every time you perform a measurement in your application, you send hello corresponding value tooApplication Insights.</span></span> <span data-ttu-id="9424b-177">Por ejemplo, suponga que tiene una métrica que describe el número de Hola de elementos de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="9424b-177">For example, assume that you have a metric describing hello number of items in a container.</span></span> <span data-ttu-id="9424b-178">Durante un período de tiempo determinado, primero se pone tres elementos en el contenedor de hello y, a continuación, quite dos elementos.</span><span class="sxs-lookup"><span data-stu-id="9424b-178">During a particular time period, you first put three items into hello container and then you remove two items.</span></span> <span data-ttu-id="9424b-179">En consecuencia, se llamaría a `TrackMetric` dos veces: primero se pasa el valor de hello `3` y, a continuación, Hola valor `-2`.</span><span class="sxs-lookup"><span data-stu-id="9424b-179">Accordingly, you would call `TrackMetric` twice: first passing hello value `3` and then hello value `-2`.</span></span> <span data-ttu-id="9424b-180">Application Insights almacena ambos valores en su nombre.</span><span class="sxs-lookup"><span data-stu-id="9424b-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="9424b-181">Agregación.</span><span class="sxs-lookup"><span data-stu-id="9424b-181">Aggregation.</span></span> <span data-ttu-id="9424b-182">Al trabajar con métricas, las mediciones individuales pocas veces resultan de interés.</span><span class="sxs-lookup"><span data-stu-id="9424b-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="9424b-183">En su lugar, lo importante son los resúmenes de acontecimientos durante un período determinado.</span><span class="sxs-lookup"><span data-stu-id="9424b-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="9424b-184">Los resúmenes de este tipo se denominan _agregaciones_.</span><span class="sxs-lookup"><span data-stu-id="9424b-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="9424b-185">Hola ejemplo anterior, las métricas suma de agregados de Hola durante ese período de tiempo es `1` y Hola recuento de valores de métrica de hello es `2`.</span><span class="sxs-lookup"><span data-stu-id="9424b-185">In hello above example, hello aggregate metric sum for that time period is `1` and hello count of hello metric values is `2`.</span></span> <span data-ttu-id="9424b-186">Cuando se usa el enfoque de agregación de hello, solo se invoque `TrackMetric` una vez por período y envío Hola agregados valores de hora.</span><span class="sxs-lookup"><span data-stu-id="9424b-186">When using hello aggregation approach, you only invoke `TrackMetric` once per time period and send hello aggregate values.</span></span> <span data-ttu-id="9424b-187">Se trata de hello enfoque recomendado, ya que puede reducir considerablemente el coste de Hola y rendimiento sobrecarga mediante el envío de datos menos puntos tooApplication visión, mientras todavía recopilar toda la información pertinente.</span><span class="sxs-lookup"><span data-stu-id="9424b-187">This is hello recommended approach since it can significantly reduce hello cost and performance overhead by sending fewer data points tooApplication Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="9424b-188">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="9424b-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="9424b-189">Valores únicos</span><span class="sxs-lookup"><span data-stu-id="9424b-189">Single values</span></span>

<span data-ttu-id="9424b-190">toosend un único valor de métrica:</span><span class="sxs-lookup"><span data-stu-id="9424b-190">toosend a single metric value:</span></span>

<span data-ttu-id="9424b-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9424b-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="9424b-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="9424b-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="9424b-193">Agregación de métricas</span><span class="sxs-lookup"><span data-stu-id="9424b-193">Aggregating metrics</span></span>

<span data-ttu-id="9424b-194">Se recomienda tooaggregate métricas antes de enviarlos desde su aplicación, el ancho de banda de tooreduce, tooimprove y costo de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9424b-194">It is recommended tooaggregate metrics before sending them from your app, tooreduce bandwidth, cost and tooimprove performance.</span></span>
<span data-ttu-id="9424b-195">Este es un ejemplo de código de agregación:</span><span class="sxs-lookup"><span data-stu-id="9424b-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="9424b-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-196">*C#*</span></span>

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="9424b-197">Métricas personalizadas en el Explorador de métricas</span><span class="sxs-lookup"><span data-stu-id="9424b-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="9424b-198">resultados de hello toosee, abra el Explorador de métricas y agregar un nuevo gráfico.</span><span class="sxs-lookup"><span data-stu-id="9424b-198">toosee hello results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="9424b-199">Editar Hola gráfico tooshow la métrica.</span><span class="sxs-lookup"><span data-stu-id="9424b-199">Edit hello chart tooshow your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="9424b-200">La métrica personalizada puede tardar varios tooappear minutos en lista de Hola de métricas disponibles.</span><span class="sxs-lookup"><span data-stu-id="9424b-200">Your custom metric might take several minutes tooappear in hello list of available metrics.</span></span>
>

![Agregue un gráfico nuevo o seleccione un gráfico y, en Personalizada, seleccione su métrica.](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="9424b-202">Métricas personalizadas en Analytics</span><span class="sxs-lookup"><span data-stu-id="9424b-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="9424b-203">telemetría Hola está disponible en hello `customMetrics` tabla [el análisis de visión aplicaciones](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-203">hello telemetry is available in hello `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="9424b-204">Cada fila representa una llamada demasiado`trackMetric(..)` en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9424b-204">Each row represents a call too`trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="9424b-205">`valueSum`-Esta es la suma de Hola de mediciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-205">`valueSum` - This is hello sum of hello measurements.</span></span> <span data-ttu-id="9424b-206">valor promedio tooget hello, división por `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="9424b-206">tooget hello mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="9424b-207">`valueCount`-Hola número de medidas que se han agregado en este `trackMetric(..)` llamar.</span><span class="sxs-lookup"><span data-stu-id="9424b-207">`valueCount` - hello number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="9424b-208">Vistas de página</span><span class="sxs-lookup"><span data-stu-id="9424b-208">Page views</span></span>
<span data-ttu-id="9424b-209">En una aplicación de dispositivo o de página web, se envían datos de telemetría de la vista de página de forma predeterminada cuando se carga cada pantalla o página.</span><span class="sxs-lookup"><span data-stu-id="9424b-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="9424b-210">Pero puede cambiar las vistas de esa página tootrack en momentos diferentes o adicionales.</span><span class="sxs-lookup"><span data-stu-id="9424b-210">But you can change that tootrack page views at additional or different times.</span></span> <span data-ttu-id="9424b-211">Por ejemplo, en una aplicación que muestra las pestañas o las hojas, conviene tootrack una página siempre que sea usuario de hello abre una nueva hoja.</span><span class="sxs-lookup"><span data-stu-id="9424b-211">For example, in an app that displays tabs or blades, you might want tootrack a page whenever hello user opens a new blade.</span></span>

![Uso de modos en la hoja Información general](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="9424b-213">Datos de usuario y la sesión se envían como propiedades junto con las vistas de página, por lo que Hola gráficos de usuario y la sesión dotándolo cuando hay telemetría de vista de página.</span><span class="sxs-lookup"><span data-stu-id="9424b-213">User and session data is sent as properties along with page views, so hello user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="9424b-214">Vistas de página personalizadas</span><span class="sxs-lookup"><span data-stu-id="9424b-214">Custom page views</span></span>
<span data-ttu-id="9424b-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9424b-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="9424b-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="9424b-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9424b-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="9424b-218">Si tiene varias pestañas en distintas páginas HTML, puede especificar la dirección URL de hello demasiado:</span><span class="sxs-lookup"><span data-stu-id="9424b-218">If you have several tabs within different HTML pages, you can specify hello URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="9424b-219">Cronometrar las vistas de página</span><span class="sxs-lookup"><span data-stu-id="9424b-219">Timing page views</span></span>
<span data-ttu-id="9424b-220">De forma predeterminada, los tiempos de Hola se notifican como **tiempo de carga de vista de página** se miden desde al explorador de hello envía la solicitud de hello, hasta que se llama al evento de carga de página del explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-220">By default, hello times reported as **Page view load time** are measured from when hello browser sends hello request, until hello browser's page load event is called.</span></span>

<span data-ttu-id="9424b-221">En su lugar, puede:</span><span class="sxs-lookup"><span data-stu-id="9424b-221">Instead, you can either:</span></span>

* <span data-ttu-id="9424b-222">Establecer una duración explícita en hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) llamar: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="9424b-222">Set an explicit duration in hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="9424b-223">Usar llamadas de control de tiempo de vista de página de hello `startTrackPage` y `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="9424b-223">Use hello page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="9424b-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9424b-224">*JavaScript*</span></span>

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="9424b-225">...</span><span class="sxs-lookup"><span data-stu-id="9424b-225">...</span></span>

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="9424b-226">Hola nombre que se utiliza como primer parámetro de hello asocia inicio hello y detener las llamadas.</span><span class="sxs-lookup"><span data-stu-id="9424b-226">hello name that you use as hello first parameter associates hello start and stop calls.</span></span> <span data-ttu-id="9424b-227">El valor predeterminado es toohello nombre actual de la página.</span><span class="sxs-lookup"><span data-stu-id="9424b-227">It defaults toohello current page name.</span></span>

<span data-ttu-id="9424b-228">carga de página resultante Hello las duraciones que se muestra en el Explorador de métricas se derivan de intervalo de saludo entre Hola iniciar y detener las llamadas.</span><span class="sxs-lookup"><span data-stu-id="9424b-228">hello resulting page load durations displayed in Metrics Explorer are derived from hello interval between hello start and stop calls.</span></span> <span data-ttu-id="9424b-229">Es una tooyou el intervalo de tiempo si realmente.</span><span class="sxs-lookup"><span data-stu-id="9424b-229">It's up tooyou what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="9424b-230">Telemetría de páginas en Analytics</span><span class="sxs-lookup"><span data-stu-id="9424b-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="9424b-231">En [Analytics](app-insights-analytics.md) hay dos tablas en las que se muestran datos de operaciones de explorador:</span><span class="sxs-lookup"><span data-stu-id="9424b-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="9424b-232">Hola `pageViews` tabla contiene datos sobre el título de página y la dirección URL de Hola</span><span class="sxs-lookup"><span data-stu-id="9424b-232">hello `pageViews` table contains data about hello URL and page title</span></span>
* <span data-ttu-id="9424b-233">Hola `browserTimings` tabla contiene datos sobre el rendimiento de cliente, como tooprocess de tiempo que tarda Hola Hola los datos entrantes</span><span class="sxs-lookup"><span data-stu-id="9424b-233">hello `browserTimings` table contains data about client performance, such as hello time taken tooprocess hello incoming data</span></span>

<span data-ttu-id="9424b-234">toofind cuánto explorador Hola toma tooprocess páginas diferentes:</span><span class="sxs-lookup"><span data-stu-id="9424b-234">toofind how long hello browser takes tooprocess different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="9424b-235">toodiscover popularities de Hola de exploradores diferentes:</span><span class="sxs-lookup"><span data-stu-id="9424b-235">toodiscover hello popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="9424b-236">vistas de página tooassociate llamadas tooAJAX, unir con dependencias:</span><span class="sxs-lookup"><span data-stu-id="9424b-236">tooassociate page views tooAJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="9424b-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="9424b-237">TrackRequest</span></span>
<span data-ttu-id="9424b-238">servidor de Hello SDK usa las solicitudes HTTP de toolog TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="9424b-238">hello server SDK uses TrackRequest toolog HTTP requests.</span></span>

<span data-ttu-id="9424b-239">También puede llamarlo usted mismo si desea que las solicitudes de toosimulate en un contexto donde no haya hello web servicio módulo que se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="9424b-239">You can also call it yourself if you want toosimulate requests in a context where you don't have hello web service module running.</span></span>

<span data-ttu-id="9424b-240">Sin embargo, Hola recomienda telemetría de solicitud de manera toosend es donde solicitud Hola actúa como un <a href="#operation-context">contexto de operación</a>.</span><span class="sxs-lookup"><span data-stu-id="9424b-240">However, hello recommended way toosend request telemetry is where hello request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="9424b-241">Contexto de operación</span><span class="sxs-lookup"><span data-stu-id="9424b-241">Operation context</span></span>
<span data-ttu-id="9424b-242">Puede asociar elementos de telemetría juntos mediante una asociación toothem un identificador de operación común.</span><span class="sxs-lookup"><span data-stu-id="9424b-242">You can associate telemetry items together by attaching toothem a common operation ID.</span></span> <span data-ttu-id="9424b-243">módulo de seguimiento de solicitud estándar Hola hace excepciones y otros eventos que se envían mientras se procesa una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="9424b-243">hello standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="9424b-244">En [búsqueda](app-insights-diagnostic-search.md) y [análisis](app-insights-analytics.md), puede usar los eventos asociados con la solicitud de Hola Hola identificador tooeasily buscar.</span><span class="sxs-lookup"><span data-stu-id="9424b-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use hello ID tooeasily find any events associated with hello request.</span></span>

<span data-ttu-id="9424b-245">Identificador de Hola de manera más fácil de Hello tooset es tooset un contexto de la operación mediante el uso de este patrón:</span><span class="sxs-lookup"><span data-stu-id="9424b-245">hello easiest way tooset hello ID is tooset an operation context by using this pattern:</span></span>

<span data-ttu-id="9424b-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="9424b-247">Junto con la configuración de un contexto de la operación, `StartOperation` crea un elemento de telemetría de tipo hello que especifique.</span><span class="sxs-lookup"><span data-stu-id="9424b-247">Along with setting an operation context, `StartOperation` creates a telemetry item of hello type that you specify.</span></span> <span data-ttu-id="9424b-248">Envía elementos telemetría hello cuando dispose operación hello, o si se llama explícitamente a `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="9424b-248">It sends hello telemetry item when you dispose hello operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="9424b-249">Si usa `RequestTelemetry` como tipo de telemetría de hello, su duración se establece intervalo toohello ha superado el tiempo entre el inicio y detención.</span><span class="sxs-lookup"><span data-stu-id="9424b-249">If you use `RequestTelemetry` as hello telemetry type, its duration is set toohello timed interval between start and stop.</span></span>

<span data-ttu-id="9424b-250">Los contextos de operación no pueden estar anidados.</span><span class="sxs-lookup"><span data-stu-id="9424b-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="9424b-251">Si ya hay un contexto de la operación, entonces su identificador está asociado a todos los elementos de hello contenido, incluido elemento Hola creado con `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="9424b-251">If there is already an operation context, then its ID is associated with all hello contained items, including hello item created with `StartOperation`.</span></span>

<span data-ttu-id="9424b-252">En la búsqueda, contexto de la operación de hello es hello toocreate usado **elementos relacionados** lista:</span><span class="sxs-lookup"><span data-stu-id="9424b-252">In Search, hello operation context is used toocreate hello **Related Items** list:</span></span>

![Elementos relacionados](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="9424b-254">Consulte [application-insights-custom-operations-tracking.md.md] para más información sobre el seguimiento de las operaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="9424b-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="9424b-255">Solicitudes en Analytics</span><span class="sxs-lookup"><span data-stu-id="9424b-255">Requests in Analytics</span></span> 

<span data-ttu-id="9424b-256">En [el análisis de visión aplicaciones](app-insights-analytics.md), solicita mostrar seguridad Hola `requests` tabla.</span><span class="sxs-lookup"><span data-stu-id="9424b-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in hello `requests` table.</span></span>

<span data-ttu-id="9424b-257">Si [muestreo](app-insights-sampling.md) está en funcionamiento, propiedad itemCount de hello muestra un valor mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="9424b-257">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="9424b-258">Para el ejemplo itemCount == 10 significa que de 10 llamadas tootrackRequest(), proceso de muestreo de hello sólo transmite uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="9424b-258">For example itemCount==10 means that of 10 calls tootrackRequest(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="9424b-259">un número correcto de las solicitudes y la duración media de tooget segmentadas por nombres de la solicitud, utilice código como:</span><span class="sxs-lookup"><span data-stu-id="9424b-259">tooget a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="9424b-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="9424b-260">TrackException</span></span>
<span data-ttu-id="9424b-261">Enviar excepciones tooApplication visión:</span><span class="sxs-lookup"><span data-stu-id="9424b-261">Send exceptions tooApplication Insights:</span></span>

* <span data-ttu-id="9424b-262">demasiado[contarlas](app-insights-metrics-explorer.md), como una indicación de frecuencia de Hola de un problema.</span><span class="sxs-lookup"><span data-stu-id="9424b-262">too[count them](app-insights-metrics-explorer.md), as an indication of hello frequency of a problem.</span></span>
* <span data-ttu-id="9424b-263">demasiado[examine todos los casos individuales](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-263">too[examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="9424b-264">los informes de Hello incluyen seguimientos de pila de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-264">hello reports include hello stack traces.</span></span>

<span data-ttu-id="9424b-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="9424b-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9424b-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="9424b-267">SDK de Hello detecta automáticamente, muchas de las excepciones para que no tenga siempre toocall TrackException explícitamente.</span><span class="sxs-lookup"><span data-stu-id="9424b-267">hello SDKs catch many exceptions automatically, so you don't always have toocall TrackException explicitly.</span></span>

* <span data-ttu-id="9424b-268">ASP.NET: [escribir código excepciones toocatch](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-268">ASP.NET: [Write code toocatch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="9424b-269">J2EE: [las excepciones se detectan automáticamente](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="9424b-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="9424b-270">JavaScript: las excepciones se detectan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9424b-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="9424b-271">Si desea que la recopilación automática de toodisable, agregue un fragmento de código de toohello de línea que se inserta en las páginas Web:</span><span class="sxs-lookup"><span data-stu-id="9424b-271">If you want toodisable automatic collection, add a line toohello code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="9424b-272">Excepciones en Analytics</span><span class="sxs-lookup"><span data-stu-id="9424b-272">Exceptions in Analytics</span></span>

<span data-ttu-id="9424b-273">En [el análisis de visión aplicaciones](app-insights-analytics.md), las excepciones se mostrarán en hello `exceptions` tabla.</span><span class="sxs-lookup"><span data-stu-id="9424b-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in hello `exceptions` table.</span></span>

<span data-ttu-id="9424b-274">Si [muestreo](app-insights-sampling.md) está en funcionamiento, hello `itemCount` propiedad muestra un valor mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="9424b-274">If [sampling](app-insights-sampling.md) is in operation, hello `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="9424b-275">Para el ejemplo itemCount == 10 significa que de 10 llamadas tootrackException(), proceso de muestreo de hello sólo transmite uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="9424b-275">For example itemCount==10 means that of 10 calls tootrackException(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="9424b-276">tooget un número correcto de excepciones segmentadas por tipo de excepción, utilice código como:</span><span class="sxs-lookup"><span data-stu-id="9424b-276">tooget a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="9424b-277">La mayoría de hello importante información de la pila ya se extrae en variables independientes, pero se puede extraer de hello distinguirlos `details` tooget estructura más.</span><span class="sxs-lookup"><span data-stu-id="9424b-277">Most of hello important stack information is already extracted into separate variables, but you can pull apart hello `details` structure tooget more.</span></span> <span data-ttu-id="9424b-278">Puesto que esta estructura es dinámica, debe convertir el tipo del resultado de hello toohello que espera.</span><span class="sxs-lookup"><span data-stu-id="9424b-278">Since this structure is dynamic, you should cast hello result toohello type you expect.</span></span> <span data-ttu-id="9424b-279">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9424b-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="9424b-280">excepciones de tooassociate con sus solicitudes relacionados, use una combinación:</span><span class="sxs-lookup"><span data-stu-id="9424b-280">tooassociate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="9424b-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="9424b-281">TrackTrace</span></span>
<span data-ttu-id="9424b-282">Use TrackTrace toohelp diagnosticar problemas mediante el envío de un "rastro de la ruta de navegación" tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="9424b-282">Use TrackTrace toohelp diagnose problems by sending a "breadcrumb trail" tooApplication Insights.</span></span> <span data-ttu-id="9424b-283">Puede enviar fragmentos de datos de diagnóstico e inspeccionarlos en [Búsqueda de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="9424b-284">[Registrar adaptadores](app-insights-asp-net-trace-logs.md) usar este portal de toohello API toosend registros de aplicaciones de terceros.</span><span class="sxs-lookup"><span data-stu-id="9424b-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API toosend third-party logs toohello portal.</span></span>

<span data-ttu-id="9424b-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="9424b-286">Puede buscar en el contenido del mensaje, pero (a diferencia de los valores de propiedad) no puede filtrar por él.</span><span class="sxs-lookup"><span data-stu-id="9424b-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="9424b-287">límite de tamaño Hello `message` es mucho mayor que el límite de hello en Propiedades.</span><span class="sxs-lookup"><span data-stu-id="9424b-287">hello size limit on `message` is much higher than hello limit on properties.</span></span>
<span data-ttu-id="9424b-288">La ventaja de TrackTrace es que puede colocar datos relativamente largos en mensajes de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="9424b-288">An advantage of TrackTrace is that you can put relatively long data in hello message.</span></span> <span data-ttu-id="9424b-289">Por ejemplo, aquí puede codificar datos POST.</span><span class="sxs-lookup"><span data-stu-id="9424b-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="9424b-290">Además, puede agregar un mensaje de tooyour de nivel de gravedad.</span><span class="sxs-lookup"><span data-stu-id="9424b-290">In addition, you can add a severity level tooyour message.</span></span> <span data-ttu-id="9424b-291">Y, al igual que otros telemetría, puede agregar toohelp de valores de propiedad que filtra o buscar para diferentes conjuntos de seguimientos.</span><span class="sxs-lookup"><span data-stu-id="9424b-291">And, like other telemetry, you can add property values toohelp you filter or search for different sets of traces.</span></span> <span data-ttu-id="9424b-292">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9424b-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="9424b-293">En [búsqueda](app-insights-diagnostic-search.md), a continuación, puede filtrar fácilmente todos los mensajes de Hola un nivel de gravedad determinado que se relacionan tooa base de datos determinada.</span><span class="sxs-lookup"><span data-stu-id="9424b-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all hello messages of a particular severity level that relate tooa particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="9424b-294">Seguimientos en Analytics</span><span class="sxs-lookup"><span data-stu-id="9424b-294">Traces in Analytics</span></span>

<span data-ttu-id="9424b-295">En [el análisis de visión aplicaciones](app-insights-analytics.md), se llama tooTrackTrace mostrar Hola `traces` tabla.</span><span class="sxs-lookup"><span data-stu-id="9424b-295">In [Application Insights Analytics](app-insights-analytics.md), calls tooTrackTrace show up in hello `traces` table.</span></span>

<span data-ttu-id="9424b-296">Si [muestreo](app-insights-sampling.md) está en funcionamiento, la propiedad itemCount de hello muestra un valor mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="9424b-296">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="9424b-297">Para el ejemplo itemCount == 10 significa que de 10 llamadas demasiado`trackTrace()`, proceso de muestreo de hello transmite solo uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="9424b-297">For example itemCount==10 means that of 10 calls too`trackTrace()`, hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="9424b-298">tooget un número correcto de las llamadas de seguimiento, se debe utilizar, por tanto, código como `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="9424b-298">tooget a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="9424b-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="9424b-299">TrackDependency</span></span>
<span data-ttu-id="9424b-300">Hola de uso TrackDependency llamar a tiempos de respuesta de hello tootrack y las tasas de éxito de pieza externo de tooan de llamadas de código.</span><span class="sxs-lookup"><span data-stu-id="9424b-300">Use hello TrackDependency call tootrack hello response times and success rates of calls tooan external piece of code.</span></span> <span data-ttu-id="9424b-301">los resultados de Hello aparecen en los gráficos de dependencia de hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-301">hello results appear in hello dependency charts in hello portal.</span></span>

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

<span data-ttu-id="9424b-302">Recuerde que ese servidor hello SDKs incluyen un [módulo dependencia](app-insights-asp-net-dependencies.md) que detecta y realiza un seguimiento de determinadas llamadas de dependencia automáticamente; por ejemplo, toodatabases y las API de REST.</span><span class="sxs-lookup"><span data-stu-id="9424b-302">Remember that hello server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, toodatabases and REST APIs.</span></span> <span data-ttu-id="9424b-303">Deberá tooinstall un agente en el módulo de hello toomake de servidor de trabajo.</span><span class="sxs-lookup"><span data-stu-id="9424b-303">You have tooinstall an agent on your server toomake hello module work.</span></span> <span data-ttu-id="9424b-304">Use esta llamada si desea que no detectar llamadas tootrack que Hola seguimiento automatizado o si no desea a tooinstall agente de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-304">You use this call if you want tootrack calls that hello automated tracking doesn't catch, or if you don't want tooinstall hello agent.</span></span>

<span data-ttu-id="9424b-305">Editar tooturn desactivar el módulo de seguimiento de dependencias estándar hello, [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) y elimine la referencia de hello demasiado`DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="9424b-305">tooturn off hello standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete hello reference too`DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="9424b-306">Dependencias en Analytics</span><span class="sxs-lookup"><span data-stu-id="9424b-306">Dependencies in Analytics</span></span>

<span data-ttu-id="9424b-307">En [el análisis de visión aplicaciones](app-insights-analytics.md), trackDependency llamadas aparecen en hello `dependencies` tabla.</span><span class="sxs-lookup"><span data-stu-id="9424b-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in hello `dependencies` table.</span></span>

<span data-ttu-id="9424b-308">Si [muestreo](app-insights-sampling.md) está en funcionamiento, la propiedad itemCount de hello muestra un valor mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="9424b-308">If [sampling](app-insights-sampling.md) is in operation, hello itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="9424b-309">Para el ejemplo itemCount == 10 significa que de 10 llamadas tootrackDependency(), proceso de muestreo de hello sólo transmite uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="9424b-309">For example itemCount==10 means that of 10 calls tootrackDependency(), hello sampling process only transmitted one of them.</span></span> <span data-ttu-id="9424b-310">tooget un número correcto de dependencias segmentadas por componente de destino, utilice código como:</span><span class="sxs-lookup"><span data-stu-id="9424b-310">tooget a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="9424b-311">dependencias de tooassociate con sus solicitudes relacionados, use una combinación:</span><span class="sxs-lookup"><span data-stu-id="9424b-311">tooassociate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="9424b-312">Datos de vaciado</span><span class="sxs-lookup"><span data-stu-id="9424b-312">Flushing data</span></span>
<span data-ttu-id="9424b-313">Normalmente, Hola SDK envía datos a veces elegidos toominimize impacto de hello en usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-313">Normally, hello SDK sends data at times chosen toominimize hello impact on hello user.</span></span> <span data-ttu-id="9424b-314">Sin embargo, en algunos casos, conviene búfer de Hola tooflush: por ejemplo, si usas Hola SDK en una aplicación que se cierra.</span><span class="sxs-lookup"><span data-stu-id="9424b-314">However, in some cases, you might want tooflush hello buffer--for example, if you are using hello SDK in an application that shuts down.</span></span>

<span data-ttu-id="9424b-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="9424b-316">Tenga en cuenta que la función hello es asincrónico para hello [canal del servidor de telemetría](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="9424b-316">Note that hello function is asynchronous for hello [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="9424b-317">Usuarios autenticados</span><span class="sxs-lookup"><span data-stu-id="9424b-317">Authenticated users</span></span>
<span data-ttu-id="9424b-318">En una aplicación web, los usuarios se identifican por cookies (de manera predeterminada).</span><span class="sxs-lookup"><span data-stu-id="9424b-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="9424b-319">Se puede contar al usuario más de una vez si accede a la aplicación desde un equipo o explorador diferente, o si elimina las cookies.</span><span class="sxs-lookup"><span data-stu-id="9424b-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="9424b-320">Si los usuarios inician sesión en la aplicación de tooyour, puede obtener un recuento más preciso estableciendo Id. de usuario de hello autenticado en el código de hello explorador:</span><span class="sxs-lookup"><span data-stu-id="9424b-320">If users sign in tooyour app, you can get a more accurate count by setting hello authenticated user ID in hello browser code:</span></span>

<span data-ttu-id="9424b-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9424b-321">*JavaScript*</span></span>

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="9424b-322">En una aplicación MVC web de ASP.NET, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9424b-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="9424b-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="9424b-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="9424b-324">No es el nombre de inicio de sesión real del usuario de hello toouse necesarios.</span><span class="sxs-lookup"><span data-stu-id="9424b-324">It isn't necessary toouse hello user's actual sign-in name.</span></span> <span data-ttu-id="9424b-325">Solo tiene toobe un identificador de usuario único toothat.</span><span class="sxs-lookup"><span data-stu-id="9424b-325">It only has toobe an ID that is unique toothat user.</span></span> <span data-ttu-id="9424b-326">No puede contener espacios ni ninguno de los caracteres de hello `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="9424b-326">It must not include spaces or any of hello characters `,;=|`.</span></span>

<span data-ttu-id="9424b-327">Id. de usuario de Hello también se establece en una cookie de sesión y envía toohello server.</span><span class="sxs-lookup"><span data-stu-id="9424b-327">hello user ID is also set in a session cookie and sent toohello server.</span></span> <span data-ttu-id="9424b-328">Si el servidor de hello SDK está instalado, Hola autentica usuario que identificador se envía como parte de las propiedades de contexto de Hola de telemetría de cliente y servidor.</span><span class="sxs-lookup"><span data-stu-id="9424b-328">If hello server SDK is installed, hello authenticated user ID is sent as part of hello context properties of both client and server telemetry.</span></span> <span data-ttu-id="9424b-329">A continuación, puede filtrar y buscar en ella.</span><span class="sxs-lookup"><span data-stu-id="9424b-329">You can then filter and search on it.</span></span>

<span data-ttu-id="9424b-330">Si la aplicación agrupa a los usuarios en las cuentas, también se puede pasar un identificador de cuenta de hello (con hello mismo carácter restricciones).</span><span class="sxs-lookup"><span data-stu-id="9424b-330">If your app groups users into accounts, you can also pass an identifier for hello account (with hello same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="9424b-331">En el [Explorador de métricas](app-insights-metrics-explorer.md), puede crear un gráfico que cuente los **Usuarios autenticados** y las **Cuentas de usuario**.</span><span class="sxs-lookup"><span data-stu-id="9424b-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="9424b-332">También puede [buscar](app-insights-diagnostic-search.md) puntos de datos de cliente con cuentas y nombres de usuario específicos.</span><span class="sxs-lookup"><span data-stu-id="9424b-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="9424b-333"><a name="properties"></a>Filtrado, búsqueda y segmentación de los datos mediante el uso de propiedades</span><span class="sxs-lookup"><span data-stu-id="9424b-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="9424b-334">Puede asociar propiedades y las medidas tooyour eventos (y también toometrics, vistas de página, las excepciones y otros datos de telemetría).</span><span class="sxs-lookup"><span data-stu-id="9424b-334">You can attach properties and measurements tooyour events (and also toometrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="9424b-335">*Propiedades* son valores de cadena que puede usar la telemetría toofilter en informes de uso de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-335">*Properties* are string values that you can use toofilter your telemetry in hello usage reports.</span></span> <span data-ttu-id="9424b-336">Por ejemplo, si la aplicación proporciona varios juegos, puede adjuntar nombre Hola de evento de hello tooeach juego para que pueda comprobar qué juegos son los más populares.</span><span class="sxs-lookup"><span data-stu-id="9424b-336">For example, if your app provides several games, you can attach hello name of hello game tooeach event so that you can see which games are more popular.</span></span>

<span data-ttu-id="9424b-337">Hay un límite de 8192 en longitud de la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-337">There's a limit of 8192 on hello string length.</span></span> <span data-ttu-id="9424b-338">(Si desea que toosend grandes cantidades de datos, utilice el parámetro de mensaje de Hola de [TrackTrace](#track-trace).)</span><span class="sxs-lookup"><span data-stu-id="9424b-338">(If you want toosend large chunks of data, use hello message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="9424b-339">*métricas* son valores numéricos que se pueden presentar de forma gráfica.</span><span class="sxs-lookup"><span data-stu-id="9424b-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="9424b-340">Por ejemplo, puede toosee si hay un aumento gradual de las puntuaciones de hello lograr los jugadores.</span><span class="sxs-lookup"><span data-stu-id="9424b-340">For example, you might want toosee if there's a gradual increase in hello scores that your gamers achieve.</span></span> <span data-ttu-id="9424b-341">gráficos de Hola se pueden segmentar por hello separan de propiedades que se envían con el evento de hello, para que pueda obtener o apilan gráficos de juegos.</span><span class="sxs-lookup"><span data-stu-id="9424b-341">hello graphs can be segmented by hello properties that are sent with hello event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="9424b-342">Para valores de métrica toobe muestra correctamente, deben ser igual o mayor que too0.</span><span class="sxs-lookup"><span data-stu-id="9424b-342">For metric values toobe correctly displayed, they should be greater than or equal too0.</span></span>

<span data-ttu-id="9424b-343">Hay algunos [límites en hello número de propiedades, valores de propiedad y las métricas de](#limits) que puede usar.</span><span class="sxs-lookup"><span data-stu-id="9424b-343">There are some [limits on hello number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="9424b-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9424b-344">*JavaScript*</span></span>

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


<span data-ttu-id="9424b-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="9424b-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9424b-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="9424b-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="9424b-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="9424b-348">Tenga cuidado de no toolog información personal identificable en Propiedades.</span><span class="sxs-lookup"><span data-stu-id="9424b-348">Take care not toolog personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="9424b-349">*Si ha usado las métricas*, abra el Explorador de métricas y seleccione la métrica de hello en hello **personalizado** grupo:</span><span class="sxs-lookup"><span data-stu-id="9424b-349">*If you used metrics*, open Metrics Explorer and select hello metric from hello **Custom** group:</span></span>

![Abra el Explorador de métricas, gráfico de hello seleccione y seleccione Hola métrica](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="9424b-351">Si no aparece la métrica, o si hello **personalizado** encabezado no está allí, hoja de selección de hello cierre y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="9424b-351">If your metric doesn't appear, or if hello **Custom** heading isn't there, close hello selection blade and try again later.</span></span> <span data-ttu-id="9424b-352">Las métricas pueden durar una hora toobe se agregan a través de la canalización de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-352">Metrics can sometimes take an hour toobe aggregated through hello pipeline.</span></span>

<span data-ttu-id="9424b-353">*Si ha utilizado propiedades y las métricas*, segmentar métrica Hola propiedad hello:</span><span class="sxs-lookup"><span data-stu-id="9424b-353">*If you used properties and metrics*, segment hello metric by hello property:</span></span>

![Establecer agrupación y, a continuación, seleccione la propiedad de hello en Agrupar por](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="9424b-355">*En la búsqueda de diagnóstico*, puede ver las propiedades de Hola y métricas de repeticiones individuales de un evento.</span><span class="sxs-lookup"><span data-stu-id="9424b-355">*In Diagnostic Search*, you can view hello properties and metrics of individual occurrences of an event.</span></span>

![Seleccione una instancia y luego seleccione "...".](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="9424b-357">Hola de uso **búsqueda** campo toosee repeticiones del evento que tienen un valor de propiedad concreto.</span><span class="sxs-lookup"><span data-stu-id="9424b-357">Use hello **Search** field toosee event occurrences that have a particular property value.</span></span>

![Escriba un término en Buscar.](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="9424b-359">[Más información sobre las expresiones de búsqueda](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-tooset-properties-and-metrics"></a><span data-ttu-id="9424b-360">Las métricas y las propiedades de tooset de manera alternativa</span><span class="sxs-lookup"><span data-stu-id="9424b-360">Alternative way tooset properties and metrics</span></span>
<span data-ttu-id="9424b-361">Si resulta más eficaz, puede recopilar parámetros de Hola de un evento en un objeto independiente:</span><span class="sxs-lookup"><span data-stu-id="9424b-361">If it's more convenient, you can collect hello parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="9424b-362">No volver a usar Hola misma instancia de elemento de telemetría (`event` en este ejemplo) toocall Track*() varias veces.</span><span class="sxs-lookup"><span data-stu-id="9424b-362">Don't reuse hello same telemetry item instance (`event` in this example) toocall Track*() multiple times.</span></span> <span data-ttu-id="9424b-363">Esto puede provocar toobe telemetría enviado con una configuración incorrecta.</span><span class="sxs-lookup"><span data-stu-id="9424b-363">This may cause telemetry toobe sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="9424b-364">Mediciones y propiedades personalizadas en Analytics</span><span class="sxs-lookup"><span data-stu-id="9424b-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="9424b-365">En [análisis](app-insights-analytics.md), métricas personalizadas y propiedades que se muestran en hello `customMeasurements` y `customDimensions` atributos de cada registro de telemetría.</span><span class="sxs-lookup"><span data-stu-id="9424b-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in hello `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="9424b-366">Por ejemplo, si ha agregado una propiedad denominada "juegos" tooyour telemetría de solicitud, esta consulta recuentos de apariciones de Hola de valores distintos de "juego" y muestra la media de Hola de hello métrica personalizada "puntuación":</span><span class="sxs-lookup"><span data-stu-id="9424b-366">For example, if you have added a property named "game" tooyour request telemetry, this query counts hello occurrences of different values of "game", and show hello average of hello custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="9424b-367">Tenga en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9424b-367">Notice that:</span></span>

* <span data-ttu-id="9424b-368">Cuando se extrae un valor de hello customDimensions o customMeasurements JSON, tiene el tipo dinámico y, por lo que debe convertir `tostring` o `todouble`.</span><span class="sxs-lookup"><span data-stu-id="9424b-368">When you extract a value from hello customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="9424b-369">cuenta de tootake de posibilidad de Hola de [muestreo](app-insights-sampling.md), debe usar `sum(itemCount)`, no `count()`.</span><span class="sxs-lookup"><span data-stu-id="9424b-369">tootake account of hello possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="9424b-370"><a name="timed"></a> Eventos de temporización</span><span class="sxs-lookup"><span data-stu-id="9424b-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="9424b-371">A veces desea toochart cuánto tiempo tarda tooperform una acción.</span><span class="sxs-lookup"><span data-stu-id="9424b-371">Sometimes you want toochart how long it takes tooperform an action.</span></span> <span data-ttu-id="9424b-372">Por ejemplo, puede querer tooknow cuánto tiempo los usuarios realizar tooconsider opciones en un juego.</span><span class="sxs-lookup"><span data-stu-id="9424b-372">For example, you might want tooknow how long users take tooconsider choices in a game.</span></span> <span data-ttu-id="9424b-373">Puede usar el parámetro de medición de Hola para esto.</span><span class="sxs-lookup"><span data-stu-id="9424b-373">You can use hello measurement parameter for this.</span></span>

<span data-ttu-id="9424b-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="9424b-375"><a name="defaults"></a>Propiedades predeterminadas para la telemetría personalizada</span><span class="sxs-lookup"><span data-stu-id="9424b-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="9424b-376">Si desea tooset valores de propiedad predeterminados para algunos de los eventos personalizados de hello creado por usted, se puede establecer en una instancia de TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="9424b-376">If you want tooset default property values for some of hello custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="9424b-377">Son elementos de telemetría tooevery adjunto que se envían desde ese cliente.</span><span class="sxs-lookup"><span data-stu-id="9424b-377">They are attached tooevery telemetry item that's sent from that client.</span></span>

<span data-ttu-id="9424b-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="9424b-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9424b-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="9424b-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="9424b-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="9424b-381">Llamadas de telemetría individual pueden invalidar valores predeterminados de hello en los diccionarios de propiedad.</span><span class="sxs-lookup"><span data-stu-id="9424b-381">Individual telemetry calls can override hello default values in their property dictionaries.</span></span>

<span data-ttu-id="9424b-382">*Para los clientes web de JavaScript*, [use los inicializadores de telemetría de JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="9424b-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="9424b-383">*telemetría de tooadd propiedades tooall*, incluidos los datos de Hola de los módulos de colección estándar, [implementar `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="9424b-383">*tooadd properties tooall telemetry*, including hello data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="9424b-384">Muestreo, filtrado y procesamiento de telemetría</span><span class="sxs-lookup"><span data-stu-id="9424b-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="9424b-385">Puede escribir código tooprocess la telemetría antes de que se envíe desde Hola SDK.</span><span class="sxs-lookup"><span data-stu-id="9424b-385">You can write code tooprocess your telemetry before it's sent from hello SDK.</span></span> <span data-ttu-id="9424b-386">el procesamiento de Hello incluye datos que se envían desde los módulos de telemetría estándar hello, como colección de solicitud HTTP y la colección de dependencias.</span><span class="sxs-lookup"><span data-stu-id="9424b-386">hello processing includes data that's sent from hello standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="9424b-387">[Agregar propiedades](app-insights-api-filtering-sampling.md#add-properties) tootelemetry implementando `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="9424b-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) tootelemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="9424b-388">Por ejemplo, puede agregar números de versión o valores calculados a partir de otras propiedades.</span><span class="sxs-lookup"><span data-stu-id="9424b-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="9424b-389">[Filtrado](app-insights-api-filtering-sampling.md#filtering) puede modificar o descartar telemetría antes de que se envíe de hello SDK mediante la implementación de `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="9424b-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from hello SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="9424b-390">Controlar lo que se envía o se descartan, pero tienes tooaccount de efecto de hello en las métricas.</span><span class="sxs-lookup"><span data-stu-id="9424b-390">You control what is sent or discarded, but you have tooaccount for hello effect on your metrics.</span></span> <span data-ttu-id="9424b-391">Dependiendo de cómo descartar elementos, podría perder Hola capacidad toonavigate entre los elementos relacionados.</span><span class="sxs-lookup"><span data-stu-id="9424b-391">Depending on how you discard items, you might lose hello ability toonavigate between related items.</span></span>

<span data-ttu-id="9424b-392">[Muestreo](app-insights-api-filtering-sampling.md) es un volumen de solución empaquetada tooreduce Hola de datos que se envían desde el portal de toohello de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9424b-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution tooreduce hello volume of data that's sent from your app toohello portal.</span></span> <span data-ttu-id="9424b-393">Lo hace sin que afecte a las métricas de muestra de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-393">It does so without affecting hello displayed metrics.</span></span> <span data-ttu-id="9424b-394">Y lo hace sin que afecte a los problemas de capacidad toodiagnose por navegar entre elementos relacionados, como excepciones, las solicitudes y las vistas de página.</span><span class="sxs-lookup"><span data-stu-id="9424b-394">And it does so without affecting your ability toodiagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="9424b-395">[Más información](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="9424b-396">Deshabilitación de la telemetría</span><span class="sxs-lookup"><span data-stu-id="9424b-396">Disabling telemetry</span></span>
<span data-ttu-id="9424b-397">demasiado*dinámicamente detener e iniciar* Hola recopilación y transmisión de telemetría:</span><span class="sxs-lookup"><span data-stu-id="9424b-397">too*dynamically stop and start* hello collection and transmission of telemetry:</span></span>

<span data-ttu-id="9424b-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="9424b-399">demasiado*deshabilitar los recopiladores estándares seleccionados*: por ejemplo, los contadores de rendimiento, las solicitudes HTTP o dependencias: eliminar o marque como comentario las líneas relevantes de hello en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Para hacer esto, por ejemplo, si desea que toosend sus propios datos TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="9424b-399">too*disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <span data-ttu-id="9424b-400"><a name="debug"></a>Modo de programador</span><span class="sxs-lookup"><span data-stu-id="9424b-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="9424b-401">Durante la depuración, resulta útil toohave la telemetría acelerada a través de la canalización de Hola para que puedan ver los resultados inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="9424b-401">During debugging, it's useful toohave your telemetry expedited through hello pipeline so that you can see results immediately.</span></span> <span data-ttu-id="9424b-402">Get también mensajes adicionales que le ayudarán a seguimiento de los problemas con la telemetría Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-402">You also get additional messages that help you trace any problems with hello telemetry.</span></span> <span data-ttu-id="9424b-403">Desactívelo en producción, ya que puede ralentizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9424b-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="9424b-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="9424b-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="9424b-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="9424b-406"><a name="ikey"></a>Configuración de clave de instrumentación de Hola para telemetría personalizada seleccionada</span><span class="sxs-lookup"><span data-stu-id="9424b-406"><a name="ikey"></a> Setting hello instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="9424b-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="9424b-408"><a name="dynamic-ikey"></a> Copia de la clave de instrumentación</span><span class="sxs-lookup"><span data-stu-id="9424b-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="9424b-409">tooavoid combinación de telemetría de desarrollo, pruebas y entornos de producción, también puede [crear recursos de Application Insights separados](app-insights-create-new-resource.md) y cambiar sus claves, según el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-409">tooavoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on hello environment.</span></span>

<span data-ttu-id="9424b-410">En lugar de obtener clave de instrumentación de Hola Hola archivo de configuración, puede establecer en el código.</span><span class="sxs-lookup"><span data-stu-id="9424b-410">Instead of getting hello instrumentation key from hello configuration file, you can set it in your code.</span></span> <span data-ttu-id="9424b-411">Establezca la clave de hello en un método de inicialización, como global.aspx.cs en un servicio ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="9424b-411">Set hello key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="9424b-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="9424b-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="9424b-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9424b-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="9424b-414">En las páginas Web, le podría interesar tooset desde el servidor web de hello estado, en lugar de codificar de forma literal en script de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-414">In webpages, you might want tooset it from hello web server's state, rather than coding it literally into hello script.</span></span> <span data-ttu-id="9424b-415">Por ejemplo, en una página web generada en una aplicación ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="9424b-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="9424b-416">*JavaScript en Razor*</span><span class="sxs-lookup"><span data-stu-id="9424b-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="9424b-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="9424b-417">TelemetryContext</span></span>
<span data-ttu-id="9424b-418">TelemetryClient tiene una propiedad de Context, que contiene valores que se envían junto con todos los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="9424b-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="9424b-419">Normalmente se establecen mediante módulos de hello telemetría estándar, pero también puede establecerlas usted mismo.</span><span class="sxs-lookup"><span data-stu-id="9424b-419">They are normally set by hello standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="9424b-420">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9424b-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="9424b-421">Si se establece cualquiera de estos valores usted mismo, considere la posibilidad de quitar la línea correspondiente de Hola de [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), de modo que no confundir a los valores y Hola estándar.</span><span class="sxs-lookup"><span data-stu-id="9424b-421">If you set any of these values yourself, consider removing hello relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and hello standard values don't get confused.</span></span>

* <span data-ttu-id="9424b-422">**Componente**: Hola aplicación y su versión.</span><span class="sxs-lookup"><span data-stu-id="9424b-422">**Component**: hello app and its version.</span></span>
* <span data-ttu-id="9424b-423">**Dispositivo**: datos sobre el que se ejecuta la aplicación hello de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-423">**Device**: Data about hello device where hello app is running.</span></span> <span data-ttu-id="9424b-424">(En las aplicaciones web, esto es servidor de Hola o dispositivo de cliente que telemetría Hola se envía desde.)</span><span class="sxs-lookup"><span data-stu-id="9424b-424">(In web apps, this is hello server or client device that hello telemetry is sent from.)</span></span>
* <span data-ttu-id="9424b-425">**InstrumentationKey**: Hola recursos de Application Insights en Azure dónde deben aparecer telemetría Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-425">**InstrumentationKey**: hello Application Insights resource in Azure where hello telemetry appear.</span></span> <span data-ttu-id="9424b-426">Normalmente, se selecciona de ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="9424b-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="9424b-427">**Ubicación**: Hola ubicación geográfica del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-427">**Location**: hello geographic location of hello device.</span></span>
* <span data-ttu-id="9424b-428">**Operación**: en las aplicaciones web, Hola solicitud HTTP actual.</span><span class="sxs-lookup"><span data-stu-id="9424b-428">**Operation**: In web apps, hello current HTTP request.</span></span> <span data-ttu-id="9424b-429">En otros tipos de aplicación, puede establecer esta eventos toogroup juntos.</span><span class="sxs-lookup"><span data-stu-id="9424b-429">In other app types, you can set this toogroup events together.</span></span>
  * <span data-ttu-id="9424b-430">**Id**: valor generado que correlaciona distintos eventos, de modo que cuando usted inspeccione cualquier evento en Búsqueda de diagnóstico, puede encontrar elementos relacionados.</span><span class="sxs-lookup"><span data-stu-id="9424b-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="9424b-431">**Nombre**: un identificador, normalmente Hola dirección URL de solicitud de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="9424b-431">**Name**: An identifier, usually hello URL of hello HTTP request.</span></span>
  * <span data-ttu-id="9424b-432">**SyntheticSource**: si no nulo o está vacío, una cadena que indica que ese origen Hola de solicitud de hello ha identificado como una prueba web o robot.</span><span class="sxs-lookup"><span data-stu-id="9424b-432">**SyntheticSource**: If not null or empty, a string that indicates that hello source of hello request has been identified as a robot or web test.</span></span> <span data-ttu-id="9424b-433">De forma predeterminada, se excluye de cálculos en el Explorador de métricas.</span><span class="sxs-lookup"><span data-stu-id="9424b-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="9424b-434">**Properties**: propiedades que se envían con todos los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="9424b-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="9424b-435">Se pueden invalidar en llamadas de seguimiento* individuales.</span><span class="sxs-lookup"><span data-stu-id="9424b-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="9424b-436">**Sesión**: sesión de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9424b-436">**Session**: hello user's session.</span></span> <span data-ttu-id="9424b-437">Id. de Hello es establecer el valor de tooa generado, que se cambia cuando el usuario de hello no ha estado activo durante un tiempo.</span><span class="sxs-lookup"><span data-stu-id="9424b-437">hello ID is set tooa generated value, which is changed when hello user has not been active for a while.</span></span>
* <span data-ttu-id="9424b-438">**User**: información del usuario.</span><span class="sxs-lookup"><span data-stu-id="9424b-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="9424b-439">límites</span><span class="sxs-lookup"><span data-stu-id="9424b-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="9424b-440">tooavoid alcanzando el límite de velocidad de datos de hello, use [muestreo](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-440">tooavoid hitting hello data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="9424b-441">toodetermine cómo se mantienen los datos de tipo long, consulte [retención de datos y privacidad](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-441">toodetermine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="9424b-442">Documentos de referencia</span><span class="sxs-lookup"><span data-stu-id="9424b-442">Reference docs</span></span>
* [<span data-ttu-id="9424b-443">Referencia de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9424b-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="9424b-444">Referencia de Java</span><span class="sxs-lookup"><span data-stu-id="9424b-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="9424b-445">Referencia de JavaScript</span><span class="sxs-lookup"><span data-stu-id="9424b-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="9424b-446">SDK de Android</span><span class="sxs-lookup"><span data-stu-id="9424b-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="9424b-447">SDK de iOS</span><span class="sxs-lookup"><span data-stu-id="9424b-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="9424b-448">Código del SDK</span><span class="sxs-lookup"><span data-stu-id="9424b-448">SDK code</span></span>
* [<span data-ttu-id="9424b-449">SDK básico de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9424b-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="9424b-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="9424b-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="9424b-451">Paquetes de Windows Server</span><span class="sxs-lookup"><span data-stu-id="9424b-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="9424b-452">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="9424b-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="9424b-453">SDK de JavaScript</span><span class="sxs-lookup"><span data-stu-id="9424b-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="9424b-454">Todas las plataformas</span><span class="sxs-lookup"><span data-stu-id="9424b-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="9424b-455">Preguntas</span><span class="sxs-lookup"><span data-stu-id="9424b-455">Questions</span></span>
* <span data-ttu-id="9424b-456">*¿Qué excepciones pueden iniciar las llamadas de seguimiento_()?*</span><span class="sxs-lookup"><span data-stu-id="9424b-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="9424b-457">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="9424b-457">None.</span></span> <span data-ttu-id="9424b-458">No es necesario toowrap usarlas en las cláusulas try-catch.</span><span class="sxs-lookup"><span data-stu-id="9424b-458">You don't need toowrap them in try-catch clauses.</span></span> <span data-ttu-id="9424b-459">Si Hola SDK detecta problemas, registrará mensajes de salida de consola de depuración de hello y--si hello los mensajes lleguen a través de: en la búsqueda de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="9424b-459">If hello SDK encounters problems, it will log messages in hello debug console output and--if hello messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="9424b-460">*¿Hay un dato de tooget de API de REST desde el portal de hello?*</span><span class="sxs-lookup"><span data-stu-id="9424b-460">*Is there a REST API tooget data from hello portal?*</span></span>

    <span data-ttu-id="9424b-461">Sí, Hola [API de acceso a datos](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="9424b-461">Yes, hello [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="9424b-462">Incluyen otros datos de formas tooextract [exportar de análisis tooPower BI](app-insights-export-power-bi.md) y [exportación continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="9424b-462">Other ways tooextract data include [export from Analytics tooPower BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="9424b-463"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9424b-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="9424b-464">Búsqueda de eventos y registros</span><span class="sxs-lookup"><span data-stu-id="9424b-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="9424b-465">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="9424b-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


