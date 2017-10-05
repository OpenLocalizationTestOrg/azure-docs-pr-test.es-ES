---
title: Enlaces de Queue Storage en Azure Functions | Microsoft Docs
description: "Descubra cómo utilizar desencadenadores y enlaces de almacenamiento de Azure en funciones de Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "funciones de azure, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: e007acd75a2210d54f512e2c6698c90919f0fcd2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="d6975-104">Enlaces de Queue Storage en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d6975-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="d6975-105">En este artículo se describe cómo configurar enlaces de Azure Queue Storage y codificarlos en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="d6975-105">This article describes how to configure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="d6975-106">Azure Functions admite enlaces de desencadenador y salida para colas de Azure.</span><span class="sxs-lookup"><span data-stu-id="d6975-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="d6975-107">Para las características que estén disponibles en todos los enlaces, consulte [conceptos sobre desencadenadores y enlaces de Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="d6975-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="d6975-108">Desencadenador de Queue Storage</span><span class="sxs-lookup"><span data-stu-id="d6975-108">Queue storage trigger</span></span>
<span data-ttu-id="d6975-109">El desencadenador de Azure Queue Storage permite supervisar si hay mensajes nuevos en una cola de almacenamiento y reaccionar ante ellos.</span><span class="sxs-lookup"><span data-stu-id="d6975-109">The Azure Queue storage trigger enables you to monitor a queue storage for new messages and react to them.</span></span> 

<span data-ttu-id="d6975-110">Defina un desencadenador de cola mediante la pestaña **Integrar** del portal de Functions.</span><span class="sxs-lookup"><span data-stu-id="d6975-110">Define a queue trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="d6975-111">El portal crea la siguiente definición en la sección de **enlaces** de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="d6975-111">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<The name used to identify the trigger data in your code>",
    "queueName": "<Name of queue to poll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="d6975-112">La propiedad `connection` debe contener el nombre de una configuración de aplicación que contenga una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d6975-112">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="d6975-113">En Azure Portal, el editor estándar de la pestaña **Integrar** permite modificar esta configuración de aplicación al seleccionar una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d6975-113">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="d6975-114">Se pueden proporcionar opciones de configuración adicionales en un archivo [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) para ajustar aún más los desencadenadores de Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="d6975-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) to further fine-tune queue storage triggers.</span></span> <span data-ttu-id="d6975-115">Por ejemplo, puede cambiar el intervalo de sondeo de cola de host.json.</span><span class="sxs-lookup"><span data-stu-id="d6975-115">For example, you can change the queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="d6975-116">Uso de un desencadenador de cola</span><span class="sxs-lookup"><span data-stu-id="d6975-116">Using a queue trigger</span></span>
<span data-ttu-id="d6975-117">En las funciones de Node.js, acceda a los datos de cola mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d6975-117">In Node.js functions, access the queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="d6975-118">En las funciones de .NET, acceda a la carga útil de la cola mediante un parámetro de método como `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="d6975-118">In .NET functions, access the queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="d6975-119">Aquí, `paramName` es el valor que especificó en la [configuración del desencadenador](#trigger).</span><span class="sxs-lookup"><span data-stu-id="d6975-119">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="d6975-120">El mensaje de la cola se puede deserializar en cualquiera de los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="d6975-120">The queue message can be deserialized to any of the following types:</span></span>

