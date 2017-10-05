---
title: Desencadenadores de aplicaciones de API de App Service | Microsoft Docs
description: "Cómo implementar desencadenadores en una aplicación de API del Servicio de aplicaciones de Azure"
services: logic-apps
documentationcenter: .net
author: guangyang
manager: erikre
editor: jimbe
ms.assetid: 493c3703-786d-4434-9dca-8f77744b2f5d
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/25/2016
ms.author: rachelap
ms.openlocfilehash: 3ddfb142e7f1a47e2a8564387da785acf36fa61f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="c1bc8-103">Desencadenadores de aplicación de API del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c1bc8-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="c1bc8-104">Esta versión del artículo se aplica a la versión de esquema 2014-12-01-preview de las aplicaciones de API.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-104">This version of the article applies to API apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="c1bc8-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c1bc8-105">Overview</span></span>
<span data-ttu-id="c1bc8-106">En este artículo, se explica cómo implementar desencadenadores de aplicación de API y consumirlos desde una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-106">This article explains how to implement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="c1bc8-107">Todos los fragmentos de código de este tema proceden del [ejemplo de código de la aplicación de API FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="c1bc8-107">All of the code snippets in this topic are copied from the [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="c1bc8-108">Tenga en cuenta que tendrá que descargar el siguiente paquete de NuGet para el código en este artículo para realizar la compilación y ejecución: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="c1bc8-108">Note that you'll need to download the following nuget package for the code in this article to build and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="c1bc8-109">¿Qué son los desencadenadores de aplicación de API?</span><span class="sxs-lookup"><span data-stu-id="c1bc8-109">What are API app triggers?</span></span>
<span data-ttu-id="c1bc8-110">Es frecuente que una aplicación de API deba desencadenar un evento de forma que los clientes de la aplicación de API realicen la acción apropiada como respuesta al evento.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-110">It's a common scenario for an API app to fire an event so that clients of the API app can take the appropriate action in response to the event.</span></span> <span data-ttu-id="c1bc8-111">El mecanismo basado en la API de REST que hace posible este escenario se denomina "desencadenador de aplicación de API".</span><span class="sxs-lookup"><span data-stu-id="c1bc8-111">The REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="c1bc8-112">Por ejemplo, supongamos que el código de su cliente utiliza la [aplicación API de conector de Twitter](../connectors/connectors-create-api-twitter.md) , y el código necesita realizar una acción basada en nuevos tweets que contengan palabras específicas.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-112">For example, let's say your client code is using the [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs to perform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="c1bc8-113">En este caso, puede configurar un desencadenador de inserción o de extracción para facilitar esta tarea.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-113">In this case, you might set up a poll or push trigger to facilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="c1bc8-114">Desencadenador de sondeo frente a desencadenador de inserción</span><span class="sxs-lookup"><span data-stu-id="c1bc8-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="c1bc8-115">Actualmente, se admiten dos tipos de desencadenadores:</span><span class="sxs-lookup"><span data-stu-id="c1bc8-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="c1bc8-116">Desencadenador de sondeo: el cliente sondea la aplicación de API para la notificación de un evento que se ha activado.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-116">Poll trigger - Client polls the API app for notification of an event having been fired</span></span>
* <span data-ttu-id="c1bc8-117">Desencadenador de inserción: se notifica al cliente mediante la aplicación de API cuando se activa un evento.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-117">Push trigger - Client is notified by the API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="c1bc8-118">Desencadenador de sondeo</span><span class="sxs-lookup"><span data-stu-id="c1bc8-118">Poll trigger</span></span>
<span data-ttu-id="c1bc8-119">Un desencadenador de sondeo se implementa como una API de REST normal y espera que sus clientes (por ejemplo, una aplicación lógica) efectúen un sondeo para obtener notificaciones.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) to poll it in order to get notification.</span></span> <span data-ttu-id="c1bc8-120">El cliente puede conservar el estado, pero desencadenador de sondeo en sí no tiene estado.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-120">While the client may maintain state, the poll trigger itself is stateless.</span></span>

