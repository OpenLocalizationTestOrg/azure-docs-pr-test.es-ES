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
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="cee94-103">Introducción a la API estándar de .NET de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cee94-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="cee94-104">En este artículo se resume algunas de las API de cliente .NET de concentradores de eventos estándar de clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="cee94-104">This article summarizes some of hello key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="cee94-105">Actualmente existen dos bibliotecas de cliente estándar .NET:</span><span class="sxs-lookup"><span data-stu-id="cee94-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="cee94-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="cee94-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="cee94-107">Esta biblioteca proporciona todas las operaciones básicas en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="cee94-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="cee94-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="cee94-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="cee94-109">Esta biblioteca agrega una funcionalidad adicional que permite realizar el seguimiento de los eventos procesados y es hello tooread de manera más sencilla de un concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="cee94-109">This library adds additional functionality that allows for keeping track of processed events, and is hello easiest way tooread from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="cee94-110">Cliente de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cee94-110">Event Hubs client</span></span>
<span data-ttu-id="cee94-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) se hello objeto principal, usar eventos toosend, crear destinatarios y tooget información en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="cee94-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primary object you use toosend events, create receivers, and tooget run-time information.</span></span> <span data-ttu-id="cee94-112">Este cliente es vinculado tooa centro de eventos determinado y crea un nuevo extremo de los centros de eventos de toohello de conexión.</span><span class="sxs-lookup"><span data-stu-id="cee94-112">This client is linked tooa particular event hub, and creates a new connection toohello Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="cee94-113">Creación de un cliente de Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="cee94-113">Create an Event Hubs client</span></span>
<span data-ttu-id="cee94-114">Se crea un objeto [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) a partir de una cadena de conexión.</span><span class="sxs-lookup"><span data-stu-id="cee94-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="cee94-115">tooinstantiate de manera más sencilla de Hello un nuevo cliente se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="cee94-115">hello simplest way tooinstantiate a new client is shown in hello following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="cee94-116">tooprogrammatically Editar cadena de conexión de hello, puede usar hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) clase y pasar la cadena de conexión de Hola como un parámetro demasiado[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="cee94-116">tooprogrammatically edit hello connection string, you can use hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass hello connection string as a parameter too[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="cee94-117">Envío de eventos</span><span class="sxs-lookup"><span data-stu-id="cee94-117">Send events</span></span>
<span data-ttu-id="cee94-118">Centro de eventos tooan toosend eventos, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) clase.</span><span class="sxs-lookup"><span data-stu-id="cee94-118">toosend events tooan event hub, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="cee94-119">Hola cuerpo debe ser un `byte` matriz, o un `byte` segmento de la matriz.</span><span class="sxs-lookup"><span data-stu-id="cee94-119">hello body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="cee94-120">Recepción de eventos</span><span class="sxs-lookup"><span data-stu-id="cee94-120">Receive events</span></span>
<span data-ttu-id="cee94-121">Hola recomendada eventos de forma tooreceive desde los centros de eventos usa hello [Host procesador de eventos](#event-processor-host-apis), que proporciona funcionalidad tooautomatically realizar un seguimiento del desplazamiento e información de partición.</span><span class="sxs-lookup"><span data-stu-id="cee94-121">hello recommended way tooreceive events from Event Hubs is using hello [Event Processor Host](#event-processor-host-apis), which provides functionality tooautomatically keep track of offset, and partition information.</span></span> <span data-ttu-id="cee94-122">Sin embargo, hay algunas situaciones en las que puede que desee flexibilidad de hello toouse de eventos tooreceive de la biblioteca de los centros de eventos principales de Hola.</span><span class="sxs-lookup"><span data-stu-id="cee94-122">However, there are certain situations in which you may want toouse hello flexibility of hello core Event Hubs library tooreceive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="cee94-123">Creación de un receptor</span><span class="sxs-lookup"><span data-stu-id="cee94-123">Create a receiver</span></span>
<span data-ttu-id="cee94-124">Receptores son particiones toospecific relacionados, por lo que en orden tooreceive todos los eventos en un centro de eventos, deberá toocreate varias instancias.</span><span class="sxs-lookup"><span data-stu-id="cee94-124">Receivers are tied toospecific partitions, so in order tooreceive all events in an event hub, you will need toocreate multiple instances.</span></span> <span data-ttu-id="cee94-125">Por lo general, es una buena práctica tooget Hola partición información mediante programación, en lugar de Id. de partición Hola de codificar de forma rígida.</span><span class="sxs-lookup"><span data-stu-id="cee94-125">Generally speaking, it is a good practice tooget hello partition information programatically, rather than hard-coding hello partition ids.</span></span> <span data-ttu-id="cee94-126">En Ordenar toodo esto, puede usar hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) método.</span><span class="sxs-lookup"><span data-stu-id="cee94-126">In order toodo so, you can use hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

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

<span data-ttu-id="cee94-127">Dado que eventos nunca se quitan de un concentrador de eventos (y solo caducan), deberá punto de partida adecuado toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="cee94-127">Since events are never removed from an event hub (and only expire), you need toospecify hello proper starting point.</span></span> <span data-ttu-id="cee94-128">Hello en el ejemplo siguiente se muestra las combinaciones posibles.</span><span class="sxs-lookup"><span data-stu-id="cee94-128">hello following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="cee94-129">Consumo de un evento</span><span class="sxs-lookup"><span data-stu-id="cee94-129">Consume an event</span></span>
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

## <a name="event-processor-host-apis"></a><span data-ttu-id="cee94-130">API de host del procesador de eventos</span><span class="sxs-lookup"><span data-stu-id="cee94-130">Event Processor Host APIs</span></span>
<span data-ttu-id="cee94-131">Estas API ofrecen procesos de tooworker de resistencia que podrían no estar disponibles, mediante la distribución de particiones a través de los trabajadores disponibles.</span><span class="sxs-lookup"><span data-stu-id="cee94-131">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

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

<span data-ttu-id="cee94-132">Hello siguiente es una implementación de ejemplo de Hola [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="cee94-132">hello following is a sample implementation of hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cee94-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cee94-133">Next steps</span></span>
<span data-ttu-id="cee94-134">toolearn más información acerca de escenarios de centros de eventos, visite estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="cee94-134">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="cee94-135">¿Qué es Centros de eventos de Azure?</span><span class="sxs-lookup"><span data-stu-id="cee94-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="cee94-136">API disponibles de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cee94-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="cee94-137">referencias de API de .NET de Hello son aquí:</span><span class="sxs-lookup"><span data-stu-id="cee94-137">hello .NET API references are here:</span></span>

* [<span data-ttu-id="cee94-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="cee94-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="cee94-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="cee94-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)