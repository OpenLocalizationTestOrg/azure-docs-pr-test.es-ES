---
title: "aaaOverview de hello Azure eventos centros de .NET estándar API | Documentos de Microsoft"
description: "Introducción a la API estándar de .NET"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a>Introducción a la API estándar de .NET de Event Hubs
En este artículo se resume algunas de las API de cliente .NET de concentradores de eventos estándar de clave de Hola. Actualmente existen dos bibliotecas de cliente estándar .NET:
* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
  *  Esta biblioteca proporciona todas las operaciones básicas en tiempo de ejecución.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
  * Esta biblioteca agrega una funcionalidad adicional que permite realizar el seguimiento de los eventos procesados y es hello tooread de manera más sencilla de un concentrador de eventos.

## <a name="event-hubs-client"></a>Cliente de Event Hubs
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) se hello objeto principal, usar eventos toosend, crear destinatarios y tooget información en tiempo de ejecución. Este cliente es vinculado tooa centro de eventos determinado y crea un nuevo extremo de los centros de eventos de toohello de conexión.

### <a name="create-an-event-hubs-client"></a>Creación de un cliente de Centro de eventos
Se crea un objeto [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) a partir de una cadena de conexión. tooinstantiate de manera más sencilla de Hello un nuevo cliente se muestra en el siguiente ejemplo de Hola:

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

tooprogrammatically Editar cadena de conexión de hello, puede usar hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) clase y pasar la cadena de conexión de Hola como un parámetro demasiado[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>Envío de eventos
Centro de eventos tooan toosend eventos, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) clase. Hola cuerpo debe ser un `byte` matriz, o un `byte` segmento de la matriz.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>Recepción de eventos
Hola recomendada eventos de forma tooreceive desde los centros de eventos usa hello [Host procesador de eventos](#event-processor-host-apis), que proporciona funcionalidad tooautomatically realizar un seguimiento del desplazamiento e información de partición. Sin embargo, hay algunas situaciones en las que puede que desee flexibilidad de hello toouse de eventos tooreceive de la biblioteca de los centros de eventos principales de Hola.

#### <a name="create-a-receiver"></a>Creación de un receptor
Receptores son particiones toospecific relacionados, por lo que en orden tooreceive todos los eventos en un centro de eventos, deberá toocreate varias instancias. Por lo general, es una buena práctica tooget Hola partición información mediante programación, en lugar de Id. de partición Hola de codificar de forma rígida. En Ordenar toodo esto, puede usar hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) método.

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

Dado que eventos nunca se quitan de un concentrador de eventos (y solo caducan), deberá punto de partida adecuado toospecify Hola. Hello en el ejemplo siguiente se muestra las combinaciones posibles.

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>Consumo de un evento
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a>API de host del procesador de eventos
Estas API ofrecen procesos de tooworker de resistencia que podrían no estar disponibles, mediante la distribución de particiones a través de los trabajadores disponibles.

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

Hello siguiente es una implementación de ejemplo de Hola [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de escenarios de centros de eventos, visite estos vínculos:

* [¿Qué es Centros de eventos de Azure?](event-hubs-what-is-event-hubs.md)
* [API disponibles de Event Hubs](event-hubs-api-overview.md)

referencias de API de .NET de Hello son aquí:

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)