<span data-ttu-id="c1bc8-121">En la información siguiente sobre los paquetes de solicitud y respuesta, se ilustran algunos aspectos claves del contrato del desencadenador de sondeo:</span><span class="sxs-lookup"><span data-stu-id="c1bc8-121">The following information regarding the request and response packets illustrate some key aspects of the poll trigger contract:</span></span>

* <span data-ttu-id="c1bc8-122">Solicitud</span><span class="sxs-lookup"><span data-stu-id="c1bc8-122">Request</span></span>
  * <span data-ttu-id="c1bc8-123">Método HTTP: GET</span><span class="sxs-lookup"><span data-stu-id="c1bc8-123">HTTP method: GET</span></span>
  * <span data-ttu-id="c1bc8-124">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c1bc8-124">Parameters</span></span>
    * <span data-ttu-id="c1bc8-125">triggerState: este parámetro opcional permite a los clientes especificar su estado para que el desencadenador de sondeo pueda decidir correctamente si debe devolver la notificación o no según el estado especificado.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-125">triggerState - This optional parameter allows clients to specify their state so that the poll trigger can properly decide whether to return notification or not based on the specified state.</span></span>
    * <span data-ttu-id="c1bc8-126">Parámetros específicos de la API</span><span class="sxs-lookup"><span data-stu-id="c1bc8-126">API-specific parameters</span></span>
* <span data-ttu-id="c1bc8-127">Response</span><span class="sxs-lookup"><span data-stu-id="c1bc8-127">Response</span></span>
  * <span data-ttu-id="c1bc8-128">Código de estado **200** : la solicitud es válida y hay una notificación desde el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-128">Status code **200** - Request is valid and there is a notification from the trigger.</span></span> <span data-ttu-id="c1bc8-129">El contenido de la notificación será el cuerpo de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-129">The content of the notification will be the response body.</span></span> <span data-ttu-id="c1bc8-130">El encabezado "Retry-After" en la respuesta indica que hay que recuperar datos de notificación adicionales con una llamada de solicitud posterior.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-130">A "Retry-After" header in the response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="c1bc8-131">Código de estado **202** : la solicitud es válida, pero no hay una notificación nueva desde el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-131">Status code **202** - Request is valid, but there is no new notification from the trigger.</span></span>
  * <span data-ttu-id="c1bc8-132">Código de estado **4xx** : la solicitud no es válida.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="c1bc8-133">El cliente no debe intentar efectuar la solicitud de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-133">The client should not retry the request.</span></span>
  * <span data-ttu-id="c1bc8-134">Código de estado **5xx** : la solicitud ha producido un error interno en el servidor o un problema temporal.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="c1bc8-135">El cliente debe intentar efectuar la solicitud de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-135">The client should retry the request.</span></span>

