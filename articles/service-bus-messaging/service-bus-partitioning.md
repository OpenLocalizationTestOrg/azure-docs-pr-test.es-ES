---
title: aaaCreate particiones temas y colas de Service Bus de Azure | Documentos de Microsoft
description: "Describe cómo corredores de temas mediante el uso de varios mensajes y colas de Bus de servicio de toopartition."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>Temas y colas con particiones
Service Bus de Azure emplea varios mensajes de corredores de bolsa tooprocess mensajes y mensajería múltiple almacena los mensajes de toostore. Un único agente de mensajes controla una cola o tema convencional, que se almacena en un almacén de mensajería. Bus de servicio *particiones* habilitar las colas y temas, o *entidades de mensajería*, toobe particionado entre varios agentes de mensajes y almacenes de mensajería. Esto significa que el rendimiento global de una entidad con particiones de Hola ya no está limitado por el rendimiento de Hola de un solo agente de mensajes o almacén de mensajería. Además, una interrupción temporal de un almacén de mensajería no hace que una cola o tema con particiones deje de estar disponible. Las colas y los temas con particiones pueden contener todas las características avanzadas de Service Bus, como la compatibilidad con transacciones y sesiones.

Para obtener información sobre características internas de Bus de servicio, vea hello [arquitectura de Service Bus] [ Service Bus architecture] artículo.

La partición está activada de forma predeterminada al crear la entidad en todas las colas y temas de mensajería Estándar y Premium. Puede crear entidades de nivel de mensajería Estándar sin particiones, pero las colas y los temas en un espacio de nombres Premium siempre están particionados; esta opción no se puede deshabilitar. 

No es posible toochange Hola particiones opción en una cola o tema existente en los niveles Standard o Premium, puede establecer solo la opción de hello cuando se crea la entidad de Hola.

## <a name="how-it-works"></a>Cómo funciona

Cada cola o tema con particiones consta de varios fragmentos. Cada fragmento se almacena en un almacén de mensajería diferente y se controla por un agente de mensajes diferente. Cuando se envía un mensaje tooa cola o tema particionado, Service Bus asigna tooone de mensaje Hola de fragmentos de Hola. selección de saludo se realiza aleatoriamente por Bus de servicio o mediante una clave de partición que Hola remitente puede especificar.

Cuando un cliente desea tooreceive un mensaje de una cola con particiones, o desde un tema con particiones tooa de suscripción, Bus de servicio consulta todos los fragmentos de mensajes, a continuación, devuelve Hola primer mensaje que se obtiene de cualquiera de hello receptor toohello de almacenes de mensajería. Las memorias caché de Bus de servicio Hola otros mensajes y la devuelve cuando recibe adicionales reciban solicitudes. Un cliente de recepción no es consciente de hello particiones; Hola comportamiento de cara al cliente de una cola o tema particionado (por ejemplo, leer, finalización, aplazamiento, mensajes fallidos y captura previa) es idéntica toohello comportamiento de una entidad regular.

No hay costos adicionales cuando se envía un mensaje a una cola o tema con particiones o cuando se recibe un mensaje de ellos.

## <a name="enable-partitioning"></a>Habilitación de las particiones

toouse particiones colas y temas con Bus de servicio de Azure, usar hello Azure SDK versión 2.2 o posterior, o especificar `api-version=2013-10` en sus solicitudes HTTP.

### <a name="standard"></a>Estándar

En el nivel de mensajería estándar de hello, puede crear colas de Bus de servicio y los temas de los tamaños de 1, 2, 3, 4 o 5 GB (valor predeterminado de hello es 1 GB). Con las particiones habilitadas, Bus de servicio crea 16 (16 particiones) de copias de entidad de Hola por cada GB que especifique. Por lo tanto, si crea una cola que es de 5 GB de tamaño, con 16 particiones tamaño máximo de cola de Hola se convierte en (5 \* 16) = 80 GB. Puede ver el tamaño máximo de saludo de la cola o tema particionados examinando su entrada en hello [portal de Azure][Azure portal], Hola **Introducción** hoja para esa entidad.

### <a name="premium"></a>Premium

