---
title: "aaaAzure autenticación y autorización de retransmisión | Documentos de Microsoft"
description: "Introducción a la autenticación de Firma de acceso compartido (SAS) en Azure Relay"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a>Autenticación y autorización en Azure Relay
Las aplicaciones pueden autenticarse tooAzure de retransmisión mediante la autenticación de firma de acceso compartido (SAS). Similar demasiado[Bus de servicio de mensajería](../service-bus-messaging/service-bus-authentication-and-authorization.md), autenticación de SAS permite que aplicaciones tooauthenticate toohello servicio de retransmisión de Azure mediante una clave de acceso configurada en el espacio de nombres de hello retransmisión. A continuación, puede usar esta clave toogenerate un token de firma de acceso compartido que los clientes pueden usar el servicio de retransmisión de tooauthenticate toohello.

## <a name="shared-access-signature-authentication"></a>Autenticación con Firma de acceso compartido
[Autenticación de SAS](../service-bus-messaging/service-bus-sas.md) permite toogrant un recursos de retransmisión de tooAzure de acceso de usuario con derechos específicos. Autenticación de SAS implica la configuración de Hola de una clave criptográfica con derechos asociados en un recurso. Los clientes, a continuación, pueden obtener acceso a recursos de toothat presentando un token SAS, que consta del URI que se obtiene acceso de recurso de hello y una fecha de expiración firmada con hello configurado clave.

Puede configurar claves para SAS en un espacio de nombres de Relay. A diferencia de la mensajería de Service Bus, [Conexiones híbridas de Relay](relay-hybrid-connections-protocol.md) admite remitentes no autorizados o anónimos. Puede habilitar el acceso anónimo para la entidad de hello al crearlo, como se muestra en hello después de la pantalla desde el portal de hello:

![][0]

toouse SAS, puede configurar un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objeto en un espacio de nombres de retransmisión que consta de hello siguiente:

* *KeyName* que identifica la regla de Hola.
* *PrimaryKey* es toosign y validar tokens SAS usa una clave criptográfica.
* *SecondaryKey* es toosign y validar tokens SAS usa una clave criptográfica.
* *Derechos de* que representa colección de Hola de escucha, envío y administración de derechos concedidos.

Reglas de autorización configuradas en el nivel de espacio de nombres de hello pueden conceder acceso tooall conexiones de retransmisión en un espacio de nombres para los clientes con tokens firmados con la clave correspondiente Hola. Seguridad too12 tales reglas de autorización pueden configurarse en un espacio de nombres de retransmisión. De forma predeterminada, se configura un objeto [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) con todos los derechos para cada espacio de nombres cuando se aprovisiona por primera vez.

tooaccess una entidad, el cliente de hello requiere un token SAS generado con un determinado [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). token de SAS de Hola se genera utilizando Hola se notifica el HMAC-SHA256 de una cadena de recurso que consta del recurso de hello acceso URI toowhich y una fecha de expiración con una clave criptográfica asociada la regla de autorización de Hola.

Compatibilidad con la autenticación SAS para la retransmisión de Azure se incluye en versiones de hello Azure SDK para .NET 2.0 y posteriores. SAS incluye compatibilidad con un objeto [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Todas las API que aceptan una cadena de conexión como parámetro incluyen compatibilidad con cadenas de conexión SAS.

## <a name="next-steps"></a>Pasos siguientes
- Para obtener más información sobre SAS, siga consultando [Autenticación en Service Bus con Firmas de acceso compartido](../service-bus-messaging/service-bus-sas.md).
- Vea hello [conexiones híbridas de Azure retransmisión protocolo guía](relay-hybrid-connections-protocol.md) para obtener información detallada acerca de la capacidad de conexiones híbridas de Hola.
- Para más información sobre la autenticación de mensajería de Service Bus, consulte [Autenticación y autorización de Service Bus](../service-bus-messaging/service-bus-authentication-and-authorization.md). 

[0]: ./media/relay-authentication-and-authorization/hcanon.png