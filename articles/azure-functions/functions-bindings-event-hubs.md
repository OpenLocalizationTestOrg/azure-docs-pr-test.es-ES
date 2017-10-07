---
title: enlaces de centros de eventos de funciones aaaAzure | Documentos de Microsoft
description: "Comprender cómo toouse enlaces de centros de eventos de Azure en las funciones de Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a>Enlaces de Event Hubs de Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo se explica cómo tooconfigure y usar [centros de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md) enlaces para las funciones de Azure.
Azure Functions admite enlaces de desencadenador y salida para Event Hubs.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Si es nuevo centros de eventos de tooAzure, vea hello [información general de los centros de eventos](../event-hubs/event-hubs-what-is-event-hubs.md).

<a name="trigger"></a>

## <a name="event-hub-trigger"></a>Desencadenador de centro de eventos
Los concentradores de eventos de uso Hola desencadenar toorespond tooan eventos enviado la secuencia de eventos de concentrador de eventos de tooan. Debe tener el concentrador de eventos de acceso de lectura toohello tooset seguridad desencadenador Hola.

desencadenador de función de los centros de eventos de Hello usa Hola siguiente objeto JSON en hello `bindings` matriz de function.json:

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

`consumerGroup`es un hello de propiedad opcional que se utiliza tooset [grupo de consumidores](../event-hubs/event-hubs-features.md#event-consumers) utiliza toosubscribe tooevents en el concentrador de Hola. Si se omite, Hola `$Default` se utiliza el grupo de consumidores.  
`connection`debe ser el nombre de Hola de una configuración de aplicación que contiene el espacio de nombres del centro de hello conexión cadena toohello eventos.
Copie esta cadena de conexión, haga clic en hello **información de conexión** botón para hello *espacio de nombres*, no concentrador de eventos de hello propio. Esta cadena de conexión debe tener al menos de lectura desencadenador de hello tooactivate de permisos.

[Opciones de configuración adicionales](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) puede proporcionarse en un host.json archivo toofurther bien optimiza los desencadenadores de los centros de eventos.  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Uso del desencadenador
Cuando se activa una función de activación de los centros de eventos, mensajes de Hola que lo activa se pasan a función hello como una cadena.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Ejemplo de desencadenador
Suponga que tiene Hola siguientes centros de eventos se desencadenan en hello `bindings` matriz de function.json:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Vea el ejemplo de específica del lenguaje de Hola que registra el cuerpo del mensaje Hola de desencadenador de concentrador de eventos de Hola.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Ejemplo de desencadenador en C# #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

También puede recibir eventos de Hola como un [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) objeto, que proporciona acceso a metadatos de evento toohello.

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

tooreceive eventos en un lote, cambiar la firma de método hello demasiado`string[]` o `EventData[]`.

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Ejemplo de desencadenador en F# #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Ejemplo de desencadenador en Node.js

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a>Enlace de salida de Event Hubs
Hola usar centros de eventos de salida flujo de eventos del concentrador de eventos de enlace toowrite eventos tooan. Debe tener envío permiso tooan evento concentrador toowrite eventos tooit.

enlace de salida Hello usa Hola siguiente objeto JSON en hello `bindings` matriz de function.json:

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

`connection`debe ser el nombre de Hola de una configuración de aplicación que contiene el espacio de nombres del centro de hello conexión cadena toohello eventos.
Copie esta cadena de conexión, haga clic en hello **información de conexión** botón para hello *espacio de nombres*, no concentrador de eventos de hello propio. Esta cadena de conexión debe tener el flujo de eventos del toohello de mensaje de envío permisos toosend Hola.

## <a name="output-usage"></a>Uso de salidas
Esta sección muestra cómo toouse sus centros de eventos de salida en el código de función de enlace.

Puede generar el concentrador de eventos de mensajes toohello configurado con hello siguientes tipos de parámetro:

* `out string`
* `ICollector<string>`(toooutput varios mensajes)
* `IAsyncCollector<string>` (versión asincrónica de `ICollector<T>`)

<a name="outputsample"></a>

## <a name="output-sample"></a>Ejemplo de salida
Imagine que tiene Hola siguientes centros de eventos de salida enlace Hola `bindings` matriz de function.json:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Vea ejemplo de Hola a específicos del idioma que se escribe una secuencia de eventos de toohello incluso.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Ejemplo de salida en C# #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

O bien, toocreate varios mensajes:

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Ejemplo de salida en F# #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a>Ejemplo de salida de Node.js

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

O bien, toosend varios mensajes,

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
