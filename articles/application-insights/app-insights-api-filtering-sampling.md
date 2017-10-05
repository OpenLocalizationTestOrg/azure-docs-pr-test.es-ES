---
title: Filtrado y preprocesamiento en el SDK de Azure Application Insights | Microsoft Docs
description: "Escriba procesadores e inicializadores de telemetría para que el SDK filtre o agregue propiedades a los datos antes de enviar la telemetría al portal de Application Insights."
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
ms.openlocfilehash: 17e66775dd2cd1c858594102f1ddb32e2fbbccc8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="filtering-and-preprocessing-telemetry-in-the-application-insights-sdk"></a><span data-ttu-id="7a4fc-103">Filtro y preprocesamiento de la telemetría en el SDK de Application Insights</span><span class="sxs-lookup"><span data-stu-id="7a4fc-103">Filtering and preprocessing telemetry in the Application Insights SDK</span></span>


<span data-ttu-id="7a4fc-104">Puede escribir y configurar complementos para el SDK de Application Insights con el fin de personalizar cómo se captura y se procesa la telemetría antes de enviarla al servicio de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span></span>

* <span data-ttu-id="7a4fc-105">[muestreo](app-insights-sampling.md) reduce el volumen de la telemetría sin que ello influya en las estadísticas.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="7a4fc-106">Mantiene juntos los puntos de datos relacionados para que pueda navegar entre ellos a la hora de diagnosticar un problema.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="7a4fc-107">En el portal, se multiplican los recuentos totales para compensar el muestreo.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-107">In the portal, the total counts are multiplied to compensate for the sampling.</span></span>
* <span data-ttu-id="7a4fc-108">El filtrado con procesadores de telemetría [para ASP.NET](#filtering) o [Java](app-insights-java-filter-telemetry.md) permite seleccionar o modificar la telemetría en el SDK antes de enviarla al servidor.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span></span> <span data-ttu-id="7a4fc-109">Por ejemplo, para reducir el volumen de la telemetría puede excluir las solicitudes de robots.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="7a4fc-110">Sin embargo, el filtro constituye un enfoque más básico que el muestreo para reducir el tráfico.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-110">But filtering is a more basic approach to reducing traffic than sampling.</span></span> <span data-ttu-id="7a4fc-111">Permite ejercer más control sobre lo que se transmite, pero debe tener en cuenta que se verán afectadas las estadísticas: por ejemplo, si filtra todas las solicitudes correctas.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="7a4fc-112">[inicializadores de telemetría agregan propiedades](#add-properties) a cualquier telemetría enviada desde la aplicación, incluida la de los módulos estándar.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span></span> <span data-ttu-id="7a4fc-113">Por ejemplo, puede agregar valores calculados o números de versión para filtrar los datos en el portal.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span></span>
* <span data-ttu-id="7a4fc-114">[API del SDK](app-insights-api-custom-events-metrics.md) se usa para enviar métricas y eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span></span>

<span data-ttu-id="7a4fc-115">Antes de comenzar:</span><span class="sxs-lookup"><span data-stu-id="7a4fc-115">Before you start:</span></span>

* <span data-ttu-id="7a4fc-116">Instale el [SDK de Application Insights para ASP.NET](app-insights-asp-net.md) o [SDK para Java](app-insights-java-get-started.md) en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="7a4fc-117">Filtrado: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="7a4fc-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="7a4fc-118">Esta técnica le ofrece un control más directo sobre lo que se incluirá en la transmisión de telemetría o lo que se excluirá de ella.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span></span> <span data-ttu-id="7a4fc-119">Se puede utilizar junto con el muestreo o por separado.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="7a4fc-120">Para filtrar la telemetría, escriba un procesador de telemetría y regístrelo con el SDK.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span></span> <span data-ttu-id="7a4fc-121">Toda la telemetría pasa por el procesador. Puede optar por no incluirlo en la transmisión o por agregar propiedades.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span></span> <span data-ttu-id="7a4fc-122">Esto incluye la telemetría de los módulos estándar como el recopilador de solicitudes HTTP y el recopilador de dependencia, así como la telemetría que haya escrito.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="7a4fc-123">Por ejemplo, puede filtrar para dejar fuera la telemetría acerca de las solicitudes de robots o las llamadas de dependencia correctas.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="7a4fc-124">El filtrado de la telemetría enviada desde el SDK usando procesadores puede sesgar las estadísticas que se ven en el portal, y dificultar el seguimiento de elementos relacionados.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span></span>
>
> <span data-ttu-id="7a4fc-125">En su lugar, puede efectuar un [muestreo](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="7a4fc-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="7a4fc-126">Creación de un procesador de telemetría (C#)</span><span class="sxs-lookup"><span data-stu-id="7a4fc-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="7a4fc-127">Compruebe que la versión del SDK de Application Insights de su proyecto es la versión 2.0.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="7a4fc-128">Haga clic con el botón derecho en el proyecto en el Explorador de soluciones de Visual Studio y elija Administrar paquetes de NuGet.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="7a4fc-129">En el Administrador de paquetes NuGet, compruebe Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="7a4fc-130">Para crear un filtro, implemente ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-130">To create a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="7a4fc-131">Se trata de otro punto de extensibilidad como el módulo de telemetría, el inicializador de telemetría y el canal de telemetría.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="7a4fc-132">Observe que los procesadores de telemetría forman una cadena de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="7a4fc-133">Al crear instancias de un procesador de telemetría, se pasa un vínculo al procesador siguiente en la cadena.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span></span> <span data-ttu-id="7a4fc-134">Cuando un punto de datos de telemetría se pasa al método de proceso, realiza su trabajo y, a continuación, llama al procesador de telemetría siguiente de la cadena.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors to each other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // To filter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify the item if required
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
1. <span data-ttu-id="7a4fc-135">Inserte esto en ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="7a4fc-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="7a4fc-136">(Se trata de la misma sección donde inicializa un filtro de muestreo).</span><span class="sxs-lookup"><span data-stu-id="7a4fc-136">(This is the same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="7a4fc-137">Puede pasar valores de cadena desde el archivo .config proporcionando propiedades con nombre públicas en la clase.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-137">You can pass string values from the .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="7a4fc-138">Tenga cuidado para que el nombre de tipo y los nombres de propiedad del archivo .config coincidan con los nombres de clase y propiedad del código.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span></span> <span data-ttu-id="7a4fc-139">Si el archivo .config hace referencia a un tipo o propiedad que no existe, el SDK puede producir un error de forma silenciosa al enviar cualquier telemetría.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span></span>
>
>

<span data-ttu-id="7a4fc-140">**Alternativamente,** se puede inicializar el filtro en el código.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-140">**Alternatively,** you can initialize the filter in code.</span></span> <span data-ttu-id="7a4fc-141">En una clase de inicialización adecuada (por ejemplo AppStart de Global.asax.cs) inserte el procesador en la cadena:</span><span class="sxs-lookup"><span data-stu-id="7a4fc-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="7a4fc-142">Los TelemetryClients creados a partir de este punto usarán sus procesadores.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="7a4fc-143">Filtros de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7a4fc-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="7a4fc-144">Solicitudes sintéticas</span><span class="sxs-lookup"><span data-stu-id="7a4fc-144">Synthetic requests</span></span>
<span data-ttu-id="7a4fc-145">Filtrar las pruebas web y robots.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-145">Filter out bots and web tests.</span></span> <span data-ttu-id="7a4fc-146">Aunque el Explorador de métricas proporciona la opción para filtrar y dejar fuera los orígenes sintéticos, esta opción reduce el tráfico filtrándolos en el SDK.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="7a4fc-147">Error de autenticación</span><span class="sxs-lookup"><span data-stu-id="7a4fc-147">Failed authentication</span></span>
<span data-ttu-id="7a4fc-148">Filtrar solicitudes con una respuesta "401".</span><span class="sxs-lookup"><span data-stu-id="7a4fc-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // To filter out an item, just terminate the chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="7a4fc-149">Filtrar las llamadas de dependencia rápida y remota</span><span class="sxs-lookup"><span data-stu-id="7a4fc-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="7a4fc-150">Si solo desea diagnosticar las llamadas que son lentas, descarte las rápidas.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="7a4fc-151">Esto sesgará las estadísticas que se ve en el portal.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-151">This will skew the statistics you see on the portal.</span></span> <span data-ttu-id="7a4fc-152">El gráfico de dependencias será como si las llamadas de dependencia fuesen todos errores.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-152">The dependency chart will look as if the dependency calls are all failures.</span></span>
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

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="7a4fc-153">Diagnóstico de problemas de dependencia</span><span class="sxs-lookup"><span data-stu-id="7a4fc-153">Diagnose dependency issues</span></span>
<span data-ttu-id="7a4fc-154">[este blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) se describe un proyecto para diagnosticar problemas de dependencia enviando automáticamente pings regulares a las dependencias.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="7a4fc-155">Agregar propiedades: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="7a4fc-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="7a4fc-156">Use inicializadores de telemetría para definir las propiedades globales que se envían con toda la telemetría; y para invalidar el comportamiento seleccionado de los módulos de telemetría estándar.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span></span>

<span data-ttu-id="7a4fc-157">Por ejemplo, para el paquete Application Insights para web recopila telemetría acerca de las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="7a4fc-158">De forma predeterminada, marca como errónea cualquier solicitud con un código de respuesta >= 400.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="7a4fc-159">Pero si desea tratar 400 como correcto, puede proporcionar un inicializador de telemetría que establezca la propiedad Éxito.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span></span>

<span data-ttu-id="7a4fc-160">Si se proporciona un inicializador de telemetría, se llama cada vez que se llama a cualquiera de los métodos Track*().</span><span class="sxs-lookup"><span data-stu-id="7a4fc-160">If you provide a telemetry initializer, it is called whenever any of the Track*() methods is called.</span></span> <span data-ttu-id="7a4fc-161">Esto incluye los métodos llamados por los módulos de telemetría estándar.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-161">This includes methods called by the standard telemetry modules.</span></span> <span data-ttu-id="7a4fc-162">Por convención, estos módulos no establecen ninguna propiedad que ya haya sido establecida por un inicializador.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="7a4fc-163">**Defina su inicializador**</span><span class="sxs-lookup"><span data-stu-id="7a4fc-163">**Define your initializer**</span></span>

<span data-ttu-id="7a4fc-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="7a4fc-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides the default SDK
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
                // If we set the Success property, the SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us to filter these requests in the portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave the SDK to set the Success property      
        }
      }
    }
