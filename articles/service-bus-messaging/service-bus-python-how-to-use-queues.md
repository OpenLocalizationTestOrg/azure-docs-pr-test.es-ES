---
title: Uso de colas de Service Bus de Azure con Python | Microsoft Docs
description: Aprenda a usar las colas de del Bus de servicio de Azure desde Python.
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
ms.openlocfilehash: e1e81ad1d7b4fe0e044917f090cac59dfd5b6332
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-python"></a><span data-ttu-id="3c5a7-103">Uso de colas de Service Bus con Python</span><span class="sxs-lookup"><span data-stu-id="3c5a7-103">How to use Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="3c5a7-104">Este artículo describe cómo usar las colas del Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-104">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="3c5a7-105">Los ejemplos están escritos en Python y usan el [paquete de Service Bus de Azure para Python][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="3c5a7-105">The samples are written in Python and use the [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="3c5a7-106">Entre los escenarios proporcionados se incluyen los siguientes: **creación de colas, envío y recepción de mensajes** y **eliminación de colas**.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-106">The scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="3c5a7-107">Para instalar Python o el [paquete de Service Bus de Azure para Python][Python Azure Service Bus package], consulte la [Guía de instalación de Python](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="3c5a7-107">To install Python or the [Python Azure Service Bus package][Python Azure Service Bus package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="3c5a7-108">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="3c5a7-108">Create a queue</span></span>
<span data-ttu-id="3c5a7-109">El objeto **ServiceBusService** le permite trabajar con colas.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-109">The **ServiceBusService** object enables you to work with queues.</span></span> <span data-ttu-id="3c5a7-110">Agregue el siguiente código cerca de la parte superior de todo archivo Python en el que desee obtener acceso al Bus de servicio mediante programación:</span><span class="sxs-lookup"><span data-stu-id="3c5a7-110">Add the following code near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="3c5a7-111">El siguiente código crea un objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-111">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="3c5a7-112">Reemplace `mynamespace`, `sharedaccesskeyname` y `sharedaccesskey` por el espacio de nombres, el valor y el nombre de clave de la firma de acceso compartido (SAS).</span><span class="sxs-lookup"><span data-stu-id="3c5a7-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="3c5a7-113">Los valores para el nombre de clave y el valor de la SAS pueden encontrarse en la información de conexión de [Azure Portal][Azure portal] o en el panel **Propiedades** de Visual Studio al seleccionar el espacio de nombres de Service Bus en el Explorador de servidores (como se muestra en la sección anterior).</span><span class="sxs-lookup"><span data-stu-id="3c5a7-113">The values for the SAS key name and value can be found in the [Azure portal][Azure portal] connection information, or in the Visual Studio **Properties** pane when selecting the Service Bus namespace in Server Explorer (as shown in the previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="3c5a7-114">El método `create_queue` también admite opciones adicionales, que le permiten invalidar la configuración predeterminada de las colas, como el período de vida de los mensajes (TTL) o el tamaño máximo de las colas.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-114">The `create_queue` method also supports additional options, which enable you to override default queue settings such as message time to live (TTL) or maximum queue size.</span></span> <span data-ttu-id="3c5a7-115">En el siguiente ejemplo se establece el tamaño máximo de las colas en 5 GB y el valor de TTL en 1 minuto:</span><span class="sxs-lookup"><span data-stu-id="3c5a7-115">The following example sets the maximum queue size to 5 GB, and the TTL value to 1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="3c5a7-116">mensajes a una cola</span><span class="sxs-lookup"><span data-stu-id="3c5a7-116">Send messages to a queue</span></span>
<span data-ttu-id="3c5a7-117">Para enviar un mensaje a una cola de Service Bus, la aplicación debe llamar al método `send_queue_message` del objeto **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-117">To send a message to a Service Bus queue, your application calls the `send_queue_message` method on the **ServiceBusService** object.</span></span>

<span data-ttu-id="3c5a7-118">En el ejemplo siguiente se muestra cómo enviar un mensaje de prueba a la cola `taskqueue` mediante `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="3c5a7-118">The following example demonstrates how to send a test message to the queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="3c5a7-119">El tamaño máximo de mensaje que admiten las colas de Service Bus es de 256 KB en el [nivel Estándar](service-bus-premium-messaging.md) y de 1 MB en el [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="3c5a7-119">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="3c5a7-120">El encabezado, que incluye propiedades de la aplicación estándar y personalizadas, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-120">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="3c5a7-121">No hay límite para el número de mensajes que contiene una cola, pero hay un tope para el tamaño total de los mensajes contenidos en una cola.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-121">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="3c5a7-122">El tamaño de la cola se define en el momento de la creación, con un límite de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="3c5a7-123">Para obtener más información sobre las cuotas, vea [Cuotas de Service Bus][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="3c5a7-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="3c5a7-124">mensajes de una cola</span><span class="sxs-lookup"><span data-stu-id="3c5a7-124">Receive messages from a queue</span></span>
<span data-ttu-id="3c5a7-125">Los mensajes se reciben de una cola utilizando el método `receive_queue_message` del objeto **ServiceBusService**:</span><span class="sxs-lookup"><span data-stu-id="3c5a7-125">Messages are received from a queue using the `receive_queue_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="3c5a7-126">Los mensajes se eliminan de la cola a medida que se leen cuando el parámetro `peek_lock` está establecido en **False**.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-126">Messages are deleted from the queue as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="3c5a7-127">Puede leer y bloquear los mensajes sin eliminarlos de la cola si establece el parámetro opcional `peek_lock` en **True**.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-127">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="3c5a7-128">El comportamiento por el que los mensajes se eliminan tras leerlos como parte del proceso de recepción es el modelo más sencillo y el que mejor funciona en aquellas situaciones en las que una aplicación puede tolerar que no se procese un mensaje en caso de error.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-128">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="3c5a7-129">Para entenderlo mejor, pongamos una situación en la que un consumidor emite la solicitud de recepción que se bloquea antes de procesarla.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-129">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="3c5a7-130">Como el Bus de servicio habrá marcado el mensaje como consumido, cuando la aplicación se reinicie y empiece a consumir mensajes de nuevo, habrá perdido el mensaje que se consumió antes del bloqueo.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-130">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="3c5a7-131">Si el parámetro `peek_lock` está establecido en **True**, el proceso de recepción se convierte en una operación en dos fases que permite admitir aplicaciones que no toleran la pérdida de mensajes.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-131">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="3c5a7-132">Cuando el Bus de servicio recibe una solicitud, busca el siguiente mensaje que se va a consumir, lo bloquea para impedir que otros consumidores lo reciban y, a continuación, lo devuelve a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-132">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="3c5a7-133">Una vez que la aplicación termina de procesar el mensaje (o lo almacena de forma confiable para su futuro procesamiento), completa la segunda fase del proceso de recepción llamando al método **delete** en el objeto **Message**.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-133">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling the **delete** method on the **Message** object.</span></span> <span data-ttu-id="3c5a7-134">El método **delete** marcará el mensaje como consumido y lo eliminará de la cola.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-134">The **delete** method will mark the message as being consumed and remove it from the queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="3c5a7-135">Actuación ante errores de la aplicación y mensajes que no se pueden leer</span><span class="sxs-lookup"><span data-stu-id="3c5a7-135">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="3c5a7-136">El Bus de servicio proporciona una funcionalidad que le ayuda a superar sin problemas los errores de la aplicación o las dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-136">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="3c5a7-137">Si por cualquier motivo una aplicación de recepción es incapaz de procesar el mensaje, entonces puede llamar al método **unlock** del objeto **Message**.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-137">If a receiver application is unable to process the message for some reason, then it can call the **unlock** method on the **Message** object.</span></span> <span data-ttu-id="3c5a7-138">Esto hará que el Bus de servicio desbloquee el mensaje de la cola y esté disponible para que pueda volver a recibirse, ya sea por la misma aplicación que lo consume o por otra.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-138">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="3c5a7-139">También hay un tiempo de espera asociado con un mensaje bloqueado en la cola y, si la aplicación no puede procesar el mensaje antes de que finalice el tiempo de espera del bloqueo (por ejemplo, si la aplicación sufre un error), entonces el bus de servicio desbloquea el mensaje automáticamente y hace que esté disponible para que pueda volver a recibirse.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-139">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="3c5a7-140">En caso de que la aplicación sufra un error después de procesar el mensaje y antes de llamar al método **delete**, entonces el mensaje se volverá a entregar a la aplicación cuando esta se reinicie.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-140">In the event that the application crashes after processing the message but before the **delete** method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="3c5a7-141">Habitualmente se denomina **Al menos un procesamiento**, es decir, cada mensaje se procesará al menos una vez; aunque en determinadas situaciones podría volver a entregarse el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="3c5a7-142">Si el escenario no puede tolerar el procesamiento duplicado, entonces los desarrolladores de la aplicación deberían agregar lógica adicional a su aplicación para solucionar la entrega de mensajes duplicados.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-142">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="3c5a7-143">A menudo, esto se consigue usando la propiedad **MessageId** del mensaje, que permanecerá constante en todos los intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-143">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c5a7-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c5a7-144">Next steps</span></span>
<span data-ttu-id="3c5a7-145">Ahora que conoce los fundamentos de las colas de Service Bus, consulte estos vínculos para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="3c5a7-145">Now that you have learned the basics of Service Bus queues, see these articles to learn more.</span></span>

* <span data-ttu-id="3c5a7-146">[Colas, temas y suscripciones][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="3c5a7-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

