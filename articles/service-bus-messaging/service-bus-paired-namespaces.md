---
title: aaaAzure Service Bus empareja los espacios de nombres | Documentos de Microsoft
description: "Detalles de la implementación y costos de los espacios de nombres emparejados"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2440c8d3-ed2e-47e0-93cf-ab7fbb855d2e
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 4c44b2b95d2228e1ad8075b52634d88a1593d3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="paired-namespace-implementation-details-and-cost-implications"></a>Detalles de implementación y costos asociados de los espacios de nombres emparejados
Hola [PairNamespaceAsync] [ PairNamespaceAsync] método, con un [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] de la instancia, realiza tareas visibles en su nombre. Dado que existen consideraciones de coste al usar la característica de hello, es útil toounderstand las tareas para que se espere el comportamiento de hello cuando esto ocurre. Hola API involucra Hola siguiendo el comportamiento automático en su nombre:

* Creación de colas de trabajos pendientes.
* Creación de un [MessageSender] [ MessageSender] objeto que habla tooqueues o temas.
* Cuando una entidad de mensajería deja de estar disponible, envía los mensajes ping toohello entidad en un intento de toodetect cuando esa entidad vuelve a estar disponible.
* Opcionalmente, crea un conjunto de "bombeos de mensajes" que mueva los mensajes de Hola colas principales de toohello de colas de trabajo pendiente.
* Coordina el cierre o error de hello principal y secundaria [MessagingFactory] [ MessagingFactory] instancias.

En un nivel alto, característica de hello funciona del siguiente modo: cuando la entidad principal de hello sea correcta, se produce ningún cambio de comportamiento. Cuando Hola [FailoverInterval] [ FailoverInterval] ha transcurrido de duración, y entidad primaria Hola no ve ningún envía correctamente después de un usuario no transitorio [MessagingException] [ MessagingException] o un [TimeoutException][TimeoutException], Hola siguiendo el comportamiento se produce:

1. Enviar operaciones toohello principal están deshabilitados de entidad y ping de sistema de Hola Hola entidad principal hasta que los pings se entreguen correctamente.
2. Se selecciona una cola de trabajos pendientes aleatoria.
3. [BrokeredMessage] [ BrokeredMessage] objetos son enrutado toohello elegido cola de trabajos pendientes.
4. Si se produce un error en un toohello de operación de envío seleccionado cola de trabajo pendiente, se extrae esa cola de la rotación de Hola y se selecciona una nueva cola. Todos los remitentes de hello [MessagingFactory] [ MessagingFactory] instancia Obtenga información acerca del error de Hola.

Hola siguiendo las cifras representan secuencia Hola. En primer lugar, el remitente de hello envía mensajes.

![Espacios de nombres emparejados][0]

En la cola principal de error toosend toohello, remitente Hola comienza a enviar tooa mensajes elige aleatoriamente la cola de trabajos pendientes. Simultáneamente, se inicia una tarea de ping.

![Espacios de nombres emparejados][1]

En este momento mensajes de saludo siguen en la cola secundaria hello y no se han entregado toohello de cola principal. Una vez que la cola principal Hola nuevo es correcto, debe ejecutar al menos un proceso sifón Hola. sifón Hola ofrece mensajes de Hola desde distintos de trabajo pendiente de Hola todas las entidades de colas toohello destino pertinentes (colas y temas).

![Espacios de nombres emparejados][2]

resto de Hola de este tema tratan detalles específicos de Hola de cómo funcionan estas piezas.

## <a name="creation-of-backlog-queues"></a>Creación de colas de trabajos pendientes
Hola [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] objeto pasado toohello [PairNamespaceAsync] [ PairNamespaceAsync] método indica Hola número de trabajo pendiente de las colas desea toouse. Cada cola de trabajo pendiente, a continuación, se crea con hello establecer propiedades siguientes explícitamente (todos los demás valores se establecen toohello [QueueDescription] [ QueueDescription] los valores predeterminados):

