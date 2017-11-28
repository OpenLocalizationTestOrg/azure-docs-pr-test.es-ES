---
title: "desencadenadores de aplicación de API del servicio de aaaApp | Documentos de Microsoft"
description: "¿Cómo tooimplement desencadena en un App de API de servicio de aplicaciones de Azure"
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
ms.openlocfilehash: 2d6b6a942a23c0a93987e9c48b69ecc739bfd814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-api-app-triggers"></a><span data-ttu-id="c4141-103">Desencadenadores de aplicación de API del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="c4141-103">Azure App Service API app triggers</span></span>
> [!NOTE]
> <span data-ttu-id="c4141-104">Esta versión de artículo de Hola aplica la versión del esquema de tooAPI aplicaciones 2014-12-01-versión preliminar.</span><span class="sxs-lookup"><span data-stu-id="c4141-104">This version of hello article applies tooAPI apps 2014-12-01-preview schema version.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="c4141-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c4141-105">Overview</span></span>
<span data-ttu-id="c4141-106">Este artículo explica cómo tooimplement API aplicación desencadena y consumirlos desde una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="c4141-106">This article explains how tooimplement API app triggers and consume them from a Logic app.</span></span>

<span data-ttu-id="c4141-107">Todos los fragmentos de código de hello en este tema se copian de hello [ejemplo de código de aplicación de API de FileWatcher](http://go.microsoft.com/fwlink/?LinkId=534802).</span><span class="sxs-lookup"><span data-stu-id="c4141-107">All of hello code snippets in this topic are copied from hello [FileWatcher API App code sample](http://go.microsoft.com/fwlink/?LinkId=534802).</span></span>

<span data-ttu-id="c4141-108">Tenga en cuenta que necesitará Hola de toodownload siguiente paquete de nuget para el código de hello en este artículo toobuild y ejecute: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span><span class="sxs-lookup"><span data-stu-id="c4141-108">Note that you'll need toodownload hello following nuget package for hello code in this article toobuild and run: [http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service/).</span></span>

## <a name="what-are-api-app-triggers"></a><span data-ttu-id="c4141-109">¿Qué son los desencadenadores de aplicación de API?</span><span class="sxs-lookup"><span data-stu-id="c4141-109">What are API app triggers?</span></span>
<span data-ttu-id="c4141-110">Es un escenario común para una toofire de aplicación de API un evento para que los clientes de aplicación de API de hello pueden tomar medidas apropiadas de hello en el evento de respuesta toohello.</span><span class="sxs-lookup"><span data-stu-id="c4141-110">It's a common scenario for an API app toofire an event so that clients of hello API app can take hello appropriate action in response toohello event.</span></span> <span data-ttu-id="c4141-111">Hola mecanismo en función de API de REST que admite este escenario se llama a un desencadenador de aplicaciones de API.</span><span class="sxs-lookup"><span data-stu-id="c4141-111">hello REST API based mechanism that supports this scenario is called an API app trigger.</span></span>

<span data-ttu-id="c4141-112">Por ejemplo, supongamos que el código de cliente está usando hello [aplicación de API del conector de Twitter](../connectors/connectors-create-api-twitter.md) y el código necesita tooperform acción basándose en el nuevo tweets que contienen determinadas palabras.</span><span class="sxs-lookup"><span data-stu-id="c4141-112">For example, let's say your client code is using hello [Twitter Connector API app](../connectors/connectors-create-api-twitter.md) and your code needs tooperform an action based on new tweets that contain specific words.</span></span> <span data-ttu-id="c4141-113">En este caso, podría configurar una toofacilitate de desencadenador de inserción o de sondeo esta necesidad.</span><span class="sxs-lookup"><span data-stu-id="c4141-113">In this case, you might set up a poll or push trigger toofacilitate this need.</span></span>

## <a name="poll-trigger-versus-push-trigger"></a><span data-ttu-id="c4141-114">Desencadenador de sondeo frente a desencadenador de inserción</span><span class="sxs-lookup"><span data-stu-id="c4141-114">Poll trigger versus push trigger</span></span>
<span data-ttu-id="c4141-115">Actualmente, se admiten dos tipos de desencadenadores:</span><span class="sxs-lookup"><span data-stu-id="c4141-115">Currently, two types of triggers are supported:</span></span>

* <span data-ttu-id="c4141-116">Desencadenador de sondeo: cliente sondea la aplicación de API de hello para la notificación de un evento que ha activado</span><span class="sxs-lookup"><span data-stu-id="c4141-116">Poll trigger - Client polls hello API app for notification of an event having been fired</span></span>
* <span data-ttu-id="c4141-117">Desencadenador de inserción: cliente recibe una notificación por aplicación hello API cuando se activa un evento</span><span class="sxs-lookup"><span data-stu-id="c4141-117">Push trigger - Client is notified by hello API app when an event fires</span></span>

### <a name="poll-trigger"></a><span data-ttu-id="c4141-118">Desencadenador de sondeo</span><span class="sxs-lookup"><span data-stu-id="c4141-118">Poll trigger</span></span>
<span data-ttu-id="c4141-119">Un desencadenador de sondeo se implementa como una API de REST regular y espera su toopoll de los clientes (por ejemplo, una aplicación lógica) en pedido tooget notificación.</span><span class="sxs-lookup"><span data-stu-id="c4141-119">A poll trigger is implemented as a regular REST API and expects its clients (such as a Logic app) toopoll it in order tooget notification.</span></span> <span data-ttu-id="c4141-120">Mientras el cliente de hello puede mantener el estado, no tiene estado propio desencadenador de sondeo Hola.</span><span class="sxs-lookup"><span data-stu-id="c4141-120">While hello client may maintain state, hello poll trigger itself is stateless.</span></span>

<span data-ttu-id="c4141-121">Hola después de obtener información sobre los paquetes de solicitud y respuesta de saludo muestra algunos aspectos claves del contrato de desencadenador de sondeo de hello:</span><span class="sxs-lookup"><span data-stu-id="c4141-121">hello following information regarding hello request and response packets illustrate some key aspects of hello poll trigger contract:</span></span>

* <span data-ttu-id="c4141-122">Solicitud</span><span class="sxs-lookup"><span data-stu-id="c4141-122">Request</span></span>
  * <span data-ttu-id="c4141-123">Método HTTP: GET</span><span class="sxs-lookup"><span data-stu-id="c4141-123">HTTP method: GET</span></span>
  * <span data-ttu-id="c4141-124">parameters</span><span class="sxs-lookup"><span data-stu-id="c4141-124">Parameters</span></span>
    * <span data-ttu-id="c4141-125">triggerState: este parámetro opcional permite a los clientes toospecify su estado para que el desencadenador de sondeo de Hola correctamente puede decidir si tooreturn notificación o hello no según el estado especificado.</span><span class="sxs-lookup"><span data-stu-id="c4141-125">triggerState - This optional parameter allows clients toospecify their state so that hello poll trigger can properly decide whether tooreturn notification or not based on hello specified state.</span></span>
    * <span data-ttu-id="c4141-126">Parámetros específicos de la API</span><span class="sxs-lookup"><span data-stu-id="c4141-126">API-specific parameters</span></span>
* <span data-ttu-id="c4141-127">Response</span><span class="sxs-lookup"><span data-stu-id="c4141-127">Response</span></span>
  * <span data-ttu-id="c4141-128">Código de estado **200** : la solicitud es válida y no hay una notificación de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4141-128">Status code **200** - Request is valid and there is a notification from hello trigger.</span></span> <span data-ttu-id="c4141-129">contenido de Hola de notificación de hello será el cuerpo de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4141-129">hello content of hello notification will be hello response body.</span></span> <span data-ttu-id="c4141-130">Un encabezado "Retry-After" en la respuesta de hello indica que se deben recuperar datos de notificación adicionales con una llamada de solicitud posterior.</span><span class="sxs-lookup"><span data-stu-id="c4141-130">A "Retry-After" header in hello response indicates that additional notification data must be retrieved with a subsequent request call.</span></span>
  * <span data-ttu-id="c4141-131">Código de estado **202** : la solicitud es válida, pero no hay ninguna nueva notificación de desencadenador de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4141-131">Status code **202** - Request is valid, but there is no new notification from hello trigger.</span></span>
  * <span data-ttu-id="c4141-132">Código de estado **4xx** : la solicitud no es válida.</span><span class="sxs-lookup"><span data-stu-id="c4141-132">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="c4141-133">cliente de Hello no debe reintentar la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="c4141-133">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="c4141-134">Código de estado **5xx** : la solicitud ha producido un error interno en el servidor o un problema temporal.</span><span class="sxs-lookup"><span data-stu-id="c4141-134">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="c4141-135">cliente de Hello debe reintentar la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="c4141-135">hello client should retry hello request.</span></span>

<span data-ttu-id="c4141-136">Hola siguiente fragmento de código es un ejemplo de cómo desencadenar tooimplement un sondeo.</span><span class="sxs-lookup"><span data-stu-id="c4141-136">hello following code snippet is an example of how tooimplement a poll trigger.</span></span>

    // Implement a poll trigger.
    [HttpGet]
    [Route("api/files/poll/TouchedFiles")]
    public HttpResponseMessage TouchedFilesPollTrigger(
        // triggerState is a UTC timestamp
        string triggerState,
        // Additional parameters
        string searchPattern = "*")
    {
        // Check toosee whether there is any file touched after hello timestamp.
        var lastTriggerTimeUtc = DateTime.Parse(triggerState).ToUniversalTime();
        var touchedFiles = Directory.EnumerateFiles(rootPath, searchPattern, SearchOption.AllDirectories)
            .Select(f => FileInfoWrapper.FromFileInfo(new FileInfo(f)))
            .Where(fi => fi.LastAccessTimeUtc > lastTriggerTimeUtc);

        // If there are files touched after hello timestamp, return their information.
        if (touchedFiles != null && touchedFiles.Count() != 0)
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventTriggered(new { files = touchedFiles });
        }
        // If there are no files touched after hello timestamp, tell hello caller toopoll again after 1 mintue.
        else
        {
            // Extension method provided by hello AppService service SDK.
            return this.Request.EventWaitPoll(new TimeSpan(0, 1, 0));
        }
    }

