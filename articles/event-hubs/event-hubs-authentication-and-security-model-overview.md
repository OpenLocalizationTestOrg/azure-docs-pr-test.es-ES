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
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="b0b8a-103">Introducción al modelo de autenticación y seguridad de los Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="b0b8a-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="b0b8a-104">modelo de seguridad de los centros de eventos de Azure de Hello cumple Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-104">hello Azure Event Hubs security model meets hello following requirements:</span></span>

* <span data-ttu-id="b0b8a-105">Solo los clientes que presentan credenciales válidas pueden enviar concentrador de eventos de tooan de datos.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-105">Only clients that present valid credentials can send data tooan event hub.</span></span>
* <span data-ttu-id="b0b8a-106">Un cliente no puede suplantar a otro cliente.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="b0b8a-107">Un cliente no autorizado se puede bloquear desde el centro de datos tooan eventos de envío.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-107">A rogue client can be blocked from sending data tooan event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="b0b8a-108">Autenticación de clientes</span><span class="sxs-lookup"><span data-stu-id="b0b8a-108">Client authentication</span></span>
<span data-ttu-id="b0b8a-109">modelo de seguridad de los centros de eventos de Hola se basa en una combinación de [firma de acceso compartido (SAS)](../service-bus-messaging/service-bus-sas.md) tokens y *publicadores de eventos*.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-109">hello Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="b0b8a-110">Un publicador de eventos define un punto de conexión virtual para un centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="b0b8a-111">publicador de Hello solo puede ser centro de eventos de toosend usa mensajes tooan.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-111">hello publisher can only be used toosend messages tooan event hub.</span></span> <span data-ttu-id="b0b8a-112">No es posible tooreceive mensajes desde un publicador.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-112">It is not possible tooreceive messages from a publisher.</span></span>

<span data-ttu-id="b0b8a-113">Normalmente, un centro de eventos emplea a un publicador por cliente.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="b0b8a-114">Todos los mensajes que se envían tooany de publicadores de Hola de un concentrador de eventos están en cola dentro de ese centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-114">All messages that are sent tooany of hello publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="b0b8a-115">Los publicadores permiten control de acceso y limitación avanzados.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="b0b8a-116">Cada cliente de los centros de eventos se asigna un token único, que es cargado toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-116">Each Event Hubs client is assigned a unique token, which is uploaded toohello client.</span></span> <span data-ttu-id="b0b8a-117">Hola tokens se producen de forma que cada token único concede publicador único de acceso tooa diferente.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-117">hello tokens are produced such that each unique token grants access tooa different unique publisher.</span></span> <span data-ttu-id="b0b8a-118">Sólo puede enviar a un cliente que posee un token tooone publisher, pero ningún otro editor.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-118">A client that possesses a token can only send tooone publisher, but no other publisher.</span></span> <span data-ttu-id="b0b8a-119">Si varios recursos compartidos de los clientes Hola mismo símbolo (token), a continuación, cada uno de ellos comparte un publicador.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-119">If multiple clients share hello same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="b0b8a-120">Aunque no se recomienda, es posible tooequip dispositivos con tokens que concedan concentrador de eventos de tooan de acceso directo.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-120">Although not recommended, it is possible tooequip devices with tokens that grant direct access tooan event hub.</span></span> <span data-ttu-id="b0b8a-121">Cualquier dispositivo que contenga un token de ese tipo puede enviar mensajes directamente a ese centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="b0b8a-122">Este tipo de dispositivo no estará sujeto toothrottling.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-122">Such a device will not be subject toothrottling.</span></span> <span data-ttu-id="b0b8a-123">Además, dispositivo hello no se puede ser en la lista negra en el envío de concentrador de eventos de toothat.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-123">Furthermore, hello device cannot be blacklisted from sending toothat event hub.</span></span>

<span data-ttu-id="b0b8a-124">Todos los tokens se firman con una clave de SAS.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="b0b8a-125">Normalmente, todos los tokens se firman con hello misma clave.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-125">Typically, all tokens are signed with hello same key.</span></span> <span data-ttu-id="b0b8a-126">Los clientes no son conscientes de la clave de hello; Esto impide que a otros clientes de tokens de fabricación.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-126">Clients are not aware of hello key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-hello-sas-key"></a><span data-ttu-id="b0b8a-127">Crear clave SAS de Hola</span><span class="sxs-lookup"><span data-stu-id="b0b8a-127">Create hello SAS key</span></span>

