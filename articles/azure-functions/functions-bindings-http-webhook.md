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
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="3e3cb-104">Enlaces HTTP y webhook en funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="3e3cb-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="3e3cb-105">Este artículo explica cómo se desencadena tooconfigure y trabajar con HTTP y los enlaces de funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="3e3cb-106">Con esto, puede usar las funciones de Azure toobuild sin servidor API y responden toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="3e3cb-107">Las funciones de Azure proporciona Hola siguientes enlaces:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="3e3cb-108">Un [desencadenador HTTP](#httptrigger) permite invocar una función con una solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="3e3cb-109">Esto puede ser demasiado personalizada toorespond[webhooks](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="3e3cb-110">Un [enlace de salida HTTP](#output) permite toorespond toohello solicitud.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="3e3cb-111">Desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="3e3cb-111">HTTP trigger</span></span>
<span data-ttu-id="3e3cb-112">desencadenador de Hello HTTP ejecutará la función en la solicitud HTTP de respuesta tooan.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="3e3cb-113">Puede personalizarlo toorespond tooa dirección URL en particular o un conjunto de métodos HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="3e3cb-114">Un desencadenador HTTP también puede ser toowebhooks toorespond configurado.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="3e3cb-115">Si usa el portal de funciones de hello, puede también empezará a inmediatamente mediante una plantilla definida previamente.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="3e3cb-116">Seleccione **nueva función** y elegir "API & Webhooks" hello **escenario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="3e3cb-117">Seleccione una de las plantillas de Hola y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="3e3cb-118">De forma predeterminada, un desencadenador HTTP responderá toohello solicitud con un código de estado HTTP 200 OK y un cuerpo vacío.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="3e3cb-119">toomodify Hola respuesta, configure un [HTTP el enlace de salida](#output)</span><span class="sxs-lookup"><span data-stu-id="3e3cb-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="3e3cb-120">Configuración de un desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="3e3cb-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="3e3cb-121">Se define un desencadenador HTTP mediante la inclusión de un toohello similar del objeto JSON siguiente en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

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
<span data-ttu-id="3e3cb-122">enlace de Hello admite Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="3e3cb-123">**nombre** : requerida: nombre de variable de saludo utilizado en código de la función para la solicitud de Hola o cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="3e3cb-124">Consulte [Trabajar con un desencadenador HTTP desde código](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="3e3cb-125">**tipo de** : requerida: debe estar configurado demasiado "httpTrigger".</span><span class="sxs-lookup"><span data-stu-id="3e3cb-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="3e3cb-126">**dirección** : requerida: debe ser establecido demasiado "in".</span><span class="sxs-lookup"><span data-stu-id="3e3cb-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="3e3cb-127">_authLevel_ : Esto determina qué claves, si existe, necesitan toobe presente en la solicitud de hello en función de orden tooinvoke Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="3e3cb-128">Consulte [Trabajar con claves](#keys) a continuación.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="3e3cb-129">valor de Hello puede ser uno de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="3e3cb-130">_anonymous_: no se requiere ninguna clave de API.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="3e3cb-131">_function_: se requiere una clave de API específica de la función.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="3e3cb-132">Esto es el valor predeterminado de hello si no se proporciona ninguno.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="3e3cb-133">_administración_ : Hola master clave es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="3e3cb-134">**métodos** : se trata de una matriz de los métodos de hello HTTP responderá la función de hello toowhich.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="3e3cb-135">Si no se especifica, la función hello responderá métodos tooall HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="3e3cb-136">Vea [personalizar el punto de conexión de hello HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="3e3cb-137">**ruta** : Esto define la plantilla de ruta de hello, controlar toowhich responderá la función de las direcciones URL de solicitud.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="3e3cb-138">Hello valor predeterminado si no se proporciona ninguno es `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="3e3cb-139">Vea [personalizar el punto de conexión de hello HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="3e3cb-140">**webHookType** : Esto configura Hola HTTP desencadenador tooact como un destinatario de webhook para el proveedor especificado Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="3e3cb-141">Hola _métodos_ propiedad no debe establecerse si esto se elige.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="3e3cb-142">Vea [toowebhooks responde](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="3e3cb-143">valor de Hello puede ser uno de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="3e3cb-144">_genericJson_: un punto de conexión de webhook de uso general sin lógica para un proveedor concreto.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="3e3cb-145">_github_ : función hello responderá tooGitHub webhook.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="3e3cb-146">Hola _authLevel_ propiedad no debe establecerse si esto se elige.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="3e3cb-147">_demora_ : función hello responderá tooSlack webhook.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="3e3cb-148">Hola _authLevel_ propiedad no debe establecerse si esto se elige.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="3e3cb-149">Trabajar con un desencadenador HTTP desde código</span><span class="sxs-lookup"><span data-stu-id="3e3cb-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="3e3cb-150">Para las funciones de C# y F #, puede declarar tipo hello de su toobe de entrada de desencadenador ya sea `HttpRequestMessage` o un tipo personalizado.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="3e3cb-151">Si elige `HttpRequestMessage`, a continuación, obtendrá el objeto de solicitud de acceso completo toohello.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="3e3cb-152">Para un tipo personalizado (por ejemplo, un POCO), funciones intentarán tooparse cuerpo de la solicitud de hello como propiedades del objeto JSON toopopulate Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="3e3cb-153">Para las funciones de Node.js, en tiempo de ejecución de funciones de hello proporciona cuerpo de la solicitud de hello en lugar del objeto de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="3e3cb-154">Consulte [Ejemplos de desencadenador HTTP](#httptriggersample) para ver ejemplos de uso.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="3e3cb-155">Enlace de salida de respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="3e3cb-155">HTTP response output binding</span></span>
<span data-ttu-id="3e3cb-156">Utilice Hola HTTP salida enlace toorespond toohello HTTP remitente de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="3e3cb-157">Este enlace requiere un desencadenador HTTP y permite la respuesta de hello toocustomize asociado a la solicitud del desencadenador Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="3e3cb-158">Si no se proporciona el enlace de salida HTTP, un desencadenador HTTP devolverá HTTP 200 OK con un cuerpo vacío.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="3e3cb-159">Configuración de un enlace de salida HTTP</span><span class="sxs-lookup"><span data-stu-id="3e3cb-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="3e3cb-160">Hola HTTP de salida enlace se define mediante la inclusión de un toohello similar del objeto JSON siguiente en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="3e3cb-161">enlace de Hello contiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="3e3cb-162">**nombre** : requerida: Hola nombre de variable utilizada en el código de función para hello respuesta.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="3e3cb-163">Consulte [Trabajar con un enlace de salida HTTP desde código](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="3e3cb-164">**tipo de** : requerida: debe estar configurado demasiado "http".</span><span class="sxs-lookup"><span data-stu-id="3e3cb-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="3e3cb-165">**dirección** : requerida: debe ser establecido demasiado "out".</span><span class="sxs-lookup"><span data-stu-id="3e3cb-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="3e3cb-166">Trabajar con un enlace de salida HTTP desde código</span><span class="sxs-lookup"><span data-stu-id="3e3cb-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="3e3cb-167">Puede usar Hola salida parámetro (p. ej., "res") toorespond toohello http o webhook autor de la llamada.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="3e3cb-168">Como alternativa, puede usar el estándar de `Request.CreateResponse()` (C#) o `context.res` (Node.JS) patrón tooreturn su respuesta.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="3e3cb-169">Para obtener ejemplos sobre cómo toouse Hola último método, consulte [ejemplos de desencadenador HTTP](#httptriggersample) y [ejemplos de desencadenador de Webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="3e3cb-170">Responde toowebhooks</span><span class="sxs-lookup"><span data-stu-id="3e3cb-170">Responding toowebhooks</span></span>
<span data-ttu-id="3e3cb-171">Un desencadenador HTTP con hello _webHookType_ propiedad será demasiado configurado toorespond[webhooks](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="3e3cb-172">configuración básica de Hello usa la configuración de "genericJson" Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="3e3cb-173">Esto restringe las solicitudes tooonly aquellas que usan HTTP POST y con hello `application/json` tipo de contenido.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="3e3cb-174">Hello desencadenador se puede adaptar tooa webhook específico proveedor (p. ej., [GitHub](https://developer.github.com/webhooks/) y [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="3e3cb-175">Si se especifica un proveedor, en tiempo de ejecución de funciones de hello puede ocuparse de lógica de validación del proveedor de Hola para usted.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="3e3cb-176">Configuración de GitHub como proveedor de webhook</span><span class="sxs-lookup"><span data-stu-id="3e3cb-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="3e3cb-177">toorespond tooGitHub webhooks, primero cree la función con un desencadenador de HTTP y establezca hello _webHookType_ propiedad demasiado "github".</span><span class="sxs-lookup"><span data-stu-id="3e3cb-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="3e3cb-178">A continuación, copie su [dirección URL](#url) y [la clave de API](#keys) en la página **Agregar Webhook** del repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="3e3cb-179">Consulte la documentación [Creación de Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) de GitHub para más información.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="3e3cb-180">Configuración de Slack como un proveedor de webhooks</span><span class="sxs-lookup"><span data-stu-id="3e3cb-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="3e3cb-181">Hola demora webhook genera un token en lugar de lo que le permite especificar, por lo que debe configurar una clave específica de la función con token de hello demora.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="3e3cb-182">Consulte [Trabajar con claves](#keys).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="3e3cb-183">Personalización de extremo HTTP de Hola</span><span class="sxs-lookup"><span data-stu-id="3e3cb-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="3e3cb-184">De forma predeterminada cuando se crea una función para un desencadenador HTTP, o un WebHook, función hello es direccionable con una ruta de formulario de hello:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="3e3cb-185">Puede personalizar esta ruta mediante Hola opcional `route` enlace de entrada de propiedad en el desencadenador de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="3e3cb-186">Por ejemplo, Hola después *function.json* archivo define un `route` propiedad de un desencadenador HTTP:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="3e3cb-187">Con esta configuración, función hello es ahora direccionable con hello siguiendo la ruta en lugar de la ruta original de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="3e3cb-188">Esto permite al código de la función hello toosupport dos parámetros en la dirección de hello, "categoría" e "id".</span><span class="sxs-lookup"><span data-stu-id="3e3cb-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="3e3cb-189">Puede usar cualquier [restricción de ruta de API web](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) con sus parámetros.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="3e3cb-190">Hola después el código de la función de C# hace uso de ambos parámetros.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-190">hello following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="3e3cb-191">Aquí es Hola de toouse de código de función de Node.js mismo parámetros de ruta.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-191">Here is Node.js function code toouse hello same route parameters.</span></span>

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

<span data-ttu-id="3e3cb-192">De forma predeterminada, todas las rutas de la función tienen el prefijo *api*.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="3e3cb-193">También puede personalizar o quitar prefijo hello mediante hello `http.routePrefix` propiedad en su *host.json* archivo.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="3e3cb-194">Hello en el ejemplo siguiente se quita hello *api* prefijo de ruta mediante el uso de una cadena vacía para el prefijo de Hola Hola *host.json* archivo.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="3e3cb-195">Para obtener información detallada sobre cómo hello tooupdate *host.json* archivo para la función, vea [forma en que tooupdate funcionan los archivos de la aplicación](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="3e3cb-196">Para obtener información sobre otras propiedades que puede configurar en el archivo *host.json*, consulte la [referencia de host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="3e3cb-197">Trabajar con claves</span><span class="sxs-lookup"><span data-stu-id="3e3cb-197">Working with keys</span></span>
<span data-ttu-id="3e3cb-198">HttpTriggers puede hacer uso de claves para aumentar la seguridad.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="3e3cb-199">Un estándar HttpTrigger puede utilizar como una clave de API, que requieren hello toobe clave presente en la solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="3e3cb-200">Webhooks puede usar claves tooauthorize solicitudes de varias maneras, dependiendo de qué proveedor de hello es compatible con.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="3e3cb-201">Las claves se almacenan como parte de la aplicación de función en Azure y se cifran en reposo.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="3e3cb-202">tooview sus claves, crear nuevos o toonew valores de claves de consolidación, desplácese tooone de las funciones en el portal de Hola y seleccione "Administrar".</span><span class="sxs-lookup"><span data-stu-id="3e3cb-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="3e3cb-203">Existen dos tipos de claves:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-203">There are two types of keys:</span></span>
- <span data-ttu-id="3e3cb-204">**Claves de host**: estas claves se comparten entre todas las funciones de aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="3e3cb-205">Cuando se utiliza como una clave de API, permiten acceso tooany función dentro de la aplicación de la función de hello.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="3e3cb-206">**Las teclas de función**: estas claves aplican solo toohello funciones específicas en las que se definen.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="3e3cb-207">Cuando se utiliza como una clave de API, estos solo permite acceso toothat función.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="3e3cb-208">Cada clave con el nombre de referencia y no hay una clave predeterminada (denominada "default") en el nivel de función y el host de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="3e3cb-209">Hola **clave maestra** es una clave de host predeterminado denominada "_master" que se define para cada aplicación de función y no se puede revocar.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="3e3cb-210">Proporciona acceso administrativo toohello runtime API.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="3e3cb-211">Usar `"authLevel": "admin"` Hola enlace JSON requerirá esta clave toobe presentada cuando se solicite Hola; cualquier otra clave se producirá un error de autorización.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="3e3cb-212">Due toohello elevados permisos concedidos por la clave maestra de hello, no debe compartir esta clave con terceras partes o distribuirla en aplicaciones cliente nativas.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="3e3cb-213">Tenga cuidado al elegir el nivel de administrador de autorización de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="3e3cb-214">Autorización de la clave de API</span><span class="sxs-lookup"><span data-stu-id="3e3cb-214">API key authorization</span></span>
<span data-ttu-id="3e3cb-215">De forma predeterminada, un HttpTrigger requiere una clave de API de solicitud HTTP de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="3e3cb-216">Por lo tanto, su solicitud HTTP normalmente se verá así:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="3e3cb-217">clave de Hello puede incluirse en una variable de cadena de consulta denominada `code`, como el anterior, o puede incluirse en un `x-functions-key` encabezado HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="3e3cb-218">valor de Hola de clave de hello puede ser cualquier tecla de función definido para la función de Hola o cualquier clave de host.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="3e3cb-219">Puede elegir solicitudes tooallow sin claves o especificar esa clave maestra de Hola se debe utilizar cambiando hello `authLevel` propiedad Hola enlace JSON (vea [desencadenador HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="3e3cb-220">Claves y webhooks</span><span class="sxs-lookup"><span data-stu-id="3e3cb-220">Keys and webhooks</span></span>
<span data-ttu-id="3e3cb-221">Autorización de Webhook se controla mediante el componente de hello webhook el destinatario, parte del mecanismo de Hola y de saludo HttpTrigger varía en función de tipo de webhook Hola.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="3e3cb-222">Sin embargo, cada mecanismo se basa en una clave.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="3e3cb-223">De forma predeterminada, se usará la tecla de función hello denominado "default".</span><span class="sxs-lookup"><span data-stu-id="3e3cb-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="3e3cb-224">Si desea toouse una clave diferente, necesitará tooconfigure hello webhook proveedor toosend Hola clave nombre con solicitud de hello en uno de hello siguientes maneras:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="3e3cb-225">**Cadena de consulta**: proveedor de hello pasa el nombre de clave de Hola Hola `clientid` parámetro de cadena de consulta (por ejemplo, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="3e3cb-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="3e3cb-226">**Encabezado de solicitud**: proveedor de hello pasa el nombre de clave de Hola Hola `x-functions-clientid` encabezado.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="3e3cb-227">Las claves de función tienen prioridad sobre las claves de host.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="3e3cb-228">Si se definen dos claves con el mismo nombre, hello de Hola se usará la tecla de función.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="3e3cb-229">Ejemplos de desencadenador HTTP</span><span class="sxs-lookup"><span data-stu-id="3e3cb-229">HTTP trigger samples</span></span>
<span data-ttu-id="3e3cb-230">Suponga que tiene Hola después de desencadenador HTTP en hello `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="3e3cb-231">Vea ejemplo de Hola a específicos del idioma que busca un `name` parámetro en cadena de consulta de Hola o cuerpo de saludo de solicitud de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="3e3cb-232">C#</span><span class="sxs-lookup"><span data-stu-id="3e3cb-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="3e3cb-233">F#</span><span class="sxs-lookup"><span data-stu-id="3e3cb-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="3e3cb-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="3e3cb-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="3e3cb-235">Ejemplo de desencadenador HTTP en C#</span><span class="sxs-lookup"><span data-stu-id="3e3cb-235">HTTP trigger sample in C#</span></span> #
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

<span data-ttu-id="3e3cb-236">También puede enlazar tooa POCO en lugar de `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="3e3cb-237">Esto se hidrate de cuerpo de saludo de solicitud de hello, analizado como JSON.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="3e3cb-238">De forma similar, puede pasar un tipo de salida de respuesta HTTP toohello enlace, y esto se devolverán como cuerpo de respuesta de hello, con un código de 200 estado.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="3e3cb-239">Ejemplo de desencadenador HTTP en F#</span><span class="sxs-lookup"><span data-stu-id="3e3cb-239">HTTP trigger sample in F#</span></span> #
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

<span data-ttu-id="3e3cb-240">Necesita un `project.json` archivo que usa NuGet tooreference hello `FSharp.Interop.Dynamic` y `Dynamitey` ensamblados, similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="3e3cb-241">Se usarán NuGet toofetch las dependencias y se hará referencia a ellos en el script.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="3e3cb-242">Ejemplo de desencadenador HTTP en Node.js</span><span class="sxs-lookup"><span data-stu-id="3e3cb-242">HTTP trigger sample in Node.JS</span></span>
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
## <a name="webhook-samples"></a><span data-ttu-id="3e3cb-243">Ejemplos de webhook</span><span class="sxs-lookup"><span data-stu-id="3e3cb-243">Webhook samples</span></span>
<span data-ttu-id="3e3cb-244">Suponga que tiene Hola siguiendo el desencadenador de webhook Hola `bindings` matriz de function.json:</span><span class="sxs-lookup"><span data-stu-id="3e3cb-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="3e3cb-245">Vea el ejemplo específico del idioma de Hola que registra los comentarios del problema de GitHub.</span><span class="sxs-lookup"><span data-stu-id="3e3cb-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="3e3cb-246">C#</span><span class="sxs-lookup"><span data-stu-id="3e3cb-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="3e3cb-247">F#</span><span class="sxs-lookup"><span data-stu-id="3e3cb-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="3e3cb-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="3e3cb-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="3e3cb-249">Ejemplo de webhook en C#</span><span class="sxs-lookup"><span data-stu-id="3e3cb-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="3e3cb-250">Ejemplo de webhook en F#</span><span class="sxs-lookup"><span data-stu-id="3e3cb-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="3e3cb-251">Ejemplo de webhook en Node.js</span><span class="sxs-lookup"><span data-stu-id="3e3cb-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="3e3cb-252">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e3cb-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

