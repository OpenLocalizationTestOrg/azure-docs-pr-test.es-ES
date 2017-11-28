---
title: aaaCreate una API sin servidor mediante las funciones de Azure | Documentos de Microsoft
description: "¿Cómo toocreate una API sin servidor mediante las funciones de Azure"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a><span data-ttu-id="0d546-103">Creación de una API sin servidor mediante Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0d546-103">Create a serverless API using Azure Functions</span></span>

<span data-ttu-id="0d546-104">En este tutorial, aprenderá cómo las funciones de Azure permite toobuild API altamente escalable.</span><span class="sxs-lookup"><span data-stu-id="0d546-104">In this tutorial you will learn how Azure Functions allows you toobuild highly-scalable APIs.</span></span> <span data-ttu-id="0d546-105">Las funciones de Azure incluye una colección de integrados desencadenadores HTTP y los enlaces que sea fácil tooauthor un punto de conexión en una variedad de lenguajes, como Node.JS, C# y mucho más.</span><span class="sxs-lookup"><span data-stu-id="0d546-105">Azure Functions comes with a collection of built-in HTTP triggers and bindings which make it easy tooauthor an endpoint in a variety of languages, including Node.JS, C#, and more.</span></span> <span data-ttu-id="0d546-106">En este tutorial, va a personalizar una acción específica de HTTP desencadenador toohandle en el diseño de la API.</span><span class="sxs-lookup"><span data-stu-id="0d546-106">In this tutorial, you will customize an HTTP trigger toohandle specific actions in your API design.</span></span> <span data-ttu-id="0d546-107">También va a prepararse para ampliar su API integrándola con Servidores proxy de Azure Functions y configurando API simuladas.</span><span class="sxs-lookup"><span data-stu-id="0d546-107">You will also prepare for growing your API by integrating it with Azure Functions Proxies and setting up mock APIs.</span></span> <span data-ttu-id="0d546-108">Todo esto se logra encima de entorno Hola funciones sin servidor proceso, por lo que no tiene tooworry acerca de cómo escalar recursos, puede centrarse simplemente en la lógica de la API.</span><span class="sxs-lookup"><span data-stu-id="0d546-108">All of this is accomplished on top of hello Functions serverless compute environment, so you don't have tooworry about scaling resources - you can just focus on your API logic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d546-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0d546-109">Prerequisites</span></span> 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

<span data-ttu-id="0d546-110">función resultante Hola se usará para el resto de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0d546-110">hello resulting function will be used for hello rest of this tutorial.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="0d546-111">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="0d546-111">Sign in tooAzure</span></span>

<span data-ttu-id="0d546-112">Hola abrir portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d546-112">Open hello Azure portal.</span></span> <span data-ttu-id="0d546-113">toodo esto, inicie sesión en demasiado[https://portal.azure.com](https://portal.azure.com) con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d546-113">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com) with your Azure account.</span></span>

## <a name="customize-your-http-function"></a><span data-ttu-id="0d546-114">Personalización de la función HTTP</span><span class="sxs-lookup"><span data-stu-id="0d546-114">Customize your HTTP function</span></span>

