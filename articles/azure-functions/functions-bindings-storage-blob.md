---
title: enlaces de almacenamiento de blobs de funciones aaaAzure | Documentos de Microsoft
description: "Comprender cómo se desencadena toouse almacenamiento de Azure y los enlaces de funciones de Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funciones, procesamiento de eventos, proceso dinámico, arquitectura sin servidor"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="dbe23-104">Enlaces de Blob Storage en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="dbe23-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="dbe23-105">Este artículo se explica cómo tooconfigure y trabajar con enlaces de almacenamiento de blobs de Azure en las funciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbe23-105">This article explains how tooconfigure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="dbe23-106">Azure Functions admite desencadenador y enlaces de entrada y salida para Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="dbe23-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="dbe23-107">Para las características que estén disponibles en todos los enlaces, consulte [conceptos sobre desencadenadores y enlaces de Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="dbe23-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="dbe23-108">No se admite una [cuenta de almacenamiento solo de blob](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="dbe23-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="dbe23-109">Los desencadenadores y enlaces de Blob Storage necesitan una cuenta de almacenamiento de uso general.</span><span class="sxs-lookup"><span data-stu-id="dbe23-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="dbe23-110">Desencadenadores y enlaces de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="dbe23-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="dbe23-111">Usar desencadenador de almacenamiento de blobs de Azure hello, el código de la función se llama cuando se detecta un blob nuevo o actualizado.</span><span class="sxs-lookup"><span data-stu-id="dbe23-111">Using hello Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="dbe23-112">contenido de blob de Hola se proporciona como función de entrada toohello.</span><span class="sxs-lookup"><span data-stu-id="dbe23-112">hello blob contents are provided as input toohello function.</span></span>

<span data-ttu-id="dbe23-113">Definir un desencadenador de almacenamiento de blob mediante hello **integrar** Hola funciones portal de.</span><span class="sxs-lookup"><span data-stu-id="dbe23-113">Define a blob storage trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="dbe23-114">portal de Hello crea Hola después de la definición de hello **enlaces** sección de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="dbe23-114">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="dbe23-115">BLOB de entrada y salida enlaces se definen mediante `blob` como tipo de enlace de hello:</span><span class="sxs-lookup"><span data-stu-id="dbe23-115">Blob input and output bindings are defined using `blob` as hello binding type:</span></span>

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="dbe23-116">Hola `path` admite la propiedad de enlace expresiones y parámetros de filtro.</span><span class="sxs-lookup"><span data-stu-id="dbe23-116">hello `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="dbe23-117">Consulte [Patrones de nombre](#pattern).</span><span class="sxs-lookup"><span data-stu-id="dbe23-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="dbe23-118">Hola `connection` propiedad debe contener el nombre de Hola de una configuración de aplicación que contiene una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dbe23-118">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="dbe23-119">Hola portal de Azure, Hola editor estándar en hello **integrar** ficha configura esta configuración de aplicación para cuando se selecciona una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="dbe23-119">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="dbe23-120">Cuando se usa un desencadenador de blob en un plan de consumo, puede haber una demora de 10 minutos de tooa en el procesamiento de nuevos blobs después de una aplicación de la función ha quedado inactiva.</span><span class="sxs-lookup"><span data-stu-id="dbe23-120">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="dbe23-121">Después de que se ejecuta la aplicación de la función de hello, blobs se procesan inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="dbe23-121">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="dbe23-122">tooavoid inicial este retraso, considere una de las siguientes opciones de hello:</span><span class="sxs-lookup"><span data-stu-id="dbe23-122">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="dbe23-123">Usar un plan de App Service con Always On habilitado</span><span class="sxs-lookup"><span data-stu-id="dbe23-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="dbe23-124">Utilice otro blob de hello tootrigger mecanismo de procesamiento, por ejemplo, un mensaje de la cola que contiene el nombre del blob Hola.</span><span class="sxs-lookup"><span data-stu-id="dbe23-124">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="dbe23-125">Para ver un ejemplo, consulte [desencadenador de cola con enlace de entrada de blob](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="dbe23-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="dbe23-126">Patrones de nombre</span><span class="sxs-lookup"><span data-stu-id="dbe23-126">Name patterns</span></span>
<span data-ttu-id="dbe23-127">Puede especificar un patrón de nombre de blob en hello `path` propiedad, que puede ser una expresión de filtro o enlace.</span><span class="sxs-lookup"><span data-stu-id="dbe23-127">You can specify a blob name pattern in hello `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="dbe23-128">Consulte [Patrones y expresiones de enlace](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="dbe23-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="dbe23-129">Por ejemplo, tooblobs toofilter que comienzan con hello cadena "original," usar hello después de la definición.</span><span class="sxs-lookup"><span data-stu-id="dbe23-129">For example, toofilter tooblobs that start with hello string "original," use hello following definition.</span></span> <span data-ttu-id="dbe23-130">Esta ruta de acceso busca un blob denominado *original Blob1.txt* en hello *entrada* contenedor y el valor de Hola de hello `name` la variable en el código de la función es `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="dbe23-130">This path finds a blob named *original-Blob1.txt* in hello *input* container, and hello value of hello `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="dbe23-131">extensión y nombre de archivo de blob de toobind toohello por separado, utilizan dos patrones.</span><span class="sxs-lookup"><span data-stu-id="dbe23-131">toobind toohello blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="dbe23-132">Esta ruta de acceso también busca un blob denominado *original Blob1.txt*y el valor de Hola de hello `blobname` y `blobextension` las variables en el código de función son *original Blob1* y *txt*.</span><span class="sxs-lookup"><span data-stu-id="dbe23-132">This path also finds a blob named *original-Blob1.txt*, and hello value of hello `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="dbe23-133">Puede restringir el tipo de archivo de Hola de blobs mediante el uso de un valor fijo para la extensión de archivo Hola.</span><span class="sxs-lookup"><span data-stu-id="dbe23-133">You can restrict hello file type of blobs by using a fixed value for hello file extension.</span></span> <span data-ttu-id="dbe23-134">Por ejemplo, tootrigger solo en los archivos .png, Hola de uso siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="dbe23-134">For instance, tootrigger only on .png files, use hello following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="dbe23-135">Las llaves son caracteres especiales en los patrones de nombre.</span><span class="sxs-lookup"><span data-stu-id="dbe23-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="dbe23-136">nombres de blob de toospecify que tienen las llaves en nombre de hello, puede omitir llaves hello mediante dos llaves.</span><span class="sxs-lookup"><span data-stu-id="dbe23-136">toospecify blob names that have curly braces in hello name, you can escape hello braces using two braces.</span></span> <span data-ttu-id="dbe23-137">Hello en el ejemplo siguiente se busca un blob denominado *{20140101}-soundfile.mp3* en hello *imágenes* hello y contenedor `name` es el valor de la variable en el código de la función hello  *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="dbe23-137">hello following example finds a blob named *{20140101}-soundfile.mp3* in hello *images* container, and hello `name` variable value in hello function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="dbe23-138">Metadatos de desencadenador</span><span class="sxs-lookup"><span data-stu-id="dbe23-138">Trigger metadata</span></span>

<span data-ttu-id="dbe23-139">desencadenador de blob de Hello proporciona varias propiedades de metadatos.</span><span class="sxs-lookup"><span data-stu-id="dbe23-139">hello blob trigger provides several metadata properties.</span></span> <span data-ttu-id="dbe23-140">Estas propiedades pueden usarse como parte de expresiones de enlace en otros enlaces o como parámetros del código.</span><span class="sxs-lookup"><span data-stu-id="dbe23-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="dbe23-141">Estos valores no tienen Hola misma semántica que [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="dbe23-141">These values have hello same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="dbe23-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="dbe23-142">**BlobTrigger**.</span></span> <span data-ttu-id="dbe23-143">Escriba `string`.</span><span class="sxs-lookup"><span data-stu-id="dbe23-143">Type `string`.</span></span> <span data-ttu-id="dbe23-144">ruta de acceso de blob desencadenadora Hola</span><span class="sxs-lookup"><span data-stu-id="dbe23-144">hello triggering blob path</span></span>
- <span data-ttu-id="dbe23-145">**Uri**.</span><span class="sxs-lookup"><span data-stu-id="dbe23-145">**Uri**.</span></span> <span data-ttu-id="dbe23-146">Escriba `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="dbe23-146">Type `System.Uri`.</span></span> <span data-ttu-id="dbe23-147">URI del blob de Hello para la ubicación principal Hola.</span><span class="sxs-lookup"><span data-stu-id="dbe23-147">hello blob's URI for hello primary location.</span></span>
- <span data-ttu-id="dbe23-148">**Properties**.</span><span class="sxs-lookup"><span data-stu-id="dbe23-148">**Properties**.</span></span> <span data-ttu-id="dbe23-149">Escriba `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="dbe23-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="dbe23-150">Hola propiedades del sistema del blob.</span><span class="sxs-lookup"><span data-stu-id="dbe23-150">hello blob's system properties.</span></span>
- <span data-ttu-id="dbe23-151">**Metadata**.</span><span class="sxs-lookup"><span data-stu-id="dbe23-151">**Metadata**.</span></span> <span data-ttu-id="dbe23-152">Escriba `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="dbe23-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="dbe23-153">Hola metadatos definidos por el usuario para blob Hola.</span><span class="sxs-lookup"><span data-stu-id="dbe23-153">hello user-defined metadata for hello blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="dbe23-154">Recepciones de blobs</span><span class="sxs-lookup"><span data-stu-id="dbe23-154">Blob receipts</span></span>
<span data-ttu-id="dbe23-155">en tiempo de ejecución garantiza que ninguna función de desencadenador de blob se llama más de una vez para las funciones de Azure de Hola Hola mismo blob nuevo o actualizado.</span><span class="sxs-lookup"><span data-stu-id="dbe23-155">hello Azure Functions runtime ensures that no blob trigger function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="dbe23-156">toodetermine si se ha procesado una versión determinada de blob, mantiene *blob confirmaciones*.</span><span class="sxs-lookup"><span data-stu-id="dbe23-156">toodetermine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="dbe23-157">Almacenes de funciones de Azure blob confirmaciones en un contenedor denominado *hosts de webjobs de azure* Hola cuenta de almacenamiento de Azure para la aplicación de función (definida por la configuración de la aplicación hello `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="dbe23-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in hello Azure storage account for your function app (defined by hello app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="dbe23-158">Una confirmación de blob tiene Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="dbe23-158">A blob receipt has hello following information:</span></span>

* <span data-ttu-id="dbe23-159">Hola desencadenó función ("*&lt;nombre de la aplicación de función >*. Las funciones.  *&lt;nombre de función >*", por ejemplo:"MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="dbe23-159">hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="dbe23-160">nombre del contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="dbe23-160">hello container name</span></span>
* <span data-ttu-id="dbe23-161">tipo de blob de Hello ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="dbe23-161">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="dbe23-162">nombre del blob Hola</span><span class="sxs-lookup"><span data-stu-id="dbe23-162">hello blob name</span></span>
* <span data-ttu-id="dbe23-163">Hola ETag (un identificador de versión de blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="dbe23-163">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="dbe23-164">tooforce reprocesamiento de un blob, eliminar la confirmación de blob de Hola para ese blob de hello *hosts de webjobs de azure* contenedor manualmente.</span><span class="sxs-lookup"><span data-stu-id="dbe23-164">tooforce reprocessing of a blob, delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="dbe23-165">Control de blobs dudosos</span><span class="sxs-lookup"><span data-stu-id="dbe23-165">Handling poison blobs</span></span>
<span data-ttu-id="dbe23-166">Si se produce un error en una función de desencadenador de blob, Azure Functions vuelve a intentar ejecutar esa función hasta 5 veces de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="dbe23-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="dbe23-167">Si se produce un error en todos los intentos de 5, las funciones de Azure agrega una cola de almacenamiento de tooa mensaje denominada *webjobs-blobtrigger-dudosos*.</span><span class="sxs-lookup"><span data-stu-id="dbe23-167">If all 5 tries fail, Azure Functions adds a message tooa Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="dbe23-168">mensaje de la cola de Hola para blobs dudosos es un objeto JSON que contiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="dbe23-168">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="dbe23-169">FunctionId (en formato de hello  *&lt;nombre de la aplicación de función >*. Las funciones.  *&lt;nombre de función >*)</span><span class="sxs-lookup"><span data-stu-id="dbe23-169">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="dbe23-170">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="dbe23-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="dbe23-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="dbe23-171">ContainerName</span></span>
* <span data-ttu-id="dbe23-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="dbe23-172">BlobName</span></span>
* <span data-ttu-id="dbe23-173">ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="dbe23-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="dbe23-174">Sondeo de blobs en contenedores grandes</span><span class="sxs-lookup"><span data-stu-id="dbe23-174">Blob polling for large containers</span></span>
<span data-ttu-id="dbe23-175">Si el contenedor de blobs de Hola que se está supervisando contiene más de 10.000 blobs, funciones de hello en tiempo de ejecución examina inicie sesión toowatch de archivos para blobs nuevos o modificados.</span><span class="sxs-lookup"><span data-stu-id="dbe23-175">If hello blob container being monitored contains more than 10,000 blobs, hello Functions runtime scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="dbe23-176">Este proceso no se lleva a cabo en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="dbe23-176">This process is not real time.</span></span> <span data-ttu-id="dbe23-177">Una función podría no obtener activada hasta varios minutos o más una vez creado el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="dbe23-177">A function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="dbe23-178">Además, [se crean registros de almacenamiento basados en el principio del "mejor esfuerzo"](/rest/api/storageservices/About-Storage-Analytics-Logging).</span><span class="sxs-lookup"><span data-stu-id="dbe23-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="dbe23-179">No hay ninguna garantía de que todos los eventos se capturen.</span><span class="sxs-lookup"><span data-stu-id="dbe23-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="dbe23-180">En algunos casos, podrían faltar registros.</span><span class="sxs-lookup"><span data-stu-id="dbe23-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="dbe23-181">Si necesita procesamiento de blob más rápida y confiable, considere la posibilidad de crear un [la cola de mensajes](../storage/queues/storage-dotnet-how-to-use-queues.md) cuando creas blob Hola.</span><span class="sxs-lookup"><span data-stu-id="dbe23-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create hello blob.</span></span> <span data-ttu-id="dbe23-182">A continuación, utilice un [desencadenador cola](functions-bindings-storage-queue.md) en lugar de un blob de hello blob tooprocess de desencadenador.</span><span class="sxs-lookup"><span data-stu-id="dbe23-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger tooprocess hello blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="dbe23-183">Uso de un desencadenador de blob y un enlace de entrada</span><span class="sxs-lookup"><span data-stu-id="dbe23-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="dbe23-184">En las funciones. NET, tener acceso a datos de blob de hello mediante un parámetro de método como `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="dbe23-184">In .NET functions, access hello blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="dbe23-185">En este caso, `paramName` es valor Hola especificado en hello [configuración de desencadenador](#trigger).</span><span class="sxs-lookup"><span data-stu-id="dbe23-185">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="dbe23-186">En las funciones de Node.js, Hola de acceso de entrada de datos blob mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="dbe23-186">In Node.js functions, access hello input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="dbe23-187">En. NET, puede enlazar tooany de tipos de hello en la siguiente lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="dbe23-187">In .NET, you can bind tooany of hello types in hello list below.</span></span> <span data-ttu-id="dbe23-188">Si se usan como enlace de entrada, algunos de estos tipos necesitan una dirección de enlace `inout` en *function.json*.</span><span class="sxs-lookup"><span data-stu-id="dbe23-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="dbe23-189">Esta dirección no es compatible con editor estándar de hello, por lo que debe usar Hola advanced editor.</span><span class="sxs-lookup"><span data-stu-id="dbe23-189">This direction is not supported by hello standard editor, so you must use hello advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="dbe23-190">`ICloudBlob` (necesita una dirección de enlace "inout")</span><span class="sxs-lookup"><span data-stu-id="dbe23-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="dbe23-191">`CloudBlockBlob` (necesita una dirección de enlace "inout")</span><span class="sxs-lookup"><span data-stu-id="dbe23-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="dbe23-192">`CloudPageBlob` (necesita una dirección de enlace "inout")</span><span class="sxs-lookup"><span data-stu-id="dbe23-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="dbe23-193">`CloudAppendBlob` (necesita una dirección de enlace "inout")</span><span class="sxs-lookup"><span data-stu-id="dbe23-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="dbe23-194">Si se esperan que los blobs de texto, también puede enlazar tooa .NET `string` tipo.</span><span class="sxs-lookup"><span data-stu-id="dbe23-194">If text blobs are expected, you can also bind tooa .NET `string` type.</span></span> <span data-ttu-id="dbe23-195">Esto solamente se recomienda si el tamaño del blob de hello es pequeño, como contenido de blob completo Hola se carga en memoria.</span><span class="sxs-lookup"><span data-stu-id="dbe23-195">This is only recommended if hello blob size is small, as hello entire blob contents are loaded into memory.</span></span> <span data-ttu-id="dbe23-196">Por lo general, es preferible toouse una `Stream` o `CloudBlockBlob` tipo.</span><span class="sxs-lookup"><span data-stu-id="dbe23-196">Generally, it is preferable toouse a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="dbe23-197">Ejemplo de desencadenador</span><span class="sxs-lookup"><span data-stu-id="dbe23-197">Trigger sample</span></span>
<span data-ttu-id="dbe23-198">Suponga que tiene Hola sigue function.json que define un desencadenador de almacenamiento de blobs:</span><span class="sxs-lookup"><span data-stu-id="dbe23-198">Suppose you have hello following function.json that defines a blob storage trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

<span data-ttu-id="dbe23-199">Vea el ejemplo de específica del lenguaje de Hola que registra el contenido de Hola de cada blob que se agrega toohello supervisado contenedor.</span><span class="sxs-lookup"><span data-stu-id="dbe23-199">See hello language-specific sample that logs hello contents of each blob that is added toohello monitored container.</span></span>

* [<span data-ttu-id="dbe23-200">C#</span><span class="sxs-lookup"><span data-stu-id="dbe23-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="dbe23-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="dbe23-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="dbe23-202">Ejemplos de desencadenador de blobs en C#</span><span class="sxs-lookup"><span data-stu-id="dbe23-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="dbe23-203">Ejemplo de desencadenador en Node.js</span><span class="sxs-lookup"><span data-stu-id="dbe23-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="dbe23-204">Uso de un enlace de salida de blob</span><span class="sxs-lookup"><span data-stu-id="dbe23-204">Using a blob output binding</span></span>

<span data-ttu-id="dbe23-205">En las funciones. NET, debe utilizar un `out string` parámetro en la firma de la función o usar uno de los tipos de Hola Hola lista siguiente.</span><span class="sxs-lookup"><span data-stu-id="dbe23-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of hello types in hello following list.</span></span> <span data-ttu-id="dbe23-206">En las funciones de Node.js, accederás a Hola salida blob mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="dbe23-206">In Node.js functions, you access hello output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="dbe23-207">En las funciones de .NET puede producir tooany de hello siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="dbe23-207">In .NET functions you can output tooany of hello following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="dbe23-208">Ejemplo de desencadenador de cola con entrada y salida de blob</span><span class="sxs-lookup"><span data-stu-id="dbe23-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="dbe23-209">Suponga que tiene Hola después function.json, que define un [desencadenador de almacenamiento de cola](functions-bindings-storage-queue.md), un almacenamiento de blobs de entrada y salida de un almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="dbe23-209">Suppose you have hello following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="dbe23-210">Uso de Hola de aviso de hello `queueTrigger` propiedad de metadatos.</span><span class="sxs-lookup"><span data-stu-id="dbe23-210">Notice hello use of hello `queueTrigger` metadata property.</span></span> <span data-ttu-id="dbe23-211">Hola BLOB de entrada y salida `path` propiedades:</span><span class="sxs-lookup"><span data-stu-id="dbe23-211">in hello blob input and output `path` properties:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="dbe23-212">Vea el ejemplo de específica del lenguaje de Hola que copia Hola blob de entrada toohello salida blob.</span><span class="sxs-lookup"><span data-stu-id="dbe23-212">See hello language-specific sample that copies hello input blob toohello output blob.</span></span>

* [<span data-ttu-id="dbe23-213">C#</span><span class="sxs-lookup"><span data-stu-id="dbe23-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="dbe23-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="dbe23-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="dbe23-215">Ejemplo de enlace de blob en C#</span><span class="sxs-lookup"><span data-stu-id="dbe23-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="dbe23-216">Ejemplo de enlace de blob en Node.js</span><span class="sxs-lookup"><span data-stu-id="dbe23-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="dbe23-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dbe23-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

