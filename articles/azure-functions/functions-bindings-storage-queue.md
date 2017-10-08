---
title: enlaces de almacenamiento de cola de funciones aaaAzure | Documentos de Microsoft
description: "Comprender cómo se desencadena toouse almacenamiento de Azure y los enlaces de funciones de Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a>Enlaces de Queue Storage en Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo se describe cómo tooconfigure y el código de enlaces de almacenamiento de cola de Azure en las funciones de Azure. Azure Functions admite desencadenador y enlaces de salida para Azure Queues. Para las características que estén disponibles en todos los enlaces, consulte [conceptos sobre desencadenadores y enlaces de Azure Functions](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a>Desencadenador de Queue Storage
desencadenador de almacenamiento de cola de Azure de Hello permite toomonitor un almacenamiento de cola si hay mensajes nuevos y reacciona toothem. 

Definir un desencadenador de cola mediante hello **integrar** Hola funciones portal de. portal de Hello crea Hola después de la definición de hello **enlaces** sección de *function.json*:

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* Hola `connection` propiedad debe contener el nombre de Hola de una configuración de aplicación que contiene una cadena de conexión de almacenamiento. Hola portal de Azure, Hola editor estándar en hello **integrar** ficha configura esta configuración de aplicación para cuando se selecciona una cuenta de almacenamiento.

Puede proporcionar una configuración adicional en un [host.json archivo](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther ajustar desencadenadores de almacenamiento de cola. Por ejemplo, puede cambiar el intervalo de sondeo de la cola de hello en host.json.

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a>Uso de un desencadenador de cola
En las funciones de Node.js, tener acceso a Hola cola datos mediante `context.bindings.<name>`.


En las funciones. NET, tener acceso a la carga de la cola de hello mediante un parámetro de método como `CloudQueueMessage paramName`. En este caso, `paramName` es valor Hola especificado en hello [configuración de desencadenador](#trigger). mensaje de bienvenida de cola puede ser deserializado tooany de hello siguientes tipos:

* Objeto POCO. Usar si la carga de la cola de hello es un objeto JSON. en tiempo de ejecución de funciones de Hello deserializa carga hello en el objeto POCO Hola. 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>Metadatos de desencadenador de cola
desencadenador de cola de Hello proporciona varias propiedades de metadatos. Estas propiedades pueden usarse como parte de expresiones de enlace en otros enlaces o como parámetros del código. los valores de Hello tienen Hola misma semántica que [ `CloudQueueMessage` ].

* **QueueTrigger**: carga de cola (si hay una cadena válida)
* **DequeueCount**: escriba `int`. Hola número de veces que este mensaje se ha quitado de la cola.
* **ExpirationTime**: escriba `DateTimeOffset?`. tiempo de Hello ese mensaje Hola expira.
* **Id**: escriba `string`. Es el identificador del mensaje de cola.
* **InsertionTime**: escriba `DateTimeOffset?`. tiempo de Hello ese mensaje Hola se agregó toohello cola.
* **NextVisibleTime**: tipo `DateTimeOffset?`. tiempo de Hello ese mensaje Hola volverá a resultar visible.
* **PopReceipt**: escriba `string`. confirmación de recepción del mensaje de bienvenida.

Vea cómo toouse Hola metadatos de la cola en [ejemplo de desencadenador](#triggersample).

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Ejemplo de desencadenador
Suponga que tiene Hola sigue function.json que define un desencadenador de cola:

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

Vea ejemplo de Hola a específica del lenguaje que recupera y registra los metadatos de la cola.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Ejemplo de desencadenador en C# #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Ejemplo de desencadenador en Node.js

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a>Control de mensajes dudosos en la cola
Cuando se produce un error en una función de activación de cola, las funciones de Azure vuelve a intentar esa función seguridad toofive veces para un mensaje de cola determinada, incluidos Hola primero pruebe. Si se produce un error en todos los intentos de cinco, tiempo de ejecución de funciones de hello agrega un almacenamiento de cola de mensajes tooa denominado  *&lt;originalqueuename >-dudoso*. Puede escribir una función tooprocess mensajes desde la cola de mensajes dudosos Hola registrarlos o enviar una notificación que se necesita atención manual. 

mensajes dudosos toohandle comprobación manualmente, hello `dequeueCount` de mensaje de bienvenida de cola (vea [cola desencadenador metadatos](#meta)).

<a name="output"></a>

## <a name="queue-storage-output-binding"></a>Enlace de salida de Queue Storage
Hola almacenamiento de cola de Azure de salida enlace permite la cola de mensajes tooa de toowrite. 

Definir una cola de enlace de salida mediante hello **integrar** Hola funciones portal de. portal de Hello crea Hola después de la definición de hello **enlaces** sección de *function.json*:

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* Hola `connection` propiedad debe contener el nombre de Hola de una configuración de aplicación que contiene una cadena de conexión de almacenamiento. Hola portal de Azure, Hola editor estándar en hello **integrar** ficha configura esta configuración de aplicación para cuando se selecciona una cuenta de almacenamiento.

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a>Uso de un enlace de salida de cola
En las funciones de Node.js, se obtiene acceso mediante cola de salida de hello `context.bindings.<name>`.

En las funciones. NET, puede generar tooany de los siguientes tipos de Hola. Cuando hay un parámetro de tipo `T`, `T` debe ser uno de los tipos de salida de hello compatible, como `string` o un POCO.

* `out T` (serializado como JSON)
* `out string`
* `out byte[]`
* `out`[`CloudQueueMessage`] 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

También puede utilizar el tipo de valor devuelto de método hello como Hola el enlace de salida.

<a name="outputsample"></a>

## <a name="queue-output-sample"></a>Ejemplo de salida de cola
siguiente Hello *function.json* define un desencadenador HTTP con una cola de salida de enlace:

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

Vea ejemplo de Hola a específica del lenguaje que genera un mensaje de la cola con la carga HTTP entrante de Hola.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a>Ejemplo de salida de cola en C# #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

toosend varios mensajes, utilice una `ICollector`:

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a>Ejemplo de salida de cola en Node.js

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

O bien, toosend varios mensajes,

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener un ejemplo de una función que usa desencadenadores de almacenamiento de cola y los enlaces, vea [crear un servicio de Azure de función de Azure conectado tooan](functions-create-an-azure-connected-function.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