<span data-ttu-id="0d546-115">De forma predeterminada, la función desencadena HTTP está configurado tooaccept cualquier método HTTP.</span><span class="sxs-lookup"><span data-stu-id="0d546-115">By default, your HTTP-triggered function is configured tooaccept any HTTP method.</span></span> <span data-ttu-id="0d546-116">También hay una dirección URL predeterminada del formulario de hello `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span><span class="sxs-lookup"><span data-stu-id="0d546-116">There is also a default URL of hello form `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`.</span></span> <span data-ttu-id="0d546-117">Si ha seguido inicio rápido de hello, a continuación, `<funcname>` probablemente es algo parecido a "HttpTriggerJS1".</span><span class="sxs-lookup"><span data-stu-id="0d546-117">If you followed hello quickstart, then `<funcname>` probably looks something like "HttpTriggerJS1".</span></span> <span data-ttu-id="0d546-118">En esta sección, modificará las solicitudes de toorespond tooGET solo función de Hola a `/api/hello` enrutar en su lugar.</span><span class="sxs-lookup"><span data-stu-id="0d546-118">In this section, you will modify hello function toorespond only tooGET requests against `/api/hello` route instead.</span></span> 

<span data-ttu-id="0d546-119">Navegar por función tooyour Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d546-119">Navigate tooyour function in hello Azure portal.</span></span> <span data-ttu-id="0d546-120">Seleccione **integrar** Hola barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="0d546-120">Select **Integrate** in hello left navigation.</span></span>

![Personalización de una función HTTP](./media/functions-create-serverless-api/customizing-http.png)

<span data-ttu-id="0d546-122">Use la configuración de desencadenador HTTP como se especifica en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-122">Use the HTTP trigger settings as specified in hello table.</span></span>

| <span data-ttu-id="0d546-123">Campo</span><span class="sxs-lookup"><span data-stu-id="0d546-123">Field</span></span> | <span data-ttu-id="0d546-124">Valor de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0d546-124">Sample value</span></span> | <span data-ttu-id="0d546-125">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d546-125">Description</span></span> |
|---|---|---|
| <span data-ttu-id="0d546-126">Métodos HTTP permitidos</span><span class="sxs-lookup"><span data-stu-id="0d546-126">Allowed HTTP methods</span></span> | <span data-ttu-id="0d546-127">Métodos seleccionados</span><span class="sxs-lookup"><span data-stu-id="0d546-127">Selected methods</span></span> | <span data-ttu-id="0d546-128">Determina los métodos HTTP que pueden ser tooinvoke usa esta función</span><span class="sxs-lookup"><span data-stu-id="0d546-128">Determines what HTTP methods may be used tooinvoke this function</span></span> |
| <span data-ttu-id="0d546-129">Métodos HTTP seleccionados</span><span class="sxs-lookup"><span data-stu-id="0d546-129">Selected HTTP methods</span></span> | <span data-ttu-id="0d546-130">GET</span><span class="sxs-lookup"><span data-stu-id="0d546-130">GET</span></span> | <span data-ttu-id="0d546-131">Permite solo toobe de métodos HTTP seleccionado utiliza tooinvoke esta función</span><span class="sxs-lookup"><span data-stu-id="0d546-131">Allows only selected HTTP methods toobe used tooinvoke this function</span></span> |
| <span data-ttu-id="0d546-132">Plantilla de ruta</span><span class="sxs-lookup"><span data-stu-id="0d546-132">Route template</span></span> | <span data-ttu-id="0d546-133">/hello</span><span class="sxs-lookup"><span data-stu-id="0d546-133">/hello</span></span> | <span data-ttu-id="0d546-134">Determina qué ruta es tooinvoke usa esta función</span><span class="sxs-lookup"><span data-stu-id="0d546-134">Determines what route is used tooinvoke this function</span></span> |

<span data-ttu-id="0d546-135">Tenga en cuenta que no incluía hello `/api` base prefijo de ruta de acceso en la plantilla de ruta de hello, tal y como esto se controla mediante una configuración global.</span><span class="sxs-lookup"><span data-stu-id="0d546-135">Note that you did not include hello `/api` base path prefix in hello route template, as this is handled by a global setting.</span></span>

<span data-ttu-id="0d546-136">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0d546-136">Click **Save**.</span></span>

<span data-ttu-id="0d546-137">Puede aprender más sobre cómo personalizar funciones HTTP en [Enlaces HTTP y webhook en Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span><span class="sxs-lookup"><span data-stu-id="0d546-137">You can learn more about customizing HTTP functions in [Azure Functions HTTP and webhook bindings](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).</span></span>

### <a name="test-your-api"></a><span data-ttu-id="0d546-138">Prueba de la API</span><span class="sxs-lookup"><span data-stu-id="0d546-138">Test your API</span></span>

<span data-ttu-id="0d546-139">A continuación, pruebe su toosee de función que funcione con la nueva superficie de la API de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-139">Next, test your function toosee it working with hello new API surface.</span></span>

<span data-ttu-id="0d546-140">Explorar la página de desarrollo de toohello atrás haciendo clic en el nombre de la función de Hola Hola barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="0d546-140">Navigate back toohello development page by clicking on hello function's name in hello left navigation.</span></span>

<span data-ttu-id="0d546-141">Haga clic en **obtener dirección URL de la función** y copie la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-141">Click **Get function URL** and copy hello URL.</span></span> <span data-ttu-id="0d546-142">Debería ver que usa hello `/api/hello` enrutar ahora.</span><span class="sxs-lookup"><span data-stu-id="0d546-142">You should see that it uses hello `/api/hello` route now.</span></span>

<span data-ttu-id="0d546-143">Copiar dirección URL de hello en una nueva pestaña del explorador o el cliente REST preferido.</span><span class="sxs-lookup"><span data-stu-id="0d546-143">Copy hello URL into a new browser tab or your preferred REST client.</span></span> <span data-ttu-id="0d546-144">Los exploradores utilizarán GET de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0d546-144">Browsers will use GET by default.</span></span>

<span data-ttu-id="0d546-145">Ejecute la función hello y confirme que se está trabajando.</span><span class="sxs-lookup"><span data-stu-id="0d546-145">Run hello function and confirm that it is working.</span></span> <span data-ttu-id="0d546-146">Puede que tenga parámetros de "nombre" hello tooprovide como un código de inicio rápido de consulta cadena toosatisfy Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-146">You may need tooprovide hello "name" parameter as a query string toosatisfy hello quickstart code.</span></span>

<span data-ttu-id="0d546-147">También puede intentar llamar a un extremo de hello con otro tooconfirm de método HTTP que no se ejecuta la función de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-147">You can also try calling hello endpoint with another HTTP method tooconfirm that hello function is not executed.</span></span> <span data-ttu-id="0d546-148">Para ello, deberá toouse un cliente REST, como cURL, Postman o Fiddler.</span><span class="sxs-lookup"><span data-stu-id="0d546-148">For this, you will need toouse a REST client, such as cURL, Postman, or Fiddler.</span></span>

## <a name="proxies-overview"></a><span data-ttu-id="0d546-149">Introducción a Servidores proxy</span><span class="sxs-lookup"><span data-stu-id="0d546-149">Proxies overview</span></span>

<span data-ttu-id="0d546-150">En la siguiente sección hello, mostrará la API a través de un servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="0d546-150">In hello next section, you will surface your API through a proxy.</span></span> <span data-ttu-id="0d546-151">Servidores proxy de funciones de Azure es una característica de vista previa que le permite tooforward solicitudes tooother recursos.</span><span class="sxs-lookup"><span data-stu-id="0d546-151">Azure Functions Proxies is a preview feature that allows you tooforward requests tooother resources.</span></span> <span data-ttu-id="0d546-152">Definir un extremo HTTP igual que con el desencadenador HTTP, pero en lugar de escribir código tooexecute cuando se llama a ese punto de conexión, se proporciona una implementación remota de tooa de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="0d546-152">You define an HTTP endpoint just like with HTTP trigger, but instead of writing code tooexecute when that endpoint is called, you provide a URL tooa remote implementation.</span></span> <span data-ttu-id="0d546-153">Esto le permite toocompose API varios orígenes en una superficie de API única que es fácil que los clientes tooconsume.</span><span class="sxs-lookup"><span data-stu-id="0d546-153">This allows you toocompose multiple API sources into a single API surface which is easy for clients tooconsume.</span></span> <span data-ttu-id="0d546-154">Esto es especialmente útil si desea toobuild su API como microservicios.</span><span class="sxs-lookup"><span data-stu-id="0d546-154">This is particularly useful if you wish toobuild your API as microservices.</span></span>

<span data-ttu-id="0d546-155">Un servidor proxy puede apuntar recurso tooany HTTP, como:</span><span class="sxs-lookup"><span data-stu-id="0d546-155">A proxy can point tooany HTTP resource, such as:</span></span>
- <span data-ttu-id="0d546-156">Funciones de Azure</span><span class="sxs-lookup"><span data-stu-id="0d546-156">Azure Functions</span></span> 
- <span data-ttu-id="0d546-157">Aplicaciones de API en [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span><span class="sxs-lookup"><span data-stu-id="0d546-157">API apps in [Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)</span></span>
- <span data-ttu-id="0d546-158">Contenedores de Docker en [App Service en Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span><span class="sxs-lookup"><span data-stu-id="0d546-158">Docker containers in [App Service on Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme)</span></span>
- <span data-ttu-id="0d546-159">Cualquier otra API hospedada</span><span class="sxs-lookup"><span data-stu-id="0d546-159">Any other hosted API</span></span>

<span data-ttu-id="0d546-160">toolearn más información acerca de los servidores proxy, consulte [trabajar con servidores proxy de las funciones de Azure (vista previa)].</span><span class="sxs-lookup"><span data-stu-id="0d546-160">toolearn more about proxies, see [Working with Azure Functions Proxies (preview)].</span></span>

## <a name="create-your-first-proxy"></a><span data-ttu-id="0d546-161">Creación de su primer proxy</span><span class="sxs-lookup"><span data-stu-id="0d546-161">Create your first proxy</span></span>

<span data-ttu-id="0d546-162">En esta sección, creará un nuevo proxy que actúa como un servidor front-end tooyour API general.</span><span class="sxs-lookup"><span data-stu-id="0d546-162">In this section, you will create a new proxy which serves as a frontend tooyour overall API.</span></span> 

### <a name="setting-up-hello-frontend-environment"></a><span data-ttu-id="0d546-163">Configuración de entorno de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="0d546-163">Setting up hello frontend environment</span></span>

<span data-ttu-id="0d546-164">Repita los pasos de hello demasiado[crear una aplicación de la función](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate una nueva aplicación de función en la que va a crear el proxy.</span><span class="sxs-lookup"><span data-stu-id="0d546-164">Repeat hello steps too[Create a function app](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate a new function app in which you will create your proxy.</span></span> <span data-ttu-id="0d546-165">Esta nueva aplicación servirá como front-end de Hola para nuestra API y aplicación de función hello que estaba editando previamente actuará como un back-end.</span><span class="sxs-lookup"><span data-stu-id="0d546-165">This new app will serve as hello frontend for our API, and hello function app you were previously editing will serve as a backend.</span></span>

<span data-ttu-id="0d546-166">Navegue tooyour nueva aplicación de función de front-end en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-166">Navigate tooyour new frontend function app in hello portal.</span></span>

<span data-ttu-id="0d546-167">Seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="0d546-167">Select **Settings**.</span></span> <span data-ttu-id="0d546-168">A continuación, activar o desactivar **Habilitar proxy de funciones de Azure (vista previa)** demasiado "On".</span><span class="sxs-lookup"><span data-stu-id="0d546-168">Then toggle **Enable Azure Functions Proxies (preview)** too"On".</span></span>

<span data-ttu-id="0d546-169">Seleccione **Configuración de plataforma** y elija **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0d546-169">Select **Platform Settings** and choose **Application Settings**.</span></span>

<span data-ttu-id="0d546-170">Desplácese hacia abajo demasiado**configuración de la aplicación** y crear una nueva configuración con la clave "HELLO_HOST".</span><span class="sxs-lookup"><span data-stu-id="0d546-170">Scroll down too**App settings** and create a new setting with key "HELLO_HOST".</span></span> <span data-ttu-id="0d546-171">Establezca su valor toohello de host de la aplicación de función de back-end, como `<YourApp>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0d546-171">Set its value toohello host of your backend function app, such as `<YourApp>.azurewebsites.net`.</span></span> <span data-ttu-id="0d546-172">Esto forma parte de la dirección URL de Hola que copió anteriormente al probar la función HTTP.</span><span class="sxs-lookup"><span data-stu-id="0d546-172">This is part of hello URL that you copied earlier when testing your HTTP function.</span></span> <span data-ttu-id="0d546-173">Podrá hacer referencia a esta configuración en la configuración de hello más tarde.</span><span class="sxs-lookup"><span data-stu-id="0d546-173">You'll reference this setting in hello configuration later.</span></span>