<span data-ttu-id="b0b8a-128">Al crear un espacio de nombres de los centros de eventos, el servicio de hello genera una clave SAS de 256 bits denominada **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-128">When creating an Event Hubs namespace, hello service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="b0b8a-129">Esta clave concede enviar, escucha y administra el espacio de nombres de derechos toohello.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-129">This key grants send, listen, and manage rights toohello namespace.</span></span> <span data-ttu-id="b0b8a-130">También puede crear claves adicionales.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-130">You can also create additional keys.</span></span> <span data-ttu-id="b0b8a-131">Se recomienda que genere una clave que concede enviar concentrador de eventos específicos de toohello de permisos.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-131">It is recommended that you produce a key that grants send permissions toohello specific event hub.</span></span> <span data-ttu-id="b0b8a-132">Para el resto de Hola de este tema, se supone que nombra esta clave **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-132">For hello remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="b0b8a-133">Hola de ejemplo siguiente crea una clave sólo de envío al crear el concentrador de eventos de hello:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-133">hello following example creates a send-only key when creating hello event hub:</span></span>

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

### <a name="generate-tokens"></a><span data-ttu-id="b0b8a-134">Generación de tokens</span><span class="sxs-lookup"><span data-stu-id="b0b8a-134">Generate tokens</span></span>

