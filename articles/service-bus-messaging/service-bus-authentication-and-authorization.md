---
title: "aaaAzure Bus de servicio de autenticación y autorización | Documentos de Microsoft"
description: "Autenticar aplicaciones tooService Bus con la autenticación de firma de acceso compartido (SAS)."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 18bad0ed-1cee-4a5c-a377-facc4785c8c9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: sethm
ms.openlocfilehash: 898a2144c99d8fac074b6d85604f710bf512e71e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-and-authorization"></a>Autenticación y autorización de Service Bus

Las aplicaciones pueden autenticarse tooAzure Bus de servicio con la firma de acceso compartido (SAS) authentication. Comparte la firma de acceso autenticación habilita aplicaciones tooauthenticate tooService Bus mediante una clave de acceso configurada en el espacio de nombres de Hola o de una entidad de hello con la que se asocian derechos específicos. A continuación, puede usar esta clave toogenerate un token de firma de acceso compartido que los clientes pueden usar tooauthenticate tooService Bus.

> [!IMPORTANT]
> Debe usar SAS en lugar de Azure Active Directory Access Control (también conocido como Access Control Service o ACS), ya que ACS está en desuso. SAS proporciona un esquema de autenticación sencillo, flexible y fácil de usar para Service Bus. Las aplicaciones pueden usar SAS en escenarios en los que no necesitan noción de hello toomanage de un "usuario" autorizado. Para más información, vea [esta publicación del blog](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/).

## <a name="shared-access-signature-authentication"></a>Autenticación con Firma de acceso compartido

[Autenticación de SAS](service-bus-sas.md) permite toogrant un recursos de Bus de tooService de acceso de usuario con derechos específicos. Autenticación con SAS en el Bus de servicio implica la configuración de Hola de una clave criptográfica con derechos asociados en un recurso de Bus de servicio. Los clientes, a continuación, pueden obtener acceso a recursos de toothat presentando un token SAS, que consta del URI que se obtiene acceso de recurso de hello y una fecha de expiración firmada con hello configurado clave.

Puede configurar claves para SAS en un espacio de nombres de Service Bus. clave de Hola aplica a las entidades de mensajería de tooall en ese espacio de nombres. También puede configurar claves en temas y colas de Service Bus. SAS también es compatible con [Azure Relay](../service-bus-relay/relay-authentication-and-authorization.md).

toouse SAS, puede configurar un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objeto en un espacio de nombres, cola o tema. Esta regla está formada por hello siguientes elementos:

* *KeyName* que identifica la regla de Hola.
* *PrimaryKey* es toosign y validar tokens SAS usa una clave criptográfica.
* *SecondaryKey* es toosign y validar tokens SAS usa una clave criptográfica.
* *Derechos de* que representa colección de Hola de escucha, envío y administración de derechos concedidos.

Reglas de autorización configuradas en el nivel de espacio de nombres de hello pueden conceder acceso tooall entidades en un espacio de nombres para los clientes con tokens firmados con la clave correspondiente Hola. Seguridad too12 tales reglas de autorización pueden configurarse en un espacio de nombres, cola o tema de Bus de servicio. De forma predeterminada, se configura un objeto [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) con todos los derechos para cada espacio de nombres cuando se aprovisiona por primera vez.

tooaccess una entidad, el cliente de hello requiere un token SAS generado con un determinado [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). token de SAS de Hola se genera utilizando Hola se notifica el HMAC-SHA256 de una cadena de recurso que consta del recurso de hello acceso URI toowhich y una fecha de expiración con una clave criptográfica asociada la regla de autorización de Hola.

Compatibilidad con la autenticación SAS para Bus de servicio se incluye en versiones de hello Azure SDK para .NET 2.0 y posterior. SAS incluye compatibilidad con un objeto [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Todas las API que aceptan una cadena de conexión como parámetro incluyen compatibilidad con cadenas de conexión SAS.

## <a name="next-steps"></a>Pasos siguientes

- Para obtener más información sobre SAS, siga consultando [Autenticación en Service Bus con Firmas de acceso compartido](service-bus-sas.md).
- [Cambia los espacios de nombres de tooACS habilitado.](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- Para obtener la información correspondiente a la autenticación y autorización de Azure Relay, consulte [Azure Relay authentication and authorization](../service-bus-relay/relay-authentication-and-authorization.md) (Autenticación y autorización de Azure Relay). 

