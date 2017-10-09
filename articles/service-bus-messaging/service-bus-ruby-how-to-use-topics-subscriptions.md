---
title: temas de Bus de servicio de aaaHow toouse (Ruby) | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Service Bus temas y suscripciones de Azure. Los ejemplos de código están escritos para aplicaciones Ruby."
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
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="c92c8-104">¿Cómo toouse Service Bus temas y suscripciones con Ruby</span><span class="sxs-lookup"><span data-stu-id="c92c8-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="c92c8-105">Este artículo se describe cómo toouse Service Bus temas y suscripciones desde aplicaciones Ruby.</span><span class="sxs-lookup"><span data-stu-id="c92c8-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="c92c8-106">Hello escenarios descritos se incluyen **crear temas y suscripciones, crear filtros de suscripción, enviar mensajes** tooa tema, **recibir mensajes de una suscripción**, y  **eliminar temas y suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="c92c8-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="c92c8-107">Para obtener más información sobre los temas y suscripciones, vea hello [pasos](#next-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="c92c8-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="c92c8-108">de un tema</span><span class="sxs-lookup"><span data-stu-id="c92c8-108">Create a topic</span></span>
<span data-ttu-id="c92c8-109">Hola **Azure::ServiceBusService** objeto permite toowork con temas.</span><span class="sxs-lookup"><span data-stu-id="c92c8-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="c92c8-110">Hello código siguiente se crea un **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="c92c8-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="c92c8-111">toocreate un tema, usar hello `create_topic()` método.</span><span class="sxs-lookup"><span data-stu-id="c92c8-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="c92c8-112">Hola de ejemplo siguiente crea un tema o imprime errores Hola si hay alguno.</span><span class="sxs-lookup"><span data-stu-id="c92c8-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="c92c8-113">También puede pasar un **Azure::ServiceBus::Topic** objeto con opciones adicionales, que permiten la configuración de tema predeterminada toooverride como el tamaño de cola toolive o máximo de tiempo de mensaje.</span><span class="sxs-lookup"><span data-stu-id="c92c8-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="c92c8-114">Hello ejemplo siguiente se muestra configuración máximo de cola de hello too5 GB de tamaño y de tiempo too1 toolive minuto:</span><span class="sxs-lookup"><span data-stu-id="c92c8-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="c92c8-115">Creación de suscripciones</span><span class="sxs-lookup"><span data-stu-id="c92c8-115">Create subscriptions</span></span>
<span data-ttu-id="c92c8-116">Suscripciones al tema también se crean con hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="c92c8-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="c92c8-117">Las suscripciones se denominan y pueden tener un filtro opcional que restringe el conjunto de Hola de mensajes entregados cola virtual de la suscripción de toohello.</span><span class="sxs-lookup"><span data-stu-id="c92c8-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="c92c8-118">Las suscripciones son persistentes y continuará tooexist hasta que ambos se o hello tema están asociadas, se eliminan.</span><span class="sxs-lookup"><span data-stu-id="c92c8-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="c92c8-119">Si la aplicación contiene lógica toocreate una suscripción, debe comprobar primero si Hola ya existe la suscripción mediante hello getSubscription método.</span><span class="sxs-lookup"><span data-stu-id="c92c8-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="c92c8-120">Crea una suscripción con el filtro de hello predeterminado (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="c92c8-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="c92c8-121">Hola **MatchAll** filtro es Hola predeterminado que se usa si se especifica ningún filtro cuando se crea una nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="c92c8-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="c92c8-122">Cuando Hola **MatchAll** se utiliza el filtro, tema de toohello publicada de todos los mensajes se colocan en cola virtual de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="c92c8-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="c92c8-123">Hello en el ejemplo siguiente se crea una suscripción denominada "todos los mensajes" y usa Hola predeterminado **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="c92c8-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="c92c8-124">Creación de suscripciones con filtros</span><span class="sxs-lookup"><span data-stu-id="c92c8-124">Create subscriptions with filters</span></span>
<span data-ttu-id="c92c8-125">También puede definir filtros que le permiten toospecify que envían los mensajes tooa tema debe aparecer en un plazo de una suscripción específica.</span><span class="sxs-lookup"><span data-stu-id="c92c8-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="c92c8-126">el tipo más flexible de filtro compatible con las suscripciones Hello es hello **Azure::ServiceBus::SqlFilter**, que implementa un subconjunto de SQL92.</span><span class="sxs-lookup"><span data-stu-id="c92c8-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="c92c8-127">Filtros SQL funcionan en las propiedades de Hola de mensajes de Hola que están publicados toohello tema.</span><span class="sxs-lookup"><span data-stu-id="c92c8-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="c92c8-128">Para obtener más información acerca de las expresiones de Hola que pueden usarse con un filtro SQL, revise hello [SqlFilter](service-bus-messaging-sql-filter.md) sintaxis.</span><span class="sxs-lookup"><span data-stu-id="c92c8-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="c92c8-129">Puede agregar filtros tooa suscripción mediante hello `create_rule()` método de hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="c92c8-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="c92c8-130">Este método permite tooadd nueva filtros tooan existente suscripción.</span><span class="sxs-lookup"><span data-stu-id="c92c8-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="c92c8-131">Puesto que el filtro de hello predeterminado se aplica automáticamente tooall nuevas suscripciones, primero debe quitar el filtro predeterminado de Hola u Hola **MatchAll** invalidará cualquier otro filtro que se puede especificar.</span><span class="sxs-lookup"><span data-stu-id="c92c8-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="c92c8-132">Puede quitar regla predeterminada de hello mediante hello `delete_rule()` método en hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="c92c8-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="c92c8-133">Hello en el ejemplo siguiente se crea una suscripción denominada "mensajes de alta" con un **Azure::ServiceBus::SqlFilter** que selecciona sólo los mensajes que tienen un personalizado `message_number` propiedad mayor que 3:</span><span class="sxs-lookup"><span data-stu-id="c92c8-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

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

<span data-ttu-id="c92c8-134">De forma similar, hello en el ejemplo siguiente se crea una suscripción denominada `low-messages` con una **Azure::ServiceBus::SqlFilter** que selecciona sólo los mensajes que tienen un `message_number` propiedad menor o igual too3:</span><span class="sxs-lookup"><span data-stu-id="c92c8-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

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

<span data-ttu-id="c92c8-135">Cuando se envía un mensaje ahora demasiado`test-topic`, es siempre ser entregado tooreceivers suscrito toohello `all-messages` suscripción al tema y tooreceivers selectivamente entregado suscrito toohello `high-messages` y `low-messages` (suscripciones de tema según el contenido del mensaje de Hola).</span><span class="sxs-lookup"><span data-stu-id="c92c8-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="c92c8-136">Enviar tema tooa de mensajes</span><span class="sxs-lookup"><span data-stu-id="c92c8-136">Send messages tooa topic</span></span>
<span data-ttu-id="c92c8-137">toosend un tema de Bus de servicio de tooa de mensaje, la aplicación debe utilizar hello `send_topic_message()` método en hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="c92c8-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="c92c8-138">Mensajes envían a temas de Bus tooService son instancias de hello **Azure::ServiceBus::BrokeredMessage** objetos.</span><span class="sxs-lookup"><span data-stu-id="c92c8-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="c92c8-139">**Azure::ServiceBus::BrokeredMessage** objetos tienen un conjunto de propiedades estándar (como `label` y `time_to_live`), un diccionario de propiedades de toohold usado personalizadas específicas de la aplicación y un cuerpo de datos de cadena.</span><span class="sxs-lookup"><span data-stu-id="c92c8-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="c92c8-140">Una aplicación puede establecer el cuerpo de Hola de mensaje de saludo pasando un toohello del valor de cadena `send_topic_message()` método y las necesarias propiedades estándar se rellenará con valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="c92c8-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="c92c8-141">Hello en el ejemplo siguiente se muestra cómo prueba toosend cinco mensajes demasiado`test-topic`.</span><span class="sxs-lookup"><span data-stu-id="c92c8-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="c92c8-142">Tenga en cuenta que hello `message_number` valor de propiedad personalizada de cada mensaje varía en función de iteración de Hola de bucle de hello (Esto determina qué suscripción lo recibe):</span><span class="sxs-lookup"><span data-stu-id="c92c8-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="c92c8-143">Temas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="c92c8-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="c92c8-144">encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="c92c8-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="c92c8-145">No hay ningún límite en el número de Hola de mensajes retenidos en un tema, pero hay un límite en el tamaño total de Hola de mensajes de Hola mantenidos por un tema.</span><span class="sxs-lookup"><span data-stu-id="c92c8-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="c92c8-146">El tamaño de los temas se define en el momento de la creación (el límite máximo es de 5 GB).</span><span class="sxs-lookup"><span data-stu-id="c92c8-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="c92c8-147">Recepción de mensajes de una suscripción</span><span class="sxs-lookup"><span data-stu-id="c92c8-147">Receive messages from a subscription</span></span>
<span data-ttu-id="c92c8-148">Los mensajes se reciben de una suscripción mediante hello `receive_subscription_message()` método en hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="c92c8-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="c92c8-149">De forma predeterminada, los mensajes son read(peak) y bloqueado sin eliminarla de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="c92c8-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="c92c8-150">Puede leer y eliminar mensajes de bienvenida de suscripción Hola Hola establecer `peek_lock` opción demasiado**false**.</span><span class="sxs-lookup"><span data-stu-id="c92c8-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="c92c8-151">comportamiento predeterminado de Hello hace Hola lectura y eliminación de una operación de dos fases, esto también hace que las aplicaciones de toosupport posible que no pueden tolerar mensajes perdidos.</span><span class="sxs-lookup"><span data-stu-id="c92c8-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="c92c8-152">Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="c92c8-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="c92c8-153">Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a `delete_subscription_message()` método y proporcionar toobe de mensaje de Hola eliminado como un parámetro.</span><span class="sxs-lookup"><span data-stu-id="c92c8-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="c92c8-154">Hola `delete_subscription_message()` método marcar Hola mensaje como consumido y quitarlo de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="c92c8-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="c92c8-155">Si hello `:peek_lock` parámetro está establecido demasiado**false**, leer y eliminar mensajes de bienvenida se convierte en el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error.</span><span class="sxs-lookup"><span data-stu-id="c92c8-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="c92c8-156">toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo.</span><span class="sxs-lookup"><span data-stu-id="c92c8-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="c92c8-157">Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="c92c8-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="c92c8-158">Hello en el ejemplo siguiente se muestra cómo se pueden recibir mensajes y el uso de procesado `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="c92c8-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="c92c8-159">ejemplo Hello primero recibe y elimina un mensaje de Hola `low-messages` suscripción mediante el uso de `:peek_lock` establecido demasiado**false**, a continuación, recibe otro mensaje de Hola `high-messages` y, a continuación, elimina Hola mensaje utilizando `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="c92c8-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="c92c8-160">No se puede leer mensajes y cómo se bloquea la aplicación de toohandle</span><span class="sxs-lookup"><span data-stu-id="c92c8-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="c92c8-161">Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="c92c8-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="c92c8-162">Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlock_subscription_message()` método en hello **Azure::ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="c92c8-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="c92c8-163">Este causas hello toounlock de Bus de servicio de mensajes dentro de la suscripción de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.</span><span class="sxs-lookup"><span data-stu-id="c92c8-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="c92c8-164">También hay un tiempo de espera asociado a un mensaje bloqueado dentro de suscripción de Hola y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de hello expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará el mensaje de bienvenida de automáticamente y hacerla disponible toobe recibido de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c92c8-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="c92c8-165">Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `delete_subscription_message()` se llama al método, a continuación, mensaje de bienvenida es la aplicación de toohello entregados de nuevo cuando se reinicia.</span><span class="sxs-lookup"><span data-stu-id="c92c8-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="c92c8-166">Esto se suele denominar *al menos una vez procesamiento*; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="c92c8-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="c92c8-167">Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje.</span><span class="sxs-lookup"><span data-stu-id="c92c8-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="c92c8-168">Esta lógica a menudo se logra mediante hello `message_id` propiedad del mensaje de Hola, que permanece constante entre intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="c92c8-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="c92c8-169">Eliminación de temas y suscripciones</span><span class="sxs-lookup"><span data-stu-id="c92c8-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="c92c8-170">Temas y suscripciones son persistentes y debe ser explícitamente eliminados a través de hello [portal de Azure] [ Azure portal] o mediante programación.</span><span class="sxs-lookup"><span data-stu-id="c92c8-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="c92c8-171">ejemplo de Hola siguiente muestra cómo se denomina tema de hello toodelete `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="c92c8-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="c92c8-172">Eliminar un tema, también elimina todas las suscripciones que están registradas en el tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="c92c8-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="c92c8-173">También se pueden eliminar las suscripciones de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="c92c8-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="c92c8-174">Hello código siguiente muestra cómo se denomina suscripción de hello toodelete `high-messages` de hello `test-topic` tema:</span><span class="sxs-lookup"><span data-stu-id="c92c8-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="c92c8-175">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c92c8-175">Next steps</span></span>
<span data-ttu-id="c92c8-176">Ahora que conoce los fundamentos de Hola de temas de Bus de servicio, siga estos toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="c92c8-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="c92c8-177">Vea [Colas, temas y suscripciones](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="c92c8-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="c92c8-178">Referencia de API para [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="c92c8-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="c92c8-179">Visite hello [Azure SDK para Ruby](https://github.com/Azure/azure-sdk-for-ruby) repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c92c8-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