* <span data-ttu-id="d6975-121">Objeto POCO.</span><span class="sxs-lookup"><span data-stu-id="d6975-121">POCO object.</span></span> <span data-ttu-id="d6975-122">Se debe usar si la carga útil de la cola es un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="d6975-122">Use if the queue payload is a JSON object.</span></span> <span data-ttu-id="d6975-123">El entorno en tiempo de ejecución de Functions deserializa la carga útil en el objeto POCO.</span><span class="sxs-lookup"><span data-stu-id="d6975-123">The Functions runtime deserializes the payload into the POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="d6975-124">Metadatos de desencadenador de cola</span><span class="sxs-lookup"><span data-stu-id="d6975-124">Queue trigger metadata</span></span>
<span data-ttu-id="d6975-125">El desencadenador de cola proporciona varias propiedades de metadatos.</span><span class="sxs-lookup"><span data-stu-id="d6975-125">The queue trigger provides several metadata properties.</span></span> <span data-ttu-id="d6975-126">Estas propiedades pueden usarse como parte de expresiones de enlace en otros enlaces o como parámetros del código.</span><span class="sxs-lookup"><span data-stu-id="d6975-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="d6975-127">Los valores tienen la misma semántica que [`CloudQueueMessage`].</span><span class="sxs-lookup"><span data-stu-id="d6975-127">The values have the same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="d6975-128">**QueueTrigger**: carga de cola (si hay una cadena válida)</span><span class="sxs-lookup"><span data-stu-id="d6975-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="d6975-129">**DequeueCount**: escriba `int`.</span><span class="sxs-lookup"><span data-stu-id="d6975-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="d6975-130">Es el número de veces que se ha quitado de la cola este mensaje.</span><span class="sxs-lookup"><span data-stu-id="d6975-130">The number of times this message has been dequeued.</span></span>
* <span data-ttu-id="d6975-131">**ExpirationTime**: escriba `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="d6975-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="d6975-132">Es la hora de expiración del mensaje.</span><span class="sxs-lookup"><span data-stu-id="d6975-132">The time that the message expires.</span></span>
* <span data-ttu-id="d6975-133">**Id**: escriba `string`.</span><span class="sxs-lookup"><span data-stu-id="d6975-133">**Id** - Type `string`.</span></span> <span data-ttu-id="d6975-134">Es el identificador del mensaje de cola.</span><span class="sxs-lookup"><span data-stu-id="d6975-134">Queue message ID.</span></span>
* <span data-ttu-id="d6975-135">**InsertionTime**: escriba `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="d6975-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="d6975-136">Es la hora en la que el mensaje se agregó a la cola.</span><span class="sxs-lookup"><span data-stu-id="d6975-136">The time that the message was added to the queue.</span></span>
* <span data-ttu-id="d6975-137">**NextVisibleTime**: tipo `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="d6975-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="d6975-138">Es la siguiente hora a la que será visible el mensaje.</span><span class="sxs-lookup"><span data-stu-id="d6975-138">The time that the message will next be visible.</span></span>
* <span data-ttu-id="d6975-139">**PopReceipt**: escriba `string`.</span><span class="sxs-lookup"><span data-stu-id="d6975-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="d6975-140">Es la confirmación de extracción del mensaje.</span><span class="sxs-lookup"><span data-stu-id="d6975-140">The message's pop receipt.</span></span>

<span data-ttu-id="d6975-141">Consulte cómo usar los metadatos de la cola en la sección [Ejemplo de desencadenador](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="d6975-141">See how to use the queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="d6975-142">Ejemplo de desencadenador</span><span class="sxs-lookup"><span data-stu-id="d6975-142">Trigger sample</span></span>
<span data-ttu-id="d6975-143">Suponga que tiene el siguiente elemento function.json que define un desencadenador de cola:</span><span class="sxs-lookup"><span data-stu-id="d6975-143">Suppose you have the following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="d6975-144">Consulte el ejemplo de lenguaje específico que permite recuperar y registrar los metadatos de la cola.</span><span class="sxs-lookup"><span data-stu-id="d6975-144">See the language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="d6975-145">C#</span><span class="sxs-lookup"><span data-stu-id="d6975-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="d6975-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="d6975-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="d6975-147">Ejemplo de desencadenador en C#</span><span class="sxs-lookup"><span data-stu-id="d6975-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="d6975-148">Ejemplo de desencadenador en Node.js</span><span class="sxs-lookup"><span data-stu-id="d6975-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="d6975-149">Control de mensajes dudosos en la cola</span><span class="sxs-lookup"><span data-stu-id="d6975-149">Handling poison queue messages</span></span>
<span data-ttu-id="d6975-150">Si se produce un error en una función del desencadenador de cola, Azure Functions volverá a intentar esa función hasta cinco veces para un determinado mensaje en la cola, incluido el primer intento.</span><span class="sxs-lookup"><span data-stu-id="d6975-150">When a queue trigger function fails, Azure Functions retries that function up to five times for a given queue message, including the first try.</span></span> <span data-ttu-id="d6975-151">Si se produce un error en los cinco intentos, Functions agregará un mensaje a la cola de almacenamiento llamada *&lt;nombreDeColaOriginal>-poison*.</span><span class="sxs-lookup"><span data-stu-id="d6975-151">If all five attempts fail, the functions runtime adds a message to a queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="d6975-152">Puede escribir una función para procesar los mensajes desde la cola de mensajes dudosos registrándolos o enviando una notificación indicando que se necesita atención manual.</span><span class="sxs-lookup"><span data-stu-id="d6975-152">You can write a function to process messages from the poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="d6975-153">Para controlar manualmente los mensajes dudosos, compruebe el elemento `dequeueCount` del mensaje de la cola (consulte [Metadatos de desencadenador de cola](#meta)).</span><span class="sxs-lookup"><span data-stu-id="d6975-153">To handle poison messages manually, check the `dequeueCount` of the queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="d6975-154">Enlace de salida de Queue Storage</span><span class="sxs-lookup"><span data-stu-id="d6975-154">Queue storage output binding</span></span>
<span data-ttu-id="d6975-155">El enlace de salida de Azure Queue Storage le permite escribir mensajes en una cola.</span><span class="sxs-lookup"><span data-stu-id="d6975-155">The Azure queue storage output binding enables you to write messages to a queue.</span></span> 

<span data-ttu-id="d6975-156">Defina un enlace de salida de cola mediante la pestaña **Integrar** del portal de Functions.</span><span class="sxs-lookup"><span data-stu-id="d6975-156">Define a queue output binding using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="d6975-157">El portal crea la siguiente definición en la sección de **enlaces** de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="d6975-157">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<The name used to identify the trigger data in your code>",
   "queueName": "<Name of queue to write to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="d6975-158">La propiedad `connection` debe contener el nombre de una configuración de aplicación que contenga una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d6975-158">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="d6975-159">En Azure Portal, el editor estándar de la pestaña **Integrar** permite modificar esta configuración de aplicación al seleccionar una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d6975-159">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="d6975-160">Uso de un enlace de salida de cola</span><span class="sxs-lookup"><span data-stu-id="d6975-160">Using a queue output binding</span></span>
<span data-ttu-id="d6975-161">En las funciones de Node.js, accede a la cola de salida mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="d6975-161">In Node.js functions, you access the output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="d6975-162">En las funciones de .NET, puede enviar a la salida cualquiera de los siguientes tipos.</span><span class="sxs-lookup"><span data-stu-id="d6975-162">In .NET functions, you can output to any of the following types.</span></span> <span data-ttu-id="d6975-163">Si hay algún parámetro de tipo `T`, `T` debe ser uno de los tipos de salida admitidos, como `string` o un elemento POCO.</span><span class="sxs-lookup"><span data-stu-id="d6975-163">When there is a type parameter `T`, `T` must be one of the supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="d6975-164">`out T` (serializado como JSON)</span><span class="sxs-lookup"><span data-stu-id="d6975-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="d6975-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="d6975-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="d6975-166">También puede usar el tipo de valor devuelto del método como enlace de salida.</span><span class="sxs-lookup"><span data-stu-id="d6975-166">You can also use the method return type as the output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="d6975-167">Ejemplo de salida de cola</span><span class="sxs-lookup"><span data-stu-id="d6975-167">Queue output sample</span></span>
<span data-ttu-id="d6975-168">El siguiente elemento *function.json* define un desencadenador HTTP con un enlace de salida de cola:</span><span class="sxs-lookup"><span data-stu-id="d6975-168">The following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="d6975-169">Consulte el ejemplo específico del lenguaje que envía a la salida un mensaje de cola con la carga útil HTTP entrante.</span><span class="sxs-lookup"><span data-stu-id="d6975-169">See the language-specific sample that outputs a queue message with the incoming HTTP payload.</span></span>

* [<span data-ttu-id="d6975-170">C#</span><span class="sxs-lookup"><span data-stu-id="d6975-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="d6975-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="d6975-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="d6975-172">Ejemplo de salida de cola en C#</span><span class="sxs-lookup"><span data-stu-id="d6975-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding to a custom POCO, with a queue output binding
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

<span data-ttu-id="d6975-173">Para enviar varios mensajes, use un elemento `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="d6975-173">To send multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="d6975-174">Ejemplo de salida de cola en Node.js</span><span class="sxs-lookup"><span data-stu-id="d6975-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="d6975-175">O, para enviar varios mensajes,</span><span class="sxs-lookup"><span data-stu-id="d6975-175">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for the myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="d6975-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d6975-176">Next steps</span></span>

<span data-ttu-id="d6975-177">Para ver un ejemplo de una función que usa desencadenadores y enlaces de Queue Storage, consulte [Creación de una instancia de Azure Functions conectada a un servicio de Azure](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="d6975-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected to an Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
