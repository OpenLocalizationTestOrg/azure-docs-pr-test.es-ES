---
title: "Introducción a las API de .NET Framework de Azure Event Hubs | Microsoft Docs"
description: Resumen de algunas de las principales API de cliente de .NET Framework de Event Hubs.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f3b6cc0-9600-417f-9e80-2345411bd036
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bc525e7ca8b21e9e5f1e36b3152d71420b041700
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-net-framework-api-overview"></a><span data-ttu-id="67746-103">Introducción a las API de .NET Framework de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="67746-103">Event Hubs .NET Framework API overview</span></span>
<span data-ttu-id="67746-104">Este artículo resume algunas de las principales API de cliente de .NET Framework de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="67746-104">This article summarizes some of the key Event Hubs .NET Framework client APIs.</span></span> <span data-ttu-id="67746-105">Existen dos categorías: API de administración y de tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="67746-105">There are two categories: management and run-time APIs.</span></span> <span data-ttu-id="67746-106">Las API de tiempo de ejecución están compuestas por todas las operaciones necesarias para enviar y recibir un mensaje.</span><span class="sxs-lookup"><span data-stu-id="67746-106">Run-time APIs consist of all operations needed to send and receive a message.</span></span> <span data-ttu-id="67746-107">Las operaciones de administración le permiten administrar un estado de entidad de centros de eventos mediante la creación, actualización y eliminación de entidades.</span><span class="sxs-lookup"><span data-stu-id="67746-107">Management operations enable you to manage an Event Hubs entity state by creating, updating, and deleting entities.</span></span>

<span data-ttu-id="67746-108">Los escenarios de supervisión abarcan la administración y el tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="67746-108">Monitoring scenarios span both management and run-time.</span></span> <span data-ttu-id="67746-109">Para obtener documentación de referencia detallada sobre las API de .NET, consulte las referencias [.NET de Service Bus](/dotnet/api/microsoft.servicebus.messaging) y [API de EventProcessorHost](/dotnet/api/microsoft.azure.eventhubs.processor).</span><span class="sxs-lookup"><span data-stu-id="67746-109">For detailed reference documentation on the .NET APIs, see the [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) and [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) references.</span></span>

## <a name="management-apis"></a><span data-ttu-id="67746-110">API de administración</span><span class="sxs-lookup"><span data-stu-id="67746-110">Management APIs</span></span>
<span data-ttu-id="67746-111">Para realizar las siguientes operaciones de administración debe tener permisos de **administración** en el espacio de nombres de Centros de eventos:</span><span class="sxs-lookup"><span data-stu-id="67746-111">To perform the following management operations, you must have **Manage** permissions on the Event Hubs namespace:</span></span>

### <a name="create"></a><span data-ttu-id="67746-112">Crear</span><span class="sxs-lookup"><span data-stu-id="67746-112">Create</span></span>
```csharp
// Create the event hub
var ehd = new EventHubDescription(eventHubName);
ehd.PartitionCount = SampleManager.numPartitions;
await namespaceManager.CreateEventHubAsync(ehd);
```

### <a name="update"></a><span data-ttu-id="67746-113">Actualizar</span><span class="sxs-lookup"><span data-stu-id="67746-113">Update</span></span>
```csharp
var ehd = await namespaceManager.GetEventHubAsync(eventHubName);

// Create a customer SAS rule with Manage permissions
ehd.UserMetadata = "Some updated info";
var ruleName = "myeventhubmanagerule";
var ruleKey = SharedAccessAuthorizationRule.GenerateRandomKey();
ehd.Authorization.Add(new SharedAccessAuthorizationRule(ruleName, ruleKey, new AccessRights[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send} )); 
await namespaceManager.UpdateEventHubAsync(ehd);
```

### <a name="delete"></a><span data-ttu-id="67746-114">Eliminar</span><span class="sxs-lookup"><span data-stu-id="67746-114">Delete</span></span>
```csharp
await namespaceManager.DeleteEventHubAsync("Event Hub name");
```

## <a name="run-time-apis"></a><span data-ttu-id="67746-115">API de tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="67746-115">Run-time APIs</span></span>
### <a name="create-publisher"></a><span data-ttu-id="67746-116">Crear publicador</span><span class="sxs-lookup"><span data-stu-id="67746-116">Create publisher</span></span>
```csharp
// EventHubClient model (uses implicit factory instance, so all links on same connection)
var eventHubClient = EventHubClient.Create("Event Hub name");
```

