---
title: "aaaAMQP 1.0 en la Guía de protocolo de Service Bus de Azure y concentradores de eventos | Documentos de Microsoft"
description: "Protocolo guía tooexpressions y una descripción de AMQP 1.0 en Azure Service Bus y concentradores de eventos"
services: service-bus-messaging,event-hubs
documentationcenter: .net
author: clemensv
manager: timlt
editor: 
ms.assetid: d2d3d540-8760-426a-ad10-d5128ce0ae24
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: clemensv;hillaryc;sethm
ms.openlocfilehash: 882ce0fc84af11d9f61bc95dc3e4db0b67b2b020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# Guía del protocolo AMQP 1.0 Azure Service Bus y Event Hubs

Hello Advanced Message Queueing protocolo 1.0 es un protocolo de tramas y transferencia estandarizado de forma asincrónica, segura y confiable transferir los mensajes entre dos entidades. Es Hola principal protocolo de mensajería de Bus de servicio de Azure y concentradores de eventos de Azure. Ambos servicios también admiten HTTPS. protocolo propietario de Hello SBMP que también se admite está desapareciendo en favor de AMQP.

AMQP 1.0 es resultado de hello de colaboración de industria que reúnen los proveedores de software intermedio, como Microsoft y Red Hat, con muchos usuarios de middleware de mensajería como JP Morgan Chase que representa el sector de servicios financieros Hola. Foro de normalización técnica Hola especificaciones de protocolo y la extensión AMQP de hello es OASIS y ha logrado aprobación formal como un estándar internacional como ISO/IEC 19494.

## Objetivos

En este artículo se resume los conceptos básicos de Hola de especificación de mensajería de hello AMQP 1.0 junto con un pequeño conjunto de especificaciones del borrador de extensión que actualmente está finalizando en Comité técnico de OASIS AMQP Hola brevemente y explica cómo Azure Service Bus implementa y se basa en estas especificaciones.

Hola objetivo es que cualquier desarrollador mediante cualquier pila de cliente de AMQP 1.0 existente en cualquier toointeract capaz de plataforma toobe con Bus de servicio de Azure a través de AMQP 1.0.

Las pilas de propósito general de AMQP 1.0 comunes, como Apache Proton o AMQP.NET Lite, ya implementan todos los gestos importantes de AMQP 1.0. A veces se ajustan los gestos básicos con una API de nivel superior; Proton de Apache incluso ofrece dos, Hola imperativo API de Messenger y Hola reactiva API Reactor.

En Hola después de discusión, asumimos que administración de Hola de control hello y vínculos de las transferencias de marco y control de flujo, sesiones y conexiones de AMQP se controlan mediante la pila de hello respectivos (por ejemplo, Apache Proton-C) y no requieren mucho si cualquier específica atención de los desarrolladores de aplicaciones. Suponemos abstractamente existencia Hola unos primitivos de API como tooconnect de capacidad de Hola y toocreate de alguna forma de *remitente* y *receptor* objetos de abstracción, que, a continuación, tienen alguna forma de `send()`y `receive()` operaciones, respectivamente.

Cuando se habla de las funcionalidades avanzadas de Azure Service Bus, como la consulta de mensajes o la administración de sesiones, estas características se explican en relación a AMQP, pero también como una pseudoimplementación superpuesta sobre esta abstracción de API supuesta.

## ¿Qué es AMQP?

AMQP es un protocolo de tramas y transferencia. Las tramas significa que proporciona una estructura para los flujos de datos binarios que fluyan en ambas direcciones de una conexión de red. estructura de Hello proporciona delineación para los distintos bloques de datos, denominado *fotogramas*, toobe intercambiados entre las partes de hello conectado. las capacidades de transferencia de Hello Asegúrese de que ambas partes en comunicación pueden establecer una visión compartida acerca de cuándo se transferirán los fotogramas, y cuando las transferencias se considerará completadas.

A diferencia de los versiones anteriormente expiradas borrador producidos por grupo de trabajo de AMQP de Hola que aún estén en uso por algunos agentes de mensajes, protocolo del grupo de trabajo de hello final y estandarizado de AMQP 1.0 no prescribir presencia de Hola de cualquier topología determinado o un agente de mensajes para las entidades dentro de un agente de mensajes.

Protocolo de Hello puede usarse para la comunicación simétrica de peer-to-peer, para la interacción con los agentes de mensajes que admiten las colas y las entidades de publicación/suscripción, como hace Azure Service Bus. También se puede utilizar para la interacción con la infraestructura de mensajería donde patrones de interacción de hello son diferentes de colas normales, como sucede Hola con concentradores de eventos de Azure. Un concentrador de eventos actúa como una cola cuando se envían eventos tooit, pero más actúa como un servicio de almacenamiento serie cuando se leen los eventos del mismo; algo similar a una unidad de cinta. cliente de Hello toma un desplazamiento en el flujo de datos disponibles de hello y, a continuación, se sirve a todos los eventos de ese desplazamiento toohello más reciente disponible.

