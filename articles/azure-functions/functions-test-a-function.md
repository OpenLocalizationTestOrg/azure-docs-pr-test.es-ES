---
title: aaaTesting funciones de Azure | Documentos de Microsoft
description: Pruebe las funciones de Azure con Postman, cURL y Node.js.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "funciones de Azure, funciones, procesamiento de eventos, webhooks, proceso dinámico, arquitectura sin servidor"
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/02/2017
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a084f8dbc8089356c3c19d789dc9098f2bb63052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a>Estrategias para probar el código en Azure Functions

Este tema muestra hello aproxima para distintas funciones de tootest maneras, incluido el uso de hello después general:

+ Herramientas basadas en HTTP, como cURL, Postman e incluso un explorador web para los desencadenadores basados en web
+ Explorador de almacenamiento de Azure, los desencadenadores basados en el almacenamiento de Azure de tootest
+ Ficha de prueba en el portal de Azure funciones hello
+ Función desencadenada por un temporizador
+ Comprobación de la aplicación o del marco

Todos estos métodos de prueba usan una función de desencadenador HTTP que acepta datos proporcionados a través de un cuerpo de solicitud de Hola o de parámetro de cadena de consulta. Crear esta función en la primera sección de Hola.

## <a name="create-a-function-for-testing"></a>Creación de una función para realizar pruebas
La mayor parte de este tutorial, usamos una versión ligeramente modificada de hello HttpTrigger JavaScript plantilla de función que está disponible cuando se crea una función. Si necesita ayuda para crear una función, revise este [tutorial](functions-create-first-azure-function.md). Elija hello **HttpTrigger - JavaScript** plantilla al crear la función de prueba de hello en hello [portal de Azure].

Hello función plantilla predeterminada es básicamente una función de "Hola a todos" que devuelve el nombre de back-Hola de hello solicitud cuerpo o consulta de parámetro de cadena, `name=<your name>`.  Actualizaremos código de hello tooalso permitir tooprovide Hola nombre y una dirección como contenido JSON en el cuerpo de la solicitud de saludo. A continuación, función hello repetir a estos cliente toohello atrás si está disponible.   

Actualizar función hello con hello después de código, que se usará para las pruebas:

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "hello address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults too200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a>Prueba de una función con herramientas
Fuera de hello portal de Azure, existen diversas herramientas que puede usar las funciones tootrigger para las pruebas. Entre estas se incluyen las herramientas de prueba de HTTP, tanto las basadas en interfaz de usuario como en la línea de comandos, las herramientas de acceso de Azure Storage e incluso un simple explorador web.

### <a name="test-with-a-browser"></a>Prueba con un explorador
Explorador de web de Hello es un funciones tootrigger de manera sencilla a través de HTTP. Puede utilizar un explorador para las solicitudes GET que no requieran una carga del cuerpo y que usen solo los parámetros de la cadena de consulta.

función de hello tootest anteriormente, definimos Hola copia **dirección Url de la función** desde el portal de Hola. Tiene Hola siguiente forma:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Anexar hello `name` la cadena de consulta de toohello de parámetros. Usar un nombre real para hello `<Enter a name here>` marcador de posición.

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

Pegar Hola URL en el explorador y debe obtener un siguiente toohello similar de respuesta.

![Captura de pantalla de la pestaña del explorador Chrome con respuesta de prueba](./media/functions-test-a-function/browser-test.png)

En este ejemplo es el Explorador de Chrome hello, que encapsula Hola devuelve la cadena en XML. Otros exploradores mostrar solamente el valor de cadena Hola.

