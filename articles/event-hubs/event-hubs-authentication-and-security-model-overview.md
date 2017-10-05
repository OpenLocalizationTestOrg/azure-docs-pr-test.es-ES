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
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="54a9a-103">Introducción al modelo de autenticación y seguridad de los Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="54a9a-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="54a9a-104">El modelo de seguridad de Azure Event Hubs cumple los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="54a9a-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="54a9a-105">Solo los clientes que tengan credenciales válidas pueden enviar datos a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="54a9a-106">Un cliente no puede suplantar a otro cliente.</span><span class="sxs-lookup"><span data-stu-id="54a9a-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="54a9a-107">Se puede bloquear el envío de datos por parte de un cliente no autorizado a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="54a9a-108">Autenticación de clientes</span><span class="sxs-lookup"><span data-stu-id="54a9a-108">Client authentication</span></span>
<span data-ttu-id="54a9a-109">El modelo de seguridad de Event Hubs se basa en una combinación de tokens de [firma de acceso compartido (SAS)](../service-bus-messaging/service-bus-sas.md) y *publicadores de eventos*.</span><span class="sxs-lookup"><span data-stu-id="54a9a-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="54a9a-110">Un publicador de eventos define un punto de conexión virtual para un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="54a9a-111">El publicador solo puede usarse para enviar mensajes a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="54a9a-112">No es posible recibir mensajes desde un publicador.</span><span class="sxs-lookup"><span data-stu-id="54a9a-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="54a9a-113">Normalmente, un centro de eventos emplea a un publicador por cliente.</span><span class="sxs-lookup"><span data-stu-id="54a9a-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="54a9a-114">Todos los mensajes que se envíen a cualquiera de los publicadores de un centro de eventos se ponen en cola dentro de ese centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="54a9a-115">Los publicadores permiten control de acceso y limitación avanzados.</span><span class="sxs-lookup"><span data-stu-id="54a9a-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="54a9a-116">A cada cliente de Event Hubs se le asigna un token único, que se carga en el cliente.</span><span class="sxs-lookup"><span data-stu-id="54a9a-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="54a9a-117">Los tokens se producen de forma que cada token único concede acceso a un publicador único diferente.</span><span class="sxs-lookup"><span data-stu-id="54a9a-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="54a9a-118">Un cliente que posea un token solo puede enviar a un publicador y a ningún otro.</span><span class="sxs-lookup"><span data-stu-id="54a9a-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="54a9a-119">Si varios clientes comparten el mismo token, cada uno de estos clientes comparte un publicador.</span><span class="sxs-lookup"><span data-stu-id="54a9a-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="54a9a-120">Aunque no se recomienda, es posible equipar los dispositivos con tokens que concedan acceso directo a un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="54a9a-121">Cualquier dispositivo que contenga un token de ese tipo puede enviar mensajes directamente a ese centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="54a9a-122">Ese dispositivo no estará sujeto a limitación.</span><span class="sxs-lookup"><span data-stu-id="54a9a-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="54a9a-123">Además, el dispositivo no puede estar en la lista negra que impide el envío a ese centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="54a9a-124">Todos los tokens se firman con una clave de SAS.</span><span class="sxs-lookup"><span data-stu-id="54a9a-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="54a9a-125">Normalmente, todos los tokens se firman con la misma clave.</span><span class="sxs-lookup"><span data-stu-id="54a9a-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="54a9a-126">Los clientes no conocen la clave; esto evita que los clientes produzcan tokens.</span><span class="sxs-lookup"><span data-stu-id="54a9a-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="54a9a-127">Creación de la clave SAS</span><span class="sxs-lookup"><span data-stu-id="54a9a-127">Create the SAS key</span></span>

<span data-ttu-id="54a9a-128">Cuando se crea un espacio de nombres de Event Hubs, el servicio genera una clave SAS de 256 bits llamada **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="54a9a-128">When creating an Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="54a9a-129">Esta clave permite enviar, escuchar y administrar los derechos del espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="54a9a-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="54a9a-130">También puede crear claves adicionales.</span><span class="sxs-lookup"><span data-stu-id="54a9a-130">You can also create additional keys.</span></span> <span data-ttu-id="54a9a-131">Se recomienda que genere una clave que conceda permisos de envío para el centro de eventos concreto.</span><span class="sxs-lookup"><span data-stu-id="54a9a-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="54a9a-132">En el resto de este tema, se presupone que esta clave tiene el nombre **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="54a9a-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="54a9a-133">En el ejemplo siguiente se crea una clave solo de envío cuando se crea el centro de eventos:</span><span class="sxs-lookup"><span data-stu-id="54a9a-133">The following example creates a send-only key when creating the event hub:</span></span>

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

### <a name="generate-tokens"></a><span data-ttu-id="54a9a-134">Generación de tokens</span><span class="sxs-lookup"><span data-stu-id="54a9a-134">Generate tokens</span></span>

