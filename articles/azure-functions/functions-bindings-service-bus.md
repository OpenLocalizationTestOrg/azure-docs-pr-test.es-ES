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
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="f3dad-104">Enlaces de Service Bus en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f3dad-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="f3dad-105">Este artículo se explica cómo tooconfigure y trabajar con enlaces de Bus de servicio de Azure en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3dad-105">This article explains how tooconfigure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="f3dad-106">Azure Functions admite enlaces de desencadenador y salida para colas y temas de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f3dad-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="f3dad-107">Desencadenador de Service Bus</span><span class="sxs-lookup"><span data-stu-id="f3dad-107">Service Bus trigger</span></span>
<span data-ttu-id="f3dad-108">Utilice Hola Service Bus desencadenador toorespond toomessages desde una cola de Bus de servicio o un tema.</span><span class="sxs-lookup"><span data-stu-id="f3dad-108">Use hello Service Bus trigger toorespond toomessages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="f3dad-109">Hello desencadenadores queue y topic de Bus de servicio definidos por hello siguientes objetos JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="f3dad-109">hello Service Bus queue and topic triggers are defined by hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="f3dad-110">Desencadenador de *cola*:</span><span class="sxs-lookup"><span data-stu-id="f3dad-110">*queue* trigger:</span></span>

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

* <span data-ttu-id="f3dad-111">Desencadenador de *tema*:</span><span class="sxs-lookup"><span data-stu-id="f3dad-111">*topic* trigger:</span></span>

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

<span data-ttu-id="f3dad-112">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="f3dad-112">Note hello following:</span></span>

* <span data-ttu-id="f3dad-113">Para `connection`, [crear una configuración de aplicación en la aplicación de la función](functions-how-to-use-azure-function-app-settings.md) que contiene nombres de Bus de servicio de tooyour de cadena de conexión de hello, a continuación, especifique el nombre de Hola de configuración de la aplicación Hola Hola `connection` propiedad en el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="f3dad-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your trigger.</span></span> <span data-ttu-id="f3dad-114">Obtener cadena de conexión de hello siguiendo los pasos de Hola se muestra en [obtener credenciales de administración de hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="f3dad-114">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="f3dad-115">cadena de conexión de Hello debe ser de espacio de nombres, cola específica de tooa no limita o tema de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="f3dad-115">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="f3dad-116">Si deja `connection` vacía, el desencadenador de Hola se da por supuesto que se especifica una cadena de conexión de Bus de servicio de manera predeterminada en una aplicación de configuración con nombre `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="f3dad-116">If you leave `connection` empty, hello trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="f3dad-117">Para `accessRights`, los valores disponibles son `manage` y `listen`.</span><span class="sxs-lookup"><span data-stu-id="f3dad-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="f3dad-118">valor predeterminado de Hello es `manage`, lo que indica que hello `connection` tiene hello **administrar** permiso.</span><span class="sxs-lookup"><span data-stu-id="f3dad-118">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="f3dad-119">Si usa una cadena de conexión que no tiene hello **administrar** de conjunto de permisos, `accessRights` demasiado`listen`.</span><span class="sxs-lookup"><span data-stu-id="f3dad-119">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="f3dad-120">De lo contrario, las funciones de hello en tiempo de ejecución puede producir un error tratar las operaciones de toodo que requieren derechos de administración.</span><span class="sxs-lookup"><span data-stu-id="f3dad-120">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="f3dad-121">Comportamiento de un desencadenador</span><span class="sxs-lookup"><span data-stu-id="f3dad-121">Trigger behavior</span></span>
* <span data-ttu-id="f3dad-122">**Subprocesamiento único** : de forma predeterminada, los procesos del runtime de funciones hello simultáneamente varios mensajes.</span><span class="sxs-lookup"><span data-stu-id="f3dad-122">**Single-threading** - By default, hello Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="f3dad-123">establecer toodirect hello en tiempo de ejecución tooprocess solo una única cola o tema mensaje a la vez, `serviceBus.maxConcurrentCalls` too1 en *host.json*.</span><span class="sxs-lookup"><span data-stu-id="f3dad-123">toodirect hello runtime tooprocess only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span></span> 
  <span data-ttu-id="f3dad-124">Para más información acerca de *host.json*, consulte [Estructura de carpetas](functions-reference.md#folder-structure) y [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="f3dad-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="f3dad-125">**Gestión de mensajes dudosos**: Service Bus realiza su propio tratamiento de mensajes dudosos, que no se puede controlar ni configurar en el código ni en la configuración de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f3dad-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="f3dad-126">**Comportamiento de PeekLock** -en tiempo de ejecución de funciones de hello recibe un mensaje en [ `PeekLock` modo](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) y llamadas `Complete` en el mensaje de bienvenida de si la función hello finaliza correctamente, o llamadas a `Abandon` si hello se produce un error en la función.</span><span class="sxs-lookup"><span data-stu-id="f3dad-126">**PeekLock behavior** - hello Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> 
  <span data-ttu-id="f3dad-127">Si se ejecuta más de hello función hello `PeekLock` tiempo de espera de bloqueo de Hola se renovará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f3dad-127">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="f3dad-128">Uso del desencadenador</span><span class="sxs-lookup"><span data-stu-id="f3dad-128">Trigger usage</span></span>
<span data-ttu-id="f3dad-129">Esta sección muestra cómo toouse el Bus de servicio desencadenar en el código de función.</span><span class="sxs-lookup"><span data-stu-id="f3dad-129">This section shows you how toouse your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="f3dad-130">En C# y F #, mensaje de bienvenida de desencadenador de Bus de servicio puede ser deserializado tooany de hello siguientes tipos de entrada:</span><span class="sxs-lookup"><span data-stu-id="f3dad-130">In C# and F#, hello Service Bus trigger message can be deserialized tooany of hello following input types:</span></span>

* <span data-ttu-id="f3dad-131">`string`: útil para mensajes de cadena</span><span class="sxs-lookup"><span data-stu-id="f3dad-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="f3dad-132">`byte[]`: útil para datos binarios</span><span class="sxs-lookup"><span data-stu-id="f3dad-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="f3dad-133">Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): útil para datos serializados mediante JSON.</span><span class="sxs-lookup"><span data-stu-id="f3dad-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="f3dad-134">Si se declara un tipo de entrada personalizado, como `CustomType`, las funciones de Azure intenta datos JSON de toodeserialize hello en el tipo especificado.</span><span class="sxs-lookup"><span data-stu-id="f3dad-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="f3dad-135">`BrokeredMessage`-Proporciona Hola deserializa el mensaje con hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) (método).</span><span class="sxs-lookup"><span data-stu-id="f3dad-135">`BrokeredMessage` - gives you hello deserialized message with hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="f3dad-136">En Node.js, mensajes de bienvenida del Bus de servicio desencadenador se pasan a la función hello como una cadena o un objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="f3dad-136">In Node.js, hello Service Bus trigger message is passed into hello function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="f3dad-137">Ejemplo de desencadenador</span><span class="sxs-lookup"><span data-stu-id="f3dad-137">Trigger sample</span></span>
<span data-ttu-id="f3dad-138">Suponga que tiene Hola siguientes function.json:</span><span class="sxs-lookup"><span data-stu-id="f3dad-138">Suppose you have hello following function.json:</span></span>

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