| Ruta de acceso | [espacio de nombres principal] / x-servicebus-transfer / [index] donde [index] es un valor de [0, BacklogQueueCount) |
| --- | --- |
| MaxSizeInMegabytes |5120 |
| MaxDeliveryCount |int.MaxValue |
| DefaultMessageTimeToLive |TimeSpan.MaxValue |
| AutoDeleteOnIdle |TimeSpan.MaxValue |
| LockDuration |1 minuto |
| EnableDeadLetteringOnMessageExpiration |true |
| EnableBatchedOperations |true |

Por ejemplo, cola de trabajos pendientes de primera Hola creado para el espacio de nombres **contoso** se denomina `contoso/x-servicebus-transfer/0`.

Al crear las colas de hello, código de hello comprueba primero toosee si existe dicha cola. Si no existe la cola de Hola, se crea la cola de Hola. código de Hello no limpiar las colas de trabajo pendiente "adicionales". En concreto, si hello aplicación Hola espacio de nombres principal **contoso** solicita cinco colas de trabajo pendiente, pero una cola con la ruta de acceso de hello `contoso/x-servicebus-transfer/7` existe, esa cola de trabajo pendiente adicional sigue presente pero no se usa. sistema de Hello permite explícitamente tooexist de colas de trabajo pendiente adicionales que no se usen. Como propietario del espacio de nombres de hello, es responsable de limpiar las colas de trabajo pendiente sin usar o no deseado. motivo de Hola para tomar esta decisión es que el Bus de servicio no se puede saber la finalidad de todas las colas de hello en el espacio de nombres. Además, si una cola existe con el nombre especificado de hello pero no cumple Hola supone [QueueDescription][QueueDescription], a continuación, los motivos son por su propia cambian el comportamiento predeterminado Hola. Se realiza ninguna garantía de colas de trabajo pendiente de modificaciones toohello por su código. Asegúrese de tootest confirma los cambios exhaustivamente.

## <a name="custom-messagesender"></a>MessageSender personalizado
Cuando se envía, todos los mensajes pasan por un interno [MessageSender] [ MessageSender] objeto que tiene un comportamiento normal cuando todo funciona y los redirige las colas de trabajo pendiente de toohello cuando cosas "break". Al recibir un error no transitorio, se inicia un temporizador. Después de un [TimeSpan] [ TimeSpan] período que consta de hello [FailoverInterval] [ FailoverInterval] durante el cual no se envía ningún mensaje correctamente el valor de propiedad , Hola conmutación por error está ocupado. En este momento, hello ocurrirá lo siguiente para cada entidad:

* Ejecuta una tarea de ping cada [PingPrimaryInterval] [ PingPrimaryInterval] toocheck si Hola entidad está disponible. Una vez que esta tarea se realiza correctamente, todo el código de cliente que utiliza entity Hola inmediatamente comienza a enviar nuevos mensajes toohello espacio de nombres principal.
* Solicitudes futuras toosend toothat misma entidad desde otros remitentes provocará hello [BrokeredMessage] [ BrokeredMessage] enviarse toobe modifica toosit en la cola de trabajos pendientes de Hola. modificación de Hello quita algunas propiedades de hello [BrokeredMessage] [ BrokeredMessage] objeto y los almacena en otro lugar. Hello siguientes propiedades se borran y se agregan con un nuevo alias, lo que permite hello y Bus de servicio de mensajes de SDK de tooprocess uniformemente:

| Nombre de propiedad anterior | Nombre de propiedad nuevo |
| --- | --- |
| SessionId |x-ms-sessionid |
| TimeToLive |x-ms-timetolive |
| ScheduledEnqueueTimeUtc |x-ms-path |

ruta de acceso de destino original Hello también se almacena en el mensaje de bienvenida como una propiedad denominada x-ms-path. Este diseño permite los mensajes para muchos toocoexist de entidades en una única cola. propiedades de Hola se traducen por sifón Hola.

