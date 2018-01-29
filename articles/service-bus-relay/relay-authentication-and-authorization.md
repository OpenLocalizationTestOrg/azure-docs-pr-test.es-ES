---
title: "Autenticación y autorización en Azure Relay | Microsoft Docs"
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
ms.date: 01/23/2018
ms.author: sethm
ms.openlocfilehash: 86a9cf2c1106180ba5c8c65849042784bfd2afcd
ms.sourcegitcommit: 9890483687a2b28860ec179f5fd0a292cdf11d22
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2018
---
# <a name="azure-relay-authentication-and-authorization"></a>Autenticación y autorización en Azure Relay

Las aplicaciones pueden autenticarse en Azure Relay mediante la autenticación con Firma de acceso compartido (SAS). La autenticación de SAS permite a las aplicaciones autenticarse en el servicio Azure Relay mediante una clave de acceso configurada en el espacio de nombres de Relay. A continuación, puede usar esta clave para generar un token de Firma de acceso compartido que los clientes pueden usar para autenticarse en el servicio de retransmisión.

## <a name="shared-access-signature-authentication"></a>Autenticación con Firma de acceso compartido

La [autenticación de SAS](../service-bus-messaging/service-bus-sas.md) permite conceder a los usuarios acceso a los recursos de Azure Relay con derechos específicos. La autenticación con SAS implica la configuración de una clave criptográfica con derechos asociados en un recurso. Los clientes pueden obtener acceso a ese recurso presentando un token SAS que consta del URI del recurso al que se tiene acceso y una fecha de expiración firmada con la clave configurada.

Puede configurar claves para SAS en un espacio de nombres de Relay. A diferencia de la mensajería de Service Bus, [Conexiones híbridas de Relay](relay-hybrid-connections-protocol.md) admite remitentes no autorizados o anónimos. Puede habilitar el acceso anónimo para la entidad cuando la cree, tal y como se muestra en la siguiente pantalla desde el portal:

![][0]

Para usar SAS, puede configurar un objeto [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) en un espacio de nombres de Relay que consta de lo siguiente:

* *KeyName* que identifica la regla.
* *PrimaryKey* es una clave criptográfica usada para firmar o validar tokens SAS.
* *SecondaryKey* es una clave criptográfica usada para firmar o validar tokens SAS.
* *Rights* representa la recopilación de derechos de escucha, envío o administración concedidos.

Las reglas de autorización configuradas en el nivel de espacio de nombres pueden conceder acceso a todas las conexiones de retransmisión de un espacio de nombres a los clientes con tokens firmados con la clave correspondiente. Se pueden configurar un máximo de 12 reglas de autorización en un espacio de nombres de Relay. De forma predeterminada, se configura un objeto [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) con todos los derechos para cada espacio de nombres cuando se aprovisiona por primera vez.

Para obtener acceso a una entidad, el cliente requiere un token SAS generado con un objeto [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule)determinado. El token SAS se genera mediante el HMAC-SHA256 de una cadena de recurso que consta del URI del recurso al que se notifica el acceso y una fecha de expiración con una clave criptográfica asociada a la regla de autorización.

La compatibilidad de la autenticación con SAS para Azure Relay se incluye en el SDK .NET de Azure 2.0 y versiones posteriores. SAS incluye compatibilidad con un objeto [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Todas las API que aceptan una cadena de conexión como parámetro incluyen compatibilidad con cadenas de conexión SAS.

## <a name="next-steps"></a>pasos siguientes

- Para obtener más información sobre SAS, siga consultando [Autenticación en Service Bus con Firmas de acceso compartido](../service-bus-messaging/service-bus-sas.md).
- Consulte la guía [Protocolo de conexiones híbridas de Azure Relay](relay-hybrid-connections-protocol.md) para obtener información detallada sobre la funcionalidad Conexiones híbridas.
- Para más información sobre la autenticación de mensajería de Service Bus, consulte [Autenticación y autorización de Service Bus](../service-bus-messaging/service-bus-authentication-and-authorization.md). 

[0]: ./media/relay-authentication-and-authorization/hcanon.png