---
title: aaaAMQP 1.0 en operaciones de Bus de servicio de Azure basada en solicitud-respuesta | Documentos de Microsoft
description: Lista de operaciones de respuesta/solicitud de Microsoft Azure Service Bus
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a>El protocolo AMQP 1.0 de Microsoft Azure Service Bus: operaciones de respuesta/solicitud

En este tema define la lista de Hola de operaciones de Microsoft Azure Service Bus basado en solicitud/respuesta. Esta información se basa en el borrador de trabajo de hello AMQP administración versión 1.0.  
  
Encontrará una guía detallada de nivel de conexión de protocolo AMQP 1.0, que se explica cómo el Bus de servicio implementa y se basa en hello especificaciones técnicas de OASIS AMQP, hello [AMQP 1.0 en la Guía de protocolo de Service Bus de Azure y concentradores de eventos](service-bus-amqp-protocol-guide.md).  
  
## <a name="concepts"></a>Conceptos  
  
### <a name="entity-description"></a>Descripción de entidad  

Una descripción de la entidad hace referencia a un Bus de servicio de tooeither [clase QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription clase](/dotnet/api/microsoft.servicebus.messaging.topicdescription), o [clase Queuedescription](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) objeto.  
  
### <a name="brokered-message"></a>Mensaje asincrónico  

Representa un mensaje de Bus de servicio, que es el mensaje AMQP de tooan asignado. se define la asignación de Hola Hola [Guía de protocolo de AMQP de Bus de servicio](service-bus-amqp-protocol-guide.md).  
  
## <a name="attach-tooentity-management-node"></a>Conecte el nodo de administración de tooentity  

Todas las operaciones de hello descritas en este documento siguen un patrón de solicitud/respuesta, son tooan ámbito entidad y requieren asociar tooan nodo de administración de entidad.  
  
### <a name="create-link-for-sending-requests"></a>Creación de un vínculo para enviar solicitudes  

Crea un nodo de administración de vínculo toohello para enviar solicitudes.  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a>Creación de un vínculo para recibir respuestas  

Crea un vínculo para recibir respuestas de nodo de administración de Hola.  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a>Transferencia de un mensaje de solicitud  

Transfiere un mensaje de solicitud.  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a>Recepción de un mensaje de respuesta  

Recibe el mensaje de respuesta de Hola desde el vínculo de respuesta de Hola.  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
mensaje de respuesta de Hello es Hola siguiendo el formato:
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a>Dirección de entidades de Service Bus  

Las direcciones de las entidades de Service Bus deben tener el siguiente formato:  
  
|Tipo de entidad|Dirección|Ejemplo|  
|-----------------|-------------|-------------|  
|queue|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|topic|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|subscription|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a>Operaciones de mensajes  
  
### <a name="message-renew-lock"></a>Bloqueo de renovación de mensajes  

Extiende bloqueo Hola de un mensaje Hola de tiempo especificado en la descripción de la entidad de Hola.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
 cuerpo del mensaje de solicitud de Hello debe consistir en una sección de valor de amqp que contiene una asignación con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|Matriz de UUID|Sí|Toorenew de símbolos (tokens) de bloqueo de mensaje.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; en caso contrario, significa que se ha producido un error.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
cuerpo del mensaje de respuesta de Hello debe consistir en una sección de valor de amqp que contiene una asignación con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|expirations|Matriz de marca de tiempo|Sí|Mensaje de bloqueo token expiración correspondiente toohello solicitud bloqueo tokens nuevos.|  
  
### <a name="peek-message"></a>Inspección de mensajes  

Inspecciona los mensajes sin bloquearlos.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|long|Sí|Número de secuencia de qué peek toostart.|  
|`message-count`|int|Sí|Número máximo de mensajes toopeek.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; hay más mensajes.<br /><br /> 0xCC: sin contenido; no hay más mensajes.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
cuerpo del mensaje de respuesta de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|messages|Lista de asignaciones|Sí|Lista de mensajes en el que cada asignación representa un mensaje.|  
  
mapa de Hola que representa un mensaje debe contener Hola siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|Mensaje|Matriz de byte|Sí|Mensaje codificado con AMQP 1.0.|  
  
### <a name="schedule-message"></a>Programación de mensajes  

Programa mensajes.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|messages|Lista de asignaciones|Sí|Lista de mensajes en el que cada asignación representa un mensaje.|  
  