Hola protocolo AMQP 1.0 es toobe diseñada extensible, habilitar más especificaciones tooenhance sus capacidades. especificaciones de extensión tres Hola descritas en este documento muestra cómo hacerlo. Para la comunicación a través de HTTPS/WebSockets infraestructura donde configurar puertos TCP AMQP nativo de hello puede ser difícil, una especificación de enlace define cómo toolayer AMQP a través de WebSockets. Para interactuar con la infraestructura de mensajería de hello en una solicitud/respuesta modo para fines de administración o la funcionalidad avanzada de tooprovide, especificación de administración de AMQP de hello define Hola requerido interacción básica primitivas. Integración del modelo de autorización federada, Hola especificación de seguridad basada en notificaciones AMQP define cómo tooassociate y renovar los tokens de autorización asociados con los vínculos.

## Escenarios básicos de AMQP

Esta sección explica el uso básico de Hola de AMQP 1.0 con Bus de servicio de Azure, que incluye la creación de conexiones, sesiones y vínculos y la transferencia de mensajes tooand de entidades de Service Bus como colas, temas y suscripciones.

Hello toolearn de origen autoritativo más acerca del funcionamiento de AMQP es la especificación de hello AMQP 1.0, pero especificación Hola se escribió la implementación de la Guía de tooprecisely y no el protocolo de hello tooteach. Esta sección se centra en la presentación de tanta terminología como sea necesario para describir el modo en que Service Bus usa AMQP 1.0. Para una tooAMQP más completa de introducción, así como obtener una explicación más amplia de AMQP 1.0, puede revisar [este curso vídeo][this video course].

### Conexiones y sesiones

Hola de llamadas AMQP comunicarse programas *contenedores*; esos contienen *nodos*, que comunica Hola entidades dentro de esos contenedores. Una cola puede ser uno de esos nodos. AMQP permite multiplexar, para que una sola conexión se puedan utilizar para muchas rutas de comunicación entre los nodos; Por ejemplo, un cliente de aplicación puede simultáneamente recibir desde una cola y cola de envío tooanother sobre Hola misma conexión de red.

![][1]

conexión de red de Hello, por tanto, está anclada en el contenedor de Hola. Se inicia por contenedor de hello en rol de cliente hello realizando un contenedor de tooa de conexión de socket TCP saliente en función de receptor de hello, que escucha y acepta conexiones TCP entrantes. Protocolo de enlace de conexión de Hello incluye negociar la versión de protocolo de hello, declarar ni negociar el uso de Hola de seguridad de nivel de transporte (TLS/SSL) y un protocolo de enlace de autenticación/autorización en el ámbito de la conexión de Hola que se basa en SASL.

Service Bus de Azure requiere el uso de Hola de TLS en todo momento. Admite las conexiones a través del puerto TCP 5671, según el cual primero se superpone con TLS antes de entrar en el protocolo de enlace de protocolo AMQP de Hola Hola conexión TCP y también admite conexiones a través del puerto TCP 5672 mediante el cual el servidor de hello ofrece inmediatamente una actualización obligatoria de conexión tooTLS utilizando el modelo de lo prescrito AMQP Hola. enlace de WebSockets de AMQP de Hello crea un túnel a través del puerto TCP 443, a continuación, tooAMQP equivalente 5671 conexiones.

Después de configurar la conexión de Hola y TLS, Bus de servicio ofrece dos opciones de mecanismo SASL:

* Sin formato SASL sirve principalmente para pasar un nombre de usuario y contraseña de servidor de tooa de credenciales. Service Bus no tiene cuentas, sino [reglas de seguridad de acceso compartido](service-bus-sas.md) con nombre, que confieren derechos y están asociadas a una clave. nombre de Hola de una regla se usa como nombre de usuario de Hola y clave de hello (como texto codificado con base64) se utiliza como contraseña de Hola. derechos de Hello asociados con hello elegido regla rigen las operaciones de hello permitidas en la conexión de Hola.
* SASL anónimo se utiliza para omitir la autorización de SASL al cliente hello desea toouse Hola seguridad basada en notificaciones (CBS) modelo se describe más adelante. Con esta opción, una conexión de cliente se puede establecer anónimamente durante un breve período durante qué Hola cliente sólo puede interactuar con el punto de conexión de hello CBS y se debe completar el protocolo de enlace de hello CBS.

Una vez establecida la conexión de transporte de hello, contenedores de hello cada declaran tamaño máximo de trama de hello son toohandle dispuesto y, después de un tiempo de inactividad unilateralmente dejarán desconectar el si no hay ninguna actividad en la conexión de Hola.

También declaran cuántos canales simultáneos se admiten. Un canal es una ruta de transferencia unidireccional, saliente, virtual sobre conexión Hola. Una sesión tiene un canal de cada ruta de comunicación de hello contenedores interconectados tooform un bidireccional.

