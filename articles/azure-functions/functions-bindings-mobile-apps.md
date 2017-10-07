---
title: "enlaces de aplicaciones móviles de funciones aaaAzure | Documentos de Microsoft"
description: "Comprender cómo toouse enlaces de aplicaciones móviles de Azure en las funciones de Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="743ac-104">Enlaces de Aplicaciones móviles en funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="743ac-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="743ac-105">Este artículo se explica cómo tooconfigure y código [aplicaciones móviles de Azure](../app-service-mobile/app-service-mobile-value-prop.md) enlaces en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="743ac-105">This article explains how tooconfigure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="743ac-106">Azure Functions admite enlaces de entrada y salida para Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="743ac-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="743ac-107">Hello aplicaciones móviles de entrada y salida enlaces le permiten [de lectura y escritura de tablas de toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) en su aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="743ac-107">hello Mobile Apps input and output bindings let you [read from and write toodata tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="743ac-108">Enlace de entrada de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="743ac-108">Mobile Apps input binding</span></span>
<span data-ttu-id="743ac-109">Hola enlace de entrada de aplicaciones móviles carga un registro desde un punto de conexión de tabla móvil y lo pasa a la función.</span><span class="sxs-lookup"><span data-stu-id="743ac-109">hello Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="743ac-110">En C# y F # funciones, todos los registros de toohello los cambios realizados se envían automáticamente toohello atrás tabla cuando finalice correctamente la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="743ac-110">In a C# and F# functions, any changes made toohello record are automatically sent back toohello table when hello function exits successfully.</span></span>

<span data-ttu-id="743ac-111">Hola aplicaciones móviles de entrada tooa función usa Hola siguiente objeto JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="743ac-111">hello Mobile Apps input tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="743ac-112">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="743ac-112">Note hello following:</span></span>

* <span data-ttu-id="743ac-113">`id`puede ser estático o se puede basar en desencadenador de Hola que invoca la función hello.</span><span class="sxs-lookup"><span data-stu-id="743ac-113">`id` can be static, or it can be based on hello trigger that invokes hello function.</span></span> <span data-ttu-id="743ac-114">Por ejemplo, si utiliza un [desencadenador cola]() para la función, a continuación, `"id": "{queueTrigger}"` utiliza Hola valor de cadena de mensaje de la cola de saludo como Hola tooretrieve de Id. de registro.</span><span class="sxs-lookup"><span data-stu-id="743ac-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses hello string value of hello queue message as hello record ID tooretrieve.</span></span>
* <span data-ttu-id="743ac-115">`connection`debe contener el nombre de Hola de una configuración de aplicación en la aplicación de la función, que a su vez contiene la dirección URL de saludo de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="743ac-115">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="743ac-116">función Hello usa este operaciones de REST de dirección URL tooconstruct Hola necesario en su aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="743ac-116">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="743ac-117">Se [crear una configuración de aplicación en la aplicación de la función]() que contiene la dirección URL de la aplicación móvil (qué aspecto `http://<appname>.azurewebsites.net`), a continuación, especifique el nombre de Hola de configuración de la aplicación hello en hello `connection` propiedad en el enlace de entrada.</span><span class="sxs-lookup"><span data-stu-id="743ac-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="743ac-118">Necesita toospecify `apiKey` si se [implementar una clave de API en el back-end de aplicación móvil de Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), o [implementar una clave de API en el back-end de .NET aplicación móvil](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="743ac-118">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="743ac-119">toodo, le [crear una configuración de aplicación en la aplicación de la función]() que contiene la clave de API de hello, a continuación, agregue hello `apiKey` propiedad en el enlace de entrada con el nombre de Hola de configuración de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="743ac-119">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="743ac-120">Esta clave de API no se debe compartir con los clientes de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="743ac-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="743ac-121">Solo debe ser clientes de forma segura tooservice lado distribuidos, como las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="743ac-121">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="743ac-122">Azure Functions almacena la información de conexión y las claves de API como configuración de la aplicación de forma que no se protegen en el repositorio de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="743ac-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="743ac-123">Esto protege la información confidencial.</span><span class="sxs-lookup"><span data-stu-id="743ac-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="743ac-124">Uso de entradas</span><span class="sxs-lookup"><span data-stu-id="743ac-124">Input usage</span></span>
<span data-ttu-id="743ac-125">Esta sección muestra cómo toouse las aplicaciones móviles de entrada en el código de función de enlace.</span><span class="sxs-lookup"><span data-stu-id="743ac-125">This section shows you how toouse your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="743ac-126">Al registro de hello con hello especificado se encuentra el Id. de tabla y registro, se pasa a Hola denominado [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parámetro (o, en Node.js, se pasa a hello `context.bindings.<name>` objeto).</span><span class="sxs-lookup"><span data-stu-id="743ac-126">When hello record with hello specified table and record ID is found, it is passed into hello named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into hello `context.bindings.<name>` object).</span></span> <span data-ttu-id="743ac-127">Cuando no se encuentra el registro de hello, parámetro hello es `null`.</span><span class="sxs-lookup"><span data-stu-id="743ac-127">When hello record is not found, hello parameter is `null`.</span></span> 