mapa de Hola que representa un mensaje debe contener Hola siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|message-id|string|Sí|`amqpMessage.Properties.MessageId` como cadena|  
|session-id|string|Sí|`amqpMessage.Properties.GroupId as string`|  
|partition-key|string|Sí|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|Mensaje|Matriz de byte|Sí|Mensaje codificado con AMQP 1.0.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; en caso contrario, significa que se ha producido un error.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
cuerpo del mensaje de respuesta de Hello debe constar de un **amqp valor** sección que contiene una asignación con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|Matriz de long|Sí|Número de secuencia de los mensajes programados. Número de secuencia es toocancel usado.|  
  
### <a name="cancel-scheduled-message"></a>Cancelación de mensajes programados  

Cancela mensajes programados.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|Matriz de long|Sí|Números de secuencia de mensajes programados toocancel.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; en caso contrario, significa que se ha producido un error.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
cuerpo del mensaje de respuesta de Hello debe constar de un **amqp valor** sección que contiene una asignación con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|Matriz de long|Sí|Número de secuencia de los mensajes programados. Número de secuencia es toocancel usado.|  
  
## <a name="session-operations"></a>Operaciones de sesiones  
  
### <a name="session-renew-lock"></a>Bloqueo de renovación de sesiones  

Extiende bloqueo Hola de un mensaje Hola de tiempo especificado en la descripción de la entidad de Hola.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Sí|Identificador de sesión.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; hay más mensajes.<br /><br /> 0xCC: sin contenido; no hay más mensajes.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
cuerpo del mensaje de respuesta de Hello debe constar de un **amqp valor** sección que contiene una asignación con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|expiration|timestamp|Sí|Nueva expiración.|  
  
### <a name="peek-session-message"></a>Inspección de mensajes de sesiones  

Inspecciona mensajes de sesiones sin bloquear.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|from-sequence-number|long|Sí|Número de secuencia de qué peek toostart.|  
|message-count|int|Sí|Número máximo de mensajes toopeek.|  
|session-id|string|Sí|Identificador de sesión.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; hay más mensajes.<br /><br /> 0xCC: sin contenido; no hay más mensajes.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
cuerpo del mensaje de respuesta de Hello debe constar de un **amqp valor** sección que contiene una asignación con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|messages|Lista de asignaciones|Sí|Lista de mensajes en el que cada asignación representa un mensaje.|  
  
 mapa de Hola que representa un mensaje debe contener Hola siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|Mensaje|Matriz de byte|Sí|Mensaje codificado con AMQP 1.0.|  
  
### <a name="set-session-state"></a>Establecimiento del estado de sesiones  

Conjuntos de Hola estado de una sesión.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Sí|Identificador de sesión.|  
|session-state|Matriz de bytes|Sí|Datos binarios opacos.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; en caso contrario, significa que se ha producido un error.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
### <a name="get-session-state"></a>Obtención del estado de sesiones  

Obtiene el estado de saludo de una sesión.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Sí|Identificador de sesión.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; en caso contrario, significa que se ha producido un error.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
cuerpo del mensaje de respuesta de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|session-state|Matriz de bytes|Sí|Datos binarios opacos.|  
  
### <a name="enumerate-sessions"></a>Enumeración de sesiones  

Enumera las sesiones de una entidad de mensajería.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|last-updated-time|timestamp|Sí|Filtrar tooinclude sesiones solo actualizadas después de un momento dado.|  
|skip|int|Sí|Omite un número de sesiones.|  
|top|int|Sí|Número máximo de sesiones.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; hay más mensajes.<br /><br /> 0xCC: sin contenido; no hay más mensajes.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
cuerpo del mensaje de respuesta de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|skip|int|Sí|Número de sesiones omitidas si el código de estado es 200.|  
|sessions-ids|Matriz de cadenas|Sí|Matriz de identificadores de sesiones si el código de estado es 200.|  
  
## <a name="rule-operations"></a>Operaciones de regla  
  
### <a name="add-rule"></a>Agregar regla  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|rule-name|string|Sí|Nombre de la regla, sin incluir los nombres de las suscripciones y los temas.|  
|rule-description|map|Sí|Descripción de la regla tal y como se especifica en la sección siguiente.|  
  
