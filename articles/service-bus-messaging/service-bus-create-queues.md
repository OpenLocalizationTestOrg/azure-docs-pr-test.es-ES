---
title: aplicaciones de aaaWrite que usan colas de Service Bus de Azure | Documentos de Microsoft
description: "¿Cómo toowrite una aplicación simple basada en cola que usa Service Bus de Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 93b75902a06becd6e33e05298e09f5669d0e2aef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>Creación de aplicaciones que usan colas del Bus de servicio
En este tema se describen las colas de Bus de servicio y se muestra cómo toowrite una aplicación simple basada en cola que usa Service Bus.

Considere un escenario de Hola a todos de la venta directa en que los datos de ventas de individuales Point (POS) deben ser terminales dirigirse sistema de administración de inventario de tooan que usa Hola datos toodetermine cuándo toobe reponerse existencias. Esta solución usa mensajería de Bus de servicio para la comunicación de hello entre terminales de Hola y el sistema de administración de inventario de hello, como se muestra en hello figura siguiente:

![Imagen de colas de Service Bus 1](./media/service-bus-create-queues/IC657161.gif)

Cada terminal de punto de venta informa de sus datos de venta enviando mensajes toohello **DataCollectionQueue**. Estos mensajes permanecen en esta cola hasta que se recuperan mediante el sistema de administración de inventario de Hola. Este patrón se denomina a menudo *mensajería asincrónica*, porque terminal Hola POS no tiene toowait una respuesta de procesamiento de toocontinue de sistema de administración de inventario de Hola.

## <a name="why-queuing"></a>Motivos para usar la cola
Antes de adentrarnos en el código de hello tooset necesaria de esta aplicación, considere la posibilidad de ventajas de hello del uso de una cola en este escenario en lugar de tener terminales Hola POS hablar directamente (sincrónicamente) toohello el sistema de administración de inventario.

### <a name="temporal-decoupling"></a>Desacoplamiento temporal
Con el patrón de mensajería asincrónica de hello, productores y consumidores no tienen toobe en línea en hello mismo tiempo. infraestructura de mensajería de Hello almacena de forma confiable los mensajes hasta que la parte consumidora de hello esté listo tooreceive ellos. Esto significa componentes Hola de aplicación hello distribuida pueden estar desconectados, ya sea voluntariamente; Por ejemplo, para el mantenimiento o debido a un bloqueo del componente tooa, sin que afecte a todo sistema de Hola. Además, Hola consumiendo aplicación solo puede tener toobe en línea durante determinadas horas del día de Hola. Por ejemplo, en este escenario comercial, sistema de administración de inventario de hello solo puede tener toocome en línea después del final de Hola de día laborable de Hola.

### <a name="load-leveling"></a>Redistribución de la carga
En muchas aplicaciones de la carga del sistema cambia con el tiempo, mientras que el tiempo de procesamiento de hello necesario para cada unidad de trabajo es normalmente constante. Intermediar mensaje productores y consumidores con un medio de cola que Hola aplicación que consume (trabajo hello) solo tiene toobe aprovisiona tooservice un promedio de carga en lugar de una carga máxima. profundidad de Hola de cola de hello crecerán y contrato Hola entrante carga varía. Esto directamente ahorra dinero con cantidad de toohello independientemente de la carga de la aplicación de infraestructura necesario tooservice Hola.

