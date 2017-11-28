---
title: aaaJavaScript material de referencia de funciones de Azure | Documentos de Microsoft
description: "Comprender cómo funciona toodevelop mediante JavaScript."
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
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="60cc9-104">Guía para el desarrollador de JavaScript para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="60cc9-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60cc9-105">Script de C#</span><span class="sxs-lookup"><span data-stu-id="60cc9-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="60cc9-106">Script de F#</span><span class="sxs-lookup"><span data-stu-id="60cc9-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="60cc9-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="60cc9-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="60cc9-108">Hola experiencia de JavaScript para funciones de Azure hace fácil tooexport una función, que se pasa como un `context` objeto para comunicarse con el tiempo de ejecución de Hola y para recibir y enviar datos a través de enlaces.</span><span class="sxs-lookup"><span data-stu-id="60cc9-108">hello JavaScript experience for Azure Functions makes it easy tooexport a function, which is passed as a `context` object for communicating with hello runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="60cc9-109">En este artículo se da por supuesto que ya ha leído hello [material de referencia de funciones de Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="60cc9-109">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="60cc9-110">Exportación de una función</span><span class="sxs-lookup"><span data-stu-id="60cc9-110">Exporting a function</span></span>
<span data-ttu-id="60cc9-111">Todas las funciones de JavaScript deben exportar una sola `function` a través de `module.exports` en tiempo de ejecución de Hola Hola función toofind y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="60cc9-111">All JavaScript functions must export a single `function` via `module.exports` for hello runtime toofind hello function and run it.</span></span> <span data-ttu-id="60cc9-112">Esta función siempre tiene que incluir un objeto `context` .</span><span class="sxs-lookup"><span data-stu-id="60cc9-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="60cc9-113">Enlaces de `direction === "in"` se pasan como argumentos de función, lo que significa que puede usar [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically controlar nuevas entradas (por ejemplo, mediante `arguments.length` tooiterate a través de todas las entradas).</span><span class="sxs-lookup"><span data-stu-id="60cc9-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically handle new inputs (for example, by using `arguments.length` tooiterate over all your inputs).</span></span> <span data-ttu-id="60cc9-114">Esta funcionalidad resulta conveniente si solo dispone de un desencadenador sin entradas adicionales, ya que puede acceder de manera predecible a los datos del desencadenador sin hacer referencia al objeto `context`.</span><span class="sxs-lookup"><span data-stu-id="60cc9-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="60cc9-115">Hola argumentos siempre se pasan a lo largo de la función toohello en orden de hello en el que se producen en *function.json*, incluso si no especifica en la instrucción de exportaciones.</span><span class="sxs-lookup"><span data-stu-id="60cc9-115">hello arguments are always passed along toohello function in hello order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="60cc9-116">Por ejemplo, si tiene `function(context, a, b)` y cámbiela demasiado`function(context, a)`, todavía puede obtener valor de Hola de `b` en el código de función, se hace referencia demasiado`arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="60cc9-116">For example, if you have `function(context, a, b)` and change it too`function(context, a)`, you can still get hello value of `b` in function code by referring too`arguments[3]`.</span></span>

