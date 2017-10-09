---
title: pone en cola aaaHow toouse Service Bus de Azure con Java | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Bus de servicio pone en cola en Azure. Ejemplos de código escritos en Java."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a><span data-ttu-id="5b328-104">¿Cómo toouse Bus de servicio pone en cola con Java</span><span class="sxs-lookup"><span data-stu-id="5b328-104">How toouse Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="5b328-105">Este artículo se describe cómo toouse colas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5b328-105">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="5b328-106">ejemplos de Hello están escritos en Java y usar hello [Azure SDK para Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="5b328-106">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="5b328-107">Hello escenarios descritos se incluyen **crear colas**, **enviar y recibir mensajes**, y **eliminar colas**.</span><span class="sxs-lookup"><span data-stu-id="5b328-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="5b328-108">Configurar el Bus de servicio de aplicación toouse</span><span class="sxs-lookup"><span data-stu-id="5b328-108">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="5b328-109">Asegúrese de que ha instalado hello [Azure SDK para Java] [ Azure SDK for Java] antes de compilar este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5b328-109">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="5b328-110">Si está usando Eclipse, puede instalar hello [Azure Toolkit for Eclipse] [ Azure Toolkit for Eclipse] que incluye hello Azure SDK para Java.</span><span class="sxs-lookup"><span data-stu-id="5b328-110">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="5b328-111">A continuación, puede agregar hello **bibliotecas de Microsoft Azure para Java** tooyour proyecto:</span><span class="sxs-lookup"><span data-stu-id="5b328-111">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="5b328-112">Agregue los siguiente hello `import` superior de toohello instrucciones Hola del archivo de Java:</span><span class="sxs-lookup"><span data-stu-id="5b328-112">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="5b328-113">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="5b328-113">Create a queue</span></span>
<span data-ttu-id="5b328-114">Las operaciones de administración para las colas de Service Bus se pueden realizar por medio de la clase **ServiceBusContract**.</span><span class="sxs-lookup"><span data-stu-id="5b328-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="5b328-115">A **ServiceBusContract** objeto se construyó con una configuración apropiada que encapsula el token SAS con permisos toomanage y hello **ServiceBusContract** clase es punto único de Hola comunicación con Azure.</span><span class="sxs-lookup"><span data-stu-id="5b328-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="5b328-116">Hola **ServiceBusService** clase proporciona métodos toocreate, enumerar y eliminar las colas.</span><span class="sxs-lookup"><span data-stu-id="5b328-116">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete queues.</span></span> <span data-ttu-id="5b328-117">Hola de ejemplo siguiente se muestra cómo un **ServiceBusService** objeto puede ser usado toocreate una cola con el nombre `TestQueue`, con un espacio de nombres denominado `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="5b328-117">hello example below shows how a **ServiceBusService** object can be used toocreate a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="5b328-118">Hay métodos en `QueueInfo` que permiten propiedades de hello cola toobe optimizado (por ejemplo: tooset Hola predeterminado time-to-live (TTL) valor toobe aplica toomessages envía toohello cola).</span><span class="sxs-lookup"><span data-stu-id="5b328-118">There are methods on `QueueInfo` that allow properties of hello queue toobe tuned (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello queue).</span></span> <span data-ttu-id="5b328-119">Hello en el ejemplo siguiente se muestra cómo toocreate una cola denominada `TestQueue` con un tamaño máximo de 5 GB:</span><span class="sxs-lookup"><span data-stu-id="5b328-119">hello following example shows how toocreate a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="5b328-120">Tenga en cuenta que puede usar hello `listQueues` método **ServiceBusContract** objetos toocheck si ya existe una cola con un nombre especificado dentro de un espacio de nombres de servicio.</span><span class="sxs-lookup"><span data-stu-id="5b328-120">Note that you can use hello `listQueues` method on **ServiceBusContract** objects toocheck if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="5b328-121">Cola de mensajes tooa de envío</span><span class="sxs-lookup"><span data-stu-id="5b328-121">Send messages tooa queue</span></span>
<span data-ttu-id="5b328-122">una cola de Service Bus de mensajes tooa toosend, la aplicación obtiene un **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="5b328-122">toosend a message tooa Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="5b328-123">Hola el siguiente código se muestra cómo un mensaje para hello toosend `TestQueue` cola creada previamente en hello `HowToSample` espacio de nombres:</span><span class="sxs-lookup"><span data-stu-id="5b328-123">hello following code shows how toosend a message for hello `TestQueue` queue previously created in hello `HowToSample` namespace:</span></span>

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="5b328-124">Mensajes envían a y recibidos de Bus de servicio colas son instancias de hello [BrokeredMessage] [ BrokeredMessage] clase.</span><span class="sxs-lookup"><span data-stu-id="5b328-124">Messages sent to, and received from Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="5b328-125">[BrokeredMessage] [ BrokeredMessage] objetos tienen un conjunto de propiedades estándar (como [etiqueta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) y [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un diccionario que es usado toohold personalizado propiedades específicas de la aplicación y un cuerpo de datos de aplicación arbitrarios.</span><span class="sxs-lookup"><span data-stu-id="5b328-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="5b328-126">Una aplicación puede establecer cuerpo Hola de mensaje de saludo pasando cualquier objeto serializable en el constructor de Hola de hello [BrokeredMessage][BrokeredMessage], y, a continuación, se utilizará el serializador adecuado Hola objeto de hello tooserialize.</span><span class="sxs-lookup"><span data-stu-id="5b328-126">An application can set hello body of hello message by passing any serializable object into hello constructor of hello [BrokeredMessage][BrokeredMessage], and hello appropriate serializer will then be used tooserialize hello object.</span></span> <span data-ttu-id="5b328-127">También puede especificar un objeto **java.IO.InputStream**.</span><span class="sxs-lookup"><span data-stu-id="5b328-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="5b328-128">Hello en el ejemplo siguiente se muestra cómo prueba toosend cinco mensajes toothe `TestQueue` **MessageSender** se obtenido en el fragmento de código de hello anterior:</span><span class="sxs-lookup"><span data-stu-id="5b328-128">hello following example demonstrates how toosend five test messages toothe `TestQueue` **MessageSender** we obtained in hello previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="5b328-129">Las colas de Bus de servicio admiten un tamaño máximo de los mensajes de 256 KB en hello [nivel estándar](service-bus-premium-messaging.md) y 1 MB en hello [nivel Premium](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="5b328-129">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="5b328-130">encabezado de Hello, que incluye estándar de Hola y propiedades de la aplicación personalizada, puede tener un tamaño máximo de 64 KB.</span><span class="sxs-lookup"><span data-stu-id="5b328-130">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="5b328-131">No hay ningún límite en el número de Hola de mensajes que se ponen en una cola pero no hay un límite en tamaño total de Hola de mantiene una cola de mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="5b328-131">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="5b328-132">El tamaño de la cola se define en el momento de la creación, con un límite de 5 GB.</span><span class="sxs-lookup"><span data-stu-id="5b328-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="5b328-133">mensajes de una cola</span><span class="sxs-lookup"><span data-stu-id="5b328-133">Receive messages from a queue</span></span>
<span data-ttu-id="5b328-134">mensajes de tooreceive de modo principal de saludo de una cola es toouse una **ServiceBusContract** objeto.</span><span class="sxs-lookup"><span data-stu-id="5b328-134">hello primary way tooreceive messages from a queue is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="5b328-135">Los mensajes recibidos pueden funcionar en dos modos distintos: **ReceiveAndDelete** y **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="5b328-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="5b328-136">Cuando se usa hello **ReceiveAndDelete** modo, de recepción es una operación de captura único: es decir, al Bus de servicio recibe una solicitud de lectura para un mensaje en una cola, marca Hola mensaje como consumido y lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="5b328-136">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="5b328-137">**ReceiveAndDelete** modo (que es el modo predeterminado de hello) es el modelo más sencillo de Hola y funciona mejor para escenarios en los que una aplicación puede tolerar no procesar un mensaje en caso de hello de un error.</span><span class="sxs-lookup"><span data-stu-id="5b328-137">**ReceiveAndDelete** mode (which is hello default mode) is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="5b328-138">toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo.</span><span class="sxs-lookup"><span data-stu-id="5b328-138">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span>
<span data-ttu-id="5b328-139">Dado que Service Bus habrá marcado Hola mensaje como consumido, a continuación, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="5b328-139">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="5b328-140">En **PeekLock** , el modo de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos.</span><span class="sxs-lookup"><span data-stu-id="5b328-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="5b328-141">Al Bus de servicio recibe una solicitud, busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="5b328-141">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="5b328-142">Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a **eliminar** en mensajes de bienvenida recibido.</span><span class="sxs-lookup"><span data-stu-id="5b328-142">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="5b328-143">Al Bus de servicio ve hello **eliminar** llamada, se marca el mensaje Hola como consumido y quitarlo de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="5b328-143">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="5b328-144">Hello en el ejemplo siguiente se muestra cómo se pueden recibir mensajes y el uso de procesado **PeekLock** modo (no en el modo de saludo predeterminado).</span><span class="sxs-lookup"><span data-stu-id="5b328-144">hello following example demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="5b328-145">hace un bucle infinito Hello ejemplo siguiente y procesa los mensajes que llegan en nuestro `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="5b328-145">hello example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="5b328-146">No se puede leer mensajes y cómo se bloquea la aplicación de toohandle</span><span class="sxs-lookup"><span data-stu-id="5b328-146">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="5b328-147">Bus de servicio proporciona toohelp de funcionalidad que recuperarse de errores en sus aplicaciones o dificultades para procesar un mensaje.</span><span class="sxs-lookup"><span data-stu-id="5b328-147">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="5b328-148">Si una aplicación receptora no puede tooprocess Hola mensaje por alguna razón, a continuación, puede llamar a hello **unlockMessage** método en mensajes de bienvenida recibido (en lugar de hello **deleteMessage** método).</span><span class="sxs-lookup"><span data-stu-id="5b328-148">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="5b328-149">Este causas hello toounlock de Bus de servicio de mensajes en cola de Hola y hacerla disponible toobe recibido de nuevo, ya sea por Hola mismo consumen aplicación o por otra aplicación que consume.</span><span class="sxs-lookup"><span data-stu-id="5b328-149">This causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="5b328-150">También hay un tiempo de espera asociado con un mensaje bloqueado de la cola, y si la aplicación hello falla tooprocess Hola mensaje antes de que el tiempo de espera de bloqueo expire (por ejemplo, si se bloquea aplicación hello), a continuación, Bus de servicio desbloquea el mensaje de bienvenida automáticamente y hace disponible toobe recibido de nuevo.</span><span class="sxs-lookup"><span data-stu-id="5b328-150">There is also a timeout associated with a message locked within the queue, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="5b328-151">Hola eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida pero antes de hello **deleteMessage** se emite la solicitud, a continuación, mensaje de bienvenida es la aplicación de toohello entregados de nuevo cuando se reinicia.</span><span class="sxs-lookup"><span data-stu-id="5b328-151">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="5b328-152">Esto se suele denominar *al menos una vez procesamiento*; es decir, cada mensaje se procesa al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="5b328-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="5b328-153">Si el escenario de hello no puede tolerar el procesamiento duplicado, los desarrolladores de aplicaciones deben agregar lógica adicional tootheir aplicación toohandle duplicados entrega del mensaje.</span><span class="sxs-lookup"><span data-stu-id="5b328-153">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="5b328-154">A menudo esto se logra utilizando hello **getMessageId** método del mensaje de Hola, que permanece constante en los intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="5b328-154">This is often achieved using hello **getMessageId** method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b328-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5b328-155">Next Steps</span></span>
<span data-ttu-id="5b328-156">Ahora que conoce los fundamentos de Hola de colas de Service Bus, vea [colas, temas y suscripciones] [ Queues, topics, and subscriptions] para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="5b328-156">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="5b328-157">Para obtener más información, vea hello [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="5b328-157">For more information, see hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
