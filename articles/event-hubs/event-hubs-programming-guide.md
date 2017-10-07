---
title: "Guía de aaaProgramming para los concentradores de eventos de Azure | Documentos de Microsoft"
description: "Escribir código para los concentradores de eventos de Azure con hello Azure .NET SDK."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>Guía de programación de Centros de eventos

En este artículo se describe algunos escenarios comunes para escribir código que usa hello Azure SDK para .NET y los centros de eventos de Azure. En él se presupone un conocimiento previo de los centros de eventos. Para obtener información conceptual de los centros de eventos, vea hello [información general de los centros de eventos](event-hubs-what-is-event-hubs.md).

## <a name="event-publishers"></a>Publicadores de eventos

Enviar el concentrador de eventos de eventos tooan ya sea mediante HTTP POST o a través de una conexión de AMQP 1.0. Hola elección de qué toouse y cuándo depende de escenario específico de hello está solucionando. Las conexiones AMQP 1.0 se miden como conexiones asincrónicas en el Bus de servicio y son más apropiadas en los escenarios con volúmenes mayores de mensajes frecuentes y requisitos de latencia menores, ya que proporcionan un canal de mensajería persistente.

Crear y administrar los centros de eventos con hello [NamespaceManager][] clase. Cuando API administradas mediante .NET hello, Hola principal se crea para publicar datos tooEvent concentradores son hello [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) y [EventData][] clases. [EventHubClient][] proporciona el canal de comunicación de AMQP de hello en el cual se envían eventos toohello concentrador de eventos. Hola [EventData][] clase representa un evento y centro de eventos de toopublish usa mensajes tooan. Esta clase incluye el cuerpo de hello, algunos metadatos e información de encabezado acerca del evento Hola. Otras propiedades se agregan toohello [EventData][] cuando pasan a través de un concentrador de eventos de objeto.

## <a name="get-started"></a>Primeros pasos

