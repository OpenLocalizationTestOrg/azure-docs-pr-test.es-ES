---
title: las colas de mensajes no enviados de Bus aaaService | Documentos de Microsoft
description: "Información general de colas de mensajes fallidos del Bus de servicio de Azure"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>Información general de colas de mensajes fallidos del Bus de servicio

Las colas de Service Bus y las suscripciones a temas proporcionan una subcola secundaria, llamada *cola de mensajes fallidos* (DLQ). cola de mensajes no enviados de Hello no necesita toobe creado explícitamente y no puede ser eliminada o de otra manera independiente administrado de la entidad principal de Hola.

En este artículo se describen las colas de mensajes fallidos de Azure Service Bus. Gran parte del análisis de Hola se muestra en hello [ejemplo de colas de mensajes fallidos](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue) en GitHub.
 
## <a name="hello-dead-letter-queue"></a>cola de mensajes no enviados de Hola

Hola de cola de mensajes no enviados de hello sirve toohold mensajes que no se puede entregar a tooany receptor, o que no se pudieron procesar. Mensajes, a continuación, se quita de hello DLQ e inspeccionar. Una aplicación podría, con ayuda de un operador, corregir los problemas y reenviar mensaje de bienvenida, registra que se produjo un error el hecho de Hola y tomar medidas correctivas. 

Desde una perspectiva de API y el protocolo, Hola DLQ es principalmente similar tooany otra cola, excepto en que sólo se pueden enviar mensajes mediante gestos de mensajes no enviados de Hola de entidad primaria de Hola. Además, no se observa el período de vida, y no puede tratar como fallido un mensaje desde una cola de mensajes fallidos. cola de mensajes no enviados de Hello es totalmente compatible con las operaciones transaccionales y entrega de bloqueo.

Tenga en cuenta que no hay ninguna limpieza automática de hello DLQ. Los mensajes permanecen en hello DLQ hasta que los recupera explícitamente de hello DLQ y llame al método [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) en el mensaje de bienvenida de mensajes no enviados.

## <a name="moving-messages-toohello-dlq"></a>Mover mensajes toohello DLQ

Hay varias actividades en Service Bus que provocan tooget mensajes insertado toohello DLQ desde dentro de hello propio motor de mensajería. Una aplicación explícitamente también puede mover mensajes toohello DLQ. 

A medida que obtiene mover mensaje de bienvenida de broker de hello, dos propiedades se agregan toohello mensaje como broker Hola llama a su versión interna de hello [mensajes fallidos](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) método en el mensaje de bienvenida: `DeadLetterReason` y `DeadLetterErrorDescription`.

Las aplicaciones pueden definir sus propios códigos de hello `DeadLetterReason` propiedad pero Hola sistema conjuntos Hola después de valores.

| Condición | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| Siempre |HeaderSizeExceeded |se superó la cuota de tamaño de Hola para esta secuencia. |
| !TopicDescription.<br />EnableFilteringMessagesBeforePublishing and SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |exception.GetType().Name |exception.Message |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |mensaje de saludo expirado y cuellos se fallido. |
| SubscriptionDescription.RequiresSession |El identificador de sesión es null. |La entidad habilitada por sesión no permite un mensaje cuyo identificador de sesión es null. |
| !cola de mensajes fallidos |MaxTransferHopCountExceeded |Null |
| Mensajes fallidos explícitos de aplicación |Especificado por la aplicación |Especificado por la aplicación |

## <a name="exceeding-maxdeliverycount"></a>Superación de MaxDeliveryCount
Las colas y las suscripciones tienen un [QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) y [SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount) propiedad respectivamente; hello valor predeterminado es 10. Cada vez que se ha entregado un mensaje con un bloqueo ([ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)), pero se ha ya sea explícitamente abandona o ha caducado el bloqueo de hello, mensaje de saludo [BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) es se incrementa. Cuando [DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) supera [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount), mensaje de bienvenida es movida toohello DLQ, especificar hello `MaxDeliveryCountExceeded` código de motivo.

No se puede deshabilitar este comportamiento, pero puede establecer [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) tooa gran número.

## <a name="exceeding-timetolive"></a>Superación de TimeToLive
Cuando Hola [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) o [SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration) propiedad se establece demasiado**true** (valor predeterminado de hello es **false**), todos los mensajes que van a expirar son movida toohello DLQ, especificar hello `TTLExpiredException` código de motivo.

Tenga en cuenta que los mensajes caducados se purgan solo y, por tanto, moverse toohello DLQ cuando hay al menos un destinatario active extraer en cola principal de Hola o suscripción; Este comportamiento es así por diseño.

## <a name="errors-while-processing-subscription-rules"></a>Errores al procesar reglas de suscripción
Cuando Hola [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions) propiedad está habilitada para una suscripción, se capturan los errores que se producen mientras se ejecuta la regla de filtro SQL de una suscripción en hello DLQ junto con el mensaje de Hola.

## <a name="application-level-dead-lettering"></a>Mensajes fallidos de nivel de aplicación
En suma toohello proporcionado por el sistema colas de mensajes fallidos características, las aplicaciones pueden utilizar mensajes de inaceptable de rechazo de hello DLQ tooexplicitly. Esto puede incluir los mensajes que no se puede procesar correctamente debido ordenación tooany del problema del sistema, mensajes que contienen cargas con formato incorrecto o que no superen la autenticación cuando se utiliza algún esquema de seguridad de nivel de mensaje.

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>Colas de mensajes fallidos en escenarios ForwardTo o SendVia

Mensajes serán cola de mensajes no enviados de transferencia toohello enviados en hello condiciones siguientes:

- Un mensaje pasa a través de más de 3 colas o temas que están [encadenados](service-bus-auto-forwarding.md).
- cola de destino de Hola o tema esté deshabilitado o eliminado.
- Hola destino cola o tema supera el tamaño máximo de entidad de Hola.

tooretrieve estos mensajes fallido, puede crear un receptor con hello [FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_) método de utilidad.

## <a name="example"></a>Ejemplo
Hola siguiente fragmento de código crea un receptor del mensaje. Hola recibir un bucle para la cola principal hello, código de hello recupera mensajes de bienvenida con [Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_), que le pregunta Hola broker tooinstantly devuelto ningún mensaje estén disponible o tooreturn con ningún resultado. Si el código de hello recibe un mensaje, inmediatamente abandona, que se incrementa hello `DeliveryCount`. Una vez que el sistema de hello mueve toohello de mensaje de Hola DLQ, cola principal Hola está vacía y Hola sale del bucle, como [ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_) devuelve **null**.

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
Vea Hola siguientes artículos para obtener más información acerca de las colas de Bus de servicio:

* [Introducción a las colas de Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Comparación de colas de Azure y colas de Service Bus](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

