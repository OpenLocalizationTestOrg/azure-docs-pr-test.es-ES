---
title: "API de Application Insights para eventos y métricas personalizados | Microsoft Docs"
description: "Inserte unas cuantas líneas de código en su aplicación de dispositivo o de escritorio, página o servicio web, para realizar el seguimiento del uso y diagnosticar problemas."
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
ms.openlocfilehash: e94c50de51612243386d89c5e0b3178a4f9cbd38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a><span data-ttu-id="b31bf-103">API de Application Insights para eventos y métricas personalizados</span><span class="sxs-lookup"><span data-stu-id="b31bf-103">Application Insights API for custom events and metrics</span></span>

<span data-ttu-id="b31bf-104">Inserte unas cuantas líneas de código en la aplicación para averiguar qué uso hacen de ella los usuarios o para ayudarle a diagnosticar problemas.</span><span class="sxs-lookup"><span data-stu-id="b31bf-104">Insert a few lines of code in your application to find out what users are doing with it, or to help diagnose issues.</span></span> <span data-ttu-id="b31bf-105">Puede enviar datos de telemetría desde aplicaciones de escritorio y de dispositivo y desde clientes y servidores web.</span><span class="sxs-lookup"><span data-stu-id="b31bf-105">You can send telemetry from device and desktop apps, web clients, and web servers.</span></span> <span data-ttu-id="b31bf-106">Use la API de telemetría principal de [Azure Application Insights](app-insights-overview.md) para enviar métricas y eventos personalizados, así como sus propias versiones de telemetría estándar.</span><span class="sxs-lookup"><span data-stu-id="b31bf-106">Use the [Azure Application Insights](app-insights-overview.md) core telemetry API to send custom events and metrics, and your own versions of standard telemetry.</span></span> <span data-ttu-id="b31bf-107">Esta API es la misma que usan los recopiladores de datos estándar de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b31bf-107">This API is the same API that the standard Application Insights data collectors use.</span></span>

## <a name="api-summary"></a><span data-ttu-id="b31bf-108">API summary</span><span class="sxs-lookup"><span data-stu-id="b31bf-108">API summary</span></span>
<span data-ttu-id="b31bf-109">La API es uniforme en todas las plataformas, excepto por algunas pequeñas variaciones.</span><span class="sxs-lookup"><span data-stu-id="b31bf-109">The API is uniform across all platforms, apart from a few small variations.</span></span>

