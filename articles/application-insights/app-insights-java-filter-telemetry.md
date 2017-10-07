---
title: "aaaFilter telemetría de Azure Application Insights en la aplicación web de Java | Documentos de Microsoft"
description: "Reducir el tráfico de telemetría mediante el filtrado de los eventos de hello no es necesario toomonitor."
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
ms.openlocfilehash: 95713e11d5f86472777c67e4e7f3177fbf2cd0b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="filter-telemetry-in-your-java-web-app"></a><span data-ttu-id="ad049-103">Filtrado de telemetría en la aplicación web de Java</span><span class="sxs-lookup"><span data-stu-id="ad049-103">Filter telemetry in your Java web app</span></span>

<span data-ttu-id="ad049-104">Filtros proporcionan una telemetría de hello tooselect de manera que su [aplicación web de Java envía información de tooApplication](app-insights-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ad049-104">Filters provide a way tooselect hello telemetry that your [Java web app sends tooApplication Insights](app-insights-java-get-started.md).</span></span> <span data-ttu-id="ad049-105">Hay algunos filtros de serie que puede utilizar y también puede escribir sus propios filtros personalizados.</span><span class="sxs-lookup"><span data-stu-id="ad049-105">There are some out-of-the-box filters that you can use, and you can also write your own custom filters.</span></span>

<span data-ttu-id="ad049-106">Hola de cuadro filtros incluye:</span><span class="sxs-lookup"><span data-stu-id="ad049-106">hello out-of-the-box filters include:</span></span>

* <span data-ttu-id="ad049-107">El nivel de gravedad del seguimiento</span><span class="sxs-lookup"><span data-stu-id="ad049-107">Trace severity level</span></span>
* <span data-ttu-id="ad049-108">Direcciones URL específicas, palabras clave o códigos de respuesta</span><span class="sxs-lookup"><span data-stu-id="ad049-108">Specific URLs, keywords or response codes</span></span>
* <span data-ttu-id="ad049-109">Respuestas rápidas: es decir, solicitudes toowhich la aplicación respondió tooquickly</span><span class="sxs-lookup"><span data-stu-id="ad049-109">Fast responses - that is, requests toowhich your app responded tooquickly</span></span>
* <span data-ttu-id="ad049-110">Nombres de eventos específicos</span><span class="sxs-lookup"><span data-stu-id="ad049-110">Specific event names</span></span>

> [!NOTE]
> <span data-ttu-id="ad049-111">Filtros sesgar las métricas de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ad049-111">Filters skew hello metrics of your app.</span></span> <span data-ttu-id="ad049-112">Por ejemplo, podría decidir que, en orden toodiagnose lentitud, establecerá un filtro toodiscard rápidos tiempos de respuesta.</span><span class="sxs-lookup"><span data-stu-id="ad049-112">For example, you might decide that, in order toodiagnose slow responses, you will set a filter toodiscard fast response times.</span></span> <span data-ttu-id="ad049-113">Pero debe ser consciente de que los tiempos de respuesta promedio de hello notificados por Application Insights, a continuación, será más lentos que la velocidad de hello true y recuento de Hola de solicitudes será menor que el número real de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad049-113">But you must be aware that hello average response times reported by Application Insights will then be slower than hello true speed, and hello count of requests will be smaller than hello real count.</span></span>
> <span data-ttu-id="ad049-114">Si puede resultar un problema, use el [muestreo](app-insights-sampling.md) en su lugar.</span><span class="sxs-lookup"><span data-stu-id="ad049-114">If this is a concern, use [Sampling](app-insights-sampling.md) instead.</span></span>

## <a name="setting-filters"></a><span data-ttu-id="ad049-115">Establecimiento de filtros</span><span class="sxs-lookup"><span data-stu-id="ad049-115">Setting filters</span></span>

<span data-ttu-id="ad049-116">En ApplicationInsights.xml, agregue una sección `TelemetryProcessors` como la de este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ad049-116">In ApplicationInsights.xml, add a `TelemetryProcessors` section like this example:</span></span>


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
                  <!-- Names of events we don't want toosee -->
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




<span data-ttu-id="ad049-117">[Inspeccionar el conjunto completo de Hola de procesadores integrados](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span><span class="sxs-lookup"><span data-stu-id="ad049-117">[Inspect hello full set of built-in processors](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).</span></span>

## <a name="built-in-filters"></a><span data-ttu-id="ad049-118">Filtros integrados</span><span class="sxs-lookup"><span data-stu-id="ad049-118">Built-in filters</span></span>

### <a name="metric-telemetry-filter"></a><span data-ttu-id="ad049-119">Filtro de telemetría de métricas</span><span class="sxs-lookup"><span data-stu-id="ad049-119">Metric Telemetry filter</span></span>

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* <span data-ttu-id="ad049-120">`NotNeeded`: lista de nombres de métricas personalizados separada por comas.</span><span class="sxs-lookup"><span data-stu-id="ad049-120">`NotNeeded` - Comma-separated list of custom metric names.</span></span>


### <a name="page-view-telemetry-filter"></a><span data-ttu-id="ad049-121">Filtro de telemetría de vista de página</span><span class="sxs-lookup"><span data-stu-id="ad049-121">Page View Telemetry filter</span></span>

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* <span data-ttu-id="ad049-122">`DurationThresholdInMS`-Duración refiere a tiempo toohello página de hello tooload.</span><span class="sxs-lookup"><span data-stu-id="ad049-122">`DurationThresholdInMS` - Duration refers toohello time taken tooload hello page.</span></span> <span data-ttu-id="ad049-123">Si está establecido el tiempo, no se notifican las páginas que se cargan más rápido que en este momento.</span><span class="sxs-lookup"><span data-stu-id="ad049-123">If this is set, pages that loaded faster than this time are not reported.</span></span>
* <span data-ttu-id="ad049-124">`NotNeededNames`: lista de nombres de página separados por comas.</span><span class="sxs-lookup"><span data-stu-id="ad049-124">`NotNeededNames` - Comma-separated list of page names.</span></span>
* <span data-ttu-id="ad049-125">`NotNeededUrls`: lista de fragmentos de URL separados por comas.</span><span class="sxs-lookup"><span data-stu-id="ad049-125">`NotNeededUrls` - Comma-separated list of URL fragments.</span></span> <span data-ttu-id="ad049-126">Por ejemplo, `"home"` filtra todas las páginas que tienen "inicio" en la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="ad049-126">For example, `"home"` filters out all pages that have "home" in hello URL.</span></span>


### <a name="request-telemetry-filter"></a><span data-ttu-id="ad049-127">Filtro de telemetría de solicitudes</span><span class="sxs-lookup"><span data-stu-id="ad049-127">Request Telemetry Filter</span></span>


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a><span data-ttu-id="ad049-128">Filtro de origen sintético</span><span class="sxs-lookup"><span data-stu-id="ad049-128">Synthetic Source filter</span></span>

<span data-ttu-id="ad049-129">Filtra todos los telemetría que tienen valores en hello SyntheticSource propiedad.</span><span class="sxs-lookup"><span data-stu-id="ad049-129">Filters out all telemetry that have values in hello SyntheticSource property.</span></span> <span data-ttu-id="ad049-130">Incluye solicitudes de bots, spiders y pruebas de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="ad049-130">These include requests from bots, spiders and availability tests.</span></span>

<span data-ttu-id="ad049-131">Filtre la telemetría para todas las solicitudes sintéticas:</span><span class="sxs-lookup"><span data-stu-id="ad049-131">Filter out telemetry for all synthetic requests:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" />
```

<span data-ttu-id="ad049-132">Filtre la telemetría para orígenes sintéticos específicos:</span><span class="sxs-lookup"><span data-stu-id="ad049-132">Filter out telemetry for specific synthetic sources:</span></span>


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* <span data-ttu-id="ad049-133">`NotNeeded`: Lista de nombres de origen sintético separados por comas.</span><span class="sxs-lookup"><span data-stu-id="ad049-133">`NotNeeded` - Comma-separated list of synthetic source names.</span></span>

### <a name="telemetry-event-filter"></a><span data-ttu-id="ad049-134">Filtro de eventos de telemetría</span><span class="sxs-lookup"><span data-stu-id="ad049-134">Telemetry Event filter</span></span>

<span data-ttu-id="ad049-135">Filtra los eventos personalizados (registrados mediante [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span><span class="sxs-lookup"><span data-stu-id="ad049-135">Filters custom events (logged using [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).</span></span>


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* <span data-ttu-id="ad049-136">`NotNeededNames`: lista de nombres de eventos separados por comas.</span><span class="sxs-lookup"><span data-stu-id="ad049-136">`NotNeededNames` - Comma-separated list of event names.</span></span>


### <a name="trace-telemetry-filter"></a><span data-ttu-id="ad049-137">Filtro de telemetría de seguimiento</span><span class="sxs-lookup"><span data-stu-id="ad049-137">Trace Telemetry filter</span></span>

<span data-ttu-id="ad049-138">Filtra los seguimientos de registros (registrados mediante [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) o un [recopilador de plataforma de registro](app-insights-java-trace-logs.md)).</span><span class="sxs-lookup"><span data-stu-id="ad049-138">Filters log traces (logged using [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) or a [logging framework collector](app-insights-java-trace-logs.md)).</span></span>

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* <span data-ttu-id="ad049-139">Los valores válidos de `FromSeverityLevel` son:</span><span class="sxs-lookup"><span data-stu-id="ad049-139">`FromSeverityLevel` valid values are:</span></span>
 *  <span data-ttu-id="ad049-140">OFF             - Filtra TODOS los seguimientos</span><span class="sxs-lookup"><span data-stu-id="ad049-140">OFF             - Filter out ALL traces</span></span>
 *  <span data-ttu-id="ad049-141">TRACE           - Sin filtrado.</span><span class="sxs-lookup"><span data-stu-id="ad049-141">TRACE           - No filtering.</span></span> <span data-ttu-id="ad049-142">es igual a nivel de tooTrace</span><span class="sxs-lookup"><span data-stu-id="ad049-142">equals tooTrace level</span></span>
 *  <span data-ttu-id="ad049-143">INFO            - Filtra el nivel TRACE</span><span class="sxs-lookup"><span data-stu-id="ad049-143">INFO            - Filter out TRACE level</span></span>
 *  <span data-ttu-id="ad049-144">WARN            - Filtra el nivel TRACE e INFO</span><span class="sxs-lookup"><span data-stu-id="ad049-144">WARN            - Filter out TRACE and INFO</span></span>
 *  <span data-ttu-id="ad049-145">ERROR           - Filtra WARN, INFO, TRACE</span><span class="sxs-lookup"><span data-stu-id="ad049-145">ERROR           - Filter out WARN, INFO, TRACE</span></span>
 *  <span data-ttu-id="ad049-146">CRITICAL        - Filtra todo menos CRITICAL</span><span class="sxs-lookup"><span data-stu-id="ad049-146">CRITICAL        - filter out all but CRITICAL</span></span>


## <a name="custom-filters"></a><span data-ttu-id="ad049-147">Filtros personalizados</span><span class="sxs-lookup"><span data-stu-id="ad049-147">Custom filters</span></span>

### <a name="1-code-your-filter"></a><span data-ttu-id="ad049-148">1. Codificación del filtro</span><span class="sxs-lookup"><span data-stu-id="ad049-148">1. Code your filter</span></span>

<span data-ttu-id="ad049-149">En el código, cree una clase que implemente `TelemetryProcessor`:</span><span class="sxs-lookup"><span data-stu-id="ad049-149">In your code, create a class that implements `TelemetryProcessor`:</span></span>

```Java

    package com.fabrikam.MyFilter;
    import com.microsoft.applicationinsights.extensibility.TelemetryProcessor;
    import com.microsoft.applicationinsights.telemetry.Telemetry;

    public class SuccessFilter implements TelemetryProcessor {

       /* Any parameters that are required toosupport hello filter.*/
       private final String successful;

       /* Initializers for hello parameters, named "setParameterName" */
       public void setNotNeeded(String successful)
       {
          this.successful = successful;
       }

       /* This method is called for each item of telemetry toobe sent.
          Return false toodiscard it.
          Return true tooallow other processors tooinspect it. */
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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a><span data-ttu-id="ad049-150">2. Invocar el filtro en el archivo de configuración de hello</span><span class="sxs-lookup"><span data-stu-id="ad049-150">2. Invoke your filter in hello configuration file</span></span>

<span data-ttu-id="ad049-151">En ApplicationInsights.xml:</span><span class="sxs-lookup"><span data-stu-id="ad049-151">In ApplicationInsights.xml:</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="ad049-152">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="ad049-152">Troubleshooting</span></span>

<span data-ttu-id="ad049-153">*El filtro no funciona.*</span><span class="sxs-lookup"><span data-stu-id="ad049-153">*My filter isn't working.*</span></span>

* <span data-ttu-id="ad049-154">Compruebe que ha proporcionado valores de parámetro válidos.</span><span class="sxs-lookup"><span data-stu-id="ad049-154">Check that you have provided valid parameter values.</span></span> <span data-ttu-id="ad049-155">Por ejemplo, las duraciones deben ser números enteros.</span><span class="sxs-lookup"><span data-stu-id="ad049-155">For example, durations should be integers.</span></span> <span data-ttu-id="ad049-156">Valores no válidos harán que Hola filtro toobe pasa por alto.</span><span class="sxs-lookup"><span data-stu-id="ad049-156">Invalid values will cause hello filter toobe ignored.</span></span> <span data-ttu-id="ad049-157">Si el filtro personalizado produce una excepción desde un constructor o el método set, se omitirá.</span><span class="sxs-lookup"><span data-stu-id="ad049-157">If your custom filter throws an exception from a constructor or set method, it will be ignored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad049-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ad049-158">Next steps</span></span>

* <span data-ttu-id="ad049-159">[Muestreo](app-insights-sampling.md): considere la posibilidad del muestreo como una alternativa que no sesga las métricas.</span><span class="sxs-lookup"><span data-stu-id="ad049-159">[Sampling](app-insights-sampling.md) - Consider sampling as an alternative that does not skew your metrics.</span></span>
