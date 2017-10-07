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
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="44148-103">Encadenamiento de entidades de Service Bus con reenvío automático</span><span class="sxs-lookup"><span data-stu-id="44148-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="44148-104">Hola Service Bus *reenvío automático* característica permite toochain una cola o cola de suscripción tooanother o tema que forme parte del programa Hola mismo espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="44148-104">hello Service Bus *auto-forwarding* feature enables you toochain a queue or subscription tooanother queue or topic that is part of hello same namespace.</span></span> <span data-ttu-id="44148-105">Cuando está habilitado el reenvío automático, Bus de servicio quita los mensajes que se colocan en la primera cola de Hola o suscripción (origen) automáticamente y se pone en cola de segundo de Hola o un tema (destino).</span><span class="sxs-lookup"><span data-stu-id="44148-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in hello first queue or subscription (source) and puts them in hello second queue or topic (destination).</span></span> <span data-ttu-id="44148-106">Tenga en cuenta que es posible toosend una entidad de destino de mensaje toohello directamente.</span><span class="sxs-lookup"><span data-stu-id="44148-106">Note that it is still possible toosend a message toohello destination entity directly.</span></span> <span data-ttu-id="44148-107">Además, no es posible toochain una subcola, como una cola de mensajes fallidos, tooanother cola o tema.</span><span class="sxs-lookup"><span data-stu-id="44148-107">Also, it is not possible toochain a subqueue, such as a deadletter queue, tooanother queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="44148-108">Uso del reenvío automático</span><span class="sxs-lookup"><span data-stu-id="44148-108">Using auto-forwarding</span></span>
<span data-ttu-id="44148-109">Puede habilitar el reenvío automático por establecer hello [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] o [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] propiedades de hello [QueueDescription] [ QueueDescription] o [Queuedescription] [ SubscriptionDescription] objetos para el origen de hello, como en hello ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="44148-109">You can enable auto-forwarding by setting hello [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on hello [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for hello source, as in hello following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="44148-110">entidad de destino de Hello debe existir en tiempo de Hola se crea la entidad de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="44148-110">hello destination entity must exist at hello time hello source entity is created.</span></span> <span data-ttu-id="44148-111">Si no existe la entidad de destino de hello, Bus de servicio devuelve una excepción cuando toocreate frecuentes Hola entidad de origen.</span><span class="sxs-lookup"><span data-stu-id="44148-111">If hello destination entity does not exist, Service Bus returns an exception when asked toocreate hello source entity.</span></span>

<span data-ttu-id="44148-112">Puede utilizar el reenvío automático tooscale horizontalmente un tema individual.</span><span class="sxs-lookup"><span data-stu-id="44148-112">You can use auto-forwarding tooscale out an individual topic.</span></span> <span data-ttu-id="44148-113">Bus de servicio límites hello [número de suscripciones en un tema determinado](service-bus-quotas.md) too2, 000.</span><span class="sxs-lookup"><span data-stu-id="44148-113">Service Bus limits hello [number of subscriptions on a given topic](service-bus-quotas.md) too2,000.</span></span> <span data-ttu-id="44148-114">Para alojar suscripciones adicionales, cree temas de segundo nivel.</span><span class="sxs-lookup"><span data-stu-id="44148-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="44148-115">Tenga en cuenta que, incluso si no se encuentra restringido por hello puede mejorar el límite de número de Hola de suscripciones, al agregar un segundo nivel de temas de Bus de servicio Hola el rendimiento global de su tema.</span><span class="sxs-lookup"><span data-stu-id="44148-115">Note that even if you are not bound by hello Service Bus limitation on hello number of subscriptions, adding a second level of topics can improve hello overall throughput of your topic.</span></span>

![Escenario de reenvío automático][0]

<span data-ttu-id="44148-117">También puede utilizar el reenvío automático toodecouple remitentes de mensajes a destinatarios.</span><span class="sxs-lookup"><span data-stu-id="44148-117">You can also use auto-forwarding toodecouple message senders from receivers.</span></span> <span data-ttu-id="44148-118">Por ejemplo, suponga que un sistema ERP consta de tres módulos: procesamiento de pedidos, administración de inventario y administración de relaciones con clientes.</span><span class="sxs-lookup"><span data-stu-id="44148-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="44148-119">Cada uno de estos módulos genera mensajes que se ponen en cola en el tema correspondiente.</span><span class="sxs-lookup"><span data-stu-id="44148-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="44148-120">Alice y Bob es representantes de ventas que están interesados en todos los mensajes relacionados con los clientes de tootheir.</span><span class="sxs-lookup"><span data-stu-id="44148-120">Alice and Bob are sales representatives that are interested in all messages that relate tootheir customers.</span></span> <span data-ttu-id="44148-121">tooreceive los mensajes, Alice y Bob crea una cola personal y una suscripción en cada uno de los temas ERP de Hola que reenvían automáticamente la cola de tootheir para todos los mensajes.</span><span class="sxs-lookup"><span data-stu-id="44148-121">tooreceive those messages, Alice and Bob each create a personal queue and a subscription on each of hello ERP topics that automatically forward all messages tootheir queue.</span></span>

![Escenario de reenvío automático][1]

<span data-ttu-id="44148-123">Si Alice se va de vacaciones, su cola personal, en lugar de tema de hello ERP, se llena.</span><span class="sxs-lookup"><span data-stu-id="44148-123">If Alice goes on vacation, her personal queue, rather than hello ERP topic, fills up.</span></span> <span data-ttu-id="44148-124">En este escenario, dado que un representante de ventas no ha recibido ningún mensaje, ninguno de los temas de hello ERP alcanza la cuota.</span><span class="sxs-lookup"><span data-stu-id="44148-124">In this scenario, because a sales representative has not received any messages, none of hello ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="44148-125">Consideraciones sobre el reenvío automático</span><span class="sxs-lookup"><span data-stu-id="44148-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="44148-126">Si entidad de destino de hello acumula demasiados mensajes y excede la cuota de Hola o entidad de destino de hello está deshabilitado, entidad de origen de Hola agrega mensajes de Hola tooits [cola de mensajes no enviados](service-bus-dead-letter-queues.md) hasta que haya espacio en el destino de Hola (o se vuelve a habilitar la entidad de hello).</span><span class="sxs-lookup"><span data-stu-id="44148-126">If hello destination entity accumulates too many messages and exceeds hello quota, or hello destination entity is disabled, hello source entity adds hello messages tooits [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in hello destination (or hello entity is re-enabled).</span></span> <span data-ttu-id="44148-127">Los mensajes seguirán toolive en cola de mensajes no enviados de hello, por lo que debe recibir y procesarlos de cola de mensajes no enviados de hello explícitamente.</span><span class="sxs-lookup"><span data-stu-id="44148-127">Those messages will continue toolive in hello dead-letter queue, so you must explicitly receive and process them from hello dead-letter queue.</span></span>

<span data-ttu-id="44148-128">Al encadenar juntos temas individuales tooobtain un tema compuesto con muchas suscripciones, se recomienda que tienen un número moderado de suscripciones en el tema de primer nivel de Hola y muchas suscripciones en los temas de segundo nivel Hola.</span><span class="sxs-lookup"><span data-stu-id="44148-128">When chaining together individual topics tooobtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on hello first-level topic and many subscriptions on hello second-level topics.</span></span> <span data-ttu-id="44148-129">Por ejemplo, un tema de primer nivel con 20 suscripciones, cada una de ellas encadenada tooa tema de segundo nivel con 200 suscripciones, permite un mayor rendimiento que un tema de primer nivel con 200 suscripciones, cada uno de ellos encadenadas tooa tema de segundo nivel con 20 suscripciones .</span><span class="sxs-lookup"><span data-stu-id="44148-129">For example, a first-level topic with 20 subscriptions, each of them chained tooa second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained tooa second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="44148-130">Service Bus factura una operación por cada mensaje reenviado.</span><span class="sxs-lookup"><span data-stu-id="44148-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="44148-131">Por ejemplo, enviar un tema de mensaje tooa con 20 suscripciones, cada uno de ellos configurado mensajes de avance tooauto tooanother cola o tema, se factura como 21 operaciones si todas las suscripciones de primer nivel reciben una copia del mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="44148-131">For example, sending a message tooa topic with 20 subscriptions, each of them configured tooauto-forward messages tooanother queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of hello message.</span></span>

<span data-ttu-id="44148-132">toocreate una suscripción que está encadenada tooanother cola o tema, debe tener creador de Hola de suscripción de hello **administrar** permisos en el origen de Hola y de entidad de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="44148-132">toocreate a subscription that is chained tooanother queue or topic, hello creator of hello subscription must have **Manage** permissions on both hello source and hello destination entity.</span></span> <span data-ttu-id="44148-133">Enviar sólo requiere el tema de origen de mensajes toohello **enviar** permisos en el tema de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="44148-133">Sending messages toohello source topic only requires **Send** permissions on hello source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44148-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44148-134">Next steps</span></span>

<span data-ttu-id="44148-135">Para obtener información detallada sobre el reenvío automático, vea Hola temas de referencia siguientes:</span><span class="sxs-lookup"><span data-stu-id="44148-135">For detailed information about auto-forwarding, see hello following reference topics:</span></span>

* <span data-ttu-id="44148-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="44148-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="44148-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="44148-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="44148-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="44148-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="44148-139">toolearn más información acerca de las mejoras de rendimiento de Bus de servicio, vea</span><span class="sxs-lookup"><span data-stu-id="44148-139">toolearn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="44148-140">Procedimientos recomendados para mejorar el rendimiento mediante la mensajería de Service Bus</span><span class="sxs-lookup"><span data-stu-id="44148-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="44148-141">[Entidades de mensajería con particiones][Partitioned messaging entities]</span><span class="sxs-lookup"><span data-stu-id="44148-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
