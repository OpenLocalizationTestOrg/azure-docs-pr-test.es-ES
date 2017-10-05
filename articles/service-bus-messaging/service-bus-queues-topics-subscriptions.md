---
title: "Información general sobre colas de mensajes, temas y suscripciones de Azure Service Bus | Microsoft Docs"
description: "Información general de las entidades de mensajería del Bus de servicio."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 00f9f38fbae028486270053dedb4df580a3f1a44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a><span data-ttu-id="b0276-103">Colas, temas y suscripciones de Service Bus</span><span class="sxs-lookup"><span data-stu-id="b0276-103">Service Bus queues, topics, and subscriptions</span></span>

<span data-ttu-id="b0276-104">Microsoft Azure Service Bus admite un conjunto de tecnologías de middleware basadas en la nube y orientadas a mensajes, incluidas una cola de mensajes de confianza y una mensajería de publicación/suscripción duradera.</span><span class="sxs-lookup"><span data-stu-id="b0276-104">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> <span data-ttu-id="b0276-105">Estas funcionalidades de mensajería "asíncrona" pueden considerarse como características de mensajería desacopladas que admiten la publicación-suscripción, el desacoplamiento temporal y los escenarios de equilibrio de carga mediante el tejido de la mensajería de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b0276-105">These "brokered" messaging capabilities can be thought of as decoupled messaging features that support publish-subscribe, temporal decoupling, and load balancing scenarios using the Service Bus messaging fabric.</span></span> <span data-ttu-id="b0276-106">La comunicación desacoplada ofrece muchas ventajas; por ejemplo, los clientes y servidores pueden conectarse según sea necesario y realizar sus operaciones de forma asincrónica.</span><span class="sxs-lookup"><span data-stu-id="b0276-106">Decoupled communication has many advantages; for example, clients and servers can connect as needed and perform their operations in an asynchronous fashion.</span></span>

<span data-ttu-id="b0276-107">Las entidades de mensajería que forman el núcleo de las funcionalidades de mensajería de Service Bus son las colas, los temas y suscripciones y las reglas o acciones.</span><span class="sxs-lookup"><span data-stu-id="b0276-107">The messaging entities that form the core of the messaging capabilities in Service Bus are queues, topics and subscriptions, and rules/actions.</span></span>

## <a name="queues"></a><span data-ttu-id="b0276-108">Colas</span><span class="sxs-lookup"><span data-stu-id="b0276-108">Queues</span></span>

<span data-ttu-id="b0276-109">Las colas ofrecen una entrega de mensajes según el modelo *primero en entrar, primero en salir (FIFO [PEPS])* a uno o más destinatarios de la competencia.</span><span class="sxs-lookup"><span data-stu-id="b0276-109">Queues offer *First In, First Out* (FIFO) message delivery to one or more competing consumers.</span></span> <span data-ttu-id="b0276-110">Es decir, normalmente los receptores reciben y procesan los mensajes en el orden en el que se agregaron a la cola y solo un destinatario del mensaje recibe y procesa cada uno de los mensajes.</span><span class="sxs-lookup"><span data-stu-id="b0276-110">That is, messages are typically expected to be received and processed by the receivers in the order in which they were added to the queue, and each message is received and processed by only one message consumer.</span></span> <span data-ttu-id="b0276-111">La principal ventaja del uso de colas es conseguir un "desacoplamiento temporal" de los componentes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0276-111">A key benefit of using queues is to achieve "temporal decoupling" of application components.</span></span> <span data-ttu-id="b0276-112">En otras palabras, los productores (remitentes) y los consumidores (receptores) no tienen que enviar y recibir mensajes al mismo tiempo, ya que los mensajes se almacenan de forma duradera en la cola.</span><span class="sxs-lookup"><span data-stu-id="b0276-112">In other words, the producers (senders) and consumers (receivers) do not have to be sending and receiving messages at the same time, because messages are stored durably in the queue.</span></span> <span data-ttu-id="b0276-113">El productor no tiene que esperar una respuesta del destinatario para continuar el proceso y el envío de más mensajes.</span><span class="sxs-lookup"><span data-stu-id="b0276-113">Furthermore, the producer does not have to wait for a reply from the consumer in order to continue to process and send messages.</span></span>

