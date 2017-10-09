---
title: las aplicaciones de aaaCreate que usan los temas de Service Bus de Azure y suscripciones | Documentos de Microsoft
description: "Introducción toohello publicación / suscripción capacidades que ofrecen las suscripciones y los temas de Bus de servicio."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: f6d7de46ace7bd5b49de612db213ced789308d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Creación de aplicaciones que usan temas y suscripciones de Service Bus
El Bus de servicio de Azure admite un conjunto de tecnologías middleware orientadas a mensajes basadas en la nube, entre las que se incluyen una cola de mensajes de confianza y una mensajería de publicación/suscripción duradera. En este artículo se basa en información de hello proporcionada en [crear aplicaciones que usan colas de Service Bus](service-bus-create-queues.md) y ofrece una introducción de capacidades de publicación/suscripción toohello ofrecidas por temas de Bus de servicio.

## <a name="evolving-retail-scenario"></a>Escenario minorista en evolución
Este artículo continúa el escenario de venta directa de hello utilizado en [crear aplicaciones que usan colas de Service Bus](service-bus-create-queues.md). Recuerde que los datos de ventas de los terminales individuales de punto de venta (POS) deben ser el sistema de administración de inventario de tooan enrutado que utiliza ese toodetermine datos cuándo toobe reponerse existencias. Cada terminal de punto de venta informa de sus datos de venta enviando mensajes toohello **DataCollectionQueue** cola, donde permanecen hasta que se reciben por el sistema de administración de inventario de hello, como se muestra aquí:

![Service Bus 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

tooevolve este escenario, un nuevo requisito ha sido agregado toohello sistema: propietario de la tienda de hello desea toobe toomonitor capaz de rendimiento de almacén de hello en tiempo real.

tooaddress este requisito, sistema de hello debe "cerrar" flujo de datos de ventas de Hola. Todavía queremos que cada mensaje enviado por hello POS terminales toobe envía toohello sistema de administración de inventario como antes pero queremos otra copia de cada mensaje que podemos usar propietario de la tienda de toopresent Hola panel Vista toohello.

En cualquier situación como esta, en el que necesita cada toobe mensaje consumido por varias partes, puede utilizar Service Bus *temas*. Temas proporcionan un modelo de publicación/suscripción en la que cada mensaje publicado se pone disponible tooone o más suscripciones registradas con tema de Hola. En cambio, con las colas cada mensaje lo recibe un único consumidor.

Tema de tooa se envían los mensajes de Hola misma forma en que se envían tooa cola. Sin embargo, los mensajes no se reciben del tema de hello directamente; que se reciben de las suscripciones. Un tema de tooa de suscripción se puede considerar como una cola virtual que recibe copias de mensajes de saludo que se envían toothat tema. Los mensajes se reciben de una suscripción Hola de igual manera que se reciben de una cola.

Volviendo toohello escenario de venta directa, cola de Hola se sustituye por un tema y se agrega una suscripción, puede usar qué componente de sistema de administración de inventario de Hola. sistema de Hello aparece ahora como sigue:

![Service Bus 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

configuración de Hello aquí tiene un rendimiento idéntico toohello anterior basada en cola diseño. Es decir, los mensajes enviados toohello tema son enrutado toohello **inventario** suscripción, de qué hello **sistema de administración de inventario** los consume.

En el panel de administración de orden toosupport hello, creamos una segunda suscripción en el tema de hello, como se muestra aquí:

![Service Bus 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

Con esta configuración, cada mensaje de los terminales de hello POS estará disponible tooboth hello **panel** y **inventario** suscripciones.

## <a name="show-me-hello-code"></a>Muéstrame el código de hello
artículo de Hello [crear aplicaciones que usan colas de Service Bus](service-bus-create-queues.md) describe cómo toosign una copia de seguridad para una cuenta de Azure y crear un espacio de nombres de servicio. dependencias de Bus de servicio de manera más fáciles de Hello tooreference es tooinstall hello Service Bus [paquete Nuget](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). También puede encontrar hello las bibliotecas de Bus de servicio como parte del programa Hola a Azure SDK. Hello descarga está disponible en hello [página de descarga del SDK de Azure](https://azure.microsoft.com/downloads/).

### <a name="create-hello-topic-and-subscriptions"></a>Crear suscripciones y tema Hola
Las operaciones de administración de Service Bus entidades de mensajería (colas y publicación/suscripción temas) se realizan a través de hello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) clase. Son necesarias las credenciales adecuadas en orden toocreate una **NamespaceManager** instancia para un espacio de nombres determinado. Service Bus usa un modelo de seguridad basado en la [firma de acceso compartido (SAS)](service-bus-sas.md). Hola [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) clase representa un proveedor de tokens de seguridad con métodos de fábrica integrados que devuelven algunos proveedores de tokens bien conocidos. Vamos a usar un [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) credenciales SAS de método toohold Hola. Hola [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) instancia, a continuación, se construye con la dirección base de hello del espacio de nombres de Bus de servicio de Hola y el proveedor de tokens de Hola.

Hola [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) clase proporciona métodos toocreate, enumerar y eliminar entidades de mensajería. Hola código que se muestra a continuación se muestra cómo Hola **NamespaceManager** instancia es Hola crea y se utiliza toocreate **DataCollectionTopic** tema.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Tenga en cuenta que hay sobrecargas de hello [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) método que le permiten tooset propiedades de tema de Hola. Por ejemplo, puede establecer Hola time-to-live (TTL) predeterminado para los mensajes enviados toohello tema. A continuación, agregue hello **inventario** y **panel** suscripciones.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-toohello-topic"></a>Enviar tema toohello de mensajes
En el caso de operaciones en tiempo de ejecución en entidades de Service Bus (por ejemplo, enviar y recibir mensajes), una aplicación debe crear primero un objeto [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory). Toohello similar [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) clase hello **MessagingFactory** se crea una instancia de la dirección base de Hola de espacio de nombres de servicio de Hola y el proveedor de tokens de Hola.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

Tooand envía los mensajes recibido de temas de Bus de servicio, son instancias de hello [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) clase. Esta clase está formada por un conjunto de propiedades estándar (como [etiqueta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) y [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), un diccionario de propiedades de la aplicación de uso toohold y un cuerpo de datos de aplicación arbitrarios. Una aplicación puede establecer cuerpo Hola pasando cualquier objeto serializable (hello en el ejemplo siguiente se pasa en un **SalesData** objeto que representa los datos de ventas de Hola de terminal de hello POS), que va a usar hello [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) objeto de hello tooserialize. También se puede proporcionar un objeto [Stream](https://msdn.microsoft.com/library/system.io.stream.aspx).

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

tema de Hello más fácil manera toosend mensajes toohello es toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate una [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) objeto directamente desde hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instancia:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Recepción de mensajes de una suscripción
Colas de toousing similar, los mensajes de tooreceive de una suscripción puede utilizar un [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objeto que cree directamente desde hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) con [ CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Puede usar uno de hello diferentes modos de recepción (**ReceiveAndDelete** y **PeekLock**), como se describe en [crear aplicaciones que usan colas de Service Bus](service-bus-create-queues.md).

Tenga en cuenta que, cuando se crea un **MessageReceiver** para las suscripciones, Hola *entityPath* parámetro tiene forma de hello `topicPath/subscriptions/subscriptionName`. Por lo tanto, toocreate una **MessageReceiver** para hello **inventario** suscripción de hello **DataCollectionTopic** tema, *entityPath*debe establecerse demasiado`DataCollectionTopic/subscriptions/Inventory`. código de Hello aparece como sigue:

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
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

## <a name="subscription-filters"></a>Filtros de suscripción
Hasta ahora, en este escenario, todos los mensajes enviados toohello tema se realizan suscripciones disponibles tooall registrado. Hola de frases clave aquí es "puesto a disposición." Mientras que las suscripciones de Bus de servicio ven todos los mensajes enviados toohello tema, puede copiar solo un subconjunto de esas cola de mensajes toohello suscripción virtual. Esto se realiza mediante los *filtros* de suscripción. Cuando se crea una suscripción, puede proporcionar una expresión de filtro en forma de Hola de un predicado de estilo de SQL92 que opera en las propiedades de Hola de mensaje de bienvenida, ambos Hola propiedades del sistema (por ejemplo, [etiqueta](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) y la aplicación hello propiedades, como **StoreName** en el ejemplo anterior de Hola.

Evolucionando Hola escenario tooillustrate esto, es un segundo almacén de escenario de venta directa de toobe tooour agregada. Datos de ventas de todos los terminales de hello POS desde ambos almacenes de todavía tienen sistema de administración de inventario de toobe enrutan toohello centralizada, pero un jefe de tienda con hello panel herramienta solo está interesado en el rendimiento de Hola de ese almacén. Puede usar el filtrado tooachieve esto de suscripción. Tenga en cuenta que cuando los terminales de hello POS publican mensajes, establezca hello **StoreName** propiedad de la aplicación en el mensaje de bienvenida. Proporcionar dos almacenes, por ejemplo **Redmond** y **Seattle**, terminales de hello POS Hola Redmond almacenan marca los mensajes de sus datos de ventas con un **StoreName** igual demasiado **Redmond**, mientras que Hola Seattle almacenar POS terminales use un **StoreName** igual demasiado**Seattle**. Administrador de almacén de Hola de hello Redmond almacenar solo desea toosee datos de sus terminales de punto de venta. sistema de Hello aparece como sigue:

![Service-Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

tooset el enrutamiento, creas hello **panel** suscripción como se indica a continuación:

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

Con este [filtro de suscripción](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), sólo los mensajes que tienen hello **StoreName** propiedad establecida demasiado**Redmond** será toohello copiada cola virtual para hello **Panel** suscripción. Hay mucho más toosubscription filtrado, sin embargo. Las aplicaciones pueden tener varias reglas de filtro por suscripción en suma toohello capacidad toomodify Hola propiedades de un mensaje cuando pasan cola virtual de la suscripción de tooa.

## <a name="summary"></a>Resumen
Todos de hello motivos toouse Queue descritos en [crear aplicaciones que usan colas de Service Bus](service-bus-create-queues.md) también se aplican tootopics, específicamente:

* Desacoplamiento temporal: mensaje productores y consumidores no tienen toobe en línea en hello mismo tiempo.
* Nivelado de carga: picos de carga son atenuados por tema Hola habilitar consumo toobe aplicaciones aprovisionado para la carga Media en lugar de carga máxima.
* Equilibrio de carga: cola tooa similar, puede tener varios consumidores en competencia escuchando una sola suscripción, con cada mensaje entregado tooonly uno de los consumidores de hello, con lo que Equilibrio de carga.
* Acoplamiento flexible: puede evolucionar Hola mensajería red sin que afecte a los extremos existentes; Por ejemplo, agregando suscripciones o cambiando filtros tooa tema tooallow nuevos consumidores.

## <a name="next-steps"></a>Pasos siguientes

Vea [crear aplicaciones que usan colas de Service Bus](service-bus-create-queues.md) para obtener información acerca de cómo toouse pone en cola en el escenario de venta directa de hello POS.