> [!NOTE] 
> <span data-ttu-id="0d546-174">Configuración de la aplicación se recomienda para tooprevent de configuración de host de hello una dependencia codificada de forma rígida entorno para el proxy de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-174">App settings are recommended for hello host configuration tooprevent a hard-coded environment dependency for hello proxy.</span></span> <span data-ttu-id="0d546-175">Con la configuración de aplicación significa que puede mover la configuración de proxy de hello entre entornos, y se aplicará la configuración de la aplicación específica del entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-175">Using app settings means that you can move hello proxy configuration between environments, and hello environment-specific app settings will be applied.</span></span>

<span data-ttu-id="0d546-176">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0d546-176">Click **Save**.</span></span>

### <a name="creating-a-proxy-on-hello-frontend"></a><span data-ttu-id="0d546-177">Crear a un proxy en hello front-end</span><span class="sxs-lookup"><span data-stu-id="0d546-177">Creating a proxy on hello frontend</span></span>

<span data-ttu-id="0d546-178">Navegue tooyour atrás front-end función aplicación de portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-178">Navigate back tooyour frontend function app in hello portal.</span></span>

<span data-ttu-id="0d546-179">En el panel de navegación izquierdo hello, haga clic en hello signo '+' siguiente demasiado "Servidores proxy (vista previa)".</span><span class="sxs-lookup"><span data-stu-id="0d546-179">In hello left-hand navigation, click hello plus sign '+' next too"Proxies (preview)".</span></span>

