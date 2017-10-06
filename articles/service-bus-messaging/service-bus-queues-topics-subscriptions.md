---
title: "aaaOverview de colas, temas y suscripciones de mensajería de Service Bus de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>Colas, temas y suscripciones de Service Bus

Microsoft Azure Service Bus admite un conjunto de tecnologías de middleware basadas en la nube y orientadas a mensajes, incluidas una cola de mensajes de confianza y una mensajería de publicación/suscripción duradera. Estas capacidades de mensajes "asíncronas" pueden considerarse como desacoplada características que admiten la publicación y suscripción de mensajería, temporal desacoplamiento y escenarios que se utiliza el tejido de mensajería de Bus de servicio de Hola de equilibrio de carga. La comunicación desacoplada ofrece muchas ventajas; por ejemplo, los clientes y servidores pueden conectarse según sea necesario y realizar sus operaciones de forma asincrónica.

entidades de mensajería de Hola que forman el núcleo de Hola de hello capacidades de Bus de servicio de mensajería son colas, temas y suscripciones y reglas/acciones.

## <a name="queues"></a>Colas

Las colas ofrecen *primero en ENTRAR, primero en salir* tooone de entrega de mensajes (FIFO) o varios consumidores en competencia. Es decir, los mensajes son normalmente esperado toobe recibe y procesa receptores de hello en orden de hello en el que se agregaron toohello cola, y cada mensaje lo recibe y procesa por un solo consumidor de mensaje. Una ventaja clave del uso de colas es tooachieve "desacoplamiento temporal" de componentes de la aplicación. Hola en otras palabras, los productores (remitentes) y los consumidores (receptores) no es necesario enviar toobe y reciben mensajes en hello mismo tiempo, ya que los mensajes se almacenan de manera duradera en cola de Hola. Además, productor hello no tienen toowait una respuesta de consumidor de hello en orden toocontinue tooprocess y enviar mensajes.

Una ventaja relacionada es "equilibrio de la carga," que permite a los productores y consumidores toosend y recibe mensajes a distintas tasas. En muchas aplicaciones, la carga del sistema Hola varía con el tiempo; Sin embargo, el tiempo de procesamiento de hello necesario para cada unidad de trabajo es normalmente constante. Intermediar de mensaje de productores y consumidores con una cola significa ese Hola consumiendo aplicación únicamente tiene aprovisionado toobe toobe toohandle capaz de carga Media en lugar de carga máxima. profundidad de Hola de cola de hello aumenta y disminuye medida que varía la carga entrante Hola. Esto directamente ahorra dinero con cantidad de toohello independientemente de la carga de la aplicación de infraestructura necesario tooservice Hola. Como Hola aumenta la carga, más procesos de trabajo pueden ser agregado tooread de cola de Hola. Cada mensaje se procesa solamente mediante uno de los procesos de trabajo de Hola. Además, este equilibrio de carga basados en extracción permite un uso óptimo de los equipos de trabajo de hello incluso si los equipos de trabajo de hello diferencian la potencia de tooprocessing tener en cuenta, ya que extraerán mensajes a su propia velocidad máxima. Este patrón a menudo se denomina patrón de Hola "consumidor en competencia".

Uso de colas toointermediate entre los consumidores y productores de mensajes proporciona un acoplamiento débil inherente entre los componentes de Hola. Como los productores y consumidores no son compatibles con unos de otros, un consumidor puede actualizarse sin tener ningún efecto en productor Hola.

La creación de una cola es un proceso de varios pasos. Realizar operaciones de administración de entidades (colas y temas) a través de Hola de mensajería de Service Bus [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) (clase), que se construye suministrando la dirección base de Hola de hello Bus de servicio credenciales de usuario de hello y espacio de nombres. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) proporciona métodos toocreate, enumerar y eliminar entidades de mensajería. Después de crear un [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) objeto objeto de nombre de la SAS de Hola y clave y una administración de espacio de nombres de servicio, puede usar hello [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) cola de método toocreate Hola. Por ejemplo:

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