En un espacio de nombres de nivel Premium, puede crear colas de Bus de servicio y los temas de los tamaños de 1, 2, 3, 4, 5, 10, 20, 40 o 80 GB (valor predeterminado de hello es 1 GB). Con las particiones habilitadas de forma predeterminada, Service Bus crea dos particiones por entidad. Puede ver el tamaño máximo de saludo de la cola o tema particionados examinando su entrada en hello [portal de Azure][Azure portal], Hola **Introducción** hoja para esa entidad.

Para obtener más información acerca de las particiones en el nivel de mensajería de hello Premium, consulte [Premium de Bus de servicio y niveles de mensajes estándares](service-bus-premium-messaging.md). 

### <a name="create-a-partitioned-entity"></a>Creación de una entidad particionada

Hay varias maneras toocreate una cola con particiones o un tema. Cuando creas Hola cola o tema de la aplicación, puede habilitar las particiones para hello cola o tema por respectivamente Hola de configuración [QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning] o [TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning] propiedad demasiado**true**. Estas propiedades deben establecerse en hello tiempo Hola cola o tema se crea. Como se mencionó anteriormente, es imposible toochange estas propiedades en una cola o tema existente. Por ejemplo:

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Como alternativa, puede crear una cola o tema particionado Hola [portal de Azure] [ Azure portal] o en Visual Studio. Cuando se crea una cola o tema en el portal de hello, Hola **habilitar las particiones** opción en hello cola o tema **crear** hoja está activada de forma predeterminada. Solo puede deshabilitar esta opción en una entidad de nivel estándar; Hola siempre está habilitada la creación de particiones de nivel Premium. En Visual Studio, haga clic en hello **habilitar particiones** checkbox en hello **nueva cola** o **nuevo tema** cuadro de diálogo.

## <a name="use-of-partition-keys"></a>Uso de claves de partición
Cuando un mensaje se pone en cola en una cola o tema particionado, Bus de servicio comprueba Hola presencia de una clave de partición. Si encuentra uno, selecciona el fragmento de hello basado en esa clave. Si no encuentra una clave de partición, selecciona el fragmento de hello basado en un algoritmo interno.

### <a name="using-a-partition-key"></a>Uso de una clave de partición
Algunos escenarios, como sesiones o transacciones, requieren toobe de mensajes almacenado en un fragmento específico. Todos estos escenarios requieren el uso de Hola de una clave de partición. Todos los mensajes que Hola de uso se asignan la misma clave de partición toohello mismo fragmento. Si no está disponible temporalmente el fragmento de hello, Bus de servicio devuelve un error.

Según el escenario de hello, se usan diferentes propiedades de mensaje como una clave de partición:

**SessionId**: si un mensaje tiene hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] propiedad establecida, a continuación, Bus de servicio usa esta propiedad como clave de partición de Hola. De este modo, todos los mensajes que pertenecen toohello misma sesión se controlan mediante Hola mismo agente de mensajes. Esto permite ordenamiento, así como la coherencia de Hola de Estados de sesión de mensajes de tooguarantee de Bus de servicio.

**PartitionKey**: si un mensaje tiene hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propiedad pero no hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] propiedad establecida, a continuación, Service Bus usa hello [PartitionKey] [ PartitionKey] propiedad como clave de partición de Hola. Si el mensaje de Hola tiene ambos hello [SessionId] [ SessionId] hello y [PartitionKey] [ PartitionKey] propiedades establecidas, ambas propiedades deben ser idénticas. Si hello [PartitionKey] [ PartitionKey] propiedad se establece el valor diferente tooa hello [SessionId] [ SessionId] propiedad, Service Bus devuelve no válido excepción de operación. Hola [PartitionKey] [ PartitionKey] propiedad debe utilizarse si un remitente envía mensajes transaccionales de sesión no es compatible con. Hello clave de partición asegura que todos los mensajes que se envían dentro de una transacción se gestionan por hello mismo agente de mensajería.

**MessageId**: si Hola cola o tema tiene hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] propiedad establecida demasiado**true** hello y[BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] o [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propiedades no están establecidos, a continuación Hola [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] propiedad actúa como clave de partición de Hola. (Tenga en cuenta que las bibliotecas de Microsoft .NET y AMQP Hola asignar automáticamente un identificador de mensaje si la aplicación de envío de hello no lo hace). En este caso, todas las copias de hello controla mismo mensaje Hola a miso agente de mensajes. Esto permite toodetect de Bus de servicio y eliminar mensajes duplicados. Si hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] propiedad no se establece demasiado**true**, Bus de servicio no tiene en cuenta hello [MessageId] [ MessageId] propiedad como una clave de partición.

