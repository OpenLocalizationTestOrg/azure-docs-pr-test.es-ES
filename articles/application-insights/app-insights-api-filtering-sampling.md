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
# <a name="filtering-and-preprocessing-telemetry-in-hello-application-insights-sdk"></a><span data-ttu-id="312cb-103">Filtrado y preprocesamiento telemetría en hello Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="312cb-103">Filtering and preprocessing telemetry in hello Application Insights SDK</span></span>


<span data-ttu-id="312cb-104">Puede escribir y configurar complementos para hello Application Insights SDK toocustomize cómo telemetría se capturan y se procesa antes de enviarlo toohello servicio Application Insights.</span><span class="sxs-lookup"><span data-stu-id="312cb-104">You can write and configure plug-ins for hello Application Insights SDK toocustomize how telemetry is captured and processed before it is sent toohello Application Insights service.</span></span>

* <span data-ttu-id="312cb-105">[Muestreo](app-insights-sampling.md) reduce el volumen de Hola de telemetría sin que afecte a las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="312cb-105">[Sampling](app-insights-sampling.md) reduces hello volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="312cb-106">Mantiene juntos los puntos de datos relacionados para que pueda navegar entre ellos a la hora de diagnosticar un problema.</span><span class="sxs-lookup"><span data-stu-id="312cb-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="312cb-107">En el portal de hello, recuentos totales de hello son toocompensate multiplicada para el muestreo de Hola.</span><span class="sxs-lookup"><span data-stu-id="312cb-107">In hello portal, hello total counts are multiplied toocompensate for hello sampling.</span></span>
* <span data-ttu-id="312cb-108">Filtrar con procesadores de telemetría [para ASP.NET](#filtering) o [Java](app-insights-java-filter-telemetry.md) le permite seleccionar o modificar la telemetría en hello SDK antes de enviarlo toohello server.</span><span class="sxs-lookup"><span data-stu-id="312cb-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in hello SDK before it is sent toohello server.</span></span> <span data-ttu-id="312cb-109">Por ejemplo, podría reducir el volumen de Hola de telemetría mediante la exclusión de las solicitudes de robots.</span><span class="sxs-lookup"><span data-stu-id="312cb-109">For example, you could reduce hello volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="312cb-110">Pero el filtrado es un tráfico de tooreducing enfoque más básico que el muestreo.</span><span class="sxs-lookup"><span data-stu-id="312cb-110">But filtering is a more basic approach tooreducing traffic than sampling.</span></span> <span data-ttu-id="312cb-111">Permite más control sobre lo que se transmite, pero tienes toobe tenga en cuenta que afectará a las estadísticas: por ejemplo, si se filtran todas las solicitudes correctas.</span><span class="sxs-lookup"><span data-stu-id="312cb-111">It allows you more control over what is transmitted, but you have toobe aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="312cb-112">[Inicializadores de telemetría agregar propiedades](#add-properties) telemetría tooany enviado desde su aplicación, incluida la telemetría de los módulos estándares Hola.</span><span class="sxs-lookup"><span data-stu-id="312cb-112">[Telemetry Initializers add properties](#add-properties) tooany telemetry sent from your app, including telemetry from hello standard modules.</span></span> <span data-ttu-id="312cb-113">Por ejemplo, podría agregar valores calculados; números de versión según las cuales toofilter hello en el portal de Hola o.</span><span class="sxs-lookup"><span data-stu-id="312cb-113">For example, you could add calculated values; or version numbers by which toofilter hello data in hello portal.</span></span>
* <span data-ttu-id="312cb-114">[la API del SDK de Hello](app-insights-api-custom-events-metrics.md) es toosend usado los eventos personalizados y las métricas.</span><span class="sxs-lookup"><span data-stu-id="312cb-114">[hello SDK API](app-insights-api-custom-events-metrics.md) is used toosend custom events and metrics.</span></span>

<span data-ttu-id="312cb-115">Antes de comenzar:</span><span class="sxs-lookup"><span data-stu-id="312cb-115">Before you start:</span></span>

* <span data-ttu-id="312cb-116">Instalar Hola Application Insights [SDK para ASP.NET](app-insights-asp-net.md) o [SDK para Java](app-insights-java-get-started.md) en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="312cb-116">Install hello Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="312cb-117">Filtrado: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="312cb-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="312cb-118">Esta técnica proporciona un control más directo sobre lo que se incluirán o excluirán de la secuencia de telemetría de Hola.</span><span class="sxs-lookup"><span data-stu-id="312cb-118">This technique gives you more direct control over what is included or excluded from hello telemetry stream.</span></span> <span data-ttu-id="312cb-119">Se puede utilizar junto con el muestreo o por separado.</span><span class="sxs-lookup"><span data-stu-id="312cb-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="312cb-120">telemetría toofilter, escribir un procesador de telemetría y registrarlo con hello SDK.</span><span class="sxs-lookup"><span data-stu-id="312cb-120">toofilter telemetry, you write a telemetry processor and register it with hello SDK.</span></span> <span data-ttu-id="312cb-121">Telemetría todos pasa por el procesador y puede elegir toodrop desde Hola transmitir por secuencias o agregar propiedades.</span><span class="sxs-lookup"><span data-stu-id="312cb-121">All telemetry goes through your processor, and you can choose toodrop it from hello stream, or add properties.</span></span> <span data-ttu-id="312cb-122">Esto incluye la telemetría de los módulos estándares como recopilador de solicitud HTTP de Hola y el recopilador de dependencia de Hola Hola, así como la telemetría que haya escrito usted mismo.</span><span class="sxs-lookup"><span data-stu-id="312cb-122">This includes telemetry from hello standard modules such as hello HTTP request collector and hello dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="312cb-123">Por ejemplo, puede filtrar para dejar fuera la telemetría acerca de las solicitudes de robots o las llamadas de dependencia correctas.</span><span class="sxs-lookup"><span data-stu-id="312cb-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="312cb-124">Filtrado telemetría Hola enviado desde Hola SDK utilizan procesadores puede sesgar las estadísticas que se produzcan en el portal de hello y que sea difícil toofollow de Hola de elementos relacionados.</span><span class="sxs-lookup"><span data-stu-id="312cb-124">Filtering hello telemetry sent from hello SDK using processors can skew hello statistics that you see in hello portal, and make it difficult toofollow related items.</span></span>
>
> <span data-ttu-id="312cb-125">En su lugar, puede efectuar un [muestreo](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="312cb-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="312cb-126">Creación de un procesador de telemetría (C#)</span><span class="sxs-lookup"><span data-stu-id="312cb-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="312cb-127">Compruebe que Application Insights SDK hello en el proyecto es la versión 2.0.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="312cb-127">Verify that hello Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="312cb-128">Haga clic con el botón derecho en el proyecto en el Explorador de soluciones de Visual Studio y elija Administrar paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="312cb-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="312cb-129">En el Administrador de paquetes NuGet, compruebe Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="312cb-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="312cb-130">toocreate un filtro, implemente ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="312cb-130">toocreate a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="312cb-131">Se trata de otro punto de extensibilidad como el módulo de telemetría, el inicializador de telemetría y el canal de telemetría.</span><span class="sxs-lookup"><span data-stu-id="312cb-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="312cb-132">Observe que los procesadores de telemetría forman una cadena de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="312cb-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="312cb-133">Cuando crea una instancia de un procesador de telemetría, pasar un procesador siguiente toohello de vínculo en la cadena de Hola.</span><span class="sxs-lookup"><span data-stu-id="312cb-133">When you instantiate a telemetry processor, you pass a link toohello next processor in hello chain.</span></span> <span data-ttu-id="312cb-134">Cuando un punto de datos de telemetría se pasa el método de proceso toohello, que realiza su trabajo y, a continuación, llamadas Hola siguiente procesador de telemetría en cadena Hola.</span><span class="sxs-lookup"><span data-stu-id="312cb-134">When a telemetry data point is passed toohello Process method, it does its work and then calls hello next Telemetry Processor in hello chain.</span></span>

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
1. <span data-ttu-id="312cb-135">Inserte esto en ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="312cb-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="312cb-136">(Esto es hello misma sección donde se inicializa un filtro de muestreo.)</span><span class="sxs-lookup"><span data-stu-id="312cb-136">(This is hello same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="312cb-137">Puede pasar valores de cadena del archivo .config de hello proporcionando las propiedades públicas con nombre en la clase.</span><span class="sxs-lookup"><span data-stu-id="312cb-137">You can pass string values from hello .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="312cb-138">Tenga cuidado de nombre de tipo hello toomatch y los nombres de propiedad de clase de hello config file toohello y nombres de propiedad en el código de hello.</span><span class="sxs-lookup"><span data-stu-id="312cb-138">Take care toomatch hello type name and any property names in hello .config file toohello class and property names in hello code.</span></span> <span data-ttu-id="312cb-139">Si el archivo .config de hello hace referencia a un tipo no existente o una propiedad, Hola SDK en modo silencioso producirán toosend cualquier telemetría.</span><span class="sxs-lookup"><span data-stu-id="312cb-139">If hello .config file references a non-existent type or property, hello SDK may silently fail toosend any telemetry.</span></span>
>
>

<span data-ttu-id="312cb-140">**O bien,** se puede inicializar el filtro de hello en el código.</span><span class="sxs-lookup"><span data-stu-id="312cb-140">**Alternatively,** you can initialize hello filter in code.</span></span> <span data-ttu-id="312cb-141">En una clase de inicialización adecuado - por ejemplo AppStart en Global.asax.cs - insertar un procesador en cadena hello:</span><span class="sxs-lookup"><span data-stu-id="312cb-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into hello chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="312cb-142">Los TelemetryClients creados a partir de este punto usarán sus procesadores.</span><span class="sxs-lookup"><span data-stu-id="312cb-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="312cb-143">Filtros de ejemplo</span><span class="sxs-lookup"><span data-stu-id="312cb-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="312cb-144">Solicitudes sintéticas</span><span class="sxs-lookup"><span data-stu-id="312cb-144">Synthetic requests</span></span>
<span data-ttu-id="312cb-145">Filtrar las pruebas web y robots.</span><span class="sxs-lookup"><span data-stu-id="312cb-145">Filter out bots and web tests.</span></span> <span data-ttu-id="312cb-146">Aunque el Explorador de métricas ofrece Hola toofilter opción orígenes sintético, esta opción reduce el tráfico filtrando en hello SDK.</span><span class="sxs-lookup"><span data-stu-id="312cb-146">Although Metrics Explorer gives you hello option toofilter out synthetic sources, this option reduces traffic by filtering them at hello SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="312cb-147">Error de autenticación</span><span class="sxs-lookup"><span data-stu-id="312cb-147">Failed authentication</span></span>
<span data-ttu-id="312cb-148">Filtrar solicitudes con una respuesta "401".</span><span class="sxs-lookup"><span data-stu-id="312cb-148">Filter out requests with a "401" response.</span></span>

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

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="312cb-149">Filtrar las llamadas de dependencia rápida y remota</span><span class="sxs-lookup"><span data-stu-id="312cb-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="312cb-150">Si solo desea llamadas toodiagnose que son lentas, filtrar Hola fast los.</span><span class="sxs-lookup"><span data-stu-id="312cb-150">If you only want toodiagnose calls that are slow, filter out hello fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="312cb-151">Esto sesga las estadísticas de Hola que se ven en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="312cb-151">This will skew hello statistics you see on hello portal.</span></span> <span data-ttu-id="312cb-152">gráfico de dependencia de Hello será como si las llamadas de dependencia de hello son todos los errores.</span><span class="sxs-lookup"><span data-stu-id="312cb-152">hello dependency chart will look as if hello dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="312cb-153">Diagnóstico de problemas de dependencia</span><span class="sxs-lookup"><span data-stu-id="312cb-153">Diagnose dependency issues</span></span>
<span data-ttu-id="312cb-154">[Este blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describe un problemas de dependencia de proyecto toodiagnose enviando automáticamente toodependencies pings regular.</span><span class="sxs-lookup"><span data-stu-id="312cb-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project toodiagnose dependency issues by automatically sending regular pings toodependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="312cb-155">Agregar propiedades: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="312cb-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="312cb-156">Usar la telemetría inicializadores toodefine propiedades globales que se envían con la telemetría todos; y el comportamiento de toooverride seleccionada de módulos de hello telemetría estándar.</span><span class="sxs-lookup"><span data-stu-id="312cb-156">Use telemetry initializers toodefine global properties that are sent with all telemetry; and toooverride selected behavior of hello standard telemetry modules.</span></span>

<span data-ttu-id="312cb-157">Por ejemplo, hello Application Insights para paquete de Web recopila telemetría acerca de las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="312cb-157">For example, hello Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="312cb-158">De forma predeterminada, marca como errónea cualquier solicitud con un código de respuesta >= 400.</span><span class="sxs-lookup"><span data-stu-id="312cb-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="312cb-159">Pero si desea tootreat 400 como tales, puede proporcionar a un inicializador de telemetría que establece la propiedad de corrección de Hola.</span><span class="sxs-lookup"><span data-stu-id="312cb-159">But if you want tootreat 400 as a success, you can provide a telemetry initializer that sets hello Success property.</span></span>

<span data-ttu-id="312cb-160">Si se proporciona un inicializador de telemetría, se llama cada vez que cualquiera de Hola Track*() se llama a métodos.</span><span class="sxs-lookup"><span data-stu-id="312cb-160">If you provide a telemetry initializer, it is called whenever any of hello Track*() methods is called.</span></span> <span data-ttu-id="312cb-161">Esto incluye los métodos llamados por los módulos de hello telemetría estándar.</span><span class="sxs-lookup"><span data-stu-id="312cb-161">This includes methods called by hello standard telemetry modules.</span></span> <span data-ttu-id="312cb-162">Por convención, estos módulos no establecen ninguna propiedad que ya haya sido establecida por un inicializador.</span><span class="sxs-lookup"><span data-stu-id="312cb-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="312cb-163">**Defina su inicializador**</span><span class="sxs-lookup"><span data-stu-id="312cb-163">**Define your initializer**</span></span>

<span data-ttu-id="312cb-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="312cb-164">*C#*</span></span>

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

<span data-ttu-id="312cb-165">**Cargue su inicializador**</span><span class="sxs-lookup"><span data-stu-id="312cb-165">**Load your initializer**</span></span>

<span data-ttu-id="312cb-166">En ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="312cb-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="312cb-167">*O bien,* puede crear instancias de inicializador de hello en el código, por ejemplo, en Global.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="312cb-167">*Alternatively,* you can instantiate hello initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="312cb-168">Obtenga más información de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="312cb-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="312cb-169">Inicializadores de telemetría de JavaScript</span><span class="sxs-lookup"><span data-stu-id="312cb-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="312cb-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="312cb-170">*JavaScript*</span></span>

<span data-ttu-id="312cb-171">Insertar a un inicializador de telemetría inmediatamente después de código de inicialización de Hola que obtuvo en el portal de hello:</span><span class="sxs-lookup"><span data-stu-id="312cb-171">Insert a telemetry initializer immediately after hello initialization code that you got from hello portal:</span></span>

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

<span data-ttu-id="312cb-172">Para obtener un resumen de las propiedades de no personalizado de hello disponibles en hello telemetryItem, consulte [modelo de datos de exportación de aplicación visión](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="312cb-172">For a summary of hello non-custom properties available on hello telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="312cb-173">Puede agregar tantos inicializadores como desee.</span><span class="sxs-lookup"><span data-stu-id="312cb-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="312cb-174">ITelemetryProcessor e ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="312cb-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="312cb-175">¿Cuál es la diferencia de hello entre procesadores de telemetría y los inicializadores de telemetría?</span><span class="sxs-lookup"><span data-stu-id="312cb-175">What's hello difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="312cb-176">Hay algunos superposiciones en lo que puede hacer con ellos: ambos pueden ser utilizados tooadd propiedades tootelemetry.</span><span class="sxs-lookup"><span data-stu-id="312cb-176">There are some overlaps in what you can do with them: both can be used tooadd properties tootelemetry.</span></span>
* <span data-ttu-id="312cb-177">Siempre se ejecutan los objetos TelemetryInitializer antes que los objetos TelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="312cb-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="312cb-178">TelemetryProcessors permiten toocompletely reemplazar o descartar un elemento de telemetría.</span><span class="sxs-lookup"><span data-stu-id="312cb-178">TelemetryProcessors allow you toocompletely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="312cb-179">Los objetos TelemetryProcessor no procesan telemetría de contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="312cb-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="312cb-180">Documentos de referencia</span><span class="sxs-lookup"><span data-stu-id="312cb-180">Reference docs</span></span>
* [<span data-ttu-id="312cb-181">Información general acerca de la API</span><span class="sxs-lookup"><span data-stu-id="312cb-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="312cb-182">Referencia de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="312cb-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="312cb-183">Código del SDK</span><span class="sxs-lookup"><span data-stu-id="312cb-183">SDK Code</span></span>
* [<span data-ttu-id="312cb-184">SDK básico de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="312cb-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="312cb-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="312cb-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="312cb-186">SDK de JavaScript</span><span class="sxs-lookup"><span data-stu-id="312cb-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="312cb-187"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="312cb-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="312cb-188">Búsqueda de eventos y registros</span><span class="sxs-lookup"><span data-stu-id="312cb-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="312cb-189">Muestreo</span><span class="sxs-lookup"><span data-stu-id="312cb-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="312cb-190">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="312cb-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
