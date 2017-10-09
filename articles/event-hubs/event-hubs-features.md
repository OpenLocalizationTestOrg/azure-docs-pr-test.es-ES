---
title: "información general de características de aaaAzure centros de eventos | Documentos de Microsoft"
description: "Introducción y detalles acerca de las características de Azure Event Hubs"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 8094e48abc8455ed725d4d5d3f9895f431441e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-features-overview"></a>Introducción a las características de Event Hubs

Azure Event Hubs es un servicio escalable de procesamiento de eventos que recopila y procesa grandes volúmenes de eventos y datos, con una baja latencia y una alta fiabilidad. Vea [¿qué es centros de eventos?](event-hubs-what-is-event-hubs.md) para una descripción general del servicio de Hola.

En este artículo se basa en información de Hola Hola [Introducción](event-hubs-what-is-event-hubs.md)y proporciona detalles de implementación y la técnica sobre características y componentes de los centros de eventos.

## <a name="event-publishers"></a>Publicadores de eventos

Cualquier entidad que envía el concentrador de eventos de tooan de datos es un productor de eventos, o *publicador de eventos*. Los publicadores de eventos pueden publicar eventos mediante HTTPS o AMQP 1.0. Los publicadores de eventos usar un tooidentify de token de firma de acceso compartido (SAS) por sí mismos tooan centro de eventos y pueden tener una identidad única o usar un token SAS común.

### <a name="publishing-an-event"></a>Publicación de un evento