![Creación de un proxy](./media/functions-create-serverless-api/creating-proxy.png)

<span data-ttu-id="0d546-181">Usar configuración de proxy como se especifica en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-181">Use proxy settings as specified in hello table.</span></span>

| <span data-ttu-id="0d546-182">Campo</span><span class="sxs-lookup"><span data-stu-id="0d546-182">Field</span></span> | <span data-ttu-id="0d546-183">Valor de ejemplo</span><span class="sxs-lookup"><span data-stu-id="0d546-183">Sample value</span></span> | <span data-ttu-id="0d546-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="0d546-184">Description</span></span> |
|---|---|---|
| <span data-ttu-id="0d546-185">Nombre</span><span class="sxs-lookup"><span data-stu-id="0d546-185">Name</span></span> | <span data-ttu-id="0d546-186">HelloProxy</span><span class="sxs-lookup"><span data-stu-id="0d546-186">HelloProxy</span></span> | <span data-ttu-id="0d546-187">Un nombre descriptivo que se usa solo para la administración</span><span class="sxs-lookup"><span data-stu-id="0d546-187">A friendly name used only for management</span></span> |
| <span data-ttu-id="0d546-188">Plantilla de ruta</span><span class="sxs-lookup"><span data-stu-id="0d546-188">Route template</span></span> | <span data-ttu-id="0d546-189">/api/hello</span><span class="sxs-lookup"><span data-stu-id="0d546-189">/api/hello</span></span> | <span data-ttu-id="0d546-190">Determina qué ruta es tooinvoke usado este proxy</span><span class="sxs-lookup"><span data-stu-id="0d546-190">Determines what route is used tooinvoke this proxy</span></span> |
| <span data-ttu-id="0d546-191">Dirección URL de back-end</span><span class="sxs-lookup"><span data-stu-id="0d546-191">Backend URL</span></span> | <span data-ttu-id="0d546-192">https://%HELLO_HOST%/api/hello</span><span class="sxs-lookup"><span data-stu-id="0d546-192">https://%HELLO_HOST%/api/hello</span></span> | <span data-ttu-id="0d546-193">Especifica la solicitud de hello extremo toowhich Hola debe ser procesadas por el proxy</span><span class="sxs-lookup"><span data-stu-id="0d546-193">Specifies hello endpoint toowhich hello request should be proxied</span></span> |