clases de .NET de Hola que admiten los concentradores de eventos se muestran en hello ensamblado Microsoft.ServiceBus.dll. Hola más fácil Hola de manera tooreference API de Service Bus y tooconfigure la aplicación con todas las dependencias de Bus de servicio de hello es hello toodownload [paquete NuGet de Bus de servicio](https://www.nuget.org/packages/WindowsAzure.ServiceBus). Como alternativa, puede usar hello [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) en Visual Studio. toodo por lo tanto, emitir Hola siguiente comando en hello [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ventana:

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>Creación de un centro de eventos
Puede usar hello [NamespaceManager][] clase toocreate centros de eventos. Por ejemplo:

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

En la mayoría de los casos, se recomienda que utilice hello [CreateEventHubIfNotExists][] tooavoid de métodos que se generen excepciones si se reinicia el servicio de Hola. Por ejemplo:

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

Todas las operaciones de creación de centros de eventos, incluidos los [CreateEventHubIfNotExists][], requieren **administrar** permisos en el espacio de nombres de hello en cuestión. Si desea que los permisos de hello toolimit de las aplicaciones de consumidor o publicador, puede evitar estas crear llamadas de operación en el código de producción cuando utilice credenciales con permisos limitados.

Hola [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) clase contiene detalles acerca de un centro de eventos, incluidas las reglas de autorización de hello, intervalo de retención de mensajes de Hola, Id. de partición, estado y ruta de acceso. Puede usar estos metadatos de clase tooupdate hello en un centro de eventos.

## <a name="create-an-event-hubs-client"></a>Creación de un cliente de Centro de eventos
Hola clase principal para interactuar con los concentradores de eventos es [Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]. Esta clase proporciona capacidades de remitente y receptor. Puede crear una instancia de esta clase utilizando hello [Create](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) método, como se muestra en el siguiente ejemplo de Hola.

```csharp
var client = EventHubClient.Create(description.Path);
```

Este método usa la información de conexión de Bus de servicio de hello en hello archivo App.config, hello `appSettings` sección. Para obtener un ejemplo de Hola `appSettings` XML utiliza la información de conexión de Bus de servicio de toostore hello, consulte la documentación de Hola para hello [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) método.

Otra opción es cliente de hello toocreate desde una cadena de conexión. Esta opción funciona bien cuando se utilizan los roles de trabajador de Azure, ya que permite almacenar la cadena de hello en Propiedades de configuración de hello para el trabajo de Hola. Por ejemplo:

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

cadena de conexión de Hello estará en hello mismo formato tal y como aparece en el archivo App.config de Hola para los métodos anteriores de hello:

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

Por último, también es posible toocreate una [EventHubClient][] objeto desde un [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) instancia, tal y como se muestra en el siguiente ejemplo de Hola.

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

Es importante toonote adicional que [EventHubClient][] objetos creados a partir de una instancia del generador de mensajería reutilizará Hola misma conexión TCP subyacente. Por lo tanto, estos objetos tienen un límite de cliente en el rendimiento. Hola [Create](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) método reutiliza una única fábrica de mensajería. Si necesita un rendimiento muy alto desde un único remitente, puede crear varios generadores de mensajería y un objeto [EventHubClient][] desde cada uno de ellos.

## <a name="send-events-tooan-event-hub"></a>Centro de eventos de tooan de eventos de envío
Enviar el concentrador de eventos de tooan de eventos mediante la creación de un [EventData][] instancia y enviarlo a través de hello [enviar](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) método. Este método toma un único [EventData][] parámetro de instancia y envía de forma sincrónica, tooan concentrador de eventos.

## <a name="event-serialization"></a>Serialización de eventos
Hola [EventData][] clase tiene [cuatro sobrecargados constructores](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) que tomar una amplia variedad de parámetros, como un objeto y serializador, una matriz de bytes o una secuencia. También es posible tooinstantiate hello [EventData][] clase y establezca la secuencia del cuerpo Hola posteriormente. Al usar JSON con [EventData][], puede usar **Encoding.UTF8.GetBytes()** tooretrieve matriz de bytes de Hola para una cadena codificada en JSON.

## <a name="partition-key"></a>Clave de partición
Hola [EventData][] clase tiene un [PartitionKey][] propiedad que habilita Hola remitente toospecify un valor que se aplica un algoritmo hash tooproduce una asignación de la partición. El uso de una clave de partición garantiza todos Hola eventos con la misma clave se envían de hello toohello igual de partición en el concentrador de eventos de Hola. Las claves de partición comunes incluyen identificadores de sesión e identificadores de remitente únicos. Hola [PartitionKey][] propiedad es opcional y puede proporcionarse al usar hello [Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) o [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) métodos. Si no proporciona un valor para [PartitionKey][], envía los eventos son toopartitions distribuida mediante un modelo round-robin.

### <a name="availability-considerations"></a>Consideraciones sobre disponibilidad

Uso de una clave de partición es opcional y debe considerar detenidamente si toouse uno. En muchos casos, el uso de una clave de partición es una buena elección si el orden de los eventos es importante. Cuando se usa una clave de partición, estas particiones requieren la disponibilidad en un solo nodo y las interrupciones pueden producirse a lo largo del tiempo; por ejemplo, cuando los nodos de ejecución se reinician y revisan. Por lo tanto, si establece un Id. de partición y esa partición deja de estar disponible por alguna razón, un intento de tooaccess los datos de hello en esa partición se producirá un error. Si la alta disponibilidad es más importante, no especifique una clave de partición; en ese caso se enviará eventos toopartitions con hello round robin modelo que se ha descrito anteriormente. En este escenario, se realiza una selección explícita entre disponibilidad (ningún Id. de partición) y la coherencia (fijar el Id. de partición de tooa de eventos).

Otra consideración es el control de retrasos en el procesamiento de eventos. En algunos casos podría ser mejor datos toodrop y vuelva a intentar que tootry y mantenerse al día con el procesamiento, que puede provocar retrasos de procesamiento adicional que se siguen en la cadena. Por ejemplo, con un indicador de cotizaciones bursátiles es mejor toowait para completa de los datos actualizada, pero en un chat en vivo o escenario VOIP que prefiere tener datos Hola rápidamente, incluso si no está completa.

Debido a estas consideraciones de disponibilidad, en estos escenarios puede elegir uno de hello siguiendo las estrategias de control de errores:

- Detener (dejar de leer Event Hubs hasta que se solucionen cosas)
- Quitar (los mensajes no son importantes, quítelos)
- Vuelva a intentar (Hola de reintento mensajes como ver ajusten)
- [Mensajes no enviados](../service-bus-messaging/service-bus-dead-letter-queues.md) (utilice una cola o toodead de concentrador de eventos otra carta solo los mensajes de Hola no pudo procesar)

Para obtener más información y una explicación sobre Hola ventajas y desventajas de disponibilidad y la coherencia, consulte [disponibilidad y coherencia en los centros de eventos](event-hubs-availability-and-consistency.md). 

## <a name="batch-event-send-operations"></a>Operaciones de envío de eventos por lotes
El envío de eventos por lotes puede aumentar drásticamente el rendimiento. Hola [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) método toma una **IEnumerable** parámetro de tipo [EventData][] y envía Hola lote completo como un concentrador de eventos de toohello operación atómica.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

Tenga en cuenta que un único lote no debe superar el límite de 256 KB de Hola de un evento. Además, cada mensaje Hola lote usa Hola misma identidad de publicador. Es responsabilidad Hola de hello remitente tooensure que Hola por lotes no supere el tamaño máximo del evento de Hola. Si es así, se generará un error de **envío** de cliente.

## <a name="send-asynchronously-and-send-at-scale"></a>Enviar de forma asincrónica y enviar a escala
También puede enviar concentrador de eventos de tooan de eventos de forma asincrónica. Envío asincrónico puede aumentar la velocidad de hello en el que un cliente es capaz de toosend eventos. Ambos hello [enviar](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) y [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) métodos están disponibles en las versiones asincrónicas que devuelven un [tarea](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) objeto. Aunque esta técnica puede aumentar el rendimiento, pueden hacer Hola eventos de cliente toocontinue toosend incluso mientras se está limitando por hello servicio de centros de eventos y puede dar lugar a Hola cliente experimente errores o mensajes perdidos si no se implementa correctamente. Además, puede usar hello [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) propiedad sobre las opciones de reintento de hello cliente toocontrol cliente.

## <a name="create-a-partition-sender"></a>Crear un remitente de partición
Aunque es más común toosend eventos tooan concentrador de eventos sin una clave de partición, en algunos casos le podría interesar toosend eventos directamente tooa dada la partición. Por ejemplo:

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) devuelve un [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) objeto que puede usar toopublish partición del concentrador de eventos tooa evento específico.

