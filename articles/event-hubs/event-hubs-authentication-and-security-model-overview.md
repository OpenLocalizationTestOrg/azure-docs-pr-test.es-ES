---
title: "Introducción al modelo de autenticación y seguridad de Event Hubs de Azure | Microsoft Docs"
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
ms.openlocfilehash: 5abdbf70d4fdb2c7feb0f3537ecc0f2abf0775a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a>Introducción al modelo de autenticación y seguridad de los Centros de eventos
El modelo de seguridad de Azure Event Hubs cumple los siguientes requisitos:

* Solo los clientes que tengan credenciales válidas pueden enviar datos a un centro de eventos.
* Un cliente no puede suplantar a otro cliente.
* Se puede bloquear el envío de datos por parte de un cliente no autorizado a un centro de eventos.

## <a name="client-authentication"></a>Autenticación de clientes
El modelo de seguridad de Event Hubs se basa en una combinación de tokens de [firma de acceso compartido (SAS)](../service-bus-messaging/service-bus-sas.md) y *publicadores de eventos*. Un publicador de eventos define un punto de conexión virtual para un centro de eventos. El publicador solo puede usarse para enviar mensajes a un centro de eventos. No es posible recibir mensajes desde un publicador.

Normalmente, un centro de eventos emplea a un publicador por cliente. Todos los mensajes que se envíen a cualquiera de los publicadores de un centro de eventos se ponen en cola dentro de ese centro de eventos. Los publicadores permiten control de acceso y limitación avanzados.

A cada cliente de Event Hubs se le asigna un token único, que se carga en el cliente. Los tokens se producen de forma que cada token único concede acceso a un publicador único diferente. Un cliente que posea un token solo puede enviar a un publicador y a ningún otro. Si varios clientes comparten el mismo token, cada uno de estos clientes comparte un publicador.

Aunque no se recomienda, es posible equipar los dispositivos con tokens que concedan acceso directo a un centro de eventos. Cualquier dispositivo que contenga un token de ese tipo puede enviar mensajes directamente a ese centro de eventos. Ese dispositivo no estará sujeto a limitación. Además, el dispositivo no puede estar en la lista negra que impide el envío a ese centro de eventos.

Todos los tokens se firman con una clave de SAS. Normalmente, todos los tokens se firman con la misma clave. Los clientes no conocen la clave; esto evita que los clientes produzcan tokens.

### <a name="create-the-sas-key"></a>Creación de la clave SAS

Cuando se crea un espacio de nombres de Event Hubs, el servicio genera una clave SAS de 256 bits llamada **RootManageSharedAccessKey**. Esta clave permite enviar, escuchar y administrar los derechos del espacio de nombres. También puede crear claves adicionales. Se recomienda que genere una clave que conceda permisos de envío para el centro de eventos concreto. En el resto de este tema, se presupone que esta clave tiene el nombre **EventHubSendKey**.

En el ejemplo siguiente se crea una clave solo de envío cuando se crea el centro de eventos:

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a>Generación de tokens

Puede generar tokens con la clave de SAS. Solo debe generar un token por cliente. Los tokens se pueden producir con el método siguiente. Todos los tokens se generan con la clave **EventHubSendKey** . A cada token se le asigna un URI único.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Al llamar a este método, se debe especificar el URI como `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`. Para todos los tokens, el URI es idéntico, con la excepción de `PUBLISHER_NAME`, que debe ser diferente para cada token. Idealmente, `PUBLISHER_NAME` representa el identificador del cliente que recibe ese token.

Este método genera un token con la estructura siguiente:

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

La fecha de expiración del token se especifica en segundos desde el 1 de enero de 1970. A continuación, se muestra un ejemplo de un token:

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

Normalmente, los tokens tienen una duración que se parece o supera la duración del cliente. Si el cliente tiene la capacidad de obtener un nuevo token, pueden usarse tokens con una duración más corta.

### <a name="sending-data"></a>Envío de datos
Cuando se han creado los tokens, cada cliente se aprovisiona con su propio token único.

Cuando el cliente envía datos a un centro de eventos, se etiqueta la solicitud de envío con el token. Para evitar que un atacante use la técnica de eavesdropping y robe el token, la comunicación entre el cliente y el centro de eventos debe realizarse a través de un canal cifrado.

### <a name="blacklisting-clients"></a>Incorporación de clientes a la lista negra
Si un atacante roba un token, el atacante puede suplantar el cliente al que se ha robado el token. Al incorporar al cliente a la lista negra el cliente queda inutilizable hasta que recibe un token nuevo que usa un publicador diferente.

## <a name="authentication-of-back-end-applications"></a>Autenticación de aplicaciones de back-end

Para autenticar aplicaciones de back-end que consumen los datos que generan los clientes de Event Hubs, Event Hubs emplea un modelo de seguridad similar al que se usa en los temas de Service Bus. Un grupo de consumidores de Centros de eventos equivale a una suscripción a un tema de Bus de servicio. Un cliente puede crear un grupo de consumidores si la solicitud para ello viene acompañada de un token que concede privilegios de administración para el centro de eventos o para el espacio de nombres al que pertenece. Se permite que un cliente pueda consumir datos de un grupo de consumidores si la solicitud de recepción está acompañada de un token que conceda derechos de recepción en ese grupo de consumidores, centro de eventos o espacio de nombres al que pertenece el centro de eventos.

La versión actual de Bus de servicio no admite reglas SAS para suscripciones individuales. Lo mismo sucede con los grupos de consumidores de los Centros de eventos. La compatibilidad con SAS se agregará para ambas características en el futuro.

En ausencia de autenticación SAS para grupos de consumidores individuales, puede usar claves SAS para proteger todos los grupos de consumidores con una clave común. Este enfoque permite que una aplicación consuma datos desde cualquiera de los grupos de consumidores de un centro de eventos.

## <a name="next-steps"></a>Pasos siguientes
Para más información sobre Centros de eventos, visite los siguientes temas:

* [Información general de Event Hubs]
* [Información general sobre las firmas de acceso compartido]
* [Aplicaciones de ejemplo que usan Event Hubs]

[Información general de Event Hubs]: event-hubs-what-is-event-hubs.md
[Aplicaciones de ejemplo que usan Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Información general sobre las firmas de acceso compartido]: ../service-bus-messaging/service-bus-sas.md