<span data-ttu-id="f3dad-139">Vea el ejemplo específico del idioma de Hola que procesa un mensaje de cola de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="f3dad-139">See hello language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="f3dad-140">C#</span><span class="sxs-lookup"><span data-stu-id="f3dad-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="f3dad-141">F#</span><span class="sxs-lookup"><span data-stu-id="f3dad-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="f3dad-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="f3dad-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="f3dad-143">Ejemplo de desencadenador en C#</span><span class="sxs-lookup"><span data-stu-id="f3dad-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="f3dad-144">Ejemplo de desencadenador en F#</span><span class="sxs-lookup"><span data-stu-id="f3dad-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="f3dad-145">Ejemplo de desencadenador en Node.js</span><span class="sxs-lookup"><span data-stu-id="f3dad-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="f3dad-146">Enlace de salida de Service Bus</span><span class="sxs-lookup"><span data-stu-id="f3dad-146">Service Bus output binding</span></span>
<span data-ttu-id="f3dad-147">Hola salida queue y topic de Bus de servicio para una función usar hello siguientes objetos JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="f3dad-147">hello Service Bus queue and topic output for a function use hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="f3dad-148">Salida de *cola*:</span><span class="sxs-lookup"><span data-stu-id="f3dad-148">*queue* output:</span></span>

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
* <span data-ttu-id="f3dad-149">Salida de *tema*:</span><span class="sxs-lookup"><span data-stu-id="f3dad-149">*topic* output:</span></span>

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

<span data-ttu-id="f3dad-150">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="f3dad-150">Note hello following:</span></span>