<span data-ttu-id="c1bc8-136">El siguiente fragmento de código es un ejemplo de cómo se debe implementar un desencadenador de sondeo.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-136">The following code snippet is an example of how to implement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check to see whether there is any file touched after the timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after the timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after the timestamp, tell the caller to poll again after 1 mintue.
        else
        {
            // Extension method provided by the AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="c1bc8-137">Para probar este desencadenador de sondeo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c1bc8-137">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="c1bc8-138">Implemente la aplicación de API con una configuración de autenticación de **anónimo público**.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-138">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="c1bc8-139">Ejecute la operación **touch** para tocar un archivo.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-139">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="c1bc8-140">La siguiente imagen muestra una solicitud de ejemplo a través de Postman.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-140">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="c1bc8-141">![Llamada a la operación Touch mediante Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="c1bc8-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="c1bc8-142">Efectúe una llamada al desencadenador de sondeo con el parámetro **triggerState** establecido en una marca de tiempo anterior al paso 2.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-142">Call the poll trigger with the **triggerState** parameter set to a time stamp prior to Step #2.</span></span> <span data-ttu-id="c1bc8-143">La siguiente imagen muestra la solicitud de ejemplo a través de Postman.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-143">The following image shows the sample request via Postman.</span></span>
   <span data-ttu-id="c1bc8-144">![Llamada al desencadenador de sondeo mediante Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="c1bc8-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="c1bc8-145">Desencadenador de inserción</span><span class="sxs-lookup"><span data-stu-id="c1bc8-145">Push trigger</span></span>
<span data-ttu-id="c1bc8-146">Un desencadenador de inserción se implementa como una API de REST normal que envía notificaciones a los clientes que se han registrado para recibir notificaciones cuando se activan determinados eventos.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-146">A push trigger is implemented as a regular REST API that pushes notifications to clients who have registered to be notified when specific events fire.</span></span>

<span data-ttu-id="c1bc8-147">En la información siguiente sobre los paquetes de solicitud y respuesta, se ilustran algunos aspectos claves del contrato del desencadenador de inserción.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-147">The following information regarding the request and response packets illustrate some key aspects of the push trigger contract.</span></span>

* <span data-ttu-id="c1bc8-148">Solicitud</span><span class="sxs-lookup"><span data-stu-id="c1bc8-148">Request</span></span>
  * <span data-ttu-id="c1bc8-149">Método HTTP: PUT</span><span class="sxs-lookup"><span data-stu-id="c1bc8-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="c1bc8-150">Parámetros</span><span class="sxs-lookup"><span data-stu-id="c1bc8-150">Parameters</span></span>
    * <span data-ttu-id="c1bc8-151">triggerId: (obligatorio) cadena opaca (por ejemplo, un GUID) que representa el registro de un desencadenador de inserción.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-151">triggerId: required - Opaque string (such as a GUID) that represents the registration of a push trigger.</span></span>
    * <span data-ttu-id="c1bc8-152">callbackUrl: (obligatorio) dirección URL de la devolución de llamada que se ejecuta al activarse el evento.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-152">callbackUrl: required - URL of the callback to invoke when the event fires.</span></span> <span data-ttu-id="c1bc8-153">La ejecución es una llamada HTTP POST simple.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-153">The invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="c1bc8-154">Parámetros específicos de la API</span><span class="sxs-lookup"><span data-stu-id="c1bc8-154">API-specific parameters</span></span>
* <span data-ttu-id="c1bc8-155">Response</span><span class="sxs-lookup"><span data-stu-id="c1bc8-155">Response</span></span>
  * <span data-ttu-id="c1bc8-156">Código de estado **200** : solicitud de registro de cliente correcta.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-156">Status code **200** - Request to register client successful.</span></span>
  * <span data-ttu-id="c1bc8-157">Código de estado **4xx** : la solicitud no es válida.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="c1bc8-158">El cliente no debe intentar efectuar la solicitud de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-158">The client should not retry the request.</span></span>
  * <span data-ttu-id="c1bc8-159">Código de estado **5xx** : la solicitud ha producido un error interno en el servidor o un problema temporal.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="c1bc8-160">El cliente debe intentar efectuar la solicitud de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-160">The client should retry the request.</span></span>
* <span data-ttu-id="c1bc8-161">Devolución de llamada</span><span class="sxs-lookup"><span data-stu-id="c1bc8-161">Callback</span></span>
  * <span data-ttu-id="c1bc8-162">Método HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="c1bc8-162">HTTP method: POST</span></span>
  * <span data-ttu-id="c1bc8-163">Cuerpo de la solicitud: contenido de la notificación.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-163">Request body: Notification content.</span></span>

<span data-ttu-id="c1bc8-164">El siguiente fragmento de código es un ejemplo de cómo se debe implementar un desencadenador de inserción.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-164">The following code snippet is an example of how to implement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by the AppService service SDK.
        // Here it defines the input of the push trigger is a string and the output to the callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register the trigger to some trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by the AppService service SDK indicating the registration is completed.
        return this.Request.PushTriggerRegistered(triggerInput.GetCallback());
    }

    // A simple in-memory trigger store.
    public class InMemoryTriggerStore
    {
        private static InMemoryTriggerStore instance;

        private IDictionary<string, FileSystemWatcher> _store;

        private InMemoryTriggerStore()
        {
            _store = new Dictionary<string, FileSystemWatcher>();
        }

        public static InMemoryTriggerStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new InMemoryTriggerStore();
                }
                return instance;
            }
        }

        // Register a push trigger.
        public void RegisterTrigger(string triggerId, string rootPath,
            TriggerInput<string, FileInfoWrapper> triggerInput)
        {
            // Use FileSystemWatcher to listen to file change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire the push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate the FileSystemWatcher object with the triggerId.
            _store[triggerId] = watcher;

        }

        // Fire the assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed to invoke the callback.
            Runtime runtime,
            // The callback to invoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK to invoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="c1bc8-165">Para probar este desencadenador de sondeo, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c1bc8-165">To test this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="c1bc8-166">Implemente la aplicación de API con una configuración de autenticación de **anónimo público**.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-166">Deploy the API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="c1bc8-167">Vaya a [http://requestb.in/](http://requestb.in/) para crear un RequestBin que servirá como dirección URL de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-167">Browse to [http://requestb.in/](http://requestb.in/) to create a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="c1bc8-168">Ejecute una llamada al desencadenador de push con un GUID como **triggerId** y la dirección URL de RequestBin como **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-168">Call the push trigger with a GUID as **triggerId** and the RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="c1bc8-169">![Llamada al desencadenador de inserción mediante Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="c1bc8-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="c1bc8-170">Ejecute la operación **touch** para tocar un archivo.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-170">Call the **touch** operation to touch a file.</span></span> <span data-ttu-id="c1bc8-171">La siguiente imagen muestra una solicitud de ejemplo a través de Postman.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-171">The following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="c1bc8-172">![Llamada a la operación Touch mediante Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="c1bc8-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="c1bc8-173">Compruebe el RequestBin para confirmar que la devolución de llamada del desencadenador de inserción se realiza con una salida de propiedad.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-173">Check the RequestBin to confirm that the push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="c1bc8-174">![Llamada al desencadenador de sondeo mediante Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="c1bc8-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="c1bc8-175">Descripción de los desencadenadores en la definición de la API</span><span class="sxs-lookup"><span data-stu-id="c1bc8-175">Describe triggers in API definition</span></span>
