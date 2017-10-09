---
title: "excepciones de retransmisión aaaAzure y cómo tooresolve ellos | Documentos de Microsoft"
description: "Obtener una lista de excepciones de retransmisión de Azure y las acciones sugeridas que puede seguir toohelp resolución."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5f9dd02c-cce0-43b3-8eb8-744f0c27f38c
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: de417c8e9e43407ef355fd44f6170cf2cdc46d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-exceptions"></a>Excepciones de Azure Relay

Este artículo enumeran algunas excepciones que pueden generarse por hello las API de retransmisión de Azure. Esta referencia es toochange de asunto, por lo que se compruebe si hay actualizaciones.

## <a name="exception-categories"></a>Categorías de excepciones

Hola retransmisión API generan excepciones que podrían pertenecer a Hola siguientes categorías. También se presentan acciones sugeridas que puede tardar toohelp resolver las excepciones de Hola.

*   **Error de codificación de usuario**: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). 

    **Acción general**: pruebe el código de hello de toofix antes de continuar.
*   **Error de instalación o configuración**: [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). 

    **Acción general**: revise la configuración. Si es necesario, cambiar la configuración de Hola.
*   **Excepciones transitorias**: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). 

    **Acción general**: vuelva a intentar la operación de Hola o notificar a los usuarios.
*   **Otras excepciones**: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx). 

    **Acción general**: tipo de excepción toohello específico. Vea la tabla de Hola Hola pasos de la sección. 

## <a name="exception-types"></a>Tipos de excepciones

Hello tabla siguiente enumeran los tipos de excepción mensajería y sus causas. También observa acciones sugeridas que puede seguir toohelp resolver las excepciones de Hola.

