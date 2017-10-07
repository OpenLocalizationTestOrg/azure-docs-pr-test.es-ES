---
title: aaaOverview de procesamiento de transacciones en el Bus de servicio de Azure | Documentos de Microsoft
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
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="ab54e-103">Información general sobre el procesamiento de transacciones del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="ab54e-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="ab54e-104">Este artículo describe las capacidades de transacción de Hola de Bus de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="ab54e-104">This article discusses hello transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="ab54e-105">Gran parte del análisis de Hola se muestra en hello [transacciones atómicas con ejemplo de Bus de servicio](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="ab54e-105">Much of hello discussion is illustrated by hello [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="ab54e-106">Este artículo es información general de tooan limitado de procesamiento de transacciones y hello *enviar a través de* característica de Bus de servicio, mientras que muestra de Hola a las transacciones atómicas es más amplios y complejos en el ámbito.</span><span class="sxs-lookup"><span data-stu-id="ab54e-106">This article is limited tooan overview of transaction processing and hello *send via* feature in Service Bus, while hello Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="ab54e-107">Transacciones en el Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="ab54e-107">Transactions in Service Bus</span></span>
<span data-ttu-id="ab54e-108">Una [transacción](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) agrupa dos o más operaciones en un *ámbito de ejecución*.</span><span class="sxs-lookup"><span data-stu-id="ab54e-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="ab54e-109">Por naturaleza, una transacción debe asegurarse de que todas las operaciones que pertenecen tooa dado grupo de operaciones ejecutan correcta o incorrectamente conjuntamente.</span><span class="sxs-lookup"><span data-stu-id="ab54e-109">By nature, such a transaction must ensure that all operations belonging tooa given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="ab54e-110">En este sentido transacciones actúan como una unidad, que a menudo es que se hace referencia tooas *atomicidad*.</span><span class="sxs-lookup"><span data-stu-id="ab54e-110">In this respect transactions act as one unit, which is often referred tooas *atomicity*.</span></span> 

<span data-ttu-id="ab54e-111">El Bus de servicio es un agente de mensajes transaccional, y garantiza la integridad transaccional de todas las operaciones internas en sus almacenes de mensajes.</span><span class="sxs-lookup"><span data-stu-id="ab54e-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="ab54e-112">Todas las transferencias de mensajes dentro de Bus de servicio, como mover tooa mensajes [cola de mensajes no enviados](service-bus-dead-letter-queues.md) o [reenvío automático](service-bus-auto-forwarding.md) de mensajes entre las entidades, son transaccionales.</span><span class="sxs-lookup"><span data-stu-id="ab54e-112">All transfers of messages inside of Service Bus, such as moving messages tooa [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="ab54e-113">Por lo tanto, si el Bus de servicio acepta un mensaje, es que ya se ha almacenado y etiquetado con un número de secuencia.</span><span class="sxs-lookup"><span data-stu-id="ab54e-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="ab54e-114">Desde ese momento, las transferencias de mensajes dentro de Bus de servicio son operaciones coordinadas en entidades, y ninguna de ellas, se llevará tooloss (origen se realiza correctamente y se produce un error de destino) o tooduplication (se produce un error de origen y destino se realiza correctamente) del mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="ab54e-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead tooloss (source succeeds and target fails) or tooduplication (source fails and target succeeds) of hello message.</span></span>

<span data-ttu-id="ab54e-115">Bus de servicio admite las operaciones de agrupación en una única entidad de mensajería (cola, tema, suscripción) dentro del ámbito de Hola de una transacción.</span><span class="sxs-lookup"><span data-stu-id="ab54e-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within hello scope of a transaction.</span></span> <span data-ttu-id="ab54e-116">Por ejemplo, puede enviar varias colas de tooone de mensajes desde dentro de un ámbito de transacción y mensajes de saludo sólo estará el registro de la cola de toohello confirmada cuando Hola transacción se complete correctamente.</span><span class="sxs-lookup"><span data-stu-id="ab54e-116">For example, you can send several messages tooone queue from within a transaction scope, and hello messages will only be committed toohello queue's log when hello transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="ab54e-117">Operaciones dentro de un ámbito de transacción</span><span class="sxs-lookup"><span data-stu-id="ab54e-117">Operations within a transaction scope</span></span>
<span data-ttu-id="ab54e-118">las operaciones de Hola que se pueden realizar en un ámbito de transacción son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ab54e-118">hello operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="ab54e-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="ab54e-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="ab54e-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="ab54e-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="ab54e-121">Recibir operaciones no se incluyen, como se supone que la aplicación hello adquiere mensajes mediante hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) el bucle de recepción de modo, dentro de algunas o con un [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) devolución de llamada, y de ámbito solo, a continuación, se abre una transacción para procesar el mensaje Hola.</span><span class="sxs-lookup"><span data-stu-id="ab54e-121">Receive operations are not included, because it is assumed that hello application acquires messages using hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing hello message.</span></span>