Las sesiones tienen un modelo de control de flujo basado en la ventana; Cuando se crea una sesión, cada entidad declara el número de marcos es tooaccept dispuesto en su ventana de recepción. Tal y como se transfieren hello marcos de exchange de entidades, marcos de relleno que ventana y las transferencias de detendrán cuando se completa la ventana de Hola y hasta que la ventana hello restablece o expandirse con hello *flujo performative* (*performative*es hello AMQP término movimientos de nivel de protocolo intercambiados entre las partes de hello dos).

Este modelo basado en Windows es más o menos análoga toohello concepto TCP de control de flujo basado en Windows, pero en nivel de sesión de hello dentro de socket de Hola. Hello del protocolo existe concepto de lo que permite varias sesiones simultáneas para que el tráfico de alta prioridad podría prisa más allá de tráfico normal limitado, como en una calle express autopista.

En la actualidad, Azure Service Bus utiliza exactamente una sesión para cada conexión. Hola marco-tamaño máximo de Bus de servicio es 262.144 bytes (256 K bytes) para el Bus de servicio estándar y concentradores de eventos. Para Service Bus Premium es 1 048 576 (1 MB). Bus de servicio no impone las ventanas de limitación de nivel de sesión determinadas, pero restablece Hola ventana periódicamente como parte del control de flujo de nivel de vínculo (consulte [Hola próxima sección](#links)).

Las conexiones, los canales y las sesiones son efímeros. Si contrae la conexión subyacente hello, conexiones, deben restablecerse túnel TSL, contexto de autorización de SASL y sesiones.

### Vínculos

AMQP transfiere los mensajes a través de vínculos. Un vínculo es una ruta de comunicación creada sobre una sesión que permite transferir mensajes en una dirección; negociación de estado de transferencia de Hello está por encima de vínculo de Hola y bidireccionales entre partes de hello conectado.

![][2]

Se pueden crear vínculos por cualquier contenedor en cualquier momento y a través de una sesión existente, lo que hace diferente de muchos otros protocolos, como HTTP y MQTT, donde iniciación de Hola de las transferencias y la ruta de acceso de transferencia es un privilegio exclusivo de entidad de hello crea AMQP conexión de socket de Hola.

contenedor de vínculo de inicio de Hello pide Hola opuesto contenedor tooaccept un vínculo y elige un rol de remitente o receptor. Por lo tanto, el contenedor puede iniciar la creación unidireccional o rutas de acceso de comunicación bidireccional con hello este último se modelan como pares de vínculos.

Se asigna nombre a los vínculos y se asocian a los nodos. Como se indica en el principio de hello, nodos son Hola comunicarse entidades dentro de un contenedor.

En el Bus de servicio, un nodo es directamente equivalente tooa cola, un tema, una suscripción o una subcola de mensajes fallidos de una cola o suscripción. nombre de nodo de Hello usado en AMQP, por tanto, es nombre relativo del Hola de entidad de hello dentro del espacio de nombres de Bus de servicio de Hola. Si una cola se denomina **myqueue**, ese es también su nombre de nodo de AMQP. Una suscripción de tema sigue la convención de API HTTP de Hola por la que se va a ordenar en una colección de recursos "suscripciones" y por lo tanto, una suscripción **sub** o un tema **mytopic** tiene el nombre de nodo de hello AMQP **mytopic/suscripciones/sub**.

cliente que se conecta Hello también es toouse requiere un nombre de nodo local para crear vínculos; Bus de servicio no es prescriptivo acerca de los nombres de nodo y no los interpreta. Pilas de cliente de AMQP 1.0 generalmente utilizan un tooassure de esquema que estos nombres de nodo efímero son únicos en el ámbito de Hola de cliente de Hola.

### Transferencias

Una vez establecido un vínculo, los mensajes se pueden transferir a través de ese vínculo. En AMQP, se ejecuta una transferencia con un gesto de protocolo explícita (hello *transferencia* performative) que mueve un mensaje de remitente tooreceiver sobre un vínculo. Una transferencia está completa cuando lo es "liquidar", lo que significa que ambas partes han establecido una visión compartida del resultado de hello de esa transferencia.

![][3]

En el caso más simple de hello, remitente Hola puede elegir mensajes toosend "previamente liquidados", lo que significa que no está interesado en el resultado de hello cliente hello y receptor de hello no proporciona ningún tipo de información sobre el resultado de hello de operación de Hola. Este modo es compatible con Bus de servicio en el nivel de protocolo AMQP de hello, pero no se exponen en cualquiera de las API de cliente de Hola.

Hola caso normal es que los mensajes se envían sin liquidar y receptor hello, a continuación, indica la aceptación o rechazo mediante hello *disposition* performative. Rechazo se produce al receptor de hello no puede aceptar mensajes de bienvenida por cualquier motivo y mensaje de rechazo de saludo contiene información sobre el motivo hello, que es una estructura de error definida por AMQP. Si se rechazan los mensajes debido a errores de toointernal dentro de Bus de servicio, servicio de hello devuelve información adicional dentro de esa estructura que puede usarse para proporcionar diagnósticos personal de toosupport sugerencias Si archiva las solicitudes de soporte técnico. Aprenderá más detalles acerca de los errores más adelante.

Una forma especial de rechazo es hello *publicado* estado, lo que no indica que receptor hello tiene ninguna transferencia de toohello objeciones técnica, pero también ningún interés en estableciendo Hola transferencia. Que caso existe, por ejemplo, cuando un mensaje se entrega a tooa cliente de Bus de servicio y cliente hello elige demasiado "abandonar" mensaje de saludo porque no se puede realizar trabajo Hola resultantes de procesar el mensaje de Hola; entrega de mensajes de Hola sí mismo no es erróneo. Una variación de ese estado es hello *modificar* estado, lo que permite el mensaje de toohello de cambios a medida que se publique. En la actualidad, Service Bus no utiliza ese estado.

Hola especificación AMQP 1.0 define una disposición más estado llamado *recibido*, que le ayuda a recuperación de vínculo toohandle específicamente. Recuperación de vínculo permite reconstituir estado Hola de un vínculo y pendientes entregas sobre una nueva conexión y la sesión, cuando han perdido la conexión anterior de Hola y de sesión.

Bus de servicio no admite la recuperación de vínculo; Si pierde el cliente de Hola Hola conexión tooService Bus con un mensaje sin liquidar transferir pendiente, esa transferencia de mensaje se pierde y debe volver a conectarse, Restablecer vínculo hello y vuelva a intentar la transferencia de Hola cliente hello.

Por lo tanto, Service Bus y concentradores de eventos "al menos una vez" admiten a transferencias donde remitente Hola puede tener la seguridad de mensaje de bienvenida de tener han almacenado y aceptado, pero no admite "exactamente una vez" las transferencias en el nivel AMQP, donde el sistema de hello intentaría toorecover Hola Hola vínculo y continuar duplicación toonegotiate Hola entrega estado tooavoid de transferencia de mensajes de Hola.

envía toocompensate posibles duplicadas, Service Bus admite la detección de duplicados como una característica opcional en colas y temas. Registros de detección de duplicados Hola identificadores de mensaje de todos los mensajes entrantes durante un período de tiempo definido por el usuario, a continuación, en modo silencioso quita con que todos los mensajes enviados Hola identificadores de mensaje mismo durante esa misma ventana.

### Control de flujo

Además del modelo de control de flujo de nivel de sesión de toohello que ya se ha comentado, cada vínculo tiene su propio modelo de flujo de control. Control de flujo de nivel de sesión impide que se con toohandle demasiados marcos en una vez, el control de flujo de nivel de vínculo coloca aplicación Hola a cargo de la cantidad de mensajes desea toohandle desde un vínculo al contenedor de Hola.

![][4]

En los vínculos, las transferencias solo pueden ocurrir si hello remitente tiene suficiente *vincular crédito*. Crédito de vínculo es un conjunto de contadores consiste un receptor de hello usando hello *flujo* performative, que tiene un ámbito tooa vínculo. Cuando el remitente de Hola se asigna crédito de vínculo, intentos toouse ese crédito entregar los mensajes. Cada disminuye de entrega de mensaje Hola crédito restante de vínculo en 1. Cuando se agota el crédito de vínculo de hello, detenga las entregas.

Cuando está en el Bus de servicio en función de receptor de hello, proporciona al instante remitente Hola crédito suficiente vínculo, para que los mensajes pueden enviarse inmediatamente. Dado que se utiliza el crédito de vínculo, Bus de servicio envía ocasionalmente un *flujo* saldo de crédito de vínculo de toohello performative remitente tooupdate Hola.

En función de remitente de hello, Bus de servicio envía mensajes toouse cualquier crédito vínculo pendientes.

Una llamada de "recepción" en el nivel de API de Hola se traduce en un *flujo* performative enviarse tooService consume Bus cliente hello y Service Bus que primero del crédito por tomar Hola disponibles, desbloquear el mensaje de cola de hello, bloqueo, y transferirlo. Si no hay ningún mensaje disponible para la entrega, el crédito pendiente por cualquier vínculo establecidas con que permanece grabado en orden de llegada entidad en particular, y mensajes están bloqueados y transfieren en cuanto estén disponibles, toouse cualquier crédito pendiente.

se libera el bloqueo de Hello en un mensaje cuando se liquide transferencia hello en uno de los Estados de terminal de hello *acepta*, *rechazado*, o *publicado*. mensaje de bienvenida se quita de Bus de servicio cuando el estado de terminal de hello es *aceptan*. Se mantiene en el Bus de servicio y se entrega a toohello siguiente receptor cuando transferencia Hola alcanza cualquiera de hello otros Estados. Bus de servicio mueve automáticamente los mensajes de bienvenida en cola de mensajes fallidos de la entidad de hello cuando alcanza el número máximo de entregas de hello permitido para la entidad de hello debido toorepeated rechazos o versiones.

Aunque Hola API del Bus de servicio no exponer directamente dicha opción hoy en día, un cliente de protocolo AMQP de nivel inferior puede usar Hola vínculo crédito modelo tooturn Hola "estilo de extracción" interacción de emisión de una unidad de crédito para cada solicitud de recepción en un modelo de "inserción de estilo" mediante la emisión de un gran número de vínculo créditos y, a continuación, recibir mensajes cuando estén disponibles sin ninguna intervención. Se admite la inserción a través de hello [MessagingFactory.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PrefetchCount) o [MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount) valores de las propiedades. Cuando son distintos de cero, cliente AMQP de hello lo utiliza como crédito de vínculo de Hola.

En este contexto, es importante toounderstand que Hola reloj de expiración de Hola de bloqueo de hello en el mensaje de saludo dentro de la entidad de Hola se inicia cuando hello mensaje procede de entidad de hello, no cuando se colocó el mensaje de Hola en conexión Hola. Cada vez que el cliente de hello indica mensajes de preparación tooreceive mediante la emisión de crédito de vínculo, es mensajes activamente extracción de por lo tanto, toobe esperado a través de red de Hola y ser toohandle listo ellos. En caso contrario, puede haber expirado el bloqueo del mensaje de Hola antes incluso se entregue el mensaje de bienvenida. uso de Hola de control de flujo de crédito de vínculo directamente debe reflejar Hola preparación inmediata toodeal con receptor de mensajes disponible distribuidos toohello.

En resumen, hello las secciones siguientes se proporcionan una introducción esquemática de flujo de performative de Hola durante las interacciones de API diferentes. Cada sección describe una operación lógica diferente. Algunas de esas interacciones pueden ser "perezosas", lo que significa que solo pueden realizarse cuando se solicitan. Creación de un remitente del mensaje no puede causar una interacción de red hasta que el primer mensaje de Hola se envía o se solicita.

flechas de Hello en hello en la tabla siguiente muestran dirección de flujo performative Hola.

#### Creación del receptor del mensaje

| Cliente | SERVICE BUS |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source={entity name},<br/>target={client link id}<br/>) |Cliente adjunta tooentity como receptor |
| Respuestas de Bus de servicio adjuntar su extremo del vínculo de Hola |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={entity name},<br/>target={client link id}<br/>) |