<span data-ttu-id="b0276-114">Una ventaja relacionada es la "nivelación de la carga", lo que permite a los productores y consumidores enviar y recibir mensajes con distintas velocidades.</span><span class="sxs-lookup"><span data-stu-id="b0276-114">A related benefit is "load leveling," which enables producers and consumers to send and receive messages at different rates.</span></span> <span data-ttu-id="b0276-115">En muchas aplicaciones, la carga del sistema varía con el tiempo, mientras que el tiempo de procesamiento requerido por cada unidad de trabajo suele ser constante.</span><span class="sxs-lookup"><span data-stu-id="b0276-115">In many applications, the system load varies over time; however, the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="b0276-116">La intermediación de productores y consumidores de mensajes con una cola implica que la aplicación consumidora solo necesita ser aprovisionada para administrar una carga promedio en lugar de una carga pico.</span><span class="sxs-lookup"><span data-stu-id="b0276-116">Intermediating message producers and consumers with a queue means that the consuming application only has to be provisioned to be able to handle average load instead of peak load.</span></span> <span data-ttu-id="b0276-117">La profundidad de la cola aumenta y se contrae a medida que varíe la carga entrante,</span><span class="sxs-lookup"><span data-stu-id="b0276-117">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="b0276-118">lo que permite ahorrar dinero directamente en función de la cantidad de infraestructura requerida para dar servicio a la carga de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0276-118">This directly saves money with regard to the amount of infrastructure required to service the application load.</span></span> <span data-ttu-id="b0276-119">A medida que aumenta la carga, se pueden agregar más procesos de trabajo para que puedan leerse desde la cola.</span><span class="sxs-lookup"><span data-stu-id="b0276-119">As the load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="b0276-120">Cada mensaje se procesa únicamente por uno de los procesos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b0276-120">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="b0276-121">Es más, este equilibrio de carga basado en la extracción permite el uso óptimo de los equipos de trabajo aunque estos equipos difieran en términos de capacidad de procesamiento ya que extraerán mensajes a su frecuencia máxima propia.</span><span class="sxs-lookup"><span data-stu-id="b0276-121">Furthermore, this pull-based load balancing allows for optimum use of the worker computers even if the worker computers differ with regard to processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="b0276-122">Este patrón con frecuencia se denomina "patrón de consumo de competidor".</span><span class="sxs-lookup"><span data-stu-id="b0276-122">This pattern is often termed the "competing consumer" pattern.</span></span>

<span data-ttu-id="b0276-123">El uso de colas para intermediar entre los consumidores y productores de mensajes proporciona un acoplamiento no estricto inherente entre los componentes.</span><span class="sxs-lookup"><span data-stu-id="b0276-123">Using queues to intermediate between message producers and consumers provides an inherent loose coupling between the components.</span></span> <span data-ttu-id="b0276-124">Dado que los productores y consumidores no están relacionados entre sí, un consumidor puede actualizarse sin tener ningún efecto en el productor.</span><span class="sxs-lookup"><span data-stu-id="b0276-124">Because producers and consumers are not aware of each other, a consumer can be upgraded without having any effect on the producer.</span></span>

<span data-ttu-id="b0276-125">La creación de una cola es un proceso de varios pasos.</span><span class="sxs-lookup"><span data-stu-id="b0276-125">Creating a queue is a multi-step process.</span></span> <span data-ttu-id="b0276-126">Las operaciones de administración de las entidades de mensajería de Service Bus (colas y temas) se realizan a través la clase [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager), que se construye mediante el suministro de la dirección base del espacio de nombres de Service Bus y las credenciales de usuario.</span><span class="sxs-lookup"><span data-stu-id="b0276-126">You perform management operations for Service Bus messaging entities (both queues and topics) via the [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) class, which is constructed by supplying the base address of the Service Bus namespace and the user credentials.</span></span> <span data-ttu-id="b0276-127">La clase [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) proporciona métodos para crear, enumerar y eliminar entidades de mensajería.</span><span class="sxs-lookup"><span data-stu-id="b0276-127">[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) provides methods to create, enumerate and delete messaging entities.</span></span> <span data-ttu-id="b0276-128">Después de crear un objeto [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) a partir del nombre y la clave SAS y un objeto de administración del espacio de nombres de servicios, puede usar el método [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) para crear la cola.</span><span class="sxs-lookup"><span data-stu-id="b0276-128">After creating a [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) object from the SAS name and key, and a service namespace management object, you can use the [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) method to create the queue.</span></span> <span data-ttu-id="b0276-129">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b0276-129">For example:</span></span>

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