| **Tipo de excepción** | **Descripción** | **Acción sugerida** | **Nota sobre el reintento automático o inmediato** |
| --- | --- | --- | --- |
| [Tiempo de espera](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello servidor no respondió toohello solicitado operación dentro de hello especifica el tiempo, lo que se controla mediante [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout). Hola server podría Hola completado solicitaron la operación. Esto puede suceder debido a toonetwork u otros retrasos de infraestructura. |Compruebe el estado del sistema Hola para mantener la coherencia y, a continuación, intente de nuevo, si es necesario. Consulte [TimeoutException](#timeoutexception). |Reintento puede ser útil en algunos casos; Agregar toocode de lógica de reintento. |
| [Operación no válida](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hola solicitado no se permite la operación de usuario dentro de servidor de Hola o servicio. Consulte el mensaje de excepción de Hola para obtener más información. |Compruebe el código de hello y la documentación de Hola. Asegúrese de que ese Hola solicitó la operación es válida. |El reintento no le será de ayuda. |
| [Operación cancelada](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Es un intento realizado tooinvoke una operación en un objeto que tiene ya se ha cerrado, anulado o eliminado. En raras ocasiones, transacción ambiente Hola ya se ha eliminado. |Compruebe el código de hello y asegúrese de que no invoca las operaciones en un objeto desechado. |El reintento no le será de ayuda. |
| [Acceso no autorizado](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hola [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) objeto no pudo adquirir un token, Hola token no es válido u Hola token no contiene Hola notificaciones tooperform necesario Hola operación. |Asegúrese de que ese proveedor de tokens de Hola se crea con los valores correctos de Hola. Comprobar la configuración de Hola de hello servicio de Control de acceso. |Reintento puede ser útil en algunos casos; Agregar toocode de lógica de reintento. |
| [Excepción de argumento](https://msdn.microsoft.com/library/system.argumentexception.aspx),<br /> [Argumento Null](https://msdn.microsoft.com/library/system.argumentnullexception.aspx),<br />[Argumento fuera del intervalo](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Se ha producido uno o más de hello siguientes:<br />Método de toohello uno o más argumentos proporcionados no son válidos.<br /> Hello URI proporcionado demasiado[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crear](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) contiene uno o más segmentos de ruta de acceso.<br />esquema URI de Hello proporcionado demasiado[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) o [crear](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) no es válido. <br />valor de la propiedad de Hello es mayor que 32 KB. |Compruebe el código de llamada de Hola y asegúrese de Hola argumentos son correctos. |El reintento no le será de ayuda. |
| [Servidor ocupado](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Servicio no es capaz de tooprocess solicitud de hello en este momento. |cliente de Hello puede esperar durante un período de tiempo y después vuelva a intentar la operación de Hola. |cliente de Hello podría Reintentar después de un intervalo específico. Si un reintento da como resultado una excepción diferente, compruebe el comportamiento de reintento de Hola de esa excepción. |
| [Cuota superada](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hola entidad de mensajería ha alcanzado su tamaño máximo permitido. |Crear espacio en la entidad de Hola recibir los mensajes de entidad de Hola o sus subcolas. Consulte [QuotaExceededException](#quotaexceededexception). |Reintento puede ser útil si los mensajes se han quitado en hello mientras tanto. |
| [Tamaño de mensaje superado](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Una carga de mensaje supera el límite de 256 KB de Hola. Tenga en cuenta que ese límite de 256 KB hello es el tamaño total del mensaje de Hola. tamaño total del mensaje de Hola puede incluir propiedades del sistema y cualquier sobrecarga de .NET de Microsoft. |Reducir tamaño de Hola de carga de mensaje de Hola y vuelva a intentar la operación de Hola. |El reintento no le será de ayuda. |

## <a name="quotaexceededexception"></a>QuotaExceededException

[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indica que se ha superado una cuota de una entidad específica.

Para la retransmisión, esta excepción contiene hello [System.ServiceModel.QuotaExceededException](https://msdn.microsoft.com/library/system.servicemodel.quotaexceededexception.aspx), que indica el número máximo Hola de agentes de escucha se ha superado para este punto de conexión. Esto se indica en hello **MaximumListenersPerEndpoint** valor de mensaje de excepción de saludo.

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indica que una operación iniciada por el usuario está tardando más de tiempo de espera de operación de Hola. 

Comprobar valor Hola de hello [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) propiedad. Alcanzar este límite puede provocar una [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

Para Relay, puede que reciba excepciones de tiempo de espera al abrir por primera vez una conexión de remitente de la retransmisión. Hay dos causas comunes de esta excepción:

*   Hola [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) valor podría ser demasiado pequeño (incluso por una fracción de segundo).
* Un agente de escucha de retransmisión local podría ser que no responde (o puede surgir problemas de las reglas de firewall que prohíben a los agentes de escucha aceptando nuevas conexiones de cliente), hello y [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) valor es menor que unos 20 segundos.

Ejemplo:

```
'System.TimeoutException’: hello operation did not complete within hello allotted timeout of 00:00:10.
hello time allotted toothis operation may have been a portion of a longer timeout.
```

### <a name="common-causes"></a>Causas comunes
Hay dos causas comunes de este error:

*   **Configuración incorrecta**
    
    tiempo de espera de operación de Hello podría ser demasiado pequeño para la condición operativa Hola. valor predeterminado de Hello para el tiempo de espera de operación de hello en el SDK de cliente de hello es 60 segundos. Compruebe toosee si hello en el código se establece valor toosomething demasiado pequeño. Tenga en cuenta que condición de Hola y el uso de CPU de red de Hola puede afectar a Hola que tarda un toocomplete de operación. Es una buena idea no tooset Hola operación tiempo de espera tooa valor muy pequeño.
*   **Error temporal del servicio**

    En ocasiones, servicio de retransmisión de hello podría producirse retrasos en el procesamiento de solicitudes. Esto puede ocurrir, por ejemplo, durante los períodos de mucho tráfico. Si esto ocurre, vuelva a intentar la operación después de un retraso hasta que se realiza correctamente la operación de Hola. Si hello misma operación continúa toofail después de varios intentos, compruebe hello [sitio de estado de servicio de Azure](https://azure.microsoft.com/status/) toosee si hay interrupciones de servicio.

## <a name="next-steps"></a>Pasos siguientes
* [Preguntas frecuentes sobre Azure Relay](relay-faq.md)
* [Crear un espacio de nombres de Relay](relay-create-namespace-portal.md)
* [Introducción a Azure Relay y .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introducción a Azure Relay y Node](relay-hybrid-connections-node-get-started.md)