A continuación, puede crear un objeto de cola y una fábrica de mensajería con hello URI de Bus de servicio como un argumento. Por ejemplo:

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

A continuación, puede enviar la cola de mensajes toohello. Por ejemplo, si tiene una lista de mensajes asíncronos llamada `MessageList`, código de hello aparece a continuación toohello similar:

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

A continuación, recibe los mensajes de cola de hello como sigue:

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

Hola [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) Hola de modo de recepción operación es sola fase; es decir, al Bus de servicio recibe una solicitud de hello, marca Hola mensaje como consumido y lo devuelve toohello aplicación. **ReceiveAndDelete** modo es el modelo más sencillo de Hola y funciona mejor para escenarios en que Hola aplicación puede tolerar no procesar un mensaje en caso de hello de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Dado que Service Bus marca mensaje Hola como consumido, cuando la aplicación hello se reinicia y comienza a consumir mensajes de nuevo, habrá perdido mensaje Hola que estaba consumido bloqueo toohello anterior.

En [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) Hola de modo de recepción operación se convierte en dos fases, por lo que hace que las aplicaciones de toosupport posible que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud de hello, busca Hola siguiente mensaje toobe consumido, la bloquea tooprevent otros consumidores de recibir y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a [completar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) en mensajes de bienvenida recibido. Al Bus de servicio ve hello **completar** llamada, marca Hola mensaje como consumido.