<span data-ttu-id="c4141-137">tootest este sondeo activa, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c4141-137">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="c4141-138">Implementar Hola API aplicación con una configuración de autenticación de **público anónimo**.</span><span class="sxs-lookup"><span data-stu-id="c4141-138">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="c4141-139">Llamar a hello **táctil** operación tootouch un archivo.</span><span class="sxs-lookup"><span data-stu-id="c4141-139">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="c4141-140">Hola siguiente imagen muestra una solicitud de ejemplo a través de Postman.</span><span class="sxs-lookup"><span data-stu-id="c4141-140">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="c4141-141">![Llamada a la operación Touch mediante Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="c4141-141">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
3. <span data-ttu-id="c4141-142">Llamar al desencadenador de sondeo de hello con hello **triggerState** parámetro establece tooStep anterior de una marca de tiempo tooa #2.</span><span class="sxs-lookup"><span data-stu-id="c4141-142">Call hello poll trigger with hello **triggerState** parameter set tooa time stamp prior tooStep #2.</span></span> <span data-ttu-id="c4141-143">Hello siguiente imagen muestra solicitud de ejemplo de Hola a través de Postman.</span><span class="sxs-lookup"><span data-stu-id="c4141-143">hello following image shows hello sample request via Postman.</span></span>
   <span data-ttu-id="c4141-144">![Llamada al desencadenador de sondeo mediante Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="c4141-144">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/callpolltriggerfrompostman.PNG)</span></span>