<span data-ttu-id="ab54e-122">Hello disposición de mensaje de Hola (completo, abandono, mensajes no enviados, aplazar), a continuación, se produce dentro de ámbito de Hola de y dependiente de la sesión, hello resultado global de transacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab54e-122">hello disposition of hello message (complete, abandon, dead-letter, defer) then occurs within hello scope of, and dependent on, hello overall outcome of hello transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="ab54e-123">Transferencias y "enviar por"</span><span class="sxs-lookup"><span data-stu-id="ab54e-123">Transfers and "send via"</span></span>
<span data-ttu-id="ab54e-124">tooenable entrega transaccional de los datos de un procesador de tooa de cola y, a continuación, una cola de tooanother, Service Bus admite *transferencias*.</span><span class="sxs-lookup"><span data-stu-id="ab54e-124">tooenable transactional handover of data from a queue tooa processor, and then tooanother queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="ab54e-125">Durante una operación de transferencia, un remitente envía primero una tooa mensaje "cola de transferencia" y cola de transferencias de hello cambia inmediatamente toohello de mensaje de Hola pensado cola de destino utilizando Hola mismo sólida transferencia de implementación que se basa la capacidad de reenvío automático de Hola en.</span><span class="sxs-lookup"><span data-stu-id="ab54e-125">In a transfer operation, a sender first sends a message tooa "transfer queue" and hello transfer queue immediately moves hello message toohello intended destination queue using hello same robust transfer implementation that hello auto-forward capability relies on.</span></span> <span data-ttu-id="ab54e-126">mensaje de saludo nunca es registro de la cola de transferencia toohello confirma de forma que resulta visible para los consumidores de la cola de transferencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab54e-126">hello message is never committed toohello transfer queue's log in a way that it becomes visible for hello transfer queue's consumers.</span></span>

<span data-ttu-id="ab54e-127">potencia de Hola de esta capacidad transaccional queda patente cuando propia cola de transferencia hello es el origen de Hola de mensajes de entrada del remitente de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab54e-127">hello power of this transactional capability becomes apparent when hello transfer queue itself is hello source of hello sender's input messages.</span></span> <span data-ttu-id="ab54e-128">En otras palabras, Bus de servicio puede transferir cola de destino de toohello de mensajes de Hola "a través de" cola de transferencia de hello, al realizar una completa (o aplazar, o de mensajes no enviados) operación en el mensaje de entrada de hello, todo en una operación atómica.</span><span class="sxs-lookup"><span data-stu-id="ab54e-128">In other words, Service Bus can transfer hello message toohello destination queue "via" hello transfer queue, while performing a complete (or defer, or dead-letter) operation on hello input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="ab54e-129">Verlo en el código</span><span class="sxs-lookup"><span data-stu-id="ab54e-129">See it in code</span></span>
<span data-ttu-id="ab54e-130">tooset de dichas transferencias, cree el remitente de un mensaje destinado a la cola de destino de Hola a través de la cola de transferencias de Hola.</span><span class="sxs-lookup"><span data-stu-id="ab54e-130">tooset up such transfers, you create a message sender that targets hello destination queue via hello transfer queue.</span></span> <span data-ttu-id="ab54e-131">También habrá un receptor que extrae los mensajes de esa misma cola.</span><span class="sxs-lookup"><span data-stu-id="ab54e-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="ab54e-132">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ab54e-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="ab54e-133">Una transacción simple, a continuación, utiliza los siguientes elementos, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="ab54e-133">A simple transaction then uses these elements, as in hello following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="ab54e-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ab54e-134">Next steps</span></span>

<span data-ttu-id="ab54e-135">Vea Hola siguientes artículos para obtener más información acerca de las colas de Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="ab54e-135">See hello following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="ab54e-136">Encadenamiento de entidades de Service Bus con reenvío automático</span><span class="sxs-lookup"><span data-stu-id="ab54e-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="ab54e-137">Ejemplo de reenvío automático</span><span class="sxs-lookup"><span data-stu-id="ab54e-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="ab54e-138">Ejemplo de transacciones atómicas con Service Bus</span><span class="sxs-lookup"><span data-stu-id="ab54e-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="ab54e-139">Comparación de colas de Azure y colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="ab54e-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="ab54e-140">¿Cómo toouse colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="ab54e-140">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