Si no puede aplicación hello tooprocess Hola mensaje por alguna razón, puede llamar a hello [abandonar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) método en mensajes de bienvenida recibido (en lugar de [completar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Esto permite que el mensaje de bienvenida de Bus de servicio toounlock y hacerla disponible toobe recibido de nuevo, ya sea mediante Hola mismo consumidor o por otro consumidor en competencia. En segundo lugar, no existe un tiempo de espera asociado con la tecla BLOQ hello y aplicación hello provoca un error tooprocess Hola mensaje antes de tiempo de espera de bloqueo de hello expira (por ejemplo, si se bloquea aplicación hello), a continuación, desbloquea el mensaje de bienvenida de Bus de servicio y la convierte en disponible toobe recibido nuevo (básicamente realizar un [abandonar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operación de forma predeterminada).

Tenga en cuenta que en hello eventos que Hola aplicación se bloquea después de procesar el mensaje de bienvenida, pero antes de hello **completar** se emite la solicitud, mensaje de bienvenida es la aplicación de toohello entregados de nuevo cuando se reinicia. Esto se conoce como *Al menos un procesamiento*; es decir, cada mensaje se procesa como mínimo una vez. Sin embargo, en cierto Hola situaciones mismo mensaje puede volverse a entregar. Si el escenario de hello no puede tolerar el procesamiento duplicado, hará falta lógica adicional en duplicados de toodetect de aplicación Hola que se pueden lograr en función de hello **MessageId** propiedad de mensaje hello, que sigue siendo constante entre intentos de entrega. Esto se conoce como procesamiento *Exactamente una vez*.

## <a name="topics-and-subscriptions"></a>Temas y suscripciones
En contraste tooqueues, en el que se procesa cada mensaje mediante un único consumidor *temas* y *suscripciones* proporcionan una forma de comunicación, uno a varios en una *depublicación/suscripción* patrón. Es útil para ajustar la escala toovery gran número de destinatarios, cada mensaje publicado se pone tooeach disponibles las suscripciones registradas con el tema de Hola. Se envían mensajes tooa tema y entregado tooone o más suscripciones asociadas, según las reglas de filtro que se pueden establecer por suscripción. las suscripciones de Hello pueden utilizar mensajes de saludo de toorestrict filtros adicionales que desean tooreceive. Los mensajes se envían tooa tema Hola misma forma se envían tooa cola, pero no se reciben mensajes de tema de hello directamente. En su lugar, se reciben de las suscripciones. Una suscripción de tema es similar a una cola virtual que recibe copias de mensajes de saludo que se envían toohello tema. Se reciben mensajes de una suscripción de forma idéntica forma toohello que se reciben de una cola.

Si se compara, hello funcionalidad de envío de mensajes de una cola asigna directamente tooa tema y su funcionalidad de recepción de mensajes asigna tooa suscripción. Entre otras cosas, esto significa que las suscripciones admiten Hola mismos patrones descritos anteriormente en esta sección con tooqueues de tener en cuenta: consumidor en competencia, desacoplamiento temporal, nivelado de carga y equilibrio de carga.

Crear un tema es similar toocreating una cola, tal y como se muestra en el ejemplo de Hola en la sección anterior de Hola. Crear el URI del servicio de hello y, a continuación, usar hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) cliente de espacio de nombres de clase toocreate Hola. A continuación, puede crear un tema mediante hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) método. Por ejemplo:

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

Después, agregue las suscripciones que desee:

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

Luego puede crear un cliente del tema. Por ejemplo:

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

El remitente del mensaje de Hola puede enviar y recibir mensajes tooand de tema de hello, como se muestra en la sección anterior de Hola. Por ejemplo:

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

Tooqueues similar, los mensajes se reciben de una suscripción con un [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) objeto en lugar de un [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) objeto. Crear a cliente de suscripción de hello, pasando Hola nombre de tema de hello, nombre de Hola de suscripción de hello, y (opcionalmente) Hola modo de recepción como parámetros. Por ejemplo, con hello **inventario** suscripción:

```csharp
// Create hello subscription client
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

### <a name="rules-and-actions"></a>Reglas y acciones
En muchos escenarios, los mensajes que tienen características específicas deben procesarse de maneras diferentes. tooenable esto, puede configurar mensajes de toofind de las suscripciones que tengan las propiedades adecuadas y, a continuación, realizan ciertas propiedades de toothose modificaciones. Mientras que las suscripciones de Bus de servicio ven todos los mensajes enviados toohello tema, puede copiar solo un subconjunto de esas cola de mensajes toohello suscripción virtual. Esto se consigue mediante los filtros de suscripción. Dichas modificaciones se denominan *acciones de filtrado*. Cuando se crea una suscripción, puede proporcionar una expresión de filtro que opera en las propiedades de Hola de mensaje de bienvenida, ambos Hola propiedades del sistema (por ejemplo, **etiqueta**) y las propiedades de la aplicación personalizada (por ejemplo, **StoreName**.) Hola expresión de filtro SQL es opcional en este caso; sin una expresión de filtro SQL, se realizará ninguna acción de filtro definida en una suscripción en todos los mensajes de Hola para esa suscripción.

Mediante el ejemplo anterior de hello, mensajes toofilter procedentes únicamente de **Store1**, debe crear suscripción de panel de hello como sigue:

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

Con este filtro de suscripción en su lugar, sólo los mensajes que tienen hello `StoreName` propiedad establecida demasiado`Store1` son copiados toohello cola virtual para hello `Dashboard` suscripción.

Para obtener más información acerca de los valores de filtro posibles, vea la documentación Hola Hola [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) y [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) clases. Consulte también hello [mensajería asíncrona: filtro avanzado](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) y [tema filtros](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) ejemplos.

## <a name="next-steps"></a>Pasos siguientes
Vea a continuación Hola avanzado de temas para obtener más información y ejemplos del uso de la mensajería de Bus de servicio.

* [Introducción a la mensajería del Bus de servicio](service-bus-messaging-overview.md)
* [Tutorial de .NET de mensajería asincrónica de Service Bus](service-bus-brokered-tutorial-dotnet.md)
* [Tutorial de REST de mensajería asincrónica de Service Bus](service-bus-brokered-tutorial-rest.md)
* [Ejemplo de filtros de tema](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [Mensajería asincrónica: ejemplo de filtros avanzados](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)

