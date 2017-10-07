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
# <a name="application-insights-api-for-custom-events-and-metrics"></a>API de Application Insights para eventos y métricas personalizados

Insertar unas pocas líneas de código en su toofind de aplicación a lo que hacen los usuarios con él o toohelp diagnosticar problemas. Puede enviar datos de telemetría desde aplicaciones de escritorio y de dispositivo y desde clientes y servidores web. Hola de uso [Azure Application Insights](app-insights-overview.md) principales de eventos personalizados de telemetría API toosend y las métricas y las versiones de telemetría estándar. Esta API es Hola misma API dicho estándar Hola usar recopiladores de datos de Application Insights.

## <a name="api-summary"></a>API summary
Hola API es uniforme en todas las plataformas, además de algunas pequeñas variaciones.

| Método | Usado para |
| --- | --- |
| [`TrackPageView`](#page-views) |Páginas, pantallas, hojas o formularios. |
| [`TrackEvent`](#trackevent) |Acciones de usuario y otros eventos. Rendimiento de comportamiento o toomonitor de usuario tootrack usado. |
| [`TrackMetric`](#trackmetric) |Medidas de rendimiento, como la longitud de las colas no relacionados con eventos toospecific. |
| [`TrackException`](#trackexception) |Excepciones de registro para diagnóstico. Seguimiento donde se producen en los eventos de relación tooother y examinar los seguimientos de pila. |
| [`TrackRequest`](#trackrequest) |Registro de hello frecuencia y duración de las solicitudes de servidor para el análisis de rendimiento. |
| [`TrackTrace`](#tracktrace) |Mensajes de registro de diagnóstico. También puede capturar registros de terceros. |
| [`TrackDependency`](#trackdependency) |Registro de hello duración y frecuencia de los componentes de tooexternal de llamadas que depende de la aplicación. |

También puede [adjuntar propiedades y las métricas de](#properties) toomost de estas llamadas de telemetría.

## <a name="prep"></a>Antes de comenzar
Si aún no tiene una referencia en el SDK de Application Insights:

* Agregar proyecto de hello Application Insights SDK tooyour:

  * [Proyecto de ASP.NET](app-insights-asp-net.md)
  * [Proyecto de Java](app-insights-java-get-started.md)
  * [JavaScript en cada página web](app-insights-javascript.md) 
* En el código de servidor web o de dispositivo, incluya:

    *C#:*`using Microsoft.ApplicationInsights;`

    *Visual Basic:*`Imports Microsoft.ApplicationInsights`

    *Java:*`import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>Construcción de una instancia de TelemetryClient
Construcción de una instancia de `TelemetryClient` (excepto en JavaScript en páginas web):

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

TelemetryClient es seguro para subprocesos.

Se recomienda que use una instancia de TelemetryClient para cada módulo de la aplicación. Por ejemplo, puede tener una instancia de TelemetryClient en las solicitudes de HTTP entrantes y tooreport con servicio web y otra en una eventos de lógica de negocios de middleware clase tooreport. Puede establecer las propiedades como `TelemetryClient.Context.User.Id` tootrack usuarios y sesiones, o `TelemetryClient.Context.Device.Id` máquina de hello tooidentify. Esta información es eventos tooall adjunto que Hola envíos de instancia.

## <a name="trackevent"></a>TrackEvent
En Application Insights, un *evento personalizado* es un punto de datos que se puede mostrar en el [Explorador de métricas](app-insights-metrics-explorer.md) como recuento agregado, y como repeticiones individuales en [Búsqueda de diagnóstico](app-insights-diagnostic-search.md). (No relacionado tooMVC u otros framework "eventos".)

Insertar `TrackEvent` llama en su código toocount diversos eventos. la frecuencia con la que los usuarios eligen una determinada característica, con la que logran unos determinados objetivos o con la que cometen determinados tipos de errores.

Por ejemplo, en una aplicación de juego, enviar un evento cada vez que un usuario gana el juego de hello:

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>Ver los eventos en el portal de Microsoft Azure Hola
toosee un recuento de los eventos, abra un [Explorer métricas](app-insights-metrics-explorer.md) hoja, agregar un nuevo gráfico y seleccione **eventos**.  

![Visualización de un recuento de eventos personalizados](./media/app-insights-api-custom-events-metrics/01-custom.png)

recuentos de hello toocompare diversos eventos, establezca el tipo de gráfico de Hola de demasiado**cuadrícula**y de grupo por nombre de evento:

![Establece el tipo de gráfico de Hola y de agrupación](./media/app-insights-api-custom-events-metrics/07-grid.png)

En la cuadrícula de hello, haga clic en a través de un evento nombre toosee las repeticiones individuales de ese evento. toosee más detallada: haga clic en cualquier aparición en la lista de Hola.

![Obtención de eventos de Hola](./media/app-insights-api-custom-events-metrics/03-instances.png)

toofocus según determinados eventos en la búsqueda o en el Explorador de métricas, nombres de evento de toohello de filtro del conjunto Hola hoja que le interesa:

![Abre filtros, expanda el nombre del evento y seleccione uno o varios valores.](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>Eventos personalizados en Analytics

telemetría Hola está disponible en hello `customEvents` tabla [el análisis de visión aplicaciones](app-insights-analytics.md). Cada fila representa una llamada demasiado`trackEvent(..)` en la aplicación. 

Si [muestreo](app-insights-sampling.md) está en funcionamiento, la propiedad itemCount de hello muestra un valor mayor que 1. Para el ejemplo itemCount == 10 significa que de 10 llamadas tootrackEvent(), proceso de muestreo de hello sólo transmite uno de ellos. tooget un número correcto de eventos personalizados, debe utilizar, por tanto, use código como `customEvent | summarize sum(itemCount)`.


## <a name="trackmetric"></a>TrackMetric

Application Insights pueden gráfico de métricas que no son eventos tooparticular adjunto. Por ejemplo, puede supervisar una longitud de cola a intervalos regulares. Con métricas, medidas individuales de hello son de menos interés que las variaciones de Hola y las tendencias y, por lo que estadística gráficos son útiles.

En ordenar las métricas de toosend tooApplication visión, puede usar hello `TrackMetric(..)` API. Una métrica no hay toosend de dos maneras: 

* Valor único. Cada vez que realiza una medida en la aplicación, debe enviar valor correspondiente de hello tooApplication visión. Por ejemplo, suponga que tiene una métrica que describe el número de Hola de elementos de un contenedor. Durante un período de tiempo determinado, primero se pone tres elementos en el contenedor de hello y, a continuación, quite dos elementos. En consecuencia, se llamaría a `TrackMetric` dos veces: primero se pasa el valor de hello `3` y, a continuación, Hola valor `-2`. Application Insights almacena ambos valores en su nombre. 

* Agregación. Al trabajar con métricas, las mediciones individuales pocas veces resultan de interés. En su lugar, lo importante son los resúmenes de acontecimientos durante un período determinado. Los resúmenes de este tipo se denominan _agregaciones_. Hola ejemplo anterior, las métricas suma de agregados de Hola durante ese período de tiempo es `1` y Hola recuento de valores de métrica de hello es `2`. Cuando se usa el enfoque de agregación de hello, solo se invoque `TrackMetric` una vez por período y envío Hola agregados valores de hora. Se trata de hello enfoque recomendado, ya que puede reducir considerablemente el coste de Hola y rendimiento sobrecarga mediante el envío de datos menos puntos tooApplication visión, mientras todavía recopilar toda la información pertinente.

### <a name="examples"></a>Ejemplos:

#### <a name="single-values"></a>Valores únicos

toosend un único valor de métrica:

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>Agregación de métricas

Se recomienda tooaggregate métricas antes de enviarlos desde su aplicación, el ancho de banda de tooreduce, tooimprove y costo de rendimiento.
Este es un ejemplo de código de agregación:

*C#*

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

### <a name="custom-metrics-in-metrics-explorer"></a>Métricas personalizadas en el Explorador de métricas

resultados de hello toosee, abra el Explorador de métricas y agregar un nuevo gráfico. Editar Hola gráfico tooshow la métrica.

> [!NOTE]
> La métrica personalizada puede tardar varios tooappear minutos en lista de Hola de métricas disponibles.
>

![Agregue un gráfico nuevo o seleccione un gráfico y, en Personalizada, seleccione su métrica.](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Métricas personalizadas en Analytics

telemetría Hola está disponible en hello `customMetrics` tabla [el análisis de visión aplicaciones](app-insights-analytics.md). Cada fila representa una llamada demasiado`trackMetric(..)` en la aplicación.
* `valueSum`-Esta es la suma de Hola de mediciones de Hola. valor promedio tooget hello, división por `valueCount`.
* `valueCount`-Hola número de medidas que se han agregado en este `trackMetric(..)` llamar.

## <a name="page-views"></a>Vistas de página
En una aplicación de dispositivo o de página web, se envían datos de telemetría de la vista de página de forma predeterminada cuando se carga cada pantalla o página. Pero puede cambiar las vistas de esa página tootrack en momentos diferentes o adicionales. Por ejemplo, en una aplicación que muestra las pestañas o las hojas, conviene tootrack una página siempre que sea usuario de hello abre una nueva hoja.

![Uso de modos en la hoja Información general](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

Datos de usuario y la sesión se envían como propiedades junto con las vistas de página, por lo que Hola gráficos de usuario y la sesión dotándolo cuando hay telemetría de vista de página.

### <a name="custom-page-views"></a>Vistas de página personalizadas
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


Si tiene varias pestañas en distintas páginas HTML, puede especificar la dirección URL de hello demasiado:

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>Cronometrar las vistas de página
De forma predeterminada, los tiempos de Hola se notifican como **tiempo de carga de vista de página** se miden desde al explorador de hello envía la solicitud de hello, hasta que se llama al evento de carga de página del explorador de Hola.

En su lugar, puede:

* Establecer una duración explícita en hello [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) llamar: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.
* Usar llamadas de control de tiempo de vista de página de hello `startTrackPage` y `stopTrackPage`.

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

Hola nombre que se utiliza como primer parámetro de hello asocia inicio hello y detener las llamadas. El valor predeterminado es toohello nombre actual de la página.

carga de página resultante Hello las duraciones que se muestra en el Explorador de métricas se derivan de intervalo de saludo entre Hola iniciar y detener las llamadas. Es una tooyou el intervalo de tiempo si realmente.

### <a name="page-telemetry-in-analytics"></a>Telemetría de páginas en Analytics

En [Analytics](app-insights-analytics.md) hay dos tablas en las que se muestran datos de operaciones de explorador:

* Hola `pageViews` tabla contiene datos sobre el título de página y la dirección URL de Hola
* Hola `browserTimings` tabla contiene datos sobre el rendimiento de cliente, como tooprocess de tiempo que tarda Hola Hola los datos entrantes

toofind cuánto explorador Hola toma tooprocess páginas diferentes:

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

toodiscover popularities de Hola de exploradores diferentes:

```
pageViews | summarize count() by client_Browser
```

vistas de página tooassociate llamadas tooAJAX, unir con dependencias:

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
servidor de Hello SDK usa las solicitudes HTTP de toolog TrackRequest.

También puede llamarlo usted mismo si desea que las solicitudes de toosimulate en un contexto donde no haya hello web servicio módulo que se ejecuta.

Sin embargo, Hola recomienda telemetría de solicitud de manera toosend es donde solicitud Hola actúa como un <a href="#operation-context">contexto de operación</a>.

## <a name="operation-context"></a>Contexto de operación
Puede asociar elementos de telemetría juntos mediante una asociación toothem un identificador de operación común. módulo de seguimiento de solicitud estándar Hola hace excepciones y otros eventos que se envían mientras se procesa una solicitud HTTP. En [búsqueda](app-insights-diagnostic-search.md) y [análisis](app-insights-analytics.md), puede usar los eventos asociados con la solicitud de Hola Hola identificador tooeasily buscar.

Identificador de Hola de manera más fácil de Hello tooset es tooset un contexto de la operación mediante el uso de este patrón:

*C#*

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

Junto con la configuración de un contexto de la operación, `StartOperation` crea un elemento de telemetría de tipo hello que especifique. Envía elementos telemetría hello cuando dispose operación hello, o si se llama explícitamente a `StopOperation`. Si usa `RequestTelemetry` como tipo de telemetría de hello, su duración se establece intervalo toohello ha superado el tiempo entre el inicio y detención.

Los contextos de operación no pueden estar anidados. Si ya hay un contexto de la operación, entonces su identificador está asociado a todos los elementos de hello contenido, incluido elemento Hola creado con `StartOperation`.

En la búsqueda, contexto de la operación de hello es hello toocreate usado **elementos relacionados** lista:

![Elementos relacionados](./media/app-insights-api-custom-events-metrics/21.png)

Consulte [application-insights-custom-operations-tracking.md.md] para más información sobre el seguimiento de las operaciones personalizadas.

### <a name="requests-in-analytics"></a>Solicitudes en Analytics 

En [el análisis de visión aplicaciones](app-insights-analytics.md), solicita mostrar seguridad Hola `requests` tabla.

Si [muestreo](app-insights-sampling.md) está en funcionamiento, propiedad itemCount de hello muestra un valor mayor que 1. Para el ejemplo itemCount == 10 significa que de 10 llamadas tootrackRequest(), proceso de muestreo de hello sólo transmite uno de ellos. un número correcto de las solicitudes y la duración media de tooget segmentadas por nombres de la solicitud, utilice código como:

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
Enviar excepciones tooApplication visión:

* demasiado[contarlas](app-insights-metrics-explorer.md), como una indicación de frecuencia de Hola de un problema.
* demasiado[examine todos los casos individuales](app-insights-diagnostic-search.md).

los informes de Hello incluyen seguimientos de pila de Hola.

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

SDK de Hello detecta automáticamente, muchas de las excepciones para que no tenga siempre toocall TrackException explícitamente.

* ASP.NET: [escribir código excepciones toocatch](app-insights-asp-net-exceptions.md).
* J2EE: [las excepciones se detectan automáticamente](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript: las excepciones se detectan automáticamente. Si desea que la recopilación automática de toodisable, agregue un fragmento de código de toohello de línea que se inserta en las páginas Web:

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>Excepciones en Analytics

En [el análisis de visión aplicaciones](app-insights-analytics.md), las excepciones se mostrarán en hello `exceptions` tabla.

Si [muestreo](app-insights-sampling.md) está en funcionamiento, hello `itemCount` propiedad muestra un valor mayor que 1. Para el ejemplo itemCount == 10 significa que de 10 llamadas tootrackException(), proceso de muestreo de hello sólo transmite uno de ellos. tooget un número correcto de excepciones segmentadas por tipo de excepción, utilice código como:

```
exceptions | summarize sum(itemCount) by type
```

La mayoría de hello importante información de la pila ya se extrae en variables independientes, pero se puede extraer de hello distinguirlos `details` tooget estructura más. Puesto que esta estructura es dinámica, debe convertir el tipo del resultado de hello toohello que espera. Por ejemplo:

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

excepciones de tooassociate con sus solicitudes relacionados, use una combinación:

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
Use TrackTrace toohelp diagnosticar problemas mediante el envío de un "rastro de la ruta de navegación" tooApplication visión. Puede enviar fragmentos de datos de diagnóstico e inspeccionarlos en [Búsqueda de diagnóstico](app-insights-diagnostic-search.md).

[Registrar adaptadores](app-insights-asp-net-trace-logs.md) usar este portal de toohello API toosend registros de aplicaciones de terceros.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


Puede buscar en el contenido del mensaje, pero (a diferencia de los valores de propiedad) no puede filtrar por él.

límite de tamaño Hello `message` es mucho mayor que el límite de hello en Propiedades.
La ventaja de TrackTrace es que puede colocar datos relativamente largos en mensajes de bienvenida. Por ejemplo, aquí puede codificar datos POST.  

Además, puede agregar un mensaje de tooyour de nivel de gravedad. Y, al igual que otros telemetría, puede agregar toohelp de valores de propiedad que filtra o buscar para diferentes conjuntos de seguimientos. Por ejemplo:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

En [búsqueda](app-insights-diagnostic-search.md), a continuación, puede filtrar fácilmente todos los mensajes de Hola un nivel de gravedad determinado que se relacionan tooa base de datos determinada.


### <a name="traces-in-analytics"></a>Seguimientos en Analytics

En [el análisis de visión aplicaciones](app-insights-analytics.md), se llama tooTrackTrace mostrar Hola `traces` tabla.

Si [muestreo](app-insights-sampling.md) está en funcionamiento, la propiedad itemCount de hello muestra un valor mayor que 1. Para el ejemplo itemCount == 10 significa que de 10 llamadas demasiado`trackTrace()`, proceso de muestreo de hello transmite solo uno de ellos. tooget un número correcto de las llamadas de seguimiento, se debe utilizar, por tanto, código como `traces | summarize sum(itemCount)`.

## <a name="trackdependency"></a>TrackDependency
Hola de uso TrackDependency llamar a tiempos de respuesta de hello tootrack y las tasas de éxito de pieza externo de tooan de llamadas de código. los resultados de Hello aparecen en los gráficos de dependencia de hello en el portal de Hola.

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

Recuerde que ese servidor hello SDKs incluyen un [módulo dependencia](app-insights-asp-net-dependencies.md) que detecta y realiza un seguimiento de determinadas llamadas de dependencia automáticamente; por ejemplo, toodatabases y las API de REST. Deberá tooinstall un agente en el módulo de hello toomake de servidor de trabajo. Use esta llamada si desea que no detectar llamadas tootrack que Hola seguimiento automatizado o si no desea a tooinstall agente de Hola.

Editar tooturn desactivar el módulo de seguimiento de dependencias estándar hello, [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md) y elimine la referencia de hello demasiado`DependencyCollector.DependencyTrackingTelemetryModule`.

### <a name="dependencies-in-analytics"></a>Dependencias en Analytics

En [el análisis de visión aplicaciones](app-insights-analytics.md), trackDependency llamadas aparecen en hello `dependencies` tabla.

Si [muestreo](app-insights-sampling.md) está en funcionamiento, la propiedad itemCount de hello muestra un valor mayor que 1. Para el ejemplo itemCount == 10 significa que de 10 llamadas tootrackDependency(), proceso de muestreo de hello sólo transmite uno de ellos. tooget un número correcto de dependencias segmentadas por componente de destino, utilice código como:

```
dependencies | summarize sum(itemCount) by target
```

dependencias de tooassociate con sus solicitudes relacionados, use una combinación:

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>Datos de vaciado
Normalmente, Hola SDK envía datos a veces elegidos toominimize impacto de hello en usuario Hola. Sin embargo, en algunos casos, conviene búfer de Hola tooflush: por ejemplo, si usas Hola SDK en una aplicación que se cierra.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

Tenga en cuenta que la función hello es asincrónico para hello [canal del servidor de telemetría](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).

## <a name="authenticated-users"></a>Usuarios autenticados
En una aplicación web, los usuarios se identifican por cookies (de manera predeterminada). Se puede contar al usuario más de una vez si accede a la aplicación desde un equipo o explorador diferente, o si elimina las cookies.

Si los usuarios inician sesión en la aplicación de tooyour, puede obtener un recuento más preciso estableciendo Id. de usuario de hello autenticado en el código de hello explorador:

*JavaScript*

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

En una aplicación MVC web de ASP.NET, por ejemplo:

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

No es el nombre de inicio de sesión real del usuario de hello toouse necesarios. Solo tiene toobe un identificador de usuario único toothat. No puede contener espacios ni ninguno de los caracteres de hello `,;=|`.

Id. de usuario de Hello también se establece en una cookie de sesión y envía toohello server. Si el servidor de hello SDK está instalado, Hola autentica usuario que identificador se envía como parte de las propiedades de contexto de Hola de telemetría de cliente y servidor. A continuación, puede filtrar y buscar en ella.

Si la aplicación agrupa a los usuarios en las cuentas, también se puede pasar un identificador de cuenta de hello (con hello mismo carácter restricciones).

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

En el [Explorador de métricas](app-insights-metrics-explorer.md), puede crear un gráfico que cuente los **Usuarios autenticados** y las **Cuentas de usuario**.

También puede [buscar](app-insights-diagnostic-search.md) puntos de datos de cliente con cuentas y nombres de usuario específicos.

## <a name="properties"></a>Filtrado, búsqueda y segmentación de los datos mediante el uso de propiedades
Puede asociar propiedades y las medidas tooyour eventos (y también toometrics, vistas de página, las excepciones y otros datos de telemetría).

*Propiedades* son valores de cadena que puede usar la telemetría toofilter en informes de uso de Hola. Por ejemplo, si la aplicación proporciona varios juegos, puede adjuntar nombre Hola de evento de hello tooeach juego para que pueda comprobar qué juegos son los más populares.

Hay un límite de 8192 en longitud de la cadena de Hola. (Si desea que toosend grandes cantidades de datos, utilice el parámetro de mensaje de Hola de [TrackTrace](#track-trace).)

*métricas* son valores numéricos que se pueden presentar de forma gráfica. Por ejemplo, puede toosee si hay un aumento gradual de las puntuaciones de hello lograr los jugadores. gráficos de Hola se pueden segmentar por hello separan de propiedades que se envían con el evento de hello, para que pueda obtener o apilan gráficos de juegos.

Para valores de métrica toobe muestra correctamente, deben ser igual o mayor que too0.

Hay algunos [límites en hello número de propiedades, valores de propiedad y las métricas de](#limits) que puede usar.

*JavaScript*

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


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> Tenga cuidado de no toolog información personal identificable en Propiedades.
>
>

*Si ha usado las métricas*, abra el Explorador de métricas y seleccione la métrica de hello en hello **personalizado** grupo:

![Abra el Explorador de métricas, gráfico de hello seleccione y seleccione Hola métrica](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> Si no aparece la métrica, o si hello **personalizado** encabezado no está allí, hoja de selección de hello cierre y vuelva a intentarlo. Las métricas pueden durar una hora toobe se agregan a través de la canalización de Hola.

*Si ha utilizado propiedades y las métricas*, segmentar métrica Hola propiedad hello:

![Establecer agrupación y, a continuación, seleccione la propiedad de hello en Agrupar por](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*En la búsqueda de diagnóstico*, puede ver las propiedades de Hola y métricas de repeticiones individuales de un evento.

![Seleccione una instancia y luego seleccione "...".](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

Hola de uso **búsqueda** campo toosee repeticiones del evento que tienen un valor de propiedad concreto.

![Escriba un término en Buscar.](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[Más información sobre las expresiones de búsqueda](app-insights-diagnostic-search.md).

### <a name="alternative-way-tooset-properties-and-metrics"></a>Las métricas y las propiedades de tooset de manera alternativa
Si resulta más eficaz, puede recopilar parámetros de Hola de un evento en un objeto independiente:

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> No volver a usar Hola misma instancia de elemento de telemetría (`event` en este ejemplo) toocall Track*() varias veces. Esto puede provocar toobe telemetría enviado con una configuración incorrecta.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>Mediciones y propiedades personalizadas en Analytics

En [análisis](app-insights-analytics.md), métricas personalizadas y propiedades que se muestran en hello `customMeasurements` y `customDimensions` atributos de cada registro de telemetría.

Por ejemplo, si ha agregado una propiedad denominada "juegos" tooyour telemetría de solicitud, esta consulta recuentos de apariciones de Hola de valores distintos de "juego" y muestra la media de Hola de hello métrica personalizada "puntuación":

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

Tenga en lo siguiente:

* Cuando se extrae un valor de hello customDimensions o customMeasurements JSON, tiene el tipo dinámico y, por lo que debe convertir `tostring` o `todouble`.
* cuenta de tootake de posibilidad de Hola de [muestreo](app-insights-sampling.md), debe usar `sum(itemCount)`, no `count()`.



## <a name="timed"></a> Eventos de temporización
A veces desea toochart cuánto tiempo tarda tooperform una acción. Por ejemplo, puede querer tooknow cuánto tiempo los usuarios realizar tooconsider opciones en un juego. Puede usar el parámetro de medición de Hola para esto.

*C#*

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



## <a name="defaults"></a>Propiedades predeterminadas para la telemetría personalizada
Si desea tooset valores de propiedad predeterminados para algunos de los eventos personalizados de hello creado por usted, se puede establecer en una instancia de TelemetryClient. Son elementos de telemetría tooevery adjunto que se envían desde ese cliente.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



Llamadas de telemetría individual pueden invalidar valores predeterminados de hello en los diccionarios de propiedad.

*Para los clientes web de JavaScript*, [use los inicializadores de telemetría de JavaScript](#js-initializer).

*telemetría de tooadd propiedades tooall*, incluidos los datos de Hola de los módulos de colección estándar, [implementar `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).

## <a name="sampling-filtering-and-processing-telemetry"></a>Muestreo, filtrado y procesamiento de telemetría
Puede escribir código tooprocess la telemetría antes de que se envíe desde Hola SDK. el procesamiento de Hello incluye datos que se envían desde los módulos de telemetría estándar hello, como colección de solicitud HTTP y la colección de dependencias.

[Agregar propiedades](app-insights-api-filtering-sampling.md#add-properties) tootelemetry implementando `ITelemetryInitializer`. Por ejemplo, puede agregar números de versión o valores calculados a partir de otras propiedades.

[Filtrado](app-insights-api-filtering-sampling.md#filtering) puede modificar o descartar telemetría antes de que se envíe de hello SDK mediante la implementación de `ITelemetryProcesor`. Controlar lo que se envía o se descartan, pero tienes tooaccount de efecto de hello en las métricas. Dependiendo de cómo descartar elementos, podría perder Hola capacidad toonavigate entre los elementos relacionados.

[Muestreo](app-insights-api-filtering-sampling.md) es un volumen de solución empaquetada tooreduce Hola de datos que se envían desde el portal de toohello de aplicación. Lo hace sin que afecte a las métricas de muestra de Hola. Y lo hace sin que afecte a los problemas de capacidad toodiagnose por navegar entre elementos relacionados, como excepciones, las solicitudes y las vistas de página.

[Más información](app-insights-api-filtering-sampling.md).

## <a name="disabling-telemetry"></a>Deshabilitación de la telemetría
demasiado*dinámicamente detener e iniciar* Hola recopilación y transmisión de telemetría:

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

demasiado*deshabilitar los recopiladores estándares seleccionados*: por ejemplo, los contadores de rendimiento, las solicitudes HTTP o dependencias: eliminar o marque como comentario las líneas relevantes de hello en [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Para hacer esto, por ejemplo, si desea que toosend sus propios datos TrackRequest.

## <a name="debug"></a>Modo de programador
Durante la depuración, resulta útil toohave la telemetría acelerada a través de la canalización de Hola para que puedan ver los resultados inmediatamente. Get también mensajes adicionales que le ayudarán a seguimiento de los problemas con la telemetría Hola. Desactívelo en producción, ya que puede ralentizar la aplicación.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>Configuración de clave de instrumentación de Hola para telemetría personalizada seleccionada
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a> Copia de la clave de instrumentación
tooavoid combinación de telemetría de desarrollo, pruebas y entornos de producción, también puede [crear recursos de Application Insights separados](app-insights-create-new-resource.md) y cambiar sus claves, según el entorno de Hola.

En lugar de obtener clave de instrumentación de Hola Hola archivo de configuración, puede establecer en el código. Establezca la clave de hello en un método de inicialización, como global.aspx.cs en un servicio ASP.NET:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



En las páginas Web, le podría interesar tooset desde el servidor web de hello estado, en lugar de codificar de forma literal en script de Hola. Por ejemplo, en una página web generada en una aplicación ASP.NET:

*JavaScript en Razor*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>TelemetryContext
TelemetryClient tiene una propiedad de Context, que contiene valores que se envían junto con todos los datos de telemetría. Normalmente se establecen mediante módulos de hello telemetría estándar, pero también puede establecerlas usted mismo. Por ejemplo:

    telemetry.Context.Operation.Name = "MyOperationName";

Si se establece cualquiera de estos valores usted mismo, considere la posibilidad de quitar la línea correspondiente de Hola de [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), de modo que no confundir a los valores y Hola estándar.

* **Componente**: Hola aplicación y su versión.
* **Dispositivo**: datos sobre el que se ejecuta la aplicación hello de dispositivo de Hola. (En las aplicaciones web, esto es servidor de Hola o dispositivo de cliente que telemetría Hola se envía desde.)
* **InstrumentationKey**: Hola recursos de Application Insights en Azure dónde deben aparecer telemetría Hola. Normalmente, se selecciona de ApplicationInsights.config.
* **Ubicación**: Hola ubicación geográfica del dispositivo de Hola.
* **Operación**: en las aplicaciones web, Hola solicitud HTTP actual. En otros tipos de aplicación, puede establecer esta eventos toogroup juntos.
  * **Id**: valor generado que correlaciona distintos eventos, de modo que cuando usted inspeccione cualquier evento en Búsqueda de diagnóstico, puede encontrar elementos relacionados.
  * **Nombre**: un identificador, normalmente Hola dirección URL de solicitud de hello HTTP.
  * **SyntheticSource**: si no nulo o está vacío, una cadena que indica que ese origen Hola de solicitud de hello ha identificado como una prueba web o robot. De forma predeterminada, se excluye de cálculos en el Explorador de métricas.
* **Properties**: propiedades que se envían con todos los datos de telemetría. Se pueden invalidar en llamadas de seguimiento* individuales.
* **Sesión**: sesión de usuario de Hola. Id. de Hello es establecer el valor de tooa generado, que se cambia cuando el usuario de hello no ha estado activo durante un tiempo.
* **User**: información del usuario.

## <a name="limits"></a>límites
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

tooavoid alcanzando el límite de velocidad de datos de hello, use [muestreo](app-insights-sampling.md).

toodetermine cómo se mantienen los datos de tipo long, consulte [retención de datos y privacidad](app-insights-data-retention-privacy.md).

## <a name="reference-docs"></a>Documentos de referencia
* [Referencia de ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)
* [Referencia de Java](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [Referencia de JavaScript](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [SDK de Android](https://github.com/Microsoft/ApplicationInsights-Android)
* [SDK de iOS](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>Código del SDK
* [SDK básico de ASP.NET](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Paquetes de Windows Server](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [SDK de Java](https://github.com/Microsoft/ApplicationInsights-Java)
* [SDK de JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)
* [Todas las plataformas](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>Preguntas
* *¿Qué excepciones pueden iniciar las llamadas de seguimiento_()?*

    Ninguno. No es necesario toowrap usarlas en las cláusulas try-catch. Si Hola SDK detecta problemas, registrará mensajes de salida de consola de depuración de hello y--si hello los mensajes lleguen a través de: en la búsqueda de diagnóstico.
* *¿Hay un dato de tooget de API de REST desde el portal de hello?*

    Sí, Hola [API de acceso a datos](https://dev.applicationinsights.io/). Incluyen otros datos de formas tooextract [exportar de análisis tooPower BI](app-insights-export-power-bi.md) y [exportación continua](app-insights-export-telemetry.md).

## <a name="next"></a>Pasos siguientes
* [Búsqueda de eventos y registros](app-insights-diagnostic-search.md)

* [Solución de problemas](app-insights-troubleshoot-faq.md)


