---
title: "prácticas recomendadas de aaaBest para mejorar el rendimiento de uso del Bus de servicio de Azure | Documentos de Microsoft"
description: "Describe cómo toouse rendimiento toooptimize de Bus de servicio al intercambiar asíncrona los mensajes."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e756c15d-31fc-45c0-8df4-0bca0da10bb2
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2017
ms.author: sethm
ms.openlocfilehash: 52764d227757cbb11246675878933f21685817f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-performance-improvements-using-service-bus-messaging"></a>Procedimientos recomendados para mejorar el rendimiento mediante la mensajería de Service Bus

Este artículo se describe cómo toouse [mensajería de Service Bus de Azure](https://azure.microsoft.com/services/service-bus/) asíncrona de toooptimize rendimiento al intercambiar mensajes. Hola primera parte de este tema describe mecanismos diferentes Hola que se ofrecen toohelp aumento del rendimiento. segunda parte de Hello proporciona instrucciones sobre cómo Hola a toouse Bus de servicio de forma que pueda ofrecer un rendimiento óptimo en un escenario determinado.

A lo largo de este tema, término Hola "cliente" hace referencia a entidad tooany que tiene acceso a Service Bus. Un cliente puede asumir el rol de Hola de un remitente o destinatario. Hola término "remitente" se usa para un cliente de cola o tema de Bus de servicio que envía mensajes tooa Bus de servicio cola o tema. Hola "receptor" se entiende a tooa Bus de servicio cola o suscripción de cliente que recibe los mensajes de una cola de Bus de servicio o la suscripción.

Estas secciones presentan varios conceptos que Service Bus usa toohelp mejorar el rendimiento.

## <a name="protocols"></a>Protocolos
Bus de servicio permite a los clientes toosend y recibir mensajes a través de uno de tres protocolos:

1. Advanced Message Queuing Protocol (AMQP)
2. Protocolo de mensajería de Service Bus (SBMP)
3. HTTP

AMQP y SBMP son más eficaces, debido a que mantienen Hola conexión tooService Bus siempre que exista el generador de mensajería de Hola. También implementa el procesamiento por lotes y la captura previa. A menos que se mencione explícitamente, todo el contenido de este tema supone el uso de Hola de AMQP o SBMP.

## <a name="reusing-factories-and-clients"></a>Reutilización de factorías y clientes
Los objetos de cliente de Service Bus, como [QueueClient][QueueClient] o [MessageSender][MessageSender], se crean mediante un objeto [MessagingFactory][MessagingFactory], que también proporciona administración interna de las conexiones. No debería cerrar fábricas de mensajes o cola, tema y los clientes de la suscripción después de enviar un mensaje y, a continuación, volver a crearlos cuando envíe mensajes de bienvenida del siguiente. Cerrar una fábrica de mensajería elimina Hola conexión toohello servicio service Bus, y se establece una nueva conexión al volver a crear el generador de Hola. Establecer que una conexión es una operación costosa, puede evitar al volver a usar Hola mismo cliente y generador de objetos para varias operaciones. Puede utilizar sin ningún riesgo hello [QueueClient] [ QueueClient] objeto para enviar mensajes desde varios subprocesos y de operaciones asincrónicas simultáneas. 

## <a name="concurrent-operations"></a>Operaciones simultáneas
Se tarda tiempo en realizar una operación (enviar, recibir, eliminar, etc.). Este tiempo incluye el procesamiento de Hola de operación de Hola por hello servicio de Bus de servicio en la latencia de toohello de adición de solicitud de Hola y respuesta de Hola. número de hello tooincrease de operaciones por tiempo, las operaciones deberán ejecutarse simultáneamente. Puede hacerlo de varias maneras diferentes:

* **Operaciones asincrónicas**: cliente hello programa las operaciones mediante la realización de operaciones asincrónicas. Hola siguiente solicitud se inicia antes de completar la solicitud anterior de Hola. Hola te mostramos un ejemplo de una operación de envío asincrónico:
  
 ```csharp
  BrokeredMessage m1 = new BrokeredMessage(body);
  BrokeredMessage m2 = new BrokeredMessage(body);
  
  Task send1 = queueClient.SendAsync(m1).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #1");
    });
  Task send2 = queueClient.SendAsync(m2).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #2");
    });
  Task.WaitAll(send1, send2);
  Console.WriteLine("All messages sent");
  ```
  
  Esto es un ejemplo de operación asincrónica de recepción:
  
  ```csharp
  Task receive1 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  Task receive2 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  
  Task.WaitAll(receive1, receive2);
  Console.WriteLine("All messages received");
  
  async void ProcessReceivedMessage(Task<BrokeredMessage> t)
  {
    BrokeredMessage m = t.Result;
    Console.WriteLine("{0} received", m.Label);
    await m.CompleteAsync();
    Console.WriteLine("{0} complete", m.Label);
  }
  ```
* **Varias fábricas**: Hola a todos los clientes (remitentes de suma tooreceivers) que se crean mediante misma fábrica recurso compartido de una conexión TCP. rendimiento máximo del mensaje de Hola está limitado por el número de Hola de operaciones que pueden pasar a través de esta conexión TCP. rendimiento de Hola que puede obtenerse con una sola fábrica varía en gran medida con tiempos de ida y vuelta de TCP y el tamaño de mensaje. tooobtain mayores tasas de rendimiento, debe usar varias fábricas de mensajes.

## <a name="receive-mode"></a>Modo de recepción
Al crear un cliente de cola o suscripción, puede especificar un modo de recepción: *Peek-lock* (Inspección y bloqueo) o *Receive And Delete* (Recepción y eliminación). modo de recepción predeterminado Hello es [PeekLock][PeekLock]. Cuando se trabaja en este modo, Hola cliente envía un mensaje de una solicitud tooreceive de Bus de servicio. Después de hello cliente recibe mensajes de bienvenida, envía un mensaje de saludo de solicitud toocomplete.

Al establecer Hola modo de recepción demasiado[ReceiveAndDelete][ReceiveAndDelete], ambos pasos se combinan en una sola solicitud. Esto reduce al número total de operaciones de Hola y puede mejorar Hola rendimiento global de mensajes. Esta mejora del rendimiento conlleva corre el riesgo de Hola de pérdida de mensajes.

El Bus de servicio no admite transacciones para las operaciones de recepción y eliminación. Además, se necesitan para cualquier escenario de en qué Hola cliente desea toodefer semántica de bloqueo o [mensajes no enviados](service-bus-dead-letter-queues.md) un mensaje.

## <a name="client-side-batching"></a>Procesamiento por lotes del lado cliente
Procesamiento por lotes de cliente permite a una cola o tema cliente toodelay Hola envío de un mensaje durante un período de tiempo determinado. Si el cliente de hello envía mensajes adicionales durante este período de tiempo, transmite mensajes de saludo en un único lote. Procesamiento por lotes de cliente también hace un toobatch de cliente de cola o suscripción varios **completar** solicitudes en una única solicitud. El procesamiento por lotes solo está disponible para las operaciones **Send** y **Complete** asincrónicas. Operaciones sincrónicas se envían inmediatamente toohello servicio service Bus. El procesamiento por lotes no tiene lugar para las operaciones de inspección o recepción, así como tampoco entre clientes.

De forma predeterminada, un cliente usa un intervalo entre lotes de 20 ms. Puede cambiar el intervalo del lote de Hola Hola establecer [BatchFlushInterval] [ BatchFlushInterval] propiedad antes de crear Hola fábrica de mensajería. Esta configuración afecta a todos los clientes que se creen en esta factoría.

procesamiento por lotes toodisable, establecer hello [BatchFlushInterval] [ BatchFlushInterval] propiedad demasiado**TimeSpan.Zero**. Por ejemplo:

```csharp
MessagingFactorySettings mfs = new MessagingFactorySettings();
mfs.TokenProvider = tokenProvider;
mfs.NetMessagingTransportSettings.BatchFlushInterval = TimeSpan.FromSeconds(0.05);
MessagingFactory messagingFactory = MessagingFactory.Create(namespaceUri, mfs);
```

Procesamiento por lotes no afecta al número de Hola de operaciones de mensajería facturables y solo está disponible para hello protocolo de cliente de Bus de servicio. Hola protocolo HTTP no es compatible con el procesamiento por lotes.

## <a name="batching-store-access"></a>Acceso al almacén de procesamiento por lotes
rendimiento de hello tooincrease de una cola, tema o suscripción, Bus de servicio procesa por lotes varios mensajes cuando escribe tooits internos del almacén. Si se habilita en una cola o tema, escribir mensajes en el almacén de Hola se procesarán por lotes. Si se habilita en una cola o suscripción, al eliminar los mensajes del almacén de Hola se procesarán por lotes. Si el acceso al almacén por lotes está habilitado para una entidad, Bus de servicio retrasa una operación de escritura de la tienda con respecto a esa entidad por seguridad too20ms. Operaciones de almacenamiento adicionales que se producen durante este intervalo se agregan toohello lote. El acceso al almacén de procesamiento por lotes solo afecta a las operaciones **Send** y **Complete**, pero no a las de recepción. El acceso al almacén de procesamiento por lotes es una propiedad de una entidad. El procesamiento por lotes se produce en todas las entidades que tengan habilitado el acceso al almacén de procesamiento por lotes.

Cuando se crea una cola, un tema o una suscripción nuevos, el acceso al almacén de procesamiento por lotes está habilitado de manera predeterminada. toodisable por lotes acceso al almacén, conjunto hello [EnableBatchedOperations] [ EnableBatchedOperations] propiedad demasiado**false** antes de crear entidad Hola. Por ejemplo:

```csharp
QueueDescription qd = new QueueDescription();
qd.EnableBatchedOperations = false;
Queue q = namespaceManager.CreateQueue(qd);
```

Acceso al almacén por lotes no afecta al número de Hola de operaciones de mensajería facturables y es una propiedad de una cola, tema o suscripción. Es independiente de hello hello y modo de protocolo que se utiliza entre un cliente y Hola servicio de Bus de servicio de recepción.

## <a name="prefetching"></a>Captura previa
La captura previa permite Hola cola o suscripción cliente tooload mensajes adicionales del servicio de hello cuando realiza una operación de recepción. cliente de Hello almacena estos mensajes en una caché local. tamaño de Hola de caché de hello viene determinado por hello [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] o [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] Propiedades. Cada cliente con la captura previa habilitada mantiene su propia memoria caché. La memoria caché no se comparte entre los clientes. Si el cliente de hello inicia una operación de recepción y su memoria caché está vacía, el servicio de hello transmite un lote de mensajes. tamaño de Hola de lote de hello es igual a tamaño Hola de memoria caché de Hola o 256 KB, lo que sea menor. Si Hola cliente inicia una operación de recepción y caché de hello contiene un mensaje, mensaje de bienvenida se realiza desde la caché de Hola.

Cuando un mensaje se realiza la captura previa, Hola servicio bloqueos Hola mensaje con captura previa. Al hacerlo, no se puede recibir mensaje con captura previa Hola otro destinatario. Si receptor hello no puede completar mensaje Hola antes de que expire el bloqueo de hello, mensaje de bienvenida se convierte en disponible tooother receptores. copia de Hello realiza la captura previa de mensajes de bienvenida permanece en memoria caché de Hola. Hello destinatario que consume Hola expirado en caché copia recibirá una excepción al intentar toocomplete ese mensaje. De forma predeterminada, el bloqueo del mensaje de Hola expira después de 60 segundos. Este valor puede ser extendido too5 minutos. consumo de hello tooprevent de mensajes que han expirado, tamaño de la caché de hello siempre debe ser menor que número Hola de mensajes que puede ser utilizado por un cliente dentro del intervalo de tiempo de espera de bloqueo de saludo.

Cuando se usa la expiración de bloqueo de saludo predeterminado de 60 segundos, un buen valor para [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] es 20 veces Hola máximo tasas de procesamiento de todos los destinatarios de fábrica de Hola. Por ejemplo, una fábrica crea 3 receptores y cada receptor puede procesar los mensajes de too10 por segundo. número de capturas previas Hello no debe superar 20 X 3 X 10 = 600. De forma predeterminada, [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] es too0 de conjunto, lo que significa que ningún mensaje adicional se recuperan del servicio de Hola.

La captura previa mensajes aumenta Hola rendimiento global de una cola o suscripción porque reduce Hola al número total de operaciones de mensajes o viajes de ida y vuelta. Obtener el primer mensaje de Hola, sin embargo, se tardará más tiempo (vence toohello aumentado el tamaño del mensaje). Recibir mensajes con captura previa será más rápida porque ya se han descargado estos mensajes por cliente Hola.

la propiedad time-to-live de (TTL) de Hola de un mensaje se comprueba por servidor hello en tiempo de hello servidor hello envía el cliente de toohello de mensaje de Hola. cliente Hello no comprueba la propiedad TTL del mensaje de Hola cuando se recibe el mensaje de bienvenida. En su lugar, se pueden recibir mensajes de bienvenida incluso si ha pasado el TTL del mensaje de Hola mientras se almacenó en caché de los mensajes de bienvenida del cliente Hola.

La captura previa no afecta al número de Hola de operaciones de mensajería facturables y solo está disponible para hello protocolo de cliente de Bus de servicio. Hola protocolo HTTP no admite la captura previa. La captura previa está disponible para las operaciones de recepción sincrónicas y asincrónicas.

## <a name="express-queues-and-topics"></a>Colas y temas exprés

Las entidades exprés habilitar los escenarios de menor latencia y alto rendimiento y solo se admiten en nivel de mensajería estándar Hola. Entidades creadas en [los espacios de nombres Premium](service-bus-premium-messaging.md) no admiten la opción rápida Hola. Con las entidades exprés, si se envía un mensaje tooa cola o tema, mensaje de bienvenida no se inmediatamente almacena en el almacén de mensajes de Hola. En su lugar, se almacena en la memoria caché. Si un mensaje permanece en la cola de Hola durante más de unos segundos, se escribe automáticamente almacenamiento toostable, lo que se protege contra la pérdida de vencimiento tooan interrupción. Escribir mensaje de saludo en una memoria caché aumenta el rendimiento y reduce la latencia porque no hay ningún acceso toostable storage en el mensaje de saludo de tiempo de Hola se envía. Los mensajes que se consumen en cuestión de segundos no se escriben toohello almacén de mensajes. Hola de ejemplo siguiente crea un tema exprés.

```csharp
TopicDescription td = new TopicDescription(TopicName);
td.EnableExpress = true;
namespaceManager.CreateTopic(td);
```

Si un mensaje que contiene información importante que no debe perderse se envía la entidad exprés tooan, remitente Hola puede forzar el Bus de servicio tooimmediately persista almacenamiento de toostable de mensajes de Hola Hola establecer [ForcePersistence] [ ForcePersistence] propiedad demasiado**true**.

> [!NOTE]
> Las entidades con la opción Rápido no admiten transacciones.

## <a name="use-of-partitioned-queues-or-topics"></a>Uso de colas o temas con particiones
Internamente, Bus de servicio usa Hola mismo nodo y tooprocess de almacén de mensajería y almacena todos los mensajes para una entidad de mensajería (cola o tema). Una cola o tema particionado, en hello otra parte, se distribuye por varios nodos y almacenes de mensajería. Las colas y los temas con particiones no solo producen un rendimiento mayor que las colas y los temas normales, sino que también ofrecen una mayor disponibilidad. toocreate una entidad particionada, conjunto hello [EnablePartitioning] [ EnablePartitioning] propiedad demasiado**true**, tal y como se muestra en el siguiente ejemplo de Hola. Para obtener más información sobre las entidades con particiones, consulte [Entidades de mensajería con particiones][Partitioned messaging entities].

```csharp
// Create partitioned queue.
QueueDescription qd = new QueueDescription(QueueName);
qd.EnablePartitioning = true;
namespaceManager.CreateQueue(qd);
```

## <a name="use-of-multiple-queues"></a>Uso de varias colas

Si no es posible toouse que una cola o tema o particionado Hola espera de carga no puede controlar una única cola o tema particionados, debe usar varias entidades de mensajes. Al usar varias entidades, cree un cliente dedicado para cada entidad, en lugar de usar Hola mismo cliente para todas las entidades.

## <a name="development-and-testing-features"></a>Características de desarrollo y pruebas

Service Bus tiene una característica que se utiliza específicamente para desarrollo que **nunca debe utilizarse en configuraciones de producción**: [TopicDescription.EnableFilteringMessagesBeforePublishing][].

Cuando se agregan nuevas reglas o filtros el tema toohello, puede usar [TopicDescription.EnableFilteringMessagesBeforePublishing][] tooverify que Hola nueva expresión de filtro funciona según lo previsto.

## <a name="scenarios"></a>Escenarios
Hello las secciones siguientes describen los escenarios de mensajería típicos y describen la configuración de Bus de servicio de hello preferido. Las tasas de rendimiento se clasifican como pequeñas (menos de 1 mensaje/segundo), moderadas (1 mensaje/segundo o más, pero menos de 100 mensajes/segundo) y altas (100 mensajes/segundo o más). Hello número de clientes que son pequeños moderados (5 o menos), (más de 5 pero menor que o igual too20) y gran tamaño (más de 20).

### <a name="high-throughput-queue"></a>Cola de alto rendimiento
Objetivo: Maximizar el rendimiento de Hola de una sola cola. Hola número de remitentes y destinatarios es pequeño.

* Use una cola particionada para mejorar la disponibilidad y el rendimiento.
* Hola tooincrease general tasa de envío en la cola de hello, utilice varios remitentes de toocreate de generadores de mensajes. Para cada remitente, use operaciones asincrónicas o varios subprocesos.
* Hola tooincrease general velocidad de recepción de cola de hello, utilice varios receptores de toocreate de generadores de mensaje.
* Utilice las operaciones asincrónicas tootake aprovechar el procesamiento por lotes de cliente.
* Establecer Hola número de intervalo too50ms tooreduce Hola de las transmisiones de protocolo de cliente de Bus de servicio de procesamiento por lotes. Si se utilizan varios remitentes, aumente hello too100ms de intervalo de procesamiento por lotes.
* Deje habilitado el acceso al almacén de procesamiento por lotes. Esto aumenta Hola general tasa a la que se pueden escribir mensajes en cola de Hola.
* Establecer tiempos de too20 de recuento de hello precarga de velocidad de procesamiento máxima de Hola de todos los destinatarios de una fábrica. Esto reduce el número de Hola de las transmisiones de protocolo de cliente de Bus de servicio.

### <a name="multiple-high-throughput-queues"></a>Varias colas de alto rendimiento
Objetivo: Maximizar el rendimiento general de varias colas. rendimiento de Hola de una cola individual es moderado o alto.

tooobtain al máximo el rendimiento a través de varias colas, usar la configuración de hello describe el rendimiento de hello toomaximize de una sola cola. Además, usar a los clientes de toocreate distintas fábricas que envíen o reciban desde diferentes colas.

### <a name="low-latency-queue"></a>Cola de baja latencia
Objetivo: minimizar la latencia de un extremo a otro de una cola o un tema. Hola número de remitentes y destinatarios es pequeño. rendimiento de Hola de cola de hello es pequeño o moderado.

* Use una cola particionada para mejorar la disponibilidad.
* Deshabilite el procesamiento por lotes del lado cliente. cliente de Hello envía inmediatamente un mensaje.
* Deshabilite el acceso al almacén de procesamiento por lotes. servicio de Hello escribe inmediatamente el almacén de toohello de mensajes de Hola.
* Si usa a un solo cliente, establezca el velocidad de procesamiento de hello precarga recuento too20 veces Hola de receptor de Hola. Si llegan varios mensajes en cola Hola Hola mismo tiempo, Hola protocolo de cliente de Bus de servicio transmitirá todos al Hola mismo tiempo. Cuando el cliente de hello recibe mensajes de bienvenida del siguiente, ese mensaje ya está en memoria caché local de Hola. caché de Hello debería ser bajo.
* Si usa a varios clientes, defina too0 de recuento de precarga de Hola. Al hacerlo, Hola segundo cliente puede recibir mensajes de bienvenida del segundo mientras el primer cliente de hello todavía está procesando el primer mensaje de Hola.

### <a name="queue-with-a-large-number-of-senders"></a>Cola con un gran número de remitentes
Objetivo: maximizar el rendimiento de una cola o un tema con un gran número de remitentes. Cada remitente envía mensajes a una tasa moderada. número de Hola de destinatarios es pequeño.

Bus de servicio permite una entidad de mensajería de too1000 conexiones simultáneas tooa (o 5000 mediante AMQP). Este límite se aplica en el nivel de espacio de nombres de Hola y las colas, temas/suscripciones quedan restringidas por límite de Hola de conexiones simultáneas por espacio de nombres. Para las colas, este número se comparte entre remitentes y receptores. Si todas las conexiones de 1000 son necesarias para los remitentes, debe reemplazar Hola cola con un tema y una sola suscripción. Un tema acepta too1000 conexiones simultáneas de remitentes, mientras que la suscripción de hello acepta un adicionales 1000 conexiones simultáneas a destinatarios. Si se requieren más de 1000 remitentes simultáneos, Hola deberán enviar mensajes toohello protocolo de Service Bus a través de HTTP.

rendimiento de toomaximize, Hola siguientes:

* Use una cola particionada para mejorar la disponibilidad y el rendimiento.
* Si cada remitente reside en un proceso diferente, use solo una única factoría para cada proceso.
* Utilice las operaciones asincrónicas tootake aprovechar el procesamiento por lotes de cliente.
* Usar valor predeterminado de hello intervalo de 20 ms. tooreduce Hola número de transmisiones de protocolo de cliente de Bus de servicio de procesamiento por lotes.
* Deje habilitado el acceso al almacén de procesamiento por lotes. Esto aumenta Hola general tasa a la que se pueden escribir mensajes en cola de Hola o un tema.
* Establecer tiempos de too20 de recuento de hello precarga de velocidad de procesamiento máxima de Hola de todos los destinatarios de una fábrica. Esto reduce el número de Hola de las transmisiones de protocolo de cliente de Bus de servicio.

### <a name="queue-with-a-large-number-of-receivers"></a>Cola con un gran número de receptores
Objetivo: Maximizar Hola velocidad de una cola o suscripción con un gran número de destinatarios de recepción. Cada receptor recibe mensajes a una tasa moderada. número de Hola de remitentes es pequeño.

Bus de servicio permite que una entidad de tooan de too1000 conexiones simultáneas. Si una cola requiere más de 1000 receptores, debe reemplazar Hola cola con un tema y varias suscripciones. Cada suscripción puede admitir hasta too1000 de conexiones simultáneas. Como alternativa, receptores pueden tener acceso a cola de Hola a través del protocolo HTTP Hola.

rendimiento de toomaximize, Hola siguientes:

* Use una cola particionada para mejorar la disponibilidad y el rendimiento.
* Si cada receptor reside en un proceso diferente, use solo una única factoría por proceso.
* Los receptores pueden usar operaciones sincrónicas o asincrónicas. Debido a moderada Hola velocidad de un destinatario individual de recepción, procesamiento por lotes de cliente de una solicitud completar no afecta al rendimiento del receptor.
* Deje habilitado el acceso al almacén de procesamiento por lotes. Esto reduce Hola carga global de entidad de Hola. También reduce Hola velocidad global con la que se pueden escribir mensajes en cola de Hola o un tema.
* Establecer valor pequeño tooa del recuento de precarga de hello (por ejemplo, PrefetchCount = 10). Esto evita que haya receptores inactivos mientras otros tienen un gran número de mensajes almacenados en caché.

### <a name="topic-with-a-small-number-of-subscriptions"></a>Tema con un número pequeño de suscripciones
Objetivo: Maximizar el rendimiento de Hola de un tema con un número pequeño de suscripciones. Se recibe un mensaje en numerosas suscripciones, lo que significa Hola combinan recepción velocidad en todas las suscripciones es mayor que la velocidad de envío de Hola. número de Hola de remitentes es pequeño. Hola número de destinatarios por suscripción es pequeño.

rendimiento de toomaximize, Hola siguientes:

* Use un tema con particiones para mejorar la disponibilidad y el rendimiento.
* Hola tooincrease general tasa de envío en el tema de hello, utilice varios remitentes de toocreate de generadores de mensajes. Para cada remitente, use operaciones asincrónicas o varios subprocesos.
* Hola tooincrease general velocidad de recepción de una suscripción, utilice varios receptores de toocreate de generadores de mensaje. Para cada receptor, use operaciones asincrónicas o varios subprocesos.
* Utilice las operaciones asincrónicas tootake aprovechar el procesamiento por lotes de cliente.
* Usar valor predeterminado de hello intervalo de 20 ms. tooreduce Hola número de transmisiones de protocolo de cliente de Bus de servicio de procesamiento por lotes.
* Deje habilitado el acceso al almacén de procesamiento por lotes. Esto aumenta Hola general tasa a la que se pueden escribir mensajes en el tema de Hola.
* Establecer tiempos de too20 de recuento de hello precarga de velocidad de procesamiento máxima de Hola de todos los destinatarios de una fábrica. Esto reduce el número de Hola de las transmisiones de protocolo de cliente de Bus de servicio.

### <a name="topic-with-a-large-number-of-subscriptions"></a>Tema con un gran número de suscripciones
Objetivo: Maximizar el rendimiento de Hola de un tema con un gran número de suscripciones. Se recibe un mensaje en numerosas suscripciones, lo que significa Hola combinan recepción velocidad en todas las suscripciones es mucho mayor que la velocidad de envío de Hola. número de Hola de remitentes es pequeño. Hola número de destinatarios por suscripción es pequeño.

Temas con un gran número de suscripciones suelen exponen un bajo rendimiento global si todos los mensajes enrutados tooall suscripciones. Esto se debe a hechos de Hola que cada mensaje se recibe muchas veces y todos los mensajes que se encuentran en un tema y todas sus suscripciones se almacenan en hello mismo almacenar. Se supone que el número de Hola de remitentes y el número de destinatarios por suscripción estén pequeños. Bus de servicio admite hasta too2, 000 suscripciones por tema.

rendimiento de toomaximize, Hola siguientes:

* Use un tema con particiones para mejorar la disponibilidad y el rendimiento.
* Utilice las operaciones asincrónicas tootake aprovechar el procesamiento por lotes de cliente.
* Usar valor predeterminado de hello intervalo de 20 ms. tooreduce Hola número de transmisiones de protocolo de cliente de Bus de servicio de procesamiento por lotes.
* Deje habilitado el acceso al almacén de procesamiento por lotes. Esto aumenta Hola general tasa a la que se pueden escribir mensajes en el tema de Hola.
* Establezca Hola precarga recuento too20 veces Hola se esperaba recepción de frecuencia en segundos. Esto reduce el número de Hola de las transmisiones de protocolo de cliente de Bus de servicio.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de optimizar el rendimiento de Bus de servicio, consulte [particiones entidades de mensajería][Partitioned messaging entities].

[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[PeekLock]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[ReceiveAndDelete]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[BatchFlushInterval]: /dotnet/api/microsoft.servicebus.messaging.netmessagingtransportsettings.batchflushinterval#Microsoft_ServiceBus_Messaging_NetMessagingTransportSettings_BatchFlushInterval
[EnableBatchedOperations]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablebatchedoperations#Microsoft_ServiceBus_Messaging_QueueDescription_EnableBatchedOperations
[QueueClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.queueclient.prefetchcount#Microsoft_ServiceBus_Messaging_QueueClient_PrefetchCount
[SubscriptionClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.subscriptionclient.prefetchcount#Microsoft_ServiceBus_Messaging_SubscriptionClient_PrefetchCount
[ForcePersistence]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage.forcepersistence#Microsoft_ServiceBus_Messaging_BrokeredMessage_ForcePersistence
[EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablepartitioning#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[Partitioned messaging entities]: service-bus-partitioning.md
[TopicDescription.EnableFilteringMessagesBeforePublishing]: /dotnet/api/microsoft.servicebus.messaging.topicdescription.enablefilteringmessagesbeforepublishing#Microsoft_ServiceBus_Messaging_TopicDescription_EnableFilteringMessagesBeforePublishing