#### Creación del remitente del mensaje

| Cliente | SERVICE BUS |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={client link id},<br/>target={entity name}<br/>) |Ninguna acción |
| Ninguna acción |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source={client link id},<br/>target={entity name}<br/>) |

#### Creación del remitente del mensaje (error)

| Cliente | SERVICE BUS |
| --- | --- |
| --> attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**sender**,<br/>source={client link id},<br/>target={entity name}<br/>) |Ninguna acción |
| Ninguna acción |<-- attach(<br/>name={link name},<br/>handle={numeric handle},<br/>role=**receiver**,<br/>source=null,<br/>target=null<br/>)<br/><br/><-- detach(<br/>handle={numeric handle},<br/>closed=**true**,<br/>error={error info}<br/>) |

#### Cierre del remitente/receptor del mensaje

| Cliente | SERVICE BUS |
| --- | --- |
| --> detach(<br/>handle={numeric handle},<br/>closed=**true**<br/>) |Ninguna acción |
| Ninguna acción |<-- detach(<br/>handle={numeric handle},<br/>closed=**true**<br/>) |

#### Envío (correcto)

| Cliente | SERVICE BUS |
| --- | --- |
| --> transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |Ninguna acción |
| Ninguna acción |<-- disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**accepted**<br/>) |

