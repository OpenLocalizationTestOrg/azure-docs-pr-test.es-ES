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
# <a name="track-custom-operations-with-application-insights-net-sdk"></a>Seguimiento de las operaciones personalizadas con el SDK de .NET para Application Insights

SDK de Azure Application Insights automáticamente pista solicitudes HTTP entrante y llama a toodependent servicios, como las solicitudes HTTP y las consultas SQL. Seguimiento y correlación de las solicitudes y las dependencias de obtener una visibilidad en la capacidad de respuesta y la confiabilidad de la aplicación completa de Hola a través de todos los microservicios que combinan esta aplicación. 

Hay una clase de patrones de aplicación que no se admiten de forma genérica. La supervisión correcta de estos patrones requiere la instrumentación manual de código. En este artículo se abordan algunos patrones que pueden requerir la instrumentación manual, como el procesamiento de colas personalizadas y la ejecución de tareas de larga duración en segundo plano.

Este documento proporciona instrucciones sobre cómo tootrack operaciones personalizadas con Hola Application Insights SDK. Esta documentación es relevante para:

- Application Insights para .NET (también conocido como Base SDK) versión 2.4+.
- Application Insights para aplicaciones web (con ASP.NET) versión 2.4+.
- Application Insights para ASP.NET Core versión 2.1+.

## <a name="overview"></a>Información general
Una operación es una parte de trabajo lógica ejecutada por una aplicación. Tiene un nombre, una hora de inicio, una duración, un resultado y un contexto de ejecución como el nombre de usuario, las propiedades y el resultado. Si la operación B inició la operación A, la operación B se establece como un elemento primario de A. Una operación solo puede tener un elemento primario, pero puede tener muchas operaciones secundarias. Para más información sobre las operaciones y la correlación de telemetría, vea [Correlación de telemetría en Azure Application Insights](application-insights-correlation.md).

Hola Application Insights .NET SDK, la operación de Hola se describe mediante la clase abstracta de hello [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) y sus descendientes [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) y [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).

## <a name="incoming-operations-tracking"></a>Seguimiento de operaciones de entrada 
Hola web Application Insights que SDK recopila automáticamente las solicitudes HTTP de aplicaciones de ASP.NET que se ejecutan en una canalización IIS y todas las aplicaciones de ASP.NET Core. Hay soluciones admitidas por la comunidad para otras plataformas y marcos de trabajo. Sin embargo, si la aplicación hello no es compatible con cualquiera de estándar de Hola o soluciones admitido por la Comunidad, puede instrumentar en ella manualmente.

Otro ejemplo que requiere seguimiento personalizado es trabajo Hola que recibe los elementos de cola de Hola. En algunas colas Hola llama a tooadd un mensaje a la cola de toothis se realiza un seguimiento como una dependencia. Sin embargo, operaciones de nivel superior de Hola que describe el procesamiento de mensajes no se recopilan automáticamente.

Veamos cómo se puede realizar el seguimiento de estas operaciones.

En un nivel alto, la tarea hello es toocreate `RequestTelemetry` y establezca propiedades conocidas. Una vez finalizada la operación de hello, realizar un seguimiento telemetría Hola. Hola de ejemplo siguiente muestra esta tarea.

### <a name="http-request-in-owin-self-hosted-app"></a>Solicitud HTTP en una aplicación autohospedada de Owin
En este ejemplo, seguimos hello [protocolo HTTP para la correlación](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md). Debe esperar tooreceive encabezados que se describen no existe.

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

Protocolo HTTP para la correlación de Hello también declara hello `Correlation-Context` encabezado. Pero aquí se omite para simplificar.

## <a name="queue-instrumentation"></a>Instrumentación de colas
Para la comunicación de HTTP, hemos creado un protocolo toopass detalles de correlación. Con los protocolos de algunas colas, puede pasar metadatos adicionales junto con el mensaje de bienvenida y con otros usuarios que no se puede.

### <a name="service-bus-queue"></a>Cola de Service Bus
Con hello Azure [cola de Service Bus](../service-bus-messaging/index.md), puede pasar una bolsa de propiedades junto con el mensaje de bienvenida. Usamos identificador de correlación de hello toopass.

cola de Bus de servicio de Hello usa protocolos basados en TCP. Application Insights no realiza un seguimiento automático de las operaciones de cola, por lo que se realiza manualmente. eliminación de cola de Hello operación es una API de estilo de inserción y estamos tootrack no se puede se.

#### <a name="enqueue"></a>Poner en cola

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

#### <a name="process"></a>Proceso
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

