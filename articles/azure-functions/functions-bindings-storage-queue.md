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
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="fe42d-104">Enlaces de Queue Storage en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fe42d-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="fe42d-105">Este artículo se describe cómo tooconfigure y el código de enlaces de almacenamiento de cola de Azure en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe42d-105">This article describes how tooconfigure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="fe42d-106">Azure Functions admite desencadenador y enlaces de salida para Azure Queues.</span><span class="sxs-lookup"><span data-stu-id="fe42d-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="fe42d-107">Para las características que estén disponibles en todos los enlaces, consulte [conceptos sobre desencadenadores y enlaces de Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="fe42d-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="fe42d-108">Desencadenador de Queue Storage</span><span class="sxs-lookup"><span data-stu-id="fe42d-108">Queue storage trigger</span></span>
<span data-ttu-id="fe42d-109">desencadenador de almacenamiento de cola de Azure de Hello permite toomonitor un almacenamiento de cola si hay mensajes nuevos y reacciona toothem.</span><span class="sxs-lookup"><span data-stu-id="fe42d-109">hello Azure Queue storage trigger enables you toomonitor a queue storage for new messages and react toothem.</span></span> 

<span data-ttu-id="fe42d-110">Definir un desencadenador de cola mediante hello **integrar** Hola funciones portal de.</span><span class="sxs-lookup"><span data-stu-id="fe42d-110">Define a queue trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="fe42d-111">portal de Hello crea Hola después de la definición de hello **enlaces** sección de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="fe42d-111">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="fe42d-112">Hola `connection` propiedad debe contener el nombre de Hola de una configuración de aplicación que contiene una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fe42d-112">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="fe42d-113">Hola portal de Azure, Hola editor estándar en hello **integrar** ficha configura esta configuración de aplicación para cuando se selecciona una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fe42d-113">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="fe42d-114">Puede proporcionar una configuración adicional en un [host.json archivo](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther ajustar desencadenadores de almacenamiento de cola.</span><span class="sxs-lookup"><span data-stu-id="fe42d-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther fine-tune queue storage triggers.</span></span> <span data-ttu-id="fe42d-115">Por ejemplo, puede cambiar el intervalo de sondeo de la cola de hello en host.json.</span><span class="sxs-lookup"><span data-stu-id="fe42d-115">For example, you can change hello queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="fe42d-116">Uso de un desencadenador de cola</span><span class="sxs-lookup"><span data-stu-id="fe42d-116">Using a queue trigger</span></span>
<span data-ttu-id="fe42d-117">En las funciones de Node.js, tener acceso a Hola cola datos mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="fe42d-117">In Node.js functions, access hello queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="fe42d-118">En las funciones. NET, tener acceso a la carga de la cola de hello mediante un parámetro de método como `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="fe42d-118">In .NET functions, access hello queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="fe42d-119">En este caso, `paramName` es valor Hola especificado en hello [configuración de desencadenador](#trigger).</span><span class="sxs-lookup"><span data-stu-id="fe42d-119">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="fe42d-120">mensaje de bienvenida de cola puede ser deserializado tooany de hello siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="fe42d-120">hello queue message can be deserialized tooany of hello following types:</span></span>

* <span data-ttu-id="fe42d-121">Objeto POCO.</span><span class="sxs-lookup"><span data-stu-id="fe42d-121">POCO object.</span></span> <span data-ttu-id="fe42d-122">Usar si la carga de la cola de hello es un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="fe42d-122">Use if hello queue payload is a JSON object.</span></span> <span data-ttu-id="fe42d-123">en tiempo de ejecución de funciones de Hello deserializa carga hello en el objeto POCO Hola.</span><span class="sxs-lookup"><span data-stu-id="fe42d-123">hello Functions runtime deserializes hello payload into hello POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="fe42d-124">Metadatos de desencadenador de cola</span><span class="sxs-lookup"><span data-stu-id="fe42d-124">Queue trigger metadata</span></span>
<span data-ttu-id="fe42d-125">desencadenador de cola de Hello proporciona varias propiedades de metadatos.</span><span class="sxs-lookup"><span data-stu-id="fe42d-125">hello queue trigger provides several metadata properties.</span></span> <span data-ttu-id="fe42d-126">Estas propiedades pueden usarse como parte de expresiones de enlace en otros enlaces o como parámetros del código.</span><span class="sxs-lookup"><span data-stu-id="fe42d-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="fe42d-127">los valores de Hello tienen Hola misma semántica que [ `CloudQueueMessage` ].</span><span class="sxs-lookup"><span data-stu-id="fe42d-127">hello values have hello same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="fe42d-128">**QueueTrigger**: carga de cola (si hay una cadena válida)</span><span class="sxs-lookup"><span data-stu-id="fe42d-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="fe42d-129">**DequeueCount**: escriba `int`.</span><span class="sxs-lookup"><span data-stu-id="fe42d-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="fe42d-130">Hola número de veces que este mensaje se ha quitado de la cola.</span><span class="sxs-lookup"><span data-stu-id="fe42d-130">hello number of times this message has been dequeued.</span></span>
* <span data-ttu-id="fe42d-131">**ExpirationTime**: escriba `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="fe42d-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="fe42d-132">tiempo de Hello ese mensaje Hola expira.</span><span class="sxs-lookup"><span data-stu-id="fe42d-132">hello time that hello message expires.</span></span>
* <span data-ttu-id="fe42d-133">**Id**: escriba `string`.</span><span class="sxs-lookup"><span data-stu-id="fe42d-133">**Id** - Type `string`.</span></span> <span data-ttu-id="fe42d-134">Es el identificador del mensaje de cola.</span><span class="sxs-lookup"><span data-stu-id="fe42d-134">Queue message ID.</span></span>
* <span data-ttu-id="fe42d-135">**InsertionTime**: escriba `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="fe42d-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="fe42d-136">tiempo de Hello ese mensaje Hola se agregó toohello cola.</span><span class="sxs-lookup"><span data-stu-id="fe42d-136">hello time that hello message was added toohello queue.</span></span>
* <span data-ttu-id="fe42d-137">**NextVisibleTime**: tipo `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="fe42d-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="fe42d-138">tiempo de Hello ese mensaje Hola volverá a resultar visible.</span><span class="sxs-lookup"><span data-stu-id="fe42d-138">hello time that hello message will next be visible.</span></span>
* <span data-ttu-id="fe42d-139">**PopReceipt**: escriba `string`.</span><span class="sxs-lookup"><span data-stu-id="fe42d-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="fe42d-140">confirmación de recepción del mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="fe42d-140">hello message's pop receipt.</span></span>

<span data-ttu-id="fe42d-141">Vea cómo toouse Hola metadatos de la cola en [ejemplo de desencadenador](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="fe42d-141">See how toouse hello queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="fe42d-142">Ejemplo de desencadenador</span><span class="sxs-lookup"><span data-stu-id="fe42d-142">Trigger sample</span></span>
<span data-ttu-id="fe42d-143">Suponga que tiene Hola sigue function.json que define un desencadenador de cola:</span><span class="sxs-lookup"><span data-stu-id="fe42d-143">Suppose you have hello following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="fe42d-144">Vea ejemplo de Hola a específica del lenguaje que recupera y registra los metadatos de la cola.</span><span class="sxs-lookup"><span data-stu-id="fe42d-144">See hello language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="fe42d-145">C#</span><span class="sxs-lookup"><span data-stu-id="fe42d-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="fe42d-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="fe42d-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="fe42d-147">Ejemplo de desencadenador en C#</span><span class="sxs-lookup"><span data-stu-id="fe42d-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="fe42d-148">Ejemplo de desencadenador en Node.js</span><span class="sxs-lookup"><span data-stu-id="fe42d-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="fe42d-149">Control de mensajes dudosos en la cola</span><span class="sxs-lookup"><span data-stu-id="fe42d-149">Handling poison queue messages</span></span>
<span data-ttu-id="fe42d-150">Cuando se produce un error en una función de activación de cola, las funciones de Azure vuelve a intentar esa función seguridad toofive veces para un mensaje de cola determinada, incluidos Hola primero pruebe.</span><span class="sxs-lookup"><span data-stu-id="fe42d-150">When a queue trigger function fails, Azure Functions retries that function up toofive times for a given queue message, including hello first try.</span></span> <span data-ttu-id="fe42d-151">Si se produce un error en todos los intentos de cinco, tiempo de ejecución de funciones de hello agrega un almacenamiento de cola de mensajes tooa denominado  *&lt;originalqueuename >-dudoso*.</span><span class="sxs-lookup"><span data-stu-id="fe42d-151">If all five attempts fail, hello functions runtime adds a message tooa queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="fe42d-152">Puede escribir una función tooprocess mensajes desde la cola de mensajes dudosos Hola registrarlos o enviar una notificación que se necesita atención manual.</span><span class="sxs-lookup"><span data-stu-id="fe42d-152">You can write a function tooprocess messages from hello poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="fe42d-153">mensajes dudosos toohandle comprobación manualmente, hello `dequeueCount` de mensaje de bienvenida de cola (vea [cola desencadenador metadatos](#meta)).</span><span class="sxs-lookup"><span data-stu-id="fe42d-153">toohandle poison messages manually, check hello `dequeueCount` of hello queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="fe42d-154">Enlace de salida de Queue Storage</span><span class="sxs-lookup"><span data-stu-id="fe42d-154">Queue storage output binding</span></span>
<span data-ttu-id="fe42d-155">Hola almacenamiento de cola de Azure de salida enlace permite la cola de mensajes tooa de toowrite.</span><span class="sxs-lookup"><span data-stu-id="fe42d-155">hello Azure queue storage output binding enables you toowrite messages tooa queue.</span></span> 

<span data-ttu-id="fe42d-156">Definir una cola de enlace de salida mediante hello **integrar** Hola funciones portal de.</span><span class="sxs-lookup"><span data-stu-id="fe42d-156">Define a queue output binding using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="fe42d-157">portal de Hello crea Hola después de la definición de hello **enlaces** sección de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="fe42d-157">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="fe42d-158">Hola `connection` propiedad debe contener el nombre de Hola de una configuración de aplicación que contiene una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fe42d-158">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="fe42d-159">Hola portal de Azure, Hola editor estándar en hello **integrar** ficha configura esta configuración de aplicación para cuando se selecciona una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fe42d-159">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="fe42d-160">Uso de un enlace de salida de cola</span><span class="sxs-lookup"><span data-stu-id="fe42d-160">Using a queue output binding</span></span>
<span data-ttu-id="fe42d-161">En las funciones de Node.js, se obtiene acceso mediante cola de salida de hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="fe42d-161">In Node.js functions, you access hello output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="fe42d-162">En las funciones. NET, puede generar tooany de los siguientes tipos de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe42d-162">In .NET functions, you can output tooany of hello following types.</span></span> <span data-ttu-id="fe42d-163">Cuando hay un parámetro de tipo `T`, `T` debe ser uno de los tipos de salida de hello compatible, como `string` o un POCO.</span><span class="sxs-lookup"><span data-stu-id="fe42d-163">When there is a type parameter `T`, `T` must be one of hello supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="fe42d-164">`out T` (serializado como JSON)</span><span class="sxs-lookup"><span data-stu-id="fe42d-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="fe42d-165">`out`[`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="fe42d-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="fe42d-166">También puede utilizar el tipo de valor devuelto de método hello como Hola el enlace de salida.</span><span class="sxs-lookup"><span data-stu-id="fe42d-166">You can also use hello method return type as hello output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="fe42d-167">Ejemplo de salida de cola</span><span class="sxs-lookup"><span data-stu-id="fe42d-167">Queue output sample</span></span>
<span data-ttu-id="fe42d-168">siguiente Hello *function.json* define un desencadenador HTTP con una cola de salida de enlace:</span><span class="sxs-lookup"><span data-stu-id="fe42d-168">hello following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="fe42d-169">Vea ejemplo de Hola a específica del lenguaje que genera un mensaje de la cola con la carga HTTP entrante de Hola.</span><span class="sxs-lookup"><span data-stu-id="fe42d-169">See hello language-specific sample that outputs a queue message with hello incoming HTTP payload.</span></span>

* [<span data-ttu-id="fe42d-170">C#</span><span class="sxs-lookup"><span data-stu-id="fe42d-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="fe42d-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="fe42d-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="fe42d-172">Ejemplo de salida de cola en C#</span><span class="sxs-lookup"><span data-stu-id="fe42d-172">Queue output sample in C#</span></span> #

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

<span data-ttu-id="fe42d-173">toosend varios mensajes, utilice una `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="fe42d-173">toosend multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="fe42d-174">Ejemplo de salida de cola en Node.js</span><span class="sxs-lookup"><span data-stu-id="fe42d-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="fe42d-175">O bien, toosend varios mensajes,</span><span class="sxs-lookup"><span data-stu-id="fe42d-175">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="fe42d-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe42d-176">Next steps</span></span>

<span data-ttu-id="fe42d-177">Para obtener un ejemplo de una función que usa desencadenadores de almacenamiento de cola y los enlaces, vea [crear un servicio de Azure de función de Azure conectado tooan](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="fe42d-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected tooan Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

[`CloudQueueMessage`]: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