#### Envío (error)

| Cliente | SERVICE BUS |
| --- | --- |
| --> transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |Ninguna acción |
| Ninguna acción |<-- disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**rejected**(<br/>error={error info}<br/>)<br/>) |

#### Recepción

| Cliente | SERVICE BUS |
| --- | --- |
| --> flow(<br/>link-credit=1<br/>) |Ninguna acción |
| Ninguna acción |< transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=**receiver**,<br/>first={delivery id},<br/>last={delivery id},<br/>settled=**true**,<br/>state=**accepted**<br/>) |Ninguna acción |

#### Recepción de múltiples mensajes

| Cliente | SERVICE BUS |
| --- | --- |
| --> flow(<br/>link-credit=3<br/>) |Ninguna acción |
| Ninguna acción |< transfer(<br/>delivery-id={numeric handle},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| Ninguna acción |< transfer(<br/>delivery-id={numeric handle+1},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| Ninguna acción |< transfer(<br/>delivery-id={numeric handle+2},<br/>delivery-tag={binary handle},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=receiver,<br/>first={delivery id},<br/>last={delivery id+2},<br/>settled=**true**,<br/>state=**accepted**<br/>) |Ninguna acción |

### error de Hadoop

Hello las secciones siguientes explican las propiedades de las secciones de mensaje estándares de AMQP de hello utilizadas por Bus de servicio y cómo se asignan toohello conjunto de API de Service Bus.

#### encabezado

| Nombre del campo | Uso | Nombre de la API |
| --- | --- | --- |
| duradero |- |- |
| prioridad |- |- |
| ttl |Tiempo toolive para este mensaje |[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive) |
| first-acquirer |- |- |
| delivery-count |- |[DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) |

#### propiedades

| Nombre del campo | Uso | Nombre de la API |
| --- | --- | --- |
| message-id |Identificador de formato libre definido por la aplicación para este mensaje. Se usa para la detección de duplicados. |[MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) |
| user-id |Identificador del usuario definido por la aplicación; no interpretado por Service Bus. |No es accesible a través de hello API de Service Bus. |
| demasiado|Identificador del destino definido por la aplicación; no interpretado por Service Bus. |[To](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_To) |
| subject |Identificador del propósito de mensaje definido por la aplicación; no interpretado por Service Bus. |[Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) |
| respuesta demasiado|Indicador de la ruta de respuesta definido por la aplicación; no interpretado por Service Bus. |[ReplyTo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyTo) |
| correlation-id |Identificador de la correlación definido por la aplicación; no interpretado por Service Bus. |[CorrelationId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CorrelationId) |
| content-type |Indicador de tipo de contenido definido por la aplicación en el cuerpo de hello, no interpretado por Bus de servicio. |[ContentType](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType) |
| content-encoding |Definida por la aplicación codificación de contenido de indicador en el cuerpo de hello, no interpretado por Bus de servicio. |No es accesible a través de hello API de Service Bus. |
| absolute-expiry-time |Se declara en qué Hola instantánea absoluta expira el mensaje. Se ignora en la entrada (se observa el TTL de encabezado), es autoritativo en la salida. |[ExpiresAtUtc](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ExpiresAtUtc) |
| creation-time |Se declara en qué Hola de tiempo se creó el mensaje. No usado por Service Bus |No es accesible a través de hello API de Service Bus. |
| group-id |Identificador definido por la aplicación para un conjunto de mensajes relacionado. Se utiliza para sesiones de Service Bus. |[SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) |
| group-sequence |Contador de hello secuencia relativa número de identificación de mensaje de saludo dentro de una sesión. Omitido por Service Bus. |No es accesible a través de hello API de Service Bus. |
| reply-to-group-id |- |[ReplyToSessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyToSessionId) |

## Funcionalidades avanzadas de Service Bus

Esta sección describen las funciones avanzadas de Bus de servicio de Azure que se basan en borrador extensiones tooAMQP, actualmente que se desarrollan en hello Comité técnico de OASIS para AMQP. Bus de servicio implementa hello las versiones más recientes de estas borradores y adopta los cambios introducidos como los borradores alcance estado estándar.

> [!NOTE]
> Se admiten las operaciones avanzadas de mensajería de Service Bus mediante un modelo de solicitud y respuesta. detalles de Hola de estas operaciones se describen en el documento de hello [AMQP 1.0 en el Bus de servicio: operaciones de solicitud-respuesta-based](service-bus-amqp-request-response.md).
> 
> 

### Administración de AMQP

especificación de la administración de AMQP de Hello es hello primera de las extensiones de borrador de Hola se tratan aquí. Esta especificación define un conjunto de movimientos de protocolo superpuesta Hola protocolo AMQP que permiten a las interacciones de administración con hello infraestructura de mensajería a través de AMQP. especificación de Hello define operaciones genéricas como *crear*, *leer*, *actualizar*, y *eliminar* para administrar entidades dentro de un infraestructura de mensajería y un conjunto de operaciones de consulta.

Todos los movimientos requieren una interacción de solicitud/respuesta entre el cliente de Hola y la infraestructura de mensajería de hello y, por lo tanto, especificación de hello define cómo toomodel esa interacción patrón encima de AMQP: toohello de mensajería que conecta el cliente de Hola infraestructura, inicia una sesión y, a continuación, crea un par de vínculos. En un vínculo, cliente hello actúa como remitente y en hello otro actúa como receptor, lo que crea un par de vínculos que pueden actuar como un canal bidireccional.

| Operadores lógicos | Cliente | Service Bus |
| --- | --- | --- |
| Creación de una ruta de acceso de respuesta de solicitud |--> attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**sender**,<br/>source=**null**,<br/>target=”myentity/$management”<br/>) |Ninguna acción |
| Creación de una ruta de acceso de respuesta de solicitud |Ninguna acción |\<-- attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**receiver**,<br/>source=null,<br/>target=”myentity”<br/>) |
| Creación de una ruta de acceso de respuesta de solicitud |--> attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**receiver**,<br/>source=”myentity/$management”,<br/>target=”myclient$id”<br/>) | |
| Creación de una ruta de acceso de respuesta de solicitud |Ninguna acción |\<-- attach(<br/>name={*link name*},<br/>handle={*numeric handle*},<br/>role=**sender**,<br/>source=”myentity”,<br/>target=”myclient$id”<br/>) |

