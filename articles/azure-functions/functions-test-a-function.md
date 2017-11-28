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
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="d9be5-104">Estrategias para probar el código en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d9be5-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="d9be5-105">Este tema muestra hello aproxima para distintas funciones de tootest maneras, incluido el uso de hello después general:</span><span class="sxs-lookup"><span data-stu-id="d9be5-105">This topic demonstrates hello various ways tootest functions, including using hello following general approaches:</span></span>

+ <span data-ttu-id="d9be5-106">Herramientas basadas en HTTP, como cURL, Postman e incluso un explorador web para los desencadenadores basados en web</span><span class="sxs-lookup"><span data-stu-id="d9be5-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="d9be5-107">Explorador de almacenamiento de Azure, los desencadenadores basados en el almacenamiento de Azure de tootest</span><span class="sxs-lookup"><span data-stu-id="d9be5-107">Azure Storage Explorer, tootest Azure Storage-based triggers</span></span>
+ <span data-ttu-id="d9be5-108">Ficha de prueba en el portal de Azure funciones hello</span><span class="sxs-lookup"><span data-stu-id="d9be5-108">Test tab in hello Azure Functions portal</span></span>
+ <span data-ttu-id="d9be5-109">Función desencadenada por un temporizador</span><span class="sxs-lookup"><span data-stu-id="d9be5-109">Timer-triggered function</span></span>
+ <span data-ttu-id="d9be5-110">Comprobación de la aplicación o del marco</span><span class="sxs-lookup"><span data-stu-id="d9be5-110">Testing application or framework</span></span>

<span data-ttu-id="d9be5-111">Todos estos métodos de prueba usan una función de desencadenador HTTP que acepta datos proporcionados a través de un cuerpo de solicitud de Hola o de parámetro de cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="d9be5-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or hello request body.</span></span> <span data-ttu-id="d9be5-112">Crear esta función en la primera sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-112">You create this function in hello first section.</span></span>

