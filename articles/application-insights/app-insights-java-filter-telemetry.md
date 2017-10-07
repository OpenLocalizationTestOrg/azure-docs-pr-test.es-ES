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
# <a name="filter-telemetry-in-your-java-web-app"></a>Filtrado de telemetría en la aplicación web de Java

Filtros proporcionan una telemetría de hello tooselect de manera que su [aplicación web de Java envía información de tooApplication](app-insights-java-get-started.md). Hay algunos filtros de serie que puede utilizar y también puede escribir sus propios filtros personalizados.

Hola de cuadro filtros incluye:

* El nivel de gravedad del seguimiento
* Direcciones URL específicas, palabras clave o códigos de respuesta
* Respuestas rápidas: es decir, solicitudes toowhich la aplicación respondió tooquickly
* Nombres de eventos específicos

> [!NOTE]
> Filtros sesgar las métricas de saludo de la aplicación. Por ejemplo, podría decidir que, en orden toodiagnose lentitud, establecerá un filtro toodiscard rápidos tiempos de respuesta. Pero debe ser consciente de que los tiempos de respuesta promedio de hello notificados por Application Insights, a continuación, será más lentos que la velocidad de hello true y recuento de Hola de solicitudes será menor que el número real de Hola.
> Si puede resultar un problema, use el [muestreo](app-insights-sampling.md) en su lugar.

## <a name="setting-filters"></a>Establecimiento de filtros

En ApplicationInsights.xml, agregue una sección `TelemetryProcessors` como la de este ejemplo:


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




[Inspeccionar el conjunto completo de Hola de procesadores integrados](https://github.com/Microsoft/ApplicationInsights-Java/tree/master/core/src/main/java/com/microsoft/applicationinsights/internal/processor).

## <a name="built-in-filters"></a>Filtros integrados

### <a name="metric-telemetry-filter"></a>Filtro de telemetría de métricas

```XML

           <Processor type="MetricTelemetryFilter">
                  <Add name="NotNeeded" value="metric1,metric2"/>
           </Processor>
```

* `NotNeeded`: lista de nombres de métricas personalizados separada por comas.


### <a name="page-view-telemetry-filter"></a>Filtro de telemetría de vista de página

```XML

           <Processor type="PageViewTelemetryFilter">
                  <Add name="DurationThresholdInMS" value="500"/>
                  <Add name="NotNeededNames" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```

* `DurationThresholdInMS`-Duración refiere a tiempo toohello página de hello tooload. Si está establecido el tiempo, no se notifican las páginas que se cargan más rápido que en este momento.
* `NotNeededNames`: lista de nombres de página separados por comas.
* `NotNeededUrls`: lista de fragmentos de URL separados por comas. Por ejemplo, `"home"` filtra todas las páginas que tienen "inicio" en la dirección URL de Hola.


### <a name="request-telemetry-filter"></a>Filtro de telemetría de solicitudes


```XML

           <Processor type="RequestTelemetryFilter">
                  <Add name="MinimumDurationInMS" value="500"/>
                  <Add name="NotNeededResponseCodes" value="page1,page2"/>
                  <Add name="NotNeededUrls" value="url1,url2"/>
           </Processor>
```



### <a name="synthetic-source-filter"></a>Filtro de origen sintético

Filtra todos los telemetría que tienen valores en hello SyntheticSource propiedad. Incluye solicitudes de bots, spiders y pruebas de disponibilidad.

Filtre la telemetría para todas las solicitudes sintéticas:


```XML

           <Processor type="SyntheticSourceFilter" />
```

Filtre la telemetría para orígenes sintéticos específicos:


```XML

           <Processor type="SyntheticSourceFilter" >
                  <Add name="NotNeeded" value="source1,source2"/>
           </Processor>
```

* `NotNeeded`: Lista de nombres de origen sintético separados por comas.

### <a name="telemetry-event-filter"></a>Filtro de eventos de telemetría

Filtra los eventos personalizados (registrados mediante [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)).


```XML

           <Processor type="TelemetryEventFilter" >
                  <Add name="NotNeededNames" value="event1, event2"/>
           </Processor>
```


* `NotNeededNames`: lista de nombres de eventos separados por comas.


### <a name="trace-telemetry-filter"></a>Filtro de telemetría de seguimiento

Filtra los seguimientos de registros (registrados mediante [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) o un [recopilador de plataforma de registro](app-insights-java-trace-logs.md)).

```XML

           <Processor type="TraceTelemetryFilter">
                  <Add name="FromSeverityLevel" value="ERROR"/>
           </Processor>
```

* Los valores válidos de `FromSeverityLevel` son:
 *  OFF             - Filtra TODOS los seguimientos
 *  TRACE           - Sin filtrado. es igual a nivel de tooTrace
 *  INFO            - Filtra el nivel TRACE
 *  WARN            - Filtra el nivel TRACE e INFO
 *  ERROR           - Filtra WARN, INFO, TRACE
 *  CRITICAL        - Filtra todo menos CRITICAL


## <a name="custom-filters"></a>Filtros personalizados

### <a name="1-code-your-filter"></a>1. Codificación del filtro

En el código, cree una clase que implemente `TelemetryProcessor`:

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


### <a name="2-invoke-your-filter-in-hello-configuration-file"></a>2. Invocar el filtro en el archivo de configuración de hello

En ApplicationInsights.xml:

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

## <a name="troubleshooting"></a>Solución de problemas

*El filtro no funciona.*

* Compruebe que ha proporcionado valores de parámetro válidos. Por ejemplo, las duraciones deben ser números enteros. Valores no válidos harán que Hola filtro toobe pasa por alto. Si el filtro personalizado produce una excepción desde un constructor o el método set, se omitirá.

## <a name="next-steps"></a>Pasos siguientes

* [Muestreo](app-insights-sampling.md): considere la posibilidad del muestreo como una alternativa que no sesga las métricas.