Puede publicar un evento a través de AMQP 1.0 o HTTPS. Centros de eventos proporcionan [bibliotecas de cliente y las clases](event-hubs-dotnet-framework-api-overview.md) para la publicación de centro de eventos de tooan de eventos de clientes de. NET. Para otras plataformas y tiempos de ejecución, puede usar cualquier cliente de AMQP 1.0, como [Apache Qpid](http://qpid.apache.org/). Puede publicar eventos individualmente o por lotes. Una sola publicación (instancia de datos de eventos) tiene un límite de 256 KB, independientemente de si es un evento único o un lote. La publicación de eventos que superen este umbral producirá un error. Es una práctica recomendada para publicadores toobe consciente de las particiones en el centro de eventos de Hola y especifique tooonly una *clave de partición* (que se introdujo en la sección siguiente de hello), o su identidad a través de su token SAS.

Hola elección toouse AMQP o HTTPS es el escenario de uso de toohello específico. AMQP requiere el establecimiento de Hola de un socket bidireccional persistente en la seguridad de nivel de tootransport de suma (TLS) o SSL/TLS. AMQP tiene mayor será el costo de red al inicializar la sesión de hello, sin embargo, HTTPS requiere una sobrecarga de SSL adicional para cada solicitud. AMQP tiene un mayor rendimiento para los publicadores frecuentes.

![Centros de eventos](./media/event-hubs-features/partition_keys.png)

Centros de eventos garantizan que todos los eventos de uso compartido de un valor de clave de partición se entregan en orden y toohello misma partición. Si las claves de partición se usan con las directivas de publicador, Hola, a continuación, la identidad del publicador de Hola y debe coincidir con el valor de Hola de clave de partición de Hola. De lo contrario, se produce un error.

### <a name="publisher-policy"></a>Directiva del publicador

Los Centros de eventos permiten un control granular sobre los publicadores de eventos a través de las *directivas de publicador*. Las directivas de publicador son características de tiempo de ejecución diseñadas toofacilitate gran número de publicadores de eventos independientes. Con las directivas de publicador, cada publicador utiliza su propio identificador único al publicar el concentrador de eventos de tooan de eventos, mediante Hola después mecanismo:

```
//[my namespace].servicebus.windows.net/[event hub name]/publishers/[my publisher name]
```

No tiene nombres de las editoriales toocreate adelantado, pero deben coincidir con los token de SAS hello usa al publicar un evento, identidades de publicador independientes tooensure de orden. Al usar las directivas de publicador, Hola **PartitionKey** valor se establece el nombre del publicador toohello. toowork correctamente, estos valores deben coincidir.

## <a name="capture"></a>Capture

[Captura de los centros de eventos](event-hubs-capture-overview.md) permite tooautomatically Hola de captura de transmisión de datos en los centros de eventos y guárdelo tooyour elección de una cuenta de almacenamiento Blob o una cuenta de servicio de lago de datos de Azure. Puede habilitar la captura de hello portal de Azure y especificar un tamaño mínimo y la captura de Hola de tooperform de ventana de tiempo. Mediante la captura de los centros de eventos, especificar su propia cuenta de almacenamiento de blobs de Azure y el contenedor o la cuenta de servicio de lago de datos de Azure, que es usado toostore hello los datos capturados. Datos capturados se escriben en formato de Apache Avro Hola.

## <a name="partitions"></a>Particiones

Los concentradores de eventos proporciona el mensaje de transmisión por secuencias a través de un patrón de consumidor con particiones en la que cada consumidor lee únicamente un subconjunto específico, o partición, de transmisión de mensajes de Hola. Este patrón permite un escalado horizontal para el procesamiento de eventos y ofrece otras características centradas en los flujos que no están disponibles en las colas y los temas.

Una partición es una secuencia ordenada de eventos que se mantiene en un centro de eventos. Cuando llegan los eventos más recientes, se agregan toohello final de esta secuencia. Una partición puede considerarse como un "registro de confirmación".

![Centros de eventos](./media/event-hubs-features/partition.png)

Los concentradores de eventos conserva los datos durante un tiempo de retención configurado que se aplica a través de todas las particiones de concentrador de eventos de Hola. Los eventos expiran en función del tiempo; no se pueden eliminar explícitamente. Dado que las particiones son independientes y contienen sus propias secuencias de datos, a menudo crecen a velocidades diferentes.

![Centros de eventos](./media/event-hubs-features/multiple_partitions.png)

número de Hola de particiones se especifica durante la creación y debe estar entre 2 y 32. recuento de particiones de Hello no es modificable, por lo que al establecer el recuento de particiones, debe considerar escala a largo plazo. Las particiones son un mecanismo de organización de datos que está relacionada con toohello paralelismo descendente necesario en el consumo de aplicaciones. Hello número de particiones en un centro de eventos directamente relaciona toohello número de lectores simultáneos que espera toohave. Puede aumentar el número de Hola de particiones más allá de 32 por ponerse en contacto con el equipo de los centros de eventos de Hola.

Mientras que las particiones sean identificables y se pueden enviar toodirectly, no se recomienda enviar directamente tooa partición. En su lugar, puede utilizar construcciones de nivel superior que se introdujo en hello [publicador de eventos](#event-publishers) y [capacidad](#capacity) secciones. 

Las particiones se rellenan con una secuencia de datos de eventos que contiene el cuerpo de Hola de evento de hello, una bolsa de propiedades definidas por el usuario y metadatos, como su desplazamiento en la partición de Hola y su número de secuencia de flujo de Hola.

Para obtener más información acerca de las particiones y equilibrio de hello entre la disponibilidad y confiabilidad, consulte hello [Guía de programación de los centros de eventos](event-hubs-programming-guide.md#partition-key) hello y [disponibilidad y coherencia en los centros de eventos](event-hubs-availability-and-consistency.md) artículo .

### <a name="partition-key"></a>Clave de partición

Puede usar un [clave de partición](event-hubs-programming-guide.md#partition-key) toomap de datos de eventos entrantes en particiones específicas para el propósito de Hola de organización de datos. clave de partición de Hello es un valor proporcionado por el remitente que se pasa a un concentrador de eventos. Se procesa a través de una función hash estática, que crea la asignación de la partición de Hola. Si no especifica una clave de partición cuando se publica un evento, se usa una asignación de tipo round robin.

publicador de eventos de Hello solo es consciente de su clave de partición, se publican los eventos de Hola Hola no toowhich de la partición. Este desacoplamiento de clave y la partición aísla remitente hello de la necesidad de tooknow demasiado sobre el procesamiento de nivel inferior de Hola. Un usuario único identidad hace una buena clave de partición, pero otros atributos como geography también pueden ser usado toogroup o por dispositivo eventos relacionados en una sola partición.

## <a name="sas-tokens"></a>Tokens de SAS

Centros de eventos usan *firmas de acceso compartido*, que están disponibles en nivel de concentrador de espacio de nombres y eventos de Hola. Un token de SAS se genera a partir de una clave de SAS y es un hash SHA de una dirección URL, codificado en un formato concreto. Con nombre Hola de hello clave (directiva) y símbolo (token) de hello, centros de eventos puede volver a generar el hash de Hola y autenticar el remitente de Hola. Normalmente, los tokens de SAS para publicadores de eventos se crean solo con privilegios de **envío** en un centro de eventos concreto. Este mecanismo de dirección URL de token de SAS es la base de hello para la identificación de publicador introducida en la directiva de edición de Hola. Para más información acerca de cómo trabajar con SAS, consulte [Autenticación con firma de acceso compartido en Service Bus](../service-bus-messaging/service-bus-sas.md).

## <a name="event-consumers"></a>Consumidores de eventos

Cualquier entidad que lea datos de eventos de un centro de eventos es un *consumidor de eventos*. Conectan todos los consumidores de centros de eventos a través de la sesión de AMQP 1.0 de Hola y eventos se entregan a través de la sesión de hello cuando estén disponibles. Hola cliente no necesita toopoll para disponibilidad de los datos.

### <a name="consumer-groups"></a>Grupos de consumidores

se habilitó el mecanismo de publicación/suscripción de Hola de centros de eventos a través de *grupos de consumidores*. Un grupo de consumidores es una vista (estado, posición o desplazamiento) de un centro de eventos completo. Grupos de consumidores habilitar varias aplicaciones de consumo tooeach con sus propios desplazamientos y dispone de una vista independiente del flujo de eventos de Hola y flujo de hello tooread independientemente en su propio ritmo.

En un flujo de arquitectura de procesamiento, cada aplicación descendente equivale tooa grupo de consumidores. Si desea que el almacenamiento de término toolong de datos de eventos de toowrite, esa aplicación de sistema de escritura de almacenamiento es un grupo de consumidores. Otro grupo de consumidores independiente puede realizar el procesamiento de eventos complejos. Solo puede obtener acceso a las particiones a través de un grupo de consumidores. Como máximo, puede haber cinco lectores simultáneos en una partición por grupo de consumidores; pero **se recomienda que solo haya un receptor activo en una partición por grupo de consumidores**. Siempre hay un grupo de consumidores predeterminado en un centro de eventos y puede crear los grupos de consumidores de too20 para un concentrador de eventos de nivel estándar.

siguiente Hola es ejemplos de convención URI del grupo de consumidores de hello:

```http
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #1]
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #2]
```

Hello en la ilustración siguiente se muestra arquitectura de procesamiento de flujo de hello centros de eventos:

![Centros de eventos](./media/event-hubs-features/event_hubs_architecture.png)

### <a name="stream-offsets"></a>Desplazamientos de los flujos

Un *desplazamiento* es Hola posición de un evento dentro de una partición. Puede pensar en un desplazamiento como un cursor de lado cliente. desplazamiento Hello es un byte numeración de evento Hola. Este desplazamiento permite un toospecify de consumidor (lector) un punto en el flujo de eventos de Hola desde el que desean toobegin leer los eventos de eventos. Puede especificar el desplazamiento de hello como una marca de tiempo o como un valor de desplazamiento. Los consumidores son responsables de almacenar sus propios valores de desplazamiento fuera Hola servicio de centros de eventos. Dentro de una partición, cada evento incluye un desplazamiento.

![Centros de eventos](./media/event-hubs-features/partition_offset.png)

### <a name="checkpointing"></a>Puntos de control

*Puntos de control* es un proceso en el que los lectores marcan o confirman su posición dentro de la secuencia de eventos de una partición. Puntos de comprobación es responsabilidad de hello del consumidor de Hola y se produce de forma por partición dentro de un grupo de consumidores. Esta responsabilidad significa que para cada grupo de consumidores, cada lector de partición debe realizar un seguimiento de su posición actual en la secuencia de eventos de hello y puede informar a servicio de hello cuando considera que el flujo de datos de hello ha completado.

Si se desconecta un lector de una partición, cuando se vuelve a conectar comienza a leer en el punto de control de Hola que se envió anteriormente por hello último lector de esa partición en ese grupo de consumidores. Cuando se conecta el lector de hello, pasa esta ubicación de desplazamiento toohello evento concentrador toospecify hello en qué lectura toostart. De esta manera, puede usar tooboth Marcar eventos de puntos de comprobación como "completar" por aplicaciones descendentes y se produce la resistencia de tooprovide si una conmutación por error entre lectores que se ejecutan en equipos diferentes. Es posible tooreturn tooolder datos especificando un desplazamiento inferior desde este proceso de puntos de comprobación. Mediante este mecanismo, los puntos de comprobación permiten una resistencia a la conmutación por error y una reproducción del flujo de eventos.

### <a name="common-consumer-tasks"></a>Tareas comunes del consumidor

Todos los consumidores de Event Hubs se conectan a través de una sesión de AMQP 1.0, un canal de comunicación bidireccional con estado. Cada partición tiene una sesión de AMQP 1.0 que facilita el transporte de Hola de eventos separados por partición.

#### <a name="connect-tooa-partition"></a>Conectar tooa partición

Cuando se conecte toopartitions, es común toouse práctica una concesión de particiones de mecanismo toocoordinate lector conexiones toospecific. De esta manera, es posible que cada partición de un consumidor grupo toohave solo un lector activo. Puntos de comprobación, leasing y administrar los lectores se simplifican mediante el uso de hello [EventProcessorHost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) clase para clientes de. NET. Hola Host procesador de eventos es un agente de consumidor inteligente.

#### <a name="read-events"></a>Lectura de eventos

Después de abrir una sesión de AMQP 1.0 y el vínculo de una partición específica, los eventos se entregan a cliente toohello AMQP 1.0 por hello servicio de centros de eventos. Este mecanismo de entrega permite un mayor procesamiento y una menor latencia que los mecanismos basados en extracción como HTTP GET. Tal y como se envían eventos de cliente de toohello, cada instancia de datos de evento contiene metadatos importantes como el número de secuencia y desplazamiento de Hola que son puntos de comprobación toofacilitate usado en la secuencia de eventos de Hola.

Datos de evento:
* Offset
* Número de secuencia
* Cuerpo
* Propiedades de usuario
* Propiedades del sistema

Es el desplazamiento de responsabilidad toomanage Hola.

## <a name="capacity"></a>Capacity

Los concentradores de eventos tiene una arquitectura paralela altamente escalable y hay varios tooconsider de factores clave al calcular el tamaño y escala.

### <a name="throughput-units"></a>Unidades de procesamiento

capacidad de rendimiento de Hola de centros de eventos se controla mediante *unidades de rendimiento*. Las unidades de procesamiento son unidades de capacidad adquiridas previamente. Una unidad de rendimiento única incluye Hola después de capacidad:

* Entrada: una too1 MB por segundo o 1.000 eventos por segundo (lo que ocurra primero)
* Salida: una too2 MB por segundo

Más allá de la capacidad de Hola de hello adquirida unidades de rendimiento, la entrada está limitada y un [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) se devuelve. Salida no produce excepciones de limitación, pero es toohello estando limitada capacidad de hello adquirida unidades de rendimiento. Si recibe excepciones de tasas de publicación o esperan toosee una salida más elevada, ser seguro toocheck cuántas unidades de rendimiento ha adquirido para el espacio de nombres de Hola. Puede administrar unidades de rendimiento en hello **escala** hoja de espacios de nombres de Hola Hola [portal de Azure](https://portal.azure.com). También puede administrar unidades de rendimiento mediante programación con hello [API de concentradores de eventos](event-hubs-api-overview.md).

Las unidades de procesamiento se facturan por hora y se adquieren previamente. Cuando se adquieren, las unidades de procesamiento se facturan durante un período mínimo de una hora. Seguridad too20 unidades de rendimiento se pueden adquirir para un espacio de nombres de los centros de eventos y se comparten entre todos los concentradores de eventos en el espacio de nombres de Hola.

Pueden adquirir más unidades de rendimiento en bloques de 20 unidades de rendimiento de too100, póngase en contacto con soporte técnico de Azure. A partir de ahí, también puede adquirir bloques de 100 unidades de procesamiento.

Se recomienda que un equilibrio entre rendimiento particiones y unidades tooachieve escala óptima. Una sola partición tiene una escala máxima de una unidad de procesamiento. Hello número de unidades de rendimiento debe ser menor o igual toohello número de particiones en un centro de eventos.

Para obtener información detallada sobre los precios de Event Hubs, consulte [Precios de Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los centros de eventos, visite Hola siguientes vínculos:

* Empezar a trabajar con un [tutorial de Event Hubs][Event Hubs tutorial]
* [Guía de programación de Event Hubs](event-hubs-programming-guide.md)
* [Disponibilidad y coherencia en Event Hubs](event-hubs-availability-and-consistency.md)
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)
* [Ejemplos de Event Hubs][]

[Event Hubs tutorial]: event-hubs-dotnet-standard-getstarted-send.md
[Ejemplos de Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