### <a name="push-trigger"></a><span data-ttu-id="c4141-145">Desencadenador de inserción</span><span class="sxs-lookup"><span data-stu-id="c4141-145">Push trigger</span></span>
<span data-ttu-id="c4141-146">Un desencadenador de inserción se implementa como una API de REST regular que inserta tooclients de notificaciones que se hayan registrado toobe una notificación cuando se activan eventos específicos.</span><span class="sxs-lookup"><span data-stu-id="c4141-146">A push trigger is implemented as a regular REST API that pushes notifications tooclients who have registered toobe notified when specific events fire.</span></span>

<span data-ttu-id="c4141-147">Hola después de obtener información sobre los paquetes de solicitud y respuesta de saludo ilustran algunos aspectos claves del contrato de desencadenador de inserción de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4141-147">hello following information regarding hello request and response packets illustrate some key aspects of hello push trigger contract.</span></span>

* <span data-ttu-id="c4141-148">Solicitud</span><span class="sxs-lookup"><span data-stu-id="c4141-148">Request</span></span>
  * <span data-ttu-id="c4141-149">Método HTTP: PUT</span><span class="sxs-lookup"><span data-stu-id="c4141-149">HTTP method: PUT</span></span>
  * <span data-ttu-id="c4141-150">parameters</span><span class="sxs-lookup"><span data-stu-id="c4141-150">Parameters</span></span>
    * <span data-ttu-id="c4141-151">Id. de lanzamiento: requerida: opaco de cadena (por ejemplo, un GUID) que representa Hola registro de un desencadenador de inserción.</span><span class="sxs-lookup"><span data-stu-id="c4141-151">triggerId: required - Opaque string (such as a GUID) that represents hello registration of a push trigger.</span></span>
    * <span data-ttu-id="c4141-152">callbackUrl: requerida: dirección URL de hello tooinvoke de devolución de llamada cuando se desencadene el evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4141-152">callbackUrl: required - URL of hello callback tooinvoke when hello event fires.</span></span> <span data-ttu-id="c4141-153">invocación de Hello es una simple llamada HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="c4141-153">hello invocation is a simple POST HTTP call.</span></span>
    * <span data-ttu-id="c4141-154">Parámetros específicos de la API</span><span class="sxs-lookup"><span data-stu-id="c4141-154">API-specific parameters</span></span>
