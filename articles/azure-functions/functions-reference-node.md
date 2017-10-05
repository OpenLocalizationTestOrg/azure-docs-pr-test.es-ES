---
title: Referencia para desarrolladores de JavaScript para Azure Functions | Microsoft Docs
description: "Obtenga información sobre cómo desarrollar funciones con JavaScript."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure funciones, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 7ea81ed47f391fbce1432c2b11ac176ab6c04ae0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="51f2a-104">Guía para el desarrollador de JavaScript para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="51f2a-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="51f2a-105">Script de C#</span><span class="sxs-lookup"><span data-stu-id="51f2a-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="51f2a-106">Script de F#</span><span class="sxs-lookup"><span data-stu-id="51f2a-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="51f2a-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="51f2a-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="51f2a-108">La experiencia de JavaScript para Azure Functions facilita la exportación de una función en que se transmite como un objeto `context` para comunicarse con el sistema en tiempo de ejecución, y recibir y enviar datos por medio de enlaces.</span><span class="sxs-lookup"><span data-stu-id="51f2a-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed as a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="51f2a-109">En este artículo se supone que ya ha leído [Referencia para desarrolladores de Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="51f2a-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="51f2a-110">Exportación de una función</span><span class="sxs-lookup"><span data-stu-id="51f2a-110">Exporting a function</span></span>
<span data-ttu-id="51f2a-111">Todas las funciones de JavaScript tiene que exportar un elemento `function` único mediante `module.exports` para que el sistema en tiempo de ejecución encuentre la función y la ejecute.</span><span class="sxs-lookup"><span data-stu-id="51f2a-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span></span> <span data-ttu-id="51f2a-112">Esta función siempre tiene que incluir un objeto `context` .</span><span class="sxs-lookup"><span data-stu-id="51f2a-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by the arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="51f2a-113">Los enlaces de `direction === "in"` se transmiten como argumentos de la función, lo que significa que se pueden usar [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) para controlar de forma dinámica las entradas nuevas (por ejemplo, con el uso de `arguments.length` para iterar en todas las entradas).</span><span class="sxs-lookup"><span data-stu-id="51f2a-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span></span> <span data-ttu-id="51f2a-114">Esta funcionalidad resulta conveniente si solo dispone de un desencadenador sin entradas adicionales, ya que puede acceder de manera predecible a los datos del desencadenador sin hacer referencia al objeto `context`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="51f2a-115">Los argumentos siempre se transmiten a la función en el orden en el que figuran en *function.json*, aunque no los especifique en la instrucción de exportaciones.</span><span class="sxs-lookup"><span data-stu-id="51f2a-115">The arguments are always passed along to the function in the order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="51f2a-116">Por ejemplo, si tiene la función `function(context, a, b)` y la cambia a `function(context, a)`, podrá seguir obteniendo el valor `b` en el código de función si hace referencia a `arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span></span>