<span data-ttu-id="743ac-128">En las funciones de C# y F #, cualquier cambio que realice el registro de toohello de entrada (parámetro de entrada) se envía automáticamente atrás toohello tabla de aplicaciones móviles cuando finalice correctamente la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="743ac-128">In C# and F# functions, any changes you make toohello input record (input parameter) is automatically sent back toohello Mobile Apps table when hello function exits successfully.</span></span> <span data-ttu-id="743ac-129">En las funciones de Node.js, utilice `context.bindings.<name>` tooaccess Hola registro de entrada.</span><span class="sxs-lookup"><span data-stu-id="743ac-129">In Node.js functions, use `context.bindings.<name>` tooaccess hello input record.</span></span> <span data-ttu-id="743ac-130">No se puede modificar un registro en Node.js.</span><span class="sxs-lookup"><span data-stu-id="743ac-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="743ac-131">Ejemplo de entrada</span><span class="sxs-lookup"><span data-stu-id="743ac-131">Input sample</span></span>
<span data-ttu-id="743ac-132">Suponga que tiene Hola después function.json, que recupera un registro de la tabla de aplicación móvil con el Id. de Hola Hola desencadenador del mensaje de cola:</span><span class="sxs-lookup"><span data-stu-id="743ac-132">Suppose you have hello following function.json, that retrieves a Mobile App table record with hello id of hello queue trigger message:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="743ac-133">Vea ejemplo de Hola a específicos del idioma que utiliza el registro de entrada de Hola desde el enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="743ac-133">See hello language-specific sample that uses hello input record from hello binding.</span></span> <span data-ttu-id="743ac-134">ejemplos de C# y F # Hello también modificar del registro de hello `text` propiedad.</span><span class="sxs-lookup"><span data-stu-id="743ac-134">hello C# and F# samples also modify hello record's `text` property.</span></span>