* <span data-ttu-id="c4141-155">Response</span><span class="sxs-lookup"><span data-stu-id="c4141-155">Response</span></span>
  * <span data-ttu-id="c4141-156">Código de estado **200** -solicitud tooregister cliente correctamente.</span><span class="sxs-lookup"><span data-stu-id="c4141-156">Status code **200** - Request tooregister client successful.</span></span>
  * <span data-ttu-id="c4141-157">Código de estado **4xx** : la solicitud no es válida.</span><span class="sxs-lookup"><span data-stu-id="c4141-157">Status code **4xx** - Request is not valid.</span></span> <span data-ttu-id="c4141-158">cliente de Hello no debe reintentar la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="c4141-158">hello client should not retry hello request.</span></span>
  * <span data-ttu-id="c4141-159">Código de estado **5xx** : la solicitud ha producido un error interno en el servidor o un problema temporal.</span><span class="sxs-lookup"><span data-stu-id="c4141-159">Status code **5xx** - Request has resulted in an internal server error and/or temporary issue.</span></span> <span data-ttu-id="c4141-160">cliente de Hello debe reintentar la solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="c4141-160">hello client should retry hello request.</span></span>
* <span data-ttu-id="c4141-161">Devolución de llamada</span><span class="sxs-lookup"><span data-stu-id="c4141-161">Callback</span></span>
  * <span data-ttu-id="c4141-162">Método HTTP: POST</span><span class="sxs-lookup"><span data-stu-id="c4141-162">HTTP method: POST</span></span>
  * <span data-ttu-id="c4141-163">Cuerpo de la solicitud: contenido de la notificación.</span><span class="sxs-lookup"><span data-stu-id="c4141-163">Request body: Notification content.</span></span>

