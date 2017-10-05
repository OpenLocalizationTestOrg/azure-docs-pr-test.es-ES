---
title: "Introducción al procesamiento de transacciones en Azure Service Bus| Microsoft Docs"
description: "Información general sobre las transacciones atómicas del Bus de servicio de Azure y la característica \"enviar por\""
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: a88f2d81ab43e38c9363a67aaefc178b47bfb259
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="8933b-103">Información general sobre el procesamiento de transacciones del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="8933b-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="8933b-104">En este artículo se describe las funcionalidades de transacciones del Bus de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="8933b-104">This article discusses the transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="8933b-105">Gran parte de la discusión se ilustra mediante el [ejemplo de transacciones atómicas con Service Bus](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="8933b-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="8933b-106">Este artículo se limita a proporcionar información general sobre el procesamiento de transacciones y la característica *Enviar por* de Service Bus, mientras que el ejemplo de transacciones atómicas es más amplio y con un ámbito más complejo.</span><span class="sxs-lookup"><span data-stu-id="8933b-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="8933b-107">Transacciones en el Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="8933b-107">Transactions in Service Bus</span></span>
<span data-ttu-id="8933b-108">Una [transacción](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) agrupa dos o más operaciones en un *ámbito de ejecución*.</span><span class="sxs-lookup"><span data-stu-id="8933b-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="8933b-109">Por naturaleza, una transacción de este tipo debe garantizar que todas las operaciones que pertenecen a un grupo determinado de operaciones tendrán éxito o darán error de forma conjunta.</span><span class="sxs-lookup"><span data-stu-id="8933b-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="8933b-110">En este sentido, las transacciones actúan como una unidad, lo que a menudo se conoce como *atomicidad*.</span><span class="sxs-lookup"><span data-stu-id="8933b-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span></span> 

<span data-ttu-id="8933b-111">El Bus de servicio es un agente de mensajes transaccional, y garantiza la integridad transaccional de todas las operaciones internas en sus almacenes de mensajes.</span><span class="sxs-lookup"><span data-stu-id="8933b-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="8933b-112">Todas las transferencias de mensajes dentro de Service Bus, como mover mensajes a una [cola de mensajes fallidos](service-bus-dead-letter-queues.md) o [reenviar automáticamente](service-bus-auto-forwarding.md) mensajes entre entidades, son transaccionales.</span><span class="sxs-lookup"><span data-stu-id="8933b-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="8933b-113">Por lo tanto, si el Bus de servicio acepta un mensaje, es que ya se ha almacenado y etiquetado con un número de secuencia.</span><span class="sxs-lookup"><span data-stu-id="8933b-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="8933b-114">Desde ese momento, todas las transferencias de mensajes dentro del Bus de servicio son operaciones coordinadas entre entidades, y ninguna de ellas dará lugar a la pérdida (el origen tiene éxito y el destino da error) o a la desduplicación (el origen da error y el destino tiene éxito) del mensaje.</span><span class="sxs-lookup"><span data-stu-id="8933b-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span></span>

<span data-ttu-id="8933b-115">Service Bus admite operaciones de agrupación en una sola entidad de mensajería (cola, tema, suscripción) dentro del ámbito de una transacción.</span><span class="sxs-lookup"><span data-stu-id="8933b-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span></span> <span data-ttu-id="8933b-116">Por ejemplo, puede enviar varios mensajes a una cola desde dentro de un ámbito de transacción y los mensajes solo se confirmarán en el registro de la cola cuando la transacción se complete correctamente.</span><span class="sxs-lookup"><span data-stu-id="8933b-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="8933b-117">Operaciones dentro de un ámbito de transacción</span><span class="sxs-lookup"><span data-stu-id="8933b-117">Operations within a transaction scope</span></span>
<span data-ttu-id="8933b-118">Las operaciones que pueden realizarse dentro de un ámbito de transacción son las siguientes:</span><span class="sxs-lookup"><span data-stu-id="8933b-118">The operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="8933b-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="8933b-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="8933b-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="8933b-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="8933b-121">Las operaciones de recepción no se incluyen, porque se supone que la aplicación captura mensajes mediante el modo [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode), dentro de algún bucle de recepción o con una devolución de llamada [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_), y solo entonces se abre un ámbito de transacción para procesar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="8933b-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing the message.</span></span>

