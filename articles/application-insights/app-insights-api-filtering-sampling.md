---
title: aaaFiltering y preprocesamiento en hello Azure Application Insights SDK | Documentos de Microsoft
description: "Escribir procesadores de telemetría y los inicializadores de telemetría Hola SDK toofilter o agregar datos de propiedades toohello antes de telemetría de Hola se envía el portal de Application Insights toohello."
services: application-insights
documentationcenter: 
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: bwren
ms.openlocfilehash: 51b9db69b2375b8799718f1b0e1af77620dc2692
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a>Filtrado y preprocesamiento telemetría en hello Application Insights SDK


Puede escribir y configurar complementos para hello Application Insights SDK toocustomize cómo telemetría se capturan y se procesa antes de enviarlo toohello servicio Application Insights.

* [Muestreo](app-insights-sampling.md) reduce el volumen de Hola de telemetría sin que afecte a las estadísticas. Mantiene juntos los puntos de datos relacionados para que pueda navegar entre ellos a la hora de diagnosticar un problema. En el portal de hello, recuentos totales de hello son toocompensate multiplicada para el muestreo de Hola.
* Filtrar con procesadores de telemetría [para ASP.NET](#filtering) o [Java](app-insights-java-filter-telemetry.md) le permite seleccionar o modificar la telemetría en hello SDK antes de enviarlo toohello server. Por ejemplo, podría reducir el volumen de Hola de telemetría mediante la exclusión de las solicitudes de robots. Pero el filtrado es un tráfico de tooreducing enfoque más básico que el muestreo. Permite más control sobre lo que se transmite, pero tienes toobe tenga en cuenta que afectará a las estadísticas: por ejemplo, si se filtran todas las solicitudes correctas.
* [Inicializadores de telemetría agregar propiedades](#add-properties) telemetría tooany enviado desde su aplicación, incluida la telemetría de los módulos estándares Hola. Por ejemplo, podría agregar valores calculados; números de versión según las cuales toofilter hello en el portal de Hola o.
* [la API del SDK de Hello](app-insights-api-custom-events-metrics.md) es toosend usado los eventos personalizados y las métricas.

Antes de comenzar:

* Instalar Hola Application Insights [SDK para ASP.NET](app-insights-asp-net.md) o [SDK para Java](app-insights-java-get-started.md) en la aplicación.

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a>Filtrado: ITelemetryProcessor
Esta técnica proporciona un control más directo sobre lo que se incluirán o excluirán de la secuencia de telemetría de Hola. Se puede utilizar junto con el muestreo o por separado.

telemetría toofilter, escribir un procesador de telemetría y registrarlo con hello SDK. Telemetría todos pasa por el procesador y puede elegir toodrop desde Hola transmitir por secuencias o agregar propiedades. Esto incluye la telemetría de los módulos estándares como recopilador de solicitud HTTP de Hola y el recopilador de dependencia de Hola Hola, así como la telemetría que haya escrito usted mismo. Por ejemplo, puede filtrar para dejar fuera la telemetría acerca de las solicitudes de robots o las llamadas de dependencia correctas.

> [!WARNING]
> Filtrado telemetría Hola enviado desde Hola SDK utilizan procesadores puede sesgar las estadísticas que se produzcan en el portal de hello y que sea difícil toofollow de Hola de elementos relacionados.
>
> En su lugar, puede efectuar un [muestreo](app-insights-sampling.md).
>
>

### <a name="create-a-telemetry-processor-c"></a>Creación de un procesador de telemetría (C#)
1. Compruebe que Application Insights SDK hello en el proyecto es la versión 2.0.0 o posterior. Haga clic con el botón derecho en el proyecto en el Explorador de soluciones de Visual Studio y elija Administrar paquetes de NuGet. En el Administrador de paquetes NuGet, compruebe Microsoft.ApplicationInsights.Web.
2. toocreate un filtro, implemente ITelemetryProcessor. Se trata de otro punto de extensibilidad como el módulo de telemetría, el inicializador de telemetría y el canal de telemetría.

    Observe que los procesadores de telemetría forman una cadena de procesamiento. Cuando crea una instancia de un procesador de telemetría, pasar un procesador siguiente toohello de vínculo en la cadena de Hola. Cuando un punto de datos de telemetría se pasa el método de proceso toohello, que realiza su trabajo y, a continuación, llamadas Hola siguiente procesador de telemetría en cadena Hola.

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors tooeach other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // toofilter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify hello item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. Inserte esto en ApplicationInsights.config:

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

(Esto es hello misma sección donde se inicializa un filtro de muestreo.)

Puede pasar valores de cadena del archivo .config de hello proporcionando las propiedades públicas con nombre en la clase.

> [!WARNING]
> Tenga cuidado de nombre de tipo hello toomatch y los nombres de propiedad de clase de hello config file toohello y nombres de propiedad en el código de hello. Si el archivo .config de hello hace referencia a un tipo no existente o una propiedad, Hola SDK en modo silencioso producirán toosend cualquier telemetría.
>
>

**O bien,** se puede inicializar el filtro de hello en el código. En una clase de inicialización adecuado - por ejemplo AppStart en Global.asax.cs - insertar un procesador en cadena hello:

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

Los TelemetryClients creados a partir de este punto usarán sus procesadores.

### <a name="example-filters"></a>Filtros de ejemplo
#### <a name="synthetic-requests"></a>Solicitudes sintéticas
Filtrar las pruebas web y robots. Aunque el Explorador de métricas ofrece Hola toofilter opción orígenes sintético, esta opción reduce el tráfico filtrando en hello SDK.

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a>Error de autenticación
Filtrar solicitudes con una respuesta "401".

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // toofilter out an item, just terminate hello chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a>Filtrar las llamadas de dependencia rápida y remota
Si solo desea llamadas toodiagnose que son lentas, filtrar Hola fast los.

> [!NOTE]
> Esto sesga las estadísticas de Hola que se ven en el portal de Hola. gráfico de dependencia de Hello será como si las llamadas de dependencia de hello son todos los errores.
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a>Diagnóstico de problemas de dependencia
[Este blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describe un problemas de dependencia de proyecto toodiagnose enviando automáticamente toodependencies pings regular.


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a>Agregar propiedades: ITelemetryInitializer
Usar la telemetría inicializadores toodefine propiedades globales que se envían con la telemetría todos; y el comportamiento de toooverride seleccionada de módulos de hello telemetría estándar.

Por ejemplo, hello Application Insights para paquete de Web recopila telemetría acerca de las solicitudes HTTP. De forma predeterminada, marca como errónea cualquier solicitud con un código de respuesta >= 400. Pero si desea tootreat 400 como tales, puede proporcionar a un inicializador de telemetría que establece la propiedad de corrección de Hola.

Si se proporciona un inicializador de telemetría, se llama cada vez que cualquiera de Hola Track*() se llama a métodos. Esto incluye los métodos llamados por los módulos de hello telemetría estándar. Por convención, estos módulos no establecen ninguna propiedad que ya haya sido establecida por un inicializador.

**Defina su inicializador**

*C#*

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides hello default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set hello Success property, hello SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us toofilter these requests in hello portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave hello SDK tooset hello Success property      
        }
      }
    }