<span data-ttu-id="60cc9-117">Todos los enlaces, independientemente de la dirección, también se pasan en hello `context` (vea la siguiente secuencia de comandos de hello) del objeto.</span><span class="sxs-lookup"><span data-stu-id="60cc9-117">All bindings, regardless of direction, are also passed along on hello `context` object (see hello following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="60cc9-118">objeto de contexto</span><span class="sxs-lookup"><span data-stu-id="60cc9-118">context object</span></span>
<span data-ttu-id="60cc9-119">Hola runtime usa un `context` tooand de datos de objeto toopass de su función y toolet comunicarse con hello en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="60cc9-119">hello runtime uses a `context` object toopass data tooand from your function and toolet you communicate with hello runtime.</span></span>

<span data-ttu-id="60cc9-120">siempre es la primera función de tooa parámetro hello Hello objeto de contexto y se deben incluir, porque tiene métodos, como `context.done` y `context.log`, que están en tiempo de ejecución de toouse necesario Hola correctamente.</span><span class="sxs-lookup"><span data-stu-id="60cc9-120">hello context object is always hello first parameter tooa function and must be included because it has methods such as `context.done` and `context.log`, which are required toouse hello runtime correctly.</span></span> <span data-ttu-id="60cc9-121">Puede asignar un nombre objeto Hola lo que gustaría (por ejemplo, `ctx` o `c`).</span><span class="sxs-lookup"><span data-stu-id="60cc9-121">You can name hello object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="60cc9-122">Propiedad context.bindings</span><span class="sxs-lookup"><span data-stu-id="60cc9-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="60cc9-123">Devuelve un objeto con nombre que contiene todos los datos de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="60cc9-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="60cc9-124">Por ejemplo, Hola después de la definición de enlace en su *function.json* Hola de le permite acceder a contenido de la cola de Hola de hello `context.bindings.myInput` objeto.</span><span class="sxs-lookup"><span data-stu-id="60cc9-124">For example, hello following binding definition in your *function.json* lets you access hello contents of hello queue from hello `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="60cc9-125">Método context.done</span><span class="sxs-lookup"><span data-stu-id="60cc9-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="60cc9-126">Le informa en tiempo de ejecución de Hola que ha terminado el código.</span><span class="sxs-lookup"><span data-stu-id="60cc9-126">Informs hello runtime that your code has finished.</span></span> <span data-ttu-id="60cc9-127">Debe llamar a `context.done`, o else en tiempo de ejecución de hello nunca sabe que la función se ha completado y ejecución de hello agotará el tiempo.</span><span class="sxs-lookup"><span data-stu-id="60cc9-127">You must call `context.done`, or else hello runtime never knows that your function is complete, and hello execution will time out.</span></span> 

<span data-ttu-id="60cc9-128">Hola `context.done` método permite toopass hacer un tiempo de ejecución de toohello de error definidos por el usuario y una bolsa de propiedades de propiedades que se sobrescriban propiedades hello en hello `context.bindings` objeto.</span><span class="sxs-lookup"><span data-stu-id="60cc9-128">hello `context.done` method allows you toopass back both a user-defined error toohello runtime and a property bag of properties that overwrite hello properties on hello `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="60cc9-129">Método context.log</span><span class="sxs-lookup"><span data-stu-id="60cc9-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="60cc9-130">Le permite toowrite toohello streaming registros de la consola en el nivel de seguimiento predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-130">Allows you toowrite toohello streaming console logs at hello default trace level.</span></span> <span data-ttu-id="60cc9-131">En `context.log`, métodos de registro adicionales están disponibles para que le permite escribir el registro de la consola de toohello en otros niveles de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="60cc9-131">On `context.log`, additional logging methods are available that let you write toohello console log at other trace levels:</span></span>


| <span data-ttu-id="60cc9-132">Método</span><span class="sxs-lookup"><span data-stu-id="60cc9-132">Method</span></span>                 | <span data-ttu-id="60cc9-133">Descripción</span><span class="sxs-lookup"><span data-stu-id="60cc9-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="60cc9-134">**error(_message_)**</span><span class="sxs-lookup"><span data-stu-id="60cc9-134">**error(_message_)**</span></span>   | <span data-ttu-id="60cc9-135">Escribe el nivel de tooerror registro o inferior.</span><span class="sxs-lookup"><span data-stu-id="60cc9-135">Writes tooerror level logging, or lower.</span></span>   |
| <span data-ttu-id="60cc9-136">**warn(_message_)**</span><span class="sxs-lookup"><span data-stu-id="60cc9-136">**warn(_message_)**</span></span>    | <span data-ttu-id="60cc9-137">Escribe el nivel de toowarning registro o inferior.</span><span class="sxs-lookup"><span data-stu-id="60cc9-137">Writes toowarning level logging, or lower.</span></span> |
| <span data-ttu-id="60cc9-138">**info(_message_)**</span><span class="sxs-lookup"><span data-stu-id="60cc9-138">**info(_message_)**</span></span>    | <span data-ttu-id="60cc9-139">Escribe el nivel de tooinfo registro o inferior.</span><span class="sxs-lookup"><span data-stu-id="60cc9-139">Writes tooinfo level logging, or lower.</span></span>    |
| <span data-ttu-id="60cc9-140">**verbose(_message_)**</span><span class="sxs-lookup"><span data-stu-id="60cc9-140">**verbose(_message_)**</span></span> | <span data-ttu-id="60cc9-141">Escribe el registro de nivel de tooverbose.</span><span class="sxs-lookup"><span data-stu-id="60cc9-141">Writes tooverbose level logging.</span></span>           |

<span data-ttu-id="60cc9-142">Hello en el ejemplo siguiente se escribe toohello consola en el nivel de seguimiento de advertencia de hello:</span><span class="sxs-lookup"><span data-stu-id="60cc9-142">hello following example writes toohello console at hello warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="60cc9-143">Puede establecer el umbral de nivel de seguimiento de hello para iniciar sesión en el archivo de hello host.json o desactivarla.</span><span class="sxs-lookup"><span data-stu-id="60cc9-143">You can set hello trace-level threshold for logging in hello host.json file, or turn it off.</span></span>  <span data-ttu-id="60cc9-144">Para obtener más información acerca de cómo toowrite toohello registros, vea Hola siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="60cc9-144">For more information about how toowrite toohello logs, see hello next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="60cc9-145">Tipo de datos de enlace</span><span class="sxs-lookup"><span data-stu-id="60cc9-145">Binding data type</span></span>

<span data-ttu-id="60cc9-146">toodefine tipo de datos de Hola para un enlace de entrada, usar hello `dataType` propiedad en la definición de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-146">toodefine hello data type for an input binding, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="60cc9-147">Por ejemplo, tooread Hola contenido de una solicitud HTTP en formato binario, usar tipo hello `binary`:</span><span class="sxs-lookup"><span data-stu-id="60cc9-147">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="60cc9-148">Otras opciones para `dataType` son `stream` y `string`.</span><span class="sxs-lookup"><span data-stu-id="60cc9-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-toohello-console"></a><span data-ttu-id="60cc9-149">Consola de toohello de salida de seguimiento de escritura</span><span class="sxs-lookup"><span data-stu-id="60cc9-149">Writing trace output toohello console</span></span> 

<span data-ttu-id="60cc9-150">En las funciones, use hello `context.log` consola toohello de métodos toowrite seguimiento salida.</span><span class="sxs-lookup"><span data-stu-id="60cc9-150">In Functions, you use hello `context.log` methods toowrite trace output toohello console.</span></span> <span data-ttu-id="60cc9-151">En este momento, no puede usar `console.log` toowrite toohello consola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-151">At this point, you cannot use `console.log` toowrite toohello console.</span></span>

<span data-ttu-id="60cc9-152">Cuando se llama a `context.log()`, el mensaje se escribe toohello consola en el nivel de seguimiento predeterminado de hello, que es hello _información_ el nivel de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="60cc9-152">When you call `context.log()`, your message is written toohello console at hello default trace level, which is hello _info_ trace level.</span></span> <span data-ttu-id="60cc9-153">Hello código siguiente escribe toohello consola en el nivel de seguimiento de información de hello:</span><span class="sxs-lookup"><span data-stu-id="60cc9-153">hello following code writes toohello console at hello info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="60cc9-154">Hola código anterior es equivalente toohello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="60cc9-154">hello preceding code is equivalent toohello following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="60cc9-155">Hello código siguiente escribe toohello consola en nivel de error de hello:</span><span class="sxs-lookup"><span data-stu-id="60cc9-155">hello following code writes toohello console at hello error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="60cc9-156">Dado que _error_ es seguimiento mayor de hello nivel, este seguimiento se escribe toohello salida en todos los niveles de seguimiento siempre y cuando el registro está habilitado.</span><span class="sxs-lookup"><span data-stu-id="60cc9-156">Because _error_ is hello highest trace level, this trace is written toohello output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="60cc9-157">Todos los `context.log` métodos admiten Hola mismo formato de parámetro que sea compatible con hello Node.js [util.format método](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="60cc9-157">All `context.log` methods support hello same parameter format that's supported by hello Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="60cc9-158">Considere la posibilidad de hello siguiente código, que escribe toohello consola mediante el uso de nivel de seguimiento predeterminado de hello:</span><span class="sxs-lookup"><span data-stu-id="60cc9-158">Consider hello following code, which writes toohello console by using hello default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="60cc9-159">También puede Hola de escribir el mismo código de hello siguiendo el formato:</span><span class="sxs-lookup"><span data-stu-id="60cc9-159">You can also write hello same code in hello following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a><span data-ttu-id="60cc9-160">Configurar el nivel de seguimiento de hello para el registro de la consola</span><span class="sxs-lookup"><span data-stu-id="60cc9-160">Configure hello trace level for console logging</span></span>

<span data-ttu-id="60cc9-161">Funciones le permite definir el nivel de seguimiento de umbral de Hola para escribir toohello consola, lo que facilita la forma de hello toocontrol fácil los seguimientos se escriben toohello consola desde sus funciones.</span><span class="sxs-lookup"><span data-stu-id="60cc9-161">Functions lets you define hello threshold trace level for writing toohello console, which makes it easy toocontrol hello way traces are written toohello console from your functions.</span></span> <span data-ttu-id="60cc9-162">umbral de hello tooset para todos los seguimientos que se escriben toohello consola, use hello `tracing.consoleLevel` propiedad en el archivo de hello host.json.</span><span class="sxs-lookup"><span data-stu-id="60cc9-162">tooset hello threshold for all traces written toohello console, use hello `tracing.consoleLevel` property in hello host.json file.</span></span> <span data-ttu-id="60cc9-163">Esta configuración aplica a funciones de tooall de la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="60cc9-163">This setting applies tooall functions in your function app.</span></span> <span data-ttu-id="60cc9-164">Hello en el ejemplo siguiente se establece Hola seguimiento umbral tooenable el registro detallado:</span><span class="sxs-lookup"><span data-stu-id="60cc9-164">hello following example sets hello trace threshold tooenable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="60cc9-165">Los valores de **consoleLevel** corresponden toohello nombres de hello `context.log` métodos.</span><span class="sxs-lookup"><span data-stu-id="60cc9-165">Values of **consoleLevel** correspond toohello names of hello `context.log` methods.</span></span> <span data-ttu-id="60cc9-166">registro toohello consola, de todos los seguimiento establecido a toodisable **consoleLevel** too_off_.</span><span class="sxs-lookup"><span data-stu-id="60cc9-166">toodisable all trace logging toohello console, set **consoleLevel** too_off_.</span></span> <span data-ttu-id="60cc9-167">Para obtener más información sobre el archivo de host.json hello, vea hello [tema de referencia de host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="60cc9-167">For more information about hello host.json file, see hello [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="60cc9-168">Desencadenadores y enlaces HTTP</span><span class="sxs-lookup"><span data-stu-id="60cc9-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="60cc9-169">HTTP y desencadenadores de webhook HTTP de salida y enlaces usan solicitud y respuesta objetos toorepresent Hola HTTP mensajería.</span><span class="sxs-lookup"><span data-stu-id="60cc9-169">HTTP and webhook triggers and HTTP output bindings use request and response objects toorepresent hello HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="60cc9-170">Objeto de solicitud</span><span class="sxs-lookup"><span data-stu-id="60cc9-170">Request object</span></span>

<span data-ttu-id="60cc9-171">Hola `request` objeto tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="60cc9-171">hello `request` object has hello following properties:</span></span>

| <span data-ttu-id="60cc9-172">Propiedad</span><span class="sxs-lookup"><span data-stu-id="60cc9-172">Property</span></span>      | <span data-ttu-id="60cc9-173">Descripción</span><span class="sxs-lookup"><span data-stu-id="60cc9-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="60cc9-174">_body_</span><span class="sxs-lookup"><span data-stu-id="60cc9-174">_body_</span></span>        | <span data-ttu-id="60cc9-175">Objeto que contiene el cuerpo de saludo de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-175">An object that contains hello body of hello request.</span></span>               |
| <span data-ttu-id="60cc9-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="60cc9-176">_headers_</span></span>     | <span data-ttu-id="60cc9-177">Objeto que contiene los encabezados de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="60cc9-177">An object that contains hello request headers.</span></span>                   |
| <span data-ttu-id="60cc9-178">_method_</span><span class="sxs-lookup"><span data-stu-id="60cc9-178">_method_</span></span>      | <span data-ttu-id="60cc9-179">método HTTP de solicitud de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-179">hello HTTP method of hello request.</span></span>                                |
| <span data-ttu-id="60cc9-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="60cc9-180">_originalUrl_</span></span> | <span data-ttu-id="60cc9-181">Hola dirección URL de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="60cc9-181">hello URL of hello request.</span></span>                                        |
| <span data-ttu-id="60cc9-182">_params_</span><span class="sxs-lookup"><span data-stu-id="60cc9-182">_params_</span></span>      | <span data-ttu-id="60cc9-183">Objeto que contiene parámetros de enrutamiento de saludo de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-183">An object that contains hello routing parameters of hello request.</span></span> |
| <span data-ttu-id="60cc9-184">_consulta_</span><span class="sxs-lookup"><span data-stu-id="60cc9-184">_query_</span></span>       | <span data-ttu-id="60cc9-185">Objeto que contiene los parámetros de consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-185">An object that contains hello query parameters.</span></span>                  |
| <span data-ttu-id="60cc9-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="60cc9-186">_rawBody_</span></span>     | <span data-ttu-id="60cc9-187">cuerpo de Hello del mensaje de bienvenida de como una cadena.</span><span class="sxs-lookup"><span data-stu-id="60cc9-187">hello body of hello message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="60cc9-188">Objeto de respuesta</span><span class="sxs-lookup"><span data-stu-id="60cc9-188">Response object</span></span>

<span data-ttu-id="60cc9-189">Hola `response` objeto tiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="60cc9-189">hello `response` object has hello following properties:</span></span>

| <span data-ttu-id="60cc9-190">Propiedad</span><span class="sxs-lookup"><span data-stu-id="60cc9-190">Property</span></span>  | <span data-ttu-id="60cc9-191">Descripción</span><span class="sxs-lookup"><span data-stu-id="60cc9-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="60cc9-192">_body_</span><span class="sxs-lookup"><span data-stu-id="60cc9-192">_body_</span></span>    | <span data-ttu-id="60cc9-193">Objeto que contiene el cuerpo de Hola de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-193">An object that contains hello body of hello response.</span></span>         |
| <span data-ttu-id="60cc9-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="60cc9-194">_headers_</span></span> | <span data-ttu-id="60cc9-195">Objeto que contiene los encabezados de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-195">An object that contains hello response headers.</span></span>             |
| <span data-ttu-id="60cc9-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="60cc9-196">_isRaw_</span></span>   | <span data-ttu-id="60cc9-197">Indica que se omite el formato de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-197">Indicates that formatting is skipped for hello response.</span></span>    |
| <span data-ttu-id="60cc9-198">_estado_</span><span class="sxs-lookup"><span data-stu-id="60cc9-198">_status_</span></span>  | <span data-ttu-id="60cc9-199">código de estado HTTP de respuesta de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-199">hello HTTP status code of hello response.</span></span>                     |

### <a name="accessing-hello-request-and-response"></a><span data-ttu-id="60cc9-200">Obtener acceso a la solicitud de Hola y respuesta</span><span class="sxs-lookup"><span data-stu-id="60cc9-200">Accessing hello request and response</span></span> 

<span data-ttu-id="60cc9-201">Cuando se trabaja con desencadenadores HTTP, puede tener acceso a los objetos de solicitud y respuesta HTTP hello en cualquiera de estas tres maneras:</span><span class="sxs-lookup"><span data-stu-id="60cc9-201">When you work with HTTP triggers, you can access hello HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="60cc9-202">De hello denominada entrada y salida de enlaces.</span><span class="sxs-lookup"><span data-stu-id="60cc9-202">From hello named input and output bindings.</span></span> <span data-ttu-id="60cc9-203">De esta manera, desencadenador HTTP de Hola y trabajo de enlaces Hola igual como cualquier otro enlace.</span><span class="sxs-lookup"><span data-stu-id="60cc9-203">In this way, hello HTTP trigger and bindings work hello same as any other binding.</span></span> <span data-ttu-id="60cc9-204">Hello en el ejemplo siguiente se establece Hola respuesta objeto mediante el uso de un conjunto con nombre `response` enlace:</span><span class="sxs-lookup"><span data-stu-id="60cc9-204">hello following example sets hello response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="60cc9-205">De `req` y `res` propiedades en hello `context` objeto.</span><span class="sxs-lookup"><span data-stu-id="60cc9-205">From `req` and `res` properties on hello `context` object.</span></span> <span data-ttu-id="60cc9-206">De esta manera, puede usar datos de tooaccess HTTP de patrón convencional de Hola de objeto de contexto de hello, en lugar de tener toouse Hola completa `context.bindings.name` patrón.</span><span class="sxs-lookup"><span data-stu-id="60cc9-206">In this way, you can use hello conventional pattern tooaccess HTTP data from hello context object, instead of having toouse hello full `context.bindings.name` pattern.</span></span> <span data-ttu-id="60cc9-207">Hola siguiente ejemplo se muestra cómo hello tooaccess `req` y `res` objetos en Hola `context`:</span><span class="sxs-lookup"><span data-stu-id="60cc9-207">hello following example shows how tooaccess hello `req` and `res` objects on hello `context`:</span></span>

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="60cc9-208">Mediante una llamada a `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="60cc9-208">By calling `context.done()`.</span></span> <span data-ttu-id="60cc9-209">Un tipo especial de enlace HTTP devuelve la respuesta de Hola que se pasa toohello `context.done()` método.</span><span class="sxs-lookup"><span data-stu-id="60cc9-209">A special kind of HTTP binding returns hello response that is passed toohello `context.done()` method.</span></span> <span data-ttu-id="60cc9-210">Hola después de HTTP de salida enlace define un `$return` parámetro de salida:</span><span class="sxs-lookup"><span data-stu-id="60cc9-210">hello following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="60cc9-211">Este enlace de salida espera respuesta de hello toosupply cuando se llama a `done()`, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="60cc9-211">This output binding expects you toosupply hello response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="60cc9-212">Versión de Node y administración de paquetes</span><span class="sxs-lookup"><span data-stu-id="60cc9-212">Node version and Package Management</span></span>
<span data-ttu-id="60cc9-213">versión del nodo Hola ya está bloqueada actualmente en `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="60cc9-213">hello node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="60cc9-214">Estamos investigando para agregar compatibilidad con más versiones y hacerlo configurable.</span><span class="sxs-lookup"><span data-stu-id="60cc9-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="60cc9-215">Hola pasos le permiten incluir paquetes en la aplicación de la función:</span><span class="sxs-lookup"><span data-stu-id="60cc9-215">hello following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="60cc9-216">Vaya demasiado`https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="60cc9-216">Go too`https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="60cc9-217">Haga clic en **Consola de depuración** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="60cc9-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="60cc9-218">Vaya demasiado`D:\home\site\wwwroot`y, a continuación, arrastre el toohello de archivo package.json **wwwroot** carpeta a la mitad superior de Hola de página Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-218">Go too`D:\home\site\wwwroot`, and then drag your package.json file toohello **wwwroot** folder at hello top half of hello page.</span></span>  
    <span data-ttu-id="60cc9-219">También puede cargar archivos tooyour función aplicación de otras maneras.</span><span class="sxs-lookup"><span data-stu-id="60cc9-219">You can upload files tooyour function app in other ways also.</span></span> <span data-ttu-id="60cc9-220">Para obtener más información, consulte [forma en que funcionan los archivos de aplicación tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="60cc9-220">For more information, see [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="60cc9-221">Después de carga el archivo de package.json hello, ejecute hello `npm install` comando hello **consola de la ejecución remota de Kudu**.</span><span class="sxs-lookup"><span data-stu-id="60cc9-221">After hello package.json file is uploaded, run hello `npm install` command in hello **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="60cc9-222">Esta acción descarga los paquetes de saludo indicados en el archivo de package.json hello y reinicia la aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="60cc9-222">This action downloads hello packages indicated in hello package.json file and restarts hello function app.</span></span>

<span data-ttu-id="60cc9-223">Después de hello paquetes necesarios están instalados, importarlos tooyour función mediante una llamada a `require('packagename')`, como en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="60cc9-223">After hello packages you need are installed, you import them tooyour function by calling `require('packagename')`, as in hello following example:</span></span>

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="60cc9-224">Debe definir un `package.json` archivo en hello raíz de la aplicación de la función.</span><span class="sxs-lookup"><span data-stu-id="60cc9-224">You should define a `package.json` file at hello root of your function app.</span></span> <span data-ttu-id="60cc9-225">Archivo de definición hello permite todas las funciones de recurso compartido de aplicación Hola Hola mismos paquetes almacenados en caché, que proporciona un rendimiento óptimo Hola.</span><span class="sxs-lookup"><span data-stu-id="60cc9-225">Defining hello file lets all functions in hello app share hello same cached packages, which gives hello best performance.</span></span> <span data-ttu-id="60cc9-226">Si surge un conflicto de versiones, puede resolverlo agregando un `package.json` archivo en la carpeta Hola de una función específica.</span><span class="sxs-lookup"><span data-stu-id="60cc9-226">If a version conflict arises, you can resolve it by adding a `package.json` file in hello folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="60cc9-227">Variables de entorno</span><span class="sxs-lookup"><span data-stu-id="60cc9-227">Environment variables</span></span>
<span data-ttu-id="60cc9-228">tooget una variable de entorno o un valor de configuración de aplicación, utilice `process.env`, tal y como se muestra en el siguiente código de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="60cc9-228">tooget an environment variable or an app setting value, use `process.env`, as shown in hello following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="60cc9-229">Consideraciones para las funciones de JavaScript</span><span class="sxs-lookup"><span data-stu-id="60cc9-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="60cc9-230">Cuando se trabaja con las funciones de JavaScript, tener en cuenta las consideraciones de Hola Hola siguientes dos secciones.</span><span class="sxs-lookup"><span data-stu-id="60cc9-230">When you work with JavaScript functions, be aware of hello considerations in hello following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="60cc9-231">Elección de los planes de App Service de un solo núcleo</span><span class="sxs-lookup"><span data-stu-id="60cc9-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="60cc9-232">Cuando se crea una aplicación de función que use Hola plan de servicio de aplicaciones, se recomienda que seleccione un plan de núcleo en lugar de un plan con varios núcleos.</span><span class="sxs-lookup"><span data-stu-id="60cc9-232">When you create a function app that uses hello App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="60cc9-233">En la actualidad, las funciones se ejecuta funciones de JavaScript más eficazmente en máquinas virtuales de núcleo y usando máquinas virtuales de mayor no producir mejoras de rendimiento de hello esperada.</span><span class="sxs-lookup"><span data-stu-id="60cc9-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce hello expected performance improvements.</span></span> <span data-ttu-id="60cc9-234">Cuando sea necesario, puede escalar horizontalmente de forma manual mediante la adición de más instancias de máquina virtual de un solo núcleo, o bien puede habilitar el escalado automático.</span><span class="sxs-lookup"><span data-stu-id="60cc9-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="60cc9-235">Para obtener más información, consulte [Escalación del recuento de instancias de forma manual o automática](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60cc9-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="60cc9-236">Compatibilidad con TypeScript y CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="60cc9-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="60cc9-237">Debido a la compatibilidad directa aún no existe para TypeScript se compila automáticamente o CoffeeScript a través de hello en tiempo de ejecución, dicha compatibilidad necesario toobe administran fuera de hello en tiempo de ejecución, durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="60cc9-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via hello runtime, such support needs toobe handled outside hello runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="60cc9-238">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="60cc9-238">Next steps</span></span>
<span data-ttu-id="60cc9-239">Para obtener más información, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="60cc9-239">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="60cc9-240">Procedimientos recomendados para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="60cc9-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="60cc9-241">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="60cc9-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="60cc9-242">Referencia para desarrolladores de C# de Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="60cc9-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="60cc9-243">Referencia para desarrolladores de F# de Azure Functions</span><span class="sxs-lookup"><span data-stu-id="60cc9-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="60cc9-244">Enlaces y desencadenadores de las Funciones de azure</span><span class="sxs-lookup"><span data-stu-id="60cc9-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

