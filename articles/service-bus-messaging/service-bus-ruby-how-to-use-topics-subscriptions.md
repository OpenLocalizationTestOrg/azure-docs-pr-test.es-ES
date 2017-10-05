---
title: Uso de temas de Service Bus (Ruby) | Microsoft Docs
description: "Aprenda a usar los temas y las suscripciones del Bus de servicio de Azure. Los ejemplos de código están escritos para aplicaciones Ruby."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 4a4c9949843b16ae6be2f516de4fd1e3f7415959
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="487fb-104">Uso de temas y suscripciones de Service Bus con Ruby</span><span class="sxs-lookup"><span data-stu-id="487fb-104">How to use Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="487fb-105">En este artículo se describe cómo usar los temas y las suscripciones de Service Bus desde aplicaciones Ruby.</span><span class="sxs-lookup"><span data-stu-id="487fb-105">This article describes how to use Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="487fb-106">Entre los escenarios tratados se incluyen la **creación de temas y suscripciones, la creación de filtros de suscripción, el envío de mensajes** a un tema, la **recepción de mensajes de una suscripción** y la **eliminación de temas y suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="487fb-106">The scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** to a topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="487fb-107">Para más información sobre los temas y las suscripciones, vea la sección [Pasos siguientes](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="487fb-107">For more information on topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="487fb-108">Creación de un tema</span><span class="sxs-lookup"><span data-stu-id="487fb-108">Create a topic</span></span>
<span data-ttu-id="487fb-109">El objeto **Azure::ServiceBusService** le permite trabajar con temas.</span><span class="sxs-lookup"><span data-stu-id="487fb-109">The **Azure::ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="487fb-110">El siguiente código crea un objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="487fb-110">The following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="487fb-111">Para crear un tema, use el método `create_topic()`.</span><span class="sxs-lookup"><span data-stu-id="487fb-111">To create a topic, use the `create_topic()` method.</span></span> <span data-ttu-id="487fb-112">En el siguiente ejemplo se crea un tema o se imprime el error si lo hubiera.</span><span class="sxs-lookup"><span data-stu-id="487fb-112">The following example creates a topic or prints out the errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="487fb-113">También puede pasar un objeto **Azure::ServiceBus::Topic** con opciones adicionales, lo que le permite reemplazar la configuración de la cola predeterminada, como el período de vida del mensaje o el tamaño de cola máximo.</span><span class="sxs-lookup"><span data-stu-id="487fb-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you to override default topic settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="487fb-114">En el siguiente ejemplo se muestra cómo establecer el tamaño máximo de las colas en 5 GB y el período de vida en 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="487fb-114">The following example shows setting the maximum queue size to 5 GB and time to live to 1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="487fb-115">Creación de suscripciones</span><span class="sxs-lookup"><span data-stu-id="487fb-115">Create subscriptions</span></span>
<span data-ttu-id="487fb-116">Las suscripciones a temas también se crean con el objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="487fb-116">Topic subscriptions are also created with the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="487fb-117">A las suscripciones se les asigna un nombre y pueden tener un filtro opcional que restrinja el conjunto de mensajes que se entregan a su cola virtual.</span><span class="sxs-lookup"><span data-stu-id="487fb-117">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

<span data-ttu-id="487fb-118">Las suscripciones son permanentes y seguirán existiendo hasta que se eliminen, o se elimine el tema al que están asociadas.</span><span class="sxs-lookup"><span data-stu-id="487fb-118">Subscriptions are persistent and will continue to exist until either they, or the topic they are associated with, are deleted.</span></span> <span data-ttu-id="487fb-119">Si la aplicación contiene lógica para crear una suscripción, primero debe comprobar si esta ya existe utilizando el método getSubscription.</span><span class="sxs-lookup"><span data-stu-id="487fb-119">If your application contains logic to create a subscription, it should first check if the subscription already exists by using the getSubscription method.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="487fb-120">Creación de una suscripción con el filtro predeterminado (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="487fb-120">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="487fb-121">El filtro predeterminado **MatchAll** se usa en caso de que no se haya especificado ninguno al crear una suscripción.</span><span class="sxs-lookup"><span data-stu-id="487fb-121">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="487fb-122">Al usar el filtro **MatchAll**, todos los mensajes publicados en el tema se colocan en la cola virtual de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="487fb-122">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="487fb-123">En el ejemplo siguiente se crea una suscripción llamada "all-messages" que usa el filtro predeterminado **MatchAll**.</span><span class="sxs-lookup"><span data-stu-id="487fb-123">The following example creates a subscription named "all-messages" and uses the default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="487fb-124">Creación de suscripciones con filtros</span><span class="sxs-lookup"><span data-stu-id="487fb-124">Create subscriptions with filters</span></span>
<span data-ttu-id="487fb-125">También puede definir filtros que le permitan especificar qué mensajes enviados a un tema deben mostrarse dentro de una suscripción a una suscripción determinada.</span><span class="sxs-lookup"><span data-stu-id="487fb-125">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific subscription.</span></span>

<span data-ttu-id="487fb-126">El tipo de filtro más flexible compatible con las suscripciones es **Azure::ServiceBus::SqlFilter**, que implementa un subconjunto de SQL92.</span><span class="sxs-lookup"><span data-stu-id="487fb-126">The most flexible type of filter supported by subscriptions is the **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="487fb-127">Los filtros de SQL operan en las propiedades de los mensajes que se publican en el tema.</span><span class="sxs-lookup"><span data-stu-id="487fb-127">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="487fb-128">Para obtener más información sobre las expresiones que se pueden usar con un filtro de SQL, revise la sintaxis de [SqlFilter](service-bus-messaging-sql-filter.md).</span><span class="sxs-lookup"><span data-stu-id="487fb-128">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="487fb-129">Es posible agregar filtros a una suscripción a través del método `create_rule()` del objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="487fb-129">You can add filters to a subscription by using the `create_rule()` method of the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="487fb-130">Este método le permite agregar nuevos filtros a una suscripción existente.</span><span class="sxs-lookup"><span data-stu-id="487fb-130">This method enables you to add new filters to an existing subscription.</span></span>

<span data-ttu-id="487fb-131">Dado que el filtro predeterminado se aplica automáticamente a todas las suscripciones nuevas, primero debe eliminar el filtro predeterminado si no quiere que **MatchAll** anule todos los otros filtros que especifique.</span><span class="sxs-lookup"><span data-stu-id="487fb-131">Since the default filter is applied automatically to all new subscriptions, you must first remove the default filter, or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="487fb-132">Puede eliminar la regla predeterminada utilizando el método `delete_rule()` en el objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="487fb-132">You can remove the default rule by using the `delete_rule()` method on the **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="487fb-133">En el ejemplos siguiente se crea una suscripción llamada "high-messages" con **Azure::ServiceBus::SqlFilter** que solo selecciona los mensajes que tienen una propiedad `message_number` personalizada superior a 3:</span><span class="sxs-lookup"><span data-stu-id="487fb-133">The following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="487fb-134">Del mismo modo, en el ejemplo que aparece a continuación, se crea una suscripción denominada `low-messages` con un filtro **Azure::ServiceBus::SqlFilter** que solo selecciona los mensajes cuyo valor de la propiedad `message_number` es menor o igual que 3:</span><span class="sxs-lookup"><span data-stu-id="487fb-134">Similarly, the following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal to 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="487fb-135">Cuando ahora se envía un mensaje a `test-topic`, siempre se entrega a los destinatarios que están suscritos al tema `all-messages`, mientras que se entrega de forma selectiva a los que están suscritos a los temas `high-messages` y `low-messages` (según el contenido del mensaje).</span><span class="sxs-lookup"><span data-stu-id="487fb-135">When a message is now sent to `test-topic`, it is always be delivered to receivers subscribed to the `all-messages` topic subscription, and selectively delivered to receivers subscribed to the `high-messages` and `low-messages` topic subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="487fb-136">Envío de mensajes a un tema</span><span class="sxs-lookup"><span data-stu-id="487fb-136">Send messages to a topic</span></span>
<span data-ttu-id="487fb-137">Para enviar un mensaje a un tema de Service Bus, la aplicación debe utilizar el método `send_topic_message()` en el objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="487fb-137">To send a message to a Service Bus topic, your application must use the `send_topic_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="487fb-138">Los mensajes enviados a los temas de Service Bus son instancias de los objetos **Azure::ServiceBus::BrokeredMessage**.</span><span class="sxs-lookup"><span data-stu-id="487fb-138">Messages sent to Service Bus topics are instances of the **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="487fb-139">Los objetos **Azure::ServiceBus::BrokeredMessage** cuentan con un conjunto de propiedades estándar (como `label` y `time_to_live`), un diccionario que se usa para mantener las propiedades personalizadas específicas de la aplicación y un conjunto de datos de cadenas.</span><span class="sxs-lookup"><span data-stu-id="487fb-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used to hold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="487fb-140">Una aplicación puede establecer el cuerpo del mensaje pasando un valor de cadena al método `send_topic_message()`, con lo que las propiedades estándar requeridas adquieren valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="487fb-140">An application can set the body of the message by passing a string value to the `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="487fb-141">En el ejemplo siguiente se demuestra cómo enviar cinco mensajes de prueba a `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="487fb-141">The following example demonstrates how to send five test messages to `test-topic`.</span></span> <span data-ttu-id="487fb-142">Tenga en cuenta que el valor de la propiedad personalizado `message_number` de cada mensaje varía en función de la iteración del bucle (lo que determina qué suscripción lo recibe):</span><span class="sxs-lookup"><span data-stu-id="487fb-142">Note that the `message_number` custom property value of each message varies on the iteration of the loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="487fb-143">El tamaño máximo de mensaje que admiten los temas de Service Bus es de 256 KB en el [nivel Estándar](service-bus-premium-messaging.md) y de 1 MB en el [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="487fb-143">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="487fb-144">El encabezado, que incluye propiedades de la aplicación estándar y personalizadas, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="487fb-144">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="487fb-145">No hay límite para el número de mensajes que contiene un tema, pero hay un tope para el tamaño total de los mensajes contenidos en un tema.</span><span class="sxs-lookup"><span data-stu-id="487fb-145">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="487fb-146">El tamaño de los temas se define en el momento de la creación (el límite máximo es de 5 GB).</span><span class="sxs-lookup"><span data-stu-id="487fb-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="487fb-147">Recepción de mensajes de una suscripción</span><span class="sxs-lookup"><span data-stu-id="487fb-147">Receive messages from a subscription</span></span>
<span data-ttu-id="487fb-148">Los mensajes se reciben de una suscripción utilizando el método `receive_subscription_message()` del objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="487fb-148">Messages are received from a subscription using the `receive_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="487fb-149">De forma predeterminada, los mensajes se leen (máximo) y bloquean sin que se eliminen de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="487fb-149">By default, messages are read(peak) and locked without deleting it from the subscription.</span></span> <span data-ttu-id="487fb-150">Puede leer y eliminar el mensaje de la suscripción estableciendo la opción `peek_lock` en **false**.</span><span class="sxs-lookup"><span data-stu-id="487fb-150">You can read and delete the message from the subscription by setting the `peek_lock` option to **false**.</span></span>

<span data-ttu-id="487fb-151">El comportamiento predeterminado convierte la lectura y eliminación en una operación de dos fases que también hace posible admitir aplicaciones que no toleran la pérdida de mensajes.</span><span class="sxs-lookup"><span data-stu-id="487fb-151">The default behavior makes the reading and deleting a two-stage operation, which also makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="487fb-152">Cuando el Bus de servicio recibe una solicitud, busca el siguiente mensaje que se va a consumir, lo bloquea para impedir que otros consumidores lo reciban y, a continuación, lo devuelve a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="487fb-152">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="487fb-153">Una vez que la aplicación termina de procesar el mensaje (o lo almacena de forma fiable para su futuro procesamiento), completa la segunda fase del proceso de recepción llamando al método `delete_subscription_message()` y facilitando el mensaje que se va a eliminar a modo de parámetro.</span><span class="sxs-lookup"><span data-stu-id="487fb-153">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete_subscription_message()` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="487fb-154">El método `delete_subscription_message()` marcará el mensaje como consumido y lo eliminará de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="487fb-154">The `delete_subscription_message()` method will mark the message as being consumed and remove it from the subscription.</span></span>

<span data-ttu-id="487fb-155">Si el parámetro `:peek_lock` se establece en **false**, la lectura y eliminación del mensaje se convierte en el modelo más simple y funciona mejor para los escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de error.</span><span class="sxs-lookup"><span data-stu-id="487fb-155">If the `:peek_lock` parameter is set to **false**, reading and deleting the message becomes the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="487fb-156">Para entenderlo mejor, pongamos una situación en la que un consumidor emite la solicitud de recepción que se bloquea antes de procesarla.</span><span class="sxs-lookup"><span data-stu-id="487fb-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="487fb-157">Como el Bus de servicio habrá marcado el mensaje como consumido, cuando la aplicación se reinicie y empiece a consumir mensajes de nuevo, habrá perdido el mensaje que se consumió antes del bloqueo.</span><span class="sxs-lookup"><span data-stu-id="487fb-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="487fb-158">En el ejemplo siguiente se muestra cómo se pueden recibir y procesar mensajes mediante `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="487fb-158">The following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="487fb-159">El ejemplo primero recibe y elimina un mensaje de la suscripción `low-messages` mediante `:peek_lock` establecido en **false**; después, recibe otro mensaje de `high-messages` y, por último, elimina el mensaje mediante `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="487fb-159">The example first receives and deletes a message from the `low-messages` subscription by using `:peek_lock` set to **false**, then it receives another message from the `high-messages` and then deletes the message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="487fb-160">Actuación ante errores de la aplicación y mensajes que no se pueden leer</span><span class="sxs-lookup"><span data-stu-id="487fb-160">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="487fb-161">El Bus de servicio proporciona una funcionalidad que le ayuda a superar sin problemas los errores de la aplicación o las dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="487fb-161">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="487fb-162">Si por cualquier motivo una aplicación de recepción es incapaz de procesar el mensaje, entonces puede llamar al método `unlock_subscription_message()` del objeto **Azure::ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="487fb-162">If a receiver application is unable to process the message for some reason, then it can call the `unlock_subscription_message()` method on the **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="487fb-163">Esto hace que Service Bus desbloquee el mensaje de la suscripción y esté disponible para que pueda volver a recibirse, ya sea por la misma aplicación que lo consume o por otra.</span><span class="sxs-lookup"><span data-stu-id="487fb-163">This causes Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="487fb-164">También hay un tiempo de espera asociado con un mensaje bloqueado en la suscripción y, si la aplicación no puede procesar el mensaje antes de que finalice el tiempo de espera del bloqueo (por ejemplo, si la aplicación sufre un error), entonces Service Bus desbloquea el mensaje automáticamente y hace que esté disponible para que pueda volver a recibirse.</span><span class="sxs-lookup"><span data-stu-id="487fb-164">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="487fb-165">En caso de que la aplicación sufra un error después de procesar el mensaje y antes de llamar al método `delete_subscription_message()`, entonces el mensaje se vuelve a entregar a la aplicación cuando esta se reinicie.</span><span class="sxs-lookup"><span data-stu-id="487fb-165">In the event that the application crashes after processing the message but before the `delete_subscription_message()` method is called, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="487fb-166">Habitualmente se denomina *Al menos un procesamiento*, es decir, cada mensaje se procesará al menos una vez; aunque en determinadas situaciones podría volver a entregarse el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="487fb-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="487fb-167">Si el escenario no puede tolerar el procesamiento duplicado, entonces los desarrolladores de la aplicación deberían agregar lógica adicional a su aplicación para solucionar la entrega de mensajes duplicados.</span><span class="sxs-lookup"><span data-stu-id="487fb-167">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="487fb-168">A menudo, esta lógica se consigue usando la propiedad `message_id` del mensaje, que permanecerá constante en todos los intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="487fb-168">This logic is often achieved using the `message_id` property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="487fb-169">Eliminación de temas y suscripciones</span><span class="sxs-lookup"><span data-stu-id="487fb-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="487fb-170">Los temas y las suscripciones son permanentes, por lo que deben eliminarse explícitamente a través del [Azure Portal][Azure portal] o mediante programación.</span><span class="sxs-lookup"><span data-stu-id="487fb-170">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="487fb-171">En el ejemplo siguiente se muestra cómo eliminar el tema llamado `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="487fb-171">The example below demonstrates how to delete the topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="487fb-172">Al eliminar un tema también se eliminan todas las suscripciones que estén registradas con él.</span><span class="sxs-lookup"><span data-stu-id="487fb-172">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="487fb-173">También se pueden eliminar las suscripciones de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="487fb-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="487fb-174">El código siguiente muestra cómo eliminar la suscripción denominada `high-messages` del tema `test-topic`:</span><span class="sxs-lookup"><span data-stu-id="487fb-174">The following code demonstrates how to delete the subscription named `high-messages` from the `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="487fb-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="487fb-175">Next steps</span></span>
<span data-ttu-id="487fb-176">Ahora que conoce los fundamentos de los temas del Bus de servicio, siga estos vínculos para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="487fb-176">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="487fb-177">Vea [Colas, temas y suscripciones](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="487fb-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="487fb-178">Referencia de API para [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="487fb-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="487fb-179">Visite el repositorio de [SDK de Azure para Ruby](https://github.com/Azure/azure-sdk-for-ruby) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="487fb-179">Visit the [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
