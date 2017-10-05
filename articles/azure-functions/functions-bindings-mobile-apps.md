---
title: Enlaces de Mobile Apps en Azure Functions | Microsoft Docs
description: "Descubra cómo utilizar los enlaces de Aplicaciones móviles en funciones de Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "funciones de azure, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: c5e1c02984f9773b263c0bee7685c7d5ff62e658
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="c5e0b-104">Enlaces de Aplicaciones móviles en funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c5e0b-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="c5e0b-105">Este artículo explica cómo configurar y codificar enlaces de [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="c5e0b-106">Azure Functions admite enlaces de entrada y salida para Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="c5e0b-107">Los enlaces de entrada y salida enlaces de Mobile Apps le permiten [realizar operaciones de lectura y escritura en tablas de datos](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) en su aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="c5e0b-108">Enlace de entrada de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="c5e0b-108">Mobile Apps input binding</span></span>
<span data-ttu-id="c5e0b-109">El enlace de entrada de Mobile Apps carga un registro desde un punto de conexión de tabla móvil y lo pasa a la función.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="c5e0b-110">En una función de C# y F#, los cambios realizados en el registro se enviarán automáticamente a la tabla una vez que la función se complete correctamente.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

<span data-ttu-id="c5e0b-111">La entrada de Mobile Apps a una función usa el siguiente objeto JSON en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="c5e0b-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of the record to retrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="c5e0b-112">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5e0b-112">Note the following:</span></span>

* <span data-ttu-id="c5e0b-113">`id` puede ser estático o se puede basar en el desencadenador que invoca la función.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-113">`id` can be static, or it can be based on the trigger that invokes the function.</span></span> <span data-ttu-id="c5e0b-114">Por ejemplo, si utiliza un [desencadenador cola]() para la función, entonces `"id": "{queueTrigger}"` usa el valor de cadena del mensaje de cola como el identificador de registro para recuperar.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>
* <span data-ttu-id="c5e0b-115">`connection` debe contener el nombre de una configuración de aplicación en la aplicación de la función que, a su vez, contiene la dirección URL de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="c5e0b-116">La función utiliza esta dirección URL para construir las operaciones de REST necesarias en su aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-116">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="c5e0b-117">[Creará una configuración de aplicación en la aplicación de la función]() que contiene la dirección URL de la aplicación móvil (cuyo aspecto es como `http://<appname>.azurewebsites.net`) y después especificará el nombre de la configuración de la aplicación en la propiedad `connection` en el enlace de entrada.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="c5e0b-118">Debe especificar `apiKey` si [implementa una clave de API en el back-end de aplicación móvil de Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key) o [implementa una clave de API en el back-end de aplicación móvil de .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="c5e0b-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="c5e0b-119">Para hacer esto, [creará una configuración de aplicación en la aplicación de la función]() que contiene la clave de API y después agregará la propiedad `apiKey` en el enlace de entrada con el nombre de la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="c5e0b-120">Esta clave de API no se debe compartir con los clientes de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="c5e0b-121">Solo se debe distribuir de forma segura a los clientes del servicio, como Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-121">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="c5e0b-122">Azure Functions almacena la información de conexión y las claves de API como configuración de la aplicación de forma que no se protegen en el repositorio de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="c5e0b-123">Esto protege la información confidencial.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="c5e0b-124">Uso de entradas</span><span class="sxs-lookup"><span data-stu-id="c5e0b-124">Input usage</span></span>
<span data-ttu-id="c5e0b-125">En esta sección se muestra cómo utilizar el enlace de entrada de Mobile Apps en el código de función.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-125">This section shows you how to use your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="c5e0b-126">Cuando se encuentra el registro con la tabla especificada y un identificador de registro, se pasa en el parámetro denominado [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) (o, en Node.js, se pasa en el objeto `context.bindings.<name>`).</span><span class="sxs-lookup"><span data-stu-id="c5e0b-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span></span> <span data-ttu-id="c5e0b-127">Si no se encuentra el registro, el parámetro es `null`.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-127">When the record is not found, the parameter is `null`.</span></span> 

<span data-ttu-id="c5e0b-128">En funciones de C# y F#, los cambios realizados en el registro de entrada (parámetro de entrada) se devuelven automáticamente a la tabla de Mobile Apps cuando la función termina correctamente.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span></span> <span data-ttu-id="c5e0b-129">En las funciones de Node.js, use `context.bindings.<name>` para acceder al registro de entrada.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span></span> <span data-ttu-id="c5e0b-130">No se puede modificar un registro en Node.js.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="c5e0b-131">Ejemplo de entrada</span><span class="sxs-lookup"><span data-stu-id="c5e0b-131">Input sample</span></span>
<span data-ttu-id="c5e0b-132">Suponga que tiene el siguiente function.json, que recupera un registro de tabla de Mobile Apps con el identificador del mensaje de desencadenador de cola:</span><span class="sxs-lookup"><span data-stu-id="c5e0b-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span></span>

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

<span data-ttu-id="c5e0b-133">Vea el ejemplo específico del idioma que utiliza el registro de entrada del enlace.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-133">See the language-specific sample that uses the input record from the binding.</span></span> <span data-ttu-id="c5e0b-134">Los ejemplos de C# y F # también modifican la propiedad `text` del registro.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-134">The C# and F# samples also modify the record's `text` property.</span></span>

* [<span data-ttu-id="c5e0b-135">C#</span><span class="sxs-lookup"><span data-stu-id="c5e0b-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="c5e0b-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="c5e0b-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="c5e0b-137">Ejemplo de entrada en C#</span><span class="sxs-lookup"><span data-stu-id="c5e0b-137">Input sample in C#</span></span> #

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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="c5e0b-138">Ejemplo de entrada en Node.js</span><span class="sxs-lookup"><span data-stu-id="c5e0b-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="c5e0b-139">Enlace de salida de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="c5e0b-139">Mobile Apps output binding</span></span>
<span data-ttu-id="c5e0b-140">Utilice el enlace de salida Mobile Apps para escribir un registro en un punto de conexión de tabla de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="c5e0b-141">La salida de Mobile Apps para una función usa el siguiente objeto JSON en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="c5e0b-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="c5e0b-142">Tenga en cuenta lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c5e0b-142">Note the following:</span></span>

* <span data-ttu-id="c5e0b-143">`connection` debe contener el nombre de una configuración de aplicación en la aplicación de la función que, a su vez, contiene la dirección URL de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="c5e0b-144">La función utiliza esta dirección URL para construir las operaciones de REST necesarias en su aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-144">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="c5e0b-145">[Creará una configuración de aplicación en la aplicación de la función]() que contiene la dirección URL de la aplicación móvil (cuyo aspecto es como `http://<appname>.azurewebsites.net`) y después especificará el nombre de la configuración de la aplicación en la propiedad `connection` en el enlace de entrada.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="c5e0b-146">Debe especificar `apiKey` si [implementa una clave de API en el back-end de aplicación móvil de Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key) o [implementa una clave de API en el back-end de aplicación móvil de .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="c5e0b-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="c5e0b-147">Para hacer esto, [creará una configuración de aplicación en la aplicación de la función]() que contiene la clave de API y después agregará la propiedad `apiKey` en el enlace de entrada con el nombre de la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="c5e0b-148">Esta clave de API no se debe compartir con los clientes de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="c5e0b-149">Solo se debe distribuir de forma segura a los clientes del servicio, como Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-149">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="c5e0b-150">Azure Functions almacena la información de conexión y las claves de API como configuración de la aplicación de forma que no se protegen en el repositorio de control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="c5e0b-151">Esto protege la información confidencial.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="c5e0b-152">Uso de salidas</span><span class="sxs-lookup"><span data-stu-id="c5e0b-152">Output usage</span></span>
<span data-ttu-id="c5e0b-153">En esta sección se muestra cómo utilizar el enlace de salida de Mobile Apps en el código de función.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-153">This section shows you how to use your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="c5e0b-154">En funciones de C#, utilice un parámetro de salida con nombre de tipo `out object` para acceder al registro de salida.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="c5e0b-155">En las funciones de Node.js, use `context.bindings.<name>` para acceder al registro de salida.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="c5e0b-156">Ejemplo de salida</span><span class="sxs-lookup"><span data-stu-id="c5e0b-156">Output sample</span></span>
<span data-ttu-id="c5e0b-157">Suponga que tiene la siguiente function.json que define un desencadenador de cola y una salida de Mobile Apps:</span><span class="sxs-lookup"><span data-stu-id="c5e0b-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

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

<span data-ttu-id="c5e0b-158">Vea el ejemplo específico del idioma que crea un registro en el punto de conexión de la tabla de Mobile Apps con el contenido del mensaje de cola.</span><span class="sxs-lookup"><span data-stu-id="c5e0b-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span></span>

* [<span data-ttu-id="c5e0b-159">C#</span><span class="sxs-lookup"><span data-stu-id="c5e0b-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="c5e0b-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="c5e0b-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="c5e0b-161">Ejemplo de salida en C#</span><span class="sxs-lookup"><span data-stu-id="c5e0b-161">Output sample in C#</span></span> #

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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="c5e0b-162">Ejemplo de salida en Node.js</span><span class="sxs-lookup"><span data-stu-id="c5e0b-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="c5e0b-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c5e0b-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

