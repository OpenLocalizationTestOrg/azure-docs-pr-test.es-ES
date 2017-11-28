---
title: "aaaOverview de hello las API de nodo de retransmisión de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="67c83-103">Introducción a las API de Node para conexiones híbridas de Relay</span><span class="sxs-lookup"><span data-stu-id="67c83-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="67c83-104">Información general</span><span class="sxs-lookup"><span data-stu-id="67c83-104">Overview</span></span>

<span data-ttu-id="67c83-105">Hola [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) paquete de nodo para las conexiones híbridas de retransmisión de Azure se basa y extiende hello ['ws'](https://www.npmjs.com/package/ws) paquete NPM.</span><span class="sxs-lookup"><span data-stu-id="67c83-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="67c83-106">Este paquete volver a exporta todas las exportaciones de ese paquete base y agrega nuevas exportaciones que habilitar la integración con la característica de conexiones híbridas del servicio de retransmisión de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="67c83-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="67c83-107">Las aplicaciones existentes que `require('ws')` puede usar este paquete con `require('hyco-ws')` en su lugar, lo que también permite escenarios híbridos en el que una aplicación puede escuchar para las conexiones de WebSocket localmente desde "dentro del firewall de hello" y a través de conexiones híbridas, todo en el Hola mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="67c83-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="67c83-108">Documentación</span><span class="sxs-lookup"><span data-stu-id="67c83-108">Documentation</span></span>

<span data-ttu-id="67c83-109">Hello API son [documentados en el paquete de principal 'ws' hello](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="67c83-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="67c83-110">En este artículo se describe la diferencia de este paquete con esa línea de base.</span><span class="sxs-lookup"><span data-stu-id="67c83-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="67c83-111">Hola diferencias principales entre el paquete básico de Hola y esta 'hyco-ws' es que agrega una nueva clase de servidor exportada mediante `require('hyco-ws').RelayedServer`y varios métodos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="67c83-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="67c83-112">Métodos auxiliares del paquete</span><span class="sxs-lookup"><span data-stu-id="67c83-112">Package helper methods</span></span>

<span data-ttu-id="67c83-113">Hay varios métodos de utilidad durante la exportación de paquete de Hola que puede hacer referencia como sigue:</span><span class="sxs-lookup"><span data-stu-id="67c83-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="67c83-114">métodos de aplicación auxiliar de Hello son para su uso con este paquete, pero también pueden utilizarse un servidor de nodo para habilitar web o dispositivo clientes toocreate los agentes de escucha o remitentes.</span><span class="sxs-lookup"><span data-stu-id="67c83-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="67c83-115">servidor de Hello usa estos métodos pasándolos URI que inserte tokens de corta duración.</span><span class="sxs-lookup"><span data-stu-id="67c83-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="67c83-116">Estos URI también se pueden usar con pilas de WebSocket común que no admiten establecer los encabezados HTTP para el protocolo de enlace de hello WebSocket.</span><span class="sxs-lookup"><span data-stu-id="67c83-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="67c83-117">La incorporación de tokens de autorización en hello que URI se admite principalmente para los escenarios de uso de biblioteca externa.</span><span class="sxs-lookup"><span data-stu-id="67c83-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="67c83-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="67c83-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="67c83-119">Crea una escucha de conexión híbrida de Azure retransmisión URI válida para hello tiene espacio de nombres y la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="67c83-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="67c83-120">Este URI, a continuación, puede utilizarse con la versión de retransmisión de Hola de hello WebSocketServer clase.</span><span class="sxs-lookup"><span data-stu-id="67c83-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="67c83-121">`namespaceName`(obligatorio): Hola nombre completo del dominio de toouse de espacio de nombres de hello retransmisión de Azure.</span><span class="sxs-lookup"><span data-stu-id="67c83-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="67c83-122">`path`(obligatorio): Hola el nombre de una conexión de retransmisión híbrida de Azure existente en ese espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="67c83-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="67c83-123">`token`(opcional): un acceso de retransmisión emitido previamente símbolo (token) que está incrustada en el agente de escucha de hello URI (vea el siguiente ejemplo de Hola).</span><span class="sxs-lookup"><span data-stu-id="67c83-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="67c83-124">`id` (opcional): un identificador de seguimiento que habilita el seguimiento los diagnósticos de un extremo a otro de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="67c83-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="67c83-125">Hola `token` valor es opcional y solo debe usarse cuando no es posible toosend HTTP encabezados junto con el protocolo de enlace de WebSocket de hello, como sucede Hola con la pila de W3C WebSocket Hola.</span><span class="sxs-lookup"><span data-stu-id="67c83-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="67c83-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="67c83-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="67c83-127">Crea un envío de conexión híbrida de Azure retransmisión URI válido para hello tiene espacio de nombres y la ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="67c83-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="67c83-128">Este URI se puede utilizar con cualquier cliente de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="67c83-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="67c83-129">`namespaceName`(obligatorio): Hola nombre completo del dominio de toouse de espacio de nombres de hello retransmisión de Azure.</span><span class="sxs-lookup"><span data-stu-id="67c83-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="67c83-130">`path`(obligatorio): Hola el nombre de una conexión de retransmisión híbrida de Azure existente en ese espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="67c83-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="67c83-131">`token`enviar un token de acceso de retransmisión emitido previamente que está incrustado en hello (opcional): URI (vea el siguiente ejemplo de Hola).</span><span class="sxs-lookup"><span data-stu-id="67c83-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="67c83-132">`id` (opcional): un identificador de seguimiento que habilita el seguimiento los diagnósticos de un extremo a otro de las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="67c83-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="67c83-133">Hola `token` valor es opcional y solo debe usarse cuando no es posible toosend HTTP encabezados junto con el protocolo de enlace de WebSocket de hello, como sucede Hola con la pila de W3C WebSocket Hola.</span><span class="sxs-lookup"><span data-stu-id="67c83-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="67c83-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="67c83-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="67c83-135">Crea un token de firma de acceso compartido de Azure retransmisión (SAS) para URI de destino de hello dada, reglas SAS y clave de regla SAS que es válida para hello proporcionada instantánea número de segundos o durante una hora desde Hola actual si se omite el argumento de expiración de Hola.</span><span class="sxs-lookup"><span data-stu-id="67c83-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="67c83-136">`uri`(obligatorio): Hola URI para qué hello símbolo (token) se toobe emitido.</span><span class="sxs-lookup"><span data-stu-id="67c83-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="67c83-137">Hola URI es el esquema HTTP de Hola de toouse normalizado y se extrae la información de la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="67c83-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="67c83-138">`ruleName`(obligatorio): nombre de cualquier entidad de hello representada por hello dado URI de regla de SAS o para hello espacio de nombres representado por hello parte de host URI.</span><span class="sxs-lookup"><span data-stu-id="67c83-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="67c83-139">`key`(obligatorio): una clave válida para la regla SAS de Hola.</span><span class="sxs-lookup"><span data-stu-id="67c83-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="67c83-140">`expirationSeconds`(opcional): número de Hola de segundos hasta que Hola genere símbolo (token) debe expirar.</span><span class="sxs-lookup"><span data-stu-id="67c83-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="67c83-141">Si no se especifica, valor predeterminado de hello es 1 hora (3600).</span><span class="sxs-lookup"><span data-stu-id="67c83-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="67c83-142">símbolo (token) de Hello emitido confiere derechos de hello asociados con hello especificado reglas SAS para hello dada duración.</span><span class="sxs-lookup"><span data-stu-id="67c83-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="67c83-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="67c83-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="67c83-144">Este método es funcionalmente equivalente toohello `createRelayToken` método documentado anteriormente, pero devuelve Hola proporcionados por el token toohello correctamente anexados URI.</span><span class="sxs-lookup"><span data-stu-id="67c83-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="67c83-145">Clase ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="67c83-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="67c83-146">Hola `hycows.RelayedServer` clase es una alternativa toohello `ws.Server` clase que no escucha en la red local de hello, pero delega escucha toohello servicio de retransmisión de Azure.</span><span class="sxs-lookup"><span data-stu-id="67c83-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="67c83-147">las clases de Hello dos son principalmente contrato compatible, lo que significa que una aplicación existente mediante hello `ws.Server` clase puede ser fácilmente versión de Hola retransmitida toouse modificada.</span><span class="sxs-lookup"><span data-stu-id="67c83-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="67c83-148">diferencias principales de Hello están en el constructor de Hola y en las opciones disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="67c83-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="67c83-149">Constructor</span><span class="sxs-lookup"><span data-stu-id="67c83-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="67c83-150">Hola `RelayedServer` constructor es compatible con un conjunto diferente de argumentos que hello `Server`, porque no es un agente de escucha independientes o toobe puede incrustarse en un marco de trabajo del agente de escucha HTTP existente.</span><span class="sxs-lookup"><span data-stu-id="67c83-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="67c83-151">También hay tantas opciones disponibles ya Hola administración WebSocket es en gran medida delegado toohello servicio de retransmisión.</span><span class="sxs-lookup"><span data-stu-id="67c83-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="67c83-152">Argumentos del constructor:</span><span class="sxs-lookup"><span data-stu-id="67c83-152">Constructor arguments:</span></span>

- <span data-ttu-id="67c83-153">`server`(obligatorio): Hola completo URI con un nombre de conexión híbrida en qué toolisten, normalmente se construye con hello WebSocket.createRelayListenUri() método de aplicación auxiliar.</span><span class="sxs-lookup"><span data-stu-id="67c83-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="67c83-154">`token`(obligatorio): este argumento contiene una cadena de tokens emitida previamente o una función de devolución de llamada que se puede llamar tooobtain esta cadena de token.</span><span class="sxs-lookup"><span data-stu-id="67c83-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="67c83-155">opción de devolución de llamada de Hello es preferible, puesto que permite la renovación del token.</span><span class="sxs-lookup"><span data-stu-id="67c83-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="67c83-156">Eventos</span><span class="sxs-lookup"><span data-stu-id="67c83-156">Events</span></span>

<span data-ttu-id="67c83-157">`RelayedServer`instancias emiten tres eventos que permiten toohandle las solicitudes entrantes, establecen conexiones y detectan las condiciones de error.</span><span class="sxs-lookup"><span data-stu-id="67c83-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="67c83-158">Debe suscribirse toohello `connect` toohandle mensajes de eventos.</span><span class="sxs-lookup"><span data-stu-id="67c83-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="67c83-159">encabezados</span><span class="sxs-lookup"><span data-stu-id="67c83-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="67c83-160">Hola `headers` evento se produce justo antes de que se acepta una conexión entrante, habilitar la modificación de cliente de hello encabezados toosend toohello.</span><span class="sxs-lookup"><span data-stu-id="67c83-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="67c83-161">connection</span><span class="sxs-lookup"><span data-stu-id="67c83-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="67c83-162">Se emite cuando se acepta una nueva conexión de WebSocket.</span><span class="sxs-lookup"><span data-stu-id="67c83-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="67c83-163">objeto de Hello es de tipo `ws.WebSocket`, igual que con el paquete básico de Hola.</span><span class="sxs-lookup"><span data-stu-id="67c83-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="67c83-164">error</span><span class="sxs-lookup"><span data-stu-id="67c83-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="67c83-165">Si servidor subyacente Hola emite un error, se reenvía a continuación.</span><span class="sxs-lookup"><span data-stu-id="67c83-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="67c83-166">Aplicaciones auxiliares</span><span class="sxs-lookup"><span data-stu-id="67c83-166">Helpers</span></span>

<span data-ttu-id="67c83-167">a partir de un servidor retransmitido e inmediatamente suscribiéndose tooincoming conexiones, hello paquete toosimplify expone una función auxiliar sencilla, que también se utiliza en los ejemplos de hello, como sigue:</span><span class="sxs-lookup"><span data-stu-id="67c83-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="67c83-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="67c83-168">createRelayedListener</span></span>

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

##### <a name="createrelayedserver"></a><span data-ttu-id="67c83-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="67c83-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="67c83-170">Este método llama a una nueva instancia de hello RelayedServer Hola constructor toocreate y, a continuación, suscribe a eventos de toohello "conexión" de devolución de llamada de hello proporciona.</span><span class="sxs-lookup"><span data-stu-id="67c83-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="67c83-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="67c83-171">relayedConnect</span></span>

<span data-ttu-id="67c83-172">Basta con creación de reflejo de hello `createRelayedServer` auxiliares en función, `relayedConnect` crea una conexión de cliente y se suscribe toohello evento 'open' en el socket de hello resultante.</span><span class="sxs-lookup"><span data-stu-id="67c83-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="67c83-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="67c83-173">Next steps</span></span>
<span data-ttu-id="67c83-174">toolearn más información acerca de la retransmisión de Azure, visite estos vínculos:</span><span class="sxs-lookup"><span data-stu-id="67c83-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="67c83-175">¿Qué es Relay de Azure?</span><span class="sxs-lookup"><span data-stu-id="67c83-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* <span data-ttu-id="67c83-176">[Available Relay APIs ](relay-api-overview.md) (API de Relay disponibles)</span><span class="sxs-lookup"><span data-stu-id="67c83-176">[Available Relay APIs](relay-api-overview.md)</span></span>
