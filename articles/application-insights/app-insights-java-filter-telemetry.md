---
title: "Filtrado de la telemetría de Azure Application Insights en la aplicación web de Java | Microsoft Docs"
description: "Reduzca el tráfico de telemetría mediante el filtrado de los eventos que no necesita supervisar."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 5f6d6d4ad590b85810c42e9f9520850024c5446a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="bfe49-103">Filtrado de telemetría en la aplicación web de Java</span><span class="sxs-lookup"><span data-stu-id="bfe49-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="bfe49-104">Los filtros proporcionan una manera de seleccionar la telemetría que su [aplicación web de Java envía a Application Insights](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bfe49-104">Filters provide a way to select the telemetry that your [Java web app sends to Application Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="bfe49-105">Hay algunos filtros de serie que puede utilizar y también puede escribir sus propios filtros personalizados.</span><span class="sxs-lookup"><span data-stu-id="bfe49-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="bfe49-106">Los filtros de serie incluyen:</span><span class="sxs-lookup"><span data-stu-id="bfe49-106">The out-of-the-box filters include:</span></span>

* <span data-ttu-id="bfe49-107">El nivel de gravedad del seguimiento</span><span class="sxs-lookup"><span data-stu-id="bfe49-107">Trace severity level</span></span>
* <span data-ttu-id="bfe49-108">Direcciones URL específicas, palabras clave o códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="bfe49-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="bfe49-109">Respuestas rápidas, es decir, las solicitudes a las que la aplicación responde rápidamente</span><span class="sxs-lookup"><span data-stu-id="bfe49-109">Fast responses - that is, requests to which your app responded to quickly</span></span>
* <span data-ttu-id="bfe49-110">Nombres de eventos específicos</span><span class="sxs-lookup"><span data-stu-id="bfe49-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="bfe49-111">Los filtros sesgan las métricas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bfe49-111">Filters skew the metrics of your app.</span></span> <span data-ttu-id="bfe49-112">Por ejemplo, puede decidir que, para diagnosticar respuestas lentas, hay que establecer un filtro para descartar los tiempos de respuesta rápidos.</span><span class="sxs-lookup"><span data-stu-id="bfe49-112">For example, you might decide that, in order to diagnose slow responses, you will set a filter to discard fast response times.</span></span> <span data-ttu-id="bfe49-113">Pero debe tener en cuenta que los tiempos de respuesta promedio notificados por Application Insights serán más lentos que la velocidad real y que el recuento de las solicitudes será menor que el recuento real.</span><span class="sxs-lookup"><span data-stu-id="bfe49-113">But you must be aware that the average response times reported by Application Insights will then be slower than the true speed, and the count of requests will be smaller than the real count.</span></span>
> <span data-ttu-id="bfe49-114">Si puede resultar un problema, use el [muestreo](app-insights-sampling.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="bfe49-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="bfe49-115">Establecimiento de filtros</span><span class="sxs-lookup"><span data-stu-id="bfe49-115">Setting filters</span></span>

<span data-ttu-id="bfe49-116">En ApplicationInsights.xml, agregue una sección `TelemetryProcessors` como la de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bfe49-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


```XML

    <ApplicationInsights>
      <TelemetryProcessors>

        <BuiltInProcessors>
           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="100"/>
                  <Add name="NotNeededResponseCodes" value="200-400"/>
           </Processor>

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="100"/>
                  <Add name="NotNeededNames" value="home,index"/>
                  <Add name="NotNeededUrls" value=".jpg,.css"/>
           </Processor>

           <Processor type="TelemetryEventFilter">
                  <!-- Names of events we don't want to see -->
                  <Add name="NotNeededNames" value="Start,Stop,Pause"/>
           </Processor>

           <!-- Exclude telemetry from availability tests and bots -->
           <Processor type="SyntheticSourceFilter">
                <!-- Optional: specify which synthetic sources,
                     comma-separated
                     - default is all synthetics -->
                <Add name="NotNeededSources" value="Application Insights Availability Monitoring,BingPreview"
           </Processor>

        </BuiltInProcessors>

        <CustomProcessors>
          <Processor type="com.fabrikam.MyFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>

      </TelemetryProcessors>
    </ApplicationInsights>

```




<span data-ttu-id="bfe49-117">[Inspeccione el conjunto completo de procesadores integrados](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="bfe49-117">[Inspect the full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="bfe49-118">Filtros integrados</span><span class="sxs-lookup"><span data-stu-id="bfe49-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="bfe49-119">Filtro de telemetría de métricas</span><span class="sxs-lookup"><span data-stu-id="bfe49-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="bfe49-120">`NotNeeded`: lista de nombres de métricas personalizados separada por comas.</span><span class="sxs-lookup"><span data-stu-id="bfe49-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="bfe49-121">Filtro de telemetría de vista de página</span><span class="sxs-lookup"><span data-stu-id="bfe49-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="bfe49-122">`DurationThresholdInMS`: la duración se refiere al tiempo dedicado a cargar la página.</span><span class="sxs-lookup"><span data-stu-id="bfe49-122">`DurationThresholdInMS` - Duration refers to the time taken to load the page.</span></span> <span data-ttu-id="bfe49-123">Si está establecido el tiempo, no se notifican las páginas que se cargan más rápido que en este momento.</span><span class="sxs-lookup"><span data-stu-id="bfe49-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="bfe49-124">`NotNeededNames`: lista de nombres de página separados por comas.</span><span class="sxs-lookup"><span data-stu-id="bfe49-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="bfe49-125">`NotNeededUrls`: lista de fragmentos de URL separados por comas.</span><span class="sxs-lookup"><span data-stu-id="bfe49-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="bfe49-126">Por ejemplo, `"home"` filtra todas las páginas que tienen "inicio" en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="bfe49-126">For example, `"home"` filters out all pages that have "home" in the URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="bfe49-127">Filtro de telemetría de solicitudes</span><span class="sxs-lookup"><span data-stu-id="bfe49-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="bfe49-128">Filtro de origen sintético</span><span class="sxs-lookup"><span data-stu-id="bfe49-128">Synthetic Source filter</span></span>

<span data-ttu-id="bfe49-129">Filtra toda la telemetría con valores en la propiedad SyntheticSource.</span><span class="sxs-lookup"><span data-stu-id="bfe49-129">Filters out all telemetry that have values in the SyntheticSource property.</span></span> <span data-ttu-id="bfe49-130">Incluye solicitudes de bots, spiders y pruebas de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="bfe49-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="bfe49-131">Filtre la telemetría para todas las solicitudes sintéticas:</span><span class="sxs-lookup"><span data-stu-id="bfe49-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="bfe49-132">Filtre la telemetría para orígenes sintéticos específicos:</span><span class="sxs-lookup"><span data-stu-id="bfe49-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="bfe49-133">`NotNeeded`: Lista de nombres de origen sintético separados por comas.</span><span class="sxs-lookup"><span data-stu-id="bfe49-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="bfe49-134">Filtro de eventos de telemetría</span><span class="sxs-lookup"><span data-stu-id="bfe49-134">Telemetry Event filter</span></span>

<span data-ttu-id="bfe49-135">Filtra los eventos personalizados (registrados mediante [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="bfe49-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="bfe49-136">`NotNeededNames`: lista de nombres de eventos separados por comas.</span><span class="sxs-lookup"><span data-stu-id="bfe49-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="bfe49-137">Filtro de telemetría de seguimiento</span><span class="sxs-lookup"><span data-stu-id="bfe49-137">Trace Telemetry filter</span></span>

<span data-ttu-id="bfe49-138">Filtra los seguimientos de registros (registrados mediante [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) o un [recopilador de plataforma de registro](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="bfe49-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="bfe49-139">Los valores válidos de `FromSeverityLevel` son:</span><span class="sxs-lookup"><span data-stu-id="bfe49-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="bfe49-140">OFF             - Filtra TODOS los seguimientos</span><span class="sxs-lookup"><span data-stu-id="bfe49-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="bfe49-141">TRACE           - Sin filtrado.</span><span class="sxs-lookup"><span data-stu-id="bfe49-141">TRACE           - No filtering.</span></span> <span data-ttu-id="bfe49-142">es igual al nivel de seguimiento</span><span class="sxs-lookup"><span data-stu-id="bfe49-142">equals to Trace level</span></span>
 *  <span data-ttu-id="bfe49-143">INFO            - Filtra el nivel TRACE</span><span class="sxs-lookup"><span data-stu-id="bfe49-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="bfe49-144">WARN            - Filtra el nivel TRACE e INFO</span><span class="sxs-lookup"><span data-stu-id="bfe49-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="bfe49-145">ERROR           - Filtra WARN, INFO, TRACE</span><span class="sxs-lookup"><span data-stu-id="bfe49-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="bfe49-146">CRITICAL        - Filtra todo menos CRITICAL</span><span class="sxs-lookup"><span data-stu-id="bfe49-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="bfe49-147">Filtros personalizados</span><span class="sxs-lookup"><span data-stu-id="bfe49-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="bfe49-148">1. Codificación del filtro</span><span class="sxs-lookup"><span data-stu-id="bfe49-148">1. Code your filter</span></span>

<span data-ttu-id="bfe49-149">En el código, cree una clase que implemente `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="bfe49-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required to support the filter.*/
       private final String successful;

       /* Initializers for the parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry to be sent.
          Return false to discard it.
          Return true to allow other processors to inspect it. */
       @Override
       public boolean process(Telemetry telemetry) {
        if (telemetry == null) { return true; }
        if (telemetry instanceof RequestTelemetry)
        {
            RequestTelemetry requestTelemetry = (RequestTelemetry)telemetry;
            return request.getSuccess() == successful;
        }
        return true;
       }
    }

```


### <a name="2-invoke-your-filter-in-the-configuration-file"></a><span data-ttu-id="bfe49-150">2. Invocación del filtro en el archivo de configuración</span><span class="sxs-lookup"><span data-stu-id="bfe49-150">2. Invoke your filter in the configuration file</span></span>

<span data-ttu-id="bfe49-151">En ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="bfe49-151">In ApplicationInsights.xml:</span></span>

```XML


    <ApplicationInsights>
      <TelemetryProcessors>
        <CustomProcessors>
          <Processor type="com.fabrikam.SuccessFilter">
            <Add name="Successful" value="false"/>
          </Processor>
        </CustomProcessors>
      </TelemetryProcessors>
    </ApplicationInsights>

```

## <a name="troubleshooting"></a><span data-ttu-id="bfe49-152">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="bfe49-152">Troubleshooting</span></span>

<span data-ttu-id="bfe49-153">*El filtro no funciona.*</span><span class="sxs-lookup"><span data-stu-id="bfe49-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="bfe49-154">Compruebe que ha proporcionado valores de parámetro válidos.</span><span class="sxs-lookup"><span data-stu-id="bfe49-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="bfe49-155">Por ejemplo, las duraciones deben ser números enteros.</span><span class="sxs-lookup"><span data-stu-id="bfe49-155">For example, durations should be integers.</span></span> <span data-ttu-id="bfe49-156">Unos valores no válidos hará que el filtro que ignore.</span><span class="sxs-lookup"><span data-stu-id="bfe49-156">Invalid values will cause the filter to be ignored.</span></span> <span data-ttu-id="bfe49-157">Si el filtro personalizado produce una excepción desde un constructor o el método set, se omitirá.</span><span class="sxs-lookup"><span data-stu-id="bfe49-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfe49-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfe49-158">Next steps</span></span>

* <span data-ttu-id="bfe49-159">[Muestreo](app-insights-sampling.md): considere la posibilidad del muestreo como una alternativa que no sesga las métricas.</span><span class="sxs-lookup"><span data-stu-id="bfe49-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