<span data-ttu-id="8933b-122">La disposición del mensaje (completar, abandonar, correo devuelto, aplazar), se produce entonces dentro del ámbito del resultado general de la transacción y depende de este.</span><span class="sxs-lookup"><span data-stu-id="8933b-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="8933b-123">Transferencias y "enviar por"</span><span class="sxs-lookup"><span data-stu-id="8933b-123">Transfers and "send via"</span></span>
<span data-ttu-id="8933b-124">Para permitir la entrega transaccional de datos de una cola a un procesador y luego a otra cola, Service Bus admite *transferencias*.</span><span class="sxs-lookup"><span data-stu-id="8933b-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="8933b-125">En una operación de transferencia, un remitente envía primero un mensaje a una "cola de transferencia" y esta mueve inmediatamente el mensaje a la cola de destino deseada usando la misma implementación de transferencias sólida que la funcionalidad de reenvío automático en la que se basa.</span><span class="sxs-lookup"><span data-stu-id="8933b-125">In a transfer operation, a sender first sends a message to a "transfer queue" and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span></span> <span data-ttu-id="8933b-126">El mensaje nunca se confirma en el registro de la cola de transferencia de forma que se vuelve visible para los consumidores de dicha cola.</span><span class="sxs-lookup"><span data-stu-id="8933b-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span></span>

<span data-ttu-id="8933b-127">La eficacia de esta funcionalidad transaccional se hace evidente cuando la propia cola de transferencia es el origen de los mensajes de entrada del remitente.</span><span class="sxs-lookup"><span data-stu-id="8933b-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span></span> <span data-ttu-id="8933b-128">En otras palabras, el Bus de servicio puede transferir el mensaje a la cola de destino "mediante" la cola de transferencia y al mismo tiempo realizar una operación completa (o de aplazamiento o correo devuelto) en el mensaje de entrada, todo en una operación atómica.</span><span class="sxs-lookup"><span data-stu-id="8933b-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="8933b-129">Verlo en el código</span><span class="sxs-lookup"><span data-stu-id="8933b-129">See it in code</span></span>
<span data-ttu-id="8933b-130">Para configurar tales transferencias, se crea el remitente de un mensaje que se dirige a la cola de destino mediante la cola de transferencia.</span><span class="sxs-lookup"><span data-stu-id="8933b-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span></span> <span data-ttu-id="8933b-131">También habrá un receptor que extrae los mensajes de esa misma cola.</span><span class="sxs-lookup"><span data-stu-id="8933b-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="8933b-132">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8933b-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="8933b-133">En una transacción sencilla, se usan estos elementos, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8933b-133">A simple transaction then uses these elements, as in the following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package the result 

    msg.Complete(); // mark the message as done
    sender.Send(newmsg); // forward the result

    scope.Complete(); // declare the transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="8933b-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8933b-134">Next steps</span></span>

<span data-ttu-id="8933b-135">Consulte los siguientes artículos para más información sobre las colas de Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="8933b-135">See the following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="8933b-136">Encadenamiento de entidades de Service Bus con reenvío automático</span><span class="sxs-lookup"><span data-stu-id="8933b-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="8933b-137">Ejemplo de reenvío automático</span><span class="sxs-lookup"><span data-stu-id="8933b-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="8933b-138">Ejemplo de transacciones atómicas con Service Bus</span><span class="sxs-lookup"><span data-stu-id="8933b-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="8933b-139">Comparación de colas de Azure y colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="8933b-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="8933b-140">Utilización de las colas del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="8933b-140">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

