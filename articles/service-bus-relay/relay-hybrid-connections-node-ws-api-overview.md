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
# <a name="relay-hybrid-connections-node-api-overview"></a>Introducción a las API de Node para conexiones híbridas de Relay

## <a name="overview"></a>Información general

Hola [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) paquete de nodo para las conexiones híbridas de retransmisión de Azure se basa y extiende hello ['ws'](https://www.npmjs.com/package/ws) paquete NPM. Este paquete volver a exporta todas las exportaciones de ese paquete base y agrega nuevas exportaciones que habilitar la integración con la característica de conexiones híbridas del servicio de retransmisión de Azure de Hola. 

Las aplicaciones existentes que `require('ws')` puede usar este paquete con `require('hyco-ws')` en su lugar, lo que también permite escenarios híbridos en el que una aplicación puede escuchar para las conexiones de WebSocket localmente desde "dentro del firewall de hello" y a través de conexiones híbridas, todo en el Hola mismo tiempo.
  
## <a name="documentation"></a>Documentación

Hello API son [documentados en el paquete de principal 'ws' hello](https://github.com/websockets/ws/blob/master/doc/ws.md). En este artículo se describe la diferencia de este paquete con esa línea de base. 

Hola diferencias principales entre el paquete básico de Hola y esta 'hyco-ws' es que agrega una nueva clase de servidor exportada mediante `require('hyco-ws').RelayedServer`y varios métodos auxiliares.

### <a name="package-helper-methods"></a>Métodos auxiliares del paquete

Hay varios métodos de utilidad durante la exportación de paquete de Hola que puede hacer referencia como sigue:

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

métodos de aplicación auxiliar de Hello son para su uso con este paquete, pero también pueden utilizarse un servidor de nodo para habilitar web o dispositivo clientes toocreate los agentes de escucha o remitentes. servidor de Hello usa estos métodos pasándolos URI que inserte tokens de corta duración. Estos URI también se pueden usar con pilas de WebSocket común que no admiten establecer los encabezados HTTP para el protocolo de enlace de hello WebSocket. La incorporación de tokens de autorización en hello que URI se admite principalmente para los escenarios de uso de biblioteca externa. 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

Crea una escucha de conexión híbrida de Azure retransmisión URI válida para hello tiene espacio de nombres y la ruta de acceso. Este URI, a continuación, puede utilizarse con la versión de retransmisión de Hola de hello WebSocketServer clase.

- `namespaceName`(obligatorio): Hola nombre completo del dominio de toouse de espacio de nombres de hello retransmisión de Azure.
- `path`(obligatorio): Hola el nombre de una conexión de retransmisión híbrida de Azure existente en ese espacio de nombres.
- `token`(opcional): un acceso de retransmisión emitido previamente símbolo (token) que está incrustada en el agente de escucha de hello URI (vea el siguiente ejemplo de Hola).
- `id` (opcional): un identificador de seguimiento que habilita el seguimiento los diagnósticos de un extremo a otro de las solicitudes.

Hola `token` valor es opcional y solo debe usarse cuando no es posible toosend HTTP encabezados junto con el protocolo de enlace de WebSocket de hello, como sucede Hola con la pila de W3C WebSocket Hola.                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

Crea un envío de conexión híbrida de Azure retransmisión URI válido para hello tiene espacio de nombres y la ruta de acceso. Este URI se puede utilizar con cualquier cliente de WebSocket.

- `namespaceName`(obligatorio): Hola nombre completo del dominio de toouse de espacio de nombres de hello retransmisión de Azure.
- `path`(obligatorio): Hola el nombre de una conexión de retransmisión híbrida de Azure existente en ese espacio de nombres.
- `token`enviar un token de acceso de retransmisión emitido previamente que está incrustado en hello (opcional): URI (vea el siguiente ejemplo de Hola).
- `id` (opcional): un identificador de seguimiento que habilita el seguimiento los diagnósticos de un extremo a otro de las solicitudes.

Hola `token` valor es opcional y solo debe usarse cuando no es posible toosend HTTP encabezados junto con el protocolo de enlace de WebSocket de hello, como sucede Hola con la pila de W3C WebSocket Hola.                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Crea un token de firma de acceso compartido de Azure retransmisión (SAS) para URI de destino de hello dada, reglas SAS y clave de regla SAS que es válida para hello proporcionada instantánea número de segundos o durante una hora desde Hola actual si se omite el argumento de expiración de Hola.

- `uri`(obligatorio): Hola URI para qué hello símbolo (token) se toobe emitido. Hola URI es el esquema HTTP de Hola de toouse normalizado y se extrae la información de la cadena de consulta.
- `ruleName`(obligatorio): nombre de cualquier entidad de hello representada por hello dado URI de regla de SAS o para hello espacio de nombres representado por hello parte de host URI.
- `key`(obligatorio): una clave válida para la regla SAS de Hola. 
- `expirationSeconds`(opcional): número de Hola de segundos hasta que Hola genere símbolo (token) debe expirar. Si no se especifica, valor predeterminado de hello es 1 hora (3600).

símbolo (token) de Hello emitido confiere derechos de hello asociados con hello especificado reglas SAS para hello dada duración.

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Este método es funcionalmente equivalente toohello `createRelayToken` método documentado anteriormente, pero devuelve Hola proporcionados por el token toohello correctamente anexados URI.

### <a name="class-wsrelayedserver"></a>Clase ws.RelayedServer

Hola `hycows.RelayedServer` clase es una alternativa toohello `ws.Server` clase que no escucha en la red local de hello, pero delega escucha toohello servicio de retransmisión de Azure.

las clases de Hello dos son principalmente contrato compatible, lo que significa que una aplicación existente mediante hello `ws.Server` clase puede ser fácilmente versión de Hola retransmitida toouse modificada. diferencias principales de Hello están en el constructor de Hola y en las opciones disponibles de Hola.

#### <a name="constructor"></a>Constructor  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

Hola `RelayedServer` constructor es compatible con un conjunto diferente de argumentos que hello `Server`, porque no es un agente de escucha independientes o toobe puede incrustarse en un marco de trabajo del agente de escucha HTTP existente. También hay tantas opciones disponibles ya Hola administración WebSocket es en gran medida delegado toohello servicio de retransmisión.

Argumentos del constructor:

- `server`(obligatorio): Hola completo URI con un nombre de conexión híbrida en qué toolisten, normalmente se construye con hello WebSocket.createRelayListenUri() método de aplicación auxiliar.
- `token`(obligatorio): este argumento contiene una cadena de tokens emitida previamente o una función de devolución de llamada que se puede llamar tooobtain esta cadena de token. opción de devolución de llamada de Hello es preferible, puesto que permite la renovación del token.

#### <a name="events"></a>Eventos

`RelayedServer`instancias emiten tres eventos que permiten toohandle las solicitudes entrantes, establecen conexiones y detectan las condiciones de error. Debe suscribirse toohello `connect` toohandle mensajes de eventos. 

##### <a name="headers"></a>encabezados

```JavaScript 
function(headers)
```

Hola `headers` evento se produce justo antes de que se acepta una conexión entrante, habilitar la modificación de cliente de hello encabezados toosend toohello. 

##### <a name="connection"></a>connection

```JavaScript
function(socket)
```

Se emite cuando se acepta una nueva conexión de WebSocket. objeto de Hello es de tipo `ws.WebSocket`, igual que con el paquete básico de Hola.


##### <a name="error"></a>error

```JavaScript
function(error)
```

Si servidor subyacente Hola emite un error, se reenvía a continuación.  

#### <a name="helpers"></a>Aplicaciones auxiliares

a partir de un servidor retransmitido e inmediatamente suscribiéndose tooincoming conexiones, hello paquete toosimplify expone una función auxiliar sencilla, que también se utiliza en los ejemplos de hello, como sigue:

##### <a name="createrelayedlistener"></a>createRelayedListener

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

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

Este método llama a una nueva instancia de hello RelayedServer Hola constructor toocreate y, a continuación, suscribe a eventos de toohello "conexión" de devolución de llamada de hello proporciona.
 
##### <a name="relayedconnect"></a>relayedConnect

Basta con creación de reflejo de hello `createRelayedServer` auxiliares en función, `relayedConnect` crea una conexión de cliente y se suscribe toohello evento 'open' en el socket de hello resultante.

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

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de la retransmisión de Azure, visite estos vínculos:
* [¿Qué es Relay de Azure?](relay-what-is-it.md)
* [Available Relay APIs ](relay-api-overview.md) (API de Relay disponibles)