### <a name="azure-storage-queue"></a>Cola de Azure Storage
Hola siguiente ejemplo se muestra cómo hello tootrack [cola de almacenamiento de Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) operaciones y poner en correlación telemetría entre productores de hello, consumidores de Hola y el almacenamiento de Azure. 

cola de almacenamiento de Hello tiene una API de HTTP. Cola de toohello de todas las llamadas se controlan por hello recopilador de dependencia de visión de aplicación para las solicitudes HTTP.
Asegúrese de que tiene `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` en `applicationInsights.config`. Si no lo tiene, agregarlo mediante programación tal como se describe en [de filtrado y de preprocesamiento en hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).

Si configura Application Insights manualmente, asegúrese de crear e inicializar `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` de esta forma:
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

También puede toocorrelate Hola el identificador de operación de Application Insights con Id. de solicitud de almacenamiento de Hola. Para obtener información sobre cómo solicitar tooset y obtener un almacenamiento de cliente y un identificador de solicitud de servidor, consulte [supervisar, diagnosticar y solucionar problemas de almacenamiento de Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).

#### <a name="enqueue"></a>Poner en cola
Dado que las colas de almacenamiento admiten Hola API HTTP, todas las operaciones con cola de Hola se realiza automáticamente un seguimiento por Application Insights. En muchos casos, esta instrumentación debería ser suficiente. Sin embargo, toocorrelate realiza un seguimiento en el lado del consumidor de hello con seguimientos de productor, debe pasar algún contexto de correlación del mismo modo toohow lo hacemos en hello protocolo HTTP para la correlación. 

En este ejemplo, se realiza el seguimiento de hello opcional `Enqueue` operación. Puede:

 - **Correlacionar reintentos (si existe)**: tienen un elemento primario común que es hello `Enqueue` operación. En caso contrario, le realiza el seguimiento como elementos secundarios de la solicitud entrante de Hola. Si hay varias colas de toohello solicitudes lógico, puede que sea difícil toofind qué llamada generó reintentos.
 - **Poner en correlación los registros de Azure Storage (si es necesario y cuando sea necesario)**: Se hace con la telemetría de Application Insights.

Hola `Enqueue` operación es secundario de Hola de una operación de elemento primario (por ejemplo, una solicitud HTTP de entrada). llamada de dependencia de Hello HTTP es secundario Hola Hola `Enqueue` descendiente del secundario hello y operación de solicitud entrante de hello:

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

cantidad de hello tooreduce de telemetría informa de la aplicación o si no desea hello tootrack `Enqueue` operación por otras razones, use hello `Activity` API directamente:

- Crear (e iniciar) un nuevo `Activity` en lugar de iniciar la operación de Application Insights Hola. Lo hace *no* necesita tooassign ninguna propiedad en él excepto el nombre de la operación de Hola.
- Serializar `yourActivity.Id` en la carga de mensaje de Hola en lugar de `operation.Telemetry.Id`. También puede usar `Activity.Current.Id`.


#### <a name="dequeue"></a>Quitar de la cola
De igual forma demasiado`Enqueue`, una cola de almacenamiento de toohello de solicitud HTTP real se realiza automáticamente un seguimiento por Application Insights. Sin embargo, Hola `Enqueue` operación supuestamente se produce en el contexto de primario hello, como un contexto de solicitud entrante. SDK de Application Insights correlaciona automáticamente este tipo de operación (y su parte HTTP) con la solicitud primaria de Hola y otro telemetría notifica en hello mismo ámbito.

Hola `Dequeue` operación es difícil. Hola Application Insights SDK automáticamente realiza un seguimiento de las solicitudes HTTP. Sin embargo, desconoce contexto de correlación de Hola hasta que se analiza el mensaje de bienvenida. No es toocorrelate posible el mensaje Hola de Hola HTTP solicitud tooget con rest Hola de telemetría de Hola.

En muchos casos, puede que sea la cola de toohello de solicitudes HTTP de toocorrelate útil hello en otros seguimientos así. Hello ejemplo siguiente se muestra cómo toodo:

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

#### <a name="process"></a>Proceso

En el siguiente ejemplo de Hola, se traza un mensaje entrante de una manera de forma similar solicitar toohow se seguimiento HTTP entrante:

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

Del mismo modo, se pueden instrumentar otras operaciones de cola. Una operación de lectura se debe instrumentalizar de una manera similar a la de una operación de quitar de la cola. La instrumentación de las operaciones de administración de cola no es necesaria. Application Insights realiza el seguimiento de las operaciones como HTTP y en la mayoría de los casos es suficiente.

