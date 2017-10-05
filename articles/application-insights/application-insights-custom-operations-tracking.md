---
title: Seguimiento de las operaciones personalizadas con el SDK de .NET para Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: b31d38fe2f7060597956a1ee9c66f43ce39d7240
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="de6c8-103">Seguimiento de las operaciones personalizadas con el SDK de .NET para Application Insights</span><span class="sxs-lookup"><span data-stu-id="de6c8-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="de6c8-104">Los SDK de Azure Application Insights realizan el seguimiento automático de las solicitudes HTTP de entrada y las llamadas a los servicios dependientes, como solicitudes HTTP y consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="de6c8-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls to dependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="de6c8-105">El seguimiento y la correlación de las solicitudes y dependencias le ofrece visibilidad en la capacidad de respuesta de toda la aplicación y la confiabilidad en todos los microservicios que combinan esta aplicación.</span><span class="sxs-lookup"><span data-stu-id="de6c8-105">Tracking and correlation of requests and dependencies give you visibility into the whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="de6c8-106">Hay una clase de patrones de aplicación que no se admiten de forma genérica.</span><span class="sxs-lookup"><span data-stu-id="de6c8-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="de6c8-107">La supervisión correcta de estos patrones requiere la instrumentación manual de código.</span><span class="sxs-lookup"><span data-stu-id="de6c8-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="de6c8-108">En este artículo se abordan algunos patrones que pueden requerir la instrumentación manual, como el procesamiento de colas personalizadas y la ejecución de tareas de larga duración en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="de6c8-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="de6c8-109">En este documento se proporcionan instrucciones sobre cómo realizar el seguimiento de operaciones personalizadas con el SDK de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="de6c8-109">This document provides guidance on how to track custom operations with the Application Insights SDK.</span></span> <span data-ttu-id="de6c8-110">Esta documentación es relevante para:</span><span class="sxs-lookup"><span data-stu-id="de6c8-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="de6c8-111">Application Insights para .NET (también conocido como Base SDK) versión 2.4+.</span><span class="sxs-lookup"><span data-stu-id="de6c8-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="de6c8-112">Application Insights para aplicaciones web (con ASP.NET) versión 2.4+.</span><span class="sxs-lookup"><span data-stu-id="de6c8-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="de6c8-113">Application Insights para ASP.NET Core versión 2.1+.</span><span class="sxs-lookup"><span data-stu-id="de6c8-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="de6c8-114">Información general</span><span class="sxs-lookup"><span data-stu-id="de6c8-114">Overview</span></span>
<span data-ttu-id="de6c8-115">Una operación es una parte de trabajo lógica ejecutada por una aplicación.</span><span class="sxs-lookup"><span data-stu-id="de6c8-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="de6c8-116">Tiene un nombre, una hora de inicio, una duración, un resultado y un contexto de ejecución como el nombre de usuario, las propiedades y el resultado.</span><span class="sxs-lookup"><span data-stu-id="de6c8-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="de6c8-117">Si la operación B inició la operación A, la operación B se establece como un elemento primario de A. Una operación solo puede tener un elemento primario, pero puede tener muchas operaciones secundarias.</span><span class="sxs-lookup"><span data-stu-id="de6c8-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="de6c8-118">Para más información sobre las operaciones y la correlación de telemetría, vea [Correlación de telemetría en Azure Application Insights](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="de6c8-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="de6c8-119">En el SDK de .NET para Application Insights se describe la operación mediante la clase abstracta [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) y sus descendientes [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) y [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="de6c8-119">In the Application Insights .NET SDK, the operation is described by the abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="de6c8-120">Seguimiento de operaciones de entrada</span><span class="sxs-lookup"><span data-stu-id="de6c8-120">Incoming operations tracking</span></span> 
<span data-ttu-id="de6c8-121">El SDK web de Application Insights recopila automáticamente las solicitudes HTTP para las aplicaciones ASP.NET que se ejecutan en una canalización IIS y todas las aplicaciones ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="de6c8-121">The Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="de6c8-122">Hay soluciones admitidas por la comunidad para otras plataformas y marcos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="de6c8-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="de6c8-123">Pero si la aplicación no es compatible con ninguna solución admitida por los estándares o la comunidad, puede instrumentarla de forma manual.</span><span class="sxs-lookup"><span data-stu-id="de6c8-123">However, if the application isn't supported by any of the standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="de6c8-124">Otro ejemplo que requiere seguimiento personalizado es el proceso de trabajo que recibe los elementos de la cola.</span><span class="sxs-lookup"><span data-stu-id="de6c8-124">Another example that requires custom tracking is the worker that receives items from the queue.</span></span> <span data-ttu-id="de6c8-125">Para algunas colas, se realiza un seguimiento como dependencia de la llamada para agregar un mensaje a esta cola.</span><span class="sxs-lookup"><span data-stu-id="de6c8-125">For some queues, the call to add a message to this queue is tracked as a dependency.</span></span> <span data-ttu-id="de6c8-126">Pero la operación general que describe el procesamiento de mensajes no se recopila automáticamente.</span><span class="sxs-lookup"><span data-stu-id="de6c8-126">However, the high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="de6c8-127">Veamos cómo se puede realizar el seguimiento de estas operaciones.</span><span class="sxs-lookup"><span data-stu-id="de6c8-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="de6c8-128">Generalmente, la tarea consiste en crear `RequestTelemetry` y establecer propiedades conocidas.</span><span class="sxs-lookup"><span data-stu-id="de6c8-128">On a high level, the task is to create `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="de6c8-129">Una vez finalizada la operación, se realiza el seguimiento de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="de6c8-129">After the operation is finished, you track the telemetry.</span></span> <span data-ttu-id="de6c8-130">En el siguiente ejemplo se muestra esta tarea.</span><span class="sxs-lookup"><span data-stu-id="de6c8-130">The following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="de6c8-131">Solicitud HTTP en una aplicación autohospedada de Owin</span><span class="sxs-lookup"><span data-stu-id="de6c8-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="de6c8-132">En este ejemplo, se sigue el [Protocolo HTTP para la correlación](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="de6c8-132">In this example, we follow the [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="de6c8-133">Debe esperar recibir los encabezados que se describen ahí.</span><span class="sxs-lookup"><span data-stu-id="de6c8-133">You should expect to receive headers that are described there.</span></span>

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

        // If there is a Request-Id received from the upstream service, set the telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process the request.
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

            // Now it's time to stop the operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns the root ID from the '|' to the first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="de6c8-134">El Protocolo HTTP para la correlación también declara el encabezado `Correlation-Context`.</span><span class="sxs-lookup"><span data-stu-id="de6c8-134">The HTTP Protocol for Correlation also declares the `Correlation-Context` header.</span></span> <span data-ttu-id="de6c8-135">Pero aquí se omite para simplificar.</span><span class="sxs-lookup"><span data-stu-id="de6c8-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="de6c8-136">Instrumentación de colas</span><span class="sxs-lookup"><span data-stu-id="de6c8-136">Queue instrumentation</span></span>
<span data-ttu-id="de6c8-137">Para la comunicación HTTP, se ha creado un protocolo para pasar los detalles de correlación.</span><span class="sxs-lookup"><span data-stu-id="de6c8-137">For HTTP communication, we've created a protocol to pass correlation details.</span></span> <span data-ttu-id="de6c8-138">Con algunos protocolos de las colas se pueden pasar metadatos adicionales junto con el mensaje y con otros no.</span><span class="sxs-lookup"><span data-stu-id="de6c8-138">With some queues' protocols, you can pass additional metadata along with the message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="de6c8-139">Cola de Service Bus</span><span class="sxs-lookup"><span data-stu-id="de6c8-139">Service Bus queue</span></span>
<span data-ttu-id="de6c8-140">Con la [cola de Azure Service Bus](../service-bus-messaging/index.md), puede pasar un contenedor de propiedades junto con el mensaje.</span><span class="sxs-lookup"><span data-stu-id="de6c8-140">With the Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with the message.</span></span> <span data-ttu-id="de6c8-141">Se usa para pasar el identificador de correlación.</span><span class="sxs-lookup"><span data-stu-id="de6c8-141">We use it to pass the correlation ID.</span></span>

<span data-ttu-id="de6c8-142">La cola de Service Bus usa protocolos basados en TCP.</span><span class="sxs-lookup"><span data-stu-id="de6c8-142">The Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="de6c8-143">Application Insights no realiza un seguimiento automático de las operaciones de cola, por lo que se realiza manualmente.</span><span class="sxs-lookup"><span data-stu-id="de6c8-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="de6c8-144">La operación de quitar de la cola es una API de estilo de inserción y no es posible realizar su seguimiento.</span><span class="sxs-lookup"><span data-stu-id="de6c8-144">The dequeue operation is a push-style API, and we're unable to track it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="de6c8-145">Poner en cola</span><span class="sxs-lookup"><span data-stu-id="de6c8-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes the telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows the property bag to pass along with the message.
    // We will use them to pass our correlation identifiers (and other context)
    // to the consumer.
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

#### <a name="process"></a><span data-ttu-id="de6c8-146">Proceso</span><span class="sxs-lookup"><span data-stu-id="de6c8-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After the message is taken from the queue, create RequestTelemetry to track its processing.
    // It might also make sense to get the name from the message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
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

### <a name="azure-storage-queue"></a><span data-ttu-id="de6c8-147">Cola de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="de6c8-147">Azure Storage queue</span></span>
<span data-ttu-id="de6c8-148">En el ejemplo siguiente se muestra cómo realizar el seguimiento de operaciones de [cola de Azure Storage](../storage/queues/storage-dotnet-how-to-use-queues.md) y poner en correlación la telemetría entre el productor, el consumidor y Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="de6c8-148">The following example shows how to track the [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between the producer, the consumer, and Azure Storage.</span></span> 

<span data-ttu-id="de6c8-149">La cola de Storage tiene una API HTTP.</span><span class="sxs-lookup"><span data-stu-id="de6c8-149">The Storage queue has an HTTP API.</span></span> <span data-ttu-id="de6c8-150">El recolector de dependencias de Application Insights realiza el seguimiento de todas las llamadas a la cola para las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="de6c8-150">All calls to the queue are tracked by the Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="de6c8-151">Asegúrese de que tiene `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` en `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="de6c8-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="de6c8-152">Si no lo tiene, agréguelo mediante programación como se describe en [Filtrado y preprocesamiento de la telemetría en el SDK de Application Insights](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="de6c8-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in the Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="de6c8-153">Si configura Application Insights manualmente, asegúrese de crear e inicializar `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` de esta forma:</span><span class="sxs-lookup"><span data-stu-id="de6c8-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection to some domains by adding it to the excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on the Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget to dispose of the module during application shutdown.
```

<span data-ttu-id="de6c8-154">Es posible que también quiera poner en correlación el identificador de operación de Application Insights con el identificador de solicitud de Storage.</span><span class="sxs-lookup"><span data-stu-id="de6c8-154">You also might want to correlate the Application Insights operation ID with the Storage request ID.</span></span> <span data-ttu-id="de6c8-155">Para obtener información sobre cómo establecer y obtener un cliente de solicitud de Storage y un identificador de solicitud de servidor, vea [Supervisión, diagnóstico y solución de problemas de Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="de6c8-155">For information on how to set and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="de6c8-156">Poner en cola</span><span class="sxs-lookup"><span data-stu-id="de6c8-156">Enqueue</span></span>
<span data-ttu-id="de6c8-157">Como las colas de Storage admiten la API de HTTP, Application Insights realiza el seguimiento automático de todas las operaciones en la cola.</span><span class="sxs-lookup"><span data-stu-id="de6c8-157">Because Storage queues support the HTTP API, all operations with the queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="de6c8-158">En muchos casos, esta instrumentación debería ser suficiente.</span><span class="sxs-lookup"><span data-stu-id="de6c8-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="de6c8-159">Pero para poner en correlación seguimientos en el lado del consumidor con seguimientos del productor, tiene que pasar un contexto de correlación de forma similar a como se hace en el Protocolo HTTP para la correlación.</span><span class="sxs-lookup"><span data-stu-id="de6c8-159">However, to correlate traces on the consumer side with producer traces, you must pass some correlation context similarly to how we do it in the HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="de6c8-160">En este ejemplo, se realiza el seguimiento de la operación `Enqueue` opcional.</span><span class="sxs-lookup"><span data-stu-id="de6c8-160">In this example, we track the optional `Enqueue` operation.</span></span> <span data-ttu-id="de6c8-161">Puede:</span><span class="sxs-lookup"><span data-stu-id="de6c8-161">You can:</span></span>

 - <span data-ttu-id="de6c8-162">**Poner en correlación los reintentos (si existen)**: Todos tienen un elemento primario común que es la operación `Enqueue`.</span><span class="sxs-lookup"><span data-stu-id="de6c8-162">**Correlate retries (if any)**: They all have one common parent that's the `Enqueue` operation.</span></span> <span data-ttu-id="de6c8-163">En caso contrario, se realiza su seguimiento como elementos secundarios de la solicitud de entrada.</span><span class="sxs-lookup"><span data-stu-id="de6c8-163">Otherwise, they're tracked as children of the incoming request.</span></span> <span data-ttu-id="de6c8-164">Si hay varias solicitudes lógicas a la cola, podría ser difícil buscar qué llamada generó los reintentos.</span><span class="sxs-lookup"><span data-stu-id="de6c8-164">If there are multiple logical requests to the queue, it might be difficult to find which call resulted in retries.</span></span>
 - <span data-ttu-id="de6c8-165">**Poner en correlación los registros de Azure Storage (si es necesario y cuando sea necesario)**: Se hace con la telemetría de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="de6c8-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="de6c8-166">La operación `Enqueue` es el elemento secundario de una operación principal (por ejemplo, una solicitud HTTP de entrada).</span><span class="sxs-lookup"><span data-stu-id="de6c8-166">The `Enqueue` operation is the child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="de6c8-167">La llamada de dependencia HTTP es el elemento secundario de la operación `Enqueue` y el descendiente de la solicitud de entrada:</span><span class="sxs-lookup"><span data-stu-id="de6c8-167">The HTTP dependency call is the child of the `Enqueue` operation and the grandchild of the incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose to pass payload serialized to JSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message to process'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id to the OperationContext to correlate Storage logs and Application Insights telemetry.
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

<span data-ttu-id="de6c8-168">Para reducir la cantidad de telemetría que notifica la aplicación o si no quiere realizar el seguimiento de la operación `Enqueue` por otras razones, use directamente la API `Activity`:</span><span class="sxs-lookup"><span data-stu-id="de6c8-168">To reduce the amount of telemetry your application reports or if you don't want to track the `Enqueue` operation for other reasons, use the `Activity` API directly:</span></span>

- <span data-ttu-id="de6c8-169">Cree (e inicie) una nueva `Activity` en lugar de iniciar la operación de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="de6c8-169">Create (and start) a new `Activity` instead of starting the Application Insights operation.</span></span> <span data-ttu-id="de6c8-170">*No* es necesario asignar ninguna propiedad en este elemento, excepto el nombre de la operación.</span><span class="sxs-lookup"><span data-stu-id="de6c8-170">You do *not* need to assign any properties on it except the operation name.</span></span>
- <span data-ttu-id="de6c8-171">Serialice `yourActivity.Id` en la carga del mensaje en lugar de `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="de6c8-171">Serialize `yourActivity.Id` into the message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="de6c8-172">También puede usar `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="de6c8-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="de6c8-173">Quitar de la cola</span><span class="sxs-lookup"><span data-stu-id="de6c8-173">Dequeue</span></span>
<span data-ttu-id="de6c8-174">Al igual que `Enqueue`, Application Insights realiza el seguimiento automático de la solicitud HTTP a la cola de Storage.</span><span class="sxs-lookup"><span data-stu-id="de6c8-174">Similarly to `Enqueue`, an actual HTTP request to the Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="de6c8-175">Pero supuestamente la operación `Enqueue` se produce en el contexto principal, por ejemplo en un contexto de solicitud de entrada.</span><span class="sxs-lookup"><span data-stu-id="de6c8-175">However, the `Enqueue` operation presumably happens in the parent context, such as an incoming request context.</span></span> <span data-ttu-id="de6c8-176">Los SDK de Application Insights correlacionan automáticamente esta operación (y su elemento HTTP) con la solicitud primaria y otra telemetría notificada en el mismo ámbito.</span><span class="sxs-lookup"><span data-stu-id="de6c8-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with the parent request and other telemetry reported in the same scope.</span></span>

<span data-ttu-id="de6c8-177">La operación `Dequeue` es complicada.</span><span class="sxs-lookup"><span data-stu-id="de6c8-177">The `Dequeue` operation is tricky.</span></span> <span data-ttu-id="de6c8-178">El SDK de Application Insights realiza automáticamente el seguimiento de las solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="de6c8-178">The Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="de6c8-179">Pero desconoce el contexto de correlación hasta que se analiza el mensaje.</span><span class="sxs-lookup"><span data-stu-id="de6c8-179">However, it doesn't know the correlation context until the message is parsed.</span></span> <span data-ttu-id="de6c8-180">No es posible poner en correlación la solicitud HTTP para obtener el mensaje con el resto de la telemetría.</span><span class="sxs-lookup"><span data-stu-id="de6c8-180">It's not possible to correlate the HTTP request to get the message with the rest of the telemetry.</span></span>

<span data-ttu-id="de6c8-181">En muchos casos, es posible que resulte útil correlacionar la solicitud HTTP a la cola con otros seguimientos.</span><span class="sxs-lookup"><span data-stu-id="de6c8-181">In many cases, it might be useful to correlate the HTTP request to the queue with other traces as well.</span></span> <span data-ttu-id="de6c8-182">En el siguiente ejemplo se muestra cómo hacerlo:</span><span class="sxs-lookup"><span data-stu-id="de6c8-182">The following example demonstrates how to do it:</span></span>

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

            // If there is a message, we want to correlate the Dequeue operation with processing.
            // However, we will only know what correlation ID to use after we get it from the message,
            // so we will report telemetry after we know the IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete the message.
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

#### <a name="process"></a><span data-ttu-id="de6c8-183">Proceso</span><span class="sxs-lookup"><span data-stu-id="de6c8-183">Process</span></span>

<span data-ttu-id="de6c8-184">En el ejemplo siguiente, se realiza el seguimiento de un mensaje de entrada de forma similar a cómo se realiza el seguimiento de una solicitud HTTP de entrada:</span><span class="sxs-lookup"><span data-stu-id="de6c8-184">In the following example, we trace an incoming message in a manner similarly to how we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After the message is dequeued from the queue, create RequestTelemetry to track its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense to get the name from the message.
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

<span data-ttu-id="de6c8-185">Del mismo modo, se pueden instrumentar otras operaciones de cola.</span><span class="sxs-lookup"><span data-stu-id="de6c8-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="de6c8-186">Una operación de lectura se debe instrumentalizar de una manera similar a la de una operación de quitar de la cola.</span><span class="sxs-lookup"><span data-stu-id="de6c8-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="de6c8-187">La instrumentación de las operaciones de administración de cola no es necesaria.</span><span class="sxs-lookup"><span data-stu-id="de6c8-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="de6c8-188">Application Insights realiza el seguimiento de las operaciones como HTTP y en la mayoría de los casos es suficiente.</span><span class="sxs-lookup"><span data-stu-id="de6c8-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="de6c8-189">Al instrumentar la eliminación de mensajes, asegúrese de establecer los identificadores de la operación (correlación).</span><span class="sxs-lookup"><span data-stu-id="de6c8-189">When you instrument message deletion, make sure you set the operation (correlation) identifiers.</span></span> <span data-ttu-id="de6c8-190">Como alternativa, puede usar la API de `Activity`.</span><span class="sxs-lookup"><span data-stu-id="de6c8-190">Alternatively, you can use the `Activity` API.</span></span> <span data-ttu-id="de6c8-191">No es necesario establecer identificadores de operaciones en los elementos de telemetría, porque Application Insights lo hace automáticamente:</span><span class="sxs-lookup"><span data-stu-id="de6c8-191">Then you don't need to set operation identifiers on the telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="de6c8-192">Cree una nueva `Activity` después de que tenga un elemento de la cola.</span><span class="sxs-lookup"><span data-stu-id="de6c8-192">Create a new `Activity` after you've got an item from the queue.</span></span>
- <span data-ttu-id="de6c8-193">Use `Activity.SetParentId(message.ParentId)` para poner en correlación los registros de consumidor y productor.</span><span class="sxs-lookup"><span data-stu-id="de6c8-193">Use `Activity.SetParentId(message.ParentId)` to correlate consumer and producer logs.</span></span>
- <span data-ttu-id="de6c8-194">Inicie la `Activity`.</span><span class="sxs-lookup"><span data-stu-id="de6c8-194">Start the `Activity`.</span></span>
- <span data-ttu-id="de6c8-195">Realice el seguimiento de las operaciones de quitar de la cola, proceso y eliminación mediante las aplicaciones auxiliares `Start/StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="de6c8-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="de6c8-196">Hágalo desde el mismo flujo de control asincrónico (contexto de ejecución).</span><span class="sxs-lookup"><span data-stu-id="de6c8-196">Do it from the same asynchronous control flow (execution context).</span></span> <span data-ttu-id="de6c8-197">De esta forma, se correlacionan correctamente.</span><span class="sxs-lookup"><span data-stu-id="de6c8-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="de6c8-198">Pare la `Activity`.</span><span class="sxs-lookup"><span data-stu-id="de6c8-198">Stop the `Activity`.</span></span>
- <span data-ttu-id="de6c8-199">Use `Start/StopOperation` o llame a la telemetría de `Track` manualmente.</span><span class="sxs-lookup"><span data-stu-id="de6c8-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="de6c8-200">Procesamiento por lotes</span><span class="sxs-lookup"><span data-stu-id="de6c8-200">Batch processing</span></span>
<span data-ttu-id="de6c8-201">En algunas colas, se pueden quitar de la cola varios mensajes con una solicitud.</span><span class="sxs-lookup"><span data-stu-id="de6c8-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="de6c8-202">El procesamiento de este tipo de mensajes es supuestamente independiente y pertenece a las distintas operaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="de6c8-202">Processing such messages is presumably independent and belongs to the different logical operations.</span></span> <span data-ttu-id="de6c8-203">En este caso, no es posible poner en correlación la operación `Dequeue` con el procesamiento de mensajes determinados.</span><span class="sxs-lookup"><span data-stu-id="de6c8-203">In this case, it's not possible to correlate the `Dequeue` operation to particular message processing.</span></span>

<span data-ttu-id="de6c8-204">Cada mensaje debe procesarse en su propio flujo de control asincrónico.</span><span class="sxs-lookup"><span data-stu-id="de6c8-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="de6c8-205">Para más información, vea la sección [Seguimiento de dependencias de salida](#outgoing-dependencies-tracking).</span><span class="sxs-lookup"><span data-stu-id="de6c8-205">For more information, see the [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="de6c8-206">Tareas en segundo plano de ejecución prolongada</span><span class="sxs-lookup"><span data-stu-id="de6c8-206">Long-running background tasks</span></span>
<span data-ttu-id="de6c8-207">Algunas aplicaciones inician operaciones de larga ejecución que es posible que se deban a solicitudes del usuario.</span><span class="sxs-lookup"><span data-stu-id="de6c8-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="de6c8-208">Desde la perspectiva del seguimiento o la instrumentación, no es diferente de la instrumentación de solicitudes o dependencias:</span><span class="sxs-lookup"><span data-stu-id="de6c8-208">From the tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

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
            // Process the task.
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

<span data-ttu-id="de6c8-209">En este ejemplo, se usa `telemetryClient.StartOperation` para crear `RequestTelemetry` y rellenar el contexto de correlación.</span><span class="sxs-lookup"><span data-stu-id="de6c8-209">In this example, we use `telemetryClient.StartOperation` to create `RequestTelemetry` and fill the correlation context.</span></span> <span data-ttu-id="de6c8-210">Supongamos que tiene una operación principal creada por las solicitudes de entrada que programaron la operación.</span><span class="sxs-lookup"><span data-stu-id="de6c8-210">Let's say you have a parent operation that was created by incoming requests that scheduled the operation.</span></span> <span data-ttu-id="de6c8-211">Siempre que `BackgroundTask` se inicie en el mismo flujo de control asincrónico que una solicitud de entrada, se correlaciona con esa operación principal.</span><span class="sxs-lookup"><span data-stu-id="de6c8-211">As long as `BackgroundTask` starts in the same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="de6c8-212">`BackgroundTask` y todos los elementos de telemetría anidados se correlacionan automáticamente con la solicitud que la causó incluso después de que finalice la solicitud.</span><span class="sxs-lookup"><span data-stu-id="de6c8-212">`BackgroundTask` and all nested telemetry items are automatically correlated with the request that caused it, even after the request ends.</span></span>

<span data-ttu-id="de6c8-213">Cuando la tarea se inicia desde el subproceso en segundo plano que no tiene ninguna operación (`Activity`) asociada a él, `BackgroundTask` no tiene ningún elemento primario.</span><span class="sxs-lookup"><span data-stu-id="de6c8-213">When the task starts from the background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="de6c8-214">Pero puede tener operaciones anidadas.</span><span class="sxs-lookup"><span data-stu-id="de6c8-214">However, it can have nested operations.</span></span> <span data-ttu-id="de6c8-215">Todos los elementos de telemetría notificados desde la tarea se ponen en correlación con la `RequestTelemetry` creada en `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="de6c8-215">All telemetry items reported from the task are correlated to the `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="de6c8-216">Seguimiento de dependencias de salida</span><span class="sxs-lookup"><span data-stu-id="de6c8-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="de6c8-217">Puede realizar el seguimiento de su propio tipo de dependencia o de una operación que no es compatible con Application Insights.</span><span class="sxs-lookup"><span data-stu-id="de6c8-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="de6c8-218">El método `Enqueue` de la cola de Service Bus o la cola de Storage puede servir como ejemplo de este seguimiento personalizado.</span><span class="sxs-lookup"><span data-stu-id="de6c8-218">The `Enqueue` method in the Service Bus queue or the Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="de6c8-219">El enfoque general para el seguimiento de dependencias personalizadas es este:</span><span class="sxs-lookup"><span data-stu-id="de6c8-219">The general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="de6c8-220">Llame al método `TelemetryClient.StartOperation` (extensión) que rellena las propiedades de `DependencyTelemetry` que se necesitan para la correlación y algunas otras (inicio de la marca de tiempo, duración).</span><span class="sxs-lookup"><span data-stu-id="de6c8-220">Call the `TelemetryClient.StartOperation` (extension) method that fills the `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="de6c8-221">Establezca otras propiedades personalizadas en `DependencyTelemetry`, como el nombre y cualquier otro contexto que se necesite.</span><span class="sxs-lookup"><span data-stu-id="de6c8-221">Set other custom properties on the `DependencyTelemetry`, such as the name and any other context you need.</span></span>
- <span data-ttu-id="de6c8-222">Realice una llamada de dependencia y espere.</span><span class="sxs-lookup"><span data-stu-id="de6c8-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="de6c8-223">Detenga la operación con `StopOperation` cuando finalice.</span><span class="sxs-lookup"><span data-stu-id="de6c8-223">Stop the operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="de6c8-224">Controle las excepciones.</span><span class="sxs-lookup"><span data-stu-id="de6c8-224">Handle exceptions.</span></span>

<span data-ttu-id="de6c8-225">`StopOperation` solo detiene la operación que se inició.</span><span class="sxs-lookup"><span data-stu-id="de6c8-225">`StopOperation` only stops the operation that was started.</span></span> <span data-ttu-id="de6c8-226">Si la operación de ejecución actual no coincide con la que quiere detener, `StopOperation` no hace nada.</span><span class="sxs-lookup"><span data-stu-id="de6c8-226">If the current running operation doesn't match the one you want to stop, `StopOperation` does nothing.</span></span> <span data-ttu-id="de6c8-227">Es posible que suceda esta situación si se inician varias operaciones en paralelo en el mismo contexto de ejecución:</span><span class="sxs-lookup"><span data-stu-id="de6c8-227">This situation might happen if you start multiple operations in parallel in the same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for the first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="de6c8-228">Asegúrese de que siempre llama a `StartOperation` y ejecuta la tarea en su propio contexto:</span><span class="sxs-lookup"><span data-stu-id="de6c8-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="de6c8-229">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de6c8-229">Next steps</span></span>

- <span data-ttu-id="de6c8-230">Obtenga los conceptos básicos de la [correlación de telemetría](application-insights-correlation.md) en Application Insights.</span><span class="sxs-lookup"><span data-stu-id="de6c8-230">Learn the basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="de6c8-231">Vea el [modelo de datos](application-insights-data-model.md) para los tipos y el modelo de datos de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="de6c8-231">See the [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="de6c8-232">Notifique [eventos y métricas](app-insights-api-custom-events-metrics.md) personalizados a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="de6c8-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) to Application Insights.</span></span>
- <span data-ttu-id="de6c8-233">Compruebe la [configuración](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) de la recopilación de propiedades de contexto.</span><span class="sxs-lookup"><span data-stu-id="de6c8-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="de6c8-234">Consulte el [manual del usuario de System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) para ver cómo se correlaciona la telemetría.</span><span class="sxs-lookup"><span data-stu-id="de6c8-234">Check the [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) to see how we correlate telemetry.</span></span>
