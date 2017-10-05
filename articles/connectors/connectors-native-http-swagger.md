---
title: "Llamada a los puntos de conexión REST con el conector HTTP + Swagger para Azure Logic Apps | Microsoft Docs"
description: "Conexión a los puntos de conexión REST desde las aplicaciones lógicas a través de Swagger con el conector HTTP + Swagger"
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
ms.openlocfilehash: 3e9229d94e96aad7b769d0e55d208d856e3b80bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-http--swagger-action"></a><span data-ttu-id="77e94-103">Introducción a la acción HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="77e94-103">Get started with the HTTP + Swagger action</span></span>

<span data-ttu-id="77e94-104">Puede crear un conector de primera categoría para cualquier punto de conexión REST a través de un [documento Swagger](https://swagger.io) al usar la acción HTTP + Swagger en el flujo de trabajo de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="77e94-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="77e94-105">También puede ampliar las aplicaciones lógicas para llamar a cualquier punto de conexión REST con una experiencia de Diseñador de aplicación lógica de primer nivel.</span><span class="sxs-lookup"><span data-stu-id="77e94-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="77e94-106">Para aprender a crear aplicaciones lógicas con conectores, consulte [Creación de una aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="77e94-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="77e94-107">Uso de HTTP + Swagger como desencadenador o acción</span><span class="sxs-lookup"><span data-stu-id="77e94-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="77e94-108">El desencadenador y la acción HTTP + Swagger funcionan igual que la [acción HTTP](connectors-native-http.md), pero ofrecen una experiencia en el Diseñador de aplicación lógica mejor al exponer la estructura de la API y los resultados desde los [metadatos de Swagger](https://swagger.io).</span><span class="sxs-lookup"><span data-stu-id="77e94-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="77e94-109">También puede usar el conector HTTP + Swagger como desencadenador.</span><span class="sxs-lookup"><span data-stu-id="77e94-109">You can also use the HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="77e94-110">Si desea implementar un desencadenador de sondeo, siga el modelo de sondeo que se describe en [Creación de API personalizadas para llamar a otras API, servicio y sistemas de aplicaciones lógicas](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="77e94-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="77e94-111">Más información sobre [las acciones y los desencadenadores de aplicaciones lógicas](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77e94-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="77e94-112">A continuación se muestra un ejemplo de cómo utilizar la operación HTTP + Swagger como una acción en un flujo de trabajo de una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="77e94-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="77e94-113">Seleccione el botón **Nuevo paso** .</span><span class="sxs-lookup"><span data-stu-id="77e94-113">Select the **New Step** button.</span></span>
2. <span data-ttu-id="77e94-114">Seleccione **Add an action**(Agregar una acción).</span><span class="sxs-lookup"><span data-stu-id="77e94-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="77e94-115">En el cuadro de búsqueda de acciones, escriba **swagger** para mostrar la acción HTTP + Swagger.</span><span class="sxs-lookup"><span data-stu-id="77e94-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span></span>
   
    ![Acción de selección de HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="77e94-117">Escriba la dirección URL de un documento Swagger:</span><span class="sxs-lookup"><span data-stu-id="77e94-117">Type the URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="77e94-118">Para poder utilizarse en el diseñador de aplicaciones lógicas, la dirección URL debe ser un punto de conexión HTTPS y debe tener habilitado CORS.</span><span class="sxs-lookup"><span data-stu-id="77e94-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="77e94-119">Si el documento Swagger no cumple este requisito, puede usar el [Azure Storage con CORS habilitado](#hosting-swagger-from-storage) para almacenar el documento.</span><span class="sxs-lookup"><span data-stu-id="77e94-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span></span>
5. <span data-ttu-id="77e94-120">Haga clic en **Siguiente** para realizar operaciones de lectura y procesamiento en el documento Swagger.</span><span class="sxs-lookup"><span data-stu-id="77e94-120">Click **Next** to read and render from the Swagger document.</span></span>
6. <span data-ttu-id="77e94-121">Agregue cualquier parámetro necesario para la llamada HTTP.</span><span class="sxs-lookup"><span data-stu-id="77e94-121">Add in any parameters that are required for the HTTP call.</span></span>
   
    ![Completar acción HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="77e94-123">Para guardar y publicar la aplicación lógica, haga clic en **Guardar** en la barra de herramientas del diseñador.</span><span class="sxs-lookup"><span data-stu-id="77e94-123">To save and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="77e94-124">Hospedar Swagger desde Azure Storage</span><span class="sxs-lookup"><span data-stu-id="77e94-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="77e94-125">Puede hacer referencia a un documento de Swagger que no está hospedado, o que no cumple los requisitos de seguridad y de origen cruzado para el diseñador.</span><span class="sxs-lookup"><span data-stu-id="77e94-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span></span> <span data-ttu-id="77e94-126">Para resolver este problema, puede almacenar el documento Swagger en Azure Storage y habilitar CORS para hacer referencia al documento.</span><span class="sxs-lookup"><span data-stu-id="77e94-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span></span>  

<span data-ttu-id="77e94-127">Estos son los pasos necesarios para crear, configurar y almacenar documentos Swagger en Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="77e94-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="77e94-128">[Crear una cuenta de Azure Storage con Azure Blob Storage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="77e94-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="77e94-129">Para este paso, establezca los permisos en **Acceso público**.</span><span class="sxs-lookup"><span data-stu-id="77e94-129">To perform this step, set permissions to **Public Access**.</span></span>

2. <span data-ttu-id="77e94-130">Habilite CORS en el blob.</span><span class="sxs-lookup"><span data-stu-id="77e94-130">Enable CORS on the blob.</span></span> 

   <span data-ttu-id="77e94-131">Puede usar [este script de PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1) para configurar automáticamente esta opción.</span><span class="sxs-lookup"><span data-stu-id="77e94-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="77e94-132">Cargue el archivo de Swagger en el blob.</span><span class="sxs-lookup"><span data-stu-id="77e94-132">Upload the Swagger file to the blob.</span></span> 

   <span data-ttu-id="77e94-133">Puede realizar este paso desde [Azure Portal](https://portal.azure.com) o con una herramienta como el [Explorador de Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="77e94-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="77e94-134">Haga referencia a un vínculo HTTPS en el documento de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="77e94-134">Reference an HTTPS link to the document in Azure Blob storage.</span></span> 

   <span data-ttu-id="77e94-135">El vínculo utiliza este formato:</span><span class="sxs-lookup"><span data-stu-id="77e94-135">The link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="77e94-136">Detalles técnicos</span><span class="sxs-lookup"><span data-stu-id="77e94-136">Technical details</span></span>
<span data-ttu-id="77e94-137">A continuación se muestran los detalles de los desencadenadores y las acciones que admite el conector HTTP + Swagger.</span><span class="sxs-lookup"><span data-stu-id="77e94-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="77e94-138">Desencadenadores HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="77e94-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="77e94-139">Un desencadenador es un evento que se puede utilizar para iniciar el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="77e94-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="77e94-140">Más información sobre los desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="77e94-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="77e94-141">El conector HTTP + Swagger tiene un desencadenador.</span><span class="sxs-lookup"><span data-stu-id="77e94-141">The HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="77e94-142">Desencadenador</span><span class="sxs-lookup"><span data-stu-id="77e94-142">Trigger</span></span> | <span data-ttu-id="77e94-143">Description</span><span class="sxs-lookup"><span data-stu-id="77e94-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77e94-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="77e94-144">HTTP + Swagger</span></span> |<span data-ttu-id="77e94-145">Realizar una llamada HTTP y devolver el contenido de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="77e94-145">Make an HTTP call and return the response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="77e94-146">Acciones HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="77e94-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="77e94-147">Una acción es una operación que se lleva a cabo mediante el flujo de trabajo definido en una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="77e94-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="77e94-148">Más información acerca de las acciones.</span><span class="sxs-lookup"><span data-stu-id="77e94-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="77e94-149">El conector HTTP + Swagger tiene una acción posible.</span><span class="sxs-lookup"><span data-stu-id="77e94-149">The HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="77e94-150">Acción</span><span class="sxs-lookup"><span data-stu-id="77e94-150">Action</span></span> | <span data-ttu-id="77e94-151">Description</span><span class="sxs-lookup"><span data-stu-id="77e94-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77e94-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="77e94-152">HTTP + Swagger</span></span> |<span data-ttu-id="77e94-153">Realizar una llamada HTTP y devolver el contenido de la respuesta.</span><span class="sxs-lookup"><span data-stu-id="77e94-153">Make an HTTP call and return the response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="77e94-154">Detalles de la acción</span><span class="sxs-lookup"><span data-stu-id="77e94-154">Action details</span></span>
<span data-ttu-id="77e94-155">El conector HTTP + Swagger incluye una acción posible.</span><span class="sxs-lookup"><span data-stu-id="77e94-155">The HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="77e94-156">A continuación, se incluye información acerca de cada una de las acciones, los campos de entrada obligatorios y opcionales, y los detalles de salida correspondientes asociados a su uso.</span><span class="sxs-lookup"><span data-stu-id="77e94-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="77e94-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="77e94-157">HTTP + Swagger</span></span>
<span data-ttu-id="77e94-158">Realice una solicitud HTTP saliente con ayuda de los metadatos de Swagger.</span><span class="sxs-lookup"><span data-stu-id="77e94-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="77e94-159">Un asterisco (*) significa un campo obligatorio.</span><span class="sxs-lookup"><span data-stu-id="77e94-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="77e94-160">Nombre para mostrar</span><span class="sxs-lookup"><span data-stu-id="77e94-160">Display name</span></span> | <span data-ttu-id="77e94-161">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="77e94-161">Property name</span></span> | <span data-ttu-id="77e94-162">Description</span><span class="sxs-lookup"><span data-stu-id="77e94-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77e94-163">Método*</span><span class="sxs-lookup"><span data-stu-id="77e94-163">Method*</span></span> |<span data-ttu-id="77e94-164">estático</span><span class="sxs-lookup"><span data-stu-id="77e94-164">method</span></span> |<span data-ttu-id="77e94-165">Verbo HTTP que se va a usar</span><span class="sxs-lookup"><span data-stu-id="77e94-165">HTTP verb to use.</span></span> |
| <span data-ttu-id="77e94-166">URI*</span><span class="sxs-lookup"><span data-stu-id="77e94-166">URI*</span></span> |<span data-ttu-id="77e94-167">uri</span><span class="sxs-lookup"><span data-stu-id="77e94-167">uri</span></span> |<span data-ttu-id="77e94-168">Identificador URI de la solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="77e94-168">URI for the HTTP request.</span></span> |
| <span data-ttu-id="77e94-169">Encabezados</span><span class="sxs-lookup"><span data-stu-id="77e94-169">Headers</span></span> |<span data-ttu-id="77e94-170">Encabezados</span><span class="sxs-lookup"><span data-stu-id="77e94-170">headers</span></span> |<span data-ttu-id="77e94-171">Objeto JSON de los encabezados HTTP que se va a incluir</span><span class="sxs-lookup"><span data-stu-id="77e94-171">A JSON object of HTTP headers to include.</span></span> |
| <span data-ttu-id="77e94-172">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="77e94-172">Body</span></span> |<span data-ttu-id="77e94-173">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="77e94-173">body</span></span> |<span data-ttu-id="77e94-174">Cuerpo de la solicitud HTTP</span><span class="sxs-lookup"><span data-stu-id="77e94-174">The HTTP request body.</span></span> |
| <span data-ttu-id="77e94-175">Autenticación</span><span class="sxs-lookup"><span data-stu-id="77e94-175">Authentication</span></span> |<span data-ttu-id="77e94-176">Autenticación</span><span class="sxs-lookup"><span data-stu-id="77e94-176">authentication</span></span> |<span data-ttu-id="77e94-177">Autenticación que se utiliza para la solicitud.</span><span class="sxs-lookup"><span data-stu-id="77e94-177">Authentication to use for request.</span></span> <span data-ttu-id="77e94-178">Para más información, consulte el artículo [Conector HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="77e94-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="77e94-179">**Detalles de salida**</span><span class="sxs-lookup"><span data-stu-id="77e94-179">**Output details**</span></span>

<span data-ttu-id="77e94-180">Respuesta HTTP</span><span class="sxs-lookup"><span data-stu-id="77e94-180">HTTP response</span></span>

| <span data-ttu-id="77e94-181">Nombre de propiedad</span><span class="sxs-lookup"><span data-stu-id="77e94-181">Property Name</span></span> | <span data-ttu-id="77e94-182">Tipo de datos</span><span class="sxs-lookup"><span data-stu-id="77e94-182">Data type</span></span> | <span data-ttu-id="77e94-183">Description</span><span class="sxs-lookup"><span data-stu-id="77e94-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77e94-184">encabezados</span><span class="sxs-lookup"><span data-stu-id="77e94-184">Headers</span></span> |<span data-ttu-id="77e94-185">objeto</span><span class="sxs-lookup"><span data-stu-id="77e94-185">object</span></span> |<span data-ttu-id="77e94-186">Encabezados de respuesta</span><span class="sxs-lookup"><span data-stu-id="77e94-186">Response headers</span></span> |
| <span data-ttu-id="77e94-187">Cuerpo</span><span class="sxs-lookup"><span data-stu-id="77e94-187">Body</span></span> |<span data-ttu-id="77e94-188">objeto</span><span class="sxs-lookup"><span data-stu-id="77e94-188">object</span></span> |<span data-ttu-id="77e94-189">Objeto de respuesta</span><span class="sxs-lookup"><span data-stu-id="77e94-189">Response object</span></span> |
| <span data-ttu-id="77e94-190">Código de estado</span><span class="sxs-lookup"><span data-stu-id="77e94-190">Status Code</span></span> |<span data-ttu-id="77e94-191">int</span><span class="sxs-lookup"><span data-stu-id="77e94-191">int</span></span> |<span data-ttu-id="77e94-192">Código de estado HTTP</span><span class="sxs-lookup"><span data-stu-id="77e94-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="77e94-193">Respuestas HTTP</span><span class="sxs-lookup"><span data-stu-id="77e94-193">HTTP responses</span></span>
<span data-ttu-id="77e94-194">Al realizar llamadas a diversas acciones, es posible que obtenga determinadas respuestas.</span><span class="sxs-lookup"><span data-stu-id="77e94-194">When making calls to various actions, you might get certain responses.</span></span> <span data-ttu-id="77e94-195">A continuación se incluye una tabla que describe las respuestas y descripciones correspondientes.</span><span class="sxs-lookup"><span data-stu-id="77e94-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="77e94-196">Nombre</span><span class="sxs-lookup"><span data-stu-id="77e94-196">Name</span></span> | <span data-ttu-id="77e94-197">Descripción</span><span class="sxs-lookup"><span data-stu-id="77e94-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77e94-198">200</span><span class="sxs-lookup"><span data-stu-id="77e94-198">200</span></span> |<span data-ttu-id="77e94-199">OK</span><span class="sxs-lookup"><span data-stu-id="77e94-199">OK</span></span> |
| <span data-ttu-id="77e94-200">202</span><span class="sxs-lookup"><span data-stu-id="77e94-200">202</span></span> |<span data-ttu-id="77e94-201">Accepted</span><span class="sxs-lookup"><span data-stu-id="77e94-201">Accepted</span></span> |
| <span data-ttu-id="77e94-202">400</span><span class="sxs-lookup"><span data-stu-id="77e94-202">400</span></span> |<span data-ttu-id="77e94-203">Solicitud incorrecta</span><span class="sxs-lookup"><span data-stu-id="77e94-203">Bad request</span></span> |
| <span data-ttu-id="77e94-204">401</span><span class="sxs-lookup"><span data-stu-id="77e94-204">401</span></span> |<span data-ttu-id="77e94-205">No autorizado</span><span class="sxs-lookup"><span data-stu-id="77e94-205">Unauthorized</span></span> |
| <span data-ttu-id="77e94-206">403</span><span class="sxs-lookup"><span data-stu-id="77e94-206">403</span></span> |<span data-ttu-id="77e94-207">Prohibido</span><span class="sxs-lookup"><span data-stu-id="77e94-207">Forbidden</span></span> |
| <span data-ttu-id="77e94-208">404</span><span class="sxs-lookup"><span data-stu-id="77e94-208">404</span></span> |<span data-ttu-id="77e94-209">No encontrado</span><span class="sxs-lookup"><span data-stu-id="77e94-209">Not Found</span></span> |
| <span data-ttu-id="77e94-210">500</span><span class="sxs-lookup"><span data-stu-id="77e94-210">500</span></span> |<span data-ttu-id="77e94-211">Error interno del servidor</span><span class="sxs-lookup"><span data-stu-id="77e94-211">Internal server error.</span></span> <span data-ttu-id="77e94-212">Error desconocido.</span><span class="sxs-lookup"><span data-stu-id="77e94-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="77e94-213">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="77e94-213">Next steps</span></span>

* [<span data-ttu-id="77e94-214">Creación de una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="77e94-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="77e94-215">Buscar otros conectores</span><span class="sxs-lookup"><span data-stu-id="77e94-215">Find other connectors</span></span>](apis-list.md)