Cuando se instrumenta la eliminación del mensaje, asegúrese de que establecer operación Hola identificadores (correlación). Como alternativa, puede usar hello `Activity` API. A continuación, no es necesario tooset identificadores de operación en elementos de telemetría de hello porque Application Insights lo hace por usted:

- Crear un nuevo `Activity` después de que tiene un elemento de cola de Hola.
- Use `Activity.SetParentId(message.ParentId)` toocorrelate productor y el consumidor registros.
- Iniciar hello `Activity`.
- Realice el seguimiento de las operaciones de quitar de la cola, proceso y eliminación mediante las aplicaciones auxiliares `Start/StopOperation`. Hacerlo de hello mismo asincrónica (contexto de ejecución) de flujo de control. De esta forma, se correlacionan correctamente.
- Hola Stop `Activity`.
- Use `Start/StopOperation` o llame a la telemetría de `Track` manualmente.

### <a name="batch-processing"></a>Procesamiento por lotes
En algunas colas, se pueden quitar de la cola varios mensajes con una solicitud. Procesar mensajes de este tipo es supuestamente independiente y pertenece toohello diferentes operaciones lógicas. En este caso, no es posible toocorrelate hello `Dequeue` procesamiento de mensajes de operación tooparticular.

Cada mensaje debe procesarse en su propio flujo de control asincrónico. Para obtener más información, vea hello [dependencias saliente seguimiento](#outgoing-dependencies-tracking) sección.

## <a name="long-running-background-tasks"></a>Tareas en segundo plano de ejecución prolongada
Algunas aplicaciones inician operaciones de larga ejecución que es posible que se deban a solicitudes del usuario. Desde la perspectiva de instrumentación de seguimiento/hello, no es diferente de la instrumentación de solicitud o dependencia: 

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

En este ejemplo, utilizamos `telemetryClient.StartOperation` toocreate `RequestTelemetry` y el contexto de correlación de Hola de relleno. Supongamos que tiene una operación primario que se creó por solicitudes entrantes que Hola operación programada. Siempre que `BackgroundTask` se inicia en Hola mismo flujo de control asincrónico como una solicitud entrante, se correlaciona con esa operación primario. `BackgroundTask`y todos los elementos de telemetría anidada automáticamente están correlacionados con la solicitud de Hola que lo causó, incluso después de que finalice la solicitud de Hola.

Cuando inicia la tarea hello de subproceso en segundo plano Hola que no tiene ninguna operación (`Activity`) asociados a él, `BackgroundTask` no tiene ningún primario. Pero puede tener operaciones anidadas. Todos los elementos de telemetría registrados en la tarea hello están correlacionado toohello `RequestTelemetry` creado en `BackgroundTask`.

## <a name="outgoing-dependencies-tracking"></a>Seguimiento de dependencias de salida
Puede realizar el seguimiento de su propio tipo de dependencia o de una operación que no es compatible con Application Insights.

Hola `Enqueue` método en cola de Bus de servicio de Hola o una cola de almacenamiento de hello puede servir como ejemplos de tal seguimiento personalizado.

Hola general para seguimiento de dependencias personalizada consiste en:

- Llamar a hello `TelemetryClient.StartOperation` método (extensión) que rellena hello `DependencyTelemetry` propiedades que son necesarios para la correlación y algunas otras propiedades (hora de inicio de marca, la duración).
- Establecer otras propiedades personalizadas en hello `DependencyTelemetry`, como el nombre de Hola y cualquier otro contexto necesita.
- Realice una llamada de dependencia y espere.
- Detener la operación de hello con `StopOperation` cuando finaliza.
- Controle las excepciones.

`StopOperation`solo se detiene Hola operación que se inició. Si la operación de ejecución actual de hello no coincide con hello uno desea toostop, `StopOperation` no hace nada. Esta situación puede ocurrir si iniciar varias operaciones en paralelo en hello mismo contexto de ejecución:

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

Asegúrese de que siempre llama a `StartOperation` y ejecuta la tarea en su propio contexto:
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

## <a name="next-steps"></a>Pasos siguientes

- Obtenga información acerca de los conceptos básicos de Hola de [correlación telemetría](application-insights-correlation.md) en Application Insights.
- Vea hello [modelo de datos](application-insights-data-model.md) para el modelo de tipos y datos de Application Insights.
- Informe personalizado [eventos y métricas](app-insights-api-custom-events-metrics.md) tooApplication visión.
- Compruebe la [configuración](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) de la recopilación de propiedades de contexto.
- Comprobar hello [Guía de usuario de System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee cómo se correlacionan telemetría.
