---
title: Enlaces de webhook y HTTP de Azure Functions | Microsoft Docs
description: "Descubra cómo utilizar desencadenadores y enlaces HTTP y webhook en funciones de Azure."
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
ms.openlocfilehash: 71c0d22c4b1824078982b9d1cc76645f947ae603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="eca3e-104">Enlaces HTTP y webhook en funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="eca3e-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="eca3e-105">En este artículo se explica cómo configurar y trabajar con desencadenadores y enlaces HTTP en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="eca3e-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="eca3e-106">Con ellos, puede usar Azure Functions para crear API sin servidor y responder a webhooks.</span><span class="sxs-lookup"><span data-stu-id="eca3e-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span></span>

<span data-ttu-id="eca3e-107">Azure Functions proporciona los siguientes enlaces:</span><span class="sxs-lookup"><span data-stu-id="eca3e-107">Azure Functions provides the following bindings:</span></span>
- <span data-ttu-id="eca3e-108">Un [desencadenador HTTP](#httptrigger) permite invocar una función con una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="eca3e-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="eca3e-109">Puede personalizarlo para responder a [webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="eca3e-109">This can be customized to respond to [webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="eca3e-110">Un [enlace de salida HTTP](#output) le permite responder a la solicitud.</span><span class="sxs-lookup"><span data-stu-id="eca3e-110">An [HTTP output binding](#output) allows you to respond to the request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="eca3e-111">Desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="eca3e-111">HTTP trigger</span></span>
<span data-ttu-id="eca3e-112">El desencadenador HTTP ejecutará la función en respuesta a una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="eca3e-112">The HTTP trigger will execute your function in response to an HTTP request.</span></span> <span data-ttu-id="eca3e-113">Puede personalizarlo para que responda a una dirección URL o un conjunto de métodos HTTP determinados.</span><span class="sxs-lookup"><span data-stu-id="eca3e-113">You can customize it to respond to a particular URL or set of HTTP methods.</span></span> <span data-ttu-id="eca3e-114">Un desencadenador HTTP también se puede configurar para responder a webhooks.</span><span class="sxs-lookup"><span data-stu-id="eca3e-114">An HTTP trigger can also be configured to respond to webhooks.</span></span> 

<span data-ttu-id="eca3e-115">Si usa el portal de Functions, también puede comenzar de inmediato a usar una plantilla predefinida.</span><span class="sxs-lookup"><span data-stu-id="eca3e-115">If using the Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="eca3e-116">Seleccione **Nueva función** y elija "API y Webhooks" en el menú desplegable **Escenario**.</span><span class="sxs-lookup"><span data-stu-id="eca3e-116">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span></span> <span data-ttu-id="eca3e-117">Seleccione una de las plantillas y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="eca3e-117">Select one of the templates and click **Create**.</span></span>

<span data-ttu-id="eca3e-118">De forma predeterminada, un desencadenador HTTP responderá a la solicitud con un código de estado HTTP 200 OK y un cuerpo vacío.</span><span class="sxs-lookup"><span data-stu-id="eca3e-118">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="eca3e-119">Para modificar la respuesta, configure un [enlace de salida HTTP](#output).</span><span class="sxs-lookup"><span data-stu-id="eca3e-119">To modify the response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="eca3e-120">Configuración de un desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="eca3e-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="eca3e-121">Un desencadenador HTTP se define mediante la inclusión de un objeto JSON similar al siguiente en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="eca3e-121">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

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
<span data-ttu-id="eca3e-122">El enlace admite las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="eca3e-122">The binding supports the following properties:</span></span>

* <span data-ttu-id="eca3e-123">**name** (Requerido): el nombre de variable que se usa en el código de función para la solicitud o el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="eca3e-123">**name** : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="eca3e-124">Consulte [Trabajar con un desencadenador HTTP desde código](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="eca3e-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="eca3e-125">**type** (Requerido): debe establecerse en "httpTrigger".</span><span class="sxs-lookup"><span data-stu-id="eca3e-125">**type** : Required - must be set to "httpTrigger".</span></span>
* <span data-ttu-id="eca3e-126">**dirección** (Requerido): debe establecerse en "in".</span><span class="sxs-lookup"><span data-stu-id="eca3e-126">**direction** : Required - must be set to "in".</span></span>
* <span data-ttu-id="eca3e-127">_authLevel_: determina qué claves, si las hay, deben estar presentes en la solicitud para poder invocar la función.</span><span class="sxs-lookup"><span data-stu-id="eca3e-127">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="eca3e-128">Consulte [Trabajar con claves](#keys) a continuación.</span><span class="sxs-lookup"><span data-stu-id="eca3e-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="eca3e-129">El valor puede ser uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="eca3e-129">The value can be one of the following:</span></span>
    * <span data-ttu-id="eca3e-130">_anonymous_: no se requiere ninguna clave de API.</span><span class="sxs-lookup"><span data-stu-id="eca3e-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="eca3e-131">_function_: se requiere una clave de API específica de la función.</span><span class="sxs-lookup"><span data-stu-id="eca3e-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="eca3e-132">Este es el valor predeterminado si no se proporciona ninguno.</span><span class="sxs-lookup"><span data-stu-id="eca3e-132">This is the default value if none is provided.</span></span>
    * <span data-ttu-id="eca3e-133">_admin_: se requiere la clave maestra.</span><span class="sxs-lookup"><span data-stu-id="eca3e-133">_admin_ : The master key is required.</span></span>
* <span data-ttu-id="eca3e-134">**methods**: se trata de una matriz de los métodos HTTP a los que responderá la función.</span><span class="sxs-lookup"><span data-stu-id="eca3e-134">**methods** : This is an array of the HTTP methods to which the function will respond.</span></span> <span data-ttu-id="eca3e-135">Si no se especifica, la función responderá a todos los métodos HTTP.</span><span class="sxs-lookup"><span data-stu-id="eca3e-135">If not specified, the function will respond to all HTTP methods.</span></span> <span data-ttu-id="eca3e-136">Consulte [Personalización del punto de conexión HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="eca3e-136">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="eca3e-137">**route**: define la plantilla de ruta y controla las direcciones URL de solicitud a las que responderá la función.</span><span class="sxs-lookup"><span data-stu-id="eca3e-137">**route** : This defines the route template, controlling to which request URLs your function will respond.</span></span> <span data-ttu-id="eca3e-138">El valor predeterminado es `<functionname>` si no se proporciona ninguno.</span><span class="sxs-lookup"><span data-stu-id="eca3e-138">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="eca3e-139">Consulte [Personalización del punto de conexión HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="eca3e-139">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="eca3e-140">**webHookType**: configura el desencadenador HTTP para que actúe como un receptor de webhook para el proveedor especificado.</span><span class="sxs-lookup"><span data-stu-id="eca3e-140">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span></span> <span data-ttu-id="eca3e-141">Si se elige esta opción, no debe establecerse la propiedad _methods_.</span><span class="sxs-lookup"><span data-stu-id="eca3e-141">The _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="eca3e-142">Consulte [Respuesta a webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="eca3e-142">See [Responding to webhooks](#hooktrigger).</span></span> <span data-ttu-id="eca3e-143">El valor puede ser uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="eca3e-143">The value can be one of the following:</span></span>
    * <span data-ttu-id="eca3e-144">_genericJson_: un punto de conexión de webhook de uso general sin lógica para un proveedor concreto.</span><span class="sxs-lookup"><span data-stu-id="eca3e-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="eca3e-145">_github_: la función responderá a webhooks de GitHub.</span><span class="sxs-lookup"><span data-stu-id="eca3e-145">_github_ : The function will respond to GitHub webhooks.</span></span> <span data-ttu-id="eca3e-146">Si se elige esta opción, no debe establecerse la propiedad _authLevel_.</span><span class="sxs-lookup"><span data-stu-id="eca3e-146">The _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="eca3e-147">_slack_: la función responderá a webhooks de Slack.</span><span class="sxs-lookup"><span data-stu-id="eca3e-147">_slack_ : The function will respond to Slack webhooks.</span></span> <span data-ttu-id="eca3e-148">Si se elige esta opción, no debe establecerse la propiedad _authLevel_.</span><span class="sxs-lookup"><span data-stu-id="eca3e-148">The _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="eca3e-149">Trabajar con un desencadenador HTTP desde código</span><span class="sxs-lookup"><span data-stu-id="eca3e-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="eca3e-150">Para las funciones C# y F #, puede declarar que el tipo de entrada del desencadenador sea `HttpRequestMessage` o un tipo personalizado.</span><span class="sxs-lookup"><span data-stu-id="eca3e-150">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="eca3e-151">Si elige `HttpRequestMessage`, obtendrá acceso completo al objeto de solicitud.</span><span class="sxs-lookup"><span data-stu-id="eca3e-151">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span></span> <span data-ttu-id="eca3e-152">Para un tipo personalizado (como, POCO), Functions intentará analizar el cuerpo de la solicitud como JSON para rellenar las propiedades del objeto.</span><span class="sxs-lookup"><span data-stu-id="eca3e-152">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span></span>

<span data-ttu-id="eca3e-153">Para las funciones de Node.js, el sistema en tiempo de ejecución de Funciones proporciona el cuerpo de la solicitud en lugar del objeto de solicitud.</span><span class="sxs-lookup"><span data-stu-id="eca3e-153">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span></span>

<span data-ttu-id="eca3e-154">Consulte [Ejemplos de desencadenador HTTP](#httptriggersample) para ver ejemplos de uso.</span><span class="sxs-lookup"><span data-stu-id="eca3e-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="eca3e-155">Enlace de salida de respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="eca3e-155">HTTP response output binding</span></span>
<span data-ttu-id="eca3e-156">Use el enlace de salida HTTP para responder al remitente de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="eca3e-156">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="eca3e-157">Este enlace requiere un desencadenador HTTP y le permite personalizar la respuesta asociada con la solicitud del desencadenador.</span><span class="sxs-lookup"><span data-stu-id="eca3e-157">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="eca3e-158">Si no se proporciona el enlace de salida HTTP, un desencadenador HTTP devolverá HTTP 200 OK con un cuerpo vacío.</span><span class="sxs-lookup"><span data-stu-id="eca3e-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="eca3e-159">Configuración de un enlace de salida HTTP</span><span class="sxs-lookup"><span data-stu-id="eca3e-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="eca3e-160">El enlace de salida HTTP se define mediante la inclusión de un objeto JSON similar al siguiente en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="eca3e-160">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="eca3e-161">El enlace contiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="eca3e-161">The binding contains the following properties:</span></span>

* <span data-ttu-id="eca3e-162">**name** (Requerido): el nombre de variable que se usa en el código de función para la respuesta.</span><span class="sxs-lookup"><span data-stu-id="eca3e-162">**name** : Required - the variable name used in function code for the response.</span></span> <span data-ttu-id="eca3e-163">Consulte [Trabajar con un enlace de salida HTTP desde código](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="eca3e-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="eca3e-164">**type** (Requerido): se debe establecer en "http".</span><span class="sxs-lookup"><span data-stu-id="eca3e-164">**type** : Required - must be set to "http".</span></span>
* <span data-ttu-id="eca3e-165">**dirección** (Requerido): debe establecerse en "out".</span><span class="sxs-lookup"><span data-stu-id="eca3e-165">**direction** : Required - must be set to "out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="eca3e-166">Trabajar con un enlace de salida HTTP desde código</span><span class="sxs-lookup"><span data-stu-id="eca3e-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="eca3e-167">Puede usar el parámetro de salida (p. ej., "res") para responder a autor de la llamada de http o webhook.</span><span class="sxs-lookup"><span data-stu-id="eca3e-167">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span></span> <span data-ttu-id="eca3e-168">Como alternativa, puede usar el patrón `Request.CreateResponse()` (C#) o `context.res` estándar (Node.JS) para devolver la respuesta.</span><span class="sxs-lookup"><span data-stu-id="eca3e-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span></span> <span data-ttu-id="eca3e-169">Para ver ejemplos de cómo usar el último método, consulte [Ejemplos de desencadenador HTTP](#httptriggersample) y [Ejemplos de desencadenador de webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="eca3e-169">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a><span data-ttu-id="eca3e-170">Respuesta a webhooks</span><span class="sxs-lookup"><span data-stu-id="eca3e-170">Responding to webhooks</span></span>
<span data-ttu-id="eca3e-171">Un desencadenador HTTP con la propiedad _webHookType_ se configurará para responder a [webhooks](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="eca3e-171">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="eca3e-172">La configuración básica usa el valor "genericJson".</span><span class="sxs-lookup"><span data-stu-id="eca3e-172">The basic configuration uses the "genericJson" setting.</span></span> <span data-ttu-id="eca3e-173">Este valor restringe las solicitudes a solo aquellas que usan HTTP POST y con el tipo de contenido `application/json`.</span><span class="sxs-lookup"><span data-stu-id="eca3e-173">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span>

<span data-ttu-id="eca3e-174">El desencadenador se puede adaptar adicionalmente a un proveedor de webhook específico (p. ej., [GitHub](https://developer.github.com/webhooks/) y [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="eca3e-174">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="eca3e-175">Si se especifica un proveedor, el tiempo de ejecución de Functions puede encargarse de la lógica de validación del proveedor.</span><span class="sxs-lookup"><span data-stu-id="eca3e-175">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="eca3e-176">Configuración de GitHub como proveedor de webhook</span><span class="sxs-lookup"><span data-stu-id="eca3e-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="eca3e-177">Para responder a un webhook de GitHub, primero cree una función con un desencadenador HTTP y establezca la propiedad _webHookType_ en "github".</span><span class="sxs-lookup"><span data-stu-id="eca3e-177">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span></span> <span data-ttu-id="eca3e-178">A continuación, copie su [dirección URL](#url) y [la clave de API](#keys) en la página **Agregar Webhook** del repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="eca3e-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="eca3e-179">Consulte la documentación [Creación de Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) de GitHub para más información.</span><span class="sxs-lookup"><span data-stu-id="eca3e-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="eca3e-180">Configuración de Slack como un proveedor de webhooks</span><span class="sxs-lookup"><span data-stu-id="eca3e-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="eca3e-181">El webhook de Slack genera un token en lugar de permitirle especificarlo, por lo que debe configurar una clave específica de función con el token desde Slack.</span><span class="sxs-lookup"><span data-stu-id="eca3e-181">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="eca3e-182">Consulte [Trabajar con claves](#keys).</span><span class="sxs-lookup"><span data-stu-id="eca3e-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a><span data-ttu-id="eca3e-183">Personalización del punto de conexión HTTP</span><span class="sxs-lookup"><span data-stu-id="eca3e-183">Customizing the HTTP endpoint</span></span>
<span data-ttu-id="eca3e-184">De forma predeterminada, al crear una función para un desencadenador HTTP, o webhook, la función se puede dirigir con una ruta que tenga el siguiente formato:</span><span class="sxs-lookup"><span data-stu-id="eca3e-184">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="eca3e-185">Puede personalizar esta ruta mediante el parámetro opcional `route` del enlace de entrada del desencadenador HTTP.</span><span class="sxs-lookup"><span data-stu-id="eca3e-185">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="eca3e-186">Por ejemplo, el siguiente archivo *function.json* define una propiedad `route` para un desencadenador HTTP:</span><span class="sxs-lookup"><span data-stu-id="eca3e-186">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="eca3e-187">Al usar esta configuración, ya se podrá dirigir la función con la ruta de abajo, en lugar de con la original.</span><span class="sxs-lookup"><span data-stu-id="eca3e-187">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="eca3e-188">Esto permite que el código de función admita dos parámetros en la dirección: "category" e "id".</span><span class="sxs-lookup"><span data-stu-id="eca3e-188">This allows the function code to support two parameters in the address, "category" and "id".</span></span> <span data-ttu-id="eca3e-189">Puede usar cualquier [restricción de ruta de API web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) con sus parámetros.</span><span class="sxs-lookup"><span data-stu-id="eca3e-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="eca3e-190">El siguiente código de función de C# emplea los dos parámetros.</span><span class="sxs-lookup"><span data-stu-id="eca3e-190">The following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="eca3e-191">A continuación, encontrará un código de función de Node.js que usa los mismos parámetros de ruta.</span><span class="sxs-lookup"><span data-stu-id="eca3e-191">Here is Node.js function code to use the same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="eca3e-192">De forma predeterminada, todas las rutas de la función tienen el prefijo *api*.</span><span class="sxs-lookup"><span data-stu-id="eca3e-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="eca3e-193">También puede personalizar o quitar el prefijo con la propiedad `http.routePrefix` del archivo *host.json*.</span><span class="sxs-lookup"><span data-stu-id="eca3e-193">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="eca3e-194">En el ejemplo siguiente, se quita el prefijo de ruta *api* utilizando una cadena vacía del prefijo del archivo *host.json*.</span><span class="sxs-lookup"><span data-stu-id="eca3e-194">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="eca3e-195">Para obtener información detallada sobre cómo actualizar el archivo *host.json* para su función, consulte el artículo sobre [Actualización de los archivos de aplicación de función](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="eca3e-195">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="eca3e-196">Para obtener información sobre otras propiedades que puede configurar en el archivo *host.json*, consulte la [referencia de host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="eca3e-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="eca3e-197">Trabajar con claves</span><span class="sxs-lookup"><span data-stu-id="eca3e-197">Working with keys</span></span>
<span data-ttu-id="eca3e-198">HttpTriggers puede hacer uso de claves para aumentar la seguridad.</span><span class="sxs-lookup"><span data-stu-id="eca3e-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="eca3e-199">Un objeto HttpTrigger estándar puede usarlas como claves de API, que requieren que la clave exista en la solicitud.</span><span class="sxs-lookup"><span data-stu-id="eca3e-199">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="eca3e-200">Los webhooks pueden usar claves para autorizar solicitudes de varias maneras, según lo que admita el proveedor.</span><span class="sxs-lookup"><span data-stu-id="eca3e-200">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

<span data-ttu-id="eca3e-201">Las claves se almacenan como parte de la aplicación de función en Azure y se cifran en reposo.</span><span class="sxs-lookup"><span data-stu-id="eca3e-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="eca3e-202">Para ver las claves, crear unas nuevas o asignarles nuevos valores, desplácese a una de las funciones en el portal y seleccione "Administrar".</span><span class="sxs-lookup"><span data-stu-id="eca3e-202">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span></span> 

<span data-ttu-id="eca3e-203">Existen dos tipos de claves:</span><span class="sxs-lookup"><span data-stu-id="eca3e-203">There are two types of keys:</span></span>
- <span data-ttu-id="eca3e-204">**Claves de host**: estas claves se comparten entre todas las funciones dentro de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="eca3e-204">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="eca3e-205">Cuando se usan como una clave de API, permiten el acceso a cualquier función dentro de la aplicación de función.</span><span class="sxs-lookup"><span data-stu-id="eca3e-205">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="eca3e-206">**Claves de función**: estas claves se aplican solo a las funciones específicas en las que se definen.</span><span class="sxs-lookup"><span data-stu-id="eca3e-206">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="eca3e-207">Cuando se usan como una clave de API, solo permiten el acceso a esa función.</span><span class="sxs-lookup"><span data-stu-id="eca3e-207">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="eca3e-208">Para cada clave se usa un nombre fácilmente referenciable y hay una clave predeterminada (denominada "predeterminada") en el nivel de función y host.</span><span class="sxs-lookup"><span data-stu-id="eca3e-208">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="eca3e-209">La **clave maestra** es una clave de host predeterminada denominada "_master" que se define para cada aplicación de función y no se puede revocar.</span><span class="sxs-lookup"><span data-stu-id="eca3e-209">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="eca3e-210">Proporciona acceso administrativo a las API en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="eca3e-210">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="eca3e-211">El uso de `"authLevel": "admin"` en el enlace JSON requerirá que esta clave esté presente en la solicitud; cualquier otra clave producirá un error de autorización.</span><span class="sxs-lookup"><span data-stu-id="eca3e-211">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="eca3e-212">Debido a los permisos elevados otorgados por la clave maestra, no debe compartir esta clave con terceros ni distribuirla en aplicaciones cliente nativas.</span><span class="sxs-lookup"><span data-stu-id="eca3e-212">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="eca3e-213">Tenga cuidado al elegir el nivel de autorización del administrador.</span><span class="sxs-lookup"><span data-stu-id="eca3e-213">Exercise caution when choosing the admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="eca3e-214">Autorización de la clave de API</span><span class="sxs-lookup"><span data-stu-id="eca3e-214">API key authorization</span></span>
<span data-ttu-id="eca3e-215">De forma predeterminada, un objeto HttpTrigger requiere una clave de API en la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="eca3e-215">By default, an HttpTrigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="eca3e-216">Por lo tanto, su solicitud HTTP normalmente se verá así:</span><span class="sxs-lookup"><span data-stu-id="eca3e-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="eca3e-217">La clave se puede incluir en una variable de cadena de consulta denominada `code`, como se ha indicado anteriormente, o puede incluirse en un encabezado HTTP `x-functions-key`.</span><span class="sxs-lookup"><span data-stu-id="eca3e-217">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="eca3e-218">El valor de la clave puede ser cualquier clave de función definida para la función o cualquier clave de host.</span><span class="sxs-lookup"><span data-stu-id="eca3e-218">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="eca3e-219">Puede optar por permitir solicitudes sin claves o especificar que se use la clave maestra cambiando la propiedad `authLevel` en el JSON de enlace (consulte [Desencadenador HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="eca3e-219">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="eca3e-220">Claves y webhooks</span><span class="sxs-lookup"><span data-stu-id="eca3e-220">Keys and webhooks</span></span>
<span data-ttu-id="eca3e-221">La autorización de webhook se controla mediante el componente receptor de webhook, parte de HttpTrigger, y el mecanismo varía según el tipo de webhook.</span><span class="sxs-lookup"><span data-stu-id="eca3e-221">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="eca3e-222">Sin embargo, cada mecanismo se basa en una clave.</span><span class="sxs-lookup"><span data-stu-id="eca3e-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="eca3e-223">De forma predeterminada, se usará la clave de función denominada "predeterminada".</span><span class="sxs-lookup"><span data-stu-id="eca3e-223">By default, the function key named "default" will be used.</span></span> <span data-ttu-id="eca3e-224">Si quiere usar una clave diferente, debe configurar el proveedor de webhook para enviar el nombre de clave con la solicitud de una de las siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="eca3e-224">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="eca3e-225">**Cadena de consulta**: el proveedor pasa el nombre de la clave en el parámetro de la cadena de consulta `clientid` (por ejemplo, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="eca3e-225">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="eca3e-226">**Encabezado de solicitud**: el proveedor pasa el nombre de clave en el encabezado `x-functions-clientid`.</span><span class="sxs-lookup"><span data-stu-id="eca3e-226">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="eca3e-227">Las claves de función tienen prioridad sobre las claves de host.</span><span class="sxs-lookup"><span data-stu-id="eca3e-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="eca3e-228">Si se definen dos claves con el mismo nombre, se usará la clave de función.</span><span class="sxs-lookup"><span data-stu-id="eca3e-228">If two keys are defined with the same name, the function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="eca3e-229">Ejemplos de desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="eca3e-229">HTTP trigger samples</span></span>
<span data-ttu-id="eca3e-230">Supongamos que el siguiente desencadenador HTTP se encuentra en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="eca3e-230">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="eca3e-231">Consulte el ejemplo específico del idioma que busca un parámetro `name` en la cadena de consulta o en el cuerpo de la solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="eca3e-231">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

* [<span data-ttu-id="eca3e-232">C#</span><span class="sxs-lookup"><span data-stu-id="eca3e-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="eca3e-233">F#</span><span class="sxs-lookup"><span data-stu-id="eca3e-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="eca3e-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="eca3e-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="eca3e-235">Ejemplo de desencadenador HTTP en C#</span><span class="sxs-lookup"><span data-stu-id="eca3e-235">HTTP trigger sample in C#</span></span> #
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

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="eca3e-236">También puede enlazar a un mensaje POCO en lugar de `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="eca3e-236">You can also bind to a POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="eca3e-237">Se recibirá desde el cuerpo de la solicitud, analizado como JSON.</span><span class="sxs-lookup"><span data-stu-id="eca3e-237">This will be hydrated from the body of the request, parsed as JSON.</span></span> <span data-ttu-id="eca3e-238">De forma similar, puede pasarse un tipo al enlace de la salida de respuesta HTTP y se devolverá como cuerpo de la respuesta, con el código de estado 200.</span><span class="sxs-lookup"><span data-stu-id="eca3e-238">Similarly, a type can be passed to the HTTP response output binding, and this will be returned as the response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="eca3e-239">Ejemplo de desencadenador HTTP en F#</span><span class="sxs-lookup"><span data-stu-id="eca3e-239">HTTP trigger sample in F#</span></span> #
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
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="eca3e-240">Necesita un archivo `project.json` que use NuGet para hacer referencia a los ensamblados `FSharp.Interop.Dynamic` y `Dynamitey`, de este modo:</span><span class="sxs-lookup"><span data-stu-id="eca3e-240">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="eca3e-241">Se usará NuGet para capturar las dependencias y se hará referencia a ellas en el script.</span><span class="sxs-lookup"><span data-stu-id="eca3e-241">This will use NuGet to fetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="eca3e-242">Ejemplo de desencadenador HTTP en Node.js</span><span class="sxs-lookup"><span data-stu-id="eca3e-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="eca3e-243">Ejemplos de webhook</span><span class="sxs-lookup"><span data-stu-id="eca3e-243">Webhook samples</span></span>
<span data-ttu-id="eca3e-244">Supongamos que tiene el siguiente desencadenador webhook en la matriz `bindings` de function.json:</span><span class="sxs-lookup"><span data-stu-id="eca3e-244">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="eca3e-245">Consulte el ejemplo específico del idioma que registra comentarios de problemas de GitHub.</span><span class="sxs-lookup"><span data-stu-id="eca3e-245">See the language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="eca3e-246">C#</span><span class="sxs-lookup"><span data-stu-id="eca3e-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="eca3e-247">F#</span><span class="sxs-lookup"><span data-stu-id="eca3e-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="eca3e-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="eca3e-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="eca3e-249">Ejemplo de webhook en C#</span><span class="sxs-lookup"><span data-stu-id="eca3e-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="eca3e-250">Ejemplo de webhook en F#</span><span class="sxs-lookup"><span data-stu-id="eca3e-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="eca3e-251">Ejemplo de webhook en Node.js</span><span class="sxs-lookup"><span data-stu-id="eca3e-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="eca3e-252">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eca3e-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

