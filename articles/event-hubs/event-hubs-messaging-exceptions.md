---
title: "los concentradores de eventos de aaaAzure excepciones de mensajería | Documentos de Microsoft"
description: "Lista de excepciones de mensajería y acciones sugeridas de Centros de eventos de Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2c6273de-0106-47e5-b45d-59040e51f2c5
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 9c164e76612c26607219f08407f689aaab4050a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-messaging-exceptions"></a>Excepciones de mensajería de Centros de eventos
Este artículo enumeran algunas de las excepciones de hello generadas por hello Azure Service Bus las API, que incluyen los centros de eventos de mensajería. Esta referencia es toochange de asunto, por lo que se compruebe si hay actualizaciones.

## <a name="exception-categories"></a>Categorías de excepciones
las API de concentradores de eventos Hello generan excepciones que pueden se dividen en las siguientes categorías de hello, junto con la acción de hello asociado pueden tardar tootry toofix ellos.

1. Error de codificación de usuario: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). Acción general: pruebe toofix Hola código antes de continuar.
2. Error de instalación/configuración: [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Acción general: revise la configuración y cámbiela si es necesario.
3. Excepciones transitorias: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception), [Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). Acción general: vuelva a intentar la operación de Hola o notificar a los usuarios.
4. Otras excepciones: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](#timeoutexception), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception). Acción general: tipo de excepción específico toohello; Consulte la tabla toohello Hola pasos de la sección. 

## <a name="exception-types"></a>Tipos de excepciones
Hello tabla siguiente enumeran tipos de excepción de mensajería y sus causas y la acción sugerida de notas que puede tardar.

| **Tipo de excepción** | **Descripción/causa/ejemplos** | **Acción sugerida** | **Nota sobre el reintento automático o inmediato** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello servidor no respondió toohello solicitado operación dentro de hello especifica el tiempo, lo que se controla mediante [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). puede haber completado el servidor de Hola Hola solicitó la operación. Esto puede suceder debido a toonetwork u otros retrasos de infraestructura. |Compruebe el estado del sistema Hola para mantener la coherencia y vuelva a intentar si es necesario.<br /> Consulte [TimeoutException](#timeoutexception). |Reintento puede ser útil en algunos casos; Agregar toocode de lógica de reintento. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hola solicitado no se permite la operación de usuario dentro de servidor de Hola o servicio. Consulte el mensaje de excepción de Hola para obtener más información. Por ejemplo, [completar](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) genera esta excepción si se recibió el mensaje de bienvenida en [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modo. |Compruebe el código de hello y la documentación de Hola. Asegúrese de que Hola solicitó la operación es válida. |El reintento no le será de ayuda. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Es un intento realizado tooinvoke una operación en un objeto que ya se han cerrado, anulado o eliminado. En raras ocasiones, transacción ambiente Hola ya se ha eliminado. |Compruebe el código de hello y asegúrese de que no invoca las operaciones en un objeto desechado. |El reintento no le será de ayuda. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hola [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) objeto no pudo adquirir un token, Hola token no es válido u Hola token no contiene Hola notificaciones tooperform necesario Hola operación. |Asegúrese de que el proveedor de tokens de Hola se crea con los valores correctos de Hola. Comprobar la configuración de Hola de hello servicio de Control de acceso. |Reintento puede ser útil en algunos casos; Agregar toocode de lógica de reintento. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Método de toohello uno o más argumentos proporcionados no son válidos. Hello URI proporcionado demasiado[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crear](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) contiene segmentos de ruta de acceso. esquema URI de Hello proporcionado demasiado[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crear](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) no es válido. valor de la propiedad de Hello es mayor que 32KB. |Compruebe el código de llamada de Hola y asegúrese de Hola argumentos son correctos. |El reintento no le será de ayuda. |
| [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /> [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) |Entidad asociada con la operación de hello no existe o se ha eliminado. |Asegúrese de que existe la entidad de Hola. |El reintento no le será de ayuda. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Intente tooreceive un mensaje con un número de secuencia determinado. Este mensaje no se encuentra. |Asegúrese de que ya no se recibió el mensaje de Hola. Compruebe toosee de cola de mensajes fallidos de hello si mensajes de bienvenida se ha fallidos. |El reintento no le será de ayuda. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Cliente no es capaz de tooestablish un concentrador de conexión tooEvent. |Asegúrese de que nombre de host de hello proporcionado es correcto y host de hello es accesible. |El reintento podría resultar útil si hay problemas de conectividad intermitente. |
| [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) |Servicio no es capaz de tooprocess solicitud de hello en este momento. |Cliente puede esperar durante un período de tiempo y vuelva a intentar la operación de Hola. <br /> Consulte [ServerBusyException](#serverbusyexception). |El cliente puede volver a intentarlo tras un determinado intervalo de tiempo. Si el reintento genera otra excepción, compruebe el comportamiento de reintento de esa excepción. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Token de bloqueo asociado al mensaje de Hola ha expirado o no se encuentra el token de bloqueo de Hola. |Eliminar mensajes de bienvenida. |El reintento no le será de ayuda. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Se perdió el bloqueo asociado a esta sesión. | Anular hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) objeto. |El reintento no le será de ayuda. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Genérico mensajería excepción que se puede producir en hello casos siguientes: se realiza un intento de toocreate una [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) con un nombre o ruta de acceso que pertenece el tipo de entidad diferente tooa (por ejemplo, un tema). Es un intento de realizar un mensaje toosend supera los 256KB. Hola servidor o servicio detectó un error durante el procesamiento de solicitud de saludo. Consulte el mensaje de excepción de Hola para obtener más información. Por lo general, se trata de una excepción transitoria. |Comprobar código de hello y garantizar que sólo los objetos serializables se usan para el cuerpo del mensaje de Hola (o utilizar un serializador personalizado). Consulte la documentación de Hola para tipos de valor de hello admitida propiedades de Hola y solo los tipos de uso compatibles. Comprobar hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) propiedad. Si es **true**, puede volver a intentar la operación de Hola. |El comportamiento de reintento es indefinido y quizá no resulte útil. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Intente toocreate una entidad con un nombre que ya está en uso por otra entidad en ese espacio de nombres de servicio. |Eliminar entidad existente de Hola o elija un nombre diferente para hello entidad toobe creado. |El reintento no le será de ayuda. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hola entidad de mensajería ha alcanzado su tamaño máximo permitido. Esto puede ocurrir si ya se ha abierto el número máximo Hola de destinatarios (que es 5) en un nivel de grupo por el consumidor. |Crear espacio en la entidad de Hola recibir los mensajes de entidad de Hola o sus subcolas. <br /> Consulte [QuotaExceededException](#quotaexceededexception). |Reintento puede ser útil si los mensajes se han quitado en hello mientras tanto. |
|  | | | |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Intente tooaccept que una sesión con un identificador de sesión específico, pero la sesión de hello está bloqueada actualmente por otro cliente. |Asegúrese de que la sesión de Hola se desbloquea por otros clientes. |Reintento puede ser útil si se ha liberado la sesión de Hola Hola provisional. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Demasiadas operaciones forman parte de transacción de Hola. |Reducir el número de Hola de operaciones que forman parte de esta transacción. |El reintento no le será de ayuda. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Solicitud para realizar una operación en tiempo de ejecución en una entidad deshabilitada. |Activar la entidad de Hola. |Reintento puede ser útil si se ha activado la entidad de Hola Hola provisional. |
| [Microsoft.ServiceBus.Messaging.MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /> [Microsoft.Azure.EventHubs.MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | Una carga de mensaje supera el límite de hello 256K. Tenga en cuenta ese límite de 256k Hola tamaño total del mensaje de Hola, que puede incluir propiedades del sistema y cualquier sobrecarga. NET. |Reducir tamaño de Hola de carga de mensaje de Hola y vuelva a intentar la operación de Hola. |El reintento no le será de ayuda. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Hola transacción ambiente (*Transaction.Current*) no es válido. Puede se haya completado o anulado. La excepción interna puede proporcionar información adicional. | |El reintento no le será de ayuda. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Se intentó realizar una operación en una transacción que está en duda, o se realiza un intento de transacción de hello toocommit y se convierte en transacción hello en duda. |La aplicación debe controlar esta excepción (como un caso especial), tal y como transacción Hola puede ya se han confirmado. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indica que se ha superado una cuota de una entidad específica.

Esto puede ocurrir si ya se ha abierto el número máximo de Hola de destinatarios (5) en un nivel de grupo por el consumidor.

### <a name="event-hubs"></a>Centros de eventos
Centros de eventos tiene un límite de 20 grupos de consumidores por Centro de eventos. Si intentas toocreate más, recibirá un [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indica que una operación iniciada por el usuario está tardando más de tiempo de espera de operación de Hola. 

Los centros de eventos, tiempo de espera de Hola se especifica como parte de la cadena de conexión de hello, o a través de [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). mensaje de error de Hello propio puede variar, pero siempre contiene el valor de tiempo de espera de hello especificado para la operación actual de Hola. 

### <a name="common-causes"></a>Causas comunes
Hay dos causas comunes de este error: configuración incorrecta o un error de servicio transitorio.

1. **Una configuración incorrecta** tiempo de espera de operación de hello podría ser demasiado pequeño para la condición operativa Hola. valor predeterminado de Hello para el tiempo de espera de operación de hello en el SDK de cliente de hello es 60 segundos. Comprobar toosee si su código tiene el valor de hello establecido toosomething demasiado pequeño. Tenga en cuenta esa condición Hola de red de Hola y el uso de CPU puede afectar al tiempo de Hola que tarda un toocomplete operación en particular, por lo que no debe establecerse valor muy pequeño de tooa al tiempo de espera de operación de Hola.
2. **Error temporal del servicio** hello en ocasiones servicio de centros de eventos puede experimentar retrasos en el procesamiento de solicitudes, por ejemplo, durante los períodos de mucho tráfico. En tales casos, puede volver a intentar la operación después de un retraso hasta que se realiza correctamente la operación de Hola. Si hello misma operación sigue sin funcionar después de varios intentos, visite hello [sitio de estado de servicio de Azure](https://azure.microsoft.com/status/) toosee si hay cualquier interrupciones de servicio conocido.

## <a name="serverbusyexception"></a>ServerBusyException

Una excepción [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) o [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) indica que un servidor está sobrecargado. Hay dos códigos de error relevantes para esta excepción.

### <a name="error-code-50002"></a>Código de error 50002

Este error puede producirse por uno de estos dos motivos:

1. carga de Hello no se distribuye uniformemente a través de todas las particiones de hello centro de eventos y la limitación de unidad de una partición aciertos Hola rendimiento local.
    
    Solución: Revisión de la estrategia de distribución de particiones de Hola o intentar [EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) podría ayudar a solucionar.

2. espacio de nombres de los centros de eventos de Hello no tiene suficientes unidades de rendimiento (puede comprobar hello **métricas** hoja en la hoja de espacio de nombres de los centros de eventos en hello [portal de Azure](https://portal.azure.com) tooconfirm). Tenga en cuenta que el portal de hello muestra información de agregado (1 minuto), pero medimos el rendimiento en tiempo real: Hola por lo que es sólo una estimación.

    Solución: Aumenta el rendimiento de hello pueden ayudar unidades de espacio de nombres de Hola. Puede hacerlo en el portal de hello, Hola **escala** hoja de hoja de espacio de nombres de los centros de eventos de Hola.

### <a name="error-code-50001"></a>Código de error 50001

Este error se produce raras veces. Se produce al contenedor de Hola que se ejecuta el código para el espacio de nombres está bajo de CPU: carga de los centros de eventos de no más de unos segundos antes de hello equilibrador comienza.


## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de los centros de eventos información visitando Hola siguientes vínculos:

* [Información general de Event Hubs](event-hubs-what-is-event-hubs.md)
* [Creación de un centro de eventos](event-hubs-create.md)
* [Preguntas más frecuentes sobre Event Hubs](event-hubs-faq.md)