Hola **descripción de la regla** mapa debe incluir Hola siguiendo las entradas, donde **filtro sql** y **filtro de correlación** son mutuamente excluyentes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|sql-filter|map|Sí|`sql-filter`, como se especifica en la sección siguiente Hola.|  
|correlation-filter|map|Sí|`correlation-filter`, como se especifica en la sección siguiente Hola.|  
|sql-rule-action|map|Sí|`sql-rule-action`, como se especifica en la sección siguiente Hola.|  
  
mapa de filtro sql Hola debe incluir Hola siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|expresión|string|Sí|Expresión de filtro SQL.|  
  
Hola **filtro de correlación** mapa debe incluir al menos uno de hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|correlation-id|string|No||  
|message-id|string|No||  
|to|string|No||  
|reply-to|string|No||  
|label|string|No||  
|session-id|string|No||  
|reply-to-session-id|string|No||  
|content-type|string|No||  
|propiedades|map|No|Asigna tooService Bus [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).|  
  
Hola **acción de regla sql** mapa debe incluir Hola siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|expresión|string|Sí|Expresión de acción SQL.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; en caso contrario, significa que se ha producido un error.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
### <a name="remove-rule"></a>Eliminación de reglas  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|rule-name|string|Sí|Nombre de la regla, sin incluir los nombres de las suscripciones y los temas.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; en caso contrario, significa que se ha producido un error.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
## <a name="deferred-message-operations"></a>Operaciones de mensajes diferidos  
  
### <a name="receive-by-sequence-number"></a>Recepción por número de secuencia  

Recibe mensajes diferidos por número de secuencia.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|Matriz de long|Sí|Número de secuencias.|  
|receiver-settle-mode|ubyte|Sí|Modo de **liquidación de receptor** tal y como se especifica en AMQP Core 1.0.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; en caso contrario, significa que se ha producido un error.|  
|statusDescription|string|No|Descripción del estado de Hola.|  
  
cuerpo del mensaje de respuesta de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|messages|Lista de asignaciones|Sí|Lista de mensajes donde cada asignación representa un mensaje.|  
  
mapa de Hola que representa un mensaje debe contener Hola siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|lock-token|uuid|Sí|Token de bloqueo si el valor de `receiver-settle-mode` es 1.|  
|Mensaje|Matriz de byte|Sí|Mensaje codificado con AMQP 1.0.|  
  
### <a name="update-disposition-status"></a>Actualización del estado de disposición  

Actualiza el estado de disposición de Hola de mensajes aplazados.  
  
#### <a name="request"></a>Solicitud  

mensaje de solicitud de saludo debe incluir Hola aplicación propiedades siguientes:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|operación|string|Sí|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|uint|No|Tiempo de espera de funcionamiento del servidor en milisegundos.|  
  
cuerpo del mensaje de solicitud de Hello debe constar de un **amqp valor** sección que contiene un **mapa** con hello siguientes entradas:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|disposition-status|string|Sí|completed<br /><br /> abandoned<br /><br /> suspended|  
|lock-tokens|Matriz de UUID|Sí|El estado de disposición tooupdate los tokens de bloqueo del mensaje.|  
|deadletter-reason|string|No|Puede establecer si el estado de disposición se establece demasiado**suspendido**.|  
|deadletter-description|string|No|Puede establecer si el estado de disposición se establece demasiado**suspendido**.|  
|properties-to-modify|map|No|Lista de Bus de servicio asíncrona toomodify de propiedades de mensaje.|  
  
#### <a name="response"></a>Response  

mensaje de bienvenida de respuesta debe incluir Hola siguientes propiedades de la aplicación:  
  
|Clave|Tipo de valor|Obligatorio|Contenido del valor|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Sí|Código de respuesta HTTP [RFC2616]<br /><br /> 200: operación realizada correctamente; en caso contrario, significa que se ha producido un error.|  
|statusDescription|string|No|Descripción del estado de Hola.|

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de AMQP y Bus de servicio, visite Hola siguientes vínculos:

* [Información general sobre AMQP para Service Bus]
* [Compatibilidad de AMQP 1.0 con los temas y las colas con particiones de Service Bus]
* [AMQP de Service Bus para Windows Server]

[Información general sobre AMQP para Service Bus]: service-bus-amqp-overview.md
[Compatibilidad de AMQP 1.0 con los temas y las colas con particiones de Service Bus]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP de Service Bus para Windows Server]: https://msdn.microsoft.com/library/dn574799.asp