<span data-ttu-id="c4141-164">Hola siguiente fragmento de código es un ejemplo de cómo desencadenar tooimplement una inserción:</span><span class="sxs-lookup"><span data-stu-id="c4141-164">hello following code snippet is an example of how tooimplement a push trigger:</span></span>

    // Implement a push trigger.
    [HttpPut]
    [Route("api/files/push/TouchedFiles/{triggerId}")]
    public HttpResponseMessage TouchedFilesPushTrigger(
        // triggerId is an opaque string.
        string triggerId,
        // A helper class provided by hello AppService service SDK.
        // Here it defines hello input of hello push trigger is a string and hello output toohello callback is a FileInfoWrapper object.
        [FromBody]TriggerInput<string, FileInfoWrapper> triggerInput)
    {
        // Register hello trigger toosome trigger store.
        triggerStore.RegisterTrigger(triggerId, rootPath, triggerInput);

        // Extension method provided by hello AppService service SDK indicating hello registration is completed.
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
            // Use FileSystemWatcher toolisten toofile change event.
            var filter = string.IsNullOrEmpty(triggerInput.inputs) ? "*" : triggerInput.inputs;
            var watcher = new FileSystemWatcher(rootPath, filter);
            watcher.IncludeSubdirectories = true;
            watcher.EnableRaisingEvents = true;
            watcher.NotifyFilter = NotifyFilters.LastAccess;

            // When some file is changed, fire hello push trigger.
            watcher.Changed +=
                (sender, e) => watcher_Changed(sender, e,
                    Runtime.FromAppSettings(),
                    triggerInput.GetCallback());

            // Assoicate hello FileSystemWatcher object with hello triggerId.
            _store[triggerId] = watcher;

        }

        // Fire hello assoicated push trigger when some file is changed.
        void watcher_Changed(object sender, FileSystemEventArgs e,
            // AppService runtime object needed tooinvoke hello callback.
            Runtime runtime,
            // hello callback tooinvoke.
            ClientTriggerCallback<FileInfoWrapper> callback)
        {
            // Helper method provided by AppService service SDK tooinvoke a push trigger callback.
            callback.InvokeAsync(runtime, FileInfoWrapper.FromFileInfo(new FileInfo(e.FullPath)));
        }
    }

<span data-ttu-id="c4141-165">tootest este sondeo activa, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="c4141-165">tootest this poll trigger, follow these steps:</span></span>