Implementación de solicitud/respuesta hello tiene ese par de vínculos en su lugar, es sencillo: una solicitud es un mensaje enviado tooan entidad dentro de la infraestructura de mensajería de Hola que comprenda este patrón. En ese mensaje de solicitud, Hola *responder a* campo hello *propiedades* sección se establece toohello *destino* identificador de vínculo de hello en qué respuesta de hello toodeliver. Hola control entidad procesa la solicitud de hello y, a continuación, entrega Hola respuesta sobre Hola vincular cuyo *destino* Hola indicado coincide con el identificador *responder a* identificador.

patrón de Hello obviamente requiere que contenedor de cliente de Hola y Hola client generado por el identificador de hello respuesta del destino son únicos en todos los clientes y, por motivos de seguridad, también difícil toopredict.

intercambios de mensajes de Hola usan para protocolo de administración de Hola y de todos los demás protocolos ese Hola uso mismo patrón se realiza en el nivel de aplicación Hola; no definen nuevos movimientos de nivel de protocolo AMQP. Eso es intencionado para que las aplicaciones puedan aprovechar inmediatamente estas extensiones con pilas de AMQP 1.0 compatibles.

Bus de servicio implementa actualmente cualquiera de las características básicas de Hola de especificación de la administración de hello, sino patrón de solicitud/respuesta Hola definido por la especificación de la administración de hello es fundamental para la característica de seguridad basada en notificaciones de Hola y para casi todos Hola avanzadas funcionalidades descritas en las secciones siguientes de Hola.

