---
title: "los extremos REST de aaaCall con HTTP + Swagger conector para las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Conectar los extremos de tooREST de lógica de aplicaciones a través de Swagger con Hola HTTP + conector de Swagger"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a><span data-ttu-id="67124-103">Empezar a trabajar con Hola HTTP + acción de Swagger</span><span class="sxs-lookup"><span data-stu-id="67124-103">Get started with hello HTTP + Swagger action</span></span>

<span data-ttu-id="67124-104">Puede crear un extremo REST de primera clase conector tooany a través de un [Swagger documento](https://swagger.io) cuando usas Hola HTTP + Swagger acción en el flujo de trabajo de aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="67124-104">You can create a first-class connector tooany REST endpoint through a [Swagger document](https://swagger.io) when you use hello HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="67124-105">También puede extender lógica aplicaciones toocall cualquier extremo REST con una experiencia de diseñador de la aplicación lógica de primera clase.</span><span class="sxs-lookup"><span data-stu-id="67124-105">You can also extend logic apps toocall any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="67124-106">toolearn cómo toocreate las aplicaciones lógicas con conectores, consulte [crear una nueva aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="67124-106">toolearn how toocreate logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="67124-107">Uso de HTTP + Swagger como desencadenador o acción</span><span class="sxs-lookup"><span data-stu-id="67124-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="67124-108">Hola HTTP + Swagger desencadenador y la acción del trabajo mismo Hola como hello [acción HTTP](connectors-native-http.md) pero ofrecer una mejor experiencia de diseñador de la aplicación lógica mediante la exposición de la estructura de la API de Hola y salidas de hello [Swagger metadatos](https://swagger.io) .</span><span class="sxs-lookup"><span data-stu-id="67124-108">hello HTTP + Swagger trigger and action work hello same as hello [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing hello API structure and outputs from hello [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="67124-109">También puede utilizar Hola HTTP + Swagger conector como un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="67124-109">You can also use hello HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="67124-110">Si desea que un desencadenador de sondeo tooimplement, siguen el patrón de sondeo de Hola que se describe en [crear personalizado toocall API otras API, servicios y sistemas de aplicaciones de lógica de](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="67124-110">If you want tooimplement a polling trigger, follow hello polling pattern that's described in [Create custom APIs toocall other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="67124-111">Más información sobre [las acciones y los desencadenadores de aplicaciones lógicas](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67124-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="67124-112">Este es un ejemplo de cómo toouse Hola HTTP + Swagger operación como una acción en un flujo de trabajo en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="67124-112">Here's an example of how toouse hello HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="67124-113">Seleccione hello **nuevo paso** botón.</span><span class="sxs-lookup"><span data-stu-id="67124-113">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="67124-114">Seleccione **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="67124-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="67124-115">En el cuadro de búsqueda de la acción de hello, escriba **swagger** toolist Hola HTTP + Swagger acción.</span><span class="sxs-lookup"><span data-stu-id="67124-115">In hello action search box, type **swagger** toolist hello HTTP + Swagger action.</span></span>
   
    ![Acción de selección de HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="67124-117">Escriba la dirección URL de Hola para un documento de Swagger:</span><span class="sxs-lookup"><span data-stu-id="67124-117">Type hello URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="67124-118">toowork de hello Diseñador de la lógica de aplicaciones, Hola URL debe ser un extremo HTTPS y ha habilitado CORS.</span><span class="sxs-lookup"><span data-stu-id="67124-118">toowork from hello Logic App Designer, hello URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="67124-119">Si el documento de Swagger de hello no cumple este requisito, puede usar [con CORS habilita el almacenamiento de Azure](#hosting-swagger-from-storage) documento de hello toostore.</span><span class="sxs-lookup"><span data-stu-id="67124-119">If hello Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) toostore hello document.</span></span>
5. <span data-ttu-id="67124-120">Haga clic en **siguiente** tooread y presentación de Hola Swagger documento.</span><span class="sxs-lookup"><span data-stu-id="67124-120">Click **Next** tooread and render from hello Swagger document.</span></span>
6. <span data-ttu-id="67124-121">Agregue todos los parámetros que son necesarios para la llamada de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="67124-121">Add in any parameters that are required for hello HTTP call.</span></span>
   
    ![Completar acción HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="67124-123">toosave y publicar la aplicación lógica, haga clic en **guardar** en la barra de herramientas del diseñador.</span><span class="sxs-lookup"><span data-stu-id="67124-123">toosave and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="67124-124">Hospedar Swagger desde Azure Storage</span><span class="sxs-lookup"><span data-stu-id="67124-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="67124-125">Puede ser conveniente tooreference un documento de Swagger que no se hospeda o que no cumple los requisitos de seguridad y entre orígenes de hello para el Diseñador de Hola.</span><span class="sxs-lookup"><span data-stu-id="67124-125">You might want tooreference a Swagger document that's not hosted, or that doesn't meet hello security and cross-origin requirements for hello designer.</span></span> <span data-ttu-id="67124-126">tooresolve este problema, puede almacenar documentos de Swagger de hello en el almacenamiento de Azure y habilitar CORS tooreference Hola documentos.</span><span class="sxs-lookup"><span data-stu-id="67124-126">tooresolve this issue, you can store hello Swagger document in Azure Storage and enable CORS tooreference hello document.</span></span>  

<span data-ttu-id="67124-127">Presentamos Hola pasos toocreate, configurar y almacenar documentos de Swagger en el almacenamiento de Azure:</span><span class="sxs-lookup"><span data-stu-id="67124-127">Here are hello steps toocreate, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="67124-128">[Crear una cuenta de Azure Storage con Azure Blob Storage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="67124-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="67124-129">tooperform este paso, establecer permisos demasiado**acceso público**.</span><span class="sxs-lookup"><span data-stu-id="67124-129">tooperform this step, set permissions too**Public Access**.</span></span>

2. <span data-ttu-id="67124-130">Habilitar CORS en blob Hola.</span><span class="sxs-lookup"><span data-stu-id="67124-130">Enable CORS on hello blob.</span></span> 

   <span data-ttu-id="67124-131">tooautomatically esta configuración, puede usar [esta secuencia de comandos de PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="67124-131">tooautomatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="67124-132">Cargar blob de hello Swagger archivos toohello.</span><span class="sxs-lookup"><span data-stu-id="67124-132">Upload hello Swagger file toohello blob.</span></span> 

   <span data-ttu-id="67124-133">Puede realizar este paso de hello [portal de Azure](https://portal.azure.com) o desde una herramienta como [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="67124-133">You can perform this step from hello [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="67124-134">Hacer referencia a un documento de toohello vínculo HTTPS en almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="67124-134">Reference an HTTPS link toohello document in Azure Blob storage.</span></span> 

   <span data-ttu-id="67124-135">vínculo de Hello utiliza este formato:</span><span class="sxs-lookup"><span data-stu-id="67124-135">hello link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="67124-136">Detalles técnicos</span><span class="sxs-lookup"><span data-stu-id="67124-136">Technical details</span></span>
<span data-ttu-id="67124-137">Siguientes son los detalles de Hola de hello desencadenadores y acciones que este HTTP + Swagger conector es compatible con.</span><span class="sxs-lookup"><span data-stu-id="67124-137">Following are hello details for hello triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="67124-138">Desencadenadores HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="67124-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="67124-139">Un desencadenador es un evento que puede ser el flujo de trabajo hello toostart utilizado que se define en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="67124-139">A trigger is an event that can be used toostart hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="67124-140">Más información sobre los desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="67124-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="67124-141">Hola HTTP + Swagger conector tiene un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="67124-141">hello HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="67124-142">Desencadenador</span><span class="sxs-lookup"><span data-stu-id="67124-142">Trigger</span></span> | <span data-ttu-id="67124-143">Description</span><span class="sxs-lookup"><span data-stu-id="67124-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="67124-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="67124-144">HTTP + Swagger</span></span> |<span data-ttu-id="67124-145">Realizar una llamada HTTP y devolver el contenido de la respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="67124-145">Make an HTTP call and return hello response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="67124-146">Acciones HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="67124-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="67124-147">Una acción es una operación que se lleva a cabo por flujo de trabajo de Hola que se define en una aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="67124-147">An action is an operation that's carried out by hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="67124-148">Más información acerca de las acciones.</span><span class="sxs-lookup"><span data-stu-id="67124-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="67124-149">Hola HTTP + Swagger conector tiene una acción posible.</span><span class="sxs-lookup"><span data-stu-id="67124-149">hello HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="67124-150">Acción</span><span class="sxs-lookup"><span data-stu-id="67124-150">Action</span></span> | <span data-ttu-id="67124-151">Description</span><span class="sxs-lookup"><span data-stu-id="67124-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="67124-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="67124-152">HTTP + Swagger</span></span> |<span data-ttu-id="67124-153">Realizar una llamada HTTP y devolver el contenido de la respuesta de Hola</span><span class="sxs-lookup"><span data-stu-id="67124-153">Make an HTTP call and return hello response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="67124-154">Detalles de la acción</span><span class="sxs-lookup"><span data-stu-id="67124-154">Action details</span></span>
<span data-ttu-id="67124-155">Hola HTTP + Swagger conector viene con una acción posible.</span><span class="sxs-lookup"><span data-stu-id="67124-155">hello HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="67124-156">A continuación encontrará información sobre cada una de las acciones de Hola, hello correspondiente detalles de salida que están asociados a su uso y sus campos de entrada obligatorios y opcionales.</span><span class="sxs-lookup"><span data-stu-id="67124-156">Following is information about each of hello actions, their required and optional input fields, and hello corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="67124-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="67124-157">HTTP + Swagger</span></span>
<span data-ttu-id="67124-158">Realice una solicitud HTTP saliente con ayuda de los metadatos de Swagger.</span><span class="sxs-lookup"><span data-stu-id="67124-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="67124-159">Un asterisco (*) significa un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="67124-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="67124-160">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="67124-160">Display name</span></span> | <span data-ttu-id="67124-161">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="67124-161">Property name</span></span> | <span data-ttu-id="67124-162">Description</span><span class="sxs-lookup"><span data-stu-id="67124-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67124-163">Método*</span><span class="sxs-lookup"><span data-stu-id="67124-163">Method*</span></span> |<span data-ttu-id="67124-164">estático</span><span class="sxs-lookup"><span data-stu-id="67124-164">method</span></span> |<span data-ttu-id="67124-165">Toouse de verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="67124-165">HTTP verb toouse.</span></span> |
| <span data-ttu-id="67124-166">URI*</span><span class="sxs-lookup"><span data-stu-id="67124-166">URI*</span></span> |<span data-ttu-id="67124-167">uri</span><span class="sxs-lookup"><span data-stu-id="67124-167">uri</span></span> |<span data-ttu-id="67124-168">URI de solicitud de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="67124-168">URI for hello HTTP request.</span></span> |
| <span data-ttu-id="67124-169">Encabezados</span><span class="sxs-lookup"><span data-stu-id="67124-169">Headers</span></span> |<span data-ttu-id="67124-170">encabezados</span><span class="sxs-lookup"><span data-stu-id="67124-170">headers</span></span> |<span data-ttu-id="67124-171">Un objeto JSON de tooinclude de encabezados HTTP.</span><span class="sxs-lookup"><span data-stu-id="67124-171">A JSON object of HTTP headers tooinclude.</span></span> |
| <span data-ttu-id="67124-172">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="67124-172">Body</span></span> |<span data-ttu-id="67124-173">body</span><span class="sxs-lookup"><span data-stu-id="67124-173">body</span></span> |<span data-ttu-id="67124-174">Hola cuerpo de solicitud HTTP.</span><span class="sxs-lookup"><span data-stu-id="67124-174">hello HTTP request body.</span></span> |
| <span data-ttu-id="67124-175">Autenticación</span><span class="sxs-lookup"><span data-stu-id="67124-175">Authentication</span></span> |<span data-ttu-id="67124-176">Autenticación</span><span class="sxs-lookup"><span data-stu-id="67124-176">authentication</span></span> |<span data-ttu-id="67124-177">Toouse de autenticación para la solicitud.</span><span class="sxs-lookup"><span data-stu-id="67124-177">Authentication toouse for request.</span></span> <span data-ttu-id="67124-178">Para obtener más información, vea hello [conector HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="67124-178">For more information, see hello [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="67124-179">**Detalles de salida**</span><span class="sxs-lookup"><span data-stu-id="67124-179">**Output details**</span></span>

<span data-ttu-id="67124-180">Respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="67124-180">HTTP response</span></span>

| <span data-ttu-id="67124-181">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="67124-181">Property Name</span></span> | <span data-ttu-id="67124-182">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="67124-182">Data type</span></span> | <span data-ttu-id="67124-183">Description</span><span class="sxs-lookup"><span data-stu-id="67124-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67124-184">encabezados</span><span class="sxs-lookup"><span data-stu-id="67124-184">Headers</span></span> |<span data-ttu-id="67124-185">objeto</span><span class="sxs-lookup"><span data-stu-id="67124-185">object</span></span> |<span data-ttu-id="67124-186">Encabezados de respuesta</span><span class="sxs-lookup"><span data-stu-id="67124-186">Response headers</span></span> |
| <span data-ttu-id="67124-187">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="67124-187">Body</span></span> |<span data-ttu-id="67124-188">objeto</span><span class="sxs-lookup"><span data-stu-id="67124-188">object</span></span> |<span data-ttu-id="67124-189">Objeto de respuesta</span><span class="sxs-lookup"><span data-stu-id="67124-189">Response object</span></span> |
| <span data-ttu-id="67124-190">Código de estado</span><span class="sxs-lookup"><span data-stu-id="67124-190">Status Code</span></span> |<span data-ttu-id="67124-191">int</span><span class="sxs-lookup"><span data-stu-id="67124-191">int</span></span> |<span data-ttu-id="67124-192">Código de estado HTTP</span><span class="sxs-lookup"><span data-stu-id="67124-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="67124-193">Respuestas HTTP</span><span class="sxs-lookup"><span data-stu-id="67124-193">HTTP responses</span></span>
<span data-ttu-id="67124-194">Al realizar llamadas toovarious acciones, podría obtener determinadas respuestas.</span><span class="sxs-lookup"><span data-stu-id="67124-194">When making calls toovarious actions, you might get certain responses.</span></span> <span data-ttu-id="67124-195">A continuación se incluye una tabla que describe las respuestas y descripciones correspondientes.</span><span class="sxs-lookup"><span data-stu-id="67124-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="67124-196">Nombre</span><span class="sxs-lookup"><span data-stu-id="67124-196">Name</span></span> | <span data-ttu-id="67124-197">Descripción</span><span class="sxs-lookup"><span data-stu-id="67124-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="67124-198">200</span><span class="sxs-lookup"><span data-stu-id="67124-198">200</span></span> |<span data-ttu-id="67124-199">OK</span><span class="sxs-lookup"><span data-stu-id="67124-199">OK</span></span> |
| <span data-ttu-id="67124-200">202</span><span class="sxs-lookup"><span data-stu-id="67124-200">202</span></span> |<span data-ttu-id="67124-201">Accepted</span><span class="sxs-lookup"><span data-stu-id="67124-201">Accepted</span></span> |
| <span data-ttu-id="67124-202">400</span><span class="sxs-lookup"><span data-stu-id="67124-202">400</span></span> |<span data-ttu-id="67124-203">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="67124-203">Bad request</span></span> |
| <span data-ttu-id="67124-204">401</span><span class="sxs-lookup"><span data-stu-id="67124-204">401</span></span> |<span data-ttu-id="67124-205">No autorizado</span><span class="sxs-lookup"><span data-stu-id="67124-205">Unauthorized</span></span> |
| <span data-ttu-id="67124-206">403</span><span class="sxs-lookup"><span data-stu-id="67124-206">403</span></span> |<span data-ttu-id="67124-207">Prohibido</span><span class="sxs-lookup"><span data-stu-id="67124-207">Forbidden</span></span> |
| <span data-ttu-id="67124-208">404</span><span class="sxs-lookup"><span data-stu-id="67124-208">404</span></span> |<span data-ttu-id="67124-209">No encontrado</span><span class="sxs-lookup"><span data-stu-id="67124-209">Not Found</span></span> |
| <span data-ttu-id="67124-210">500</span><span class="sxs-lookup"><span data-stu-id="67124-210">500</span></span> |<span data-ttu-id="67124-211">Error interno del servidor</span><span class="sxs-lookup"><span data-stu-id="67124-211">Internal server error.</span></span> <span data-ttu-id="67124-212">Error desconocido.</span><span class="sxs-lookup"><span data-stu-id="67124-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="67124-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="67124-213">Next steps</span></span>

* [<span data-ttu-id="67124-214">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="67124-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="67124-215">Buscar otros conectores</span><span class="sxs-lookup"><span data-stu-id="67124-215">Find other connectors</span></span>](apis-list.md)