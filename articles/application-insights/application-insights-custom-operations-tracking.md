---
title: "aaaTrack operaciones personalizadas con el SDK de .NET de visión de aplicación de Azure | Documentos de Microsoft"
description: Seguimiento de las operaciones personalizadas con el SDK de .NET de Azure Application Insights
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/31/2017
ms.author: sergkanz
ms.openlocfilehash: fe338d3e2b17a3dae43c96c60a19f57b3f46f0a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="8c390-103">Seguimiento de las operaciones personalizadas con el SDK de .NET para Application Insights</span><span class="sxs-lookup"><span data-stu-id="8c390-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="8c390-104">SDK de Azure Application Insights automáticamente pista solicitudes HTTP entrante y llama a toodependent servicios, como las solicitudes HTTP y las consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="8c390-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls toodependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="8c390-105">Seguimiento y correlación de las solicitudes y las dependencias de obtener una visibilidad en la capacidad de respuesta y la confiabilidad de la aplicación completa de Hola a través de todos los microservicios que combinan esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="8c390-105">Tracking and correlation of requests and dependencies give you visibility into hello whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="8c390-106">Hay una clase de patrones de aplicación que no se admiten de forma genérica.</span><span class="sxs-lookup"><span data-stu-id="8c390-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="8c390-107">La supervisión correcta de estos patrones requiere la instrumentación manual de código.</span><span class="sxs-lookup"><span data-stu-id="8c390-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="8c390-108">En este artículo se abordan algunos patrones que pueden requerir la instrumentación manual, como el procesamiento de colas personalizadas y la ejecución de tareas de larga duración en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="8c390-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="8c390-109">Este documento proporciona instrucciones sobre cómo tootrack operaciones personalizadas con Hola Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="8c390-109">This document provides guidance on how tootrack custom operations with hello Application Insights SDK.</span></span> <span data-ttu-id="8c390-110">Esta documentación es relevante para:</span><span class="sxs-lookup"><span data-stu-id="8c390-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="8c390-111">Application Insights para .NET (también conocido como Base SDK) versión 2.4+.</span><span class="sxs-lookup"><span data-stu-id="8c390-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="8c390-112">Application Insights para aplicaciones web (con ASP.NET) versión 2.4+.</span><span class="sxs-lookup"><span data-stu-id="8c390-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="8c390-113">Application Insights para ASP.NET Core versión 2.1+.</span><span class="sxs-lookup"><span data-stu-id="8c390-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="8c390-114">Información general</span><span class="sxs-lookup"><span data-stu-id="8c390-114">Overview</span></span>
<span data-ttu-id="8c390-115">Una operación es una parte de trabajo lógica ejecutada por una aplicación.</span><span class="sxs-lookup"><span data-stu-id="8c390-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="8c390-116">Tiene un nombre, una hora de inicio, una duración, un resultado y un contexto de ejecución como el nombre de usuario, las propiedades y el resultado.</span><span class="sxs-lookup"><span data-stu-id="8c390-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="8c390-117">Si la operación B inició la operación A, la operación B se establece como un elemento primario de A. Una operación solo puede tener un elemento primario, pero puede tener muchas operaciones secundarias.</span><span class="sxs-lookup"><span data-stu-id="8c390-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="8c390-118">Para más información sobre las operaciones y la correlación de telemetría, vea [Correlación de telemetría en Azure Application Insights](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="8c390-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="8c390-119">Hola Application Insights .NET SDK, la operación de Hola se describe mediante la clase abstracta de hello [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) y sus descendientes [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) y [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="8c390-119">In hello Application Insights .NET SDK, hello operation is described by hello abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="8c390-120">Seguimiento de operaciones de entrada</span><span class="sxs-lookup"><span data-stu-id="8c390-120">Incoming operations tracking</span></span> 
<span data-ttu-id="8c390-121">Hola web Application Insights que SDK recopila automáticamente las solicitudes HTTP de aplicaciones de ASP.NET que se ejecutan en una canalización IIS y todas las aplicaciones de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="8c390-121">hello Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="8c390-122">Hay soluciones admitidas por la comunidad para otras plataformas y marcos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="8c390-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="8c390-123">Sin embargo, si la aplicación hello no es compatible con cualquiera de estándar de Hola o soluciones admitido por la Comunidad, puede instrumentar en ella manualmente.</span><span class="sxs-lookup"><span data-stu-id="8c390-123">However, if hello application isn't supported by any of hello standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="8c390-124">Otro ejemplo que requiere seguimiento personalizado es trabajo Hola que recibe los elementos de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c390-124">Another example that requires custom tracking is hello worker that receives items from hello queue.</span></span> <span data-ttu-id="8c390-125">En algunas colas Hola llama a tooadd un mensaje a la cola de toothis se realiza un seguimiento como una dependencia.</span><span class="sxs-lookup"><span data-stu-id="8c390-125">For some queues, hello call tooadd a message toothis queue is tracked as a dependency.</span></span> <span data-ttu-id="8c390-126">Sin embargo, operaciones de nivel superior de Hola que describe el procesamiento de mensajes no se recopilan automáticamente.</span><span class="sxs-lookup"><span data-stu-id="8c390-126">However, hello high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="8c390-127">Veamos cómo se puede realizar el seguimiento de estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="8c390-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="8c390-128">En un nivel alto, la tarea hello es toocreate `RequestTelemetry` y establezca propiedades conocidas.</span><span class="sxs-lookup"><span data-stu-id="8c390-128">On a high level, hello task is toocreate `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="8c390-129">Una vez finalizada la operación de hello, realizar un seguimiento telemetría Hola.</span><span class="sxs-lookup"><span data-stu-id="8c390-129">After hello operation is finished, you track hello telemetry.</span></span> <span data-ttu-id="8c390-130">Hola de ejemplo siguiente muestra esta tarea.</span><span class="sxs-lookup"><span data-stu-id="8c390-130">hello following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="8c390-131">Solicitud HTTP en una aplicación autohospedada de Owin</span><span class="sxs-lookup"><span data-stu-id="8c390-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="8c390-132">En este ejemplo, seguimos hello [protocolo HTTP para la correlación](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="8c390-132">In this example, we follow hello [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="8c390-133">Debe esperar tooreceive encabezados que se describen no existe.</span><span class="sxs-lookup"><span data-stu-id="8c390-133">You should expect tooreceive headers that are described there.</span></span>

``` C#
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from hello upstream service, set hello telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process hello request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time toostop hello operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns hello root ID from hello '|' toohello first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="8c390-134">Protocolo HTTP para la correlación de Hello también declara hello `Correlation-Context` encabezado.</span><span class="sxs-lookup"><span data-stu-id="8c390-134">hello HTTP Protocol for Correlation also declares hello `Correlation-Context` header.</span></span> <span data-ttu-id="8c390-135">Pero aquí se omite para simplificar.</span><span class="sxs-lookup"><span data-stu-id="8c390-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="8c390-136">Instrumentación de colas</span><span class="sxs-lookup"><span data-stu-id="8c390-136">Queue instrumentation</span></span>
<span data-ttu-id="8c390-137">Para la comunicación de HTTP, hemos creado un protocolo toopass detalles de correlación.</span><span class="sxs-lookup"><span data-stu-id="8c390-137">For HTTP communication, we've created a protocol toopass correlation details.</span></span> <span data-ttu-id="8c390-138">Con los protocolos de algunas colas, puede pasar metadatos adicionales junto con el mensaje de bienvenida y con otros usuarios que no se puede.</span><span class="sxs-lookup"><span data-stu-id="8c390-138">With some queues' protocols, you can pass additional metadata along with hello message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="8c390-139">Cola de Service Bus</span><span class="sxs-lookup"><span data-stu-id="8c390-139">Service Bus queue</span></span>
<span data-ttu-id="8c390-140">Con hello Azure [cola de Service Bus](../service-bus-messaging/index.md), puede pasar una bolsa de propiedades junto con el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="8c390-140">With hello Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with hello message.</span></span> <span data-ttu-id="8c390-141">Usamos identificador de correlación de hello toopass.</span><span class="sxs-lookup"><span data-stu-id="8c390-141">We use it toopass hello correlation ID.</span></span>

<span data-ttu-id="8c390-142">cola de Bus de servicio de Hello usa protocolos basados en TCP.</span><span class="sxs-lookup"><span data-stu-id="8c390-142">hello Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="8c390-143">Application Insights no realiza un seguimiento automático de las operaciones de cola, por lo que se realiza manualmente.</span><span class="sxs-lookup"><span data-stu-id="8c390-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="8c390-144">eliminación de cola de Hello operación es una API de estilo de inserción y estamos tootrack no se puede se.</span><span class="sxs-lookup"><span data-stu-id="8c390-144">hello dequeue operation is a push-style API, and we're unable tootrack it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="8c390-145">Poner en cola</span><span class="sxs-lookup"><span data-stu-id="8c390-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes hello telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows hello property bag toopass along with hello message.
    // We will use them toopass our correlation identifiers (and other context)
    // toohello consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a><span data-ttu-id="8c390-146">Proceso</span><span class="sxs-lookup"><span data-stu-id="8c390-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After hello message is taken from hello queue, create RequestTelemetry tootrack its processing.
    // It might also make sense tooget hello name from hello message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a><span data-ttu-id="8c390-147">Cola de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8c390-147">Azure Storage queue</span></span>
<span data-ttu-id="8c390-148">Hola siguiente ejemplo se muestra cómo hello tootrack [cola de almacenamiento de Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) operaciones y poner en correlación telemetría entre productores de hello, consumidores de Hola y el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c390-148">hello following example shows how tootrack hello [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between hello producer, hello consumer, and Azure Storage.</span></span> 

<span data-ttu-id="8c390-149">cola de almacenamiento de Hello tiene una API de HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c390-149">hello Storage queue has an HTTP API.</span></span> <span data-ttu-id="8c390-150">Cola de toohello de todas las llamadas se controlan por hello recopilador de dependencia de visión de aplicación para las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c390-150">All calls toohello queue are tracked by hello Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="8c390-151">Asegúrese de que tiene `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` en `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="8c390-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="8c390-152">Si no lo tiene, agregarlo mediante programación tal como se describe en [de filtrado y de preprocesamiento en hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="8c390-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="8c390-153">Si configura Application Insights manualmente, asegúrese de crear e inicializar `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` de esta forma:</span><span class="sxs-lookup"><span data-stu-id="8c390-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

<span data-ttu-id="8c390-154">También puede toocorrelate Hola el identificador de operación de Application Insights con Id. de solicitud de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c390-154">You also might want toocorrelate hello Application Insights operation ID with hello Storage request ID.</span></span> <span data-ttu-id="8c390-155">Para obtener información sobre cómo solicitar tooset y obtener un almacenamiento de cliente y un identificador de solicitud de servidor, consulte [supervisar, diagnosticar y solucionar problemas de almacenamiento de Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="8c390-155">For information on how tooset and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="8c390-156">Poner en cola</span><span class="sxs-lookup"><span data-stu-id="8c390-156">Enqueue</span></span>
<span data-ttu-id="8c390-157">Dado que las colas de almacenamiento admiten Hola API HTTP, todas las operaciones con cola de Hola se realiza automáticamente un seguimiento por Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8c390-157">Because Storage queues support hello HTTP API, all operations with hello queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="8c390-158">En muchos casos, esta instrumentación debería ser suficiente.</span><span class="sxs-lookup"><span data-stu-id="8c390-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="8c390-159">Sin embargo, toocorrelate realiza un seguimiento en el lado del consumidor de hello con seguimientos de productor, debe pasar algún contexto de correlación del mismo modo toohow lo hacemos en hello protocolo HTTP para la correlación.</span><span class="sxs-lookup"><span data-stu-id="8c390-159">However, toocorrelate traces on hello consumer side with producer traces, you must pass some correlation context similarly toohow we do it in hello HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="8c390-160">En este ejemplo, se realiza el seguimiento de hello opcional `Enqueue` operación.</span><span class="sxs-lookup"><span data-stu-id="8c390-160">In this example, we track hello optional `Enqueue` operation.</span></span> <span data-ttu-id="8c390-161">Puede:</span><span class="sxs-lookup"><span data-stu-id="8c390-161">You can:</span></span>

 - <span data-ttu-id="8c390-162">**Correlacionar reintentos (si existe)**: tienen un elemento primario común que es hello `Enqueue` operación.</span><span class="sxs-lookup"><span data-stu-id="8c390-162">**Correlate retries (if any)**: They all have one common parent that's hello `Enqueue` operation.</span></span> <span data-ttu-id="8c390-163">En caso contrario, le realiza el seguimiento como elementos secundarios de la solicitud entrante de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c390-163">Otherwise, they're tracked as children of hello incoming request.</span></span> <span data-ttu-id="8c390-164">Si hay varias colas de toohello solicitudes lógico, puede que sea difícil toofind qué llamada generó reintentos.</span><span class="sxs-lookup"><span data-stu-id="8c390-164">If there are multiple logical requests toohello queue, it might be difficult toofind which call resulted in retries.</span></span>
 - <span data-ttu-id="8c390-165">**Poner en correlación los registros de Azure Storage (si es necesario y cuando sea necesario)**: Se hace con la telemetría de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8c390-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="8c390-166">Hola `Enqueue` operación es secundario de Hola de una operación de elemento primario (por ejemplo, una solicitud HTTP de entrada).</span><span class="sxs-lookup"><span data-stu-id="8c390-166">hello `Enqueue` operation is hello child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="8c390-167">llamada de dependencia de Hello HTTP es secundario Hola Hola `Enqueue` descendiente del secundario hello y operación de solicitud entrante de hello:</span><span class="sxs-lookup"><span data-stu-id="8c390-167">hello HTTP dependency call is hello child of hello `Enqueue` operation and hello grandchild of hello incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose toopass payload serialized tooJSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message tooprocess'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id toohello OperationContext toocorrelate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

<span data-ttu-id="8c390-168">cantidad de hello tooreduce de telemetría informa de la aplicación o si no desea hello tootrack `Enqueue` operación por otras razones, use hello `Activity` API directamente:</span><span class="sxs-lookup"><span data-stu-id="8c390-168">tooreduce hello amount of telemetry your application reports or if you don't want tootrack hello `Enqueue` operation for other reasons, use hello `Activity` API directly:</span></span>

- <span data-ttu-id="8c390-169">Crear (e iniciar) un nuevo `Activity` en lugar de iniciar la operación de Application Insights Hola.</span><span class="sxs-lookup"><span data-stu-id="8c390-169">Create (and start) a new `Activity` instead of starting hello Application Insights operation.</span></span> <span data-ttu-id="8c390-170">Lo hace *no* necesita tooassign ninguna propiedad en él excepto el nombre de la operación de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c390-170">You do *not* need tooassign any properties on it except hello operation name.</span></span>
- <span data-ttu-id="8c390-171">Serializar `yourActivity.Id` en la carga de mensaje de Hola en lugar de `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="8c390-171">Serialize `yourActivity.Id` into hello message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="8c390-172">También puede usar `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="8c390-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="8c390-173">Quitar de la cola</span><span class="sxs-lookup"><span data-stu-id="8c390-173">Dequeue</span></span>
<span data-ttu-id="8c390-174">De igual forma demasiado`Enqueue`, una cola de almacenamiento de toohello de solicitud HTTP real se realiza automáticamente un seguimiento por Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8c390-174">Similarly too`Enqueue`, an actual HTTP request toohello Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="8c390-175">Sin embargo, Hola `Enqueue` operación supuestamente se produce en el contexto de primario hello, como un contexto de solicitud entrante.</span><span class="sxs-lookup"><span data-stu-id="8c390-175">However, hello `Enqueue` operation presumably happens in hello parent context, such as an incoming request context.</span></span> <span data-ttu-id="8c390-176">SDK de Application Insights correlaciona automáticamente este tipo de operación (y su parte HTTP) con la solicitud primaria de Hola y otro telemetría notifica en hello mismo ámbito.</span><span class="sxs-lookup"><span data-stu-id="8c390-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with hello parent request and other telemetry reported in hello same scope.</span></span>

<span data-ttu-id="8c390-177">Hola `Dequeue` operación es difícil.</span><span class="sxs-lookup"><span data-stu-id="8c390-177">hello `Dequeue` operation is tricky.</span></span> <span data-ttu-id="8c390-178">Hola Application Insights SDK automáticamente realiza un seguimiento de las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c390-178">hello Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="8c390-179">Sin embargo, desconoce contexto de correlación de Hola hasta que se analiza el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="8c390-179">However, it doesn't know hello correlation context until hello message is parsed.</span></span> <span data-ttu-id="8c390-180">No es toocorrelate posible el mensaje Hola de Hola HTTP solicitud tooget con rest Hola de telemetría de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c390-180">It's not possible toocorrelate hello HTTP request tooget hello message with hello rest of hello telemetry.</span></span>

<span data-ttu-id="8c390-181">En muchos casos, puede que sea la cola de toohello de solicitudes HTTP de toocorrelate útil hello en otros seguimientos así.</span><span class="sxs-lookup"><span data-stu-id="8c390-181">In many cases, it might be useful toocorrelate hello HTTP request toohello queue with other traces as well.</span></span> <span data-ttu-id="8c390-182">Hello ejemplo siguiente se muestra cómo toodo:</span><span class="sxs-lookup"><span data-stu-id="8c390-182">hello following example demonstrates how toodo it:</span></span>

``` C#
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want toocorrelate hello Dequeue operation with processing.
            // However, we will only know what correlation ID toouse after we get it from hello message,
            // so we will report telemetry after we know hello IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete hello message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a><span data-ttu-id="8c390-183">Proceso</span><span class="sxs-lookup"><span data-stu-id="8c390-183">Process</span></span>

<span data-ttu-id="8c390-184">En el siguiente ejemplo de Hola, se traza un mensaje entrante de una manera de forma similar solicitar toohow se seguimiento HTTP entrante:</span><span class="sxs-lookup"><span data-stu-id="8c390-184">In hello following example, we trace an incoming message in a manner similarly toohow we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After hello message is dequeued from hello queue, create RequestTelemetry tootrack its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense tooget hello name from hello message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="8c390-185">Del mismo modo, se pueden instrumentar otras operaciones de cola.</span><span class="sxs-lookup"><span data-stu-id="8c390-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="8c390-186">Una operación de lectura se debe instrumentalizar de una manera similar a la de una operación de quitar de la cola.</span><span class="sxs-lookup"><span data-stu-id="8c390-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="8c390-187">La instrumentación de las operaciones de administración de cola no es necesaria.</span><span class="sxs-lookup"><span data-stu-id="8c390-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="8c390-188">Application Insights realiza el seguimiento de las operaciones como HTTP y en la mayoría de los casos es suficiente.</span><span class="sxs-lookup"><span data-stu-id="8c390-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="8c390-189">Cuando se instrumenta la eliminación del mensaje, asegúrese de que establecer operación Hola identificadores (correlación).</span><span class="sxs-lookup"><span data-stu-id="8c390-189">When you instrument message deletion, make sure you set hello operation (correlation) identifiers.</span></span> <span data-ttu-id="8c390-190">Como alternativa, puede usar hello `Activity` API.</span><span class="sxs-lookup"><span data-stu-id="8c390-190">Alternatively, you can use hello `Activity` API.</span></span> <span data-ttu-id="8c390-191">A continuación, no es necesario tooset identificadores de operación en elementos de telemetría de hello porque Application Insights lo hace por usted:</span><span class="sxs-lookup"><span data-stu-id="8c390-191">Then you don't need tooset operation identifiers on hello telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="8c390-192">Crear un nuevo `Activity` después de que tiene un elemento de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c390-192">Create a new `Activity` after you've got an item from hello queue.</span></span>
- <span data-ttu-id="8c390-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate productor y el consumidor registros.</span><span class="sxs-lookup"><span data-stu-id="8c390-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate consumer and producer logs.</span></span>
- <span data-ttu-id="8c390-194">Iniciar hello `Activity`.</span><span class="sxs-lookup"><span data-stu-id="8c390-194">Start hello `Activity`.</span></span>
- <span data-ttu-id="8c390-195">Realice el seguimiento de las operaciones de quitar de la cola, proceso y eliminación mediante las aplicaciones auxiliares `Start/StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="8c390-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="8c390-196">Hacerlo de hello mismo asincrónica (contexto de ejecución) de flujo de control.</span><span class="sxs-lookup"><span data-stu-id="8c390-196">Do it from hello same asynchronous control flow (execution context).</span></span> <span data-ttu-id="8c390-197">De esta forma, se correlacionan correctamente.</span><span class="sxs-lookup"><span data-stu-id="8c390-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="8c390-198">Hola Stop `Activity`.</span><span class="sxs-lookup"><span data-stu-id="8c390-198">Stop hello `Activity`.</span></span>
- <span data-ttu-id="8c390-199">Use `Start/StopOperation` o llame a la telemetría de `Track` manualmente.</span><span class="sxs-lookup"><span data-stu-id="8c390-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="8c390-200">Procesamiento por lotes</span><span class="sxs-lookup"><span data-stu-id="8c390-200">Batch processing</span></span>
<span data-ttu-id="8c390-201">En algunas colas, se pueden quitar de la cola varios mensajes con una solicitud.</span><span class="sxs-lookup"><span data-stu-id="8c390-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="8c390-202">Procesar mensajes de este tipo es supuestamente independiente y pertenece toohello diferentes operaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="8c390-202">Processing such messages is presumably independent and belongs toohello different logical operations.</span></span> <span data-ttu-id="8c390-203">En este caso, no es posible toocorrelate hello `Dequeue` procesamiento de mensajes de operación tooparticular.</span><span class="sxs-lookup"><span data-stu-id="8c390-203">In this case, it's not possible toocorrelate hello `Dequeue` operation tooparticular message processing.</span></span>

<span data-ttu-id="8c390-204">Cada mensaje debe procesarse en su propio flujo de control asincrónico.</span><span class="sxs-lookup"><span data-stu-id="8c390-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="8c390-205">Para obtener más información, vea hello [dependencias saliente seguimiento](#outgoing-dependencies-tracking) sección.</span><span class="sxs-lookup"><span data-stu-id="8c390-205">For more information, see hello [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="8c390-206">Tareas en segundo plano de ejecución prolongada</span><span class="sxs-lookup"><span data-stu-id="8c390-206">Long-running background tasks</span></span>
<span data-ttu-id="8c390-207">Algunas aplicaciones inician operaciones de larga ejecución que es posible que se deban a solicitudes del usuario.</span><span class="sxs-lookup"><span data-stu-id="8c390-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="8c390-208">Desde la perspectiva de instrumentación de seguimiento/hello, no es diferente de la instrumentación de solicitud o dependencia:</span><span class="sxs-lookup"><span data-stu-id="8c390-208">From hello tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

``` C#
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process hello task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="8c390-209">En este ejemplo, utilizamos `telemetryClient.StartOperation` toocreate `RequestTelemetry` y el contexto de correlación de Hola de relleno.</span><span class="sxs-lookup"><span data-stu-id="8c390-209">In this example, we use `telemetryClient.StartOperation` toocreate `RequestTelemetry` and fill hello correlation context.</span></span> <span data-ttu-id="8c390-210">Supongamos que tiene una operación primario que se creó por solicitudes entrantes que Hola operación programada.</span><span class="sxs-lookup"><span data-stu-id="8c390-210">Let's say you have a parent operation that was created by incoming requests that scheduled hello operation.</span></span> <span data-ttu-id="8c390-211">Siempre que `BackgroundTask` se inicia en Hola mismo flujo de control asincrónico como una solicitud entrante, se correlaciona con esa operación primario.</span><span class="sxs-lookup"><span data-stu-id="8c390-211">As long as `BackgroundTask` starts in hello same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="8c390-212">`BackgroundTask`y todos los elementos de telemetría anidada automáticamente están correlacionados con la solicitud de Hola que lo causó, incluso después de que finalice la solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c390-212">`BackgroundTask` and all nested telemetry items are automatically correlated with hello request that caused it, even after hello request ends.</span></span>

<span data-ttu-id="8c390-213">Cuando inicia la tarea hello de subproceso en segundo plano Hola que no tiene ninguna operación (`Activity`) asociados a él, `BackgroundTask` no tiene ningún primario.</span><span class="sxs-lookup"><span data-stu-id="8c390-213">When hello task starts from hello background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="8c390-214">Pero puede tener operaciones anidadas.</span><span class="sxs-lookup"><span data-stu-id="8c390-214">However, it can have nested operations.</span></span> <span data-ttu-id="8c390-215">Todos los elementos de telemetría registrados en la tarea hello están correlacionado toohello `RequestTelemetry` creado en `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="8c390-215">All telemetry items reported from hello task are correlated toohello `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="8c390-216">Seguimiento de dependencias de salida</span><span class="sxs-lookup"><span data-stu-id="8c390-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="8c390-217">Puede realizar el seguimiento de su propio tipo de dependencia o de una operación que no es compatible con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8c390-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="8c390-218">Hola `Enqueue` método en cola de Bus de servicio de Hola o una cola de almacenamiento de hello puede servir como ejemplos de tal seguimiento personalizado.</span><span class="sxs-lookup"><span data-stu-id="8c390-218">hello `Enqueue` method in hello Service Bus queue or hello Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="8c390-219">Hola general para seguimiento de dependencias personalizada consiste en:</span><span class="sxs-lookup"><span data-stu-id="8c390-219">hello general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="8c390-220">Llamar a hello `TelemetryClient.StartOperation` método (extensión) que rellena hello `DependencyTelemetry` propiedades que son necesarios para la correlación y algunas otras propiedades (hora de inicio de marca, la duración).</span><span class="sxs-lookup"><span data-stu-id="8c390-220">Call hello `TelemetryClient.StartOperation` (extension) method that fills hello `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="8c390-221">Establecer otras propiedades personalizadas en hello `DependencyTelemetry`, como el nombre de Hola y cualquier otro contexto necesita.</span><span class="sxs-lookup"><span data-stu-id="8c390-221">Set other custom properties on hello `DependencyTelemetry`, such as hello name and any other context you need.</span></span>
- <span data-ttu-id="8c390-222">Realice una llamada de dependencia y espere.</span><span class="sxs-lookup"><span data-stu-id="8c390-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="8c390-223">Detener la operación de hello con `StopOperation` cuando finaliza.</span><span class="sxs-lookup"><span data-stu-id="8c390-223">Stop hello operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="8c390-224">Controle las excepciones.</span><span class="sxs-lookup"><span data-stu-id="8c390-224">Handle exceptions.</span></span>

<span data-ttu-id="8c390-225">`StopOperation`solo se detiene Hola operación que se inició.</span><span class="sxs-lookup"><span data-stu-id="8c390-225">`StopOperation` only stops hello operation that was started.</span></span> <span data-ttu-id="8c390-226">Si la operación de ejecución actual de hello no coincide con hello uno desea toostop, `StopOperation` no hace nada.</span><span class="sxs-lookup"><span data-stu-id="8c390-226">If hello current running operation doesn't match hello one you want toostop, `StopOperation` does nothing.</span></span> <span data-ttu-id="8c390-227">Esta situación puede ocurrir si iniciar varias operaciones en paralelo en hello mismo contexto de ejecución:</span><span class="sxs-lookup"><span data-stu-id="8c390-227">This situation might happen if you start multiple operations in parallel in hello same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for hello first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="8c390-228">Asegúrese de que siempre llama a `StartOperation` y ejecuta la tarea en su propio contexto:</span><span class="sxs-lookup"><span data-stu-id="8c390-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
```C#
public async Task RunMyTaskAsync()
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
    try 
    {
        var myTask = await StartMyTaskAsync();
        // Update status code and success as appropriate.
    }
    catch(...) 
    {
        // Update status code and success as appropriate.
    }
    finally 
    {
        telemetryClient.StopOperation(operation);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="8c390-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c390-229">Next steps</span></span>

- <span data-ttu-id="8c390-230">Obtenga información acerca de los conceptos básicos de Hola de [correlación telemetría](application-insights-correlation.md) en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8c390-230">Learn hello basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="8c390-231">Vea hello [modelo de datos](application-insights-data-model.md) para el modelo de tipos y datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8c390-231">See hello [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="8c390-232">Informe personalizado [eventos y métricas](app-insights-api-custom-events-metrics.md) tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="8c390-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span></span>
- <span data-ttu-id="8c390-233">Compruebe la [configuración](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) de la recopilación de propiedades de contexto.</span><span class="sxs-lookup"><span data-stu-id="8c390-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="8c390-234">Comprobar hello [Guía de usuario de System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee cómo se correlacionan telemetría.</span><span class="sxs-lookup"><span data-stu-id="8c390-234">Check hello [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee how we correlate telemetry.</span></span>
