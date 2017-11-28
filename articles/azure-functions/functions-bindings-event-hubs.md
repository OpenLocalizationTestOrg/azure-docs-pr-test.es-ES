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
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="cf6e7-104">Enlaces de Event Hubs de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cf6e7-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="cf6e7-105">Este artículo se explica cómo tooconfigure y usar [centros de eventos de Azure](../event-hubs/event-hubs-what-is-event-hubs.md) enlaces para las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-105">This article explains how tooconfigure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="cf6e7-106">Azure Functions admite enlaces de desencadenador y salida para Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="cf6e7-107">Si es nuevo centros de eventos de tooAzure, vea hello [información general de los centros de eventos](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="cf6e7-107">If you are new tooAzure Event Hubs, see hello [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="cf6e7-108">Desencadenador de centro de eventos</span><span class="sxs-lookup"><span data-stu-id="cf6e7-108">Event hub trigger</span></span>
<span data-ttu-id="cf6e7-109">Los concentradores de eventos de uso Hola desencadenar toorespond tooan eventos enviado la secuencia de eventos de concentrador de eventos de tooan.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-109">Use hello Event Hubs trigger toorespond tooan event sent tooan event hub event stream.</span></span> <span data-ttu-id="cf6e7-110">Debe tener el concentrador de eventos de acceso de lectura toohello tooset seguridad desencadenador Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-110">You must have read access toohello event hub tooset up hello trigger.</span></span>