### <a name="not-using-a-partition-key"></a>Sin uso de una clave de partición
En ausencia de Hola de una clave de partición, Bus de servicio distribuye los mensajes en una fragmentos de hello tooall turnos de hello cola o tema particionado. Si el fragmento de hello elegido no está disponible, Service Bus asigna tooa otro fragmento de mensaje de Hola. Operación de envío Hola de este modo, se realiza correctamente a pesar de no disponibilidad temporal de Hola de un almacén de mensajería. Sin embargo, no consigan Hola garantizada el orden que proporciona una clave de partición.

Para obtener una explicación más detallada de compromiso de hello entre la disponibilidad (sin clave de partición) y coherencia (mediante una clave de partición), consulte [este artículo](../event-hubs/event-hubs-availability-and-consistency.md). Esta información aplica igualmente toopartitioned entidades de Bus de servicio y las particiones de los centros de eventos.

toogive servicio Bus suficiente mensaje Hola de tooenqueue de tiempo en un fragmento diferente, hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] valor especificado por el cliente de Hola que envía el mensaje de bienvenida debe ser mayor que 15 segundos. Se recomienda que establezca hello [OperationTimeout] [ OperationTimeout] valor de propiedad toohello predeterminado de 60 segundos.

Tenga en cuenta que una clave de partición "ancla" un fragmento específico de mensaje tooa. Si el almacén de mensajes de Hola que contiene este fragmento no está disponible, Bus de servicio devuelve un error. En ausencia de Hola de una clave de partición, Bus de servicio puede elegir un fragmento diferente y Hola operación se realiza correctamente. Por lo tanto, se recomienda no suministrar una clave de partición a menos que sea necesario.

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>Temas avanzados: uso de transacciones con entidades con particiones
Los mensajes que se envían como parte de una transacción deben especificar una clave de partición. Esto puede ser uno de hello propiedades siguientes: [BrokeredMessage.SessionId][BrokeredMessage.SessionId], [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey], o [ BrokeredMessage.MessageId][BrokeredMessage.MessageId]. Hola a todos los mensajes que se envían como parte del programa Hola debe especificar la misma transacción misma clave de partición. Si intenta toosend un mensaje sin una clave de partición dentro de una transacción, Bus de servicio devuelve una excepción de operación no válida. Si intentas toosend varios mensajes dentro de Hola la misma transacción que tienen diferentes claves de partición, Bus de servicio devuelve una excepción de operación no válida. Por ejemplo:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

Si se establece cualquiera de las propiedades de Hola que actúan como una clave de partición, PIN de Bus de servicio Hola fragmento de mensaje tooa específico. Este comportamiento se produce independientemente de si se usa una transacción o no. Se recomienda que no especifique una clave de partición si no es necesario.

## <a name="using-sessions-with-partitioned-entities"></a>Uso de sesiones con entidades con particiones
toosend un tema de cuenta para la sesión de tooa mensaje transaccional o una cola, los mensajes de bienvenida deben tener Hola [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] conjunto de propiedades. Si hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] propiedad también se especifica, debe ser idéntico toohello [SessionId] [ SessionId] propiedad. Si difieren, Service Bus devuelve una excepción de operación no válida.

A diferencia de colas normales (sin particiones) o temas, no es posible toouse toosend de una sola transacción varias sesiones de toodifferent de mensajes. Si se intenta, Service Bus devuelve una excepción de operación no válida. Por ejemplo:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>Reenvío automático de mensajes en entidades con particiones
Service Bus de Azure admite el reenvío automático de mensajes desde entidades con particiones, así como a ellas y entre ellas. tooenable automática reenvío de mensajes, establezca hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] propiedad en la cola de origen de Hola o suscripción. Si el mensaje de Hola especifica una clave de partición ([SessionId][SessionId], [PartitionKey][PartitionKey], o [MessageId] [ MessageId]), se utilizará dicha clave de partición para la entidad de destino de Hola.

