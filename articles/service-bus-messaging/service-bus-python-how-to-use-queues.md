---
title: pone en cola con Python aaaHow toouse Service Bus de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Service Bus de Azure pone en cola de Python."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a><span data-ttu-id="363d6-103">¿Cómo toouse Bus de servicio pone en cola con Python</span><span class="sxs-lookup"><span data-stu-id="363d6-103">How toouse Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="363d6-104">Este artículo se describe cómo toouse colas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="363d6-104">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="363d6-105">ejemplos de Hello están escritos en Python y usar hello [paquete de Python Azure Service Bus][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="363d6-105">hello samples are written in Python and use hello [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="363d6-106">Hello escenarios descritos se incluyen **crear colas, enviar y recibir mensajes**, y **eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="363d6-106">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="363d6-107">tooinstall Python o hello [paquete de Python Azure Service Bus][Python Azure Service Bus package], vea hello [Guía de instalación de Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="363d6-107">tooinstall Python or hello [Python Azure Service Bus package][Python Azure Service Bus package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="363d6-108">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="363d6-108">Create a queue</span></span>
<span data-ttu-id="363d6-109">Hola **ServiceBusService** objeto permite toowork con colas.</span><span class="sxs-lookup"><span data-stu-id="363d6-109">hello **ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="363d6-110">Agregue Hola después código cerca de la parte superior de Hola de cualquier archivo de Python en el que desea acceso tooprogrammatically Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="363d6-110">Add hello following code near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="363d6-111">Hello código siguiente se crea un **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="363d6-111">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="363d6-112">Reemplace `mynamespace`, `sharedaccesskeyname` y `sharedaccesskey` por el espacio de nombres, el valor y el nombre de clave de la firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="363d6-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="363d6-113">Hello valores de nombre de clave de SAS de Hola y el valor pueden encontrarse en hello [portal de Azure] [ Azure portal] información de conexión, o en Visual Studio hello **propiedades** panel al seleccionar Hola nombres de Bus de servicio en el Explorador de servidores (como se muestra en la sección anterior de hello).</span><span class="sxs-lookup"><span data-stu-id="363d6-113">hello values for hello SAS key name and value can be found in hello [Azure portal][Azure portal] connection information, or in hello Visual Studio **Properties** pane when selecting hello Service Bus namespace in Server Explorer (as shown in hello previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="363d6-114">Hola `create_queue` método es compatible también con opciones adicionales, que permiten la configuración de la cola de toooverride de forma predeterminada como la hora del mensaje toolive (TTL) o tamaño máximo de cola.</span><span class="sxs-lookup"><span data-stu-id="363d6-114">hello `create_queue` method also supports additional options, which enable you toooverride default queue settings such as message time toolive (TTL) or maximum queue size.</span></span> <span data-ttu-id="363d6-115">Hello en el ejemplo siguiente se establece Hola cola máximo tamaño too5 GB y minuto de hello TTL valor too1:</span><span class="sxs-lookup"><span data-stu-id="363d6-115">hello following example sets hello maximum queue size too5 GB, and hello TTL value too1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="363d6-116">Cola de mensajes tooa de envío</span><span class="sxs-lookup"><span data-stu-id="363d6-116">Send messages tooa queue</span></span>
<span data-ttu-id="363d6-117">la aplicación llama a una cola de Service Bus de mensajes tooa toosend, hello `send_queue_message` método en hello **ServiceBusService** objeto.</span><span class="sxs-lookup"><span data-stu-id="363d6-117">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message` method on hello **ServiceBusService** object.</span></span>

<span data-ttu-id="363d6-118">Hello en el ejemplo siguiente se muestra cómo toosend una cola de toohello de mensajes de prueba denominado `taskqueue` con `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="363d6-118">hello following example demonstrates how toosend a test message toohello queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="363d6-119">Las colas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="363d6-119">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="363d6-120">encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="363d6-120">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="363d6-121">No hay ningún límite en el número de Hola de mensajes que se ponen en una cola pero no hay un límite en tamaño total de Hola de mantiene una cola de mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="363d6-121">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="363d6-122">El tamaño de la cola se define en el momento de la creación, con un límite de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="363d6-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="363d6-123">Para obtener más información sobre las cuotas, vea [Cuotas de Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="363d6-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="363d6-124">mensajes de una cola</span><span class="sxs-lookup"><span data-stu-id="363d6-124">Receive messages from a queue</span></span>
<span data-ttu-id="363d6-125">Se reciben mensajes de una cola utilizando hello `receive_queue_message` método en hello **ServiceBusService** objeto:</span><span class="sxs-lookup"><span data-stu-id="363d6-125">Messages are received from a queue using hello `receive_queue_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="363d6-126">Se eliminan mensajes de cola de hello cuando se leen cuando Hola parámetro `peek_lock` se establece demasiado**False**.</span><span class="sxs-lookup"><span data-stu-id="363d6-126">Messages are deleted from hello queue as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="363d6-127">Puede leer (peek) y bloquear los mensajes de bienvenida sin eliminarla de la cola de Hola por establecer el parámetro de hello `peek_lock` demasiado**True**.</span><span class="sxs-lookup"><span data-stu-id="363d6-127">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="363d6-128">Hola comportamiento de lectura y eliminación de mensajes de bienvenida tal como parte del programa Hola a la operación de recepción es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error.</span><span class="sxs-lookup"><span data-stu-id="363d6-128">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="363d6-129">toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo.</span><span class="sxs-lookup"><span data-stu-id="363d6-129">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="363d6-130">Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="363d6-130">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="363d6-131">Si hello `peek_lock` parámetro está establecido demasiado**True**, Hola de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos.</span><span class="sxs-lookup"><span data-stu-id="363d6-131">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="363d6-132">Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="363d6-132">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="363d6-133">Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola recibir proceso que realiza la llamada hello **eliminar** método en hello **mensaje** objeto.</span><span class="sxs-lookup"><span data-stu-id="363d6-133">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling hello **delete** method on hello **Message** object.</span></span> <span data-ttu-id="363d6-134">Hola **eliminar** método marcar Hola mensaje como consumido y quitarlo de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="363d6-134">hello **delete** method will mark hello message as being consumed and remove it from hello queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="363d6-135">No se puede leer mensajes y cómo se bloquea la aplicación de toohandle</span><span class="sxs-lookup"><span data-stu-id="363d6-135">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="363d6-136">Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="363d6-136">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="363d6-137">Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello **desbloquear** método en hello **mensaje** objeto.</span><span class="sxs-lookup"><span data-stu-id="363d6-137">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlock** method on hello **Message** object.</span></span> <span data-ttu-id="363d6-138">Esto provocará el mensaje de saludo toounlock de Bus de servicio de cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.</span><span class="sxs-lookup"><span data-stu-id="363d6-138">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="363d6-139">También hay un tiempo de espera asociado a un mensaje bloqueado en cola de Hola y si se produce un error de aplicación de hello tooprocess Hola mensaje antes de Hola tiempo de espera de bloqueo expira (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloqueará automáticamente mensajes de bienvenida y hacerla disponible toobe recibido de nuevo.</span><span class="sxs-lookup"><span data-stu-id="363d6-139">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="363d6-140">Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello **eliminar** se llama al método, mensaje de saludo será aplicación toohello entregados de nuevo cuando se reinicia.</span><span class="sxs-lookup"><span data-stu-id="363d6-140">In hello event that hello application crashes after processing hello message but before hello **delete** method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="363d6-141">Esto se suele denominar **al menos una vez procesamiento**; es decir, cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="363d6-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="363d6-142">Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje.</span><span class="sxs-lookup"><span data-stu-id="363d6-142">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="363d6-143">A menudo esto se logra utilizando hello **MessageId** propiedad del mensaje de Hola, que permanece constante entre intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="363d6-143">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="363d6-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="363d6-144">Next steps</span></span>
<span data-ttu-id="363d6-145">Ahora que ha aprendido los conceptos básicos de Hola de colas de Service Bus, vea estos toolearn artículos más.</span><span class="sxs-lookup"><span data-stu-id="363d6-145">Now that you have learned hello basics of Service Bus queues, see these articles toolearn more.</span></span>

* <span data-ttu-id="363d6-146">[Colas, temas y suscripciones][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="363d6-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

