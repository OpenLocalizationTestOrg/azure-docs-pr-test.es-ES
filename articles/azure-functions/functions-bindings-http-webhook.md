---
title: enlaces de funciones de HTTP y webhook aaaAzure | Documentos de Microsoft
description: "Comprender cómo toouse HTTP y webhook desencadenadores y los enlaces de funciones de Azure."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor, HTTP, API, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a>Enlaces HTTP y webhook en funciones de Azure
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Este artículo explica cómo se desencadena tooconfigure y trabajar con HTTP y los enlaces de funciones de Azure.
Con esto, puede usar las funciones de Azure toobuild sin servidor API y responden toowebhooks.

Las funciones de Azure proporciona Hola siguientes enlaces:
- Un [desencadenador HTTP](#httptrigger) permite invocar una función con una solicitud HTTP. Esto puede ser demasiado personalizada toorespond[webhooks](#hooktrigger).
- Un [enlace de salida HTTP](#output) permite toorespond toohello solicitud.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>Desencadenador HTTP
desencadenador de Hello HTTP ejecutará la función en la solicitud HTTP de respuesta tooan. Puede personalizarlo toorespond tooa dirección URL en particular o un conjunto de métodos HTTP. Un desencadenador HTTP también puede ser toowebhooks toorespond configurado. 

Si usa el portal de funciones de hello, puede también empezará a inmediatamente mediante una plantilla definida previamente. Seleccione **nueva función** y elegir "API & Webhooks" hello **escenario** lista desplegable. Seleccione una de las plantillas de Hola y haga clic en **crear**.

De forma predeterminada, un desencadenador HTTP responderá toohello solicitud con un código de estado HTTP 200 OK y un cuerpo vacío. toomodify Hola respuesta, configure un [HTTP el enlace de salida](#output)

### <a name="configuring-an-http-trigger"></a>Configuración de un desencadenador HTTP
Se define un desencadenador HTTP mediante la inclusión de un toohello similar del objeto JSON siguiente en hello `bindings` matriz de function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
enlace de Hello admite Hola propiedades siguientes:

* **nombre** : requerida: nombre de variable de saludo utilizado en código de la función para la solicitud de Hola o cuerpo de la solicitud. Consulte [Trabajar con un desencadenador HTTP desde código](#httptriggerusage).
* **tipo de** : requerida: debe estar configurado demasiado "httpTrigger".
* **dirección** : requerida: debe ser establecido demasiado "in".
* _authLevel_ : Esto determina qué claves, si existe, necesitan toobe presente en la solicitud de hello en función de orden tooinvoke Hola. Consulte [Trabajar con claves](#keys) a continuación. valor de Hello puede ser uno de hello siguientes:
    * _anonymous_: no se requiere ninguna clave de API.
    * _function_: se requiere una clave de API específica de la función. Esto es el valor predeterminado de hello si no se proporciona ninguno.
    * _administración_ : Hola master clave es obligatoria.
* **métodos** : se trata de una matriz de los métodos de hello HTTP responderá la función de hello toowhich. Si no se especifica, la función hello responderá métodos tooall HTTP. Vea [personalizar el punto de conexión de hello HTTP](#url).
* **ruta** : Esto define la plantilla de ruta de hello, controlar toowhich responderá la función de las direcciones URL de solicitud. Hello valor predeterminado si no se proporciona ninguno es `<functionname>`. Vea [personalizar el punto de conexión de hello HTTP](#url).
* **webHookType** : Esto configura Hola HTTP desencadenador tooact como un destinatario de webhook para el proveedor especificado Hola. Hola _métodos_ propiedad no debe establecerse si esto se elige. Vea [toowebhooks responde](#hooktrigger). valor de Hello puede ser uno de hello siguientes:
    * _genericJson_: un punto de conexión de webhook de uso general sin lógica para un proveedor concreto.
    * _github_ : función hello responderá tooGitHub webhook. Hola _authLevel_ propiedad no debe establecerse si esto se elige.
    * _demora_ : función hello responderá tooSlack webhook. Hola _authLevel_ propiedad no debe establecerse si esto se elige.

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>Trabajar con un desencadenador HTTP desde código
Para las funciones de C# y F #, puede declarar tipo hello de su toobe de entrada de desencadenador ya sea `HttpRequestMessage` o un tipo personalizado. Si elige `HttpRequestMessage`, a continuación, obtendrá el objeto de solicitud de acceso completo toohello. Para un tipo personalizado (por ejemplo, un POCO), funciones intentarán tooparse cuerpo de la solicitud de hello como propiedades del objeto JSON toopopulate Hola.

Para las funciones de Node.js, en tiempo de ejecución de funciones de hello proporciona cuerpo de la solicitud de hello en lugar del objeto de solicitud de saludo.

Consulte [Ejemplos de desencadenador HTTP](#httptriggersample) para ver ejemplos de uso.


<a name="output"></a>
## <a name="http-response-output-binding"></a>Enlace de salida de respuesta HTTP
Utilice Hola HTTP salida enlace toorespond toohello HTTP remitente de la solicitud. Este enlace requiere un desencadenador HTTP y permite la respuesta de hello toocustomize asociado a la solicitud del desencadenador Hola. Si no se proporciona el enlace de salida HTTP, un desencadenador HTTP devolverá HTTP 200 OK con un cuerpo vacío. 

### <a name="configuring-an-http-output-binding"></a>Configuración de un enlace de salida HTTP
Hola HTTP de salida enlace se define mediante la inclusión de un toohello similar del objeto JSON siguiente en hello `bindings` matriz de function.json:

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
enlace de Hello contiene Hola propiedades siguientes:

* **nombre** : requerida: Hola nombre de variable utilizada en el código de función para hello respuesta. Consulte [Trabajar con un enlace de salida HTTP desde código](#outputusage).
* **tipo de** : requerida: debe estar configurado demasiado "http".
* **dirección** : requerida: debe ser establecido demasiado "out".

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>Trabajar con un enlace de salida HTTP desde código
Puede usar Hola salida parámetro (p. ej., "res") toorespond toohello http o webhook autor de la llamada. Como alternativa, puede usar el estándar de `Request.CreateResponse()` (C#) o `context.res` (Node.JS) patrón tooreturn su respuesta. Para obtener ejemplos sobre cómo toouse Hola último método, consulte [ejemplos de desencadenador HTTP](#httptriggersample) y [ejemplos de desencadenador de Webhook](#hooktriggersample).


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a>Responde toowebhooks
Un desencadenador HTTP con hello _webHookType_ propiedad será demasiado configurado toorespond[webhooks](https://en.wikipedia.org/wiki/Webhook). configuración básica de Hello usa la configuración de "genericJson" Hola. Esto restringe las solicitudes tooonly aquellas que usan HTTP POST y con hello `application/json` tipo de contenido.

Hello desencadenador se puede adaptar tooa webhook específico proveedor (p. ej., [GitHub](https://developer.github.com/webhooks/) y [Slack](https://api.slack.com/outgoing-webhooks)). Si se especifica un proveedor, en tiempo de ejecución de funciones de hello puede ocuparse de lógica de validación del proveedor de Hola para usted.  

### <a name="configuring-github-as-a-webhook-provider"></a>Configuración de GitHub como proveedor de webhook
toorespond tooGitHub webhooks, primero cree la función con un desencadenador de HTTP y establezca hello _webHookType_ propiedad demasiado "github". A continuación, copie su [dirección URL](#url) y [la clave de API](#keys) en la página **Agregar Webhook** del repositorio de GitHub. Consulte la documentación [Creación de Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) de GitHub para más información.

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>Configuración de Slack como un proveedor de webhooks
Hola demora webhook genera un token en lugar de lo que le permite especificar, por lo que debe configurar una clave específica de la función con token de hello demora. Consulte [Trabajar con claves](#keys).

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a>Personalización de extremo HTTP de Hola
De forma predeterminada cuando se crea una función para un desencadenador HTTP, o un WebHook, función hello es direccionable con una ruta de formulario de hello:

    http://<yourapp>.azurewebsites.net/api/<funcname> 

Puede personalizar esta ruta mediante Hola opcional `route` enlace de entrada de propiedad en el desencadenador de hello HTTP. Por ejemplo, Hola después *function.json* archivo define un `route` propiedad de un desencadenador HTTP:

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

Con esta configuración, función hello es ahora direccionable con hello siguiendo la ruta en lugar de la ruta original de Hola.

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

Esto permite al código de la función hello toosupport dos parámetros en la dirección de hello, "categoría" e "id". Puede usar cualquier [restricción de ruta de API web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) con sus parámetros. Hola después el código de la función de C# hace uso de ambos parámetros.

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

Aquí es Hola de toouse de código de función de Node.js mismo parámetros de ruta.

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

De forma predeterminada, todas las rutas de la función tienen el prefijo *api*. También puede personalizar o quitar prefijo hello mediante hello `http.routePrefix` propiedad en su *host.json* archivo. Hello en el ejemplo siguiente se quita hello *api* prefijo de ruta mediante el uso de una cadena vacía para el prefijo de Hola Hola *host.json* archivo.

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

Para obtener información detallada sobre cómo hello tooupdate *host.json* archivo para la función, vea [forma en que tooupdate funcionan los archivos de la aplicación](functions-reference.md#fileupdate). 

Para obtener información sobre otras propiedades que puede configurar en el archivo *host.json*, consulte la [referencia de host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).


<a name="keys"></a>
## <a name="working-with-keys"></a>Trabajar con claves
HttpTriggers puede hacer uso de claves para aumentar la seguridad. Un estándar HttpTrigger puede utilizar como una clave de API, que requieren hello toobe clave presente en la solicitud de Hola. Webhooks puede usar claves tooauthorize solicitudes de varias maneras, dependiendo de qué proveedor de hello es compatible con.

Las claves se almacenan como parte de la aplicación de función en Azure y se cifran en reposo. tooview sus claves, crear nuevos o toonew valores de claves de consolidación, desplácese tooone de las funciones en el portal de Hola y seleccione "Administrar". 

Existen dos tipos de claves:
- **Claves de host**: estas claves se comparten entre todas las funciones de aplicación de la función de hello. Cuando se utiliza como una clave de API, permiten acceso tooany función dentro de la aplicación de la función de hello.
- **Las teclas de función**: estas claves aplican solo toohello funciones específicas en las que se definen. Cuando se utiliza como una clave de API, estos solo permite acceso toothat función.

Cada clave con el nombre de referencia y no hay una clave predeterminada (denominada "default") en el nivel de función y el host de Hola. Hola **clave maestra** es una clave de host predeterminado denominada "_master" que se define para cada aplicación de función y no se puede revocar. Proporciona acceso administrativo toohello runtime API. Usar `"authLevel": "admin"` Hola enlace JSON requerirá esta clave toobe presentada cuando se solicite Hola; cualquier otra clave se producirá un error de autorización.

> [!NOTE]
> Due toohello elevados permisos concedidos por la clave maestra de hello, no debe compartir esta clave con terceras partes o distribuirla en aplicaciones cliente nativas. Tenga cuidado al elegir el nivel de administrador de autorización de Hola.
> 
> 

### <a name="api-key-authorization"></a>Autorización de la clave de API
De forma predeterminada, un HttpTrigger requiere una clave de API de solicitud HTTP de Hola. Por lo tanto, su solicitud HTTP normalmente se verá así:

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

clave de Hello puede incluirse en una variable de cadena de consulta denominada `code`, como el anterior, o puede incluirse en un `x-functions-key` encabezado HTTP. valor de Hola de clave de hello puede ser cualquier tecla de función definido para la función de Hola o cualquier clave de host.

Puede elegir solicitudes tooallow sin claves o especificar esa clave maestra de Hola se debe utilizar cambiando hello `authLevel` propiedad Hola enlace JSON (vea [desencadenador HTTP](#httptrigger)).

### <a name="keys-and-webhooks"></a>Claves y webhooks
Autorización de Webhook se controla mediante el componente de hello webhook el destinatario, parte del mecanismo de Hola y de saludo HttpTrigger varía en función de tipo de webhook Hola. Sin embargo, cada mecanismo se basa en una clave. De forma predeterminada, se usará la tecla de función hello denominado "default". Si desea toouse una clave diferente, necesitará tooconfigure hello webhook proveedor toosend Hola clave nombre con solicitud de hello en uno de hello siguientes maneras:

- **Cadena de consulta**: proveedor de hello pasa el nombre de clave de Hola Hola `clientid` parámetro de cadena de consulta (por ejemplo, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).
- **Encabezado de solicitud**: proveedor de hello pasa el nombre de clave de Hola Hola `x-functions-clientid` encabezado.

> [!NOTE]
> Las claves de función tienen prioridad sobre las claves de host. Si se definen dos claves con el mismo nombre, hello de Hola se usará la tecla de función.
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>Ejemplos de desencadenador HTTP
Suponga que tiene Hola después de desencadenador HTTP en hello `bindings` matriz de function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

Vea ejemplo de Hola a específicos del idioma que busca un `name` parámetro en cadena de consulta de Hola o cuerpo de saludo de solicitud de hello HTTP.

* [C#](#httptriggercsharp)
* [F#](#httptriggerfsharp)
* [Node.js](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a>Ejemplo de desencadenador HTTP en C# #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

También puede enlazar tooa POCO en lugar de `HttpRequestMessage`. Esto se hidrate de cuerpo de saludo de solicitud de hello, analizado como JSON. De forma similar, puede pasar un tipo de salida de respuesta HTTP toohello enlace, y esto se devolverán como cuerpo de respuesta de hello, con un código de 200 estado.
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a>Ejemplo de desencadenador HTTP en F# #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

Necesita un `project.json` archivo que usa NuGet tooreference hello `FSharp.Interop.Dynamic` y `Dynamitey` ensamblados, similar al siguiente:

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

Se usarán NuGet toofetch las dependencias y se hará referencia a ellos en el script.

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Ejemplo de desencadenador HTTP en Node.js
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a>Ejemplos de webhook
Suponga que tiene Hola siguiendo el desencadenador de webhook Hola `bindings` matriz de function.json:

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

Vea el ejemplo específico del idioma de Hola que registra los comentarios del problema de GitHub.

* [C#](#hooktriggercsharp)
* [F#](#hooktriggerfsharp)
* [Node.js](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a>Ejemplo de webhook en C# #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a>Ejemplo de webhook en F# #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a>Ejemplo de webhook en Node.js
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