## <a name="event-consumers"></a>Consumidores de eventos
Los centros de eventos tienen dos modelos principales para el consumo de eventos: receptores directos y abstracciones de nivel superior, como [EventProcessorHost][]. Receptores directos son responsables de su propia coordinación toopartitions de acceso dentro de un grupo de consumidores.

### <a name="direct-consumer"></a>Consumidor directo
Hola tooread de manera más directa de una partición dentro de un grupo de consumidores es hello de toouse [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) clase. toocreate una instancia de esta clase, debe utilizar una instancia de hello [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) clase. En el siguiente ejemplo de Hola Hola Id. de partición debe especificarse al crear el receptor de hello para el grupo de consumidores de Hola.

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

Hola [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) método tiene varias sobrecargas que proporcionan control sobre el lector de Hola que se está creando. Estos métodos incluyen la especificación de un desplazamiento como una cadena o una marca de tiempo y Hola capacidad toospecify si tooinclude este desplazamiento especificado de hello devuelve transmitir por secuencias o iniciar después de él. Después de crear el receptor de hello, puede empezar a recibir eventos en hello devuelve el objeto. Hola [recepción](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) método tiene cuatro sobrecargas que Hola control recibir parámetros de operación, como el tamaño de lote y tiempo de espera. Puede usar las versiones asincrónicas de Hola de estos rendimiento de hello tooincrease de métodos de un consumidor. Por ejemplo:

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