```

<span data-ttu-id="7a4fc-165">**Cargue su inicializador**</span><span class="sxs-lookup"><span data-stu-id="7a4fc-165">**Load your initializer**</span></span>

<span data-ttu-id="7a4fc-166">En ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="7a4fc-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="7a4fc-167">*Alternativamente,* se pueden crear instancias del inicializador en el código, por ejemplo en Global.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="7a4fc-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="7a4fc-168">Obtenga más información de este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="7a4fc-169">Inicializadores de telemetría de JavaScript</span><span class="sxs-lookup"><span data-stu-id="7a4fc-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="7a4fc-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="7a4fc-170">*JavaScript*</span></span>

<span data-ttu-id="7a4fc-171">Inserte un inicializador de telemetría inmediatamente después del código de inicialización que obtuvo del portal:</span><span class="sxs-lookup"><span data-stu-id="7a4fc-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span></span>

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

                // To check the telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // To set custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // To set custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="7a4fc-172">Para obtener un resumen de las propiedades no personalizadas disponibles en telemetryItem, consulte [Modelo de exportación de datos de Application Insights](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="7a4fc-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="7a4fc-173">Puede agregar tantos inicializadores como desee.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="7a4fc-174">ITelemetryProcessor e ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="7a4fc-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="7a4fc-175">¿Cuál es la diferencia entre los procesadores de telemetría y los inicializadores de telemetría?</span><span class="sxs-lookup"><span data-stu-id="7a4fc-175">What's the difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="7a4fc-176">Coinciden en algunas funciones: ambos se pueden utilizar para agregar propiedades a una telemetría.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span></span>
* <span data-ttu-id="7a4fc-177">Siempre se ejecutan los objetos TelemetryInitializer antes que los objetos TelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="7a4fc-178">Los objetos TelemetryProcessor permiten reemplazar o descartar por completo un elemento de telemetría.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="7a4fc-179">Los objetos TelemetryProcessor no procesan telemetría de contador de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7a4fc-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="7a4fc-180">Documentos de referencia</span><span class="sxs-lookup"><span data-stu-id="7a4fc-180">Reference docs</span></span>
* [<span data-ttu-id="7a4fc-181">Información general acerca de la API</span><span class="sxs-lookup"><span data-stu-id="7a4fc-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="7a4fc-182">Referencia de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a4fc-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="7a4fc-183">Código del SDK</span><span class="sxs-lookup"><span data-stu-id="7a4fc-183">SDK Code</span></span>
* [<span data-ttu-id="7a4fc-184">SDK básico de ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7a4fc-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="7a4fc-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="7a4fc-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="7a4fc-186">SDK de JavaScript</span><span class="sxs-lookup"><span data-stu-id="7a4fc-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <span data-ttu-id="7a4fc-187"><a name="next"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7a4fc-187"><a name="next"></a>Next steps</span></span>
* [<span data-ttu-id="7a4fc-188">Búsqueda de eventos y registros</span><span class="sxs-lookup"><span data-stu-id="7a4fc-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="7a4fc-189">Muestreo</span><span class="sxs-lookup"><span data-stu-id="7a4fc-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="7a4fc-190">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="7a4fc-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