En el portal de hello **registros** similar siguiente toohello se registra en la ejecución de la función hello de salida de ventana,:

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a>Prueba con Postman
Hola recomendada herramienta tootest la mayoría de las funciones es Postman, que se integra con el Explorador de Chrome Hola. tooinstall Postman, consulte [obtener Postman](https://www.getpostman.com/). Postman proporciona control sobre muchos más atributos de una solicitud HTTP.

> [!TIP]
> Utilice Hola HTTP herramienta de prueba que sienta más cómodo. Estos son algunos tooPostman alternativas:  
>
> * [Fiddler](http://www.telerik.com/fiddler)  
> * [Paw](https://luckymarmot.com/paw)  
>
>

función de hello tootest con un cuerpo de solicitud en Postman:

1. Iniciar Postman desde hello **aplicaciones** botón en la esquina superior izquierda de Hola de una ventana del explorador Chrome.
2. Copie la **dirección URL de la función** y péguela en Postman. Incluye el parámetro de cadena de consulta de código de acceso de Hola.
3. Cambiar método hello HTTP demasiado**POST**.
4. Haga clic en **cuerpo** > **sin formato**y agregue la siguiente toohello similar de cuerpo de solicitud JSON:

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. Haga clic en **Enviar**.

Hello siguiente imagen muestra ejemplo de la función de eco simple de hello pruebas en este tutorial.

![Captura de pantalla de la interfaz de usuario de Postman](./media/functions-test-a-function/postman-test.png)

En el portal de hello **registros** similar siguiente toohello se registra en la ejecución de la función hello de salida de ventana,:

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a>Probar con cURL desde línea de comandos de Hola
A menudo, cuando se está probando el software, no es necesario toolook cualquier más allá de Hola depuración toohelp de línea de comandos de la aplicación. No varía con respecto a la prueba de funciones. Tenga en cuenta que cURL Hola está disponible de forma predeterminada en los sistemas basados en Linux. En Windows, primero debe descargar e instalar hello [cURL herramienta](https://curl.haxx.se/).

función de hello tootest que se definió anteriormente, Hola copia **dirección URL de la función** desde el portal de Hola. Tiene Hola siguiente forma:

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Esta es la dirección de URL de hello para la activación de la función. Pruebe esto con el comando cURL de hello en toomake de línea de comandos de hello una operación GET (`-G` o `--get`) solicitud en función de hello:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

Este ejemplo concreto requiere un parámetro de cadena de consulta, que puede pasarse como datos (`-d`) en hello cURL comando:

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

Comando de ejecución hello y verá Hola siguiendo la salida de función hello en línea de comandos de hello:

![Captura de pantalla de la salida del símbolo del sistema del comando](./media/functions-test-a-function/curl-test.png)

En el portal de hello **registros** similar siguiente toohello se registra en la ejecución de la función hello de salida de ventana,:

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a>Prueba de un desencadenador de blob mediante el Explorador de almacenamiento
Puede probar una función de desencadenador de blob mediante el [Explorador de Azure Storage](http://storageexplorer.com/).

1. Hola [portal de Azure] para la aplicación de la función, cree una función de desencadenador de blob de C#, F # o JavaScript. Establecer nombre de toohello toomonitor Hola de ruta de acceso de su contenedor de blobs. Por ejemplo:

        files
2. Haga clic en hello  **+**  botón tooselect o crear cuenta de almacenamiento de hello desea toouse. A continuación, haga clic en **Crear**.
3. Crear un archivo de texto con hello después de texto y guárdelo:

        A text file for blob trigger function testing.
4. Ejecutar [Azure Storage Explorer](http://storageexplorer.com/)y conecte el contenedor de blobs de toohello en la cuenta de almacenamiento de Hola que se está supervisando.
5. Haga clic en **cargar** archivo de texto hello tooupload.

    ![Captura de pantalla del Explorador de almacenamiento](./media/functions-test-a-function/azure-storage-explorer-test.png)

Hola predeterminado blob desencadenador función código informa de procesamiento de Hola de blob de hello en los registros de hello:

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a>Prueba de una función dentro de funciones
Hello las funciones de Azure portal está diseñada toolet probar HTTP y temporizador desencadena funciones. También puede crear funciones tootrigger otras funciones que se están probando.

### <a name="test-with-hello-functions-portal-run-button"></a>Probar con el botón de ejecución de portal de hello funciones
Hola portal proporciona un **ejecutar** limitado de botón que se puede usar toodo algunas pruebas. Puede proporcionar un cuerpo de solicitud mediante el botón de hello, pero no puede proporcionar parámetros de cadena de consulta o actualización de encabezados de solicitud.

Probar función de desencadenador de hello HTTP hemos creado con anterioridad mediante la adición de un toohello similar de cadena JSON siguiente en hello **cuerpo de la solicitud** campo. A continuación, haga clic en hello **ejecutar** botón.

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

En el portal de hello **registros** similar siguiente toohello se registra en la ejecución de la función hello de salida de ventana,:

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a>Prueba con un desencadenador de temporizador
Algunas funciones no se pueden probar adecuadamente con herramientas de hello mencionadas anteriormente. Por ejemplo, considere una función de desencadenador de cola que se ejecuta cuando se coloca un mensaje en [Azure Queue Storage](../storage/queues/storage-dotnet-how-to-use-queues.md). Siempre se puede escribir código toodrop un mensaje en la cola y se proporciona un ejemplo de esto en un proyecto de consola más adelante en este artículo. Sin embargo, hay otro método que sirve para probar las funciones directamente.  

Puede usar un desencadenador de temporizador configurado con un enlace de salida de cola. Ese código de desencadenador de temporizador, a continuación, puede escribir la cola de toohello de mensajes de prueba de Hola. Esta sección lo guía a través de un ejemplo.

Para obtener información más detallada sobre el uso de enlaces con funciones de Azure, vea hello [material de referencia de funciones de Azure](functions-reference.md).

#### <a name="create-a-queue-trigger-for-testing"></a>Creación de un desencadenador de cola para las pruebas
toodemonstrate este enfoque, primero creamos una función de activación de cola que queremos tootest para una cola denominada `queue-newusers`. Esta función procesa la información de nombre y dirección que se coloca en Queue Storage para un nuevo usuario.

> [!NOTE]
> Si utiliza un nombre de cola diferente, asegurarse de nombre de Hola que utiliza ajusta toohello [asignar nombres a colas y metadatos](https://msdn.microsoft.com/library/dd179349.aspx) reglas. De lo contrario, obtiene un error.
>
>

1. Hola [portal de Azure] para la aplicación de la función, haga clic en **nueva función** > **QueueTrigger - C#**.
2. Escriba toobe de nombre de cola de hello supervisado por la función de la cola de hello:

        queue-newusers
3. Haga clic en hello  **+**  botón tooselect o crear cuenta de almacenamiento de hello desea toouse. A continuación, haga clic en **Crear**.
4. Deje esta ventana del explorador portal abierto, para que pueda supervisar entradas del registro de hello para el código de plantilla de función de cola de Hola de forma predeterminada.

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a>Crear un toodrop de desencadenador de temporizador en un mensaje en cola Hola
1. Abra hello [portal de Azure] en una nueva ventana del explorador y navegar por la aplicación de la función de tooyour.
2. Haga clic en **Nueva función** > **TimerTrigger: - C#**. Escriba un tooset de expresión cron con qué frecuencia hello temporizador código de prueba la función de la cola. A continuación, haga clic en **Crear**. Si desea Hola prueba toorun cada 30 segundos, puede utilizar Hola siguiente [expresión CRON](https://wikipedia.org/wiki/Cron#CRON_expression):

        */30 * * * * *
3. Haga clic en hello **integrar** ficha para el nuevo desencadenador de temporizador.
4. En **Salida**, haga clic en **+ Nueva salida**. Después, haga clic en **Cola** y en **Seleccionar**.
5. Nombre de Hola de tenga en cuenta que utilice para hello **objeto de mensaje de cola**. Se usa en el código de función de temporizador de Hola.

        myQueue
6. Escriba el nombre de la cola de Hola donde se envía el mensaje de bienvenida:

        queue-newusers
7. Haga clic en hello  **+**  botón cuenta de almacenamiento de hello tooselect usado anteriormente con el desencadenador de la cola de Hola. A continuación, haga clic en **Guardar**.
8. Haga clic en hello **desarrollar** pestaña para el desencadenador de temporizador.
9. Puede usar Hola después el código de función de temporizador de hello C#, siempre y cuando usa Hola mismo nombre de objeto de mensaje mostrado anteriormente de cola. A continuación, haga clic en **Guardar**.

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

En este momento, Hola función de temporizador de C# ejecuta cada 30 segundos si ha usado la expresión cron de ejemplo de Hola. registros de Hello para la función de temporizador de hello cada ejecución del informe:

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

En la ventana del explorador de hello para la función de la cola de hello, puede ver cada mensaje que se está procesando:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a>Prueba de una función con código
Puede que necesite toocreate un tootest externo de la aplicación o marco sus funciones.

### <a name="test-an-http-trigger-function-with-code-nodejs"></a>Prueba de una función de desencadenador HTTP con código: Node.js
Puede usar un tooexecute de aplicación Node.js un tootest de solicitud HTTP de la función.
Asegúrese de tooset seguro:

* Hola `host` en host de aplicación de funciones de tooyour opciones de solicitud de Hola.
* El nombre de función en hello `path`.
* El código de acceso (`<your code>`) en hello `path`.

Ejemplo de código:

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


Salida:

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

En el portal de hello **registros** similar siguiente toohello se registra en la ejecución de la función hello de salida de ventana,:

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a>Prueba de una función de desencadenador de cola con código: C# #
Se ha mencionado anteriormente que puede probar un desencadenador de la cola mediante código toodrop un mensaje en la cola. Hola siguiendo el ejemplo de código se basa en código de hello C# presentado en hello [Introducción al almacenamiento de colas de Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial. También se ofrece código para otros lenguajes en ese vínculo.

tootest este código en una aplicación de consola, debe:

* [Configurar la cadena de conexión de almacenamiento en archivo app.config de hello](../storage/queues/storage-dotnet-how-to-use-queues.md).
* Pasar un `name` y `address` como aplicación de toohello de parámetros. Por ejemplo: `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`. (Este código acepta Hola nombre y una dirección para un nuevo usuario como argumentos de línea de comandos en tiempo de ejecución.)

Ejemplo de código C#:

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create hello queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference tooa queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create hello queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it toohello queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message too" + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

En la ventana del explorador de hello para la función de la cola de hello, puede ver cada mensaje que se está procesando:

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portal de Azure]: https://portal.azure.com