<span data-ttu-id="b0276-130">A continuación, puede crear un objeto de cola y una factoría de mensajes con el URI del Bus de servicio como argumento.</span><span class="sxs-lookup"><span data-stu-id="b0276-130">You can then create a queue object and a messaging factory with the Service Bus URI as an argument.</span></span> <span data-ttu-id="b0276-131">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b0276-131">For example:</span></span>

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

<span data-ttu-id="b0276-132">A continuación, puede enviar mensajes a la cola.</span><span class="sxs-lookup"><span data-stu-id="b0276-132">You can then send messages to the queue.</span></span> <span data-ttu-id="b0276-133">Por ejemplo, si tiene una lista de mensajes indirectos denominada `MessageList`; el código es similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="b0276-133">For example, if you have a list of brokered messages called `MessageList`, the code appears similar to the following:</span></span>

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

<span data-ttu-id="b0276-134">A continuación, recibe mensajes de la cola, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="b0276-134">You then receive messages from the queue as follows:</span></span>

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

<span data-ttu-id="b0276-135">Al usar el modo [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode), la operación de recepción consta de una sola fase; es decir, cuando Service Bus recibe una solicitud, marca el mensaje como consumido y lo devuelve a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0276-135">In the [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, the receive operation is single-shot; that is, when Service Bus receives the request, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="b0276-136">El modo **ReceiveAndDelete** es el modelo más sencillo y funciona mejor para los escenarios en los que la aplicación puede tolerar no procesar un mensaje en caso de error.</span><span class="sxs-lookup"><span data-stu-id="b0276-136">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which the application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="b0276-137">Para entenderlo mejor, pongamos una situación en la que un consumidor emite la solicitud de recepción que se bloquea antes de procesarla.</span><span class="sxs-lookup"><span data-stu-id="b0276-137">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="b0276-138">Como el Bus de servicio marca el mensaje como consumido, cuando la aplicación se reinicie y empiece a consumir mensajes de nuevo, habrá perdido el mensaje que se consumió antes del bloqueo.</span><span class="sxs-lookup"><span data-stu-id="b0276-138">Because Service Bus marks the message as being consumed, when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="b0276-139">En el modo [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode), la operación de recepción se convierte en una operación de dos fases que hace posible admitir aplicaciones que no toleran la pérdida de mensajes.</span><span class="sxs-lookup"><span data-stu-id="b0276-139">In [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, the receive operation becomes two-stage, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="b0276-140">Cuando el Bus de servicio recibe una solicitud, busca el siguiente mensaje que se va a consumir, lo bloquea para impedir que otros consumidores lo reciban y, a continuación, lo devuelve a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0276-140">When Service Bus receives the request, it finds the next message to be consumed, locks it to prevent other consumers from receiving it, and then returns it to the application.</span></span> <span data-ttu-id="b0276-141">Una vez que la aplicación termina de procesar el mensaje (o lo almacena de forma fiable para su futuro procesamiento), completa la segunda fase del proceso de recepción creando la llamada [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) en el mensaje recibido.</span><span class="sxs-lookup"><span data-stu-id="b0276-141">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) on the received message.</span></span> <span data-ttu-id="b0276-142">Cuando Service Bus ve la llamada **Complete**, marca el mensaje como consumido.</span><span class="sxs-lookup"><span data-stu-id="b0276-142">When Service Bus sees the **Complete** call, it marks the message as being consumed.</span></span>

