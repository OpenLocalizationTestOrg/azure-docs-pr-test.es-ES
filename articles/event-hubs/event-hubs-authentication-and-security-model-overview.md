---
title: "aaaOverview del modelo de seguridad y autenticación de los centros de eventos de Azure | Documentos de Microsoft"
description: "Introducción al modelo de autenticación y seguridad de Centros de eventos"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a>Introducción al modelo de autenticación y seguridad de los Centros de eventos
modelo de seguridad de los centros de eventos de Azure de Hello cumple Hola según los requisitos:

* Solo los clientes que presentan credenciales válidas pueden enviar concentrador de eventos de tooan de datos.
* Un cliente no puede suplantar a otro cliente.
* Un cliente no autorizado se puede bloquear desde el centro de datos tooan eventos de envío.

## <a name="client-authentication"></a>Autenticación de clientes
modelo de seguridad de los centros de eventos de Hola se basa en una combinación de [firma de acceso compartido (SAS)](../service-bus-messaging/service-bus-sas.md) tokens y *publicadores de eventos*. Un publicador de eventos define un punto de conexión virtual para un centro de eventos. publicador de Hello solo puede ser centro de eventos de toosend usa mensajes tooan. No es posible tooreceive mensajes desde un publicador.

Normalmente, un centro de eventos emplea a un publicador por cliente. Todos los mensajes que se envían tooany de publicadores de Hola de un concentrador de eventos están en cola dentro de ese centro de eventos. Los publicadores permiten control de acceso y limitación avanzados.

Cada cliente de los centros de eventos se asigna un token único, que es cargado toohello cliente. Hola tokens se producen de forma que cada token único concede publicador único de acceso tooa diferente. Sólo puede enviar a un cliente que posee un token tooone publisher, pero ningún otro editor. Si varios recursos compartidos de los clientes Hola mismo símbolo (token), a continuación, cada uno de ellos comparte un publicador.

Aunque no se recomienda, es posible tooequip dispositivos con tokens que concedan concentrador de eventos de tooan de acceso directo. Cualquier dispositivo que contenga un token de ese tipo puede enviar mensajes directamente a ese centro de eventos. Este tipo de dispositivo no estará sujeto toothrottling. Además, dispositivo hello no se puede ser en la lista negra en el envío de concentrador de eventos de toothat.

Todos los tokens se firman con una clave de SAS. Normalmente, todos los tokens se firman con hello misma clave. Los clientes no son conscientes de la clave de hello; Esto impide que a otros clientes de tokens de fabricación.

### <a name="create-hello-sas-key"></a>Crear clave SAS de Hola

Al crear un espacio de nombres de los centros de eventos, el servicio de hello genera una clave SAS de 256 bits denominada **RootManageSharedAccessKey**. Esta clave concede enviar, escucha y administra el espacio de nombres de derechos toohello. También puede crear claves adicionales. Se recomienda que genere una clave que concede enviar concentrador de eventos específicos de toohello de permisos. Para el resto de Hola de este tema, se supone que nombra esta clave **EventHubSendKey**.

Hola de ejemplo siguiente crea una clave sólo de envío al crear el concentrador de eventos de hello:

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a>Generación de tokens

Puede generar tokens con la clave SAS de Hola. Solo debe generar un token por cliente. A continuación, se pueden generar tokens con hello siguiendo el método. Todos los tokens se generan mediante hello **EventHubSendKey** clave. A cada token se le asigna un URI único.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Cuando se llama a este método, se debe especificar Hola URI como `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`. Para todos los tokens, Hola URI es idéntico, con excepción de Hola de `PUBLISHER_NAME`, que debe ser diferente para cada token. Idealmente, `PUBLISHER_NAME` representa Hola Id. del cliente de Hola que recibe ese token.

Este método genera un token con hello siguiente estructura:

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

tiempo de expiración del token de Hola se especifica en segundos, desde el 1 de enero de 1970. Hola te mostramos un ejemplo de un símbolo (token):

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

Por lo general, tokens de hello tienen una duración que se parece a o supera la duración Hola de cliente de Hola. Si cliente hello tiene Hola capacidad tooobtain un nuevo token, pueden utilizar tokens con una duración más corta.

### <a name="sending-data"></a>Envío de datos
Una vez que se han creado los tokens de hello, cada cliente se aprovisiona con su propio token único.

Cuando el cliente de hello envía datos a un centro de eventos, etiquetas su solicitud de envío con el token de Hola. un atacante intercepte y robe el token de hello, comunicación Hola entre el cliente de Hola y centro de eventos de hello tooprevent debe producir en un canal cifrado.

### <a name="blacklisting-clients"></a>Incorporación de clientes a la lista negra
Si un atacante roba un token, atacante Hola puede suplantar el cliente hello cuyo token se ha robado. Al incorporar al cliente a la lista negra el cliente queda inutilizable hasta que recibe un token nuevo que usa un publicador diferente.

## <a name="authentication-of-back-end-applications"></a>Autenticación de aplicaciones de back-end

aplicaciones de back-end de tooauthenticate que consumen datos de hello generados por los clientes de los centros de eventos, los concentradores de eventos emplea un modelo de seguridad que es el modelo toohello similar que se usa para temas de Bus de servicio. Un grupo de consumidores de centros de eventos es el tema de Bus de servicio de tooa de suscripción tooa equivalente. Un cliente puede crear un grupo de consumidores si el grupo de consumidores de hello solicitud toocreate Hola está acompañado por un símbolo (token) que concede privilegios de concentrador de eventos de Hola de administración o para toowhich de espacio de nombres de hello pertenece centro de eventos de Hola. Un cliente puede tooconsume datos de un grupo de consumidores si Hola recibe la solicitud están acompañados de un token que concede derechos en ese grupo de consumidores de recepción, hello concentrador de eventos o centro de eventos de hello espacio de nombres toowhich Hola pertenece.

versión actual de Hola de Bus de servicio no es compatible con las reglas de SAS para suscripciones individuales. Hola que esto mismo es aplicable para grupos de consumidores de centros de eventos. Se agregará compatibilidad de SAS para ambas características Hola futuras.

En ausencia de Hola de autenticación SAS para grupos de consumidores individuales, puede usar todos los grupos de consumidores de toosecure de claves SAS con una clave común. Este enfoque permite a un aplicación tooconsume datos de grupos de consumidores de Hola de un concentrador de eventos.

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de los centros de eventos, visite Hola temas siguientes:

* [Información general de Event Hubs]
* [Información general sobre las firmas de acceso compartido]
* [Aplicaciones de ejemplo que usan Event Hubs]

[Información general de Event Hubs]: event-hubs-what-is-event-hubs.md
[Aplicaciones de ejemplo que usan Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Información general sobre las firmas de acceso compartido]: ../service-bus-messaging/service-bus-sas.md