![Imagen de colas de Service Bus 2](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>Equilibrio de carga
Como Hola aumenta la carga, más procesos de trabajo pueden ser agregado tooread de cola de trabajo de Hola. Cada mensaje se procesa solamente mediante uno de los procesos de trabajo de Hola. Además, este equilibrio de carga basados en extracción permite un uso óptimo de los equipos de trabajo de Hola incluso si los equipos de trabajo de hello diferencian la potencia de tooprocessing tener en cuenta, ya que extraerán mensajes a su propia velocidad máxima. Este patrón a menudo se denomina patrón de consumidor competencia Hola.

![Imagen de colas de Service Bus 3](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>Acoplamiento débil
Uso de message Queue Server toointermediate entre los consumidores y productores de mensajes proporciona un acoplamiento débil intrínseco entre los componentes de Hola. Como los productores y consumidores no son compatibles con unos de otros, un consumidor puede actualizarse sin tener ningún efecto en productor Hola. Además, Hola topología de mensajería puede evolucionar sin que afecte a los extremos existentes de Hola. Esto se tratará con mayor detalle cuando se expliquen la publicación y la suscripción.

## <a name="show-me-hello-code"></a>Muéstrame el código de hello
Hola la siguiente sección se muestra cómo toouse Service Bus toobuild esta aplicación.

### <a name="sign-up-for-an-azure-account"></a>Registro para obtener una cuenta de Azure
Necesitará una cuenta de Azure en toostart orden trabajar con Bus de servicio. Si no tiene una, puede registrarse para obtener una cuenta gratuita [aquí](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="create-a-namespace"></a>Creación de un espacio de nombres
Una vez que tenga una suscripción, puede [crear un espacio de nombres de servicio](service-bus-create-namespace-portal.md). Cada espacio de nombres actúa como contenedor con un ámbito para un conjunto de entidades de Bus de servicio. Asigne un nombre único al nuevo espacio de nombres en todas las cuentas de Bus de servicio. 

### <a name="install-hello-nuget-package"></a>Instalar el paquete de NuGet Hola
espacio de nombres de Bus de servicio de hello toouse, una aplicación debe hacer referencia a Hola ensamblado de Bus de servicio, específicamente Microsoft.ServiceBus.dll. Puede encontrar este ensamblado como parte del SDK de Microsoft Azure de Hola y Hola descarga está disponible en hello [página de descarga del SDK de Azure](https://azure.microsoft.com/downloads/). Sin embargo, Hola [paquete NuGet de Bus de servicio](https://www.nuget.org/packages/WindowsAzure.ServiceBus) es hello tooget de manera más fácil de hello API de Service Bus y tooconfigure la aplicación con todas las dependencias de Bus de servicio de Hola de.

### <a name="create-hello-queue"></a>Crear cola Hola
Las operaciones de administración de Service Bus entidades de mensajería (colas y publicación/suscripción temas) se realizan a través de hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) clase. Service Bus usa un modelo de seguridad basado en la [firma de acceso compartido (SAS)](service-bus-sas.md). Hola [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) clase representa un proveedor de tokens de seguridad con métodos de fábrica integrados que devuelven algunos proveedores de tokens bien conocidos. Vamos a usar un [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) credenciales SAS de método toohold Hola. Hola [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) instancia, a continuación, se construye con la dirección base de hello del espacio de nombres de Bus de servicio de Hola y el proveedor de tokens de Hola.

Hola [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) clase proporciona métodos toocreate, enumerar y eliminar entidades de mensajería. Hola código que se muestra a continuación se muestra cómo Hola [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) instancia es Hola crea y se utiliza toocreate **DataCollectionQueue** cola.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

Tenga en cuenta que hay sobrecargas de hello [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) método que permiten las propiedades de hello cola toobe optimizado. Por ejemplo, puede establecer Hola time-to-live (TTL) predeterminado para los mensajes enviados a cola toohello.

### <a name="send-messages-toohello-queue"></a>Cola de mensajes toohello de envío
En el caso de operaciones en tiempo de ejecución en entidades de Service Bus (por ejemplo, enviar y recibir mensajes), una aplicación debe crear primero un objeto [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory). Toohello similar [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) clase hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) se crea una instancia de la dirección base de Hola de espacio de nombres de servicio de Hola y el proveedor de tokens de Hola.

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

Mensajes envían a y recibidos de Bus de servicio colas son instancias de hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) clase. Esta clase está formada por un conjunto de propiedades estándar (como [etiqueta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) y [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un diccionario de propiedades de la aplicación de uso toohold y un cuerpo de datos de aplicación arbitrarios. Una aplicación puede establecer cuerpo Hola pasando cualquier objeto serializable (hello en el ejemplo siguiente se pasa en un **SalesData** objeto que representa los datos de ventas de Hola de terminal de hello POS), que va a usar hello [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) objeto de hello tooserialize. También se puede proporcionar un objeto [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx).

Hola tooa de mensajes de toosend de manera más fácil dada cola, en nuestro caso hello **DataCollectionQueue**, es toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate una [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) objeto directamente desde hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instancia.

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-hello-queue"></a>Recibir mensajes de Hola cola
tooreceive mensajes de cola de hello, puede usar un [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objeto que cree directamente desde hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) con [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Los receptores de mensajes pueden funcionar en dos modos distintos: **ReceiveAndDelete** y **PeekLock**. Hola [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) se establece cuando se crea el receptor del mensaje de Hola, como un parámetro toohello [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) llamar.

Cuando se usa hello **ReceiveAndDelete** Hola de modo de recepción es una operación de captura único; es decir, al Bus de servicio recibe una solicitud de hello, marca Hola mensaje como consumido y lo devuelve toohello aplicación. **ReceiveAndDelete** modo es el modelo más sencillo de Hola y funciona mejor para escenarios en qué Hola aplicación puede tolerar no procesar un mensaje si toooccur de fuera de un error. toounderstand esto, considere un escenario en los problemas del consumidor Hola Hola recibir la solicitud y, a continuación, se bloquea antes de procesarlo. Puesto que el Bus de servicio marcado como mensaje de Hola como consumido, cuando reinicios de la aplicación hello y consumir mensajes de nuevo, se inicia habrá perdido mensaje de Hola que se consumió antes bloqueo Hola.

En **PeekLock** Hola de modo de recepción se convierte en una operación de dos fases, lo que hace posible toosupport aplicaciones que no pueden tolerar mensajes perdidos. Al Bus de servicio recibe una solicitud de hello, lo busca Hola siguiente mensaje toobe consumido, lo bloquea tooprevent otros consumidores de recibirlo y, a continuación, lo devuelve toohello aplicación. Después de aplicación hello finaliza el procesamiento de mensajes de bienvenida (o lo almacena de forma confiable para el procesamiento futuro), completa Hola segunda fase del programa Hola a recibir el proceso mediante una llamada a [completar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) en mensajes de bienvenida recibido. Al Bus de servicio ve hello [completar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) llamada, marca Hola mensaje como consumido.

Hay otros dos resultados posibles. En primer lugar, si no puede aplicación hello tooprocess Hola mensaje por alguna razón, puede llamar a [abandonar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) en el mensaje de bienvenida recibido (en lugar de [completar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Esto hace que el mensaje de bienvenida de Bus de servicio toounlock y hacerla disponible toobe recibido de nuevo, ya sea mediante Hola mismo consumidor o por otro consumidor completando. En segundo lugar, hay un tiempo de espera asociado con bloqueo de Hola y mensaje de Hola y configurarlo toobe disponible como si la aplicación hello no puede procesar el mensaje de bienvenida antes de tiempo de espera de bloqueo de hello expira (por ejemplo, si se bloquea aplicación hello), a continuación, desbloqueará Bus de servicio recibido nuevo (básicamente realizar un [abandonar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) operación de forma predeterminada).

Tenga en cuenta que si hello aplicación se bloquea después de procesar mensajes de bienvenida, pero antes de hello [completar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) se emitió la solicitud, mensaje de saludo será aplicación toohello entregados de nuevo cuando se reinicia. Esto se suele denominar * al menos una vez * de procesamiento. Esto significa que cada mensaje se procesará al menos una vez, pero en cierto Hola de situaciones puede volverse a entregar el mismo mensaje. Si el escenario de hello no puede tolerar el procesamiento duplicado, se requiere ninguna lógica adicional duplicados de toodetect aplicación Hola. Esto se puede conseguir basándose en hello [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) propiedad de mensaje de bienvenida. valor de Hola de esta propiedad permanece constante entre intentos de entrega. Esto se conoce como procesamiento *Una sola vez*.

recibe Hello código que se muestra aquí y procesa un mensaje mediante hello **PeekLock** modo, que es el valor predeterminado de Hola si no hay ningún [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) valor se proporciona explícitamente.

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

### <a name="use-hello-queue-client"></a>Usar el cliente de cola de Hola
Hola ejemplos anteriores de esta sección crean [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) y [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objetos directamente desde hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) toosend y recibir mensajes desde la cola de hello, respectivamente. Un enfoque alternativo es toouse una [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) objeto, que admite enviar y recibe las operaciones de adición toomore características avanzadas, como las sesiones.

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de colas, vea [crear aplicaciones que usan los temas de Bus de servicio y suscripciones](service-bus-create-topics-subscriptions.md) toocontinue esta discusión con capacidades de publicación/suscripción de Hola de temas de Bus de servicio y suscripciones.

