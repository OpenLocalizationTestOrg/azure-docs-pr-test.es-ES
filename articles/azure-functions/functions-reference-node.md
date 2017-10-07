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
# <a name="azure-functions-javascript-developer-guide"></a>Guía para el desarrollador de JavaScript para Azure Functions
> [!div class="op_single_selector"]
> * [Script de C#](functions-reference-csharp.md)
> * [Script de F#](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

Hola experiencia de JavaScript para funciones de Azure hace fácil tooexport una función, que se pasa como un `context` objeto para comunicarse con el tiempo de ejecución de Hola y para recibir y enviar datos a través de enlaces.

En este artículo se da por supuesto que ya ha leído hello [material de referencia de funciones de Azure](functions-reference.md).

## <a name="exporting-a-function"></a>Exportación de una función
Todas las funciones de JavaScript deben exportar una sola `function` a través de `module.exports` en tiempo de ejecución de Hola Hola función toofind y ejecútelo. Esta función siempre tiene que incluir un objeto `context` .

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

Enlaces de `direction === "in"` se pasan como argumentos de función, lo que significa que puede usar [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically controlar nuevas entradas (por ejemplo, mediante `arguments.length` tooiterate a través de todas las entradas). Esta funcionalidad resulta conveniente si solo dispone de un desencadenador sin entradas adicionales, ya que puede acceder de manera predecible a los datos del desencadenador sin hacer referencia al objeto `context`.

Hola argumentos siempre se pasan a lo largo de la función toohello en orden de hello en el que se producen en *function.json*, incluso si no especifica en la instrucción de exportaciones. Por ejemplo, si tiene `function(context, a, b)` y cámbiela demasiado`function(context, a)`, todavía puede obtener valor de Hola de `b` en el código de función, se hace referencia demasiado`arguments[3]`.

Todos los enlaces, independientemente de la dirección, también se pasan en hello `context` (vea la siguiente secuencia de comandos de hello) del objeto. 

## <a name="context-object"></a>objeto de contexto
Hola runtime usa un `context` tooand de datos de objeto toopass de su función y toolet comunicarse con hello en tiempo de ejecución.

siempre es la primera función de tooa parámetro hello Hello objeto de contexto y se deben incluir, porque tiene métodos, como `context.done` y `context.log`, que están en tiempo de ejecución de toouse necesario Hola correctamente. Puede asignar un nombre objeto Hola lo que gustaría (por ejemplo, `ctx` o `c`).

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>Propiedad context.bindings

```
context.bindings
```
Devuelve un objeto con nombre que contiene todos los datos de entrada y salida. Por ejemplo, Hola después de la definición de enlace en su *function.json* Hola de le permite acceder a contenido de la cola de Hola de hello `context.bindings.myInput` objeto. 

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

### <a name="contextdone-method"></a>Método context.done
```
context.done([err],[propertyBag])
```

Le informa en tiempo de ejecución de Hola que ha terminado el código. Debe llamar a `context.done`, o else en tiempo de ejecución de hello nunca sabe que la función se ha completado y ejecución de hello agotará el tiempo. 

Hola `context.done` método permite toopass hacer un tiempo de ejecución de toohello de error definidos por el usuario y una bolsa de propiedades de propiedades que se sobrescriban propiedades hello en hello `context.bindings` objeto.

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>Método context.log  

```
context.log(message)
```
Le permite toowrite toohello streaming registros de la consola en el nivel de seguimiento predeterminado de Hola. En `context.log`, métodos de registro adicionales están disponibles para que le permite escribir el registro de la consola de toohello en otros niveles de seguimiento:


| Método                 | Descripción                                |
| ---------------------- | ------------------------------------------ |
| **error(_message_)**   | Escribe el nivel de tooerror registro o inferior.   |
| **warn(_message_)**    | Escribe el nivel de toowarning registro o inferior. |
| **info(_message_)**    | Escribe el nivel de tooinfo registro o inferior.    |
| **verbose(_message_)** | Escribe el registro de nivel de tooverbose.           |

Hello en el ejemplo siguiente se escribe toohello consola en el nivel de seguimiento de advertencia de hello:

```javascript
context.log.warn("Something has happened."); 
```
Puede establecer el umbral de nivel de seguimiento de hello para iniciar sesión en el archivo de hello host.json o desactivarla.  Para obtener más información acerca de cómo toowrite toohello registros, vea Hola siguiente sección.

## <a name="binding-data-type"></a>Tipo de datos de enlace

toodefine tipo de datos de Hola para un enlace de entrada, usar hello `dataType` propiedad en la definición de enlace de Hola. Por ejemplo, tooread Hola contenido de una solicitud HTTP en formato binario, usar tipo hello `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Otras opciones para `dataType` son `stream` y `string`.

## <a name="writing-trace-output-toohello-console"></a>Consola de toohello de salida de seguimiento de escritura 

En las funciones, use hello `context.log` consola toohello de métodos toowrite seguimiento salida. En este momento, no puede usar `console.log` toowrite toohello consola.

Cuando se llama a `context.log()`, el mensaje se escribe toohello consola en el nivel de seguimiento predeterminado de hello, que es hello _información_ el nivel de seguimiento. Hello código siguiente escribe toohello consola en el nivel de seguimiento de información de hello:

```javascript
context.log({hello: 'world'});  
```

Hola código anterior es equivalente toohello siguiente código:

```javascript
context.log.info({hello: 'world'});  
```

Hello código siguiente escribe toohello consola en nivel de error de hello:

```javascript
context.log.error("An error has occurred.");  
```

Dado que _error_ es seguimiento mayor de hello nivel, este seguimiento se escribe toohello salida en todos los niveles de seguimiento siempre y cuando el registro está habilitado.  


Todos los `context.log` métodos admiten Hola mismo formato de parámetro que sea compatible con hello Node.js [util.format método](https://nodejs.org/api/util.html#util_util_format_format). Considere la posibilidad de hello siguiente código, que escribe toohello consola mediante el uso de nivel de seguimiento predeterminado de hello:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

También puede Hola de escribir el mismo código de hello siguiendo el formato:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a>Configurar el nivel de seguimiento de hello para el registro de la consola

Funciones le permite definir el nivel de seguimiento de umbral de Hola para escribir toohello consola, lo que facilita la forma de hello toocontrol fácil los seguimientos se escriben toohello consola desde sus funciones. umbral de hello tooset para todos los seguimientos que se escriben toohello consola, use hello `tracing.consoleLevel` propiedad en el archivo de hello host.json. Esta configuración aplica a funciones de tooall de la aplicación de la función. Hello en el ejemplo siguiente se establece Hola seguimiento umbral tooenable el registro detallado:

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

Los valores de **consoleLevel** corresponden toohello nombres de hello `context.log` métodos. registro toohello consola, de todos los seguimiento establecido a toodisable **consoleLevel** too_off_. Para obtener más información sobre el archivo de host.json hello, vea hello [tema de referencia de host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

## <a name="http-triggers-and-bindings"></a>Desencadenadores y enlaces HTTP

HTTP y desencadenadores de webhook HTTP de salida y enlaces usan solicitud y respuesta objetos toorepresent Hola HTTP mensajería.  

### <a name="request-object"></a>Objeto de solicitud

Hola `request` objeto tiene Hola propiedades siguientes:

| Propiedad      | Descripción                                                    |
| ------------- | -------------------------------------------------------------- |
| _body_        | Objeto que contiene el cuerpo de saludo de solicitud de Hola.               |
| _headers_     | Objeto que contiene los encabezados de solicitud de saludo.                   |
| _method_      | método HTTP de solicitud de Hola Hola.                                |
| _originalUrl_ | Hola dirección URL de solicitud de saludo.                                        |
| _params_      | Objeto que contiene parámetros de enrutamiento de saludo de solicitud de Hola. |
| _consulta_       | Objeto que contiene los parámetros de consulta de Hola.                  |
| _rawBody_     | cuerpo de Hello del mensaje de bienvenida de como una cadena.                           |


### <a name="response-object"></a>Objeto de respuesta

Hola `response` objeto tiene Hola propiedades siguientes:

| Propiedad  | Descripción                                               |
| --------- | --------------------------------------------------------- |
| _body_    | Objeto que contiene el cuerpo de Hola de respuesta de Hola.         |
| _headers_ | Objeto que contiene los encabezados de respuesta de Hola.             |
| _isRaw_   | Indica que se omite el formato de respuesta de Hola.    |
| _estado_  | código de estado HTTP de respuesta de Hola Hola.                     |

### <a name="accessing-hello-request-and-response"></a>Obtener acceso a la solicitud de Hola y respuesta 

Cuando se trabaja con desencadenadores HTTP, puede tener acceso a los objetos de solicitud y respuesta HTTP hello en cualquiera de estas tres maneras:

+ De hello denominada entrada y salida de enlaces. De esta manera, desencadenador HTTP de Hola y trabajo de enlaces Hola igual como cualquier otro enlace. Hello en el ejemplo siguiente se establece Hola respuesta objeto mediante el uso de un conjunto con nombre `response` enlace: 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ De `req` y `res` propiedades en hello `context` objeto. De esta manera, puede usar datos de tooaccess HTTP de patrón convencional de Hola de objeto de contexto de hello, en lugar de tener toouse Hola completa `context.bindings.name` patrón. Hola siguiente ejemplo se muestra cómo hello tooaccess `req` y `res` objetos en Hola `context`:

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ Mediante una llamada a `context.done()`. Un tipo especial de enlace HTTP devuelve la respuesta de Hola que se pasa toohello `context.done()` método. Hola después de HTTP de salida enlace define un `$return` parámetro de salida:

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    Este enlace de salida espera respuesta de hello toosupply cuando se llama a `done()`, como se indica a continuación:

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a>Versión de Node y administración de paquetes
versión del nodo Hola ya está bloqueada actualmente en `6.5.0`. Estamos investigando para agregar compatibilidad con más versiones y hacerlo configurable.

Hola pasos le permiten incluir paquetes en la aplicación de la función: 

1. Vaya demasiado`https://<function_app_name>.scm.azurewebsites.net`.

2. Haga clic en **Consola de depuración** > **CMD**.

3. Vaya demasiado`D:\home\site\wwwroot`y, a continuación, arrastre el toohello de archivo package.json **wwwroot** carpeta a la mitad superior de Hola de página Hola.  
    También puede cargar archivos tooyour función aplicación de otras maneras. Para obtener más información, consulte [forma en que funcionan los archivos de aplicación tooupdate](functions-reference.md#fileupdate). 

4. Después de carga el archivo de package.json hello, ejecute hello `npm install` comando hello **consola de la ejecución remota de Kudu**.  
    Esta acción descarga los paquetes de saludo indicados en el archivo de package.json hello y reinicia la aplicación de la función de hello.

Después de hello paquetes necesarios están instalados, importarlos tooyour función mediante una llamada a `require('packagename')`, como en el siguiente ejemplo de Hola:

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

Debe definir un `package.json` archivo en hello raíz de la aplicación de la función. Archivo de definición hello permite todas las funciones de recurso compartido de aplicación Hola Hola mismos paquetes almacenados en caché, que proporciona un rendimiento óptimo Hola. Si surge un conflicto de versiones, puede resolverlo agregando un `package.json` archivo en la carpeta Hola de una función específica.  

## <a name="environment-variables"></a>Variables de entorno
tooget una variable de entorno o un valor de configuración de aplicación, utilice `process.env`, tal y como se muestra en el siguiente código de ejemplo de Hola:

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
## <a name="considerations-for-javascript-functions"></a>Consideraciones para las funciones de JavaScript

Cuando se trabaja con las funciones de JavaScript, tener en cuenta las consideraciones de Hola Hola siguientes dos secciones.

### <a name="choose-single-core-app-service-plans"></a>Elección de los planes de App Service de un solo núcleo

Cuando se crea una aplicación de función que use Hola plan de servicio de aplicaciones, se recomienda que seleccione un plan de núcleo en lugar de un plan con varios núcleos. En la actualidad, las funciones se ejecuta funciones de JavaScript más eficazmente en máquinas virtuales de núcleo y usando máquinas virtuales de mayor no producir mejoras de rendimiento de hello esperada. Cuando sea necesario, puede escalar horizontalmente de forma manual mediante la adición de más instancias de máquina virtual de un solo núcleo, o bien puede habilitar el escalado automático. Para obtener más información, consulte [Escalación del recuento de instancias de forma manual o automática](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).    

### <a name="typescript-and-coffeescript-support"></a>Compatibilidad con TypeScript y CoffeeScript
Debido a la compatibilidad directa aún no existe para TypeScript se compila automáticamente o CoffeeScript a través de hello en tiempo de ejecución, dicha compatibilidad necesario toobe administran fuera de hello en tiempo de ejecución, durante la implementación. 

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea Hola recursos siguientes:

* [Procedimientos recomendados para Azure Functions](functions-best-practices.md)
* [Azure Functions developer reference](functions-reference.md)
* [Referencia para desarrolladores de C# de Funciones de Azure](functions-reference-csharp.md)
* [Referencia para desarrolladores de F# de Azure Functions](functions-reference-fsharp.md)
* [Enlaces y desencadenadores de las Funciones de azure](functions-triggers-bindings.md)