1. <span data-ttu-id="c4141-166">Implementar Hola API aplicación con una configuración de autenticación de **público anónimo**.</span><span class="sxs-lookup"><span data-stu-id="c4141-166">Deploy hello API App with an authentication setting of **public anonymous**.</span></span>
2. <span data-ttu-id="c4141-167">Examinar demasiado[http://requestb.in/](http://requestb.in/) toocreate un RequestBin que servirá como la dirección URL de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="c4141-167">Browse too[http://requestb.in/](http://requestb.in/) toocreate a RequestBin which will serve as your callback URL.</span></span>
3. <span data-ttu-id="c4141-168">Llamar al desencadenador de inserción de hello con un GUID como **triggerId** y Hola RequestBin URL como **callbackUrl**.</span><span class="sxs-lookup"><span data-stu-id="c4141-168">Call hello push trigger with a GUID as **triggerId** and hello RequestBin URL as **callbackUrl**.</span></span>
   <span data-ttu-id="c4141-169">![Llamada al desencadenador de inserción mediante Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="c4141-169">![Call Push Trigger via Postman](./media/app-service-api-dotnet-triggers/callpushtriggerfrompostman.PNG)</span></span>
4. <span data-ttu-id="c4141-170">Llamar a hello **táctil** operación tootouch un archivo.</span><span class="sxs-lookup"><span data-stu-id="c4141-170">Call hello **touch** operation tootouch a file.</span></span> <span data-ttu-id="c4141-171">Hola siguiente imagen muestra una solicitud de ejemplo a través de Postman.</span><span class="sxs-lookup"><span data-stu-id="c4141-171">hello following image shows a sample request via Postman.</span></span>
   <span data-ttu-id="c4141-172">![Llamada a la operación Touch mediante Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span><span class="sxs-lookup"><span data-stu-id="c4141-172">![Call Touch Operation via Postman](./media/app-service-api-dotnet-triggers/calltouchfilefrompostman.PNG)</span></span>
5. <span data-ttu-id="c4141-173">Comprobación de hello RequestBin tooconfirm que Hola de devolución de llamada de desencadenador de inserción se invoca con el resultado de la propiedad.</span><span class="sxs-lookup"><span data-stu-id="c4141-173">Check hello RequestBin tooconfirm that hello push trigger callback is invoked with property output.</span></span>
   <span data-ttu-id="c4141-174">![Llamada al desencadenador de sondeo mediante Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span><span class="sxs-lookup"><span data-stu-id="c4141-174">![Call Poll Trigger via Postman](./media/app-service-api-dotnet-triggers/pushtriggercallbackinrequestbin.PNG)</span></span>

### <a name="describe-triggers-in-api-definition"></a><span data-ttu-id="c4141-175">Descripción de los desencadenadores en la definición de la API</span><span class="sxs-lookup"><span data-stu-id="c4141-175">Describe triggers in API definition</span></span>
<span data-ttu-id="c4141-176">Después de implementar desencadenadores de Hola y distribuir su tooAzure de aplicación de API, navegue toohello **definición de la API** hoja en el portal de vista previa de Hola y verá que los desencadenadores se reconocen automáticamente en hello interfaz de usuario, que se controla mediante Hola definición de Swagger 2.0 API de la aplicación hello API.</span><span class="sxs-lookup"><span data-stu-id="c4141-176">After implementing hello triggers and deploying your API app tooAzure, navigate toohello **API Definition** blade in hello Azure preview portal and you'll see that triggers are automatically recognized in hello UI, which is driven by hello Swagger 2.0 API definition of hello API app.</span></span>

![Hoja de definición de la API](./media/app-service-api-dotnet-triggers/apidefinitionblade.PNG)

<span data-ttu-id="c4141-178">Si hace clic en hello **descargar Swagger** botón y archivo JSON de hello abierto, verá resultados toohello similar siguientes:</span><span class="sxs-lookup"><span data-stu-id="c4141-178">If you click hello **Download Swagger** button and open hello JSON file, you'll see results similar toohello following:</span></span>

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

<span data-ttu-id="c4141-179">propiedad de extensión de Hola **x-ms-del programador-desencadenador** es cómo se describe en la definición de la API en desencadenadores y se agrega automáticamente a puerta de enlace de aplicación Hola API cuando solicitan definición Hola API a través de puerta de enlace de hello si Hola solicitar tooone de Hola siguiendo criterios.</span><span class="sxs-lookup"><span data-stu-id="c4141-179">hello extension property **x-ms-schedular-trigger** is how triggers are described in API definition, and is automatically added by hello API app gateway when you request hello API definition via hello gateway if hello request tooone of hello following criteria.</span></span> <span data-ttu-id="c4141-180">(También puede agregar esta propiedad manualmente).</span><span class="sxs-lookup"><span data-stu-id="c4141-180">(You can also add this property manually.)</span></span>

* <span data-ttu-id="c4141-181">Desencadenador de sondeo</span><span class="sxs-lookup"><span data-stu-id="c4141-181">Poll trigger</span></span>
  * <span data-ttu-id="c4141-182">Si es el método HTTP de hello **obtener**.</span><span class="sxs-lookup"><span data-stu-id="c4141-182">If hello HTTP method is **GET**.</span></span>
  * <span data-ttu-id="c4141-183">Si hello **operationId** propiedad contiene la cadena hello **desencadenador**.</span><span class="sxs-lookup"><span data-stu-id="c4141-183">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="c4141-184">Si hello **parámetros** propiedad incluye un parámetro con un **nombre** propiedad establecida demasiado**triggerState**.</span><span class="sxs-lookup"><span data-stu-id="c4141-184">If hello **parameters** property includes a parameter with a **name** property set too**triggerState**.</span></span>
* <span data-ttu-id="c4141-185">Desencadenador de inserción</span><span class="sxs-lookup"><span data-stu-id="c4141-185">Push trigger</span></span>
  * <span data-ttu-id="c4141-186">Si es el método HTTP de hello **colocar**.</span><span class="sxs-lookup"><span data-stu-id="c4141-186">If hello HTTP method is **PUT**.</span></span>
  * <span data-ttu-id="c4141-187">Si hello **operationId** propiedad contiene la cadena hello **desencadenador**.</span><span class="sxs-lookup"><span data-stu-id="c4141-187">If hello **operationId** property contains hello string **trigger**.</span></span>
  * <span data-ttu-id="c4141-188">Si hello **parámetros** propiedad incluye un parámetro con un **nombre** propiedad establecida demasiado**triggerId**.</span><span class="sxs-lookup"><span data-stu-id="c4141-188">If hello **parameters** property includes a parameter with a **name** property set too**triggerId**.</span></span>

## <a name="use-api-app-triggers-in-logic-apps"></a><span data-ttu-id="c4141-189">Uso de desencadenadores de la aplicación de API en aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="c4141-189">Use API app triggers in Logic apps</span></span>
### <a name="list-and-configure-api-app-triggers-in-hello-logic-apps-designer"></a><span data-ttu-id="c4141-190">Mostrar y configurar desencadenadores de la aplicación de API en el Diseñador de aplicaciones de la lógica de Hola</span><span class="sxs-lookup"><span data-stu-id="c4141-190">List and configure API app triggers in hello Logic apps designer</span></span>
<span data-ttu-id="c4141-191">Si crea una aplicación de la lógica de Hola Hola de mismo grupo de recursos como aplicación de API, será capaz de tooadd lo lienzo del diseñador toohello simplemente haciendo clic en él.</span><span class="sxs-lookup"><span data-stu-id="c4141-191">If you create a Logic app in hello same resource group as hello API app, you will be able tooadd it toohello designer canvas simply by clicking it.</span></span> <span data-ttu-id="c4141-192">Hola después de imágenes muestra cómo hacerlo:</span><span class="sxs-lookup"><span data-stu-id="c4141-192">hello following images illustrate this:</span></span>

![Desencadenadores en el Diseñador de aplicaciones lógicas](./media/app-service-api-dotnet-triggers/triggersinlogicappdesigner.PNG)

![Configuración del desencadenador de sondeo en el Diseñador de aplicaciones lógicas](./media/app-service-api-dotnet-triggers/configurepolltriggerinlogicappdesigner.PNG)

![Configuración del desencadenador de inserción en el Diseñador de aplicaciones lógicas](./media/app-service-api-dotnet-triggers/configurepushtriggerinlogicappdesigner.PNG)

## <a name="optimize-api-app-triggers-for-logic-apps"></a><span data-ttu-id="c4141-196">Optimización de los desencadenadores de la aplicación de API para aplicaciones de lógicas</span><span class="sxs-lookup"><span data-stu-id="c4141-196">Optimize API app triggers for Logic apps</span></span>
<span data-ttu-id="c4141-197">Después de agregar desencadenadores tooan API de aplicación, hay algunas cosas que puede hacer experiencia de hello tooimprove cuando se utiliza la aplicación hello API en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="c4141-197">After you add triggers tooan API app, there are a few things you can do tooimprove hello experience when using hello API app in a Logic app.</span></span>

<span data-ttu-id="c4141-198">Por ejemplo, hello **triggerState** parámetro para los desencadenadores de sondeo debe establecerse toohello siguiente expresión en la aplicación de la lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="c4141-198">For instance, hello **triggerState** parameter for poll triggers should be set toohello following expression in hello Logic app.</span></span> <span data-ttu-id="c4141-199">Esta expresión debe evaluar la última invocación del desencadenador de Hola de aplicación lógica de hello de Hola y devuelve ese valor.</span><span class="sxs-lookup"><span data-stu-id="c4141-199">This expression should evaluate hello last invocation of hello trigger from hello Logic app, and return that value.</span></span>  

    @coalesce(triggers()?.outputs?.body?['triggerState'], '')

<span data-ttu-id="c4141-200">Nota: Para obtener una explicación de las funciones de hello utilizadas en expresión Hola anterior, consulte toohello documentación sobre [lenguaje de definición de flujo de trabajo de aplicación lógica](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4141-200">NOTE: For an explanation of hello functions used in hello expression above, refer toohello documentation on [Logic App Workflow Definition Language](https://msdn.microsoft.com/library/azure/dn948512.aspx).</span></span>

<span data-ttu-id="c4141-201">Los usuarios de aplicación lógica necesitaría la expresión de hello tooprovide anteriormente para hello **triggerState** parámetro al usar Hola desencadenador.</span><span class="sxs-lookup"><span data-stu-id="c4141-201">Logic app users would need tooprovide hello expression above for hello **triggerState** parameter while using hello trigger.</span></span> <span data-ttu-id="c4141-202">Es posible toohave este valor preestablecido por el Diseñador de la aplicación hello lógica a través de la propiedad de extensión de hello **x-ms-programador-recomendación**.</span><span class="sxs-lookup"><span data-stu-id="c4141-202">It is possible toohave this value preset by hello Logic app designer through hello extension property **x-ms-scheduler-recommendation**.</span></span>  <span data-ttu-id="c4141-203">Hola **x-ms-visibilidad** propiedad de extensión se puede establecer valor de tooa de *interno* para que el propio parámetro hello no se muestra en el Diseñador de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4141-203">hello **x-ms-visibility** extension property can be set tooa value of *internal* so that hello parameter itself is not shown on hello designer.</span></span>  <span data-ttu-id="c4141-204">Hola siguiente fragmento de código muestra que.</span><span class="sxs-lookup"><span data-stu-id="c4141-204">hello following snippet illustrates that.</span></span>

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

<span data-ttu-id="c4141-205">Para los desencadenadores de inserción, Hola **triggerId** parámetro debe identificar inequívocamente la aplicación de la lógica de hello.</span><span class="sxs-lookup"><span data-stu-id="c4141-205">For push triggers, hello **triggerId** parameter must uniquely identify hello Logic app.</span></span> <span data-ttu-id="c4141-206">Una práctica recomendada es tooset este nombre de propiedad toohello de flujo de trabajo de hello mediante el uso de Hola la siguiente expresión:</span><span class="sxs-lookup"><span data-stu-id="c4141-206">A recommended best practice is tooset this property toohello name of hello workflow by using hello following expression:</span></span>

    @workflow().name

<span data-ttu-id="c4141-207">Con hello **x-ms-programador-recomendación** y **x-ms-visibilidad** propiedades de extensión en su definición de API, Hola aplicación de API pueden transmitir establezca esta propiedad toohello lógica aplicación diseñador tooautomatically expresión para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="c4141-207">Using hello **x-ms-scheduler-recommendation** and **x-ms-visibility** extension properties in its API definiton, hello API app can convey toohello Logic app designer tooautomatically set this expression for hello user.</span></span>

        "parameters":[  
          {  
            "name":"triggerId",
            "in":"path",
            "required":true,
            "x-ms-visibility":"internal",
            "x-ms-scheduler-recommendation":"@workflow().name",
            "type":"string"
          },


### <a name="add-extension-properties-in-api-defintion"></a><span data-ttu-id="c4141-208">Adición de propiedades de extensión en la definición de la API</span><span class="sxs-lookup"><span data-stu-id="c4141-208">Add extension properties in API defintion</span></span>
<span data-ttu-id="c4141-209">Información de metadatos adicionales - como propiedades de extensión de hello **x-ms-programador-recomendación** y **x-ms-visibilidad** -pueden agregarse en la definición de hello API en uno de dos maneras de: estática o dinámica.</span><span class="sxs-lookup"><span data-stu-id="c4141-209">Additional metadata information - such as hello extension properties **x-ms-scheduler-recommendation** and **x-ms-visibility** - can be added in hello API defintion in one of two ways: static or dynamic.</span></span>

<span data-ttu-id="c4141-210">Para obtener metadatos estáticos, puede editar directamente hello */metadata/apiDefinition.swagger.json* un archivo en el proyecto y agregar propiedades de hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="c4141-210">For static metadata, you can directly edit hello */metadata/apiDefinition.swagger.json* file in your project and add hello properties manually.</span></span>

<span data-ttu-id="c4141-211">Para las aplicaciones de API con metadatos dinámicos, puede editar hello SwaggerConfig.cs archivo tooadd un filtro de operación que puede agregar estas extensiones.</span><span class="sxs-lookup"><span data-stu-id="c4141-211">For API apps using dynamic metadata, you can edit hello SwaggerConfig.cs file tooadd an operation filter which can add these extensions.</span></span>

    GlobalConfiguration.Configuration
        .EnableSwagger(c =>
            {
                ...
                c.OperationFilter<TriggerStateFilter>();
                ...
            }


<span data-ttu-id="c4141-212">Hola aquí te mostramos un ejemplo de cómo esta clase puede ser el escenario de implementada toofacilitate Hola metadatos dinámicos.</span><span class="sxs-lookup"><span data-stu-id="c4141-212">hello following is an example of how this class can be implemented toofacilitate hello dynamic metadata scenario.</span></span>

    // Add extension properties on hello triggerState parameter
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
                    // x-ms-visibility: set too'internal' toosignify this is an internal field
                    // x-ms-scheduler-recommendation: set tooa value that logic app can use
                    triggerStateParam.vendorExtensions.Add("x-ms-visibility", "internal");
                    triggerStateParam.vendorExtensions.Add("x-ms-scheduler-recommendation",
                                                           "@coalesce(triggers()?.outputs?.body?['triggerState'], '')");
                }
            }
        }
    }