<span data-ttu-id="c1bc8-176">Después de implementar los desencadenadores e implementar la aplicación de API en Azure, vaya a la hoja **Definición de la API** en el portal de vista previa de Azure. Verá que los desencadenadores se reconocen automáticamente en la interfaz de usuario, que se controla mediante la definición de la API Swagger 2.0 de la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-176">After implementing the triggers and deploying your API app to Azure, navigate to the **API Definition** blade in the Azure preview portal and you'll see that triggers are automatically recognized in the UI, which is driven by the Swagger 2.0 API definition of the API app.</span></span>

![Hoja de definición de la API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="c1bc8-178">Si hace clic en el botón para **Descargar Swagger** y abra el archivo JSONj. Verá resultados similares a los siguientes:</span><span class="sxs-lookup"><span data-stu-id="c1bc8-178">If you click the **Download Swagger** button and open the JSON file, you'll see results similar to the following:</span></span>

    "/api/files/poll/TouchedFiles": {
      "get": {
        "operationId": "Files_TouchedFilesPollTrigger",
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    },
    "/api/files/push/TouchedFiles/{triggerId}": {
      "put": {
        "operationId": "Files_TouchedFilesPushTrigger",
        ...
        "x-ms-scheduler-trigger": "push"
      }
    }

<span data-ttu-id="c1bc8-179">La propiedad de extensión **x-ms-schedular-trigger** representa la forma en que los desencadenadores se han descrito en la definición de la API. Esta propiedad la agrega automáticamente la puerta de enlace de la aplicación de API cuando se solicita la definición de la API a través de la puerta de enlace, si la solicitud se ajusta a uno de los siguientes criterios.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-179">The extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by the API app gateway when you request the API definition via the gateway if the request to one of the following criteria.</span></span> <span data-ttu-id="c1bc8-180">(También puede agregar esta propiedad manualmente).</span><span class="sxs-lookup"><span data-stu-id="c1bc8-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="c1bc8-181">Desencadenador de sondeo</span><span class="sxs-lookup"><span data-stu-id="c1bc8-181">Poll trigger</span></span>
  * <span data-ttu-id="c1bc8-182">Si el método HTTP es **GET**.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-182">If the HTTP method is **GET**.</span></span>
  * <span data-ttu-id="c1bc8-183">Si la propiedad **operationId** contiene la cadena **trigger**.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-183">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="c1bc8-184">Si la propiedad **parameters** incluye un parámetro con una propiedad **name** establecida en **triggerState**.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-184">If the **parameters** property includes a parameter with a **name** property set to **triggerState**.</span></span>
* <span data-ttu-id="c1bc8-185">Desencadenador de inserción</span><span class="sxs-lookup"><span data-stu-id="c1bc8-185">Push trigger</span></span>
  * <span data-ttu-id="c1bc8-186">Si el método HTTP es **PUT**.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-186">If the HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="c1bc8-187">Si la propiedad **operationId** contiene la cadena **trigger**.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-187">If the **operationId** property contains the string **trigger**.</span></span>
  * <span data-ttu-id="c1bc8-188">Si la propiedad **parameters** incluye un parámetro con una propiedad **name** establecida en **triggerId**.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-188">If the **parameters** property includes a parameter with a **name** property set to **triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="c1bc8-189">Uso de desencadenadores de la aplicación de API en aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="c1bc8-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-the-logic-apps-designer"></a><span data-ttu-id="c1bc8-190">Muestre y configure desencadenadores de la aplicación de API en el Diseñador de aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="c1bc8-190">List and configure API app triggers in the Logic apps designer</span></span>
<span data-ttu-id="c1bc8-191">Si crea una aplicación lógica en el mismo grupo de recursos que la aplicación de API, podrá agregarla al lienzo del diseñador simplemente haciendo clic en ella.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-191">If you create a Logic app in the same resource group as the API app, you will be able to add it to the designer canvas simply by clicking it.</span></span> <span data-ttu-id="c1bc8-192">Las imágenes siguientes ilustran este proceso:</span><span class="sxs-lookup"><span data-stu-id="c1bc8-192">The following images illustrate this:</span></span>

![Desencadenadores en el Diseñador de aplicaciones lógicas](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configuración del desencadenador de sondeo en el Diseñador de aplicaciones lógicas](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configuración del desencadenador de inserción en el Diseñador de aplicaciones lógicas](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="c1bc8-196">Optimización de los desencadenadores de la aplicación de API para aplicaciones de lógicas</span><span class="sxs-lookup"><span data-stu-id="c1bc8-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="c1bc8-197">Después de agregar desencadenadores a una aplicación de API, hay algunas cosas que puede hacer para mejorar la experiencia al usar la aplicación de API en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-197">After you add triggers to an API app, there are a few things you can do to improve the experience when using the API app in a Logic app.</span></span>

<span data-ttu-id="c1bc8-198">Por ejemplo, el parámetro **triggerState** para los desencadenadores de sondeo se debe configurar con la siguiente expresión en la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-198">For instance, the **triggerState** parameter for poll triggers should be set to the following expression in the Logic app.</span></span> <span data-ttu-id="c1bc8-199">Esta expresión debe evaluar la última invocación del desencadenador desde la aplicación lógica y devolver ese valor.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-199">This expression should evaluate the last invocation of the trigger from the Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="c1bc8-200">NOTA: para obtener una explicación de las funciones utilizadas en la expresión anterior, consulte la documentación sobre el [lenguaje de definición del flujo de trabajo de la aplicación lógica](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1bc8-200">NOTE: For an explanation of the functions used in the expression above, refer to the documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="c1bc8-201">Los usuarios de la aplicación lógica deben proporcionar la expresión anterior para el parámetro **triggerState** mientras usan el desencadenador.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-201">Logic app users would need to provide the expression above for the **triggerState** parameter while using the trigger.</span></span> <span data-ttu-id="c1bc8-202">Este valor se puede preconfigurar en el diseñador de aplicaciones lógicas mediante la propiedad de extensión **x-ms-scheduler_recommendation**.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-202">It is possible to have this value preset by the Logic app designer through the extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="c1bc8-203">La propiedad de extensión **x-ms-visibility** se puede establecer en el valor *internal* , de modo que el propio parámetro no se muestre en el diseñador.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-203">The **x-ms-visibility** extension property can be set to a value of *internal* so that the parameter itself is not shown on the designer.</span></span>  <span data-ttu-id="c1bc8-204">El siguiente fragmento de código ilustra este hecho.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-204">The following snippet illustrates that.</span></span>

    "/api/Messages/poll": {
      "get": {
        "operationId": "Messages_NewMessageTrigger",
        "parameters": [
          {
            "name": "triggerState",
            "in": "query",
            "required": true,
            "x-ms-visibility": "internal",
            "x-ms-scheduler-recommendation": "@coalesce(triggers()?.outputs?.body?['triggerState'], '')",
            "type": "string"
          }
        ]
        ...
        "x-ms-scheduler-trigger": "poll"
      }
    }

<span data-ttu-id="c1bc8-205">Para los desencadenadores de inserción, el parámetro **triggerId** debe identificar de forma exclusiva la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-205">For push triggers, the **triggerId** parameter must uniquely identify the Logic app.</span></span> <span data-ttu-id="c1bc8-206">Una práctica recomendada consiste en establecer esta propiedad en el nombre del flujo de trabajo mediante la expresión siguiente:</span><span class="sxs-lookup"><span data-stu-id="c1bc8-206">A recommended best practice is to set this property to the name of the workflow by using the following expression:</span></span>

    @workflow().name

<span data-ttu-id="c1bc8-207">Mediante las propiedades de extensión **x-ms-scheduler-recommendation** y **x-ms-visibility** de la definición de la API, la aplicación de API puede indicar al diseñador de aplicaciones lógicas que configure automáticamente esta expresión para el usuario.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-207">Using the **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, the API app can convey to the Logic app designer to automatically set this expression for the user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="c1bc8-208">Adición de propiedades de extensión en la definición de la API</span><span class="sxs-lookup"><span data-stu-id="c1bc8-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="c1bc8-209">La información de metadatos adicionales (por ejemplo, las propiedades de extensión **x-ms-scheduler-recommendation** y **x-ms-visibility**) puede agregarse en la definición de la API de dos maneras: estática o dinámica.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-209">Additional metadata information - such as the extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in the API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="c1bc8-210">En el caso de los metadatos estáticos, puede editar directamente el archivo */metadata/apiDefinition.swagger.json* en el proyecto y agregar manualmente las propiedades.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-210">For static metadata, you can directly edit the */metadata/apiDefinition.swagger.json* file in your project and add the properties manually.</span></span>

<span data-ttu-id="c1bc8-211">Para las aplicaciones de API con metadatos dinámicos, puede editar el archivo SwaggerConfig.cs para agregar un filtro de operación que pueda agregar estas extensiones.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-211">For API apps using dynamic metadata, you can edit the SwaggerConfig.cs file to add an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="c1bc8-212">El siguiente es un ejemplo de cómo esta clase se puede implementar para facilitar el escenario de metadatos dinámicos.</span><span class="sxs-lookup"><span data-stu-id="c1bc8-212">The following is an example of how this class can be implemented to facilitate the dynamic metadata scenario.</span></span>

    // Add extension properties on the triggerState parameter
    public class TriggerStateFilter : IOperationFilter
    {

        public void Apply(Operation operation, SchemaRegistry schemaRegistry, System.Web.Http.Description.ApiDescription apiDescription)
        {
            if (operation.operationId.IndexOf("Trigger", StringComparison.InvariantCultureIgnoreCase) >= 0)
            {
                // this is a possible trigger
                var triggerStateParam = operation.parameters.FirstOrDefault(x => x.name.Equals("triggerState"));
                if (triggerStateParam != null)
                {
                    if (triggerStateParam.vendorExtensions == null)
                    {
                        triggerStateParam.vendorExtensions = new Dictionary<string, object>();
                    }

                    // add 2 vendor extensions
                    // x-ms-visibility: set to 'internal' to signify this is an internal field
                    // x-ms-scheduler-recommendation: set to a value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
