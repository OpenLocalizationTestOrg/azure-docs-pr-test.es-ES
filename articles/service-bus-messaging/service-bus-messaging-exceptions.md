---
title: "excepciones de mensajería de Bus de servicio de aaaAzure | Documentos de Microsoft"
description: "Lista de excepciones de mensajería del Bus de servicio y las acciones sugeridas."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3d8526fe-6e47-4119-9f3e-c56d916a98f9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: sethm
ms.openlocfilehash: 0a206b7bbc808c1190044c1dfd6ffd47b9d454fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-exceptions"></a>Excepciones de mensajería de Bus de servicio
Este artículo enumeran algunas excepciones generadas por Microsoft Azure Service Bus hello las API de mensajería. Esta referencia es toochange de asunto, por lo que se compruebe si hay actualizaciones.

## <a name="exception-categories"></a>Categorías de excepciones
APIs de mensajería Hello generan excepciones que pueden se dividen en las siguientes categorías de hello, junto con la acción de hello asociado pueden tardar tootry toofix ellos. Tenga en cuenta que el significado de Hola y causas de una excepción pueden variar según el tipo de saludo de la entidad de mensajería (colas o temas o centros de eventos):

1. Error de codificación de usuario ([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)). Acción general: pruebe toofix Hola código antes de continuar.
2. Error de instalación/configuración ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) y [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx)). Acción general: revise la configuración y cámbiela si es necesario.
3. Excepciones transitorias ([Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)). Acción general: vuelva a intentar la operación de Hola o notificar a los usuarios.
4. Otras excepciones ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)). Acción general: tipo de excepción específico toohello; Consulte la tabla toohello Hola pasos de la sección. 

## <a name="exception-types"></a>Tipos de excepciones
Hello tabla siguiente enumeran tipos de excepción de mensajería y sus causas y la acción sugerida de notas que puede tardar.