<span data-ttu-id="51f2a-117">Todos los enlaces, al margen de la dirección, también se transmiten junto con el objeto `context` (consulte el script siguiente).</span><span class="sxs-lookup"><span data-stu-id="51f2a-117">All bindings, regardless of direction, are also passed along on the `context` object (see the following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="51f2a-118">objeto de contexto</span><span class="sxs-lookup"><span data-stu-id="51f2a-118">context object</span></span>
<span data-ttu-id="51f2a-119">El sistema en tiempo de ejecución usa un objeto `context` para transmitir datos desde la función y hacia esta, así como para posibilitar la comunicación con dicho sistema en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="51f2a-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span></span>

<span data-ttu-id="51f2a-120">El objeto de contexto siempre es el primer parámetro de una función y se debe incluir, porque incorpora métodos como `context.done` y `context.log`, que se precisan para usar correctamente el sistema en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="51f2a-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log`, which are required to use the runtime correctly.</span></span> <span data-ttu-id="51f2a-121">Puede asignar el nombre que desee al objeto (por ejemplo, `ctx` o `c`).</span><span class="sxs-lookup"><span data-stu-id="51f2a-121">You can name the object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="51f2a-122">Propiedad context.bindings</span><span class="sxs-lookup"><span data-stu-id="51f2a-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="51f2a-123">Devuelve un objeto con nombre que contiene todos los datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="51f2a-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="51f2a-124">Por ejemplo, la siguiente definición de enlace en *function.json* permite acceder al contenido de la cola desde el objeto `context.bindings.myInput`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-124">For example, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains the input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="51f2a-125">Método context.done</span><span class="sxs-lookup"><span data-stu-id="51f2a-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="51f2a-126">Informa al tiempo de ejecución de que el código ha terminado.</span><span class="sxs-lookup"><span data-stu-id="51f2a-126">Informs the runtime that your code has finished.</span></span> <span data-ttu-id="51f2a-127">Debe llamar a `context.done` o, de lo contrario, el tiempo de ejecución nunca sabe que la función se ha completado y, por tanto, se agota el tiempo de espera de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="51f2a-127">You must call `context.done`, or else the runtime never knows that your function is complete, and the execution will time out.</span></span> 

<span data-ttu-id="51f2a-128">El método `context.done` permite transmitir un error definido por el usuario al sistema en tiempo de ejecución y un contenedor de propiedades que sobrescribirá las propiedades del objeto `context.bindings`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-128">The `context.done` method allows you to pass back both a user-defined error to the runtime and a property bag of properties that overwrite the properties on the `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="51f2a-129">Método context.log</span><span class="sxs-lookup"><span data-stu-id="51f2a-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="51f2a-130">Permite escribir en los registros de la consola de streaming en el nivel de seguimiento predeterminado.</span><span class="sxs-lookup"><span data-stu-id="51f2a-130">Allows you to write to the streaming console logs at the default trace level.</span></span> <span data-ttu-id="51f2a-131">Hay métodos de registro adicionales disponibles en `context.log` que permiten escribir en el registro de la consola en otros niveles de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="51f2a-131">On `context.log`, additional logging methods are available that let you write to the console log at other trace levels:</span></span>


| <span data-ttu-id="51f2a-132">Método</span><span class="sxs-lookup"><span data-stu-id="51f2a-132">Method</span></span>                 | <span data-ttu-id="51f2a-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="51f2a-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="51f2a-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="51f2a-134">**error(_message_)**</span></span>   | <span data-ttu-id="51f2a-135">Escribe en el registro de nivel de error o inferior.</span><span class="sxs-lookup"><span data-stu-id="51f2a-135">Writes to error level logging, or lower.</span></span>   |
| <span data-ttu-id="51f2a-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="51f2a-136">**warn(_message_)**</span></span>    | <span data-ttu-id="51f2a-137">Escribe en el registro de nivel de advertencia o inferior.</span><span class="sxs-lookup"><span data-stu-id="51f2a-137">Writes to warning level logging, or lower.</span></span> |
| <span data-ttu-id="51f2a-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="51f2a-138">**info(_message_)**</span></span>    | <span data-ttu-id="51f2a-139">Escribe en el registro de nivel de información o inferior.</span><span class="sxs-lookup"><span data-stu-id="51f2a-139">Writes to info level logging, or lower.</span></span>    |
| <span data-ttu-id="51f2a-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="51f2a-140">**verbose(_message_)**</span></span> | <span data-ttu-id="51f2a-141">Escribe en el registro de nivel detallado.</span><span class="sxs-lookup"><span data-stu-id="51f2a-141">Writes to verbose level logging.</span></span>           |

<span data-ttu-id="51f2a-142">En el ejemplo siguiente se escribe en la consola en el nivel de seguimiento de advertencia:</span><span class="sxs-lookup"><span data-stu-id="51f2a-142">The following example writes to the console at the warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="51f2a-143">Puede establecer el umbral de nivel de seguimiento de los registros en el archivo host.json o desactivarlo.</span><span class="sxs-lookup"><span data-stu-id="51f2a-143">You can set the trace-level threshold for logging in the host.json file, or turn it off.</span></span>  <span data-ttu-id="51f2a-144">Para obtener más información sobre cómo escribir en los registros, vea la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="51f2a-144">For more information about how to write to the logs, see the next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="51f2a-145">Tipo de datos de enlace</span><span class="sxs-lookup"><span data-stu-id="51f2a-145">Binding data type</span></span>

<span data-ttu-id="51f2a-146">Para definir el tipo de datos para un enlace de entrada, use la propiedad `dataType` de la definición del enlace.</span><span class="sxs-lookup"><span data-stu-id="51f2a-146">To define the data type for an input binding, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="51f2a-147">Por ejemplo, para leer el contenido de una solicitud HTTP en formato binario, use el tipo `binary`:</span><span class="sxs-lookup"><span data-stu-id="51f2a-147">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="51f2a-148">Otras opciones para `dataType` son `stream` y `string`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-to-the-console"></a><span data-ttu-id="51f2a-149">Escribir las salidas de seguimiento en la consola</span><span class="sxs-lookup"><span data-stu-id="51f2a-149">Writing trace output to the console</span></span> 

<span data-ttu-id="51f2a-150">En Functions, use los métodos `context.log` para escribir la salida de seguimiento en la consola.</span><span class="sxs-lookup"><span data-stu-id="51f2a-150">In Functions, you use the `context.log` methods to write trace output to the console.</span></span> <span data-ttu-id="51f2a-151">En este momento, no puede usar `console.log` para escribir en la consola.</span><span class="sxs-lookup"><span data-stu-id="51f2a-151">At this point, you cannot use `console.log` to write to the console.</span></span>

<span data-ttu-id="51f2a-152">Cuando se llama a `context.log()`, el mensaje se escribe en la consola en el nivel de seguimiento predeterminado, que es el nivel de seguimiento de _información_.</span><span class="sxs-lookup"><span data-stu-id="51f2a-152">When you call `context.log()`, your message is written to the console at the default trace level, which is the _info_ trace level.</span></span> <span data-ttu-id="51f2a-153">El siguiente código escribe en la consola en el nivel de seguimiento de información:</span><span class="sxs-lookup"><span data-stu-id="51f2a-153">The following code writes to the console at the info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="51f2a-154">El código anterior es equivalente al siguiente:</span><span class="sxs-lookup"><span data-stu-id="51f2a-154">The preceding code is equivalent to the following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="51f2a-155">El siguiente código escribe en la consola en el nivel de seguimiento de error:</span><span class="sxs-lookup"><span data-stu-id="51f2a-155">The following code writes to the console at the error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="51f2a-156">Dado que _error_ es el nivel de seguimiento más alto, este seguimiento se escribe en la salida en todos los niveles de seguimiento, siempre y cuando el registro esté habilitado.</span><span class="sxs-lookup"><span data-stu-id="51f2a-156">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="51f2a-157">Todos los métodos `context.log` admiten el mismo formato de parámetro que el [método util.format](https://nodejs.org/api/util.html#util_util_format_format) de Node.js.</span><span class="sxs-lookup"><span data-stu-id="51f2a-157">All `context.log` methods support the same parameter format that's supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="51f2a-158">Considere el siguiente código que escribe en la consola mediante el nivel de seguimiento predeterminado:</span><span class="sxs-lookup"><span data-stu-id="51f2a-158">Consider the following code, which writes to the console by using the default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="51f2a-159">También puede escribir el mismo código con el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="51f2a-159">You can also write the same code in the following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a><span data-ttu-id="51f2a-160">Configuración del nivel de seguimiento para el registro de la consola</span><span class="sxs-lookup"><span data-stu-id="51f2a-160">Configure the trace level for console logging</span></span>

<span data-ttu-id="51f2a-161">Functions permite definir el nivel de seguimiento de umbral para escribir en la consola, que facilita el control de la forma en que se escriben los seguimientos en la consola desde las funciones.</span><span class="sxs-lookup"><span data-stu-id="51f2a-161">Functions lets you define the threshold trace level for writing to the console, which makes it easy to control the way traces are written to the console from your functions.</span></span> <span data-ttu-id="51f2a-162">Para establecer el umbral para todos los seguimientos que se escriben en la consola, use la propiedad `tracing.consoleLevel` en el archivo host.json .</span><span class="sxs-lookup"><span data-stu-id="51f2a-162">To set the threshold for all traces written to the console, use the `tracing.consoleLevel` property in the host.json file.</span></span> <span data-ttu-id="51f2a-163">Esta configuración se aplica a todas las funciones de Function App.</span><span class="sxs-lookup"><span data-stu-id="51f2a-163">This setting applies to all functions in your function app.</span></span> <span data-ttu-id="51f2a-164">En el ejemplo siguiente se establece el umbral de seguimiento para habilitar el registro detallado:</span><span class="sxs-lookup"><span data-stu-id="51f2a-164">The following example sets the trace threshold to enable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="51f2a-165">Los valores de **consoleLevel** corresponden a los nombres de los métodos `context.log`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-165">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span></span> <span data-ttu-id="51f2a-166">Para deshabilitar todos los registros de seguimiento en la consola, establezca **consoleLevel** en _off_.</span><span class="sxs-lookup"><span data-stu-id="51f2a-166">To disable all trace logging to the console, set **consoleLevel** to _off_.</span></span> <span data-ttu-id="51f2a-167">Para obtener más información sobre el archivo host.json, vea el [tema de referencia de host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="51f2a-167">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="51f2a-168">Desencadenadores y enlaces HTTP</span><span class="sxs-lookup"><span data-stu-id="51f2a-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="51f2a-169">Los desencadenadores HTTP y de webhook trigger y los enlaces de salida HTTP usan objetos de solicitud y respuesta para representar la mensajería HTTP.</span><span class="sxs-lookup"><span data-stu-id="51f2a-169">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="51f2a-170">Objeto de solicitud</span><span class="sxs-lookup"><span data-stu-id="51f2a-170">Request object</span></span>

<span data-ttu-id="51f2a-171">El objeto `request` tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="51f2a-171">The `request` object has the following properties:</span></span>

| <span data-ttu-id="51f2a-172">Propiedad</span><span class="sxs-lookup"><span data-stu-id="51f2a-172">Property</span></span>      | <span data-ttu-id="51f2a-173">Descripción</span><span class="sxs-lookup"><span data-stu-id="51f2a-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="51f2a-174">_body_</span><span class="sxs-lookup"><span data-stu-id="51f2a-174">_body_</span></span>        | <span data-ttu-id="51f2a-175">Objeto que contiene el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="51f2a-175">An object that contains the body of the request.</span></span>               |
| <span data-ttu-id="51f2a-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="51f2a-176">_headers_</span></span>     | <span data-ttu-id="51f2a-177">Objeto que contiene los encabezados de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="51f2a-177">An object that contains the request headers.</span></span>                   |
| <span data-ttu-id="51f2a-178">_method_</span><span class="sxs-lookup"><span data-stu-id="51f2a-178">_method_</span></span>      | <span data-ttu-id="51f2a-179">Método HTTP de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="51f2a-179">The HTTP method of the request.</span></span>                                |
| <span data-ttu-id="51f2a-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="51f2a-180">_originalUrl_</span></span> | <span data-ttu-id="51f2a-181">Dirección URL de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="51f2a-181">The URL of the request.</span></span>                                        |
| <span data-ttu-id="51f2a-182">_params_</span><span class="sxs-lookup"><span data-stu-id="51f2a-182">_params_</span></span>      | <span data-ttu-id="51f2a-183">Objeto que contiene los parámetros de enrutamiento de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="51f2a-183">An object that contains the routing parameters of the request.</span></span> |
| <span data-ttu-id="51f2a-184">_consulta_</span><span class="sxs-lookup"><span data-stu-id="51f2a-184">_query_</span></span>       | <span data-ttu-id="51f2a-185">Objeto que contiene los parámetros de consulta.</span><span class="sxs-lookup"><span data-stu-id="51f2a-185">An object that contains the query parameters.</span></span>                  |
| <span data-ttu-id="51f2a-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="51f2a-186">_rawBody_</span></span>     | <span data-ttu-id="51f2a-187">Cuerpo del mensaje como una cadena.</span><span class="sxs-lookup"><span data-stu-id="51f2a-187">The body of the message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="51f2a-188">Objeto de respuesta</span><span class="sxs-lookup"><span data-stu-id="51f2a-188">Response object</span></span>

<span data-ttu-id="51f2a-189">El objeto `response` tiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="51f2a-189">The `response` object has the following properties:</span></span>

| <span data-ttu-id="51f2a-190">Propiedad</span><span class="sxs-lookup"><span data-stu-id="51f2a-190">Property</span></span>  | <span data-ttu-id="51f2a-191">Descripción</span><span class="sxs-lookup"><span data-stu-id="51f2a-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="51f2a-192">_body_</span><span class="sxs-lookup"><span data-stu-id="51f2a-192">_body_</span></span>    | <span data-ttu-id="51f2a-193">Objeto que contiene el cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="51f2a-193">An object that contains the body of the response.</span></span>         |
| <span data-ttu-id="51f2a-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="51f2a-194">_headers_</span></span> | <span data-ttu-id="51f2a-195">Objeto que contiene los encabezados de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="51f2a-195">An object that contains the response headers.</span></span>             |
| <span data-ttu-id="51f2a-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="51f2a-196">_isRaw_</span></span>   | <span data-ttu-id="51f2a-197">Indica que se omite el formato en la respuesta.</span><span class="sxs-lookup"><span data-stu-id="51f2a-197">Indicates that formatting is skipped for the response.</span></span>    |
| <span data-ttu-id="51f2a-198">_estado_</span><span class="sxs-lookup"><span data-stu-id="51f2a-198">_status_</span></span>  | <span data-ttu-id="51f2a-199">Código de estado HTTP de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="51f2a-199">The HTTP status code of the response.</span></span>                     |

### <a name="accessing-the-request-and-response"></a><span data-ttu-id="51f2a-200">Acceso a solicitudes y respuestas</span><span class="sxs-lookup"><span data-stu-id="51f2a-200">Accessing the request and response</span></span> 

<span data-ttu-id="51f2a-201">Cuando se trabaja con desencadenadores HTTP, hay tres maneras de acceder a los objetos de solicitud y respuesta HTTP:</span><span class="sxs-lookup"><span data-stu-id="51f2a-201">When you work with HTTP triggers, you can access the HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="51f2a-202">Desde los enlaces de entrada y salida con nombre.</span><span class="sxs-lookup"><span data-stu-id="51f2a-202">From the named input and output bindings.</span></span> <span data-ttu-id="51f2a-203">De esta manera, el desencadenador HTTP y los enlaces funcionan igual que cualquier otro enlace.</span><span class="sxs-lookup"><span data-stu-id="51f2a-203">In this way, the HTTP trigger and bindings work the same as any other binding.</span></span> <span data-ttu-id="51f2a-204">En el ejemplo siguiente se establece el objeto de respuesta mediante un enlace `response` con nombre:</span><span class="sxs-lookup"><span data-stu-id="51f2a-204">The following example sets the response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="51f2a-205">Desde las propiedades `req` y `res` del objeto `context`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-205">From `req` and `res` properties on the `context` object.</span></span> <span data-ttu-id="51f2a-206">De esta manera, puede usar el patrón convencional para acceder a los datos HTTP desde el objeto de contexto, en lugar de tener que utilizar el patrón `context.bindings.name` completo.</span><span class="sxs-lookup"><span data-stu-id="51f2a-206">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span></span> <span data-ttu-id="51f2a-207">En el ejemplo siguiente se muestra cómo acceder a los objetos `req` y `res` en `context`:</span><span class="sxs-lookup"><span data-stu-id="51f2a-207">The following example shows how to access the `req` and `res` objects on the `context`:</span></span>

    ```javascript
    // You can access your http request off the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="51f2a-208">Mediante una llamada a `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-208">By calling `context.done()`.</span></span> <span data-ttu-id="51f2a-209">Un tipo especial de enlace HTTP que devuelve la respuesta que se pasa al método `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-209">A special kind of HTTP binding returns the response that is passed to the `context.done()` method.</span></span> <span data-ttu-id="51f2a-210">El enlace de salida HTTP siguiente define un parámetro de salida `$return`:</span><span class="sxs-lookup"><span data-stu-id="51f2a-210">The following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="51f2a-211">Este enlace de salida espera que proporcione la respuesta cuando se llama a `done()`, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="51f2a-211">This output binding expects you to supply the response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="51f2a-212">Versión de Node y administración de paquetes</span><span class="sxs-lookup"><span data-stu-id="51f2a-212">Node version and Package Management</span></span>
<span data-ttu-id="51f2a-213">Actualmente, la versión de Node está bloqueada en `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-213">The node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="51f2a-214">Estamos investigando para agregar compatibilidad con más versiones y hacerlo configurable.</span><span class="sxs-lookup"><span data-stu-id="51f2a-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="51f2a-215">Los pasos siguientes le permiten incluir paquetes en Function App:</span><span class="sxs-lookup"><span data-stu-id="51f2a-215">The following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="51f2a-216">Vaya a `https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="51f2a-216">Go to `https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="51f2a-217">Haga clic en **Consola de depuración** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="51f2a-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="51f2a-218">Vaya a `D:\home\site\wwwroot` y luego arrastre el archivo package.json a la carpeta **wwwroot** en la mitad superior de la página.</span><span class="sxs-lookup"><span data-stu-id="51f2a-218">Go to `D:\home\site\wwwroot`, and then drag your package.json file to the **wwwroot** folder at the top half of the page.</span></span>  
    <span data-ttu-id="51f2a-219">También puede cargar archivos en Function App de otras formas.</span><span class="sxs-lookup"><span data-stu-id="51f2a-219">You can upload files to your function app in other ways also.</span></span> <span data-ttu-id="51f2a-220">Para obtener más información, vea [Actualización de los archivos de aplicación de función](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="51f2a-220">For more information, see [How to update function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="51f2a-221">Una vez cargado el archivo package.json, ejecute el comando`npm install` en la **consola de ejecución remota de Kudu**.</span><span class="sxs-lookup"><span data-stu-id="51f2a-221">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="51f2a-222">Esta acción descarga los paquetes indicados en el archivo package.json y se reinicia Function App.</span><span class="sxs-lookup"><span data-stu-id="51f2a-222">This action downloads the packages indicated in the package.json file and restarts the function app.</span></span>

<span data-ttu-id="51f2a-223">Una vez que se hayan instalado los paquetes que necesita, impórtelos a la función llamando a `require('packagename')`, como en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="51f2a-223">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example:</span></span>

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="51f2a-224">Debe definir un archivo `package.json` en la raíz de Function App.</span><span class="sxs-lookup"><span data-stu-id="51f2a-224">You should define a `package.json` file at the root of your function app.</span></span> <span data-ttu-id="51f2a-225">La definición del archivo permite que todas las funciones de la aplicación compartan los mismos paquetes almacenados en caché, de tal manera que se ofrece el mejor rendimiento.</span><span class="sxs-lookup"><span data-stu-id="51f2a-225">Defining the file lets all functions in the app share the same cached packages, which gives the best performance.</span></span> <span data-ttu-id="51f2a-226">Cuando hay conflictos con una versión, puede resolverlo mediante la adición de un archivo `package.json` en la carpeta de una función específica.</span><span class="sxs-lookup"><span data-stu-id="51f2a-226">If a version conflict arises, you can resolve it by adding a `package.json` file in the folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="51f2a-227">Variables de entorno</span><span class="sxs-lookup"><span data-stu-id="51f2a-227">Environment variables</span></span>
<span data-ttu-id="51f2a-228">Para obtener una variable de entorno o un valor de configuración de aplicación, use `process.env`, como se muestra en el ejemplo de código siguiente:</span><span class="sxs-lookup"><span data-stu-id="51f2a-228">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="51f2a-229">Consideraciones para las funciones de JavaScript</span><span class="sxs-lookup"><span data-stu-id="51f2a-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="51f2a-230">Cuando se trabaja con las funciones de JavaScript, tenga en cuenta las consideraciones de las dos secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="51f2a-230">When you work with JavaScript functions, be aware of the considerations in the following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="51f2a-231">Elección de los planes de App Service de un solo núcleo</span><span class="sxs-lookup"><span data-stu-id="51f2a-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="51f2a-232">Al crear una Function App que usa el plan de App Service, se recomienda que seleccione un plan de un solo núcleo en lugar de un plan con varios núcleos.</span><span class="sxs-lookup"><span data-stu-id="51f2a-232">When you create a function app that uses the App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="51f2a-233">En la actualidad, Functions ejecuta funciones de JavaScript con más eficacia en máquina virtuales con un solo núcleo; el uso de máquinas virtuales más grandes no produce las mejoras de rendimiento esperadas.</span><span class="sxs-lookup"><span data-stu-id="51f2a-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce the expected performance improvements.</span></span> <span data-ttu-id="51f2a-234">Cuando sea necesario, puede escalar horizontalmente de forma manual mediante la adición de más instancias de máquina virtual de un solo núcleo, o bien puede habilitar el escalado automático.</span><span class="sxs-lookup"><span data-stu-id="51f2a-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="51f2a-235">Para obtener más información, consulte [Escalación del recuento de instancias de forma manual o automática](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51f2a-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="51f2a-236">Compatibilidad con TypeScript y CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="51f2a-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="51f2a-237">Como no hay compatibilidad directa con la compilación automática de TypeScript o CoffeeScript a través del tiempo de ejecución, dicha compatibilidad debe controlarse fuera del tiempo de ejecución, en tiempo de implementación.</span><span class="sxs-lookup"><span data-stu-id="51f2a-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via the runtime, such support needs to be handled outside the runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="51f2a-238">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="51f2a-238">Next steps</span></span>
<span data-ttu-id="51f2a-239">Para obtener más información, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="51f2a-239">For more information, see the following resources:</span></span>

* [<span data-ttu-id="51f2a-240">Procedimientos recomendados para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="51f2a-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="51f2a-241">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="51f2a-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="51f2a-242">Referencia para desarrolladores de C# de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="51f2a-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="51f2a-243">Referencia para desarrolladores de F# de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="51f2a-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="51f2a-244">Enlaces y desencadenadores de las Funciones de azure</span><span class="sxs-lookup"><span data-stu-id="51f2a-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