<span data-ttu-id="b0276-143">Si por cualquier motivo la aplicación no puede procesar el mensaje, realice la llamada al método [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) del mensaje recibido (en lugar de [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)).</span><span class="sxs-lookup"><span data-stu-id="b0276-143">If the application is unable to process the message for some reason, it can call the [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) method on the received message (instead of [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)).</span></span> <span data-ttu-id="b0276-144">Esto permite que el Bus de servicio desbloquee el mensaje y esté disponible para que el mismo consumidor u otro vuelvan a recibirlo.</span><span class="sxs-lookup"><span data-stu-id="b0276-144">This enables Service Bus to unlock the message and make it available to be received again, either by the same consumer or by another competing consumer.</span></span> <span data-ttu-id="b0276-145">En segundo lugar, hay un tiempo de espera asociado con el bloqueo y, si la aplicación no puede procesar el mensaje antes de que el tiempo de espera del bloqueo expire (por ejemplo, si la aplicación se bloquea), Service Bus desbloquea el mensaje y hace que esté disponible para recibirse de nuevo (básicamente realizando una operación [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="b0276-145">Secondly, there is a timeout associated with the lock and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message and makes it available to be received again (essentially performing an [Abandon](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operation by default).</span></span>

<span data-ttu-id="b0276-146">Tenga en cuenta que, en caso de que la aplicación se bloquee después de procesar el mensaje, pero antes de que se emita la solicitud **Complete**, se volverá a enviar el mensaje a la aplicación cuando esta se reinicie.</span><span class="sxs-lookup"><span data-stu-id="b0276-146">Note that in the event that the application crashes after processing the message, but before the **Complete** request is issued, the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="b0276-147">Esto se conoce como *Al menos un procesamiento*; es decir, cada mensaje se procesa como mínimo una vez.</span><span class="sxs-lookup"><span data-stu-id="b0276-147">This is often called *At Least Once* processing; that is, each message is processed at least once.</span></span> <span data-ttu-id="b0276-148">Sin embargo, en determinadas situaciones, es posible que se vuelva a entregar el mismo mensaje.</span><span class="sxs-lookup"><span data-stu-id="b0276-148">However, in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="b0276-149">Si el escenario no puede tolerar el procesamiento duplicado, se requiere una lógica adicional en la aplicación para detectar duplicados que se puedan conseguir de acuerdo con la propiedad **MessageId** del mensaje, que permanece constante en los intentos de entrega.</span><span class="sxs-lookup"><span data-stu-id="b0276-149">If the scenario cannot tolerate duplicate processing, then additional logic is required in the application to detect duplicates which can be achieved based upon the **MessageId** property of the message, which remains constant across delivery attempts.</span></span> <span data-ttu-id="b0276-150">Esto se conoce como procesamiento *Exactamente una vez*.</span><span class="sxs-lookup"><span data-stu-id="b0276-150">This is known as *Exactly Once* processing.</span></span>

## <a name="topics-and-subscriptions"></a><span data-ttu-id="b0276-151">Temas y suscripciones</span><span class="sxs-lookup"><span data-stu-id="b0276-151">Topics and subscriptions</span></span>
<span data-ttu-id="b0276-152">A diferencia de las colas, en las que un solo consumidor procesa cada mensaje, los *temas* y las *suscripciones* proporcionan una forma de comunicación de uno a varios mediante un patrón de *publicación o suscripción*.</span><span class="sxs-lookup"><span data-stu-id="b0276-152">In contrast to queues, in which each message is processed by a single consumer, *topics* and *subscriptions* provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="b0276-153">Cada mensaje publicado se pone a disposición de todas las suscripciones registradas en el tema, lo que es útil para escalar a un gran número de destinatarios.</span><span class="sxs-lookup"><span data-stu-id="b0276-153">Useful for scaling to very large numbers of recipients, each published message is made available to each subscription registered with the topic.</span></span> <span data-ttu-id="b0276-154">Los mensajes se envían a un tema y se entregan a una o varias suscripciones asociadas, según las reglas de filtro que se pueden establecer por suscripción.</span><span class="sxs-lookup"><span data-stu-id="b0276-154">Messages are sent to a topic and delivered to one or more associated subscriptions, depending on filter rules that can be set on a per-subscription basis.</span></span> <span data-ttu-id="b0276-155">Las suscripciones pueden usar filtros adicionales para restringir los mensajes que desean recibir.</span><span class="sxs-lookup"><span data-stu-id="b0276-155">The subscriptions can use additional filters to restrict the messages that they want to receive.</span></span> <span data-ttu-id="b0276-156">Los mensajes se envían a un tema de la misma manera que se envían a una cola, pero no se reciben del tema directamente.</span><span class="sxs-lookup"><span data-stu-id="b0276-156">Messages are sent to a topic in the same way they are sent to a queue, but messages are not received from the topic directly.</span></span> <span data-ttu-id="b0276-157">En su lugar, se reciben de las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="b0276-157">Instead, they are received from subscriptions.</span></span> <span data-ttu-id="b0276-158">Una suscripción al tema se parece a una cola virtual en que recibe copias de los mensajes que se envían al tema.</span><span class="sxs-lookup"><span data-stu-id="b0276-158">A topic subscription resembles a virtual queue that receives copies of the messages that are sent to the topic.</span></span> <span data-ttu-id="b0276-159">Los mensajes se reciben de una suscripción exactamente de la misma forma en que se reciben de una cola.</span><span class="sxs-lookup"><span data-stu-id="b0276-159">Messages are received from a subscription identically to the way they are received from a queue.</span></span>

<span data-ttu-id="b0276-160">Por medio de la comparación, la funcionalidad de envío de mensajes de una cola los asigna directamente a un tema y su funcionalidad de recepción de mensajes a una suscripción.</span><span class="sxs-lookup"><span data-stu-id="b0276-160">By way of comparison, the message-sending functionality of a queue maps directly to a topic and its message-receiving functionality maps to a subscription.</span></span> <span data-ttu-id="b0276-161">Entre otras cosas, esto significa que las suscripciones admiten los mismos patrones que se han descrito en esta misma sección con respecto a las colas: consumidor en competencia, desacoplamiento temporal, nivelación de carga y equilibrio de la carga.</span><span class="sxs-lookup"><span data-stu-id="b0276-161">Among other things, this means that subscriptions support the same patterns described earlier in this section with regard to queues: competing consumer, temporal decoupling, load leveling, and load balancing.</span></span>

<span data-ttu-id="b0276-162">La creación de un tema es similar a la creación de una cola, como se muestra en el ejemplo de la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="b0276-162">Creating a topic is similar to creating a queue, as shown in the example in the previous section.</span></span> <span data-ttu-id="b0276-163">Cree el URI de servicio y, a continuación, use la clase [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) para crear el cliente de espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="b0276-163">Create the service URI, and then use the [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) class to create the namespace client.</span></span> <span data-ttu-id="b0276-164">A continuación, puede crear un tema mediante el método [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_).</span><span class="sxs-lookup"><span data-stu-id="b0276-164">You can then create a topic using the [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) method.</span></span> <span data-ttu-id="b0276-165">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b0276-165">For example:</span></span>

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

<span data-ttu-id="b0276-166">Después, agregue las suscripciones que desee:</span><span class="sxs-lookup"><span data-stu-id="b0276-166">Next, add subscriptions as desired:</span></span>

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

<span data-ttu-id="b0276-167">Luego puede crear un cliente del tema.</span><span class="sxs-lookup"><span data-stu-id="b0276-167">You can then create a topic client.</span></span> <span data-ttu-id="b0276-168">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b0276-168">For example:</span></span>

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

<span data-ttu-id="b0276-169">Con el remitente del mensaje puede enviar mensajes al tema o recibirlos de este, como se muestra en la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="b0276-169">Using the message sender, you can send and receive messages to and from the topic, as shown in the previous section.</span></span> <span data-ttu-id="b0276-170">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b0276-170">For example:</span></span>

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

<span data-ttu-id="b0276-171">Al igual que las colas, los mensajes se reciben de una suscripción mediante un objeto [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient), en lugar de un objeto [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient).</span><span class="sxs-lookup"><span data-stu-id="b0276-171">Similar to queues, messages are received from a subscription using a [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) object instead of a [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) object.</span></span> <span data-ttu-id="b0276-172">Cree el cliente de la suscripción y pase el nombre del tema, el nombre de la suscripción y (opcionalmente) el modo de recepción como parámetros.</span><span class="sxs-lookup"><span data-stu-id="b0276-172">Create the subscription client, passing the name of the topic, the name of the subscription, and (optionally) the receive mode as parameters.</span></span> <span data-ttu-id="b0276-173">Por ejemplo, en el caso de la suscripción **Inventory**:</span><span class="sxs-lookup"><span data-stu-id="b0276-173">For example, with the **Inventory** subscription:</span></span>

```csharp
// Create the subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a><span data-ttu-id="b0276-174">Reglas y acciones</span><span class="sxs-lookup"><span data-stu-id="b0276-174">Rules and actions</span></span>
<span data-ttu-id="b0276-175">En muchos escenarios, los mensajes que tienen características específicas deben procesarse de maneras diferentes.</span><span class="sxs-lookup"><span data-stu-id="b0276-175">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="b0276-176">Para permitirlo, puede configurar suscripciones para buscar los mensajes que tengan las propiedades deseadas y, después, realizar determinadas modificaciones en dichas propiedades.</span><span class="sxs-lookup"><span data-stu-id="b0276-176">To enable this, you can configure subscriptions to find messages that have desired properties and then perform certain modifications to those properties.</span></span> <span data-ttu-id="b0276-177">Mientras que las suscripciones del Service Bus ven todos los mensajes enviados al tema, solo se puede copiar un subconjunto de dichos mensajes en la cola de suscripción virtual.</span><span class="sxs-lookup"><span data-stu-id="b0276-177">While Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="b0276-178">Esto se consigue mediante los filtros de suscripción.</span><span class="sxs-lookup"><span data-stu-id="b0276-178">This is accomplished using subscription filters.</span></span> <span data-ttu-id="b0276-179">Dichas modificaciones se denominan *acciones de filtrado*.</span><span class="sxs-lookup"><span data-stu-id="b0276-179">Such modifications are called *filter actions*.</span></span> <span data-ttu-id="b0276-180">Al crear una suscripción, se puede incluir una expresión de filtro que opere en las propiedades del mensaje, tanto en las propiedades del sistema (por ejemplo, **Label**) como en las propiedades de la aplicación personalizada (por ejemplo, **StoreName**). La expresión de filtro SQL es opcional en este caso; sin una expresión de filtro SQL, todas las acciones de filtro definidas en una suscripción se realizarán en todos los mensajes de dicha suscripción.</span><span class="sxs-lookup"><span data-stu-id="b0276-180">When a subscription is created, you can supply a filter expression that operates on the properties of the message, both the system properties (for example, **Label**) and custom application properties (for example, **StoreName**.) The SQL filter expression is optional in this case; without a SQL filter expression, any filter action defined on a subscription will be performed on all the messages for that subscription.</span></span>

<span data-ttu-id="b0276-181">En el ejemplo anterior, para filtrar los mensajes que procedan solo de **Store1**, sería preciso crear la suscripción Dashboard como sigue:</span><span class="sxs-lookup"><span data-stu-id="b0276-181">Using the previous example, to filter messages coming only from **Store1**, you would create the Dashboard subscription as follows:</span></span>

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

<span data-ttu-id="b0276-182">Con este filtro de suscripción activado, solo se copiarán en la cola virtual de la suscripción `Dashboard` los mensajes que tengan la propiedad `StoreName` establecida en `Store1`.</span><span class="sxs-lookup"><span data-stu-id="b0276-182">With this subscription filter in place, only messages that have the `StoreName` property set to `Store1` are copied to the virtual queue for the `Dashboard` subscription.</span></span>

<span data-ttu-id="b0276-183">Para más información sobre los valores de filtro posibles, vea la documentación de las clases [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) y [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction).</span><span class="sxs-lookup"><span data-stu-id="b0276-183">For more information about possible filter values, see the documentation for the [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) and [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) classes.</span></span> <span data-ttu-id="b0276-184">Vea también los ejemplos de [Brokered Messaging: Advanced Filters](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) (Mensajería asincrónica: filtros avanzados) y [filtros de temas](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters).</span><span class="sxs-lookup"><span data-stu-id="b0276-184">Also, see the [Brokered Messaging: Advanced Filters](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) and [Topic Filters](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) samples.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0276-185">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b0276-185">Next steps</span></span>
<span data-ttu-id="b0276-186">Para más información y ejemplos del uso de la mensajería de Service Bus, consulte los siguientes temas avanzados.</span><span class="sxs-lookup"><span data-stu-id="b0276-186">See the following advanced topics for more information and examples of using Service Bus messaging.</span></span>

* [<span data-ttu-id="b0276-187">Introducción a la mensajería del Bus de servicio</span><span class="sxs-lookup"><span data-stu-id="b0276-187">Service Bus messaging overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="b0276-188">Tutorial de .NET de mensajería asincrónica de Service Bus</span><span class="sxs-lookup"><span data-stu-id="b0276-188">Service Bus brokered messaging .NET tutorial</span></span>](service-bus-brokered-tutorial-dotnet.md)
* [<span data-ttu-id="b0276-189">Tutorial de REST de mensajería asincrónica de Service Bus</span><span class="sxs-lookup"><span data-stu-id="b0276-189">Service Bus brokered messaging REST tutorial</span></span>](service-bus-brokered-tutorial-rest.md)
* [<span data-ttu-id="b0276-190">Ejemplo de filtros de tema</span><span class="sxs-lookup"><span data-stu-id="b0276-190">Topic Filters sample </span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [<span data-ttu-id="b0276-191">Mensajería asincrónica: ejemplo de filtros avanzados</span><span class="sxs-lookup"><span data-stu-id="b0276-191">Brokered Messaging: Advanced Filters sample</span></span>](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)