| **Tipo de excepción** | **Descripción/causa/ejemplos** | **Acción sugerida** | **Nota sobre el reintento automático o inmediato** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello servidor no respondió toohello solicitado operación dentro de hello especifica el tiempo que está controlado por [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). puede haber completado el servidor de Hola Hola solicitó la operación. Esto puede suceder debido a toonetwork u otros retrasos de infraestructura. |Compruebe el estado del sistema Hola para mantener la coherencia y vuelva a intentar si es necesario. Consulte [Excepciones de tiempo de espera](#timeoutexception). |Reintento puede ser útil en algunos casos; Agregar toocode de lógica de reintento. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hola solicitado no se permite la operación de usuario dentro de servidor de Hola o servicio. Consulte el mensaje de excepción de Hola para obtener más información. Por ejemplo, [completar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) generará esta excepción si se recibió el mensaje de bienvenida en [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modo. |Compruebe el código de hello y la documentación de Hola. Asegúrese de que Hola solicitó la operación es válida. |El reintento no le será de ayuda. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Es un intento realizado tooinvoke una operación en un objeto que ya se han cerrado, anulado o eliminado. En raras ocasiones, transacción ambiente Hola ya se ha eliminado. |Compruebe el código de hello y asegúrese de que no invoca las operaciones en un objeto desechado. |El reintento no le será de ayuda. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hola [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) objeto no pudo adquirir un token, Hola token no es válido u Hola token no contiene Hola notificaciones tooperform necesario Hola operación. |Asegúrese de que el proveedor de tokens de Hola se crea con los valores correctos de Hola. Comprobar la configuración de Hola de hello servicio de Control de acceso. |Reintento puede ser útil en algunos casos; Agregar toocode de lógica de reintento. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Método de toohello uno o más argumentos proporcionados no son válidos.<br /> Hello URI proporcionado demasiado[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crear](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) contiene segmentos de ruta de acceso.<br /> esquema URI de Hello proporcionado demasiado[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crear](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) no es válido. <br />valor de la propiedad de Hello es mayor que 32KB. |Compruebe el código de llamada de Hola y asegúrese de Hola argumentos son correctos. |El reintento no le será de ayuda. |
| [MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) |Entidad asociada con la operación de hello no existe o se ha eliminado. |Asegúrese de que existe la entidad de Hola. |El reintento no le será de ayuda. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Intente tooreceive un mensaje con un número de secuencia determinado. Este mensaje no se encuentra. |Asegúrese de que ya no se recibió el mensaje de Hola. Compruebe toosee de cola de mensajes fallidos de hello si mensajes de bienvenida se ha fallidos. |El reintento no le será de ayuda. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Cliente no es capaz de tooestablish un tooService conexión Bus. |Asegúrese de que nombre de host de hello proporcionado es correcto y host de hello es accesible. |El reintento podría resultar útil si hay problemas de conectividad intermitente. |
| [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Servicio no es capaz de tooprocess solicitud de hello en este momento. |Cliente puede esperar durante un período de tiempo y vuelva a intentar la operación de Hola. |El cliente puede volver a intentarlo tras un determinado intervalo de tiempo. Si el reintento genera otra excepción, compruebe el comportamiento de reintento de esa excepción. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Token de bloqueo asociado al mensaje de Hola ha expirado o no se encuentra el token de bloqueo de Hola. |Eliminar mensajes de bienvenida. |El reintento no le será de ayuda. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Se perdió el bloqueo asociado a esta sesión. |Anular hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) objeto. |El reintento no le será de ayuda. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Genérico mensajería excepción que se puede producir en hello casos siguientes:<br /> Se realiza un intento de toocreate una [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) con un nombre o ruta de acceso que pertenece el tipo de entidad diferente tooa (por ejemplo, un tema).<br />  Es un intento de realizar un mensaje toosend supera los 256KB. Hola servidor o servicio detectó un error durante el procesamiento de solicitud de saludo. Consulte el mensaje de excepción de Hola para obtener más información. Por lo general, se trata de una excepción transitoria. |Comprobar código de hello y garantizar que sólo los objetos serializables se usan para el cuerpo del mensaje de Hola (o utilizar un serializador personalizado). Consulte la documentación de Hola para tipos de valor de hello admitida propiedades de Hola y solo los tipos de uso compatibles. Comprobar hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) propiedad. Si es **true**, puede volver a intentar la operación de Hola. |El comportamiento de reintento es indefinido y quizá no resulte útil. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Intente toocreate una entidad con un nombre que ya está en uso por otra entidad en ese espacio de nombres de servicio. |Eliminar entidad existente de Hola o elija un nombre diferente para hello entidad toobe creado. |El reintento no le será de ayuda. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hola entidad de mensajería ha alcanzado su tamaño máximo permitido, o se superó el número máximo de hello del espacio de nombres de las conexiones tooa. |Crear espacio en la entidad de Hola recibir los mensajes de entidad de Hola o sus subcolas. Consulte [QuotaExceededException](#quotaexceededexception). |Reintento puede ser útil si los mensajes se han quitado en hello mientras tanto. |
| [RuleActionException](/dotnet/api/microsoft.servicebus.messaging.ruleactionexception) |Bus de servicio devuelve esta excepción si intenta toocreate una acción de regla no válida. Bus de servicio se asocia este mensaje de excepción tooa fallidos si se produce un error al procesar la acción de regla de Hola para ese mensaje. |Comprobar acción de regla de hello son correctos. |El reintento no le será de ayuda. |
| [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) |Bus de servicio devuelve esta excepción si intenta toocreate un filtro no válido. Bus de servicio se asocia este mensaje de excepción tooa fallidos si se produjo un error al procesar el filtro de Hola para ese mensaje. |Filtro de Hola de comprobación son correctos. |El reintento no le será de ayuda. |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Intente tooaccept que una sesión con un identificador de sesión específico, pero la sesión de hello está bloqueada actualmente por otro cliente. |Asegúrese de que la sesión de Hola se desbloquea por otros clientes. |Reintento puede ser útil si se ha liberado la sesión de Hola Hola provisional. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Demasiadas operaciones forman parte de transacción de Hola. |Reducir el número de Hola de operaciones que forman parte de esta transacción. |El reintento no le será de ayuda. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Solicitud para realizar una operación en tiempo de ejecución en una entidad deshabilitada. |Activar la entidad de Hola. |Reintento puede ser útil si se ha activado la entidad de Hola Hola provisional. |
| [NoMatchingSubscriptionException](/dotnet/api/microsoft.servicebus.messaging.nomatchingsubscriptionexception) |Bus de servicio devuelve esta excepción si se envía un tema de tooa de mensaje que se ha habilitado el filtrado previo y coincide con ninguno de los filtros de Hola. |Asegúrese de que coincida con al menos un filtro. |El reintento no le será de ayuda. |
| [MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Una carga de mensaje supera el límite de 256 KB de Hola. Tenga en cuenta que ese límite de 256 KB hello es el tamaño total del mensaje de Hola, que puede incluir propiedades del sistema y cualquier sobrecarga. NET. |Reducir tamaño de Hola de carga de mensaje de Hola y vuelva a intentar la operación de Hola. |El reintento no le será de ayuda. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Hola transacción ambiente (*Transaction.Current*) no es válido. Puede se haya completado o anulado. La excepción interna puede proporcionar información adicional. | |El reintento no le será de ayuda. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Se intentó realizar una operación en una transacción que está en duda, o se realiza un intento de transacción de hello toocommit y se convierte en transacción hello en duda. |La aplicación debe controlar esta excepción (como un caso especial), tal y como transacción Hola puede ya se han confirmado. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indica que se ha superado una cuota de una entidad específica.

### <a name="queues-and-topics"></a>Colas y temas
Para las colas y temas, a menudo es Hola tamaño de cola de Hola. propiedad de mensaje de error de Hello contendrá obtener más información, como en el siguiente ejemplo de Hola:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException
Message: hello maximum entity size has been reached or exceeded for Topic: ‘xxx-xxx-xxx’. 
    Size of entity in bytes:1073742326, Max entity size in bytes:
1073741824..TrackingId:xxxxxxxxxxxxxxxxxxxxxxxxxx, TimeStamp:3/15/2013 7:50:18 AM
```

mensaje de bienvenida de Estados de que ese tema Hola excedido su límite de tamaño, en este caso 1 GB (límite de tamaño predeterminado de hello). 

### <a name="namespaces"></a>Espacios de nombres

Para espacios de nombres, [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) puede indicar que una aplicación ha superado el número máximo de hello del espacio de nombres de las conexiones tooa. Por ejemplo:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException: ConnectionsQuotaExceeded for namespace xxx.
<tracking-id-guid>_G12 ---> 
System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: 
ConnectionsQuotaExceeded for namespace xxx.
```

#### <a name="common-causes"></a>Causas comunes
Hay dos causas comunes de este error: Hola cola de mensajes no enviados y receptores de mensajes no funciona.

1. **Cola de mensajes no enviados** un lector está fallando toocomplete mensajes y mensajes de saludo se devuelven toohello cola/tema cuando expira el bloqueo de Hola. Esto puede ocurrir si el lector de hello encuentra una excepción que le impida que realiza la llamada [BrokeredMessage.Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx). Después de que un mensaje ha sido leído 10 veces, mueve la cola de mensajes no enviados de toohello de forma predeterminada. Este comportamiento se controla mediante hello [QueueDescription.MaxDeliveryCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.maxdeliverycount.aspx) propiedad y no tiene un valor predeterminado de 10. Como los mensajes que se apilan en cola de mensajes no enviados de hello, que ocupen espacio.
   
    problema de hello tooresolve, mensajes de Hola completa y lectura de cola de mensajes no enviados de hello, como se haría desde cualquier otra cola. Hola [QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx) clase incluso contiene una [FormatDeadLetterPath](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.formatdeadletterpath.aspx) ruta de acceso de la cola de mensajes de Hola de método toohelp formato.
2. **Receptor detenido** Un receptor ha dejado de recibir mensajes de una cola o suscripción. Hola tooidentify manera es toolook en hello [QueueDescription.MessageCountDetails](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.messagecountdetails.aspx) propiedad, que muestra hello desglose completa de mensajes de saludo. Si hello [ActiveMessageCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagecountdetails.activemessagecount.aspx) propiedad es alto o creciente, a continuación, lo más rápido está escribirse no se leen los mensajes de saludo.

### <a name="event-hubs"></a>Centros de eventos
Centros de eventos tiene un límite de 20 grupos de consumidores por Centro de eventos. Si intentas toocreate más, recibirá un [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indica que una operación iniciada por el usuario está tardando más de tiempo de espera de operación de Hola. 

Se debe comprobar el valor de Hola de hello [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) propiedad, como se alcanza este límite también puede provocar un [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

### <a name="queues-and-topics"></a>Colas y temas
Para las colas y temas, se especifica el tiempo de espera de hello en hello [MessagingFactorySettings.OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout) propiedad, como parte de la cadena de conexión de hello, o a través de [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). mensaje de error de Hello propio puede variar, pero siempre contiene el valor de tiempo de espera de hello especificado para la operación actual de Hola. 

### <a name="event-hubs"></a>Centros de eventos
Los centros de eventos, tiempo de espera de Hola se especifica como parte de la cadena de conexión de hello, o a través de [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). mensaje de error de Hello propio puede variar, pero siempre contiene el valor de tiempo de espera de hello especificado para la operación actual de Hola. 

### <a name="common-causes"></a>Causas comunes
Hay dos causas comunes de este error: configuración incorrecta o un error de servicio transitorio.

1. **Una configuración incorrecta** tiempo de espera de operación de hello podría ser demasiado pequeño para la condición operativa Hola. valor predeterminado de Hello para el tiempo de espera de operación de hello en el SDK de cliente de hello es 60 segundos. Comprobar toosee si su código tiene el valor de hello establecido toosomething demasiado pequeño. Tenga en cuenta esa condición Hola de red de Hola y el uso de CPU puede afectar al tiempo de Hola que tarda un toocomplete operación en particular, por lo que no debe establecerse valor muy pequeño de tooa al tiempo de espera de operación de Hola.
2. **Error temporal del servicio** hello en ocasiones servicio de Bus de servicio puede experimentar retrasos en el procesamiento de solicitudes, por ejemplo, durante los períodos de mucho tráfico. En tales casos, puede volver a intentar la operación después de un retraso hasta que se realiza correctamente la operación de Hola. Si hello misma operación sigue sin funcionar después de varios intentos, visite hello [sitio de estado de servicio de Azure](https://azure.microsoft.com/status/) toosee si hay cualquier interrupciones de servicio conocido.

## <a name="next-steps"></a>Pasos siguientes

Para la referencia de API de .NET de Bus de servicio completa de hello, vea hello [referencia de la API de Azure .NET](/dotnet/api/overview/azure/servicebus).

más información acerca de toolearn [Bus de servicio](https://azure.microsoft.com/services/service-bus/), vea Hola temas siguientes.

* [Introducción a la mensajería del Bus de servicio](service-bus-messaging-overview.md)
* [Elementos fundamentales de Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Arquitectura del Bus de servicio](service-bus-architecture.md)