<span data-ttu-id="b0b8a-135">Puede generar tokens con la clave SAS de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-135">You can generate tokens using hello SAS key.</span></span> <span data-ttu-id="b0b8a-136">Solo debe generar un token por cliente.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-136">You must produce only one token per client.</span></span> <span data-ttu-id="b0b8a-137">A continuación, se pueden generar tokens con hello siguiendo el método.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-137">Tokens can then be produced using hello following method.</span></span> <span data-ttu-id="b0b8a-138">Todos los tokens se generan mediante hello **EventHubSendKey** clave.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-138">All tokens are generated using hello **EventHubSendKey** key.</span></span> <span data-ttu-id="b0b8a-139">A cada token se le asigna un URI único.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="b0b8a-140">Cuando se llama a este método, se debe especificar Hola URI como `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-140">When calling this method, hello URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="b0b8a-141">Para todos los tokens, Hola URI es idéntico, con excepción de Hola de `PUBLISHER_NAME`, que debe ser diferente para cada token.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-141">For all tokens, hello URI is identical, with hello exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="b0b8a-142">Idealmente, `PUBLISHER_NAME` representa Hola Id. del cliente de Hola que recibe ese token.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-142">Ideally, `PUBLISHER_NAME` represents hello ID of hello client that receives that token.</span></span>

<span data-ttu-id="b0b8a-143">Este método genera un token con hello siguiente estructura:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-143">This method generates a token with hello following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="b0b8a-144">tiempo de expiración del token de Hola se especifica en segundos, desde el 1 de enero de 1970.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-144">hello token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="b0b8a-145">Hola te mostramos un ejemplo de un símbolo (token):</span><span class="sxs-lookup"><span data-stu-id="b0b8a-145">hello following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="b0b8a-146">Por lo general, tokens de hello tienen una duración que se parece a o supera la duración Hola de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-146">Typically, hello tokens have a lifespan that resembles or exceeds hello lifespan of hello client.</span></span> <span data-ttu-id="b0b8a-147">Si cliente hello tiene Hola capacidad tooobtain un nuevo token, pueden utilizar tokens con una duración más corta.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-147">If hello client has hello capability tooobtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="b0b8a-148">Envío de datos</span><span class="sxs-lookup"><span data-stu-id="b0b8a-148">Sending data</span></span>
<span data-ttu-id="b0b8a-149">Una vez que se han creado los tokens de hello, cada cliente se aprovisiona con su propio token único.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-149">Once hello tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="b0b8a-150">Cuando el cliente de hello envía datos a un centro de eventos, etiquetas su solicitud de envío con el token de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-150">When hello client sends data into an event hub, it tags its send request with hello token.</span></span> <span data-ttu-id="b0b8a-151">un atacante intercepte y robe el token de hello, comunicación Hola entre el cliente de Hola y centro de eventos de hello tooprevent debe producir en un canal cifrado.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-151">tooprevent an attacker from eavesdropping and stealing hello token, hello communication between hello client and hello event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="b0b8a-152">Incorporación de clientes a la lista negra</span><span class="sxs-lookup"><span data-stu-id="b0b8a-152">Blacklisting clients</span></span>
<span data-ttu-id="b0b8a-153">Si un atacante roba un token, atacante Hola puede suplantar el cliente hello cuyo token se ha robado.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-153">If a token is stolen by an attacker, hello attacker can impersonate hello client whose token has been stolen.</span></span> <span data-ttu-id="b0b8a-154">Al incorporar al cliente a la lista negra el cliente queda inutilizable hasta que recibe un token nuevo que usa un publicador diferente.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="b0b8a-155">Autenticación de aplicaciones de back-end</span><span class="sxs-lookup"><span data-stu-id="b0b8a-155">Authentication of back-end applications</span></span>

<span data-ttu-id="b0b8a-156">aplicaciones de back-end de tooauthenticate que consumen datos de hello generados por los clientes de los centros de eventos, los concentradores de eventos emplea un modelo de seguridad que es el modelo toohello similar que se usa para temas de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-156">tooauthenticate back-end applications that consume hello data generated by Event Hubs clients, Event Hubs employs a security model that is similar toohello model that is used for Service Bus topics.</span></span> <span data-ttu-id="b0b8a-157">Un grupo de consumidores de centros de eventos es el tema de Bus de servicio de tooa de suscripción tooa equivalente.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-157">An Event Hubs consumer group is equivalent tooa subscription tooa Service Bus topic.</span></span> <span data-ttu-id="b0b8a-158">Un cliente puede crear un grupo de consumidores si el grupo de consumidores de hello solicitud toocreate Hola está acompañado por un símbolo (token) que concede privilegios de concentrador de eventos de Hola de administración o para toowhich de espacio de nombres de hello pertenece centro de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-158">A client can create a consumer group if hello request toocreate hello consumer group is accompanied by a token that grants manage privileges for hello event hub, or for hello namespace toowhich hello event hub belongs.</span></span> <span data-ttu-id="b0b8a-159">Un cliente puede tooconsume datos de un grupo de consumidores si Hola recibe la solicitud están acompañados de un token que concede derechos en ese grupo de consumidores de recepción, hello concentrador de eventos o centro de eventos de hello espacio de nombres toowhich Hola pertenece.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-159">A client is allowed tooconsume data from a consumer group if hello receive request is accompanied by a token that grants receive rights on that consumer group, hello event hub, or hello namespace toowhich hello event hub belongs.</span></span>

<span data-ttu-id="b0b8a-160">versión actual de Hola de Bus de servicio no es compatible con las reglas de SAS para suscripciones individuales.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-160">hello current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="b0b8a-161">Hola que esto mismo es aplicable para grupos de consumidores de centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-161">hello same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="b0b8a-162">Se agregará compatibilidad de SAS para ambas características Hola futuras.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-162">SAS support will be added for both features in hello future.</span></span>

<span data-ttu-id="b0b8a-163">En ausencia de Hola de autenticación SAS para grupos de consumidores individuales, puede usar todos los grupos de consumidores de toosecure de claves SAS con una clave común.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-163">In hello absence of SAS authentication for individual consumer groups, you can use SAS keys toosecure all consumer groups with a common key.</span></span> <span data-ttu-id="b0b8a-164">Este enfoque permite a un aplicación tooconsume datos de grupos de consumidores de Hola de un concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-164">This approach enables an application tooconsume data from any of hello consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0b8a-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b0b8a-165">Next steps</span></span>
<span data-ttu-id="b0b8a-166">toolearn más información acerca de los centros de eventos, visite Hola temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-166">toolearn more about Event Hubs, visit hello following topics:</span></span>

* <span data-ttu-id="b0b8a-167">[Información general de Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="b0b8a-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="b0b8a-168">[Información general sobre las firmas de acceso compartido]</span><span class="sxs-lookup"><span data-stu-id="b0b8a-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="b0b8a-169">[Aplicaciones de ejemplo que usan Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="b0b8a-169">[Sample applications that use Event Hubs]</span></span>

[Información general de Event Hubs]: event-hubs-what-is-event-hubs.md
[Aplicaciones de ejemplo que usan Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Información general sobre las firmas de acceso compartido]: ../service-bus-messaging/service-bus-sas.md