<span data-ttu-id="0d546-194">Tenga en cuenta que los servidores proxy no proporciona hello `/api` prefijo de ruta de acceso base y debe incluirse en la plantilla de ruta de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-194">Note that Proxies does not provide hello `/api` base path prefix, and this must be included in hello route template.</span></span>

<span data-ttu-id="0d546-195">Hola `%HELLO_HOST%` sintaxis hará referencia a configuración de la aplicación hello que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0d546-195">hello `%HELLO_HOST%` syntax will reference hello app setting you created earlier.</span></span> <span data-ttu-id="0d546-196">Hola resuelve la que dirección URL señala tooyour de función original.</span><span class="sxs-lookup"><span data-stu-id="0d546-196">hello resolved URL will point tooyour original function.</span></span>

<span data-ttu-id="0d546-197">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0d546-197">Click **Create**.</span></span>

<span data-ttu-id="0d546-198">Puede probar el nuevo proxy copiando Hola dirección URL del Proxy y probarlo en el Explorador de Hola o con el cliente HTTP favorito.</span><span class="sxs-lookup"><span data-stu-id="0d546-198">You can try out your new proxy by copying hello Proxy URL and testing it in hello browser or with your favorite HTTP client.</span></span>

## <a name="create-a-mock-api"></a><span data-ttu-id="0d546-199">Creación de una API simulada</span><span class="sxs-lookup"><span data-stu-id="0d546-199">Create a mock API</span></span>