* <span data-ttu-id="f3dad-151">Para `connection`, [crear una configuración de aplicación en la aplicación de la función](functions-how-to-use-azure-function-app-settings.md) que contiene nombres de Bus de servicio de tooyour de cadena de conexión de hello, a continuación, especifique el nombre de Hola de configuración de la aplicación Hola Hola `connection` propiedad en el resultado enlace.</span><span class="sxs-lookup"><span data-stu-id="f3dad-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your output binding.</span></span> <span data-ttu-id="f3dad-152">Obtener cadena de conexión de hello siguiendo los pasos de Hola se muestra en [obtener credenciales de administración de hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="f3dad-152">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="f3dad-153">cadena de conexión de Hello debe ser de espacio de nombres, cola específica de tooa no limita o tema de Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="f3dad-153">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="f3dad-154">Si deja `connection` vacía, hello enlace de salida se da por supuesto que se especifica una cadena de conexión de Bus de servicio de manera predeterminada en una aplicación de configuración con nombre `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="f3dad-154">If you leave `connection` empty, hello output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="f3dad-155">Para `accessRights`, los valores disponibles son `manage` y `listen`.</span><span class="sxs-lookup"><span data-stu-id="f3dad-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="f3dad-156">valor predeterminado de Hello es `manage`, lo que indica que hello `connection` tiene hello **administrar** permiso.</span><span class="sxs-lookup"><span data-stu-id="f3dad-156">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="f3dad-157">Si usa una cadena de conexión que no tiene hello **administrar** de conjunto de permisos, `accessRights` demasiado`listen`.</span><span class="sxs-lookup"><span data-stu-id="f3dad-157">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="f3dad-158">De lo contrario, las funciones de hello en tiempo de ejecución puede producir un error tratar las operaciones de toodo que requieren derechos de administración.</span><span class="sxs-lookup"><span data-stu-id="f3dad-158">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="f3dad-159">Uso de salidas</span><span class="sxs-lookup"><span data-stu-id="f3dad-159">Output usage</span></span>
<span data-ttu-id="f3dad-160">En C# y F #, las funciones de Azure puede crear un mensaje de cola de Bus de servicio desde cualquiera de los siguientes tipos de hello:</span><span class="sxs-lookup"><span data-stu-id="f3dad-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of hello following types:</span></span>

* <span data-ttu-id="f3dad-161">Cualquier [objeto](https://msdn.microsoft.com/library/system.object.aspx): la definición de parámetro es similar a `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="f3dad-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="f3dad-162">Funciones deserializa el objeto de hello en un mensaje JSON.</span><span class="sxs-lookup"><span data-stu-id="f3dad-162">Functions deserializes hello object into a JSON message.</span></span> <span data-ttu-id="f3dad-163">Si el valor de salida de hello es nulo cuando sale de la función hello, funciones crea mensajes de bienvenida con un objeto null.</span><span class="sxs-lookup"><span data-stu-id="f3dad-163">If hello output value is null when hello function exits, Functions creates hello message with a null object.</span></span>
* <span data-ttu-id="f3dad-164">`string`: la definición de parámetro es similar a `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="f3dad-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="f3dad-165">Si el valor del parámetro hello es distinto de null cuando sale de la función hello, funciones crea un mensaje.</span><span class="sxs-lookup"><span data-stu-id="f3dad-165">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="f3dad-166">`byte[]`: la definición de parámetro es similar a `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="f3dad-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="f3dad-167">Si el valor del parámetro hello es distinto de null cuando sale de la función hello, funciones crea un mensaje.</span><span class="sxs-lookup"><span data-stu-id="f3dad-167">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="f3dad-168">`BrokeredMessage`: la definición de parámetro es similar a `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="f3dad-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="f3dad-169">Si el valor del parámetro hello es distinto de null cuando sale de la función hello, funciones crea un mensaje.</span><span class="sxs-lookup"><span data-stu-id="f3dad-169">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>

<span data-ttu-id="f3dad-170">Para crear varios mensajes en una función de C#, puede utilizar `ICollector<T>` o `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="f3dad-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="f3dad-171">Se crea un mensaje cuando se llama a hello `Add` método.</span><span class="sxs-lookup"><span data-stu-id="f3dad-171">A message is created when you call hello `Add` method.</span></span>

<span data-ttu-id="f3dad-172">En Node.js, puede asignar una cadena, una matriz de bytes o un objeto de Javascript (deserializada en JSON) demasiado`context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="f3dad-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) too`context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="f3dad-173">Ejemplo de salida</span><span class="sxs-lookup"><span data-stu-id="f3dad-173">Output sample</span></span>
<span data-ttu-id="f3dad-174">Suponga que tiene Hola después function.json, que define una salida de cola de Bus de servicio:</span><span class="sxs-lookup"><span data-stu-id="f3dad-174">Suppose you have hello following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="f3dad-175">Vea el ejemplo de específica del lenguaje de Hola que envía a una cola de bus de servicio de toohello de mensajes.</span><span class="sxs-lookup"><span data-stu-id="f3dad-175">See hello language-specific sample that sends a message toohello service bus queue.</span></span>

* [<span data-ttu-id="f3dad-176">C#</span><span class="sxs-lookup"><span data-stu-id="f3dad-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="f3dad-177">F#</span><span class="sxs-lookup"><span data-stu-id="f3dad-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="f3dad-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="f3dad-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="f3dad-179">Ejemplo de salida en C#</span><span class="sxs-lookup"><span data-stu-id="f3dad-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="f3dad-180">O bien, toocreate varios mensajes:</span><span class="sxs-lookup"><span data-stu-id="f3dad-180">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="f3dad-181">Ejemplo de salida en F#</span><span class="sxs-lookup"><span data-stu-id="f3dad-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="f3dad-182">Ejemplo de salida en Node.js</span><span class="sxs-lookup"><span data-stu-id="f3dad-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="f3dad-183">O bien, toocreate varios mensajes:</span><span class="sxs-lookup"><span data-stu-id="f3dad-183">Or, toocreate multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f3dad-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3dad-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