### <a name="publish-message"></a><span data-ttu-id="67746-117">Publicar mensaje</span><span class="sxs-lookup"><span data-stu-id="67746-117">Publish message</span></span>
```csharp
// Create the device/temperature metric
var info = new MetricEvent() { DeviceId = random.Next(SampleManager.NumDevices), Temperature = random.Next(100) };
var data = new EventData(new byte[10]); // Byte array
var data = new EventData(Stream); // Stream 
var data = new EventData(info, serializer) //Object and serializer 
{
    PartitionKey = info.DeviceId.ToString()
};

// Set user properties if needed
data.Properties.Add("Type", "Telemetry_" + DateTime.Now.ToLongTimeString());

// Send single message async
await client.SendAsync(data);
```

### <a name="create-consumer"></a><span data-ttu-id="67746-118">Crear consumidor</span><span class="sxs-lookup"><span data-stu-id="67746-118">Create consumer</span></span>
```csharp
// Create the Event Hubs client
var eventHubClient = EventHubClient.Create(EventHubName);

// Get the default consumer group
var defaultConsumerGroup = eventHubClient.GetDefaultConsumerGroup();

// All messages
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index);

// From one day ago
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index, startingDateTimeUtc:DateTime.Now.AddDays(-1));

// From specific offset, -1 means oldest
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index,startingOffset:-1); 
```

### <a name="consume-message"></a><span data-ttu-id="67746-119">Consumir mensaje</span><span class="sxs-lookup"><span data-stu-id="67746-119">Consume message</span></span>
```csharp
var message = await consumer.ReceiveAsync();

// Provide a serializer
var info = message.GetBody<Type>(Serializer)

// Get a byte[]
var info = message.GetBytes(); 
msg = UnicodeEncoding.UTF8.GetString(info);
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="67746-120">API de host del procesador de eventos</span><span class="sxs-lookup"><span data-stu-id="67746-120">Event Processor Host APIs</span></span>
<span data-ttu-id="67746-121">Estas API ofrecen resistencia a los procesos de trabajo que pueden dejar de estar disponibles, distribuyendo particiones entre trabajos disponibles.</span><span class="sxs-lookup"><span data-stu-id="67746-121">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.
// Use the EventData.Offset value for checkpointing yourself, this value is unique per partition.

var eventHubConnectionString = System.Configuration.ConfigurationManager.AppSettings["Microsoft.ServiceBus.ConnectionString"];
var blobConnectionString = System.Configuration.ConfigurationManager.AppSettings["AzureStorageConnectionString"]; // Required for checkpoint/state

var eventHubDescription = new EventHubDescription(EventHubName);
var host = new EventProcessorHost(WorkerName, EventHubName, defaultConsumerGroup.GroupName, eventHubConnectionString, blobConnectionString);
await host.RegisterEventProcessorAsync<SimpleEventProcessor>();

// To close
await host.UnregisterEventProcessorAsync();
```

<span data-ttu-id="67746-122">La interfaz [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) se define de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="67746-122">The [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    IDictionary<string, string> map;
    PartitionContext partitionContext;

    public SimpleEventProcessor()
    {
        this.map = new Dictionary<string, string>();
    }

    public Task OpenAsync(PartitionContext context)
    {
        this.partitionContext = context;

        return Task.FromResult<object>(null);
    }

    public async Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData message in messages)
        {
            // Process messages here
        }

        // Checkpoint when appropriate
        await context.CheckpointAsync();

    }

    public async Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="67746-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="67746-123">Next steps</span></span>
<span data-ttu-id="67746-124">Para obtener más información acerca de los escenarios de los centros de eventos, visite estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="67746-124">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="67746-125">¿Qué es Centros de eventos de Azure?</span><span class="sxs-lookup"><span data-stu-id="67746-125">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="67746-126">Guía de programación de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="67746-126">Event Hubs programming guide</span></span>](event-hubs-programming-guide.md)

<span data-ttu-id="67746-127">A continuación se incluyen referencias de API de .NET:</span><span class="sxs-lookup"><span data-stu-id="67746-127">The .NET API references are here:</span></span>

* [<span data-ttu-id="67746-128">Microsoft.ServiceBus.Messaging</span><span class="sxs-lookup"><span data-stu-id="67746-128">Microsoft.ServiceBus.Messaging</span></span>](/dotnet/api/microsoft.servicebus.messaging)
* [<span data-ttu-id="67746-129">Microsoft.Azure.EventHubs.EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="67746-129">Microsoft.Azure.EventHubs.EventProcessorHost</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor.eventprocessorhost)