Con partición específica de tooa de sentido, se reciben mensajes de saludo en orden de hello en el que se enviaron toohello concentrador de eventos. desplazamiento de Hello es una cadena token usado tooidentify un mensaje en una partición.

Tenga en cuenta que una sola partición dentro de un grupo de consumidores no puede tener más de 5 lectores simultáneos conectados en un determinado momento. Como los lectores se conectan o se desconectan, sus sesiones pueden permanecer activas durante varios minutos antes de que el servicio de hello reconoce que se han desconectado. Durante este tiempo, volver a conectar tooa partición puede producir un error. Para obtener un ejemplo completo de la escritura de un receptor directo para los concentradores de eventos, vea hello [receptores directos de centros de eventos](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) ejemplo.

### <a name="event-processor-host"></a>Host del procesador de eventos
Hola [EventProcessorHost][] clase procesa los datos de los centros de eventos. Debe utilizar esta implementación al generar los lectores de eventos en la plataforma .NET de Hola. [EventProcessorHost][] proporciona un entorno de tiempo de ejecución seguro, seguro para subprocesos y de varios procesos para las implementaciones de procesadores de eventos que también ofrecen administración de concesión de puntos de comprobación y particiones.

Hola toouse [EventProcessorHost][] (clase), puede implementar [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor). Esta interfaz contiene tres métodos:

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

crear una instancia de toostart procesamiento de eventos, [EventProcessorHost][], proporcionando los parámetros apropiados de hello para el centro de eventos. A continuación, llame a [RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister su [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) implementación con hello en tiempo de ejecución. En este momento, el host de hello intentará tooacquire una concesión en cada partición de concentrador de eventos de hello usando un algoritmo "expansivo". Estas concesiones durarán un período de tiempo determinado y, a continuación, deben renovarse. Como nuevos nodos, instancias de trabajo en este caso, se ponen en línea, colocan reservas de concesiones y con el tiempo carga Hola se desplaza entre los nodos según cada uno intenta tooacquire más concesiones.

![Host del procesador de eventos](./media/event-hubs-programming-guide/IC759863.png)

Con el tiempo, se establece un equilibrio. Esta capacidad dinámica permite la Autoescala basada en CPU toobe aplica tooconsumers de ampliación y reducción. Dado que los centros de eventos no tiene un concepto directo de números de mensajes, uso promedio de CPU suele ser Hola mecanismo toomeasure back-end o un consumidor escala adecuada. Si los publicadores comienzan toopublish que pueden procesar más eventos que los consumidores, aumento de la CPU de hello en los consumidores puede ser usado toocause una escala automática en el recuento de instancias de trabajo.

Hola [EventProcessorHost][] clase también implementa un mecanismo de puntos de comprobación basado en almacenamiento de Azure. Este Hola de almacenes de mecanismo de desplazamiento en una base por partición, para que cada consumidor pueda determinar qué Hola último punto de comprobación del consumidor anterior Hola era. Al igual que crea particiones transición entre los nodos mediante concesiones, este es el mecanismo de sincronización de Hola que facilita el cambio de carga.

## <a name="publisher-revocation"></a>Revocación de publicador
Además toohello avanzadas características en tiempo de ejecución de [EventProcessorHost][], centros de eventos permiten la revocación del publicador de orden tooblock específico de los publicadores en el concentrador de eventos de tooan de eventos de envío. Estas características son especialmente útiles si un token de publicador se ha puesto en peligro o una actualización de software está haciendo toobehave incorrectamente. En estas situaciones, se puede bloquear la identidad del publicador de hello, que forma parte de su token de SAS, desde la publicación de eventos.

Para obtener más información acerca de la revocación del publicador y cómo toosend tooEvent concentradores como publicador, vea hello [evento centros de gran escala publicación segura](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) ejemplo.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de escenarios de centros de eventos, visite estos vínculos:

* [Introducción a la API de centros de eventos](event-hubs-api-overview.md)
* [¿Qué es Event Hubs?](event-hubs-what-is-event-hubs.md)
* [Disponibilidad y coherencia en Event Hubs](event-hubs-availability-and-consistency.md)
* [Referencia de la API de host del procesador de eventos](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
