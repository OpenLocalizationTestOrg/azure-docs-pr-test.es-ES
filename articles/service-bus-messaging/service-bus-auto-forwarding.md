---
title: "entidades de mensajería de Service Bus de Azure de reenvío de aaaAuto | Documentos de Microsoft"
description: "¿Cómo toochain un Bus de servicio cola o una suscripción tooanother cola o un tema."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a>Encadenamiento de entidades de Service Bus con reenvío automático

Hola Service Bus *reenvío automático* característica permite toochain una cola o cola de suscripción tooanother o tema que forme parte del programa Hola mismo espacio de nombres. Cuando está habilitado el reenvío automático, Bus de servicio quita los mensajes que se colocan en la primera cola de Hola o suscripción (origen) automáticamente y se pone en cola de segundo de Hola o un tema (destino). Tenga en cuenta que es posible toosend una entidad de destino de mensaje toohello directamente. Además, no es posible toochain una subcola, como una cola de mensajes fallidos, tooanother cola o tema.

## <a name="using-auto-forwarding"></a>Uso del reenvío automático
Puede habilitar el reenvío automático por establecer hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] o [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] propiedades de hello [QueueDescription] [ QueueDescription] o [Queuedescription] [ SubscriptionDescription] objetos para el origen de hello, como en hello ejemplo siguiente.

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

entidad de destino de Hello debe existir en tiempo de Hola se crea la entidad de origen de Hola. Si no existe la entidad de destino de hello, Bus de servicio devuelve una excepción cuando toocreate frecuentes Hola entidad de origen.

Puede utilizar el reenvío automático tooscale horizontalmente un tema individual. Bus de servicio límites hello [número de suscripciones en un tema determinado](service-bus-quotas.md) too2, 000. Para alojar suscripciones adicionales, cree temas de segundo nivel. Tenga en cuenta que, incluso si no se encuentra restringido por hello puede mejorar el límite de número de Hola de suscripciones, al agregar un segundo nivel de temas de Bus de servicio Hola el rendimiento global de su tema.

![Escenario de reenvío automático][0]

También puede utilizar el reenvío automático toodecouple remitentes de mensajes a destinatarios. Por ejemplo, suponga que un sistema ERP consta de tres módulos: procesamiento de pedidos, administración de inventario y administración de relaciones con clientes. Cada uno de estos módulos genera mensajes que se ponen en cola en el tema correspondiente. Alice y Bob es representantes de ventas que están interesados en todos los mensajes relacionados con los clientes de tootheir. tooreceive los mensajes, Alice y Bob crea una cola personal y una suscripción en cada uno de los temas ERP de Hola que reenvían automáticamente la cola de tootheir para todos los mensajes.

![Escenario de reenvío automático][1]

Si Alice se va de vacaciones, su cola personal, en lugar de tema de hello ERP, se llena. En este escenario, dado que un representante de ventas no ha recibido ningún mensaje, ninguno de los temas de hello ERP alcanza la cuota.

## <a name="auto-forwarding-considerations"></a>Consideraciones sobre el reenvío automático

Si entidad de destino de hello acumula demasiados mensajes y excede la cuota de Hola o entidad de destino de hello está deshabilitado, entidad de origen de Hola agrega mensajes de Hola tooits [cola de mensajes no enviados](service-bus-dead-letter-queues.md) hasta que haya espacio en el destino de Hola (o se vuelve a habilitar la entidad de hello). Los mensajes seguirán toolive en cola de mensajes no enviados de hello, por lo que debe recibir y procesarlos de cola de mensajes no enviados de hello explícitamente.

Al encadenar juntos temas individuales tooobtain un tema compuesto con muchas suscripciones, se recomienda que tienen un número moderado de suscripciones en el tema de primer nivel de Hola y muchas suscripciones en los temas de segundo nivel Hola. Por ejemplo, un tema de primer nivel con 20 suscripciones, cada una de ellas encadenada tooa tema de segundo nivel con 200 suscripciones, permite un mayor rendimiento que un tema de primer nivel con 200 suscripciones, cada uno de ellos encadenadas tooa tema de segundo nivel con 20 suscripciones .

Service Bus factura una operación por cada mensaje reenviado. Por ejemplo, enviar un tema de mensaje tooa con 20 suscripciones, cada uno de ellos configurado mensajes de avance tooauto tooanother cola o tema, se factura como 21 operaciones si todas las suscripciones de primer nivel reciben una copia del mensaje de bienvenida.

toocreate una suscripción que está encadenada tooanother cola o tema, debe tener creador de Hola de suscripción de hello **administrar** permisos en el origen de Hola y de entidad de destino de Hola. Enviar sólo requiere el tema de origen de mensajes toohello **enviar** permisos en el tema de origen Hola.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información detallada sobre el reenvío automático, vea Hola temas de referencia siguientes:

* [ForwardTo][QueueDescription.ForwardTo]
* [QueueDescription][QueueDescription]
* [SubscriptionDescription][SubscriptionDescription]

toolearn más información acerca de las mejoras de rendimiento de Bus de servicio, vea 

* [Procedimientos recomendados para mejorar el rendimiento mediante la mensajería de Service Bus](service-bus-performance-improvements.md)
* [Entidades de mensajería con particiones][Partitioned messaging entities]

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
