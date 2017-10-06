---
title: aaaAzure funciones Service Bus desencadenadores y enlaces | Documentos de Microsoft
description: "Comprender cómo se desencadena toouse Service Bus de Azure y los enlaces de funciones de Azure."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a>Enlaces de Service Bus en Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo se explica cómo tooconfigure y trabajar con enlaces de Bus de servicio de Azure en las funciones de Azure. 

Azure Functions admite enlaces de desencadenador y salida para colas y temas de Service Bus.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a>Desencadenador de Service Bus
Utilice Hola Service Bus desencadenador toorespond toomessages desde una cola de Bus de servicio o un tema. 

Hello desencadenadores queue y topic de Bus de servicio definidos por hello siguientes objetos JSON en hello `bindings` matriz de function.json:

* Desencadenador de *cola*:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* Desencadenador de *tema*:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

Tenga en cuenta los siguiente hello:

* Para `connection`, [crear una configuración de aplicación en la aplicación de la función](functions-how-to-use-azure-function-app-settings.md) que contiene nombres de Bus de servicio de tooyour de cadena de conexión de hello, a continuación, especifique el nombre de Hola de configuración de la aplicación Hola Hola `connection` propiedad en el desencadenador. Obtener cadena de conexión de hello siguiendo los pasos de Hola se muestra en [obtener credenciales de administración de hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  cadena de conexión de Hello debe ser de espacio de nombres, cola específica de tooa no limita o tema de Bus de servicio.
  Si deja `connection` vacía, el desencadenador de Hola se da por supuesto que se especifica una cadena de conexión de Bus de servicio de manera predeterminada en una aplicación de configuración con nombre `AzureWebJobsServiceBus`.
* Para `accessRights`, los valores disponibles son `manage` y `listen`. valor predeterminado de Hello es `manage`, lo que indica que hello `connection` tiene hello **administrar** permiso. Si usa una cadena de conexión que no tiene hello **administrar** de conjunto de permisos, `accessRights` demasiado`listen`. De lo contrario, las funciones de hello en tiempo de ejecución puede producir un error tratar las operaciones de toodo que requieren derechos de administración.

## <a name="trigger-behavior"></a>Comportamiento de un desencadenador
* **Subprocesamiento único** : de forma predeterminada, los procesos del runtime de funciones hello simultáneamente varios mensajes. establecer toodirect hello en tiempo de ejecución tooprocess solo una única cola o tema mensaje a la vez, `serviceBus.maxConcurrentCalls` too1 en *host.json*. 
  Para más información acerca de *host.json*, consulte [Estructura de carpetas](functions-reference.md#folder-structure) y [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).
* **Gestión de mensajes dudosos**: Service Bus realiza su propio tratamiento de mensajes dudosos, que no se puede controlar ni configurar en el código ni en la configuración de Azure Functions. 
* **Comportamiento de PeekLock** -en tiempo de ejecución de funciones de hello recibe un mensaje en [ `PeekLock` modo](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) y llamadas `Complete` en el mensaje de bienvenida de si la función hello finaliza correctamente, o llamadas a `Abandon` si hello se produce un error en la función. 
  Si se ejecuta más de hello función hello `PeekLock` tiempo de espera de bloqueo de Hola se renovará automáticamente.

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Uso del desencadenador
Esta sección muestra cómo toouse el Bus de servicio desencadenar en el código de función. 

En C# y F #, mensaje de bienvenida de desencadenador de Bus de servicio puede ser deserializado tooany de hello siguientes tipos de entrada:

* `string`: útil para mensajes de cadena
* `byte[]`: útil para datos binarios
* Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para datos serializados mediante JSON.
  Si se declara un tipo de entrada personalizado, como `CustomType`, las funciones de Azure intenta datos JSON de toodeserialize hello en el tipo especificado.
* `BrokeredMessage`-Proporciona Hola deserializa el mensaje con hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) (método).

En Node.js, mensajes de bienvenida del Bus de servicio desencadenador se pasan a la función hello como una cadena o un objeto JSON.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Ejemplo de desencadenador
Suponga que tiene Hola siguientes function.json:

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

Vea el ejemplo específico del idioma de Hola que procesa un mensaje de cola de Bus de servicio.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Ejemplo de desencadenador en C# #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Ejemplo de desencadenador en F# #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Ejemplo de desencadenador en Node.js

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a>Enlace de salida de Service Bus
Hola salida queue y topic de Bus de servicio para una función usar hello siguientes objetos JSON en hello `bindings` matriz de function.json:

* Salida de *cola*:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* Salida de *tema*:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

Tenga en cuenta los siguiente hello:

* Para `connection`, [crear una configuración de aplicación en la aplicación de la función](functions-how-to-use-azure-function-app-settings.md) que contiene nombres de Bus de servicio de tooyour de cadena de conexión de hello, a continuación, especifique el nombre de Hola de configuración de la aplicación Hola Hola `connection` propiedad en el resultado enlace. Obtener cadena de conexión de hello siguiendo los pasos de Hola se muestra en [obtener credenciales de administración de hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  cadena de conexión de Hello debe ser de espacio de nombres, cola específica de tooa no limita o tema de Bus de servicio.
  Si deja `connection` vacía, hello enlace de salida se da por supuesto que se especifica una cadena de conexión de Bus de servicio de manera predeterminada en una aplicación de configuración con nombre `AzureWebJobsServiceBus`.
* Para `accessRights`, los valores disponibles son `manage` y `listen`. valor predeterminado de Hello es `manage`, lo que indica que hello `connection` tiene hello **administrar** permiso. Si usa una cadena de conexión que no tiene hello **administrar** de conjunto de permisos, `accessRights` demasiado`listen`. De lo contrario, las funciones de hello en tiempo de ejecución puede producir un error tratar las operaciones de toodo que requieren derechos de administración.

<a name="outputusage"></a>

## <a name="output-usage"></a>Uso de salidas
En C# y F #, las funciones de Azure puede crear un mensaje de cola de Bus de servicio desde cualquiera de los siguientes tipos de hello:

* Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): la definición de parámetro es similar a `out T paramName` (C#).
  Funciones deserializa el objeto de hello en un mensaje JSON. Si el valor de salida de hello es nulo cuando sale de la función hello, funciones crea mensajes de bienvenida con un objeto null.
* `string`: la definición de parámetro es similar a `out string paraName` (C#). Si el valor del parámetro hello es distinto de null cuando sale de la función hello, funciones crea un mensaje.
* `byte[]`: la definición de parámetro es similar a `out byte[] paraName` (C#). Si el valor del parámetro hello es distinto de null cuando sale de la función hello, funciones crea un mensaje.
* `BrokeredMessage`: la definición de parámetro es similar a `out BrokeredMessage paraName` (C#). Si el valor del parámetro hello es distinto de null cuando sale de la función hello, funciones crea un mensaje.

Para crear varios mensajes en una función de C#, puede utilizar `ICollector<T>` o `IAsyncCollector<T>`. Se crea un mensaje cuando se llama a hello `Add` método.

En Node.js, puede asignar una cadena, una matriz de bytes o un objeto de Javascript (deserializada en JSON) demasiado`context.binding.<paramName>`.

<a name="outputsample"></a>

## <a name="output-sample"></a>Ejemplo de salida
Suponga que tiene Hola después function.json, que define una salida de cola de Bus de servicio:

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

Vea el ejemplo de específica del lenguaje de Hola que envía a una cola de bus de servicio de toohello de mensajes.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Ejemplo de salida en C# #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

O bien, toocreate varios mensajes:

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Ejemplo de salida en F# #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Ejemplo de salida en Node.js

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

O bien, toocreate varios mensajes:

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