## <a name="considerations-and-guidelines"></a>Consideraciones e instrucciones
* **La funcionalidad de consistencia alta**: si una entidad utiliza características como las sesiones, detección de duplicados o control explícito de la clave de partición, las operaciones de mensajería de hello siempre son fragmentos de toospecific enrutado. Si cualquiera de los fragmentos de hello experiencia mucho tráfico o almacén subyacente Hola está en mal estado, esas operaciones producirá un error y se reduce la disponibilidad. En general, la coherencia de hello es todavía mucho mayor que las entidades sin particiones; solo un subconjunto de tráfico está experimentando problemas, como el tráfico de hello tooall opuestos. Para obtener más información, consulte este [análisis sobre la disponibilidad y la coherencia](../event-hubs/event-hubs-availability-and-consistency.md).
* **Administración**: operaciones como la creación, actualización y eliminación deben realizarse en todos los fragmentos de Hola de entidad de Hola. Si algún fragmento es incorrecto, podría provocar errores en estas operaciones. Para la operación de obtención de hello, información como números de mensajes se debe agregar de todos los fragmentos. Si cualquier fragmento que está en mal estado, se notifica el estado de disponibilidad de entidad de hello como limited.
* **Escenarios de mensajes de volumen de baja**: para estos escenarios, especialmente cuando se usa el protocolo de hello HTTP, es posible que tenga tooperform varias operaciones de recepción en orden tooobtain todos los mensajes de saludo. Para las solicitudes de recepción, front-end de hello realiza una operación de recepción en todos los fragmentos de Hola y almacena en caché todas las respuestas de saludo recibidas. Una solicitud de recepción posterior en la misma conexión podría beneficiarse de este almacenamiento en caché y recibir las latencias de hello será menor. Sin embargo, si tiene varias conexiones o utiliza el protocolo HTTP, se establecerá una conexión nueva para cada solicitud. Por lo tanto, no hay ninguna garantía de que llegaría en hello mismo nodo. Si todos los mensajes existentes están bloqueados y se almacena en caché en otro front-end, Hola recibir operación devuelve **null**. Finalmente, los mensajes caducan y podrá volver a recibirlos. Se recomienda mantener la conexión HTTP.
* **Examinar/Peek mensajes**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) no siempre devuelven número Hola de mensajes especificado en hello [MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount) propiedad. Esto tiene dos motivos habituales. Una razón es que hello agregado tamaño de colección Hola de mensajes supera el tamaño máximo de Hola de 256KB. Otro motivo es que si Hola cola o tema tiene hello [EnablePartitioning propiedad](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning) establecido demasiado**true**, una partición no tenga suficientes mensajes hello toocomplete solicita el número de mensajes. En general, si una aplicación desea tooreceive un número concreto de mensajes, debe llamar a [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) repetidamente hasta que se llega a ese número de mensajes o no hay ningún toopeek mensajes más. Para más información, incluidos algunos ejemplos de código, consulte [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) o [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_).

## <a name="latest-added-features"></a>Características agregadas más recientes
* La opción Agregar o quitar regla ya es compatible con las entidades con particiones. A diferencia de las entidades sin particiones, estas operaciones no se admiten en las transacciones. 
* Ahora se admite AMQP para enviar y recibir mensajes tooand de una entidad con particiones.
* Ahora se admite AMQP para hello las siguientes operaciones: [enviar lote](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__), [por lotes de recepción](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_), [recepción por número de secuencia](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_), [Peek](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek), [ Renovar el bloqueo](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_), [programar mensaje](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_), [Cancelar mensaje programada](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_), [Agregar regla](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Quitar regla](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Bloqueo de renovación de sesión](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock), [estado de la sesión de conjunto](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_), [obtener el estado de sesión](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState), y [enumerar las sesiones](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync).

## <a name="partitioned-entities-limitations"></a>Limitaciones de las entidades con particiones
Actualmente, Bus de servicio impone Hola siguientes limitaciones en los temas y las colas con particiones:

* Temas y colas con particiones no admiten el envío de mensajes que pertenecen toodifferent sesiones en una sola transacción.
* Bus de servicio permite que actualmente un too100 particionado colas o temas por espacio de nombres. Cada cola o tema particionado se cuenta en la cuota de Hola de 10 000 entidades por espacio de nombres (no se aplica el nivel de tooPremium).

## <a name="next-steps"></a>Pasos siguientes
Vea la descripción de Hola de [compatibilidad con AMQP 1.0 para Bus de servicio con particiones colas y temas] [ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn más acerca de las particiones de las entidades de mensajería. 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md
