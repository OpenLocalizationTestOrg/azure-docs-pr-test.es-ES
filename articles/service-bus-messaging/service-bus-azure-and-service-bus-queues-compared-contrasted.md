---
title: "colas de almacenamiento de aaaAzure y colas de Service Bus: comparación y diferencias | Documentos de Microsoft"
description: Analiza las diferencias y similitudes entre dos tipos de colas que se ofrecen en Azure.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: tysonn
ms.assetid: f07301dc-ca9b-465c-bd5b-a0f99bab606b
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: f8b915e73ea3c82d823a96bf23c8c9e24c96aa42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="storage-queues-and-service-bus-queues---compared-and-contrasted"></a>Colas de Storage y de Service Bus: comparación y diferencias
Este artículo analizan Hola diferencias y similitudes entre los tipos de hello dos de las colas que ofrece Microsoft Azure hoy: colas de almacenamiento y las colas de Bus de servicio. Con esta información, puede comparar y contrastar las tecnologías respectivas hello y ser capaz de toomake una decisión más informada acerca de qué solución que mejor satisfaga sus necesidades.

## <a name="introduction"></a>Introducción
Azure admite dos tipos de mecanismos de cola: **colas de Storage** y **colas de Service Bus**.

**Las colas de almacenamiento**, que forman parte del programa Hola a [almacenamiento de Azure](https://azure.microsoft.com/services/storage/) infraestructura, función una interfaz basada en REST GET/PUT/PEEK simple, que proporciona la mensajería confiable y persistente dentro y entre los servicios.

Las **colas de Service Bus** forman parte de una infraestructura de [mensajería de Azure](https://azure.microsoft.com/services/service-bus/) más amplia que admite la puesta en cola, así como la publicación/suscripción, y patrones de integración más avanzados. Para obtener más información acerca de las colas, temas/suscripciones del Bus de servicio, vea hello [información general del Bus de servicio](service-bus-messaging-overview.md).

Aunque ambas tecnologías de cola existen de manera simultánea, las colas de Storage se presentaron en primer lugar, como un mecanismo de almacenamiento de cola dedicado creado a partir de los servicios de Azure Storage. Las colas de Bus de servicio se compilan sobre hello más amplia de "mensajería" infraestructura diseñada toointegrate aplicaciones o componentes de aplicaciones que pueden abarcar varios protocolos de comunicación, contratos de datos, dominios de confianza o entornos de red.

## <a name="technology-selection-considerations"></a>Consideraciones de selección de tecnología
Las colas de almacenamiento y colas de Service Bus son implementaciones de message Queue Server servicio que se ofrece actualmente en Microsoft Azure de Hola. Cada uno tiene un conjunto de características ligeramente diferente, lo que significa que puede elegir una u Hola Sí o usar ambos, según las necesidades de Hola de su solución concreta o un problema empresarial/técnico que va a resolver.

Al determinar qué tecnología de puesta en cola ajusta a fin de Hola de una solución dada, los programadores y arquitectos de soluciones deben considerar las recomendaciones de Hola a continuación. Para obtener más información, vea Hola siguiente sección.

Como arquitecto o desarrollador de soluciones, **debe considerar el uso de colas de Storage** en los siguientes casos:

* La aplicación debe almacenar más de 80 GB de mensajes en una cola, donde los mensajes de Hola tienen una duración inferior a 7 días.
* La aplicación quiere tootrack progreso para procesar un mensaje dentro de la cola de Hola. Esto es útil si se bloquea un trabajador Hola que procesa un mensaje. Un trabajador posterior, a continuación, puede usar ese toocontinue información desde donde se quedó el trabajador anterior de Hola.
* Necesita registros del servidor de todas las transacciones de hello ejecutadas en las colas.

Como arquitecto o desarrollador de soluciones, **debe considerar el uso de colas de Service Bus** cuando:

* La solución debe ser capaz de tooreceive mensajes sin necesidad de cola de hello toopoll. Con el Bus de servicio, esto se puede lograr a través de hello mediante protocolos basados en TCP Hola que admite el Bus de servicio de operación de recepción de uso de sondeo largo Hola.
* La solución requiere Hola cola tooprovide un garantizada primero en-primero en salir (FIFO) entrega ordenada.
* Quiere una experiencia simétrica en Azure y en Windows Server (nube privada). Para obtener más información, vea [Service Bus para Windows Server](https://msdn.microsoft.com/library/dn282144.aspx).
* La solución debe ser capaz de toosupport detección automática de duplicados.
* Desea que sus mensajes de tooprocess de aplicación como secuencias paralelas de ejecución prolongada (mensajes están asociados a una secuencia utilizando hello [SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) propiedad de mensaje de Hola). En este modelo, cada nodo de hello consumiendo aplicación compite por secuencias, como toomessages opuestos. Cuando se asigna a un flujo tooa consumiendo nodo, nodo de hello puede examinar el estado de Hola de estado de la secuencia de aplicación Hola mediante transacciones.
* Su solución requiere un comportamiento transaccional y atomicidad al enviar o recibir varios mensajes desde una cola.
* característica de (TTL) de período de vida de Hola de carga de trabajo de hello específica de la aplicación puede superar el período de 7 días Hola.
* La aplicación administra mensajes que pueden superar los 64 KB, pero se enfoque no es probable que Hola límite de 256 KB.
* Se tratan con un requisito tooprovide un toohello de modelo de acceso basado en roles de las colas y diferentes derechos y permisos para los remitentes y receptores.
* El tamaño de la cola no aumentará a más de 80 GB.
* Desea toouse hello AMQP 1.0 basado en estándares Protocolo de mensajería. Para obtener más información sobre AMQP, vea [Introducción al AMQP de Service Bus](service-bus-amqp-overview.md).
* Puede idear una migración de punto a punto basados en cola tooa mensaje exchange patrón de comunicación que permite la integración sin problemas de receptores adicionales (suscriptores), cada uno de los cuales recibe copias independientes de algunos o todos cola de toohello envían los mensajes. Hola este último refiere a capacidad de publicación/suscripción toohello proporcionada por Bus de servicio de forma nativa.
* La solución de mensajería debe ser toosupport capaz de garantía de entrega de Hola "en-una vez máximo" sin necesidad de Hola para que los componentes de infraestructura adicionales de toobuild Hola.
* ¿Como toobe pueda toopublish y usar lotes de mensajes.

## <a name="comparing-storage-queues-and-service-bus-queues"></a>Comparación de las colas de Storage y las colas de Service Bus
tablas de Hola de hello las secciones siguientes proporcionan una agrupación lógica de características de cola y le permiten comparar, de una ojeada, capacidades de hello disponibles en las colas de almacenamiento y las colas de Bus de servicio.

## <a name="foundational-capabilities"></a>Capacidades fundamentales
En esta sección se compara algunas de hello capacidades fundamentales que poner en cola proporcionadas las colas de almacenamiento y las colas de Bus de servicio.

| Criterios de comparación | Colas de Storage | Colas de Service Bus |
| --- | --- | --- |
| Garantía de ordenación |**No** <br/><br>Para obtener más información, vea la nota primera Hola Hola sección "Información adicional".</br> |**Sí- Primero en caducar primero en salir (FIFO)**<br/><br>(mediante el uso de Hola de sesiones de mensajería) |
| Garantía de entrega |**Al menos una vez** |**Al menos una vez**<br/><br/>**Como máximo una vez** |
| Compatibilidad con la operación atómica |**No** |**Sí**<br/><br/> |
| Comportamiento de recepción |**Sin bloqueo**<br/><br/>(se completa inmediatamente si no se encuentra ningún mensaje nuevo) |**Bloqueo con/sin tiempo de espera**<br/><br/>(ofrece sondeo largo o hello ["Técnica de cometa"](http://go.microsoft.com/fwlink/?LinkId=613759))<br/><br/>**Sin bloqueo**<br/><br/>(a través de hello uso de .NET API solo administrado) |
| API de estilo de inserción |**No** |**Sí**<br/><br/>API de .NET de sesiones de [OnMessage](/dotnet/api/microsoft.servicebus.messaging.queueclient.onmessage#Microsoft_ServiceBus_Messaging_QueueClient_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__) y **OnMessage**. |
| Modo de recepción |**Ojear y alquilar** |**Ojear y bloquear**<br/><br/>**Recibir y eliminar** |
| Modo de acceso exclusivo |**Basado en concesión** |**Basado en bloqueo** |
| Duración de concesión/bloqueo |**30 segundos (valor predeterminado)**<br/><br/>**7 días (máximo)** (puede renovar o liberar una concesión de mensaje mediante hello [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API.) |**60 segundos (valor predeterminado)**<br/><br/>Puede renovar un bloqueo de mensaje utilizando hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API. |
| Precisión de concesión/bloqueo |**Nivel de mensaje**<br/><br/>(cada mensaje puede tener un valor de tiempo de espera diferentes, que, a continuación, puede actualizar según sea necesario al procesar el mensaje de Hola, mediante el uso de hello [UpdateMessage](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.updatemessage.aspx) API) |**Nivel de cola**<br/><br/>(cada cola tiene un tooall de precisión que se aplica de bloqueo de sus mensajes, pero puede renovar el bloqueo de hello utilizando hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) API.) |
| Recepción por lotes |**Sí**<br/><br/>(explícitamente especificando el número de mensajes al recuperar los mensajes, la tooa máximo de 32 mensajes) |**Sí**<br/><br/>(implícitamente habilita una propiedad de captura previa o explícitamente a través de hello uso de transacciones) |
| Envío por lotes |**No** |**Sí**<br/><br/>(mediante el uso de Hola de transacciones o de procesamiento por lotes de cliente) |

### <a name="additional-information"></a>Información adicional
* El sistema de los mensajes en las colas de Storage es normalmente primero en entrar, primero en salir; sin embargo, en ocasiones, pueden estar desordenados; por ejemplo, cuando expira la duración de tiempo de espera de visibilidad de un mensaje (por ejemplo, como resultado de una aplicación cliente que se bloquea durante el proceso). Cuando se agota el tiempo de espera de visibilidad de hello, mensajes de bienvenida deja de estar visible de nuevo en la cola de Hola para otro toodequeue de trabajo se. En ese momento, mensaje recientemente visible Hola puede colocarse en cola hello (toobe quitados nuevo) después de un mensaje que se encontraba originalmente en cola después de él.
* Hola garantiza patrón FIFO en las colas de Bus de servicio requiere el uso de Hola de sesiones de mensajería. Hola eventos que Hola aplicación se bloquea durante el procesamiento de un mensaje recibido en hello **consulta y bloqueo** Hola próxima vez, el modo de un receptor de la cola acepta una sesión de mensajería, se iniciará con el mensaje error de hello después de su período de vida (TTL) que expire.
* Las colas de almacenamiento son escenarios de mensajería estándar de toosupport diseñada, como desacoplamiento escalabilidad de tooincrease de componentes de la aplicación y la tolerancia a errores, nivelación de carga y crear flujos de trabajo de proceso.
* Las colas de Bus de servicio admiten hello *mínimo: una vez como* garantía de entrega. Además, Hola *más de una vez como* semántica puede ser compatibles con el estado de la aplicación de sesión estado toostore hello y mediante el uso de transacciones tooatomically recibir mensajes y actualizar el estado de sesión Hola.
* Las colas de Storage ofrecen un modelo de programación coherente y uniforme en las colas, tablas y blobs, tanto para desarrolladores como para los equipos de operaciones.
* Colas de Service Bus proporcionan compatibilidad para realizar transacciones locales en el contexto de Hola de una sola cola.
* Hola **recibir y eliminar** modo compatible con Bus de servicio proporciona Hola Hola de tooreduce capacidad mensajería número de operaciones (y el costo asociado) a cambio de una menor garantía de entrega.
* Las colas de almacenamiento proporcionan concesiones con concesiones de hello capacidad tooextend Hola para los mensajes. Esto permite a los trabajadores de hello concesiones cortas toomaintain en los mensajes. Por lo tanto, si se bloquea un trabajador, mensaje de saludo puede procesar rápidamente de nuevo por otro trabajador. Además, un trabajador puede ampliar la concesión de hello en un mensaje si necesita tooprocess tiempo de la concesión más Hola actual.
* Las colas de almacenamiento ofrecen visibilidad espera, ya que puede establecer en hello poner o quitar de la cola de un mensaje. Además, puede actualizar un mensaje con distintos valores de concesión en tiempo de ejecución y actualización distintos valores entre mensajes de Hola misma cola. Los tiempos de espera de bloqueo de Bus de servicio se definen en los metadatos de la cola de hello; Sin embargo, puede renovar el bloqueo de Hola por llamada hello [RenewLock](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.renewlock#Microsoft_ServiceBus_Messaging_BrokeredMessage_RenewLock) método.
* Hola de tiempo de espera máximo para un bloqueo de la operación de recepción en las colas de Bus de servicio es de 24 días. Sin embargo, los tiempos de espera basados en REST tienen un valor máximo de 55 segundos.
* Procesamiento por lotes de cliente proporcionadas por Bus de servicio permite una toobatch de cliente de cola varios mensajes en una sola operación de envío. El procesamiento por lotes solo está disponible para las operaciones de envío asincrónicas.
* Características como límite de 200 TB de Hola de colas de almacenamiento (más cuando se virtualizan las cuentas) y las colas ilimitadas convierten en una plataforma ideal para proveedores de SaaS.
* Las colas de Storage ofrecen un mecanismo de control de acceso delegado flexible y eficiente.

## <a name="advanced-capabilities"></a>Capacidades avanzadas
En esta sección se comparan algunas de las funcionalidades avanzadas ofrecidas por las colas de Storage y las colas de Service Bus.

| Criterios de comparación | Colas de Storage | Colas de Service Bus |
| --- | --- | --- |
| Entrega programada |**Sí** |**Sí** |
| Mensajes fallidos automáticos |**No** |**Sí** |
| Aumentar el valor de período de vida de cola |**Sí**<br/><br/>(a través de la actualización local de tiempo de espera de visibilidad) |**Sí**<br/><br/>(proporcionado mediante una función de API dedicada) |
| Compatibilidad con mensajes dudosos |**Sí** |**Sí** |
| Actualización local |**Sí** |**Sí** |
| Registro de transacciones del servidor |**Sí** |**No** |
| Métricas de almacenamiento |**Sí**<br/><br/>**Métricas de minuto**: ofrece métricas en tiempo real para disponibilidad, TPS, recuentos de llamadas de API, recuentos de errores y mucho más, todo en tiempo de real (agregado por minuto y notificado en unos minutos a partir de lo que acaba de ocurrir en producción. Para obtener más información, vea [Acerca de las métricas del análisis de almacenamiento](/rest/api/storageservices/fileservices/About-Storage-Analytics-Metrics). |**Sí**<br/><br/>(consultas masivas llamando a [GetQueues](/dotnet/api/microsoft.servicebus.namespacemanager.getqueues#Microsoft_ServiceBus_NamespaceManager_GetQueues)) |
| Administración de estados |**No** |**Sí**<br/><br/>[Microsoft.ServiceBus.Messaging.EntityStatus.Active](/dotnet/api/microsoft.servicebus.messaging.entitystatus.active), [Microsoft.ServiceBus.Messaging.EntityStatus.Disabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.disabled), [Microsoft.ServiceBus.Messaging.EntityStatus.SendDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.senddisabled), [Microsoft.ServiceBus.Messaging.EntityStatus.ReceiveDisabled](/dotnet/api/microsoft.servicebus.messaging.entitystatus.receivedisabled) |
| Reenvío automático de mensajes |**No** |**Sí** |
| Purgar la función de cola |**Sí** |**No** |
| Grupos de mensajes |**No** |**Sí**<br/><br/>(mediante el uso de Hola de sesiones de mensajería) |
| Estado de la aplicación por grupo de mensajes |**No** |**Sí** |
| Detección de duplicados |**No** |**Sí**<br/><br/>(configurable en el lado del remitente de hello) |
| Exploración de grupos de mensaje |**No** |**Sí** |
| Captura de sesiones de mensajes por id. |**No** |**Sí** |

### <a name="additional-information"></a>Información adicional
* Ambas tecnologías de cola permiten un toobe mensaje programado para entregarse en un momento posterior.
* Reenvío automático de cola permite que cientos de colas tooauto al día su mensajes tooa única cola, de qué aplicación receptora Hola consume el mensaje de bienvenida. Puede utilizar este mecanismo tooachieve seguridad, flujo de control y almacenamiento aislado entre cada publicador de mensajes.
* Las colas de Storage ofrecen compatibilidad para actualizar el contenido del mensaje. Puede utilizar esta funcionalidad para conservar información de estado y actualizaciones incrementales de progreso en el mensaje de bienvenida para que se pueda procesar de hello último punto de comprobación conocido, en lugar de hacerlo desde el principio. Con las colas de Bus de servicio, puede habilitar Hola mismo escenario mediante el uso de Hola de sesiones de mensajes. Las sesiones le permiten toosave y recuperar el estado de procesamiento de la aplicación hello (mediante el uso de [SetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.setstate#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_) y [GetState](/dotnet/api/microsoft.servicebus.messaging.messagesession.getstate#Microsoft_ServiceBus_Messaging_MessageSession_GetState)).
* [Cuellos mensajes fallidos](service-bus-dead-letter-queues.md), que es sólo compatible con las colas de Bus de servicio, pueden ser útil para aislar los mensajes que no se puede procesar correctamente por la aplicación receptora de Hola o cuando los mensajes no pueden llegar a su destino debido tooan expirado propiedad tiempo de vida de (TTL). Hola valor TTL especifica cuánto tiempo se conserva un mensaje en cola Hola. Con Bus de servicio, mensaje de saludo será tooa movida cola especial denominada $DeadLetterQueue cuando expira el período de vida de Hola.
* toofind mensajes "dudosos" en las colas de almacenamiento, al quitar una aplicación Hola de mensaje de la cola examina hello  **[DequeueCount](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueuemessage.dequeuecount.aspx)**  propiedad de mensaje de bienvenida. Si **DequeueCount** es mayor que un determinado umbral, la aplicación hello mueve tooan definida por la aplicación "mensajes fallidos" cola de mensajes de Hola.
* Las colas de almacenamiento le permiten tooobtain un registro detallado de todas las transacciones de Hola ejecutadas en cola de hello, así como agrega las métricas. Ambas opciones son útiles para depurar y entender cómo usa su aplicación las colas de Storage. También son útiles para optimizar rendimiento de la aplicación y reduce los costos de hello del uso de colas.
* concepto de Hola de "sesiones de mensajes" admitido por el Bus de servicio permite que los mensajes que pertenecen tooa cierto toobe grupo lógico asociado a un receptor específico, lo que a su vez crea una afinidad de sesión entre los mensajes y sus destinatarios respectivos. Puede habilitar esta funcionalidad avanzada en el Bus de servicio mediante configuración hello [SessionID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.sessionid#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) propiedad de un mensaje. Receptores, a continuación, pueden escuchar en un identificador de sesión específico y recibir mensajes que comparten Hola especificada el identificador de sesión.
* Hello funcionalidad de detección de duplicación que admiten las colas de Bus de servicio automáticamente quita mensajes duplicados enviados tooa cola o tema, basada en el valor de Hola de hello [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.messageid#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) propiedad.

## <a name="capacity-and-quotas"></a>Capacidad y cuotas
Esta sección comparan las colas de almacenamiento y las colas de Bus de servicio desde la perspectiva de Hola de [capacidad y las cuotas](service-bus-quotas.md) que podrían aplicarse.

| Criterios de comparación | Colas de Storage | Colas de Service Bus |
| --- | --- | --- |
| Tamaño de cola máximo |**500 TB**<br/><br/>(tooa limitado [único de la capacidad de la cuenta de almacenamiento](../storage/common/storage-introduction.md#queue-storage)) |**1 GB too80 GB**<br/><br/>(definido al crear una cola y [habilitar las particiones](service-bus-partitioning.md) – vea Hola sección "Información adicional") |
| Tamaño de mensaje máximo |**64 KB**<br/><br/>(48 K cuando se usa la codificación **Base64**)<br/><br/>Azure admite mensajes de gran tamaño mediante la combinación de las colas y blobs, momento en que puede poner en cola una too200GB para un elemento único. |**256 KB** o **1 MB**<br/><br/>(incluidos tanto el encabezado como el cuerpo, tamaño de encabezado máximo: 64 KB).<br/><br/>Depende de hello [nivel de servicio](service-bus-premium-messaging.md). |
| TTL de mensaje máximo |**7 días** |**`TimeSpan.Max`** |
| Número máximo de colas |**Sin límite** |**10.000**<br/><br/>(por espacio de nombres de servicio, se puede aumentar) |
| Número máximo de clientes simultáneos |**Sin límite** |**Sin límite**<br/><br/>(límite de 100 conexiones simultáneas solo aplica la comunicación basada en protocolos de tooTCP) |

### <a name="additional-information"></a>Información adicional
* Service Bus aplica límites de tamaño de cola. tamaño máximo de cola de Hola se especifica al crear cola de Hola y puede tener un valor entre 1 y 80 GB. Si se alcanza el valor de tamaño de cola de hello establecido durante la creación de cola de hello, se rechazarán los mensajes entrantes adicionales y llamar a código de hello recibirá una excepción. Para obtener más información sobre las cuotas en el Service Bus, vea [Cuotas de Service Bus](service-bus-quotas.md).
* Hola [nivel estándar](service-bus-premium-messaging.md), puede crear colas de Service Bus en tamaños de 1, 2, 3, 4 o 5 GB (valor predeterminado de hello es 1 GB). En el nivel de hello Premium, puede crear colas too80 GB de tamaño. En el estándar de capa, con las particiones habilitadas (que es el valor predeterminado de hello), Bus de servicio crea 16 particiones por cada GB que especifique. Por lo tanto, si crea una cola que es de 5 GB de tamaño, con 16 particiones tamaño máximo de cola de Hola se convierte en (5 * 16) = 80 GB. Puede ver el tamaño máximo de saludo de la cola o tema particionados examinando su entrada en hello [portal de Azure][Azure portal]. En el nivel Premium de hello, solo 2 particiones se crean por cola.
* Con las colas de almacenamiento, si hello contenido del mensaje de bienvenida no es XML seguro, se debe **Base64** codificado. Si se **Base64**-codificar los mensajes de bienvenida, carga de usuario de hello pueden funcionar too48 KB, en lugar de 64 KB.
* Con las colas de Service Bus, cada mensaje almacenado en una cola consta de dos partes: un encabezado y un cuerpo. tamaño total de Hola de mensaje de bienvenida no puede superar el tamaño admitido por nivel de servicio de hello máximo de mensaje de Hola.
* Cuando los clientes se comunican con colas de Bus de servicio a través del protocolo TCP de hello, número máximo de Hola de cola de Bus de servicio única de conexiones simultáneas tooa es too100 limitado. Este número se comparte entre remitentes y receptores. Si se alcanza esta cuota, se rechazarán las solicitudes posteriores de conexiones adicionales y llamar a código de hello recibirá una excepción. Este límite no se impone en los clientes se conectan mediante la API de REST de colas de toohello.
* Si necesita más de 10.000 colas en un único espacio de nombres de Bus de servicio, puede ponerse en contacto con el equipo de soporte técnico de Azure de Hola y solicitar un aumento. tooscale más allá de 10.000 colas con Bus de servicio, también puede crear espacios de nombres adicionales utilizando hello [portal de Azure][Azure portal].

## <a name="management-and-operations"></a>Administración y operaciones
Esta sección comparan las características de administración de hello proporcionadas por las colas de almacenamiento y las colas de Bus de servicio.

| Criterios de comparación | Colas de Storage | Colas de Service Bus |
| --- | --- | --- |
| Protocolo de administración |**REST sobre HTTP/HTTPS** |**REST sobre HTTPS** |
| Protocolo de tiempo de ejecución |**REST sobre HTTP/HTTPS** |**REST sobre HTTPS**<br/><br/>**AMQP 1.0 estándar (TCP con TLS)** |
| API de .NET |**Sí**<br/><br/>(API de cliente de Storage para .NET) |**Sí**<br/><br/>(API de Service Bus para .NET) |
| C++ nativo |**Sí** |**Sí** |
| API de Java |**Sí** |**Sí** |
| API de PHP |**Sí** |**Sí** |
| API de Node.js. |**Sí** |**Sí** |
| Compatibilidad con metadatos arbitrarios |**Sí** |**No** |
| Reglas de nomenclatura de cola |**La longitud de caracteres too63**<br/><br/>(las letras de un nombre de cola deben estar en minúscula). |**La longitud de caracteres too260**<br/><br/>(los nombres y las rutas de acceso de las colas no distinguen mayúsculas de minúsculas). |
| Función de obtención de la longitud de la cola |**Sí**<br/><br/>(Valor aproximado si los mensajes caducan más allá de hello TTL sin que se va a eliminar.) |**Sí**<br/><br/>(valor exacto en un momento dado). |
| Función de ojear |**Sí** |**Sí** |

### <a name="additional-information"></a>Información adicional
* Las colas de almacenamiento proporcionan compatibilidad con atributos arbitrarios que puede ser la descripción de la cola de toohello aplicado, en forma de Hola de pares nombre/valor.
* Ambas tecnologías de cola ofrecen un mensaje Hola capacidad toopeek sin necesidad de toolock TI, lo que puede resultar útil al implementar una herramienta de explorador/examinador de colas.
* Hola .NET de Bus de servicio asíncrona mensajería API Aproveche dúplex completo y las conexiones TCP para mejorar el rendimiento cuando se comparan tooREST a través de HTTP y que admiten el protocolo estándar de hello AMQP 1.0.
* Los nombres de colas de Storage pueden tener de 3 a 63 caracteres de longitud que pueden incluir letras minúsculas, números y guiones. Para obtener más información, vea [Nomenclatura de colas y metadatos](/rest/api/storageservices/fileservices/Naming-Queues-and-Metadata).
* Los nombres de cola de Bus de servicio pueden ser up too260 caracteres y tiene reglas de nomenclaturas menos restrictivas. Los nombres de cola de Service Bus pueden contener letras, números, puntos, guiones y caracteres de subrayado.

## <a name="authentication-and-authorization"></a>Autenticación y autorización
En esta sección se describe las características de autenticación y autorización de hello compatibles con colas de almacenamiento y las colas de Bus de servicio.

| Criterios de comparación | Colas de Storage | Colas de Service Bus |
| --- | --- | --- |
| Autenticación |**Clave simétrica** |**Clave simétrica** |
| Modelo de seguridad |Acceso delegado a través de tokens SAS. |SAS |
| Federación de proveedor de identidad: |**No** |**Sí** |

### <a name="additional-information"></a>Información adicional
* Cada tooeither de solicitud de hello tecnologías de puesta en cola debe autenticarse. No se admiten colas públicas con acceso anónimo. Con [SAS](service-bus-sas.md), puede abordar este escenario publicando un SAS de solo escritura, un SAS de solo lectura o incluso un SAS de acceso completo.
* Hello esquema de autenticación proporcionado por el almacenamiento de colas conlleva Hola usar una clave simétrica, que es un código de autenticación de mensajes basado en hash (HMAC), calculado con el algoritmo de hello SHA-256 y codificado como una **Base64** cadena. Para obtener más información sobre el protocolo respectivo hello, consulte [autenticación para servicios de almacenamiento de Azure hello](/rest/api/storageservices/fileservices/Authentication-for-the-Azure-Storage-Services). Las colas de Service Bus admiten un modelo similar mediante claves simétricas. Para obtener más información, vea [Autenticación con firma de acceso compartido con Service Bus](service-bus-sas.md).

## <a name="conclusion"></a>Conclusión
Por obtener una comprensión más profunda de las tecnologías de hello dos, tendrá que ser capaz de toomake toouse de tecnología de cola de una decisión más informada en el que y cuándo. Hola decisión sobre si las colas de almacenamiento de toouse o Bus de servicio pone en cola claramente depende de una serie de factores. Estos factores pueden dependen en gran medida de sus necesidades individuales de la aplicación y su arquitectura Hola. Si la aplicación ya usa las capacidades principales Hola de Microsoft Azure, puede ser preferible toochoose colas de almacenamiento, especialmente si necesita una comunicación básica y mensajería entre servicios o las colas de la necesidad de que pueden ser mayores que 80 GB de tamaño.

Dado que las colas de Service Bus ofrecen varias características avanzadas, como sesiones, transacciones, detección de duplicados, mensajes con problemas de entrega automáticos, y capacidades de publicación o suscripción duraderas, pueden ser la opción preferida si está creando una aplicación híbrida o si su aplicación necesita por otra parte estas características.

## <a name="next-steps"></a>Pasos siguientes
Hola siguientes artículos proporciona más instrucciones e información sobre el uso de colas de almacenamiento o colas de Service Bus.

* [Introducción a las colas de Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [¿Cómo tooUse Hola servicio de almacenamiento de cola](../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Procedimientos recomendados para mejorar el rendimiento mediante la mensajería asincrónica de Service Bus](service-bus-performance-improvements.md)
* [Introducción a las colas y los temas de Azure Service Bus (publicación en un blog)](http://www.code-magazine.com/article.aspx?quickid=1112041)
* [Hola tooService de guía del desarrollador Bus](http://www.cloudcasts.net/devguide/Default.aspx?id=11030)
* [Uso de hello servicio Queue Server en Azure](http://www.developerfusion.com/article/120197/using-the-queuing-service-in-windows-azure/)

[Azure portal]: https://portal.azure.com