### Autorización basada en notificaciones

borrador de especificación de Hello AMQP autorización basada en notificaciones (CBS) se basa en el modelo de solicitud/respuesta de especificación de administración de Hola y describe un modelo generalizado de cómo toouse había federado tokens de seguridad con AMQP.

modelo de seguridad predeterminado de Hola de AMQP se describe en la introducción de Hola se basa en SASL y se integra con el protocolo de enlace de conexión de AMQP de Hola. Uso de SASL tiene la ventaja de Hola que proporciona un modelo extensible para que se han definido un conjunto de mecanismos de que se puede beneficiar cualquier protocolo que formalmente se basa en SASL. Entre estos mecanismos son "Simple" para la transferencia de nombres de usuario y contraseñas, seguridad de nivel de tooTLS de toobind "Externo", "Anónimo" tooexpress Hola a falta de autenticación/autorización explícita y una amplia variedad de mecanismos adicionales que permiten pasar las credenciales de autenticación o autorización o símbolos (tokens).

La integración de SASL de AMQP tiene dos inconvenientes:

* Todas las credenciales y tokens son conexión toohello con ámbito. Una infraestructura de mensajería puede tooprovide diferenciado de control de acceso en una base por cada entidad; Por ejemplo, lo que permite a portador Hola de un token toosend tooqueue A, pero no tooqueue B. Con el contexto de autorización de hello anclada en conexión hello, es toouse no es posible una conexión única y aún utiliza tokens de acceso diferentes y de cola A cola B.
* Normalmente, los tokens de acceso solo son válidos durante un tiempo limitado. Esta validez requiere tooperiodically adquirir tokens de usuario de Hola y proporciona un toorefuse de emisor del token de oportunidad toohello emitir un nuevo token si han cambiado los permisos de acceso del usuario de Hola. Las conexiones de AMQP pueden durar períodos muy largos. Hello SASL modelo solo proporciona una oportunidad tooset un token en tiempo de conexión, lo que significa que Hola o de infraestructura de mensajería tiene el cliente de hello toodisconnect cuando expira el token de Hola o necesita riesgo de hello tooaccept de lo que permite una comunicación continua con una cliente que tiene derechos de acceso se han revocado en hello provisional.

Hola especificación AMQP CBS, implementado por el Bus de servicio, permite una elegante solución para ambos de esos problemas: permite a un cliente tooassociate los tokens de acceso a cada nodo y tooupdate los tokens antes de expirar, todo ello sin interrumpir el flujo de mensajes de Hola.

CBS define un nodo de administración virtual denominado *$cbs*, toobe proporcionada por la infraestructura de mensajería de Hola. nodo de administración de Hello acepta los tokens en nombre de cualquier otro nodo en hello infraestructura de mensajería.

gestos de protocolo de Hello es un intercambio de solicitud/respuesta tal como se define mediante la especificación de la administración de Hola. Que significa Hola cliente establece un par de vínculos con hello *$cbs* nodo y, a continuación, pasa una solicitud en Hola vínculo de salida y, a continuación, espera respuesta hello en Hola vínculo entrante.

mensaje de solicitud de Hello tiene Hola aplicación propiedades siguientes:

