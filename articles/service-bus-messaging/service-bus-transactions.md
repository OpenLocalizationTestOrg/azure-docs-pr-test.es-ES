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
# <a name="overview-of-service-bus-transaction-processing"></a>Información general sobre el procesamiento de transacciones del Bus de servicio
Este artículo describe las capacidades de transacción de Hola de Bus de servicio de Azure. Gran parte del análisis de Hola se muestra en hello [transacciones atómicas con ejemplo de Bus de servicio](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions). Este artículo es información general de tooan limitado de procesamiento de transacciones y hello *enviar a través de* característica de Bus de servicio, mientras que muestra de Hola a las transacciones atómicas es más amplios y complejos en el ámbito.

## <a name="transactions-in-service-bus"></a>Transacciones en el Bus de servicio
Una [transacción](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) agrupa dos o más operaciones en un *ámbito de ejecución*. Por naturaleza, una transacción debe asegurarse de que todas las operaciones que pertenecen tooa dado grupo de operaciones ejecutan correcta o incorrectamente conjuntamente. En este sentido transacciones actúan como una unidad, que a menudo es que se hace referencia tooas *atomicidad*. 

El Bus de servicio es un agente de mensajes transaccional, y garantiza la integridad transaccional de todas las operaciones internas en sus almacenes de mensajes. Todas las transferencias de mensajes dentro de Bus de servicio, como mover tooa mensajes [cola de mensajes no enviados](service-bus-dead-letter-queues.md) o [reenvío automático](service-bus-auto-forwarding.md) de mensajes entre las entidades, son transaccionales. Por lo tanto, si el Bus de servicio acepta un mensaje, es que ya se ha almacenado y etiquetado con un número de secuencia. Desde ese momento, las transferencias de mensajes dentro de Bus de servicio son operaciones coordinadas en entidades, y ninguna de ellas, se llevará tooloss (origen se realiza correctamente y se produce un error de destino) o tooduplication (se produce un error de origen y destino se realiza correctamente) del mensaje de bienvenida.

Bus de servicio admite las operaciones de agrupación en una única entidad de mensajería (cola, tema, suscripción) dentro del ámbito de Hola de una transacción. Por ejemplo, puede enviar varias colas de tooone de mensajes desde dentro de un ámbito de transacción y mensajes de saludo sólo estará el registro de la cola de toohello confirmada cuando Hola transacción se complete correctamente.

## <a name="operations-within-a-transaction-scope"></a>Operaciones dentro de un ámbito de transacción
las operaciones de Hola que se pueden realizar en un ámbito de transacción son los siguientes:

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync 

Recibir operaciones no se incluyen, como se supone que la aplicación hello adquiere mensajes mediante hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) el bucle de recepción de modo, dentro de algunas o con un [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) devolución de llamada, y de ámbito solo, a continuación, se abre una transacción para procesar el mensaje Hola.

Hello disposición de mensaje de Hola (completo, abandono, mensajes no enviados, aplazar), a continuación, se produce dentro de ámbito de Hola de y dependiente de la sesión, hello resultado global de transacción de Hola.

## <a name="transfers-and-send-via"></a>Transferencias y "enviar por"
tooenable entrega transaccional de los datos de un procesador de tooa de cola y, a continuación, una cola de tooanother, Service Bus admite *transferencias*. Durante una operación de transferencia, un remitente envía primero una tooa mensaje "cola de transferencia" y cola de transferencias de hello cambia inmediatamente toohello de mensaje de Hola pensado cola de destino utilizando Hola mismo sólida transferencia de implementación que se basa la capacidad de reenvío automático de Hola en. mensaje de saludo nunca es registro de la cola de transferencia toohello confirma de forma que resulta visible para los consumidores de la cola de transferencia de Hola.

potencia de Hola de esta capacidad transaccional queda patente cuando propia cola de transferencia hello es el origen de Hola de mensajes de entrada del remitente de Hola. En otras palabras, Bus de servicio puede transferir cola de destino de toohello de mensajes de Hola "a través de" cola de transferencia de hello, al realizar una completa (o aplazar, o de mensajes no enviados) operación en el mensaje de entrada de hello, todo en una operación atómica. 

### <a name="see-it-in-code"></a>Verlo en el código
tooset de dichas transferencias, cree el remitente de un mensaje destinado a la cola de destino de Hola a través de la cola de transferencias de Hola. También habrá un receptor que extrae los mensajes de esa misma cola. Por ejemplo:

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

Una transacción simple, a continuación, utiliza los siguientes elementos, como en el siguiente ejemplo de Hola:

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

## <a name="next-steps"></a>Pasos siguientes

Vea Hola siguientes artículos para obtener más información acerca de las colas de Bus de servicio:

* [Encadenamiento de entidades de Service Bus con reenvío automático](service-bus-auto-forwarding.md)
* [Ejemplo de reenvío automático](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [Ejemplo de transacciones atómicas con Service Bus](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [Comparación de colas de Azure y colas de Service Bus](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [¿Cómo toouse colas de Service Bus](service-bus-dotnet-get-started-with-queues.md)

