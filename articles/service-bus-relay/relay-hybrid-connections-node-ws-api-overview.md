---
title: "Introducción a las API de Node para Azure Relay | Microsoft Docs"
description: "Introducción a las API de Node para Relay"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 28526c05c7f364f0fcaaa362fc97857f850040ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="75f75-103">Introducción a las API de Node para conexiones híbridas de Relay</span><span class="sxs-lookup"><span data-stu-id="75f75-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="75f75-104">Información general</span><span class="sxs-lookup"><span data-stu-id="75f75-104">Overview</span></span>

<span data-ttu-id="75f75-105">El paquete de Node [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) para Conexiones híbridas de Azure Relay es una ampliación del paquete NPM ["ws"](https://www.npmjs.com/package/ws) en el que se basa.</span><span class="sxs-lookup"><span data-stu-id="75f75-105">The [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends the ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="75f75-106">Este paquete vuelve a exportar todas las exportaciones de ese paquete base y agrega otras nuevas que habilitan la integración con la característica Conexiones híbridas del servicio Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="75f75-106">This package re-exports all exports of that base package and adds new exports that enable integration with the Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="75f75-107">Las aplicaciones existentes con `require('ws')` pueden usar este paquete con `require('hyco-ws')` en su lugar, lo que también hace posibles escenarios híbridos en los que una aplicación puede escuchar conexiones WebSocket localmente desde "dentro del firewall", así como por medio de Conexiones híbridas, de forma simultánea.</span><span class="sxs-lookup"><span data-stu-id="75f75-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside the firewall" and via Hybrid Connections, all at the same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="75f75-108">Documentación</span><span class="sxs-lookup"><span data-stu-id="75f75-108">Documentation</span></span>

<span data-ttu-id="75f75-109">Las API están [documentadas en el paquete principal "ws"](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="75f75-109">The APIs are [documented in the main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="75f75-110">En este artículo se describe la diferencia de este paquete con esa línea de base.</span><span class="sxs-lookup"><span data-stu-id="75f75-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="75f75-111">Las diferencias principales entre el paquete base y "hyco-ws" es que este último agrega una nueva clase de servidor, exportada por medio de `require('hyco-ws').RelayedServer`, y varios métodos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="75f75-111">The key differences between the base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="75f75-112">Métodos auxiliares del paquete</span><span class="sxs-lookup"><span data-stu-id="75f75-112">Package helper methods</span></span>

<span data-ttu-id="75f75-113">Hay varios métodos de utilidad disponibles en la exportación de paquete, a los que puede hacer referencia como sigue:</span><span class="sxs-lookup"><span data-stu-id="75f75-113">There are several utility methods available on the package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="75f75-114">Los métodos auxiliares son para utilizarse con este paquete, pero también los puede usar un servidor de nodo para permitir que los clientes web o de dispositivo creen agentes de escucha o remitentes.</span><span class="sxs-lookup"><span data-stu-id="75f75-114">The helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients to create listeners or senders.</span></span> <span data-ttu-id="75f75-115">El servidor utiliza estos métodos pasándoles URI que insertan tokens de corta duración.</span><span class="sxs-lookup"><span data-stu-id="75f75-115">The server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="75f75-116">Estos URI también se pueden usar con pilas WebSocket comunes que no admiten que se establezcan encabezados HTTP para el protocolo de enlace WebSocket.</span><span class="sxs-lookup"><span data-stu-id="75f75-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for the WebSocket handshake.</span></span> <span data-ttu-id="75f75-117">Se admite la inserción de tokens de autorización en el URI principalmente para los escenarios de uso con biblioteca externa.</span><span class="sxs-lookup"><span data-stu-id="75f75-117">Embedding authorization tokens into the URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="75f75-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="75f75-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="75f75-119">Crea un URI válido para el agente de escucha de conexión híbrida de Azure Relay para el espacio de nombres y la ruta de acceso dados.</span><span class="sxs-lookup"><span data-stu-id="75f75-119">Creates a valid Azure Relay Hybrid Connection listener URI for the given namespace and path.</span></span> <span data-ttu-id="75f75-120">Este URI se puede usar con la versión de retransmisión de la clase WebSocketServer.</span><span class="sxs-lookup"><span data-stu-id="75f75-120">This URI can then be used with the relay version of the WebSocketServer class.</span></span>

- <span data-ttu-id="75f75-121">`namespaceName` (se requiere): el nombre de dominio completo del espacio de nombres de Azure Relay que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="75f75-121">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="75f75-122">`path` (se requiere): el nombre de una conexión híbrida de Azure Relay existente en dicho espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="75f75-122">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="75f75-123">`token` (opcional): un token de acceso de Relay emitido anteriormente que se inserta en el identificador URI del agente de escucha (consulte el ejemplo siguiente).</span><span class="sxs-lookup"><span data-stu-id="75f75-123">`token` (optional) - a previously issued Relay access token that is embedded in the listener URI (see the following example).</span></span>
- <span data-ttu-id="75f75-124">`id` (opcional): un identificador de seguimiento que habilita el seguimiento los diagnósticos de un extremo a otro de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="75f75-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="75f75-125">El valor `token` es opcional y solo debe usarse cuando no sea posible enviar encabezados HTTP junto con el protocolo de enlace WebSocket, como sucede con la pila WebSocket de W3C.</span><span class="sxs-lookup"><span data-stu-id="75f75-125">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="75f75-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="75f75-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="75f75-127">Crea un URI válido para envío de conexión híbrida de Azure Relay para el espacio de nombres y la ruta de acceso dados.</span><span class="sxs-lookup"><span data-stu-id="75f75-127">Creates a valid Azure Relay Hybrid Connection send URI for the given namespace and path.</span></span> <span data-ttu-id="75f75-128">Este URI se puede utilizar con cualquier cliente de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="75f75-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="75f75-129">`namespaceName` (se requiere): el nombre de dominio completo del espacio de nombres de Azure Relay que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="75f75-129">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="75f75-130">`path` (se requiere): el nombre de una conexión híbrida de Azure Relay existente en dicho espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="75f75-130">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="75f75-131">`token` (opcional): un token de acceso de Relay emitido anteriormente que se inserta en el identificador URI de envío (consulte el ejemplo siguiente).</span><span class="sxs-lookup"><span data-stu-id="75f75-131">`token` (optional) - a previously issued Relay access token that is embedded in the send URI (see the following example).</span></span>
- <span data-ttu-id="75f75-132">`id` (opcional): un identificador de seguimiento que habilita el seguimiento los diagnósticos de un extremo a otro de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="75f75-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="75f75-133">El valor `token` es opcional y solo debe usarse cuando no sea posible enviar encabezados HTTP junto con el protocolo de enlace WebSocket, como sucede con la pila WebSocket de W3C.</span><span class="sxs-lookup"><span data-stu-id="75f75-133">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="75f75-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="75f75-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="75f75-135">Crea un token de firma de acceso compartido (SAS) de Azure Relay para el identificador URI de destino, la regla de SAS y la clave de regla de SAS dados que es válido durante el número de segundos determinado o durante una hora, a partir del instante actual si se omite el argumento de expiración.</span><span class="sxs-lookup"><span data-stu-id="75f75-135">Creates an Azure Relay Shared Access Signature (SAS) token for the given target URI, SAS rule, and SAS rule key that is valid for the given number of seconds or for an hour from the current instant if the expiry argument is omitted.</span></span>

- <span data-ttu-id="75f75-136">`uri` (se requiere): el identificador URI para el que va a emitir el token.</span><span class="sxs-lookup"><span data-stu-id="75f75-136">`uri` (required) - the URI for which the token is to be issued.</span></span> <span data-ttu-id="75f75-137">El identificador URI se normaliza para usar el esquema HTTP y se quita la información de la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="75f75-137">The URI is normalized to use the HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="75f75-138">`ruleName` (se requiere): nombre de regla de SAS de la entidad representada por el identificador URI dado o del espacio de nombres representado por la parte de host del identificador URI.</span><span class="sxs-lookup"><span data-stu-id="75f75-138">`ruleName` (required) - SAS rule name for either the entity represented by the given URI, or for the namespace represented by the URI host portion.</span></span>
- <span data-ttu-id="75f75-139">`key` (se requiere): clave válida para la regla SAS.</span><span class="sxs-lookup"><span data-stu-id="75f75-139">`key` (required) - valid key for the SAS rule.</span></span> 
- <span data-ttu-id="75f75-140">`expirationSeconds` (opcional): número de segundos que faltan para que expire el token generado.</span><span class="sxs-lookup"><span data-stu-id="75f75-140">`expirationSeconds` (optional) - the number of seconds until the generated token should expire.</span></span> <span data-ttu-id="75f75-141">Si no se especifica, el valor predeterminado es 1 hora (3600).</span><span class="sxs-lookup"><span data-stu-id="75f75-141">If not specified, the default is 1 hour (3600).</span></span>

<span data-ttu-id="75f75-142">El token emitido confiere los derechos asociados a la regla de SAS especificada para la duración dada.</span><span class="sxs-lookup"><span data-stu-id="75f75-142">The issued token confers the rights associated with the specified SAS rule for the given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="75f75-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="75f75-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="75f75-144">Este método es funcionalmente equivalente al método `createRelayToken` que se documentó anteriormente, pero devuelve el token anexado correctamente al identificador URI de entrada.</span><span class="sxs-lookup"><span data-stu-id="75f75-144">This method is functionally equivalent to the `createRelayToken` method documented previously, but returns the token correctly appended to the input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="75f75-145">Clase ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="75f75-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="75f75-146">La clase `hycows.RelayedServer` es una alternativa a la clase `ws.Server` que no escucha en la red local, sino que delega la escucha en el servicio Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="75f75-146">The `hycows.RelayedServer` class is an alternative to the `ws.Server` class that does not listen on the local network, but delegates listening to the Azure Relay service.</span></span>

<span data-ttu-id="75f75-147">Ambas clases son en su mayor parte compatibles con los contratos, lo que significa que cualquier aplicación existente que use la clase `ws.Server` puede cambiarse fácilmente para que use la versión retransmitida.</span><span class="sxs-lookup"><span data-stu-id="75f75-147">The two classes are mostly contract compatible, meaning that an existing application using the `ws.Server` class can easily be changed to use the relayed version.</span></span> <span data-ttu-id="75f75-148">Las diferencias principales residen en el constructor y en las opciones disponibles.</span><span class="sxs-lookup"><span data-stu-id="75f75-148">The main differences are in the constructor and in the available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="75f75-149">Constructor</span><span class="sxs-lookup"><span data-stu-id="75f75-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="75f75-150">El constructor `RelayedServer` admite un conjunto de argumentos diferente del de `Server`, ya que ni es un agente de escucha independiente ni puede insertarse en un marco de trabajo del agente de escucha HTTP existente.</span><span class="sxs-lookup"><span data-stu-id="75f75-150">The `RelayedServer` constructor supports a different set of arguments than the `Server`, because it is not a standalone listener, or able to be embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="75f75-151">Además, hay menos opciones disponibles porque la administración de WebSocket se delega en gran medida en el servicio Relay.</span><span class="sxs-lookup"><span data-stu-id="75f75-151">There are also fewer options available since the WebSocket management is largely delegated to the Relay service.</span></span>

<span data-ttu-id="75f75-152">Argumentos del constructor:</span><span class="sxs-lookup"><span data-stu-id="75f75-152">Constructor arguments:</span></span>

- <span data-ttu-id="75f75-153">`server` (se requiere): el identificador URI completo de un nombre de conexión híbrida en la que se escucha, y que normalmente se construye con el método auxiliar WebSocket.createRelayListenUri().</span><span class="sxs-lookup"><span data-stu-id="75f75-153">`server` (required) - the fully qualified URI for a Hybrid Connection name on which to listen, usually constructed with the WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="75f75-154">`token` (se requiere): este argumento contiene una cadena de token emitida anteriormente o una función de devolución de llamada a la que se puede llamar para obtener este tipo de cadena de token.</span><span class="sxs-lookup"><span data-stu-id="75f75-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called to obtain such a token string.</span></span> <span data-ttu-id="75f75-155">Se prefiere la opción de devolución de llamada, puesto que permite la renovación del token.</span><span class="sxs-lookup"><span data-stu-id="75f75-155">The callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="75f75-156">Eventos</span><span class="sxs-lookup"><span data-stu-id="75f75-156">Events</span></span>

<span data-ttu-id="75f75-157">Las instancias de `RelayedServer` emiten tres eventos que permiten controlar las solicitudes entrantes, establecer conexiones y detectar condiciones de error.</span><span class="sxs-lookup"><span data-stu-id="75f75-157">`RelayedServer` instances emit three events that enable you to handle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="75f75-158">Debe suscribirse al evento `connect` para controlar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="75f75-158">You must subscribe to the `connect` event to handle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="75f75-159">encabezados</span><span class="sxs-lookup"><span data-stu-id="75f75-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="75f75-160">El evento `headers` se genera inmediatamente antes de que se acepte una conexión entrante, lo que permite que se modifiquen los encabezados que se envían al cliente.</span><span class="sxs-lookup"><span data-stu-id="75f75-160">The `headers` event is raised just before an incoming connection is accepted, enabling modification of the headers to send to the client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="75f75-161">connection</span><span class="sxs-lookup"><span data-stu-id="75f75-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="75f75-162">Se emite cuando se acepta una nueva conexión de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="75f75-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="75f75-163">El objeto es de tipo `ws.WebSocket`, igual que con el paquete base.</span><span class="sxs-lookup"><span data-stu-id="75f75-163">The object is of type `ws.WebSocket`, same as with the base package.</span></span>


##### <a name="error"></a><span data-ttu-id="75f75-164">error</span><span class="sxs-lookup"><span data-stu-id="75f75-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="75f75-165">Si el servidor subyacente emite un error, se reenvía aquí.</span><span class="sxs-lookup"><span data-stu-id="75f75-165">If the underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="75f75-166">Aplicaciones auxiliares</span><span class="sxs-lookup"><span data-stu-id="75f75-166">Helpers</span></span>

<span data-ttu-id="75f75-167">Para simplificar el inicio de un servidor de retransmisión y la suscripción inmediata a las conexiones entrantes, el paquete expone una función auxiliar sencilla, que también se utiliza en los ejemplos, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="75f75-167">To simplify starting a relayed server and immediately subscribing to incoming connections, the package exposes a simple helper function, which is also used in the examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="75f75-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="75f75-168">createRelayedListener</span></span>

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a><span data-ttu-id="75f75-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="75f75-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="75f75-170">Este método llama al constructor para crear una instancia de RelayedServer y después suscribe la devolución de llamada proporcionada al evento "connection".</span><span class="sxs-lookup"><span data-stu-id="75f75-170">This method calls the constructor to create a new instance of the RelayedServer and then subscribes the provided callback to the 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="75f75-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="75f75-171">relayedConnect</span></span>

<span data-ttu-id="75f75-172">Con solo reflejar la función `createRelayedServer`, `relayedConnect` crea una conexión de cliente y se suscribe al evento "open" en el socket resultante.</span><span class="sxs-lookup"><span data-stu-id="75f75-172">Simply mirroring the `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes to the 'open' event on the resulting socket.</span></span>

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a><span data-ttu-id="75f75-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="75f75-173">Next steps</span></span>
<span data-ttu-id="75f75-174">Para obtener más información sobre Azure Relay, visite estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="75f75-174">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="75f75-175">¿Qué es Relay de Azure?</span><span class="sxs-lookup"><span data-stu-id="75f75-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* <span data-ttu-id="75f75-176">[Available Relay APIs ](relay-api-overview.md) (API de Relay disponibles)</span><span class="sxs-lookup"><span data-stu-id="75f75-176">[Available Relay APIs](relay-api-overview.md)</span></span>
