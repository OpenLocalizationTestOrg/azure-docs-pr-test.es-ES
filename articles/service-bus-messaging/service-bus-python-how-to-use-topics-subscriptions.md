---
title: temas de Service Bus de Azure aaaHow toouse con Python | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Service Bus de Azure temas y suscripciones de Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="35517-103">¿Cómo toouse Service Bus temas y suscripciones a Python</span><span class="sxs-lookup"><span data-stu-id="35517-103">How toouse Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="35517-104">Este artículo se describe cómo toouse Service Bus temas y suscripciones.</span><span class="sxs-lookup"><span data-stu-id="35517-104">This article describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="35517-105">ejemplos de Hello están escritos en Python y usar hello [paquete Azure SDK para Python][Azure Python package].</span><span class="sxs-lookup"><span data-stu-id="35517-105">hello samples are written in Python and use hello [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="35517-106">Hello escenarios descritos se incluyen **crear temas y suscripciones**, **crear filtros de suscripción**, **enviar tema de mensajes tooa**, **recibir mensajes de una suscripción**, y **eliminar temas y suscripciones**.</span><span class="sxs-lookup"><span data-stu-id="35517-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="35517-107">Para obtener más información acerca de temas y suscripciones, vea hello [pasos](#next-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="35517-107">For more information about topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="35517-108">Si necesita tooinstall Python o hello [paquete de Python de Azure][Azure Python package], vea hello [Guía de instalación de Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="35517-108">If you need tooinstall Python or hello [Azure Python package][Azure Python package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="35517-109">de un tema</span><span class="sxs-lookup"><span data-stu-id="35517-109">Create a topic</span></span>
<span data-ttu-id="35517-110">Hola **ServiceBusService** objeto permite toowork con temas.</span><span class="sxs-lookup"><span data-stu-id="35517-110">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="35517-111">Agregue los siguiente Hola cerca de parte superior de Hola de cualquier archivo de Python en el que desea acceso tooprogrammatically Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="35517-111">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="35517-112">Hello código siguiente se crea un **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="35517-112">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="35517-113">Reemplace `mynamespace`, `sharedaccesskeyname` y `sharedaccesskey` por el espacio de nombres real, el valor y el nombre de clave de la firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="35517-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="35517-114">Puede obtener los valores de Hola Hola SAS como nombre de clave y valor de hello [portal de Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="35517-114">You can obtain hello values for hello SAS key name and value from hello [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="35517-115">Hola `create_topic` método es compatible también con opciones adicionales, que permiten la configuración de tema predeterminada toooverride como tamaño de tema toolive o máximo de tiempo de mensaje.</span><span class="sxs-lookup"><span data-stu-id="35517-115">hello `create_topic` method also supports additional options, which enable you toooverride default topic settings such as message time toolive or maximum topic size.</span></span> <span data-ttu-id="35517-116">Hello en el ejemplo siguiente se establece Hola tema máximo tamaño too5 GB y un valor de hora toolive (TTL) de 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="35517-116">hello following example sets hello maximum topic size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="35517-117">Creación de suscripciones</span><span class="sxs-lookup"><span data-stu-id="35517-117">Create subscriptions</span></span>
<span data-ttu-id="35517-118">También se crean suscripciones tootopics con hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="35517-118">Subscriptions tootopics are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="35517-119">Las suscripciones se denominan y pueden tener un filtro opcional que restringe el conjunto de Hola de mensajes entregados cola virtual de la suscripción de toohello.</span><span class="sxs-lookup"><span data-stu-id="35517-119">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="35517-120">Las suscripciones son persistentes y continuará tooexist hasta que ambos se o hello toowhich de tema está suscrito, se eliminan.</span><span class="sxs-lookup"><span data-stu-id="35517-120">Subscriptions are persistent and will continue tooexist until either they, or hello topic toowhich they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="35517-121">Crea una suscripción con el filtro de hello predeterminado (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="35517-121">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="35517-122">Hola **MatchAll** filtro es Hola predeterminado que se usa si se especifica ningún filtro cuando se crea una nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="35517-122">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="35517-123">Cuando Hola **MatchAll** se utiliza el filtro, tema de toohello publicada de todos los mensajes se colocan en cola virtual de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="35517-123">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="35517-124">Hello en el ejemplo siguiente se crea una suscripción denominada `AllMessages` y utiliza Hola predeterminado **MatchAll** filtro.</span><span class="sxs-lookup"><span data-stu-id="35517-124">hello following example creates a subscription named `AllMessages` and uses hello default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="35517-125">Creación de suscripciones con filtros</span><span class="sxs-lookup"><span data-stu-id="35517-125">Create subscriptions with filters</span></span>
<span data-ttu-id="35517-126">También puede definir filtros que le permiten toospecify que envían los mensajes tooa tema debe aparecer en un plazo de una suscripción de tema específico.</span><span class="sxs-lookup"><span data-stu-id="35517-126">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="35517-127">Hola tipo más flexible de filtro compatible con las suscripciones es un **SqlFilter**, que implementa un subconjunto de SQL92.</span><span class="sxs-lookup"><span data-stu-id="35517-127">hello most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="35517-128">Filtros SQL funcionan en las propiedades de Hola de mensajes de Hola que están publicados toohello tema.</span><span class="sxs-lookup"><span data-stu-id="35517-128">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="35517-129">Para obtener más información acerca de las expresiones de Hola que puede usarse con un filtro SQL, vea hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sintaxis.</span><span class="sxs-lookup"><span data-stu-id="35517-129">For more information about hello expressions that can be used with a SQL filter, see hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="35517-130">Puede agregar filtros tooa suscripción mediante hello **crear\_regla** método de hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="35517-130">You can add filters tooa subscription by using hello **create\_rule** method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="35517-131">Este método permite tooadd nueva filtros tooan existente suscripción.</span><span class="sxs-lookup"><span data-stu-id="35517-131">This method allows you tooadd new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="35517-132">Porque el filtro de hello predeterminado se aplica automáticamente tooall nuevas suscripciones, primero debe quitar filtro predeterminado de Hola o hello **MatchAll** invalidará cualquier otro filtro que se puede especificar.</span><span class="sxs-lookup"><span data-stu-id="35517-132">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="35517-133">Puede quitar regla predeterminada de hello mediante hello `delete_rule` método de hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="35517-133">You can remove hello default rule by using hello `delete_rule` method of hello **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="35517-134">Hello en el ejemplo siguiente se crea una suscripción denominada `HighMessages` con un **SqlFilter** que selecciona sólo los mensajes que tienen un personalizado `messagenumber` propiedad mayor que 3:</span><span class="sxs-lookup"><span data-stu-id="35517-134">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="35517-135">De forma similar, hello en el ejemplo siguiente se crea una suscripción denominada `LowMessages` con un **SqlFilter** que selecciona sólo los mensajes que tienen un `messagenumber` propiedad menor o igual too3:</span><span class="sxs-lookup"><span data-stu-id="35517-135">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="35517-136">Ahora, cuando se envía un mensaje demasiado`mytopic` siempre se entrega tooreceivers suscrito toohello **AllMessages** suscripción al tema y tooreceivers selectivamente entregado suscrito toohello **HighMessages**  y **LowMessages** suscripciones al tema (según el contenido del mensaje Hola).</span><span class="sxs-lookup"><span data-stu-id="35517-136">Now, when a message is sent too`mytopic` it is always delivered tooreceivers subscribed toohello **AllMessages** topic subscription, and selectively delivered tooreceivers subscribed toohello **HighMessages** and **LowMessages** topic subscriptions (depending on hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="35517-137">Enviar tema tooa de mensajes</span><span class="sxs-lookup"><span data-stu-id="35517-137">Send messages tooa topic</span></span>
<span data-ttu-id="35517-138">toosend un tema de Bus de servicio de tooa de mensaje, la aplicación debe utilizar hello `send_topic_message` método de hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="35517-138">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message` method of hello **ServiceBusService** object.</span></span>

<span data-ttu-id="35517-139">Hello en el ejemplo siguiente se muestra cómo prueba toosend cinco mensajes demasiado`mytopic`.</span><span class="sxs-lookup"><span data-stu-id="35517-139">hello following example demonstrates how toosend five test messages too`mytopic`.</span></span> <span data-ttu-id="35517-140">Tenga en cuenta que hello `messagenumber` valor de propiedad de cada mensaje varía en función de iteración de Hola de bucle de hello (Esto determina qué suscripciones reciban):</span><span class="sxs-lookup"><span data-stu-id="35517-140">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="35517-141">Temas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="35517-141">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="35517-142">encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="35517-142">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="35517-143">No hay ningún límite en el número de Hola de mensajes retenidos en un tema, pero hay un límite en el tamaño total de Hola de mensajes de Hola mantenidos por un tema.</span><span class="sxs-lookup"><span data-stu-id="35517-143">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="35517-144">El tamaño de los temas se define en el momento de la creación (el límite máximo es de 5 GB).</span><span class="sxs-lookup"><span data-stu-id="35517-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="35517-145">Para obtener más información sobre las cuotas, vea [Cuotas de Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="35517-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="35517-146">Recepción de mensajes de una suscripción</span><span class="sxs-lookup"><span data-stu-id="35517-146">Receive messages from a subscription</span></span>
<span data-ttu-id="35517-147">Los mensajes se reciben de una suscripción mediante hello `receive_subscription_message` método en hello **ServiceBusService** objeto:</span><span class="sxs-lookup"><span data-stu-id="35517-147">Messages are received from a subscription using hello `receive_subscription_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="35517-148">Se eliminan mensajes de suscripción de hello cuando se leen cuando Hola parámetro `peek_lock` se establece demasiado**False**.</span><span class="sxs-lookup"><span data-stu-id="35517-148">Messages are deleted from hello subscription as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="35517-149">Puede leer (peek) y bloquear los mensajes de bienvenida sin eliminarla de la cola de Hola por establecer el parámetro de hello `peek_lock` demasiado**True**.</span><span class="sxs-lookup"><span data-stu-id="35517-149">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="35517-150">Hola comportamiento de lectura y eliminación de mensajes de bienvenida tal como parte del programa Hola a la operación de recepción es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error.</span><span class="sxs-lookup"><span data-stu-id="35517-150">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="35517-151">toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo.</span><span class="sxs-lookup"><span data-stu-id="35517-151">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="35517-152">Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="35517-152">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="35517-153">Si hello `peek_lock` parámetro está establecido demasiado**True**, Hola de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos.</span><span class="sxs-lookup"><span data-stu-id="35517-153">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="35517-154">Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="35517-154">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="35517-155">Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a `delete` método en hello **mensaje** objeto.</span><span class="sxs-lookup"><span data-stu-id="35517-155">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete` method on hello **Message** object.</span></span> <span data-ttu-id="35517-156">Hola `delete` método marca el mensaje Hola como consumido y lo quita de la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="35517-156">hello `delete` method marks hello message as being consumed and removes it from hello subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="35517-157">No se puede leer mensajes y cómo se bloquea la aplicación de toohandle</span><span class="sxs-lookup"><span data-stu-id="35517-157">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="35517-158">Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="35517-158">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="35517-159">Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello `unlock` método en hello **mensaje** objeto.</span><span class="sxs-lookup"><span data-stu-id="35517-159">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock` method on hello **Message** object.</span></span> <span data-ttu-id="35517-160">Esto provocará el mensaje de saludo toounlock de Bus de servicio de suscripción de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.</span><span class="sxs-lookup"><span data-stu-id="35517-160">This will cause Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="35517-161">También hay un tiempo de espera asociado a un mensaje bloqueado dentro de suscripción de Hola y si la aplicación hello produce un error en el mensaje de saludo tooprocess antes de tiempo de espera de bloqueo de Hola expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloquea el mensaje de bienvenida de automáticamente y la convierte en disponible toobe recibido de nuevo.</span><span class="sxs-lookup"><span data-stu-id="35517-161">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="35517-162">Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello `delete` se llama al método, mensaje de saludo será aplicación toohello entregados de nuevo cuando se reinicia.</span><span class="sxs-lookup"><span data-stu-id="35517-162">In hello event that hello application crashes after processing hello message but before hello `delete` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="35517-163">Esto se suele denominar *al menos una vez procesamiento*; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="35517-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="35517-164">Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje.</span><span class="sxs-lookup"><span data-stu-id="35517-164">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="35517-165">A menudo esto se logra utilizando hello **MessageId** propiedad del mensaje de Hola, que permanece constante entre intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="35517-165">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="35517-166">Eliminación de temas y suscripciones</span><span class="sxs-lookup"><span data-stu-id="35517-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="35517-167">Temas y suscripciones son persistentes y debe ser explícitamente eliminados a través de hello [portal de Azure] [ Azure portal] o mediante programación.</span><span class="sxs-lookup"><span data-stu-id="35517-167">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="35517-168">Hello en el ejemplo siguiente se muestra cómo se denomina tema de hello toodelete `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="35517-168">hello following example shows how toodelete hello topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="35517-169">Eliminar un tema, también elimina todas las suscripciones que están registradas en el tema de Hola.</span><span class="sxs-lookup"><span data-stu-id="35517-169">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="35517-170">También se pueden eliminar las suscripciones de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="35517-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="35517-171">Hello código siguiente muestra cómo toodelete una suscripción denominada `HighMessages` de hello `mytopic` tema:</span><span class="sxs-lookup"><span data-stu-id="35517-171">hello following code shows how toodelete a subscription named `HighMessages` from hello `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="35517-172">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="35517-172">Next steps</span></span>
<span data-ttu-id="35517-173">Ahora que conoce los fundamentos de Hola de temas de Bus de servicio, siga estos toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="35517-173">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="35517-174">Vea [Colas, temas y suscripciones][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="35517-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="35517-175">Referencia para [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="35517-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