## <a name="create-a-function-for-testing"></a><span data-ttu-id="d9be5-113">Creación de una función para realizar pruebas</span><span class="sxs-lookup"><span data-stu-id="d9be5-113">Create a function for testing</span></span>
<span data-ttu-id="d9be5-114">La mayor parte de este tutorial, usamos una versión ligeramente modificada de hello HttpTrigger JavaScript plantilla de función que está disponible cuando se crea una función.</span><span class="sxs-lookup"><span data-stu-id="d9be5-114">For most of this tutorial, we use a slightly modified version of hello HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="d9be5-115">Si necesita ayuda para crear una función, revise este [tutorial](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="d9be5-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="d9be5-116">Elija hello **HttpTrigger - JavaScript** plantilla al crear la función de prueba de hello en hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="d9be5-116">Choose hello **HttpTrigger- JavaScript** template when creating hello test function in hello [Azure portal].</span></span>

<span data-ttu-id="d9be5-117">Hello función plantilla predeterminada es básicamente una función de "Hola a todos" que devuelve el nombre de back-Hola de hello solicitud cuerpo o consulta de parámetro de cadena, `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="d9be5-117">hello default function template is basically a "hello world" function that echoes back hello name from hello request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="d9be5-118">Actualizaremos código de hello tooalso permitir tooprovide Hola nombre y una dirección como contenido JSON en el cuerpo de la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="d9be5-118">We'll update hello code tooalso allow you tooprovide hello name and an address as JSON content in hello request body.</span></span> <span data-ttu-id="d9be5-119">A continuación, función hello repetir a estos cliente toohello atrás si está disponible.</span><span class="sxs-lookup"><span data-stu-id="d9be5-119">Then hello function echoes these back toohello client when available.</span></span>   

<span data-ttu-id="d9be5-120">Actualizar función hello con hello después de código, que se usará para las pruebas:</span><span class="sxs-lookup"><span data-stu-id="d9be5-120">Update hello function with hello following code, which we will use for testing:</span></span>

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

## <a name="test-a-function-with-tools"></a><span data-ttu-id="d9be5-121">Prueba de una función con herramientas</span><span class="sxs-lookup"><span data-stu-id="d9be5-121">Test a function with tools</span></span>
<span data-ttu-id="d9be5-122">Fuera de hello portal de Azure, existen diversas herramientas que puede usar las funciones tootrigger para las pruebas.</span><span class="sxs-lookup"><span data-stu-id="d9be5-122">Outside hello Azure portal, there are various tools that you can use tootrigger your functions for testing.</span></span> <span data-ttu-id="d9be5-123">Entre estas se incluyen las herramientas de prueba de HTTP, tanto las basadas en interfaz de usuario como en la línea de comandos, las herramientas de acceso de Azure Storage e incluso un simple explorador web.</span><span class="sxs-lookup"><span data-stu-id="d9be5-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="d9be5-124">Prueba con un explorador</span><span class="sxs-lookup"><span data-stu-id="d9be5-124">Test with a browser</span></span>
<span data-ttu-id="d9be5-125">Explorador de web de Hello es un funciones tootrigger de manera sencilla a través de HTTP.</span><span class="sxs-lookup"><span data-stu-id="d9be5-125">hello web browser is a simple way tootrigger functions via HTTP.</span></span> <span data-ttu-id="d9be5-126">Puede utilizar un explorador para las solicitudes GET que no requieran una carga del cuerpo y que usen solo los parámetros de la cadena de consulta.</span><span class="sxs-lookup"><span data-stu-id="d9be5-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="d9be5-127">función de hello tootest anteriormente, definimos Hola copia **dirección Url de la función** desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-127">tootest hello function we defined earlier, copy hello **Function Url** from hello portal.</span></span> <span data-ttu-id="d9be5-128">Tiene Hola siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="d9be5-128">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="d9be5-129">Anexar hello `name` la cadena de consulta de toohello de parámetros.</span><span class="sxs-lookup"><span data-stu-id="d9be5-129">Append hello `name` parameter toohello query string.</span></span> <span data-ttu-id="d9be5-130">Usar un nombre real para hello `<Enter a name here>` marcador de posición.</span><span class="sxs-lookup"><span data-stu-id="d9be5-130">Use an actual name for hello `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="d9be5-131">Pegar Hola URL en el explorador y debe obtener un siguiente toohello similar de respuesta.</span><span class="sxs-lookup"><span data-stu-id="d9be5-131">Paste hello URL into your browser, and you should get a response similar toohello following.</span></span>

![Captura de pantalla de la pestaña del explorador Chrome con respuesta de prueba](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="d9be5-133">En este ejemplo es el Explorador de Chrome hello, que encapsula Hola devuelve la cadena en XML.</span><span class="sxs-lookup"><span data-stu-id="d9be5-133">This example is hello Chrome browser, which wraps hello returned string in XML.</span></span> <span data-ttu-id="d9be5-134">Otros exploradores mostrar solamente el valor de cadena Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-134">Other browsers display just hello string value.</span></span>

<span data-ttu-id="d9be5-135">En el portal de hello **registros** similar siguiente toohello se registra en la ejecución de la función hello de salida de ventana,:</span><span class="sxs-lookup"><span data-stu-id="d9be5-135">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected toolog-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="d9be5-136">Prueba con Postman</span><span class="sxs-lookup"><span data-stu-id="d9be5-136">Test with Postman</span></span>
<span data-ttu-id="d9be5-137">Hola recomendada herramienta tootest la mayoría de las funciones es Postman, que se integra con el Explorador de Chrome Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-137">hello recommended tool tootest most of your functions is Postman, which integrates with hello Chrome browser.</span></span> <span data-ttu-id="d9be5-138">tooinstall Postman, consulte [obtener Postman](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="d9be5-138">tooinstall Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="d9be5-139">Postman proporciona control sobre muchos más atributos de una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="d9be5-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="d9be5-140">Utilice Hola HTTP herramienta de prueba que sienta más cómodo.</span><span class="sxs-lookup"><span data-stu-id="d9be5-140">Use hello HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="d9be5-141">Estos son algunos tooPostman alternativas:</span><span class="sxs-lookup"><span data-stu-id="d9be5-141">Here are some alternatives tooPostman:</span></span>  
>
> * [<span data-ttu-id="d9be5-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="d9be5-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="d9be5-143">Paw</span><span class="sxs-lookup"><span data-stu-id="d9be5-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="d9be5-144">función de hello tootest con un cuerpo de solicitud en Postman:</span><span class="sxs-lookup"><span data-stu-id="d9be5-144">tootest hello function with a request body in Postman:</span></span>

1. <span data-ttu-id="d9be5-145">Iniciar Postman desde hello **aplicaciones** botón en la esquina superior izquierda de Hola de una ventana del explorador Chrome.</span><span class="sxs-lookup"><span data-stu-id="d9be5-145">Start Postman from hello **Apps** button in hello upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="d9be5-146">Copie la **dirección URL de la función** y péguela en Postman.</span><span class="sxs-lookup"><span data-stu-id="d9be5-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="d9be5-147">Incluye el parámetro de cadena de consulta de código de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-147">It includes hello access code query string parameter.</span></span>
3. <span data-ttu-id="d9be5-148">Cambiar método hello HTTP demasiado**POST**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-148">Change hello HTTP method too**POST**.</span></span>
4. <span data-ttu-id="d9be5-149">Haga clic en **cuerpo** > **sin formato**y agregue la siguiente toohello similar de cuerpo de solicitud JSON:</span><span class="sxs-lookup"><span data-stu-id="d9be5-149">Click **Body** > **raw**, and add a JSON request body similar toohello following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="d9be5-150">Haga clic en **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-150">Click **Send**.</span></span>

<span data-ttu-id="d9be5-151">Hello siguiente imagen muestra ejemplo de la función de eco simple de hello pruebas en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d9be5-151">hello following image shows testing hello simple echo function example in this tutorial.</span></span>

![Captura de pantalla de la interfaz de usuario de Postman](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="d9be5-153">En el portal de hello **registros** similar siguiente toohello se registra en la ejecución de la función hello de salida de ventana,:</span><span class="sxs-lookup"><span data-stu-id="d9be5-153">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-hello-command-line"></a><span data-ttu-id="d9be5-154">Probar con cURL desde línea de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="d9be5-154">Test with cURL from hello command line</span></span>
<span data-ttu-id="d9be5-155">A menudo, cuando se está probando el software, no es necesario toolook cualquier más allá de Hola depuración toohelp de línea de comandos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d9be5-155">Often when you're testing software, it's not necessary toolook any further than hello command line toohelp debug your application.</span></span> <span data-ttu-id="d9be5-156">No varía con respecto a la prueba de funciones.</span><span class="sxs-lookup"><span data-stu-id="d9be5-156">This is no different with testing functions.</span></span> <span data-ttu-id="d9be5-157">Tenga en cuenta que cURL Hola está disponible de forma predeterminada en los sistemas basados en Linux.</span><span class="sxs-lookup"><span data-stu-id="d9be5-157">Note that hello cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="d9be5-158">En Windows, primero debe descargar e instalar hello [cURL herramienta](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="d9be5-158">On Windows, you must first download and install hello [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="d9be5-159">función de hello tootest que se definió anteriormente, Hola copia **dirección URL de la función** desde el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-159">tootest hello function that we defined earlier, copy hello **Function URL** from hello portal.</span></span> <span data-ttu-id="d9be5-160">Tiene Hola siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="d9be5-160">It has hello following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="d9be5-161">Esta es la dirección de URL de hello para la activación de la función.</span><span class="sxs-lookup"><span data-stu-id="d9be5-161">This is hello URL for triggering your function.</span></span> <span data-ttu-id="d9be5-162">Pruebe esto con el comando cURL de hello en toomake de línea de comandos de hello una operación GET (`-G` o `--get`) solicitud en función de hello:</span><span class="sxs-lookup"><span data-stu-id="d9be5-162">Test this by using hello cURL command on hello command line toomake a GET (`-G` or `--get`) request against hello function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="d9be5-163">Este ejemplo concreto requiere un parámetro de cadena de consulta, que puede pasarse como datos (`-d`) en hello cURL comando:</span><span class="sxs-lookup"><span data-stu-id="d9be5-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in hello cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="d9be5-164">Comando de ejecución hello y verá Hola siguiendo la salida de función hello en línea de comandos de hello:</span><span class="sxs-lookup"><span data-stu-id="d9be5-164">Run hello command, and you see hello following output of hello function on hello command line:</span></span>

![Captura de pantalla de la salida del símbolo del sistema del comando](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="d9be5-166">En el portal de hello **registros** similar siguiente toohello se registra en la ejecución de la función hello de salida de ventana,:</span><span class="sxs-lookup"><span data-stu-id="d9be5-166">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected toolog-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="d9be5-167">Prueba de un desencadenador de blob mediante el Explorador de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="d9be5-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="d9be5-168">Puede probar una función de desencadenador de blob mediante el [Explorador de Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d9be5-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="d9be5-169">Hola [portal de Azure] para la aplicación de la función, cree una función de desencadenador de blob de C#, F # o JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d9be5-169">In hello [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="d9be5-170">Establecer nombre de toohello toomonitor Hola de ruta de acceso de su contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="d9be5-170">Set hello path toomonitor toohello name of your blob container.</span></span> <span data-ttu-id="d9be5-171">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d9be5-171">For example:</span></span>

        files
2. <span data-ttu-id="d9be5-172">Haga clic en hello  **+**  botón tooselect o crear cuenta de almacenamiento de hello desea toouse.</span><span class="sxs-lookup"><span data-stu-id="d9be5-172">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="d9be5-173">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-173">Then click **Create**.</span></span>
3. <span data-ttu-id="d9be5-174">Crear un archivo de texto con hello después de texto y guárdelo:</span><span class="sxs-lookup"><span data-stu-id="d9be5-174">Create a text file with hello following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="d9be5-175">Ejecutar [Azure Storage Explorer](http://storageexplorer.com/)y conecte el contenedor de blobs de toohello en la cuenta de almacenamiento de Hola que se está supervisando.</span><span class="sxs-lookup"><span data-stu-id="d9be5-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect toohello blob container in hello storage account being monitored.</span></span>
5. <span data-ttu-id="d9be5-176">Haga clic en **cargar** archivo de texto hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="d9be5-176">Click **Upload** tooupload hello text file.</span></span>

    ![Captura de pantalla del Explorador de almacenamiento](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="d9be5-178">Hola predeterminado blob desencadenador función código informa de procesamiento de Hola de blob de hello en los registros de hello:</span><span class="sxs-lookup"><span data-stu-id="d9be5-178">hello default blob trigger function code reports hello processing of hello blob in hello logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected toolog-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="d9be5-179">Prueba de una función dentro de funciones</span><span class="sxs-lookup"><span data-stu-id="d9be5-179">Test a function within functions</span></span>
<span data-ttu-id="d9be5-180">Hello las funciones de Azure portal está diseñada toolet probar HTTP y temporizador desencadena funciones.</span><span class="sxs-lookup"><span data-stu-id="d9be5-180">hello Azure Functions portal is designed toolet you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="d9be5-181">También puede crear funciones tootrigger otras funciones que se están probando.</span><span class="sxs-lookup"><span data-stu-id="d9be5-181">You can also create functions tootrigger other functions that you are testing.</span></span>

### <a name="test-with-hello-functions-portal-run-button"></a><span data-ttu-id="d9be5-182">Probar con el botón de ejecución de portal de hello funciones</span><span class="sxs-lookup"><span data-stu-id="d9be5-182">Test with hello Functions portal Run button</span></span>
<span data-ttu-id="d9be5-183">Hola portal proporciona un **ejecutar** limitado de botón que se puede usar toodo algunas pruebas.</span><span class="sxs-lookup"><span data-stu-id="d9be5-183">hello portal provides a **Run** button that you can use toodo some limited testing.</span></span> <span data-ttu-id="d9be5-184">Puede proporcionar un cuerpo de solicitud mediante el botón de hello, pero no puede proporcionar parámetros de cadena de consulta o actualización de encabezados de solicitud.</span><span class="sxs-lookup"><span data-stu-id="d9be5-184">You can provide a request body by using hello button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="d9be5-185">Probar función de desencadenador de hello HTTP hemos creado con anterioridad mediante la adición de un toohello similar de cadena JSON siguiente en hello **cuerpo de la solicitud** campo.</span><span class="sxs-lookup"><span data-stu-id="d9be5-185">Test hello HTTP trigger function we created earlier by adding a JSON string similar toohello following in hello **Request body** field.</span></span> <span data-ttu-id="d9be5-186">A continuación, haga clic en hello **ejecutar** botón.</span><span class="sxs-lookup"><span data-stu-id="d9be5-186">Then click hello **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="d9be5-187">En el portal de hello **registros** similar siguiente toohello se registra en la ejecución de la función hello de salida de ventana,:</span><span class="sxs-lookup"><span data-stu-id="d9be5-187">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="d9be5-188">Prueba con un desencadenador de temporizador</span><span class="sxs-lookup"><span data-stu-id="d9be5-188">Test with a timer trigger</span></span>
<span data-ttu-id="d9be5-189">Algunas funciones no se pueden probar adecuadamente con herramientas de hello mencionadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d9be5-189">Some functions can't be adequately tested with hello tools mentioned previously.</span></span> <span data-ttu-id="d9be5-190">Por ejemplo, considere una función de desencadenador de cola que se ejecuta cuando se coloca un mensaje en [Azure Queue Storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="d9be5-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="d9be5-191">Siempre se puede escribir código toodrop un mensaje en la cola y se proporciona un ejemplo de esto en un proyecto de consola más adelante en este artículo.</span><span class="sxs-lookup"><span data-stu-id="d9be5-191">You can always write code toodrop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="d9be5-192">Sin embargo, hay otro método que sirve para probar las funciones directamente.</span><span class="sxs-lookup"><span data-stu-id="d9be5-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="d9be5-193">Puede usar un desencadenador de temporizador configurado con un enlace de salida de cola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="d9be5-194">Ese código de desencadenador de temporizador, a continuación, puede escribir la cola de toohello de mensajes de prueba de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-194">That timer trigger code can then write hello test messages toohello queue.</span></span> <span data-ttu-id="d9be5-195">Esta sección lo guía a través de un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d9be5-195">This section walks through an example.</span></span>

<span data-ttu-id="d9be5-196">Para obtener información más detallada sobre el uso de enlaces con funciones de Azure, vea hello [material de referencia de funciones de Azure](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d9be5-196">For more in-depth information on using bindings with Azure Functions, see hello [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="d9be5-197">Creación de un desencadenador de cola para las pruebas</span><span class="sxs-lookup"><span data-stu-id="d9be5-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="d9be5-198">toodemonstrate este enfoque, primero creamos una función de activación de cola que queremos tootest para una cola denominada `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="d9be5-198">toodemonstrate this approach, we first create a queue trigger function that we want tootest for a queue named `queue-newusers`.</span></span> <span data-ttu-id="d9be5-199">Esta función procesa la información de nombre y dirección que se coloca en Queue Storage para un nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="d9be5-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="d9be5-200">Si utiliza un nombre de cola diferente, asegurarse de nombre de Hola que utiliza ajusta toohello [asignar nombres a colas y metadatos](https://msdn.microsoft.com/library/dd179349.aspx) reglas.</span><span class="sxs-lookup"><span data-stu-id="d9be5-200">If you use a different queue name, make sure hello name you use conforms toohello [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="d9be5-201">De lo contrario, obtiene un error.</span><span class="sxs-lookup"><span data-stu-id="d9be5-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="d9be5-202">Hola [portal de Azure] para la aplicación de la función, haga clic en **nueva función** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-202">In hello [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="d9be5-203">Escriba toobe de nombre de cola de hello supervisado por la función de la cola de hello:</span><span class="sxs-lookup"><span data-stu-id="d9be5-203">Enter hello queue name toobe monitored by hello queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="d9be5-204">Haga clic en hello  **+**  botón tooselect o crear cuenta de almacenamiento de hello desea toouse.</span><span class="sxs-lookup"><span data-stu-id="d9be5-204">Click hello **+** button tooselect or create hello storage account you want toouse.</span></span> <span data-ttu-id="d9be5-205">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-205">Then click **Create**.</span></span>
4. <span data-ttu-id="d9be5-206">Deje esta ventana del explorador portal abierto, para que pueda supervisar entradas del registro de hello para el código de plantilla de función de cola de Hola de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="d9be5-206">Leave this portal browser window open, so you can monitor hello log entries for hello default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-toodrop-a-message-in-hello-queue"></a><span data-ttu-id="d9be5-207">Crear un toodrop de desencadenador de temporizador en un mensaje en cola Hola</span><span class="sxs-lookup"><span data-stu-id="d9be5-207">Create a timer trigger toodrop a message in hello queue</span></span>
1. <span data-ttu-id="d9be5-208">Abra hello [portal de Azure] en una nueva ventana del explorador y navegar por la aplicación de la función de tooyour.</span><span class="sxs-lookup"><span data-stu-id="d9be5-208">Open hello [Azure portal] in a new browser window, and navigate tooyour function app.</span></span>
2. <span data-ttu-id="d9be5-209">Haga clic en **Nueva función** > **TimerTrigger: - C#**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="d9be5-210">Escriba un tooset de expresión cron con qué frecuencia hello temporizador código de prueba la función de la cola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-210">Enter a cron expression tooset how often hello timer code tests your queue function.</span></span> <span data-ttu-id="d9be5-211">A continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-211">Then click **Create**.</span></span> <span data-ttu-id="d9be5-212">Si desea Hola prueba toorun cada 30 segundos, puede utilizar Hola siguiente [expresión CRON](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="d9be5-212">If you want hello test toorun every 30 seconds, you can use hello following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="d9be5-213">Haga clic en hello **integrar** ficha para el nuevo desencadenador de temporizador.</span><span class="sxs-lookup"><span data-stu-id="d9be5-213">Click hello **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="d9be5-214">En **Salida**, haga clic en **+ Nueva salida**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="d9be5-215">Después, haga clic en **Cola** y en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="d9be5-216">Nombre de Hola de tenga en cuenta que utilice para hello **objeto de mensaje de cola**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-216">Note hello name you use for hello **queue message object**.</span></span> <span data-ttu-id="d9be5-217">Se usa en el código de función de temporizador de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-217">You use this in hello timer function code.</span></span>

        myQueue
6. <span data-ttu-id="d9be5-218">Escriba el nombre de la cola de Hola donde se envía el mensaje de bienvenida:</span><span class="sxs-lookup"><span data-stu-id="d9be5-218">Enter hello queue name where hello message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="d9be5-219">Haga clic en hello  **+**  botón cuenta de almacenamiento de hello tooselect usado anteriormente con el desencadenador de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-219">Click hello **+** button tooselect hello storage account you used previously with hello queue trigger.</span></span> <span data-ttu-id="d9be5-220">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-220">Then click **Save**.</span></span>
8. <span data-ttu-id="d9be5-221">Haga clic en hello **desarrollar** pestaña para el desencadenador de temporizador.</span><span class="sxs-lookup"><span data-stu-id="d9be5-221">Click hello **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="d9be5-222">Puede usar Hola después el código de función de temporizador de hello C#, siempre y cuando usa Hola mismo nombre de objeto de mensaje mostrado anteriormente de cola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-222">You can use hello following code for hello C# timer function, as long as you used hello same queue message object name shown earlier.</span></span> <span data-ttu-id="d9be5-223">A continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="d9be5-223">Then click **Save**.</span></span>

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

<span data-ttu-id="d9be5-224">En este momento, Hola función de temporizador de C# ejecuta cada 30 segundos si ha usado la expresión cron de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-224">At this point, hello C# timer function executes every 30 seconds if you used hello example cron expression.</span></span> <span data-ttu-id="d9be5-225">registros de Hello para la función de temporizador de hello cada ejecución del informe:</span><span class="sxs-lookup"><span data-stu-id="d9be5-225">hello logs for hello timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="d9be5-226">En la ventana del explorador de hello para la función de la cola de hello, puede ver cada mensaje que se está procesando:</span><span class="sxs-lookup"><span data-stu-id="d9be5-226">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="d9be5-227">Prueba de una función con código</span><span class="sxs-lookup"><span data-stu-id="d9be5-227">Test a function with code</span></span>
<span data-ttu-id="d9be5-228">Puede que necesite toocreate un tootest externo de la aplicación o marco sus funciones.</span><span class="sxs-lookup"><span data-stu-id="d9be5-228">You may need toocreate an external application or framework tootest your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="d9be5-229">Prueba de una función de desencadenador HTTP con código: Node.js</span><span class="sxs-lookup"><span data-stu-id="d9be5-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="d9be5-230">Puede usar un tooexecute de aplicación Node.js un tootest de solicitud HTTP de la función.</span><span class="sxs-lookup"><span data-stu-id="d9be5-230">You can use a Node.js app tooexecute an HTTP request tootest your function.</span></span>
<span data-ttu-id="d9be5-231">Asegúrese de tooset seguro:</span><span class="sxs-lookup"><span data-stu-id="d9be5-231">Make sure tooset:</span></span>

* <span data-ttu-id="d9be5-232">Hola `host` en host de aplicación de funciones de tooyour opciones de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-232">hello `host` in hello request options tooyour function app host.</span></span>
* <span data-ttu-id="d9be5-233">El nombre de función en hello `path`.</span><span class="sxs-lookup"><span data-stu-id="d9be5-233">Your function name in hello `path`.</span></span>
* <span data-ttu-id="d9be5-234">El código de acceso (`<your code>`) en hello `path`.</span><span class="sxs-lookup"><span data-stu-id="d9be5-234">Your access code (`<your code>`) in hello `path`.</span></span>

<span data-ttu-id="d9be5-235">Ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="d9be5-235">Code example:</span></span>

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


<span data-ttu-id="d9be5-236">Salida:</span><span class="sxs-lookup"><span data-stu-id="d9be5-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    hello address you provided is Dallas, T.X. 75201

<span data-ttu-id="d9be5-237">En el portal de hello **registros** similar siguiente toohello se registra en la ejecución de la función hello de salida de ventana,:</span><span class="sxs-lookup"><span data-stu-id="d9be5-237">In hello portal **Logs** window, output similar toohello following is logged in executing hello function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected toolog-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="d9be5-238">Prueba de una función de desencadenador de cola con código: C#</span><span class="sxs-lookup"><span data-stu-id="d9be5-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="d9be5-239">Se ha mencionado anteriormente que puede probar un desencadenador de la cola mediante código toodrop un mensaje en la cola.</span><span class="sxs-lookup"><span data-stu-id="d9be5-239">We mentioned earlier that you can test a queue trigger by using code toodrop a message in your queue.</span></span> <span data-ttu-id="d9be5-240">Hola siguiendo el ejemplo de código se basa en código de hello C# presentado en hello [Introducción al almacenamiento de colas de Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="d9be5-240">hello following example code is based on hello C# code presented in hello [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="d9be5-241">También se ofrece código para otros lenguajes en ese vínculo.</span><span class="sxs-lookup"><span data-stu-id="d9be5-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="d9be5-242">tootest este código en una aplicación de consola, debe:</span><span class="sxs-lookup"><span data-stu-id="d9be5-242">tootest this code in a console app, you must:</span></span>

* <span data-ttu-id="d9be5-243">[Configurar la cadena de conexión de almacenamiento en archivo app.config de hello](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="d9be5-243">[Configure your storage connection string in hello app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="d9be5-244">Pasar un `name` y `address` como aplicación de toohello de parámetros.</span><span class="sxs-lookup"><span data-stu-id="d9be5-244">Pass a `name` and `address` as parameters toohello app.</span></span> <span data-ttu-id="d9be5-245">Por ejemplo: `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="d9be5-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="d9be5-246">(Este código acepta Hola nombre y una dirección para un nuevo usuario como argumentos de línea de comandos en tiempo de ejecución.)</span><span class="sxs-lookup"><span data-stu-id="d9be5-246">(This code accepts hello name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="d9be5-247">Ejemplo de código C#:</span><span class="sxs-lookup"><span data-stu-id="d9be5-247">Example C# code:</span></span>

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

<span data-ttu-id="d9be5-248">En la ventana del explorador de hello para la función de la cola de hello, puede ver cada mensaje que se está procesando:</span><span class="sxs-lookup"><span data-stu-id="d9be5-248">In hello browser window for hello queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected toolog-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[portal de Azure]: https://portal.azure.com