| <span data-ttu-id="b31bf-110">Método</span><span class="sxs-lookup"><span data-stu-id="b31bf-110">Method</span></span> | <span data-ttu-id="b31bf-111">Usado para</span><span class="sxs-lookup"><span data-stu-id="b31bf-111">Used for</span></span> |
| --- | --- |
| [`TrackPageView`](#page-views) |<span data-ttu-id="b31bf-112">Páginas, pantallas, hojas o formularios.</span><span class="sxs-lookup"><span data-stu-id="b31bf-112">Pages, screens, blades, or forms.</span></span> |
| [`TrackEvent`](#trackevent) |<span data-ttu-id="b31bf-113">Acciones de usuario y otros eventos.</span><span class="sxs-lookup"><span data-stu-id="b31bf-113">User actions and other events.</span></span> <span data-ttu-id="b31bf-114">Se usa para realizar el seguimiento del comportamiento de los usuarios o para supervisar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b31bf-114">Used to track user behavior or to monitor performance.</span></span> |
| [`TrackMetric`](#trackmetric) |<span data-ttu-id="b31bf-115">Las medidas de rendimiento, como las longitudes de cola, no están relacionadas con eventos específicos.</span><span class="sxs-lookup"><span data-stu-id="b31bf-115">Performance measurements such as queue lengths not related to specific events.</span></span> |
| [`TrackException`](#trackexception) |<span data-ttu-id="b31bf-116">Excepciones de registro para diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b31bf-116">Logging exceptions for diagnosis.</span></span> <span data-ttu-id="b31bf-117">Permite realizar el seguimiento del lugar donde se producen en relación con otros eventos y examinar los seguimientos de pila.</span><span class="sxs-lookup"><span data-stu-id="b31bf-117">Trace where they occur in relation to other events and examine stack traces.</span></span> |
| [`TrackRequest`](#trackrequest) |<span data-ttu-id="b31bf-118">Registro de la frecuencia y duración de las solicitudes de servidor para el análisis de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b31bf-118">Logging the frequency and duration of server requests for performance analysis.</span></span> |
| [`TrackTrace`](#tracktrace) |<span data-ttu-id="b31bf-119">Mensajes de registro de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b31bf-119">Diagnostic log messages.</span></span> <span data-ttu-id="b31bf-120">También puede capturar registros de terceros.</span><span class="sxs-lookup"><span data-stu-id="b31bf-120">You can also capture third-party logs.</span></span> |
| [`TrackDependency`](#trackdependency) |<span data-ttu-id="b31bf-121">Registro de la duración y frecuencia de las llamadas a componentes externos de los que depende la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b31bf-121">Logging the duration and frequency of calls to external components that your app depends on.</span></span> |

<span data-ttu-id="b31bf-122">Puede [adjuntar propiedades y métricas](#properties) a la mayoría de estas llamadas de telemetría.</span><span class="sxs-lookup"><span data-stu-id="b31bf-122">You can [attach properties and metrics](#properties) to most of these telemetry calls.</span></span>

## <span data-ttu-id="b31bf-123"><a name="prep"></a>Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="b31bf-123"><a name="prep"></a>Before you start</span></span>
<span data-ttu-id="b31bf-124">Si aún no tiene una referencia en el SDK de Application Insights:</span><span class="sxs-lookup"><span data-stu-id="b31bf-124">If you don't have a reference on Application Insights SDK yet:</span></span>

* <span data-ttu-id="b31bf-125">Agregue el SDK de Application Insights a su proyecto:</span><span class="sxs-lookup"><span data-stu-id="b31bf-125">Add the Application Insights SDK to your project:</span></span>

  * [<span data-ttu-id="b31bf-126">Proyecto de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b31bf-126">ASP.NET project</span></span>](app-insights-asp-net.md)
  * [<span data-ttu-id="b31bf-127">Proyecto de Java</span><span class="sxs-lookup"><span data-stu-id="b31bf-127">Java project</span></span>](app-insights-java-get-started.md)
  * [<span data-ttu-id="b31bf-128">JavaScript en cada página web</span><span class="sxs-lookup"><span data-stu-id="b31bf-128">JavaScript in each webpage</span></span>](app-insights-javascript.md) 
* <span data-ttu-id="b31bf-129">En el código de servidor web o de dispositivo, incluya:</span><span class="sxs-lookup"><span data-stu-id="b31bf-129">In your device or web server code, include:</span></span>

    <span data-ttu-id="b31bf-130">*C#:* `using Microsoft.ApplicationInsights;`</span><span class="sxs-lookup"><span data-stu-id="b31bf-130">*C#:* `using Microsoft.ApplicationInsights;`</span></span>

    <span data-ttu-id="b31bf-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span><span class="sxs-lookup"><span data-stu-id="b31bf-131">*Visual Basic:* `Imports Microsoft.ApplicationInsights`</span></span>

    <span data-ttu-id="b31bf-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span><span class="sxs-lookup"><span data-stu-id="b31bf-132">*Java:* `import com.microsoft.applicationinsights.TelemetryClient;`</span></span>

## <a name="constructing-a-telemetryclient-instance"></a><span data-ttu-id="b31bf-133">Construcción de una instancia de TelemetryClient</span><span class="sxs-lookup"><span data-stu-id="b31bf-133">Constructing a TelemetryClient instance</span></span>
<span data-ttu-id="b31bf-134">Construcción de una instancia de `TelemetryClient` (excepto en JavaScript en páginas web):</span><span class="sxs-lookup"><span data-stu-id="b31bf-134">Construct an instance of `TelemetryClient` (except in JavaScript in webpages):</span></span>

<span data-ttu-id="b31bf-135">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-135">*C#*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="b31bf-136">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b31bf-136">*Visual Basic*</span></span>

    Private Dim telemetry As New TelemetryClient

<span data-ttu-id="b31bf-137">*Java*</span><span class="sxs-lookup"><span data-stu-id="b31bf-137">*Java*</span></span>

    private TelemetryClient telemetry = new TelemetryClient();

<span data-ttu-id="b31bf-138">TelemetryClient es seguro para subprocesos.</span><span class="sxs-lookup"><span data-stu-id="b31bf-138">TelemetryClient is thread-safe.</span></span>

<span data-ttu-id="b31bf-139">Se recomienda que use una instancia de TelemetryClient para cada módulo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b31bf-139">We recommend that you use an instance of TelemetryClient for each module of your app.</span></span> <span data-ttu-id="b31bf-140">Por ejemplo, puede tener una instancia de TelemetryClient en el servicio web para informar de las solicitudes HTTP entrantes y otra en una clase de middleware para notificar eventos de la lógica de negocios.</span><span class="sxs-lookup"><span data-stu-id="b31bf-140">For instance, you may have one TelemetryClient instance in your web service to report incoming HTTP requests, and another in a middleware class to report business logic events.</span></span> <span data-ttu-id="b31bf-141">Puede establecer propiedades tales como `TelemetryClient.Context.User.Id` para realizar el seguimiento de los usuarios y de las sesiones, o bien `TelemetryClient.Context.Device.Id` para identificar el equipo.</span><span class="sxs-lookup"><span data-stu-id="b31bf-141">You can set properties such as `TelemetryClient.Context.User.Id` to track users and sessions, or `TelemetryClient.Context.Device.Id` to identify the machine.</span></span> <span data-ttu-id="b31bf-142">Esta información se adjunta a todos los eventos enviados por la instancia.</span><span class="sxs-lookup"><span data-stu-id="b31bf-142">This information is attached to all events that the instance sends.</span></span>

## <a name="trackevent"></a><span data-ttu-id="b31bf-143">TrackEvent</span><span class="sxs-lookup"><span data-stu-id="b31bf-143">TrackEvent</span></span>
<span data-ttu-id="b31bf-144">En Application Insights, un *evento personalizado* es un punto de datos que se puede mostrar en el [Explorador de métricas](app-insights-metrics-explorer.md) como recuento agregado, y como repeticiones individuales en [Búsqueda de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-144">In Application Insights, a *custom event* is a data point that you can display in [Metrics Explorer](app-insights-metrics-explorer.md) as an aggregated count, and in [Diagnostic Search](app-insights-diagnostic-search.md) as individual occurrences.</span></span> <span data-ttu-id="b31bf-145">(No está relacionado con MVC ni con "eventos" de otro marco).</span><span class="sxs-lookup"><span data-stu-id="b31bf-145">(It isn't related to MVC or other framework "events.")</span></span>

<span data-ttu-id="b31bf-146">Inserte llamadas a `TrackEvent` en el código para contabilizar diversos eventos:</span><span class="sxs-lookup"><span data-stu-id="b31bf-146">Insert `TrackEvent` calls in your code to count various events.</span></span> <span data-ttu-id="b31bf-147">la frecuencia con la que los usuarios eligen una determinada característica, con la que logran unos determinados objetivos o con la que cometen determinados tipos de errores.</span><span class="sxs-lookup"><span data-stu-id="b31bf-147">How often users choose a particular feature, how often they achieve particular goals, or maybe how often they make particular types of mistakes.</span></span>

<span data-ttu-id="b31bf-148">Por ejemplo, en una aplicación de juego, envíe un evento cada vez que un usuario gane el juego:</span><span class="sxs-lookup"><span data-stu-id="b31bf-148">For example, in a game app, send an event whenever a user wins the game:</span></span>

<span data-ttu-id="b31bf-149">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b31bf-149">*JavaScript*</span></span>

    appInsights.trackEvent("WinGame");

<span data-ttu-id="b31bf-150">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-150">*C#*</span></span>

    telemetry.TrackEvent("WinGame");

<span data-ttu-id="b31bf-151">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b31bf-151">*Visual Basic*</span></span>

    telemetry.TrackEvent("WinGame")

<span data-ttu-id="b31bf-152">*Java*</span><span class="sxs-lookup"><span data-stu-id="b31bf-152">*Java*</span></span>

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-the-microsoft-azure-portal"></a><span data-ttu-id="b31bf-153">Visualización de eventos en Microsoft Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b31bf-153">View your events in the Microsoft Azure portal</span></span>
<span data-ttu-id="b31bf-154">Para ver un recuento de los eventos, abra una hoja [Explorador de métricas](app-insights-metrics-explorer.md), agregue un nuevo gráfico y seleccione **Eventos**.</span><span class="sxs-lookup"><span data-stu-id="b31bf-154">To see a count of your events, open a [Metrics Explorer](app-insights-metrics-explorer.md) blade, add a new chart, and select **Events**.</span></span>  

![Visualización de un recuento de eventos personalizados](./media/app-insights-api-custom-events-metrics/01-custom.png)

<span data-ttu-id="b31bf-156">Para comparar los recuentos de eventos diferentes, establezca el tipo de gráfico en **Cuadrícula** y el grupo por nombre de evento:</span><span class="sxs-lookup"><span data-stu-id="b31bf-156">To compare the counts of different events, set the chart type to **Grid**, and group by event name:</span></span>

![Establecimiento del tipo de gráfico y agrupación](./media/app-insights-api-custom-events-metrics/07-grid.png)

<span data-ttu-id="b31bf-158">En la cuadrícula, haga clic en un nombre de evento para ver todas las repeticiones individuales de ese evento.</span><span class="sxs-lookup"><span data-stu-id="b31bf-158">On the grid, click through an event name to see individual occurrences of that event.</span></span> <span data-ttu-id="b31bf-159">Para más información, haga clic en cualquier elemento de la lista.</span><span class="sxs-lookup"><span data-stu-id="b31bf-159">To see more detail - click any occurrence in the list.</span></span>

![Obtenga detalles de los eventos.](./media/app-insights-api-custom-events-metrics/03-instances.png)

<span data-ttu-id="b31bf-161">Para centrarse en eventos concretos de la Búsqueda o el Explorador de métricas, establezca el filtro de la hoja en los nombres de eventos que le interesan:</span><span class="sxs-lookup"><span data-stu-id="b31bf-161">To focus on specific events in either Search or Metrics Explorer, set the blade's filter to the event names that you're interested in:</span></span>

![Abre filtros, expanda el nombre del evento y seleccione uno o varios valores.](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a><span data-ttu-id="b31bf-163">Eventos personalizados en Analytics</span><span class="sxs-lookup"><span data-stu-id="b31bf-163">Custom events in Analytics</span></span>

<span data-ttu-id="b31bf-164">La telemetría está disponible en la tabla `customEvents` de [Analytics de Application Insights](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-164">The telemetry is available in the `customEvents` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="b31bf-165">Cada fila representa una llamada a `trackEvent(..)` en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b31bf-165">Each row represents a call to `trackEvent(..)` in your app.</span></span> 

<span data-ttu-id="b31bf-166">Si el [muestreo](app-insights-sampling.md) está en uso, en la propiedad itemCount se muestra un valor mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="b31bf-166">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="b31bf-167">Por ejemplo, itemCount==10 significa que de cada 10 llamadas a trackEvent(), el proceso de muestreo solo transmite una.</span><span class="sxs-lookup"><span data-stu-id="b31bf-167">For example itemCount==10 means that of 10 calls to trackEvent(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="b31bf-168">Para obtener un recuento correcto de eventos personalizados, debería usar código como `customEvent | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-168">To get a correct count of custom events, you should use therefore use code such as `customEvent | summarize sum(itemCount)`.</span></span>


## <a name="trackmetric"></a><span data-ttu-id="b31bf-169">TrackMetric</span><span class="sxs-lookup"><span data-stu-id="b31bf-169">TrackMetric</span></span>

<span data-ttu-id="b31bf-170">Application Insights puede crear gráficos de métricas que no estén conectadas a eventos concretos.</span><span class="sxs-lookup"><span data-stu-id="b31bf-170">Application Insights can chart metrics that are not attached to particular events.</span></span> <span data-ttu-id="b31bf-171">Por ejemplo, puede supervisar una longitud de cola a intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="b31bf-171">For example, you could monitor a queue length at regular intervals.</span></span> <span data-ttu-id="b31bf-172">En el caso de las métricas, las mediciones individuales tienen menos interés que las variaciones y tendencias; por tanto, los gráficos estadísticos resultan útiles.</span><span class="sxs-lookup"><span data-stu-id="b31bf-172">With metrics, the individual measurements are of less interest than the variations and trends, and so statistical charts are useful.</span></span>

<span data-ttu-id="b31bf-173">Para enviar las métricas a Application Insights, puede usar la API `TrackMetric(..)`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-173">In order to send metrics to Application Insights, you can use the `TrackMetric(..)` API.</span></span> <span data-ttu-id="b31bf-174">Hay dos formas de enviar una métrica:</span><span class="sxs-lookup"><span data-stu-id="b31bf-174">There are two ways to send a metric:</span></span> 

* <span data-ttu-id="b31bf-175">Valor único.</span><span class="sxs-lookup"><span data-stu-id="b31bf-175">Single value.</span></span> <span data-ttu-id="b31bf-176">Cada vez que realiza una medición en la aplicación, envía el valor correspondiente a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b31bf-176">Every time you perform a measurement in your application, you send the corresponding value to Application Insights.</span></span> <span data-ttu-id="b31bf-177">Por ejemplo, suponga que cuenta con una métrica que describe el número de elementos de un contenedor.</span><span class="sxs-lookup"><span data-stu-id="b31bf-177">For example, assume that you have a metric describing the number of items in a container.</span></span> <span data-ttu-id="b31bf-178">Durante un período determinado, primero coloca tres elementos en el contenedor y seguidamente retira dos.</span><span class="sxs-lookup"><span data-stu-id="b31bf-178">During a particular time period, you first put three items into the container and then you remove two items.</span></span> <span data-ttu-id="b31bf-179">En consecuencia, llamaría a `TrackMetric` dos veces: la primera, para pasar el valor `3` y a continuación el valor `-2`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-179">Accordingly, you would call `TrackMetric` twice: first passing the value `3` and then the value `-2`.</span></span> <span data-ttu-id="b31bf-180">Application Insights almacena ambos valores en su nombre.</span><span class="sxs-lookup"><span data-stu-id="b31bf-180">Application Insights stores both values on your behalf.</span></span> 

* <span data-ttu-id="b31bf-181">Agregación.</span><span class="sxs-lookup"><span data-stu-id="b31bf-181">Aggregation.</span></span> <span data-ttu-id="b31bf-182">Al trabajar con métricas, las mediciones individuales pocas veces resultan de interés.</span><span class="sxs-lookup"><span data-stu-id="b31bf-182">When working with metrics, every single measurement is rarely of interest.</span></span> <span data-ttu-id="b31bf-183">En su lugar, lo importante son los resúmenes de acontecimientos durante un período determinado.</span><span class="sxs-lookup"><span data-stu-id="b31bf-183">Instead a summary of what happened during a particular time period is important.</span></span> <span data-ttu-id="b31bf-184">Los resúmenes de este tipo se denominan _agregaciones_.</span><span class="sxs-lookup"><span data-stu-id="b31bf-184">Such a summary is called _aggregation_.</span></span> <span data-ttu-id="b31bf-185">En el ejemplo anterior, la suma de las métricas agregadas del período correspondiente es de `1` y el recuento de los valores de las métricas es de `2`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-185">In the above example, the aggregate metric sum for that time period is `1` and the count of the metric values is `2`.</span></span> <span data-ttu-id="b31bf-186">Al usar el método de agregación, solo invocará `TrackMetric` una vez por período y enviará los valores agregados.</span><span class="sxs-lookup"><span data-stu-id="b31bf-186">When using the aggregation approach, you only invoke `TrackMetric` once per time period and send the aggregate values.</span></span> <span data-ttu-id="b31bf-187">Este es el método que se recomienda usar, ya que puede reducir significativamente los costos y la sobrecarga de rendimiento gracias a que envía menos puntos de datos a Application Insights, a pesar de seguir recopilado toda la información pertinente.</span><span class="sxs-lookup"><span data-stu-id="b31bf-187">This is the recommended approach since it can significantly reduce the cost and performance overhead by sending fewer data points to Application Insights, while still collecting all relevant information.</span></span>

### <a name="examples"></a><span data-ttu-id="b31bf-188">Ejemplos:</span><span class="sxs-lookup"><span data-stu-id="b31bf-188">Examples:</span></span>

#### <a name="single-values"></a><span data-ttu-id="b31bf-189">Valores únicos</span><span class="sxs-lookup"><span data-stu-id="b31bf-189">Single values</span></span>

<span data-ttu-id="b31bf-190">Para enviar un único valor de métrica:</span><span class="sxs-lookup"><span data-stu-id="b31bf-190">To send a single metric value:</span></span>

<span data-ttu-id="b31bf-191">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b31bf-191">*JavaScript*</span></span>

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

<span data-ttu-id="b31bf-192">*C#, Java*</span><span class="sxs-lookup"><span data-stu-id="b31bf-192">*C#, Java*</span></span>

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a><span data-ttu-id="b31bf-193">Agregación de métricas</span><span class="sxs-lookup"><span data-stu-id="b31bf-193">Aggregating metrics</span></span>

<span data-ttu-id="b31bf-194">Se recomienda agregar las métricas antes de enviarlas desde la aplicación para reducir el ancho de banda y los costos, y aumentar el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="b31bf-194">It is recommended to aggregate metrics before sending them from your app, to reduce bandwidth, cost and to improve performance.</span></span>
<span data-ttu-id="b31bf-195">Este es un ejemplo de código de agregación:</span><span class="sxs-lookup"><span data-stu-id="b31bf-195">Here is an example of aggregating code:</span></span>

<span data-ttu-id="b31bf-196">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-196">*C#*</span></span>

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
    /// Accepts metric values and sends the aggregated values at 1-minute intervals.
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
                    // Wait for end end of the aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap the current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute the actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct the metric telemetry item and send:
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

### <a name="custom-metrics-in-metrics-explorer"></a><span data-ttu-id="b31bf-197">Métricas personalizadas en el Explorador de métricas</span><span class="sxs-lookup"><span data-stu-id="b31bf-197">Custom metrics in Metrics Explorer</span></span>

<span data-ttu-id="b31bf-198">Para ver los resultados, abra el Explorador de métricas y agregue un gráfico nuevo.</span><span class="sxs-lookup"><span data-stu-id="b31bf-198">To see the results, open Metrics Explorer and add a new chart.</span></span> <span data-ttu-id="b31bf-199">Edite el gráfico para que muestre la métrica.</span><span class="sxs-lookup"><span data-stu-id="b31bf-199">Edit the chart to show your metric.</span></span>

> [!NOTE]
> <span data-ttu-id="b31bf-200">La métrica personalizada puede tardar varios minutos en aparecer en la lista de métricas disponibles.</span><span class="sxs-lookup"><span data-stu-id="b31bf-200">Your custom metric might take several minutes to appear in the list of available metrics.</span></span>
>

![Agregue un gráfico nuevo o seleccione un gráfico y, en Personalizada, seleccione su métrica.](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a><span data-ttu-id="b31bf-202">Métricas personalizadas en Analytics</span><span class="sxs-lookup"><span data-stu-id="b31bf-202">Custom metrics in Analytics</span></span>

<span data-ttu-id="b31bf-203">La telemetría está disponible en la tabla `customMetrics` de [Analytics de Application Insights](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-203">The telemetry is available in the `customMetrics` table in [Application Insights Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="b31bf-204">Cada fila representa una llamada a `trackMetric(..)` en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b31bf-204">Each row represents a call to `trackMetric(..)` in your app.</span></span>
* <span data-ttu-id="b31bf-205">`valueSum`: es la suma de las medidas.</span><span class="sxs-lookup"><span data-stu-id="b31bf-205">`valueSum` - This is the sum of the measurements.</span></span> <span data-ttu-id="b31bf-206">Para obtener el valor medio, divídalo por `valueCount`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-206">To get the mean value, divide by `valueCount`.</span></span>
* <span data-ttu-id="b31bf-207">`valueCount`: el número de medidas que se agregaron en esta llamada a `trackMetric(..)`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-207">`valueCount` - The number of measurements that were aggregated into this `trackMetric(..)` call.</span></span>

## <a name="page-views"></a><span data-ttu-id="b31bf-208">Vistas de página</span><span class="sxs-lookup"><span data-stu-id="b31bf-208">Page views</span></span>
<span data-ttu-id="b31bf-209">En una aplicación de dispositivo o de página web, se envían datos de telemetría de la vista de página de forma predeterminada cuando se carga cada pantalla o página.</span><span class="sxs-lookup"><span data-stu-id="b31bf-209">In a device or webpage app, page view telemetry is sent by default when each screen or page is loaded.</span></span> <span data-ttu-id="b31bf-210">Sin embargo, puede cambiar esta frecuencia para que se realice el seguimiento de las vistas de página en momentos diferentes o adicionales.</span><span class="sxs-lookup"><span data-stu-id="b31bf-210">But you can change that to track page views at additional or different times.</span></span> <span data-ttu-id="b31bf-211">Por ejemplo, en una aplicación que muestra pestañas u hojas, quizás quiera realizar el seguimiento de una página siempre que el usuario abra una nueva hoja.</span><span class="sxs-lookup"><span data-stu-id="b31bf-211">For example, in an app that displays tabs or blades, you might want to track a page whenever the user opens a new blade.</span></span>

![Uso de modos en la hoja Información general](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

<span data-ttu-id="b31bf-213">Los datos de usuario y de sesión se envían como propiedades junto con las vistas de página, por lo que los gráficos de usuario y de sesión se activan cuando hay datos de telemetría de vistas de página.</span><span class="sxs-lookup"><span data-stu-id="b31bf-213">User and session data is sent as properties along with page views, so the user and session charts come alive when there is page view telemetry.</span></span>

### <a name="custom-page-views"></a><span data-ttu-id="b31bf-214">Vistas de página personalizadas</span><span class="sxs-lookup"><span data-stu-id="b31bf-214">Custom page views</span></span>
<span data-ttu-id="b31bf-215">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b31bf-215">*JavaScript*</span></span>

    appInsights.trackPageView("tab1");

<span data-ttu-id="b31bf-216">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-216">*C#*</span></span>

    telemetry.TrackPageView("GameReviewPage");

<span data-ttu-id="b31bf-217">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b31bf-217">*Visual Basic*</span></span>

    telemetry.TrackPageView("GameReviewPage")


<span data-ttu-id="b31bf-218">Si tiene varias fichas dentro de páginas HTML diferentes, puede especificar también la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="b31bf-218">If you have several tabs within different HTML pages, you can specify the URL too:</span></span>

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a><span data-ttu-id="b31bf-219">Cronometrar las vistas de página</span><span class="sxs-lookup"><span data-stu-id="b31bf-219">Timing page views</span></span>
<span data-ttu-id="b31bf-220">De forma predeterminada, los tiempos notificados como **Tiempo de carga de la vista de página** se miden desde que el explorador envía la solicitud hasta que se llama al evento de carga de página del explorador.</span><span class="sxs-lookup"><span data-stu-id="b31bf-220">By default, the times reported as **Page view load time** are measured from when the browser sends the request, until the browser's page load event is called.</span></span>

<span data-ttu-id="b31bf-221">En su lugar, puede:</span><span class="sxs-lookup"><span data-stu-id="b31bf-221">Instead, you can either:</span></span>

* <span data-ttu-id="b31bf-222">Establecer una duración explícita en la llamada [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview): `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-222">Set an explicit duration in the [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) call: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.</span></span>
* <span data-ttu-id="b31bf-223">Usar las llamadas para cronometrar la vista de página `startTrackPage` y `stopTrackPage`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-223">Use the page view timing calls `startTrackPage` and `stopTrackPage`.</span></span>

<span data-ttu-id="b31bf-224">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b31bf-224">*JavaScript*</span></span>

    // To start timing a page:
    appInsights.startTrackPage("Page1");

<span data-ttu-id="b31bf-225">...</span><span class="sxs-lookup"><span data-stu-id="b31bf-225">...</span></span>

    // To stop timing and log the page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

<span data-ttu-id="b31bf-226">El nombre que use como primer parámetro asocia las llamadas inicial y final.</span><span class="sxs-lookup"><span data-stu-id="b31bf-226">The name that you use as the first parameter associates the start and stop calls.</span></span> <span data-ttu-id="b31bf-227">El valor predeterminado es el nombre de la página actual.</span><span class="sxs-lookup"><span data-stu-id="b31bf-227">It defaults to the current page name.</span></span>

<span data-ttu-id="b31bf-228">Las duraciones de carga de página resultantes que se muestran en el Explorador de métricas se derivan del intervalo que media entre las llamadas inicial y final.</span><span class="sxs-lookup"><span data-stu-id="b31bf-228">The resulting page load durations displayed in Metrics Explorer are derived from the interval between the start and stop calls.</span></span> <span data-ttu-id="b31bf-229">Depende del usuario qué intervalo se cronometra realmente.</span><span class="sxs-lookup"><span data-stu-id="b31bf-229">It's up to you what interval you actually time.</span></span>

### <a name="page-telemetry-in-analytics"></a><span data-ttu-id="b31bf-230">Telemetría de páginas en Analytics</span><span class="sxs-lookup"><span data-stu-id="b31bf-230">Page telemetry in Analytics</span></span>

<span data-ttu-id="b31bf-231">En [Analytics](app-insights-analytics.md) hay dos tablas en las que se muestran datos de operaciones de explorador:</span><span class="sxs-lookup"><span data-stu-id="b31bf-231">In [Analytics](app-insights-analytics.md) two tables show data from browser operations:</span></span>

* <span data-ttu-id="b31bf-232">La tabla `pageViews` contiene datos sobre la URL y el título de la página.</span><span class="sxs-lookup"><span data-stu-id="b31bf-232">The `pageViews` table contains data about the URL and page title</span></span>
* <span data-ttu-id="b31bf-233">La tabla `browserTimings` contiene datos sobre el rendimiento del cliente, como el tiempo que se tarda en procesar los datos entrantes.</span><span class="sxs-lookup"><span data-stu-id="b31bf-233">The `browserTimings` table contains data about client performance, such as the time taken to process the incoming data</span></span>

<span data-ttu-id="b31bf-234">Para averiguar cuánto tarda el explorador en procesar diferentes páginas:</span><span class="sxs-lookup"><span data-stu-id="b31bf-234">To find how long the browser takes to process different pages:</span></span>

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

<span data-ttu-id="b31bf-235">Para descubrir la popularidad de distintos exploradores:</span><span class="sxs-lookup"><span data-stu-id="b31bf-235">To discover the popularities of different browsers:</span></span>

```
pageViews | summarize count() by client_Browser
```

<span data-ttu-id="b31bf-236">Para asociar las vistas de página a las llamadas AJAX, realice una combinación con dependencias:</span><span class="sxs-lookup"><span data-stu-id="b31bf-236">To associate page views to AJAX calls, join with dependencies:</span></span>

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a><span data-ttu-id="b31bf-237">TrackRequest</span><span class="sxs-lookup"><span data-stu-id="b31bf-237">TrackRequest</span></span>
<span data-ttu-id="b31bf-238">El SDK del servidor usa TrackRequest para registrar las solicitudes de HTTP.</span><span class="sxs-lookup"><span data-stu-id="b31bf-238">The server SDK uses TrackRequest to log HTTP requests.</span></span>

<span data-ttu-id="b31bf-239">También puede llamarlo usted mismo si quiere simular solicitudes en un contexto en el que no se está ejecutando el módulo de servicio web.</span><span class="sxs-lookup"><span data-stu-id="b31bf-239">You can also call it yourself if you want to simulate requests in a context where you don't have the web service module running.</span></span>

<span data-ttu-id="b31bf-240">Sin embargo, lo que se recomienda para enviar telemetría de solicitudes es que la solicitud actúe como <a href="#operation-context">contexto de operación</a>.</span><span class="sxs-lookup"><span data-stu-id="b31bf-240">However, the recommended way to send request telemetry is where the request acts as an <a href="#operation-context">operation context</a>.</span></span>

## <a name="operation-context"></a><span data-ttu-id="b31bf-241">Contexto de operación</span><span class="sxs-lookup"><span data-stu-id="b31bf-241">Operation context</span></span>
<span data-ttu-id="b31bf-242">Se pueden asociar elementos de telemetría adjuntándoles un identificador de operación común.</span><span class="sxs-lookup"><span data-stu-id="b31bf-242">You can associate telemetry items together by attaching to them a common operation ID.</span></span> <span data-ttu-id="b31bf-243">El módulo de seguimiento de solicitud estándar realiza esta operación para excepciones y otros eventos enviados al procesar una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="b31bf-243">The standard request-tracking module does this for exceptions and other events that are sent while an HTTP request is being processed.</span></span> <span data-ttu-id="b31bf-244">En [Búsqueda](app-insights-diagnostic-search.md) y [Análisis](app-insights-analytics.md), puede utilizar el identificador para encontrar fácilmente los eventos asociados a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="b31bf-244">In [Search](app-insights-diagnostic-search.md) and [Analytics](app-insights-analytics.md), you can use the ID to easily find any events associated with the request.</span></span>

<span data-ttu-id="b31bf-245">La manera más fácil de establecer el identificador es definir un contexto de operación mediante este patrón:</span><span class="sxs-lookup"><span data-stu-id="b31bf-245">The easiest way to set the ID is to set an operation context by using this pattern:</span></span>

<span data-ttu-id="b31bf-246">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-246">*C#*</span></span>

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use the same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

<span data-ttu-id="b31bf-247">Junto con la configuración de un contexto de la operación, `StartOperation` crea un elemento de telemetría del tipo que especifique.</span><span class="sxs-lookup"><span data-stu-id="b31bf-247">Along with setting an operation context, `StartOperation` creates a telemetry item of the type that you specify.</span></span> <span data-ttu-id="b31bf-248">Envía el elemento de telemetría al eliminar la operación, o si llama explícitamente a `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-248">It sends the telemetry item when you dispose the operation, or if you explicitly call `StopOperation`.</span></span> <span data-ttu-id="b31bf-249">Si usa `RequestTelemetry` como tipo de telemetría, su duración se establece en el intervalo cronometrado entre el inicio y la detención.</span><span class="sxs-lookup"><span data-stu-id="b31bf-249">If you use `RequestTelemetry` as the telemetry type, its duration is set to the timed interval between start and stop.</span></span>

<span data-ttu-id="b31bf-250">Los contextos de operación no pueden estar anidados.</span><span class="sxs-lookup"><span data-stu-id="b31bf-250">Operation contexts can't be nested.</span></span> <span data-ttu-id="b31bf-251">Si ya existe un contexto de operación, su identificador está asociado a todos los elementos contenidos, incluido el elemento que se ha creado con `StartOperation`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-251">If there is already an operation context, then its ID is associated with all the contained items, including the item created with `StartOperation`.</span></span>

<span data-ttu-id="b31bf-252">En la Búsqueda, el contexto de la operación se utiliza para crear la lista de **Elementos relacionados**:</span><span class="sxs-lookup"><span data-stu-id="b31bf-252">In Search, the operation context is used to create the **Related Items** list:</span></span>

![Elementos relacionados](./media/app-insights-api-custom-events-metrics/21.png)

<span data-ttu-id="b31bf-254">Consulte [application-insights-custom-operations-tracking.md.md] para más información sobre el seguimiento de las operaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="b31bf-254">See [application-insights-custom-operations-tracking.md] for more information on custom operations tracking.</span></span>

### <a name="requests-in-analytics"></a><span data-ttu-id="b31bf-255">Solicitudes en Analytics</span><span class="sxs-lookup"><span data-stu-id="b31bf-255">Requests in Analytics</span></span> 

<span data-ttu-id="b31bf-256">En [Analytics de Application Insights](app-insights-analytics.md), las solicitudes aparecen en la tabla `requests`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-256">In [Application Insights Analytics](app-insights-analytics.md), requests show up in the `requests` table.</span></span>

<span data-ttu-id="b31bf-257">Si el [muestreo](app-insights-sampling.md) está en uso, en la propiedad de itemCount se mostrará un valor superior a 1.</span><span class="sxs-lookup"><span data-stu-id="b31bf-257">If [sampling](app-insights-sampling.md) is in operation, the itemCount property will show a value greater than 1.</span></span> <span data-ttu-id="b31bf-258">Por ejemplo, itemCount==10 significa que de cada 10 llamadas a trackRequest(), el proceso de muestreo solo transmite una.</span><span class="sxs-lookup"><span data-stu-id="b31bf-258">For example itemCount==10 means that of 10 calls to trackRequest(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="b31bf-259">Para obtener un recuento correcto de solicitudes y la duración media segmentada por nombres de solicitudes, use código como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="b31bf-259">To get a correct count of requests and average duration segmented by request names, use code such as:</span></span>

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a><span data-ttu-id="b31bf-260">TrackException</span><span class="sxs-lookup"><span data-stu-id="b31bf-260">TrackException</span></span>
<span data-ttu-id="b31bf-261">Enviar excepciones a Application Insights:</span><span class="sxs-lookup"><span data-stu-id="b31bf-261">Send exceptions to Application Insights:</span></span>

* <span data-ttu-id="b31bf-262">Para [contarlas](app-insights-metrics-explorer.md), como indicación de la frecuencia de un problema.</span><span class="sxs-lookup"><span data-stu-id="b31bf-262">To [count them](app-insights-metrics-explorer.md), as an indication of the frequency of a problem.</span></span>
* <span data-ttu-id="b31bf-263">Para [examinar los casos individuales](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-263">To [examine individual occurrences](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="b31bf-264">Los informes incluyen los seguimientos de la pila.</span><span class="sxs-lookup"><span data-stu-id="b31bf-264">The reports include the stack traces.</span></span>

<span data-ttu-id="b31bf-265">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-265">*C#*</span></span>

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

<span data-ttu-id="b31bf-266">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b31bf-266">*JavaScript*</span></span>

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

<span data-ttu-id="b31bf-267">Los SDK capturan muchas excepciones automáticamente, por lo que no siempre es necesario llamar explícitamente a TrackException.</span><span class="sxs-lookup"><span data-stu-id="b31bf-267">The SDKs catch many exceptions automatically, so you don't always have to call TrackException explicitly.</span></span>

* <span data-ttu-id="b31bf-268">ASP.NET: [escritura de código para detectar excepciones](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-268">ASP.NET: [Write code to catch exceptions](app-insights-asp-net-exceptions.md).</span></span>
* <span data-ttu-id="b31bf-269">J2EE: [las excepciones se detectan automáticamente](app-insights-java-get-started.md#exceptions-and-request-failures).</span><span class="sxs-lookup"><span data-stu-id="b31bf-269">J2EE: [Exceptions are caught automatically](app-insights-java-get-started.md#exceptions-and-request-failures).</span></span>
* <span data-ttu-id="b31bf-270">JavaScript: las excepciones se detectan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b31bf-270">JavaScript: Exceptions are caught automatically.</span></span> <span data-ttu-id="b31bf-271">Si desea deshabilitar la colección automática, agregue una línea al fragmento de código que se inserta en las páginas web:</span><span class="sxs-lookup"><span data-stu-id="b31bf-271">If you want to disable automatic collection, add a line to the code snippet that you insert in your webpages:</span></span>

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a><span data-ttu-id="b31bf-272">Excepciones en Analytics</span><span class="sxs-lookup"><span data-stu-id="b31bf-272">Exceptions in Analytics</span></span>

<span data-ttu-id="b31bf-273">En [Analytics de Application Insights](app-insights-analytics.md), las excepciones aparecen en la tabla `exceptions`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-273">In [Application Insights Analytics](app-insights-analytics.md), exceptions show up in the `exceptions` table.</span></span>

<span data-ttu-id="b31bf-274">Si el [muestreo](app-insights-sampling.md) está en uso, en la propiedad `itemCount` se muestra un valor mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="b31bf-274">If [sampling](app-insights-sampling.md) is in operation, the `itemCount` property shows a value greater than 1.</span></span> <span data-ttu-id="b31bf-275">Por ejemplo, itemCount==10 significa que de cada 10 llamadas a trackException(), el proceso de muestreo solo transmite una.</span><span class="sxs-lookup"><span data-stu-id="b31bf-275">For example itemCount==10 means that of 10 calls to trackException(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="b31bf-276">Para obtener un recuento correcto de excepciones segmentadas por tipo de excepción, use código como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="b31bf-276">To get a correct count of exceptions segmented by type of exception, use code such as:</span></span>

```
exceptions | summarize sum(itemCount) by type
```

<span data-ttu-id="b31bf-277">La mayor parte de la información importante sobre pilas ya se extrajo en variables independientes, pero puede desmontar la estructura `details` para obtener más.</span><span class="sxs-lookup"><span data-stu-id="b31bf-277">Most of the important stack information is already extracted into separate variables, but you can pull apart the `details` structure to get more.</span></span> <span data-ttu-id="b31bf-278">Puesto que se trata de una estructura dinámica, debería convertir el resultado al tipo que espere.</span><span class="sxs-lookup"><span data-stu-id="b31bf-278">Since this structure is dynamic, you should cast the result to the type you expect.</span></span> <span data-ttu-id="b31bf-279">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b31bf-279">For example:</span></span>

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

<span data-ttu-id="b31bf-280">Para asociar las excepciones a sus respectivas solicitudes, use una combinación:</span><span class="sxs-lookup"><span data-stu-id="b31bf-280">To associate exceptions with their related requests, use a join:</span></span>

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a><span data-ttu-id="b31bf-281">TrackTrace</span><span class="sxs-lookup"><span data-stu-id="b31bf-281">TrackTrace</span></span>
<span data-ttu-id="b31bf-282">Use TrackTrace para ayudar a diagnosticar problemas mediante el envío de una ''ruta de exploración'' a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b31bf-282">Use TrackTrace to help diagnose problems by sending a "breadcrumb trail" to Application Insights.</span></span> <span data-ttu-id="b31bf-283">Puede enviar fragmentos de datos de diagnóstico e inspeccionarlos en [Búsqueda de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-283">You can send chunks of diagnostic data and inspect them in [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="b31bf-284">Los [adaptadores de registro](app-insights-asp-net-trace-logs.md) usan esta API para enviar registros de terceros al portal.</span><span class="sxs-lookup"><span data-stu-id="b31bf-284">[Log adapters](app-insights-asp-net-trace-logs.md) use this API to send third-party logs to the portal.</span></span>

<span data-ttu-id="b31bf-285">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-285">*C#*</span></span>

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


<span data-ttu-id="b31bf-286">Puede buscar en el contenido del mensaje, pero (a diferencia de los valores de propiedad) no puede filtrar por él.</span><span class="sxs-lookup"><span data-stu-id="b31bf-286">You can search on message content, but (unlike property values) you can't filter on it.</span></span>

<span data-ttu-id="b31bf-287">El límite de tamaño en `message` es mucho mayor que el límite en propiedades.</span><span class="sxs-lookup"><span data-stu-id="b31bf-287">The size limit on `message` is much higher than the limit on properties.</span></span>
<span data-ttu-id="b31bf-288">Una ventaja de TrackTrace es que puede colocar datos relativamente largos en el mensaje.</span><span class="sxs-lookup"><span data-stu-id="b31bf-288">An advantage of TrackTrace is that you can put relatively long data in the message.</span></span> <span data-ttu-id="b31bf-289">Por ejemplo, aquí puede codificar datos POST.</span><span class="sxs-lookup"><span data-stu-id="b31bf-289">For example, you can encode POST data there.</span></span>  

<span data-ttu-id="b31bf-290">Además, puede agregar un nivel de gravedad al mensaje.</span><span class="sxs-lookup"><span data-stu-id="b31bf-290">In addition, you can add a severity level to your message.</span></span> <span data-ttu-id="b31bf-291">Y, al igual que con otra telemetría, puede agregar valores de propiedad para ayudar a filtrar o buscar distintos conjuntos de seguimientos.</span><span class="sxs-lookup"><span data-stu-id="b31bf-291">And, like other telemetry, you can add property values to help you filter or search for different sets of traces.</span></span> <span data-ttu-id="b31bf-292">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b31bf-292">For example:</span></span>

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

<span data-ttu-id="b31bf-293">En [Búsqueda](app-insights-diagnostic-search.md), puede filtrar fácilmente todos los mensajes de un determinado nivel de gravedad relativos a una determinada base de datos.</span><span class="sxs-lookup"><span data-stu-id="b31bf-293">In [Search](app-insights-diagnostic-search.md), you can then easily filter out all the messages of a particular severity level that relate to a particular database.</span></span>


### <a name="traces-in-analytics"></a><span data-ttu-id="b31bf-294">Seguimientos en Analytics</span><span class="sxs-lookup"><span data-stu-id="b31bf-294">Traces in Analytics</span></span>

<span data-ttu-id="b31bf-295">En [Analytics de Application Insights](app-insights-analytics.md), las llamadas a TrackTrace aparecen en la tabla `traces`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-295">In [Application Insights Analytics](app-insights-analytics.md), calls to TrackTrace show up in the `traces` table.</span></span>

<span data-ttu-id="b31bf-296">Si el [muestreo](app-insights-sampling.md) está en uso, en la propiedad itemCount se muestra un valor mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="b31bf-296">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="b31bf-297">Por ejemplo, itemCount==10 significa que de cada 10 llamadas a `trackTrace()`, el proceso de muestreo solo transmite una.</span><span class="sxs-lookup"><span data-stu-id="b31bf-297">For example itemCount==10 means that of 10 calls to `trackTrace()`, the sampling process only transmitted one of them.</span></span> <span data-ttu-id="b31bf-298">Para obtener un recuento correcto de llamadas de seguimiento, debería codificar por tanto como `traces | summarize sum(itemCount)`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-298">To get a correct count of trace calls, you should use therefore code such as `traces | summarize sum(itemCount)`.</span></span>

## <a name="trackdependency"></a><span data-ttu-id="b31bf-299">TrackDependency</span><span class="sxs-lookup"><span data-stu-id="b31bf-299">TrackDependency</span></span>
<span data-ttu-id="b31bf-300">Utilice la llamada de TrackDependency para realizar un seguimiento de los tiempos de respuesta y las tasas de éxito de las llamadas a un fragmento de código externo.</span><span class="sxs-lookup"><span data-stu-id="b31bf-300">Use the TrackDependency call to track the response times and success rates of calls to an external piece of code.</span></span> <span data-ttu-id="b31bf-301">Los resultados se muestran en los gráficos de dependencia del portal.</span><span class="sxs-lookup"><span data-stu-id="b31bf-301">The results appear in the dependency charts in the portal.</span></span>

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

<span data-ttu-id="b31bf-302">Recuerde que los SDK del servidor incluyen un [módulo de dependencia](app-insights-asp-net-dependencies.md) que detecta y realiza automáticamente el seguimiento de ciertas llamadas de dependencia; por ejemplo, a bases de datos y API de REST.</span><span class="sxs-lookup"><span data-stu-id="b31bf-302">Remember that the server SDKs include a [dependency module](app-insights-asp-net-dependencies.md) that discovers and tracks certain dependency calls automatically--for example, to databases and REST APIs.</span></span> <span data-ttu-id="b31bf-303">Debe instalar un agente en el servidor para que el módulo funcione.</span><span class="sxs-lookup"><span data-stu-id="b31bf-303">You have to install an agent on your server to make the module work.</span></span> <span data-ttu-id="b31bf-304">Utilizará esta llamada si desea hacer un seguimiento de las llamadas no captadas por el seguimiento automatizado, o bien si no desea instalar el agente.</span><span class="sxs-lookup"><span data-stu-id="b31bf-304">You use this call if you want to track calls that the automated tracking doesn't catch, or if you don't want to install the agent.</span></span>

<span data-ttu-id="b31bf-305">Para desactivar el módulo de seguimiento de dependencias estándar, edite [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) y elimine la referencia a `DependencyCollector.DependencyTrackingTelemetryModule`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-305">To turn off the standard dependency-tracking module, edit [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) and delete the reference to `DependencyCollector.DependencyTrackingTelemetryModule`.</span></span>

### <a name="dependencies-in-analytics"></a><span data-ttu-id="b31bf-306">Dependencias en Analytics</span><span class="sxs-lookup"><span data-stu-id="b31bf-306">Dependencies in Analytics</span></span>

<span data-ttu-id="b31bf-307">En [Analytics de Application Insights](app-insights-analytics.md), las llamadas de trackDependency aparecen en la tabla `dependencies`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-307">In [Application Insights Analytics](app-insights-analytics.md), trackDependency calls show up in the `dependencies` table.</span></span>

<span data-ttu-id="b31bf-308">Si el [muestreo](app-insights-sampling.md) está en uso, en la propiedad itemCount se muestra un valor mayor que 1.</span><span class="sxs-lookup"><span data-stu-id="b31bf-308">If [sampling](app-insights-sampling.md) is in operation, the itemCount property shows a value greater than 1.</span></span> <span data-ttu-id="b31bf-309">Por ejemplo, itemCount==10 significa que de cada 10 llamadas a trackDependency(), el proceso de muestreo solo transmite una.</span><span class="sxs-lookup"><span data-stu-id="b31bf-309">For example itemCount==10 means that of 10 calls to trackDependency(), the sampling process only transmitted one of them.</span></span> <span data-ttu-id="b31bf-310">Para obtener un recuento correcto de dependencias segmentadas por componente de destino, use código como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="b31bf-310">To get a correct count of dependencies segmented by target component, use code such as:</span></span>

```
dependencies | summarize sum(itemCount) by target
```

<span data-ttu-id="b31bf-311">Para asociar las dependencias a sus respectivas solicitudes, use una combinación:</span><span class="sxs-lookup"><span data-stu-id="b31bf-311">To associate dependencies with their related requests, use a join:</span></span>

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a><span data-ttu-id="b31bf-312">Datos de vaciado</span><span class="sxs-lookup"><span data-stu-id="b31bf-312">Flushing data</span></span>
<span data-ttu-id="b31bf-313">Normalmente, el SDK envía datos en momentos elegidos para minimizar el impacto en el usuario.</span><span class="sxs-lookup"><span data-stu-id="b31bf-313">Normally, the SDK sends data at times chosen to minimize the impact on the user.</span></span> <span data-ttu-id="b31bf-314">Sin embargo, en algunos casos puede que desee vaciar el búfer: por ejemplo, si usa el SDK en una aplicación que se apaga.</span><span class="sxs-lookup"><span data-stu-id="b31bf-314">However, in some cases, you might want to flush the buffer--for example, if you are using the SDK in an application that shuts down.</span></span>

<span data-ttu-id="b31bf-315">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-315">*C#*</span></span>

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

<span data-ttu-id="b31bf-316">Tenga en cuenta que la función es asincrónica para el [canal del servidor de telemetría](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span><span class="sxs-lookup"><span data-stu-id="b31bf-316">Note that the function is asynchronous for the [server telemetry channel](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).</span></span>

## <a name="authenticated-users"></a><span data-ttu-id="b31bf-317">Usuarios autenticados</span><span class="sxs-lookup"><span data-stu-id="b31bf-317">Authenticated users</span></span>
<span data-ttu-id="b31bf-318">En una aplicación web, los usuarios se identifican por cookies (de manera predeterminada).</span><span class="sxs-lookup"><span data-stu-id="b31bf-318">In a web app, users are (by default) identified by cookies.</span></span> <span data-ttu-id="b31bf-319">Se puede contar al usuario más de una vez si accede a la aplicación desde un equipo o explorador diferente, o si elimina las cookies.</span><span class="sxs-lookup"><span data-stu-id="b31bf-319">A user might be counted more than once if they access your app from a different machine or browser, or if they delete cookies.</span></span>

<span data-ttu-id="b31bf-320">Si los usuarios inician sesión en su aplicación, puede obtener un recuento más preciso estableciendo el identificador del usuario autenticado en el código del explorador:</span><span class="sxs-lookup"><span data-stu-id="b31bf-320">If users sign in to your app, you can get a more accurate count by setting the authenticated user ID in the browser code:</span></span>

<span data-ttu-id="b31bf-321">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b31bf-321">*JavaScript*</span></span>

```JS
// Called when my app has identified the user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

<span data-ttu-id="b31bf-322">En una aplicación MVC web de ASP.NET, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b31bf-322">In an ASP.NET web MVC application, for example:</span></span>

<span data-ttu-id="b31bf-323">*Razor*</span><span class="sxs-lookup"><span data-stu-id="b31bf-323">*Razor*</span></span>

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

<span data-ttu-id="b31bf-324">No es necesario usar el nombre de inicio de sesión real del usuario.</span><span class="sxs-lookup"><span data-stu-id="b31bf-324">It isn't necessary to use the user's actual sign-in name.</span></span> <span data-ttu-id="b31bf-325">Solo tiene que ser un identificador único para ese usuario.</span><span class="sxs-lookup"><span data-stu-id="b31bf-325">It only has to be an ID that is unique to that user.</span></span> <span data-ttu-id="b31bf-326">No debe incluir espacios ni ninguno de los caracteres `,;=|`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-326">It must not include spaces or any of the characters `,;=|`.</span></span>

<span data-ttu-id="b31bf-327">El identificador de usuario también se establece en una cookie de sesión y se envía al servidor.</span><span class="sxs-lookup"><span data-stu-id="b31bf-327">The user ID is also set in a session cookie and sent to the server.</span></span> <span data-ttu-id="b31bf-328">Si está instalado el SDK del servidor, el identificador de usuario autenticado se envía como parte de las propiedades de contexto tanto de la telemetría del cliente como del servidor.</span><span class="sxs-lookup"><span data-stu-id="b31bf-328">If the server SDK is installed, the authenticated user ID is sent as part of the context properties of both client and server telemetry.</span></span> <span data-ttu-id="b31bf-329">A continuación, puede filtrar y buscar en ella.</span><span class="sxs-lookup"><span data-stu-id="b31bf-329">You can then filter and search on it.</span></span>

<span data-ttu-id="b31bf-330">Si su aplicación agrupa a los usuarios en cuentas, también puede pasar un identificador de la cuenta (con las mismas restricciones de caracteres).</span><span class="sxs-lookup"><span data-stu-id="b31bf-330">If your app groups users into accounts, you can also pass an identifier for the account (with the same character restrictions).</span></span>

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

<span data-ttu-id="b31bf-331">En el [Explorador de métricas](app-insights-metrics-explorer.md), puede crear un gráfico que cuente los **Usuarios autenticados** y las **Cuentas de usuario**.</span><span class="sxs-lookup"><span data-stu-id="b31bf-331">In [Metrics Explorer](app-insights-metrics-explorer.md), you can create a chart that counts **Users, Authenticated**, and **User accounts**.</span></span>

<span data-ttu-id="b31bf-332">También puede [buscar](app-insights-diagnostic-search.md) puntos de datos de cliente con cuentas y nombres de usuario específicos.</span><span class="sxs-lookup"><span data-stu-id="b31bf-332">You can also [search](app-insights-diagnostic-search.md) for client data points with specific user names and accounts.</span></span>

## <span data-ttu-id="b31bf-333"><a name="properties"></a>Filtrado, búsqueda y segmentación de los datos mediante el uso de propiedades</span><span class="sxs-lookup"><span data-stu-id="b31bf-333"><a name="properties"></a>Filtering, searching, and segmenting your data by using properties</span></span>
<span data-ttu-id="b31bf-334">Puede asociar propiedades y medidas a los eventos (y también a las métricas, vistas de página, excepciones y otros datos de telemetría).</span><span class="sxs-lookup"><span data-stu-id="b31bf-334">You can attach properties and measurements to your events (and also to metrics, page views, exceptions, and other telemetry data).</span></span>

<span data-ttu-id="b31bf-335">*propiedades* son valores de cadena que se pueden usar para filtrar los datos de telemetría en los informes de uso.</span><span class="sxs-lookup"><span data-stu-id="b31bf-335">*Properties* are string values that you can use to filter your telemetry in the usage reports.</span></span> <span data-ttu-id="b31bf-336">Por ejemplo, si su aplicación proporciona varios juegos, puede adjuntar el nombre del juego a cada evento para así poder ver cuáles son los juegos más populares.</span><span class="sxs-lookup"><span data-stu-id="b31bf-336">For example, if your app provides several games, you can attach the name of the game to each event so that you can see which games are more popular.</span></span>

<span data-ttu-id="b31bf-337">Hay un límite de aproximadamente 8192 en la longitud de cadena.</span><span class="sxs-lookup"><span data-stu-id="b31bf-337">There's a limit of 8192 on the string length.</span></span> <span data-ttu-id="b31bf-338">(Si quiere enviar fragmentos grandes de datos, use el parámetro de mensaje de [TrackTrace](#track-trace)).</span><span class="sxs-lookup"><span data-stu-id="b31bf-338">(If you want to send large chunks of data, use the message parameter of [TrackTrace](#track-trace).)</span></span>

<span data-ttu-id="b31bf-339">*métricas* son valores numéricos que se pueden presentar de forma gráfica.</span><span class="sxs-lookup"><span data-stu-id="b31bf-339">*Metrics* are numeric values that can be presented graphically.</span></span> <span data-ttu-id="b31bf-340">Por ejemplo, puede que quiera ver si hay un aumento gradual en las puntuaciones que alcanzan sus jugadores.</span><span class="sxs-lookup"><span data-stu-id="b31bf-340">For example, you might want to see if there's a gradual increase in the scores that your gamers achieve.</span></span> <span data-ttu-id="b31bf-341">Los gráficos se pueden segmentar por las propiedades enviadas con el evento, así que puede separar o apilar los gráficos para diferentes juegos.</span><span class="sxs-lookup"><span data-stu-id="b31bf-341">The graphs can be segmented by the properties that are sent with the event, so that you can get separate or stacked graphs for different games.</span></span>

<span data-ttu-id="b31bf-342">Para que valores de métricas se muestren correctamente, deben ser mayores o iguales que 0.</span><span class="sxs-lookup"><span data-stu-id="b31bf-342">For metric values to be correctly displayed, they should be greater than or equal to 0.</span></span>

<span data-ttu-id="b31bf-343">Hay algunos [límites en el número de propiedades, valores de propiedad y métricas](#limits) que puede usar.</span><span class="sxs-lookup"><span data-stu-id="b31bf-343">There are some [limits on the number of properties, property values, and metrics](#limits) that you can use.</span></span>

<span data-ttu-id="b31bf-344">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b31bf-344">*JavaScript*</span></span>

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


<span data-ttu-id="b31bf-345">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-345">*C#*</span></span>

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics);


<span data-ttu-id="b31bf-346">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b31bf-346">*Visual Basic*</span></span>

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send the event:
    telemetry.TrackEvent("WinGame", properties, metrics)


<span data-ttu-id="b31bf-347">*Java*</span><span class="sxs-lookup"><span data-stu-id="b31bf-347">*Java*</span></span>

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> <span data-ttu-id="b31bf-348">Tenga cuidado de no registrar información de identificación personal en las propiedades.</span><span class="sxs-lookup"><span data-stu-id="b31bf-348">Take care not to log personally identifiable information in properties.</span></span>
>
>

<span data-ttu-id="b31bf-349">*Si utilizó métricas*, abra el Explorador de métricas y seleccione la métrica del grupo **Personalizada**:</span><span class="sxs-lookup"><span data-stu-id="b31bf-349">*If you used metrics*, open Metrics Explorer and select the metric from the **Custom** group:</span></span>

![Abra el Explorador de métricas, seleccione el gráfico y seleccione la métrica.](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> <span data-ttu-id="b31bf-351">Si no aparece la métrica o el encabezado **Personalizada** no se encuentra allí, cierre la hoja de selección e inténtelo de nuevo más tarde.</span><span class="sxs-lookup"><span data-stu-id="b31bf-351">If your metric doesn't appear, or if the **Custom** heading isn't there, close the selection blade and try again later.</span></span> <span data-ttu-id="b31bf-352">A veces las métricas pueden tardar una hora en agregarse a través de la canalización.</span><span class="sxs-lookup"><span data-stu-id="b31bf-352">Metrics can sometimes take an hour to be aggregated through the pipeline.</span></span>

<span data-ttu-id="b31bf-353">*Si usó propiedades y métricas*, segmente la métrica por la propiedad:</span><span class="sxs-lookup"><span data-stu-id="b31bf-353">*If you used properties and metrics*, segment the metric by the property:</span></span>

![Establezca la opción de agrupación y seleccione la propiedad en Agrupar por.](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

<span data-ttu-id="b31bf-355">*En Búsqueda de diagnóstico*, puede ver las propiedades y las métricas de repeticiones individuales de un evento.</span><span class="sxs-lookup"><span data-stu-id="b31bf-355">*In Diagnostic Search*, you can view the properties and metrics of individual occurrences of an event.</span></span>

![Seleccione una instancia y luego seleccione "...".](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

<span data-ttu-id="b31bf-357">Utilice el campo de **Búsqueda** para ver las apariciones del evento con un valor de propiedad concreto.</span><span class="sxs-lookup"><span data-stu-id="b31bf-357">Use the **Search** field to see event occurrences that have a particular property value.</span></span>

![Escriba un término en Buscar.](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

<span data-ttu-id="b31bf-359">[Más información sobre las expresiones de búsqueda](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-359">[Learn more about search expressions](app-insights-diagnostic-search.md).</span></span>

### <a name="alternative-way-to-set-properties-and-metrics"></a><span data-ttu-id="b31bf-360">Método alternativo para establecer propiedades y métricas</span><span class="sxs-lookup"><span data-stu-id="b31bf-360">Alternative way to set properties and metrics</span></span>
<span data-ttu-id="b31bf-361">Si le resulta más cómodo, puede recopilar los parámetros de un evento en un objeto independiente:</span><span class="sxs-lookup"><span data-stu-id="b31bf-361">If it's more convenient, you can collect the parameters of an event in a separate object:</span></span>

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> <span data-ttu-id="b31bf-362">No vuelva a usar la misma instancia de elemento de telemetría (`event` en este ejemplo) para llamar a Track*() varias veces.</span><span class="sxs-lookup"><span data-stu-id="b31bf-362">Don't reuse the same telemetry item instance (`event` in this example) to call Track*() multiple times.</span></span> <span data-ttu-id="b31bf-363">Esto puede hacer que se envíe la telemetría con una configuración incorrecta.</span><span class="sxs-lookup"><span data-stu-id="b31bf-363">This may cause telemetry to be sent with incorrect configuration.</span></span>
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a><span data-ttu-id="b31bf-364">Mediciones y propiedades personalizadas en Analytics</span><span class="sxs-lookup"><span data-stu-id="b31bf-364">Custom measurements and properties in Analytics</span></span>

<span data-ttu-id="b31bf-365">En [Analytics](app-insights-analytics.md), las métricas y propiedades personalizadas aparecen en los atributos `customMeasurements` y `customDimensions` de cada registro de telemetría.</span><span class="sxs-lookup"><span data-stu-id="b31bf-365">In [Analytics](app-insights-analytics.md), custom metrics and properties show in the `customMeasurements` and `customDimensions` attributes of each telemetry record.</span></span>

<span data-ttu-id="b31bf-366">Por ejemplo, si agregó una propiedad llamada "game" a la telemetría de solicitudes, esta consulta cuenta el número de apariciones de diferentes valores de "game" y muestra la media de la métrica personalizada "score":</span><span class="sxs-lookup"><span data-stu-id="b31bf-366">For example, if you have added a property named "game" to your request telemetry, this query counts the occurrences of different values of "game", and show the average of the custom metric "score":</span></span>

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

<span data-ttu-id="b31bf-367">Tenga en lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b31bf-367">Notice that:</span></span>

* <span data-ttu-id="b31bf-368">Al extraer un valor de los elementos de JSON customDimensions o customMeasurements, es de tipo dinámico, por lo que debe convertirlo a `tostring` o `todouble`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-368">When you extract a value from the customDimensions or customMeasurements JSON, it has dynamic type, and so you must cast it `tostring` or `todouble`.</span></span>
* <span data-ttu-id="b31bf-369">Para tener en cuenta la posibilidad de [muestreo](app-insights-sampling.md), debería usar `sum(itemCount)`, no `count()`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-369">To take account of the possibility of [sampling](app-insights-sampling.md), you should use `sum(itemCount)`, not `count()`.</span></span>



## <span data-ttu-id="b31bf-370"><a name="timed"></a> Eventos de temporización</span><span class="sxs-lookup"><span data-stu-id="b31bf-370"><a name="timed"></a> Timing events</span></span>
<span data-ttu-id="b31bf-371">Seguro que en ocasiones le gustaría representar el tiempo que se tarda en realizar alguna acción.</span><span class="sxs-lookup"><span data-stu-id="b31bf-371">Sometimes you want to chart how long it takes to perform an action.</span></span> <span data-ttu-id="b31bf-372">Por ejemplo, puede que quiera saber cuánto tiempo tardan los usuarios en considerar las opciones de un juego.</span><span class="sxs-lookup"><span data-stu-id="b31bf-372">For example, you might want to know how long users take to consider choices in a game.</span></span> <span data-ttu-id="b31bf-373">Puede usar el parámetro de medida para ello.</span><span class="sxs-lookup"><span data-stu-id="b31bf-373">You can use the measurement parameter for this.</span></span>

<span data-ttu-id="b31bf-374">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-374">*C#*</span></span>

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform the timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send the event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <span data-ttu-id="b31bf-375"><a name="defaults"></a>Propiedades predeterminadas para la telemetría personalizada</span><span class="sxs-lookup"><span data-stu-id="b31bf-375"><a name="defaults"></a>Default properties for custom telemetry</span></span>
<span data-ttu-id="b31bf-376">Si quiere establecer valores de propiedad predeterminados para algunos de los eventos personalizados que escriba, puede hacerlo en una instancia de TelemetryClient.</span><span class="sxs-lookup"><span data-stu-id="b31bf-376">If you want to set default property values for some of the custom events that you write, you can set them in a TelemetryClient instance.</span></span> <span data-ttu-id="b31bf-377">Se adjuntarán a cada elemento de telemetría enviado desde ese cliente.</span><span class="sxs-lookup"><span data-stu-id="b31bf-377">They are attached to every telemetry item that's sent from that client.</span></span>

<span data-ttu-id="b31bf-378">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-378">*C#*</span></span>

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame");

<span data-ttu-id="b31bf-379">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b31bf-379">*Visual Basic*</span></span>

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with the context property:
    gameTelemetry.TrackEvent("WinGame")

<span data-ttu-id="b31bf-380">*Java*</span><span class="sxs-lookup"><span data-stu-id="b31bf-380">*Java*</span></span>

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



<span data-ttu-id="b31bf-381">Las llamadas de telemetría individuales pueden invalidar los valores predeterminados en los diccionarios de propiedad.</span><span class="sxs-lookup"><span data-stu-id="b31bf-381">Individual telemetry calls can override the default values in their property dictionaries.</span></span>

<span data-ttu-id="b31bf-382">*Para los clientes web de JavaScript*, [use los inicializadores de telemetría de JavaScript](#js-initializer).</span><span class="sxs-lookup"><span data-stu-id="b31bf-382">*For JavaScript web clients*, [use JavaScript telemetry initializers](#js-initializer).</span></span>

<span data-ttu-id="b31bf-383">*Para agregar propiedades a toda la telemetría*, incluidos los datos de los módulos de recopilación estándar, [implemente `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span><span class="sxs-lookup"><span data-stu-id="b31bf-383">*To add properties to all telemetry*, including the data from standard collection modules, [implement `ITelemetryInitializer`](app-insights-api-filtering-sampling.md#add-properties).</span></span>

## <a name="sampling-filtering-and-processing-telemetry"></a><span data-ttu-id="b31bf-384">Muestreo, filtrado y procesamiento de telemetría</span><span class="sxs-lookup"><span data-stu-id="b31bf-384">Sampling, filtering, and processing telemetry</span></span>
<span data-ttu-id="b31bf-385">Puede escribir código para procesar la telemetría antes de que se envíe desde el SDK.</span><span class="sxs-lookup"><span data-stu-id="b31bf-385">You can write code to process your telemetry before it's sent from the SDK.</span></span> <span data-ttu-id="b31bf-386">El procesamiento incluye los datos enviados desde los módulos de telemetría estándar, como la recopilación de solicitudes HTTP y de dependencias.</span><span class="sxs-lookup"><span data-stu-id="b31bf-386">The processing includes data that's sent from the standard telemetry modules, such as HTTP request collection and dependency collection.</span></span>

<span data-ttu-id="b31bf-387">[Agregue propiedades](app-insights-api-filtering-sampling.md#add-properties) a la telemetría mediante la implementación de `ITelemetryInitializer`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-387">[Add properties](app-insights-api-filtering-sampling.md#add-properties) to telemetry by implementing `ITelemetryInitializer`.</span></span> <span data-ttu-id="b31bf-388">Por ejemplo, puede agregar números de versión o valores calculados a partir de otras propiedades.</span><span class="sxs-lookup"><span data-stu-id="b31bf-388">For example, you can add version numbers or values that are calculated from other properties.</span></span>

<span data-ttu-id="b31bf-389">El [filtrado](app-insights-api-filtering-sampling.md#filtering) puede modificar o descartar la telemetría antes de que se envíe desde el SDK, mediante la implementación de `ITelemetryProcesor`.</span><span class="sxs-lookup"><span data-stu-id="b31bf-389">[Filtering](app-insights-api-filtering-sampling.md#filtering) can modify or discard telemetry before it's sent from the SDK by implementing `ITelemetryProcesor`.</span></span> <span data-ttu-id="b31bf-390">Puede controlar qué se envía y qué se descarta, pero debe tener en cuenta el efecto en las métricas.</span><span class="sxs-lookup"><span data-stu-id="b31bf-390">You control what is sent or discarded, but you have to account for the effect on your metrics.</span></span> <span data-ttu-id="b31bf-391">Según la forma en que se descarten los elementos, podría perder la capacidad de navegar entre elementos relacionados.</span><span class="sxs-lookup"><span data-stu-id="b31bf-391">Depending on how you discard items, you might lose the ability to navigate between related items.</span></span>

<span data-ttu-id="b31bf-392">El [muestreo](app-insights-api-filtering-sampling.md) es una solución empaquetada para reducir el volumen de datos enviado desde la aplicación al portal.</span><span class="sxs-lookup"><span data-stu-id="b31bf-392">[Sampling](app-insights-api-filtering-sampling.md) is a packaged solution to reduce the volume of data that's sent from your app to the portal.</span></span> <span data-ttu-id="b31bf-393">Lo hace sin que las métricas mostradas resulten afectadas.</span><span class="sxs-lookup"><span data-stu-id="b31bf-393">It does so without affecting the displayed metrics.</span></span> <span data-ttu-id="b31bf-394">Y sin repercutir tampoco sobre capacidad para diagnosticar problemas navegando entre elementos relacionados, como excepciones, solicitudes y vistas de página.</span><span class="sxs-lookup"><span data-stu-id="b31bf-394">And it does so without affecting your ability to diagnose problems by navigating between related items such as exceptions, requests, and page views.</span></span>

<span data-ttu-id="b31bf-395">[Más información](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-395">[Learn more](app-insights-api-filtering-sampling.md).</span></span>

## <a name="disabling-telemetry"></a><span data-ttu-id="b31bf-396">Deshabilitación de la telemetría</span><span class="sxs-lookup"><span data-stu-id="b31bf-396">Disabling telemetry</span></span>
<span data-ttu-id="b31bf-397">Para *iniciar y detener dinámicamente* la recopilación y la transmisión de telemetría:</span><span class="sxs-lookup"><span data-stu-id="b31bf-397">To *dynamically stop and start* the collection and transmission of telemetry:</span></span>

<span data-ttu-id="b31bf-398">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-398">*C#*</span></span>

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

<span data-ttu-id="b31bf-399">Para *deshabilitar los recopiladores estándar seleccionados* (por ejemplo, contadores de rendimiento, solicitudes HTTP o dependencias), elimine o convierta en comentarios las líneas correspondientes en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Puede hacer esto, por ejemplo, si quiere enviar sus propios datos de TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="b31bf-399">To *disable selected standard collectors*--for example, performance counters, HTTP requests, or dependencies--delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). You can do this, for example, if you want to send your own TrackRequest data.</span></span>

## <span data-ttu-id="b31bf-400"><a name="debug"></a>Modo de programador</span><span class="sxs-lookup"><span data-stu-id="b31bf-400"><a name="debug"></a>Developer mode</span></span>
<span data-ttu-id="b31bf-401">Durante la depuración, resulta útil enviar los datos de telemetría por la canalización para así poder ver los resultados inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="b31bf-401">During debugging, it's useful to have your telemetry expedited through the pipeline so that you can see results immediately.</span></span> <span data-ttu-id="b31bf-402">También puede recibir mensajes adicionales que le ayuden a realizar el seguimiento de los posibles problemas con la telemetría.</span><span class="sxs-lookup"><span data-stu-id="b31bf-402">You also get additional messages that help you trace any problems with the telemetry.</span></span> <span data-ttu-id="b31bf-403">Desactívelo en producción, ya que puede ralentizar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b31bf-403">Switch it off in production, because it may slow down your app.</span></span>

<span data-ttu-id="b31bf-404">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-404">*C#*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

<span data-ttu-id="b31bf-405">*Visual Basic*</span><span class="sxs-lookup"><span data-stu-id="b31bf-405">*Visual Basic*</span></span>

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <span data-ttu-id="b31bf-406"><a name="ikey"></a> Establecimiento de la clave de instrumentación para datos de telemetría personalizados seleccionados</span><span class="sxs-lookup"><span data-stu-id="b31bf-406"><a name="ikey"></a> Setting the instrumentation key for selected custom telemetry</span></span>
<span data-ttu-id="b31bf-407">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-407">*C#*</span></span>

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <span data-ttu-id="b31bf-408"><a name="dynamic-ikey"></a> Copia de la clave de instrumentación</span><span class="sxs-lookup"><span data-stu-id="b31bf-408"><a name="dynamic-ikey"></a> Dynamic instrumentation key</span></span>
<span data-ttu-id="b31bf-409">Para evitar la mezcla de telemetría de entornos de desarrollo, pruebas y producción, puede [crear recursos separados de Application Insights](app-insights-create-new-resource.md) y cambiar sus claves en función del entorno.</span><span class="sxs-lookup"><span data-stu-id="b31bf-409">To avoid mixing up telemetry from development, test, and production environments, you can [create separate Application Insights resources](app-insights-create-new-resource.md) and change their keys, depending on the environment.</span></span>

<span data-ttu-id="b31bf-410">En lugar de obtener la clave de instrumentación del archivo de configuración, puede establecerla en el código.</span><span class="sxs-lookup"><span data-stu-id="b31bf-410">Instead of getting the instrumentation key from the configuration file, you can set it in your code.</span></span> <span data-ttu-id="b31bf-411">Establezca la clave en un método de inicialización, como global.aspx.cs en un servicio de ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="b31bf-411">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="b31bf-412">*C#*</span><span class="sxs-lookup"><span data-stu-id="b31bf-412">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

<span data-ttu-id="b31bf-413">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="b31bf-413">*JavaScript*</span></span>

    appInsights.config.instrumentationKey = myKey;



<span data-ttu-id="b31bf-414">En una página web, podría configurarla a partir del estado del servidor web, en lugar de codificarla literalmente en el script.</span><span class="sxs-lookup"><span data-stu-id="b31bf-414">In webpages, you might want to set it from the web server's state, rather than coding it literally into the script.</span></span> <span data-ttu-id="b31bf-415">Por ejemplo, en una página web generada en una aplicación ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="b31bf-415">For example, in a webpage generated in an ASP.NET app:</span></span>

<span data-ttu-id="b31bf-416">*JavaScript en Razor*</span><span class="sxs-lookup"><span data-stu-id="b31bf-416">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a><span data-ttu-id="b31bf-417">TelemetryContext</span><span class="sxs-lookup"><span data-stu-id="b31bf-417">TelemetryContext</span></span>
<span data-ttu-id="b31bf-418">TelemetryClient tiene una propiedad de Context, que contiene valores que se envían junto con todos los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="b31bf-418">TelemetryClient has a Context property, which contains values that are sent along with all telemetry data.</span></span> <span data-ttu-id="b31bf-419">Normalmente, se establecen mediante los módulos de telemetría estándar, pero también los puede establecer usted mismo.</span><span class="sxs-lookup"><span data-stu-id="b31bf-419">They are normally set by the standard telemetry modules, but you can also set them yourself.</span></span> <span data-ttu-id="b31bf-420">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b31bf-420">For example:</span></span>

    telemetry.Context.Operation.Name = "MyOperationName";

<span data-ttu-id="b31bf-421">Si establece cualquiera de estos valores manualmente, considere la posibilidad de quitar la línea pertinente de [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), de modo que no se confundan sus valores con los valores estándar.</span><span class="sxs-lookup"><span data-stu-id="b31bf-421">If you set any of these values yourself, consider removing the relevant line from [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), so that your values and the standard values don't get confused.</span></span>

* <span data-ttu-id="b31bf-422">**Component**: la aplicación y su versión</span><span class="sxs-lookup"><span data-stu-id="b31bf-422">**Component**: The app and its version.</span></span>
* <span data-ttu-id="b31bf-423">**Device**: datos sobre el dispositivo donde se ejecuta la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b31bf-423">**Device**: Data about the device where the app is running.</span></span> <span data-ttu-id="b31bf-424">(En aplicaciones web, se trata del servidor o el dispositivo de cliente desde el que se envía la telemetría).</span><span class="sxs-lookup"><span data-stu-id="b31bf-424">(In web apps, this is the server or client device that the telemetry is sent from.)</span></span>
* <span data-ttu-id="b31bf-425">**InstrumentationKey**: el recurso de Application Insights en Azure donde aparece la telemetría.</span><span class="sxs-lookup"><span data-stu-id="b31bf-425">**InstrumentationKey**: The Application Insights resource in Azure where the telemetry appear.</span></span> <span data-ttu-id="b31bf-426">Normalmente, se selecciona de ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="b31bf-426">It's usually picked up from ApplicationInsights.config.</span></span>
* <span data-ttu-id="b31bf-427">**Location**: la ubicación geográfica del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b31bf-427">**Location**: The geographic location of the device.</span></span>
* <span data-ttu-id="b31bf-428">**Operation**: en aplicaciones web, es la solicitud HTTP actual.</span><span class="sxs-lookup"><span data-stu-id="b31bf-428">**Operation**: In web apps, the current HTTP request.</span></span> <span data-ttu-id="b31bf-429">En otros tipos de aplicaciones, puede establecer este valor para agrupar los eventos juntos.</span><span class="sxs-lookup"><span data-stu-id="b31bf-429">In other app types, you can set this to group events together.</span></span>
  * <span data-ttu-id="b31bf-430">**Id**: valor generado que correlaciona distintos eventos, de modo que cuando usted inspeccione cualquier evento en Búsqueda de diagnóstico, puede encontrar elementos relacionados.</span><span class="sxs-lookup"><span data-stu-id="b31bf-430">**Id**: A generated value that correlates different events, so that when you inspect any event in Diagnostic Search, you can find related items.</span></span>
  * <span data-ttu-id="b31bf-431">**Name**: un identificador, generalmente la dirección URL de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="b31bf-431">**Name**: An identifier, usually the URL of the HTTP request.</span></span>
  * <span data-ttu-id="b31bf-432">**SyntheticSource**: si no es un valor nulo ni está vacío, esta cadena indica que el origen de la solicitud se ha identificado como un robot o una prueba web.</span><span class="sxs-lookup"><span data-stu-id="b31bf-432">**SyntheticSource**: If not null or empty, a string that indicates that the source of the request has been identified as a robot or web test.</span></span> <span data-ttu-id="b31bf-433">De forma predeterminada, se excluye de cálculos en el Explorador de métricas.</span><span class="sxs-lookup"><span data-stu-id="b31bf-433">By default, it is excluded from calculations in Metrics Explorer.</span></span>
* <span data-ttu-id="b31bf-434">**Properties**: propiedades que se envían con todos los datos de telemetría.</span><span class="sxs-lookup"><span data-stu-id="b31bf-434">**Properties**: Properties that are sent with all telemetry data.</span></span> <span data-ttu-id="b31bf-435">Se pueden invalidar en llamadas de seguimiento* individuales.</span><span class="sxs-lookup"><span data-stu-id="b31bf-435">It can be overridden in individual Track* calls.</span></span>
* <span data-ttu-id="b31bf-436">**Session**: la sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="b31bf-436">**Session**: The user's session.</span></span> <span data-ttu-id="b31bf-437">El identificador se establece en un valor generado, que cambia cuando el usuario lleva un tiempo sin estar activo.</span><span class="sxs-lookup"><span data-stu-id="b31bf-437">The ID is set to a generated value, which is changed when the user has not been active for a while.</span></span>
* <span data-ttu-id="b31bf-438">**User**: información del usuario.</span><span class="sxs-lookup"><span data-stu-id="b31bf-438">**User**: User information.</span></span>

## <a name="limits"></a><span data-ttu-id="b31bf-439">límites</span><span class="sxs-lookup"><span data-stu-id="b31bf-439">Limits</span></span>
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

<span data-ttu-id="b31bf-440">Para evitar llegar al límite de velocidad de datos, utilice el [muestreo](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-440">To avoid hitting the data rate limit, use [sampling](app-insights-sampling.md).</span></span>

<span data-ttu-id="b31bf-441">Para determinar cuánto tiempo se conservan los datos, consulte el artículo sobre [retención de datos y privacidad](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-441">To determine how long data is kept, see [Data retention and privacy](app-insights-data-retention-privacy.md).</span></span>

## <a name="reference-docs"></a><span data-ttu-id="b31bf-442">Documentos de referencia</span><span class="sxs-lookup"><span data-stu-id="b31bf-442">Reference docs</span></span>
* [<span data-ttu-id="b31bf-443">Referencia de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b31bf-443">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)
* [<span data-ttu-id="b31bf-444">Referencia de Java</span><span class="sxs-lookup"><span data-stu-id="b31bf-444">Java reference</span></span>](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [<span data-ttu-id="b31bf-445">Referencia de JavaScript</span><span class="sxs-lookup"><span data-stu-id="b31bf-445">JavaScript reference</span></span>](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [<span data-ttu-id="b31bf-446">SDK de Android</span><span class="sxs-lookup"><span data-stu-id="b31bf-446">Android SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Android)
* [<span data-ttu-id="b31bf-447">SDK de iOS</span><span class="sxs-lookup"><span data-stu-id="b31bf-447">iOS SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a><span data-ttu-id="b31bf-448">Código del SDK</span><span class="sxs-lookup"><span data-stu-id="b31bf-448">SDK code</span></span>
* [<span data-ttu-id="b31bf-449">SDK básico de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b31bf-449">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="b31bf-450">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="b31bf-450">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="b31bf-451">Paquetes de Windows Server</span><span class="sxs-lookup"><span data-stu-id="b31bf-451">Windows Server packages</span></span>](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [<span data-ttu-id="b31bf-452">SDK de Java</span><span class="sxs-lookup"><span data-stu-id="b31bf-452">Java SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-Java)
* [<span data-ttu-id="b31bf-453">SDK de JavaScript</span><span class="sxs-lookup"><span data-stu-id="b31bf-453">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)
* [<span data-ttu-id="b31bf-454">Todas las plataformas</span><span class="sxs-lookup"><span data-stu-id="b31bf-454">All platforms</span></span>](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a><span data-ttu-id="b31bf-455">Preguntas</span><span class="sxs-lookup"><span data-stu-id="b31bf-455">Questions</span></span>
* <span data-ttu-id="b31bf-456">*¿Qué excepciones pueden iniciar las llamadas de seguimiento_()?*</span><span class="sxs-lookup"><span data-stu-id="b31bf-456">*What exceptions might Track_() calls throw?*</span></span>

    <span data-ttu-id="b31bf-457">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="b31bf-457">None.</span></span> <span data-ttu-id="b31bf-458">No es necesario agruparlas en cláusulas try-catch.</span><span class="sxs-lookup"><span data-stu-id="b31bf-458">You don't need to wrap them in try-catch clauses.</span></span> <span data-ttu-id="b31bf-459">Si el SDK encuentra problemas, registrará los mensajes en la salida de la consola de depuración, y, si los mensajes pasan, en la Búsqueda de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="b31bf-459">If the SDK encounters problems, it will log messages in the debug console output and--if the messages get through--in Diagnostic Search.</span></span>
* <span data-ttu-id="b31bf-460">*¿Hay una API de REST para obtener datos desde el portal?*</span><span class="sxs-lookup"><span data-stu-id="b31bf-460">*Is there a REST API to get data from the portal?*</span></span>

    <span data-ttu-id="b31bf-461">Sí, la [API de acceso a datos](https://dev.applicationinsights.io/).</span><span class="sxs-lookup"><span data-stu-id="b31bf-461">Yes, the [data access API](https://dev.applicationinsights.io/).</span></span> <span data-ttu-id="b31bf-462">Otras maneras de extraer datos son [exportar desde Analytics a Power BI](app-insights-export-power-bi.md) y la [exportación continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="b31bf-462">Other ways to extract data include [export from Analytics to Power BI](app-insights-export-power-bi.md) and [continuous export](app-insights-export-telemetry.md).</span></span>

## <span data-ttu-id="b31bf-463"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b31bf-463"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="b31bf-464">Búsqueda de eventos y registros</span><span class="sxs-lookup"><span data-stu-id="b31bf-464">Search events and logs</span></span>](app-insights-diagnostic-search.md)

* [<span data-ttu-id="b31bf-465">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="b31bf-465">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)