Hola personalizado [MessageSender] [ MessageSender] objeto puede encontrar problemas cuando mensajes aproximarse al límite de 256 KB de Hola y conmutación por error está ocupado. Hola personalizado [MessageSender] [ MessageSender] objeto almacena los mensajes para todas las colas y temas juntos en las colas de trabajo pendiente de Hola. Este objeto mezcla los mensajes de varias entidades principales juntos en las colas de trabajo pendiente de Hola. toohandle equilibrio de carga entre muchos clientes que no se conocen cada otra Hola SDK aleatoriamente toma una cola de trabajo pendiente para cada [QueueClient] [ QueueClient] o [TopicClient] [ TopicClient] crear en código.

## <a name="pings"></a>Pings
Un mensaje ping está vacío [BrokeredMessage] [ BrokeredMessage] con su [ContentType] [ ContentType] propiedad establece tooapplication/vnd.ms-servicebus-ping y un [TimeToLive] [ TimeToLive] valor de 1 segundo. Este ping tiene una característica especial en el Bus de servicio: servidor hello nunca entrega un ping cuando algún llamador solicita un [BrokeredMessage][BrokeredMessage]. Por lo tanto, nunca tendrá toolearn cómo tooreceive y omitir estos mensajes. Cada entidad (cola o tema únicos) por [MessagingFactory] [ MessagingFactory] instancia por cliente recibirá mensajes de ping cuando se consideran toobe no está disponible. De forma predeterminada, esto ocurre una vez por minuto. Los mensajes ping se consideran mensajes normales de Bus de servicio de toobe y pueden dar lugar a gastos de ancho de banda y mensajes. Tan pronto como los clientes de hello detectan que el sistema de hello está disponible, los mensajes de Hola se detienen.

## <a name="hello-syphon"></a>sifón Hola
Al menos un programa ejecutable de la aplicación hello debe estar ejecutándose activamente sifón Hola. sifón Hola realiza un valor largo que dura 15 minutos recepción de sondeo. Cuando todas las entidades están disponibles y tienen 10 colas de trabajo pendiente, Hola aplicación que hospeda las llamadas de sifón de Hola Hola recibirán operación 40 veces por hora, 960 veces al día y 28.800 veces en 30 días. Cuando Hola sifón mueve activamente mensajes desde la cola principal de toohello de trabajo pendiente de hello, cada mensaje experimenta Hola siguientes cargos (cargos estándar según el tamaño del mensaje y el ancho de banda se aplica en todas las fases):

1. Enviar trabajo pendiente de toohello.
2. Recibir de trabajo pendiente de Hola.
3. Enviar toohello principal.
4. Recibir de hello principal.

## <a name="closefault-behavior"></a>Comportamiento de cierre o error
Dentro de una aplicación que hospeda el sifón hello, una vez Hola principal o secundaria [MessagingFactory] [ MessagingFactory] produce un error o se cierra sin su asociado también está error o se cierre y Hola sifón detecta este estado , sifón Hola actúa. Si otro Hola [MessagingFactory] [ MessagingFactory] no se cierra en cinco segundos, Hola sifón creará un error Hola sigue abierto [MessagingFactory] [ MessagingFactory] .

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre la mensajería asincrónica de Service Bus, consulte [Patrones de mensajería asincrónica y alta disponibilidad][Asynchronous messaging patterns and high availability]. 

[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[FailoverInterval]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions#Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_FailoverInterval
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[TimeoutException]: https://msdn.microsoft.com/library/azure/system.timeoutexception.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[TimeSpan]: https://msdn.microsoft.com/library/azure/system.timespan.aspx
[PingPrimaryInterval]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_PingPrimaryInterval
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[ContentType]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType
[TimeToLive]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md
[0]: ./media/service-bus-paired-namespaces/IC673405.png
[1]: ./media/service-bus-paired-namespaces/IC673406.png
[2]: ./media/service-bus-paired-namespaces/IC673407.png