```

**Cargue su inicializador**

En ApplicationInsights.config:

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

*O bien,* puede crear instancias de inicializador de hello en el código, por ejemplo, en Global.aspx.cs:

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[Obtenga más información de este ejemplo.](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a>Inicializadores de telemetría de JavaScript
*JavaScript*

Insertar a un inicializador de telemetría inmediatamente después de código de inicialización de Hola que obtuvo en el portal de hello:

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // toocheck hello telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // tooset custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // tooset custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

Para obtener un resumen de las propiedades de no personalizado de hello disponibles en hello telemetryItem, consulte [modelo de datos de exportación de aplicación visión](app-insights-export-data-model.md).

Puede agregar tantos inicializadores como desee.

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a>ITelemetryProcessor e ITelemetryInitializer
¿Cuál es la diferencia de hello entre procesadores de telemetría y los inicializadores de telemetría?

* Hay algunos superposiciones en lo que puede hacer con ellos: ambos pueden ser utilizados tooadd propiedades tootelemetry.
* Siempre se ejecutan los objetos TelemetryInitializer antes que los objetos TelemetryProcessor.
* TelemetryProcessors permiten toocompletely reemplazar o descartar un elemento de telemetría.
* Los objetos TelemetryProcessor no procesan telemetría de contador de rendimiento.


## <a name="reference-docs"></a>Documentos de referencia
* [Información general acerca de la API](app-insights-api-custom-events-metrics.md)
* [Referencia de ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a>Código del SDK
* [SDK básico de ASP.NET](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [SDK de JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a>Pasos siguientes
* [Búsqueda de eventos y registros](app-insights-diagnostic-search.md)
* [Muestreo](app-insights-sampling.md)
* [Solución de problemas](app-insights-troubleshoot-faq.md)