| Clave | Opcional | Tipo de valor | Contenido del valor |
| --- | --- | --- | --- |
| operación |No |string |**put-token** |
| type |No |cadena |tipo de Hello del token de Hola se va a poner. |
| name |No |cadena |se aplica el token de Hola "público" toowhich Hola. |
| expiration |Sí |timestamp |hora de expiración de Hello del token de Hola. |

Hola *nombre* propiedad identifica la entidad de Hola a qué Hola símbolo (token) debe estar asociado. Bus de servicio de la cola de toohello de ruta de acceso de Hola o temas/suscripciones. Hola *tipo* propiedad identifica el tipo de token hello:

| Tipo de token | Descripción del token | Tipo de cuerpo | Notas |
| --- | --- | --- | --- |
| amqp:jwt |JSON Web Token (JWT) |Valor de AMQP (cadena) |No disponible todavía. |
| amqp:swt |Simple Web Token (SWT) |Valor de AMQP (cadena) |Solo se admite para los tokens SWT emitidos por AAD y ACS |
| servicebus.windows.net:sastoken |Token SAS de Service Bus |Valor de AMQP (cadena) |- |

Los tokens confieren derechos. Service Bus conoce tres derechos fundamentales: "Enviar" permite enviar, "Escuchar" permite recibir y "Administrar" permite manipular las entidades. Los tokens SWT emitidos por AAD/ACS incluyen explícitamente dichos derechos como notificaciones. Tokens de SAS del Bus de servicio hacen referencia toorules configurado en el espacio de nombres de Hola o entidad, y dichas reglas se configuran con derechos. Token de firma Hola con clave de hello asociada con dicha regla, por tanto, hace derechos respectivos de Hola Hola express símbolo (token). símbolo (token) de Hello asociado a una entidad con *put token* permite Hola conectado toointeract de cliente con la entidad de Hola por derechos de token de Hola. Un vínculo donde se realiza el cliente de hello en hello *remitente* rol requiere Hola "Envío" derecha; poner en hello *receptor* rol requiere el derecho de "Escuchar" Hola.

mensaje de respuesta Hello tiene siguientes de hello *propiedades de la aplicación* valores

| Clave | Opcional | Tipo de valor | Contenido del valor |
| --- | --- | --- | --- |
| status-code |No |int |Código de respuesta HTTP**[RFC2616]**. |
| status-description |Sí |cadena |Descripción del estado de Hola. |

Hola cliente puede llamar a *put token* repetidamente y de cualquier entidad de la infraestructura de mensajería de Hola. tokens de Hello son toohello con ámbito de cliente actual y anclado en la conexión actual de hello, servidor de hello significado quita los tokens retenidos al fallo de conexión de Hola.

implementación del Bus de servicio actual de Hello solo permite CBS junto con hello método SASL "Anónimo". Protocolo de enlace SASL toohello anterior siempre debe existir en una conexión de SSL/TLS.

Hola mecanismo ANÓNIMA, por tanto, debe ser compatibles con hello elegido a cliente de AMQP 1.0. Acceso anónimo decir Hola protocolo de enlace de conexión inicial, incluida la creación de sesión inicial Hola se produce sin saber quién está creando conexión Hola de Bus de servicio.

Una vez establecida la conexión de Hola y de sesión, adjuntar Hola vincula toohello *$cbs* nodo y enviar hello *put token* solicitud son Hola solo las operaciones permitidas. Un token válido debe establecerse correctamente mediante un *put token* solicitud para alguno de los nodos entidad dentro de 20 segundos después de que se ha establecido la conexión de hello, en caso contrario, conexión Hola unilateralmente quita Bus de servicio.

cliente de Hello es posteriormente responsable de mantener un seguimiento de la caducidad del testigo. Cuando caduca un token, Bus de servicio quita inmediatamente todos los vínculos en la entidad correspondiente de hello conexión toohello. tooprevent, Hola cliente puede reemplazar el token de hello para el nodo de Hola por una nueva en cualquier momento a través de hello virtual *$cbs* Hola de nodo de administración con mismo *put token* gestos y sin obtener Hola forma de carga de hello el tráfico que fluye en vínculos diferentes.

## Pasos siguientes

toolearn más información acerca de AMQP, visite Hola siguientes vínculos:

* [Información general sobre AMQP para Service Bus]
* [Compatibilidad de AMQP 1.0 con los temas y las colas con particiones de Service Bus]
* [AMQP de Service Bus para Windows Server]

[this video course]: https://www.youtube.com/playlist?list=PLmE4bZU0qx-wAP02i0I7PJWvDWoCytEjD
[1]: ./media/service-bus-amqp-protocol-guide/amqp1.png
[2]: ./media/service-bus-amqp-protocol-guide/amqp2.png
[3]: ./media/service-bus-amqp-protocol-guide/amqp3.png
[4]: ./media/service-bus-amqp-protocol-guide/amqp4.png

[Información general sobre AMQP para Service Bus]: service-bus-amqp-overview.md
[Compatibilidad de AMQP 1.0 con los temas y las colas con particiones de Service Bus]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP de Service Bus para Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