<span data-ttu-id="0d546-200">A continuación, usará un toocreate una API ficticia de proxy para la solución.</span><span class="sxs-lookup"><span data-stu-id="0d546-200">Next, you will use a proxy toocreate a mock API for your solution.</span></span> <span data-ttu-id="0d546-201">Esto permite el desarrollo de cliente tooprogress, sin necesidad de back-end de hello totalmente implementada.</span><span class="sxs-lookup"><span data-stu-id="0d546-201">This allows client development tooprogress, without needing hello backend fully implemented.</span></span> <span data-ttu-id="0d546-202">Más adelante en el desarrollo, puede crear una nueva aplicación de función que admite esta lógica y redirigir el tooit de proxy.</span><span class="sxs-lookup"><span data-stu-id="0d546-202">Later in development, you could create a new function app which supports this logic and redirect your proxy tooit.</span></span>

<span data-ttu-id="0d546-203">toocreate este ejemplo de API, se creará un nuevo proxy, esta vez utilizando hello [Editor de aplicación de servicio](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span><span class="sxs-lookup"><span data-stu-id="0d546-203">toocreate this mock API, we will create a new proxy, this time using hello [App Service Editor](https://github.com/projectkudu/kudu/wiki/App-Service-Editor).</span></span> <span data-ttu-id="0d546-204">tooget iniciado, navegue tooyour función aplicación de portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-204">tooget started, navigate tooyour function app in hello portal.</span></span> <span data-ttu-id="0d546-205">Seleccione **Características de la plataforma** y busque **Editor de App Service**.</span><span class="sxs-lookup"><span data-stu-id="0d546-205">Select **Platform features** and find **App Service Editor**.</span></span> <span data-ttu-id="0d546-206">Al hacer clic en este se abrirá Hola Editor de aplicación de servicio en una nueva pestaña.</span><span class="sxs-lookup"><span data-stu-id="0d546-206">Clicking this will open hello App Service Editor in a new tab.</span></span>

<span data-ttu-id="0d546-207">Seleccione `proxies.json` Hola barra de navegación izquierda.</span><span class="sxs-lookup"><span data-stu-id="0d546-207">Select `proxies.json` in hello left navigation.</span></span> <span data-ttu-id="0d546-208">Se trata de un archivo hello que almacena la configuración de Hola de todos los servidores proxy.</span><span class="sxs-lookup"><span data-stu-id="0d546-208">This is hello file which stores hello configuration for all of your proxies.</span></span> <span data-ttu-id="0d546-209">Si utiliza uno de hello [las funciones de métodos de implementación](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), se trata de archivo hello mantendrá en control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="0d546-209">If you use one of hello [Functions deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), this is hello file you will maintain in source control.</span></span> <span data-ttu-id="0d546-210">toolearn más información acerca de este archivo, consulte [configuración avanzada de servidores proxy](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span><span class="sxs-lookup"><span data-stu-id="0d546-210">toolearn more about this file, see [Proxies advanced configuration](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).</span></span>

<span data-ttu-id="0d546-211">Si ha seguido estos pasos hasta ahora, su proxies.json debería ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="0d546-211">If you've followed along so far, your proxies.json should look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

<span data-ttu-id="0d546-212">A continuación, va a agregar su API simulada.</span><span class="sxs-lookup"><span data-stu-id="0d546-212">Next you'll add your mock API.</span></span> <span data-ttu-id="0d546-213">Reemplace el archivo proxies.json con hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="0d546-213">Replace your proxies.json file with hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

<span data-ttu-id="0d546-214">Esto agrega a un nuevo proxy, "GetUserByName", sin una propiedad backendUri Hola.</span><span class="sxs-lookup"><span data-stu-id="0d546-214">This adds a new proxy, "GetUserByName", without hello backendUri property.</span></span> <span data-ttu-id="0d546-215">En lugar de llamar a otro recurso, modifica la respuesta predeterminada de Hola de servidores proxy mediante una invalidación de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="0d546-215">Instead of calling another resource, it modifies hello default response from Proxies using a response override.</span></span> <span data-ttu-id="0d546-216">Las invalidaciones de solicitud y respuesta también pueden utilizarse junto con una dirección URL de back-end.</span><span class="sxs-lookup"><span data-stu-id="0d546-216">Request and response overrides can also be used in conjunction with a backend URL.</span></span> <span data-ttu-id="0d546-217">Esto es especialmente útil cuando un proxy tooa heredado system, que podrían necesitar toomodify encabezados, parámetros de consulta, etc. toolearn más acerca de las invalidaciones de solicitud y respuesta, vea [modificar las solicitudes y respuestas en los Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span><span class="sxs-lookup"><span data-stu-id="0d546-217">This is particularly useful when proxying tooa legacy system, where you might need toomodify headers, query parameters, etc. toolearn more about request and response overrides, see [Modifying requests and responses in Proxies](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).</span></span>

<span data-ttu-id="0d546-218">Probar la API ficticia llamada Hola `/api/users/{username}` punto de conexión mediante un explorador o el cliente REST favoritos.</span><span class="sxs-lookup"><span data-stu-id="0d546-218">Test your mock API by calling hello `/api/users/{username}` endpoint using a browser or your favorite REST client.</span></span> <span data-ttu-id="0d546-219">Ser seguro tooreplace _{username}_ con un valor de cadena que representa un nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="0d546-219">Be sure tooreplace _{username}_ with a string value representing a username.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d546-220">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0d546-220">Next steps</span></span>

<span data-ttu-id="0d546-221">En este tutorial, se habrá aprendido cómo toobuild y personalizar una API en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d546-221">In this tutorial, you learned how toobuild and customize an API on Azure Functions.</span></span> <span data-ttu-id="0d546-222">También ha aprendido cómo toobring varias API, incluidos mocks, juntos como una superficie de API unificada.</span><span class="sxs-lookup"><span data-stu-id="0d546-222">You also learned how toobring multiple APIs, including mocks, together as a unified API surface.</span></span> <span data-ttu-id="0d546-223">Puede usar estos toobuild técnicas a las API de cualquier complejidad, todos los mientras se ejecutan en hello sin servidor de proceso modelo que proporcionan funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="0d546-223">You can use these techniques toobuild out APIs of any complexity, all while running on hello serverless compute model provided by Azure Functions.</span></span>

<span data-ttu-id="0d546-224">Hello las referencias siguientes pueden serle de ayuda a medida que desarrolla su API adicional:</span><span class="sxs-lookup"><span data-stu-id="0d546-224">hello following references may be helpful as you develop your API further:</span></span>

- [<span data-ttu-id="0d546-225">Enlaces HTTP y webhook en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0d546-225">Azure Functions HTTP and webhook bindings</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- <span data-ttu-id="0d546-226">[trabajar con servidores proxy de las funciones de Azure (vista previa)]</span><span class="sxs-lookup"><span data-stu-id="0d546-226">[Working with Azure Functions Proxies (preview)]</span></span>
- [<span data-ttu-id="0d546-227">Documentación de una API de Azure Functions (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="0d546-227">Documenting an Azure Functions API (preview)</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[trabajar con servidores proxy de las funciones de Azure (vista previa)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