<span data-ttu-id="cf6e7-111">desencadenador de función de los centros de eventos de Hello usa Hola siguiente objeto JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="cf6e7-111">hello Event Hubs function trigger uses hello following JSON object in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="cf6e7-112">`consumerGroup`es un hello de propiedad opcional que se utiliza tooset [grupo de consumidores](../event-hubs/event-hubs-features.md#event-consumers) utiliza toosubscribe tooevents en el concentrador de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-112">`consumerGroup` is an optional property used tooset hello [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used toosubscribe tooevents in hello hub.</span></span> <span data-ttu-id="cf6e7-113">Si se omite, Hola `$Default` se utiliza el grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-113">If omitted, hello `$Default` consumer group is used.</span></span>  
<span data-ttu-id="cf6e7-114">`connection`debe ser el nombre de Hola de una configuración de aplicación que contiene el espacio de nombres del centro de hello conexión cadena toohello eventos.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-114">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="cf6e7-115">Copie esta cadena de conexión, haga clic en hello **información de conexión** botón para hello *espacio de nombres*, no concentrador de eventos de hello propio.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-115">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="cf6e7-116">Esta cadena de conexión debe tener al menos de lectura desencadenador de hello tooactivate de permisos.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-116">This connection string must have at least read permissions tooactivate hello trigger.</span></span>

<span data-ttu-id="cf6e7-117">[Opciones de configuración adicionales](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) puede proporcionarse en un host.json archivo toofurther bien optimiza los desencadenadores de los centros de eventos.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file toofurther fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="cf6e7-118">Uso del desencadenador</span><span class="sxs-lookup"><span data-stu-id="cf6e7-118">Trigger usage</span></span>
<span data-ttu-id="cf6e7-119">Cuando se activa una función de activación de los centros de eventos, mensajes de Hola que lo activa se pasan a función hello como una cadena.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-119">When an Event Hubs trigger function is triggered, hello message that triggers it is passed into hello function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="cf6e7-120">Ejemplo de desencadenador</span><span class="sxs-lookup"><span data-stu-id="cf6e7-120">Trigger sample</span></span>
<span data-ttu-id="cf6e7-121">Suponga que tiene Hola siguientes centros de eventos se desencadenan en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="cf6e7-121">Suppose you have hello following Event Hubs trigger in hello `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="cf6e7-122">Vea el ejemplo de específica del lenguaje de Hola que registra el cuerpo del mensaje Hola de desencadenador de concentrador de eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-122">See hello language-specific sample that logs hello message body of hello event hub trigger.</span></span>

* [<span data-ttu-id="cf6e7-123">C#</span><span class="sxs-lookup"><span data-stu-id="cf6e7-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="cf6e7-124">F#</span><span class="sxs-lookup"><span data-stu-id="cf6e7-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="cf6e7-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="cf6e7-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="cf6e7-126">Ejemplo de desencadenador en C#</span><span class="sxs-lookup"><span data-stu-id="cf6e7-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="cf6e7-127">También puede recibir eventos de Hola como un [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) objeto, que proporciona acceso a metadatos de evento toohello.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-127">You can also receive hello event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access toohello event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="cf6e7-128">tooreceive eventos en un lote, cambiar la firma de método hello demasiado`string[]` o `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-128">tooreceive events in a batch, change hello method signature too`string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="cf6e7-129">Ejemplo de desencadenador en F#</span><span class="sxs-lookup"><span data-stu-id="cf6e7-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="cf6e7-130">Ejemplo de desencadenador en Node.js</span><span class="sxs-lookup"><span data-stu-id="cf6e7-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="cf6e7-131">Enlace de salida de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cf6e7-131">Event Hubs output binding</span></span>
<span data-ttu-id="cf6e7-132">Hola usar centros de eventos de salida flujo de eventos del concentrador de eventos de enlace toowrite eventos tooan.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-132">Use hello Event Hubs output binding toowrite events tooan event hub event stream.</span></span> <span data-ttu-id="cf6e7-133">Debe tener envío permiso tooan evento concentrador toowrite eventos tooit.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-133">You must have send permission tooan event hub toowrite events tooit.</span></span>

<span data-ttu-id="cf6e7-134">enlace de salida Hello usa Hola siguiente objeto JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="cf6e7-134">hello output binding uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="cf6e7-135">`connection`debe ser el nombre de Hola de una configuración de aplicación que contiene el espacio de nombres del centro de hello conexión cadena toohello eventos.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-135">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="cf6e7-136">Copie esta cadena de conexión, haga clic en hello **información de conexión** botón para hello *espacio de nombres*, no concentrador de eventos de hello propio.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-136">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="cf6e7-137">Esta cadena de conexión debe tener el flujo de eventos del toohello de mensaje de envío permisos toosend Hola.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-137">This connection string must have send permissions toosend hello message toohello event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="cf6e7-138">Uso de salidas</span><span class="sxs-lookup"><span data-stu-id="cf6e7-138">Output usage</span></span>
<span data-ttu-id="cf6e7-139">Esta sección muestra cómo toouse sus centros de eventos de salida en el código de función de enlace.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-139">This section shows you how toouse your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="cf6e7-140">Puede generar el concentrador de eventos de mensajes toohello configurado con hello siguientes tipos de parámetro:</span><span class="sxs-lookup"><span data-stu-id="cf6e7-140">You can output messages toohello configured event hub with hello following parameter types:</span></span>

* `out string`
* <span data-ttu-id="cf6e7-141">`ICollector<string>`(toooutput varios mensajes)</span><span class="sxs-lookup"><span data-stu-id="cf6e7-141">`ICollector<string>` (toooutput multiple messages)</span></span>
* <span data-ttu-id="cf6e7-142">`IAsyncCollector<string>` (versión asincrónica de `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="cf6e7-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="cf6e7-143">Ejemplo de salida</span><span class="sxs-lookup"><span data-stu-id="cf6e7-143">Output sample</span></span>
<span data-ttu-id="cf6e7-144">Imagine que tiene Hola siguientes centros de eventos de salida enlace Hola `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="cf6e7-144">Suppose you have hello following Event Hubs output binding in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="cf6e7-145">Vea ejemplo de Hola a específicos del idioma que se escribe una secuencia de eventos de toohello incluso.</span><span class="sxs-lookup"><span data-stu-id="cf6e7-145">See hello language-specific sample that writes an event toohello even stream.</span></span>

* [<span data-ttu-id="cf6e7-146">C#</span><span class="sxs-lookup"><span data-stu-id="cf6e7-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="cf6e7-147">F#</span><span class="sxs-lookup"><span data-stu-id="cf6e7-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="cf6e7-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="cf6e7-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="cf6e7-149">Ejemplo de salida en C#</span><span class="sxs-lookup"><span data-stu-id="cf6e7-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="cf6e7-150">O bien, toocreate varios mensajes:</span><span class="sxs-lookup"><span data-stu-id="cf6e7-150">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="cf6e7-151">Ejemplo de salida en F#</span><span class="sxs-lookup"><span data-stu-id="cf6e7-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="cf6e7-152">Ejemplo de salida de Node.js</span><span class="sxs-lookup"><span data-stu-id="cf6e7-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="cf6e7-153">O bien, toosend varios mensajes,</span><span class="sxs-lookup"><span data-stu-id="cf6e7-153">Or, toosend multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cf6e7-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf6e7-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