<span data-ttu-id="54a9a-135">Puede generar tokens con la clave de SAS.</span><span class="sxs-lookup"><span data-stu-id="54a9a-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="54a9a-136">Solo debe generar un token por cliente.</span><span class="sxs-lookup"><span data-stu-id="54a9a-136">You must produce only one token per client.</span></span> <span data-ttu-id="54a9a-137">Los tokens se pueden producir con el método siguiente.</span><span class="sxs-lookup"><span data-stu-id="54a9a-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="54a9a-138">Todos los tokens se generan con la clave **EventHubSendKey** .</span><span class="sxs-lookup"><span data-stu-id="54a9a-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="54a9a-139">A cada token se le asigna un URI único.</span><span class="sxs-lookup"><span data-stu-id="54a9a-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="54a9a-140">Al llamar a este método, se debe especificar el URI como `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="54a9a-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="54a9a-141">Para todos los tokens, el URI es idéntico, con la excepción de `PUBLISHER_NAME`, que debe ser diferente para cada token.</span><span class="sxs-lookup"><span data-stu-id="54a9a-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="54a9a-142">Idealmente, `PUBLISHER_NAME` representa el identificador del cliente que recibe ese token.</span><span class="sxs-lookup"><span data-stu-id="54a9a-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="54a9a-143">Este método genera un token con la estructura siguiente:</span><span class="sxs-lookup"><span data-stu-id="54a9a-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="54a9a-144">La fecha de expiración del token se especifica en segundos desde el 1 de enero de 1970.</span><span class="sxs-lookup"><span data-stu-id="54a9a-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="54a9a-145">A continuación, se muestra un ejemplo de un token:</span><span class="sxs-lookup"><span data-stu-id="54a9a-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="54a9a-146">Normalmente, los tokens tienen una duración que se parece o supera la duración del cliente.</span><span class="sxs-lookup"><span data-stu-id="54a9a-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="54a9a-147">Si el cliente tiene la capacidad de obtener un nuevo token, pueden usarse tokens con una duración más corta.</span><span class="sxs-lookup"><span data-stu-id="54a9a-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="54a9a-148">Envío de datos</span><span class="sxs-lookup"><span data-stu-id="54a9a-148">Sending data</span></span>
<span data-ttu-id="54a9a-149">Cuando se han creado los tokens, cada cliente se aprovisiona con su propio token único.</span><span class="sxs-lookup"><span data-stu-id="54a9a-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="54a9a-150">Cuando el cliente envía datos a un centro de eventos, se etiqueta la solicitud de envío con el token.</span><span class="sxs-lookup"><span data-stu-id="54a9a-150">When the client sends data into an event hub, it tags its send request with the token.</span></span> <span data-ttu-id="54a9a-151">Para evitar que un atacante use la técnica de eavesdropping y robe el token, la comunicación entre el cliente y el centro de eventos debe realizarse a través de un canal cifrado.</span><span class="sxs-lookup"><span data-stu-id="54a9a-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="54a9a-152">Incorporación de clientes a la lista negra</span><span class="sxs-lookup"><span data-stu-id="54a9a-152">Blacklisting clients</span></span>
<span data-ttu-id="54a9a-153">Si un atacante roba un token, el atacante puede suplantar el cliente al que se ha robado el token.</span><span class="sxs-lookup"><span data-stu-id="54a9a-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="54a9a-154">Al incorporar al cliente a la lista negra el cliente queda inutilizable hasta que recibe un token nuevo que usa un publicador diferente.</span><span class="sxs-lookup"><span data-stu-id="54a9a-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="54a9a-155">Autenticación de aplicaciones de back-end</span><span class="sxs-lookup"><span data-stu-id="54a9a-155">Authentication of back-end applications</span></span>

<span data-ttu-id="54a9a-156">Para autenticar aplicaciones de back-end que consumen los datos que generan los clientes de Event Hubs, Event Hubs emplea un modelo de seguridad similar al que se usa en los temas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="54a9a-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="54a9a-157">Un grupo de consumidores de Centros de eventos equivale a una suscripción a un tema de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="54a9a-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="54a9a-158">Un cliente puede crear un grupo de consumidores si la solicitud para ello viene acompañada de un token que concede privilegios de administración para el centro de eventos o para el espacio de nombres al que pertenece.</span><span class="sxs-lookup"><span data-stu-id="54a9a-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub, or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="54a9a-159">Se permite que un cliente pueda consumir datos de un grupo de consumidores si la solicitud de recepción está acompañada de un token que conceda derechos de recepción en ese grupo de consumidores, centro de eventos o espacio de nombres al que pertenece el centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>

<span data-ttu-id="54a9a-160">La versión actual de Bus de servicio no admite reglas SAS para suscripciones individuales.</span><span class="sxs-lookup"><span data-stu-id="54a9a-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="54a9a-161">Lo mismo sucede con los grupos de consumidores de los Centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="54a9a-162">La compatibilidad con SAS se agregará para ambas características en el futuro.</span><span class="sxs-lookup"><span data-stu-id="54a9a-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="54a9a-163">En ausencia de autenticación SAS para grupos de consumidores individuales, puede usar claves SAS para proteger todos los grupos de consumidores con una clave común.</span><span class="sxs-lookup"><span data-stu-id="54a9a-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="54a9a-164">Este enfoque permite que una aplicación consuma datos desde cualquiera de los grupos de consumidores de un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="54a9a-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="54a9a-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="54a9a-165">Next steps</span></span>
<span data-ttu-id="54a9a-166">Para más información sobre Centros de eventos, visite los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="54a9a-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="54a9a-167">[Información general de Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="54a9a-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="54a9a-168">[Información general sobre las firmas de acceso compartido]</span><span class="sxs-lookup"><span data-stu-id="54a9a-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="54a9a-169">[Aplicaciones de ejemplo que usan Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="54a9a-169">[Sample applications that use Event Hubs]</span></span>

<span data-ttu-id="54a9a-170">[Información general de Event Hubs]: event-hubs-what-is-event-hubs.md</span><span class="sxs-lookup"><span data-stu-id="54a9a-170">[Event Hubs overview]: event-hubs-what-is-event-hubs.md</span></span>
<span data-ttu-id="54a9a-171">[Aplicaciones de ejemplo que usan Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="54a9a-171">[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span></span>
<span data-ttu-id="54a9a-172">[Información general sobre las firmas de acceso compartido]: ../service-bus-messaging/service-bus-sas.md</span><span class="sxs-lookup"><span data-stu-id="54a9a-172">[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md</span></span>