* [<span data-ttu-id="743ac-135">C#</span><span class="sxs-lookup"><span data-stu-id="743ac-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="743ac-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="743ac-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="743ac-137">Ejemplo de entrada en C#</span><span class="sxs-lookup"><span data-stu-id="743ac-137">Input sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="743ac-138">Ejemplo de entrada en Node.js</span><span class="sxs-lookup"><span data-stu-id="743ac-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="743ac-139">Enlace de salida de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="743ac-139">Mobile Apps output binding</span></span>
<span data-ttu-id="743ac-140">Utilice Hola aplicaciones móviles salida enlace toowrite un nuevo extremo de tabla de registro tooa aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="743ac-140">Use hello Mobile Apps output binding toowrite a new record tooa Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="743ac-141">Hola aplicaciones móviles de salida para una función usa Hola siguiente objeto JSON en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="743ac-141">hello Mobile Apps output for a function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

<span data-ttu-id="743ac-142">Tenga en cuenta los siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="743ac-142">Note hello following:</span></span>

* <span data-ttu-id="743ac-143">`connection`debe contener el nombre de Hola de una configuración de aplicación en la aplicación de la función, que a su vez contiene la dirección URL de saludo de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="743ac-143">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="743ac-144">función Hello usa este operaciones de REST de dirección URL tooconstruct Hola necesario en su aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="743ac-144">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="743ac-145">Se [crear una configuración de aplicación en la aplicación de la función]() que contiene la dirección URL de la aplicación móvil (qué aspecto `http://<appname>.azurewebsites.net`), a continuación, especifique el nombre de Hola de configuración de la aplicación hello en hello `connection` propiedad en el enlace de entrada.</span><span class="sxs-lookup"><span data-stu-id="743ac-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="743ac-146">Necesita toospecify `apiKey` si se [implementar una clave de API en el back-end de aplicación móvil de Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), o [implementar una clave de API en el back-end de .NET aplicación móvil](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="743ac-146">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="743ac-147">toodo, le [crear una configuración de aplicación en la aplicación de la función]() que contiene la clave de API de hello, a continuación, agregue hello `apiKey` propiedad en el enlace de entrada con el nombre de Hola de configuración de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="743ac-147">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="743ac-148">Esta clave de API no se debe compartir con los clientes de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="743ac-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="743ac-149">Solo debe ser clientes de forma segura tooservice lado distribuidos, como las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="743ac-149">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="743ac-150">Azure Functions almacena la información de conexión y las claves de API como configuración de la aplicación de forma que no se protegen en el repositorio de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="743ac-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="743ac-151">Esto protege la información confidencial.</span><span class="sxs-lookup"><span data-stu-id="743ac-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="743ac-152">Uso de salidas</span><span class="sxs-lookup"><span data-stu-id="743ac-152">Output usage</span></span>
<span data-ttu-id="743ac-153">Esta sección muestra cómo toouse las aplicaciones móviles de salida en el código de función de enlace.</span><span class="sxs-lookup"><span data-stu-id="743ac-153">This section shows you how toouse your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="743ac-154">En funciones de C#, utilice un parámetro de salida con nombre de tipo `out object` tooaccess Hola registro de salida.</span><span class="sxs-lookup"><span data-stu-id="743ac-154">In C# functions, use a named output parameter of type `out object` tooaccess hello output record.</span></span> <span data-ttu-id="743ac-155">En las funciones de Node.js, utilice `context.bindings.<name>` tooaccess Hola registro de salida.</span><span class="sxs-lookup"><span data-stu-id="743ac-155">In Node.js functions, use `context.bindings.<name>` tooaccess hello output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="743ac-156">Ejemplo de salida</span><span class="sxs-lookup"><span data-stu-id="743ac-156">Output sample</span></span>
<span data-ttu-id="743ac-157">Suponga que tiene Hola después function.json, que define un desencadenador de cola y una salida de aplicaciones móviles:</span><span class="sxs-lookup"><span data-stu-id="743ac-157">Suppose you have hello following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="743ac-158">Vea el ejemplo de específica del lenguaje de Hola que crea un registro en el extremo de tabla de aplicaciones móviles de hello con contenido de hello del mensaje de bienvenida de cola.</span><span class="sxs-lookup"><span data-stu-id="743ac-158">See hello language-specific sample that creates a record in hello Mobile Apps table endpoint with hello content of hello queue message.</span></span>

* [<span data-ttu-id="743ac-159">C#</span><span class="sxs-lookup"><span data-stu-id="743ac-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="743ac-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="743ac-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="743ac-161">Ejemplo de salida en C#</span><span class="sxs-lookup"><span data-stu-id="743ac-161">Output sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="743ac-162">Ejemplo de salida en Node.js</span><span class="sxs-lookup"><span data-stu-id="743ac-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="743ac-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="743ac-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

