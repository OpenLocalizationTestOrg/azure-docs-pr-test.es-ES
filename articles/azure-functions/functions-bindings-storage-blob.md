---
title: Enlaces de Blob Storage en Azure Functions | Microsoft Docs
description: "Descubra cómo utilizar desencadenadores y enlaces de almacenamiento de Azure en funciones de Azure."
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
ms.openlocfilehash: 8d8f510ec906c0e0420ec48d45d88b93c144658a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="f3634-104">Enlaces de Blob Storage en Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f3634-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="f3634-105">En este artículo se explica cómo configurar enlaces de Azure Blob Storage y trabajar con ellos en Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f3634-105">This article explains how to configure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="f3634-106">Azure Functions admite enlaces de desencadenador, entrada y salida para Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f3634-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="f3634-107">Para las características que estén disponibles en todos los enlaces, consulte [conceptos sobre desencadenadores y enlaces de Azure Functions](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="f3634-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="f3634-108">No se admite una [cuenta de almacenamiento solo de blob](../storage/common/storage-create-storage-account.md#blob-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="f3634-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="f3634-109">Los desencadenadores y enlaces de Blob Storage necesitan una cuenta de almacenamiento de uso general.</span><span class="sxs-lookup"><span data-stu-id="f3634-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="f3634-110">Desencadenadores y enlaces de Blob Storage</span><span class="sxs-lookup"><span data-stu-id="f3634-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="f3634-111">Al usar el desencadenador de Azure Blob Storage, se llama al código de la función cuando se detecte un blob nuevo o actualizado.</span><span class="sxs-lookup"><span data-stu-id="f3634-111">Using the Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="f3634-112">El contenido del blob se proporciona a modo de entrada para la función.</span><span class="sxs-lookup"><span data-stu-id="f3634-112">The blob contents are provided as input to the function.</span></span>

<span data-ttu-id="f3634-113">Defina un desencadenador de Blob Storage con la pestaña **Integrar** del portal de Functions.</span><span class="sxs-lookup"><span data-stu-id="f3634-113">Define a blob storage trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="f3634-114">El portal crea la siguiente definición en la sección de **enlaces** de *function.json*:</span><span class="sxs-lookup"><span data-stu-id="f3634-114">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<The name used to identify the trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container to monitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="f3634-115">Los enlaces de entrada y salida de blob se definen con `blob` como tipo de enlace:</span><span class="sxs-lookup"><span data-stu-id="f3634-115">Blob input and output bindings are defined using `blob` as the binding type:</span></span>

```json
{
  "name": "<The name used to identify the blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="f3634-116">La propiedad `path` admite las expresiones de enlace y los parámetros de filtrado.</span><span class="sxs-lookup"><span data-stu-id="f3634-116">The `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="f3634-117">Consulte [Patrones de nombre](#pattern).</span><span class="sxs-lookup"><span data-stu-id="f3634-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="f3634-118">La propiedad `connection` debe contener el nombre de una configuración de aplicación que contenga una cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3634-118">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="f3634-119">En Azure Portal, el editor estándar de la pestaña **Integrar** permite modificar esta configuración de aplicación al seleccionar una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3634-119">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="f3634-120">Al usar un desencadenador de blobs en un plan de consumo, puede haber un retraso de hasta 10 minutos en el procesamiento de nuevos blobs después de que una aplicación de función quede inactiva.</span><span class="sxs-lookup"><span data-stu-id="f3634-120">When you're using a blob trigger on a Consumption plan, there can be up to a 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="f3634-121">Después de que se ejecute la aplicación de función, los blobs se procesan inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="f3634-121">After the function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="f3634-122">Para evitar este retraso inicial, considere una de las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="f3634-122">To avoid this initial delay, consider one of the following options:</span></span>
> - <span data-ttu-id="f3634-123">Usar un plan de App Service con Always On habilitado</span><span class="sxs-lookup"><span data-stu-id="f3634-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="f3634-124">Usar otro mecanismo para desencadenar el procesamiento de blobs, por ejemplo, un mensaje de la cola que contenga el nombre del blob</span><span class="sxs-lookup"><span data-stu-id="f3634-124">Use another mechanism to trigger the blob processing, such as a queue message that contains the blob name.</span></span> <span data-ttu-id="f3634-125">Para ver un ejemplo, consulte [desencadenador de cola con enlace de entrada de blob](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="f3634-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="f3634-126">Patrones de nombre</span><span class="sxs-lookup"><span data-stu-id="f3634-126">Name patterns</span></span>
<span data-ttu-id="f3634-127">Puede especificar un patrón de nombre de blob en la propiedad `path`, que puede ser una expresión de filtro o de enlace.</span><span class="sxs-lookup"><span data-stu-id="f3634-127">You can specify a blob name pattern in the `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="f3634-128">Consulte [Patrones y expresiones de enlace](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="f3634-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="f3634-129">Por ejemplo, para filtrar blobs que empiecen por la cadena "original", use la siguiente definición.</span><span class="sxs-lookup"><span data-stu-id="f3634-129">For example, to filter to blobs that start with the string "original," use the following definition.</span></span> <span data-ttu-id="f3634-130">Esta ruta de acceso encuentra un blob llamado *original-Blob1.txt* en el contenedor *input* y el valor de la variable `name` en el código de la función es `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="f3634-130">This path finds a blob named *original-Blob1.txt* in the *input* container, and the value of the `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="f3634-131">Para enlazar el nombre de archivo del blob y la extensión por separado, use dos patrones.</span><span class="sxs-lookup"><span data-stu-id="f3634-131">To bind to the blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="f3634-132">Esta ruta de acceso también encuentra un blob llamado *original-Blob1.txt* y el valor de las variables `blobname` y `blobextension` del código de la función son *original-Blob1* y *txt*.</span><span class="sxs-lookup"><span data-stu-id="f3634-132">This path also finds a blob named *original-Blob1.txt*, and the value of the `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="f3634-133">Puede restringir el tipo de archivo de los blobs mediante el uso de un valor fijo para la extensión de archivo.</span><span class="sxs-lookup"><span data-stu-id="f3634-133">You can restrict the file type of blobs by using a fixed value for the file extension.</span></span> <span data-ttu-id="f3634-134">Por ejemplo, para realizar desencadenamientos solo en archivos .png, use el siguiente patrón:</span><span class="sxs-lookup"><span data-stu-id="f3634-134">For instance, to trigger only on .png files, use the following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="f3634-135">Las llaves son caracteres especiales en los patrones de nombre.</span><span class="sxs-lookup"><span data-stu-id="f3634-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="f3634-136">Para especificar nombres de blob que tengan llaves, puede omitirlas mediante dos llaves.</span><span class="sxs-lookup"><span data-stu-id="f3634-136">To specify blob names that have curly braces in the name, you can escape the braces using two braces.</span></span> <span data-ttu-id="f3634-137">En el siguiente ejemplo, se encuentra un blob llamado *{20140101}-soundfile.mp3* en el contenedor *images* y el valor de la variable `name` del código de la función es *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="f3634-137">The following example finds a blob named *{20140101}-soundfile.mp3* in the *images* container, and the `name` variable value in the function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="f3634-138">Metadatos de desencadenador</span><span class="sxs-lookup"><span data-stu-id="f3634-138">Trigger metadata</span></span>

<span data-ttu-id="f3634-139">El desencadenador de blobs proporciona varias propiedades de metadatos.</span><span class="sxs-lookup"><span data-stu-id="f3634-139">The blob trigger provides several metadata properties.</span></span> <span data-ttu-id="f3634-140">Estas propiedades pueden usarse como parte de expresiones de enlace en otros enlaces o como parámetros del código.</span><span class="sxs-lookup"><span data-stu-id="f3634-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="f3634-141">Estos valores tienen la misma semántica que [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="f3634-141">These values have the same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="f3634-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="f3634-142">**BlobTrigger**.</span></span> <span data-ttu-id="f3634-143">Escriba `string`.</span><span class="sxs-lookup"><span data-stu-id="f3634-143">Type `string`.</span></span> <span data-ttu-id="f3634-144">Es la ruta de acceso del blob de desencadenamiento.</span><span class="sxs-lookup"><span data-stu-id="f3634-144">The triggering blob path</span></span>
- <span data-ttu-id="f3634-145">**Uri**.</span><span class="sxs-lookup"><span data-stu-id="f3634-145">**Uri**.</span></span> <span data-ttu-id="f3634-146">Escriba `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="f3634-146">Type `System.Uri`.</span></span> <span data-ttu-id="f3634-147">Es el identificador URI del blob correspondiente a la ubicación principal.</span><span class="sxs-lookup"><span data-stu-id="f3634-147">The blob's URI for the primary location.</span></span>
- <span data-ttu-id="f3634-148">**Properties**.</span><span class="sxs-lookup"><span data-stu-id="f3634-148">**Properties**.</span></span> <span data-ttu-id="f3634-149">Escriba `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="f3634-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="f3634-150">Son las propiedades del sistema del blob.</span><span class="sxs-lookup"><span data-stu-id="f3634-150">The blob's system properties.</span></span>
- <span data-ttu-id="f3634-151">**Metadata**.</span><span class="sxs-lookup"><span data-stu-id="f3634-151">**Metadata**.</span></span> <span data-ttu-id="f3634-152">Escriba `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="f3634-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="f3634-153">Son los metadatos definidos por el usuario para el blob.</span><span class="sxs-lookup"><span data-stu-id="f3634-153">The user-defined metadata for the blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="f3634-154">Recepciones de blobs</span><span class="sxs-lookup"><span data-stu-id="f3634-154">Blob receipts</span></span>
<span data-ttu-id="f3634-155">El entorno en tiempo de ejecución de Azure Functions garantiza que no se llame más de una vez a ninguna función de desencadenador de blobs para un mismo blob, ya sea nuevo o actualizado.</span><span class="sxs-lookup"><span data-stu-id="f3634-155">The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="f3634-156">Mantiene *recepciones de blobs* para determinar si se ha procesado una determinada versión de blob.</span><span class="sxs-lookup"><span data-stu-id="f3634-156">To determine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="f3634-157">Azure Functions almacena confirmaciones de blobs en un contenedor llamado *azure-webjobs-hosts* en la cuenta de almacenamiento de Azure de la aplicación de función (que se especifica mediante la configuración de la aplicación `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="f3634-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="f3634-158">Una recepción de blobs tiene la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="f3634-158">A blob receipt has the following information:</span></span>

* <span data-ttu-id="f3634-159">La función desencadenada ("*&lt;nombre de aplicación de función>*.Functions.*&lt;nombre de función>*", por ejemplo: "MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="f3634-159">The triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="f3634-160">El nombre del contenedor</span><span class="sxs-lookup"><span data-stu-id="f3634-160">The container name</span></span>
* <span data-ttu-id="f3634-161">El tipo de blob ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="f3634-161">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="f3634-162">El nombre del blob</span><span class="sxs-lookup"><span data-stu-id="f3634-162">The blob name</span></span>
* <span data-ttu-id="f3634-163">ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="f3634-163">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="f3634-164">Si desea forzar el reprocesamiento de un blob, puede eliminar manualmente la recepción de ese blob desde el contenedor *azure-webjobs-hosts* .</span><span class="sxs-lookup"><span data-stu-id="f3634-164">To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="f3634-165">Control de blobs dudosos</span><span class="sxs-lookup"><span data-stu-id="f3634-165">Handling poison blobs</span></span>
<span data-ttu-id="f3634-166">Si se produce un error en una función de desencadenador de blob, Azure Functions vuelve a intentar ejecutar esa función hasta 5 veces de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f3634-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="f3634-167">Si se produce un error en los 5 intentos, Azure Functions agregará un mensaje a una cola de Storage llamada *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="f3634-167">If all 5 tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="f3634-168">El mensaje de cola para los blobs dudosos es un objeto JSON que contiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="f3634-168">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="f3634-169">FunctionId (con el formato *&lt;nombre de aplicación de función>*.Functions.*&lt;nombre de función>*)</span><span class="sxs-lookup"><span data-stu-id="f3634-169">FunctionId (in the format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="f3634-170">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="f3634-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="f3634-171">ContainerName</span><span class="sxs-lookup"><span data-stu-id="f3634-171">ContainerName</span></span>
* <span data-ttu-id="f3634-172">BlobName</span><span class="sxs-lookup"><span data-stu-id="f3634-172">BlobName</span></span>
* <span data-ttu-id="f3634-173">ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="f3634-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="f3634-174">Sondeo de blobs en contenedores grandes</span><span class="sxs-lookup"><span data-stu-id="f3634-174">Blob polling for large containers</span></span>
<span data-ttu-id="f3634-175">Si el contenedor de blobs supervisado contiene más de 10 000 blobs, el entorno en tiempo de ejecución de Functions examinará los archivos de registro para detectar blobs nuevos o modificados.</span><span class="sxs-lookup"><span data-stu-id="f3634-175">If the blob container being monitored contains more than 10,000 blobs, the Functions runtime scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="f3634-176">Este proceso no se lleva a cabo en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="f3634-176">This process is not real time.</span></span> <span data-ttu-id="f3634-177">Una función podría tardar en desencadenarse varios minutos o más después de crear el blob.</span><span class="sxs-lookup"><span data-stu-id="f3634-177">A function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="f3634-178">Además, [se crean registros de almacenamiento basados en el principio del "mejor esfuerzo"](/rest/api/storageservices/About-Storage-Analytics-Logging).</span><span class="sxs-lookup"><span data-stu-id="f3634-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="f3634-179">No hay ninguna garantía de que todos los eventos se capturen.</span><span class="sxs-lookup"><span data-stu-id="f3634-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="f3634-180">En algunos casos, podrían faltar registros.</span><span class="sxs-lookup"><span data-stu-id="f3634-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="f3634-181">Si necesita un procesamiento de blobs más rápido o confiable, considere crear un [mensaje de cola](../storage/queues/storage-dotnet-how-to-use-queues.md) al crear el blob.</span><span class="sxs-lookup"><span data-stu-id="f3634-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create the blob.</span></span> <span data-ttu-id="f3634-182">A continuación, use un [desencadenador de cola](functions-bindings-storage-queue.md) en lugar de un desencadenador de blob para procesar el blob.</span><span class="sxs-lookup"><span data-stu-id="f3634-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger to process the blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="f3634-183">Uso de un desencadenador de blob y un enlace de entrada</span><span class="sxs-lookup"><span data-stu-id="f3634-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="f3634-184">En las funciones de .NET, acceda a los datos del blob mediante un parámetro de método como `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="f3634-184">In .NET functions, access the blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="f3634-185">Aquí, `paramName` es el valor que especificó en la [configuración del desencadenador](#trigger).</span><span class="sxs-lookup"><span data-stu-id="f3634-185">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="f3634-186">En las funciones de Node.js, acceda a los datos de entrada del blob mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f3634-186">In Node.js functions, access the input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="f3634-187">En. NET, puede crear enlaces a cualquiera de los tipos de la siguiente lista.</span><span class="sxs-lookup"><span data-stu-id="f3634-187">In .NET, you can bind to any of the types in the list below.</span></span> <span data-ttu-id="f3634-188">Si se usan como enlace de entrada, algunos de estos tipos necesitan una dirección de enlace `inout` en *function.json*.</span><span class="sxs-lookup"><span data-stu-id="f3634-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="f3634-189">El editor estándar no admite esta dirección, por lo que debe usar el avanzado.</span><span class="sxs-lookup"><span data-stu-id="f3634-189">This direction is not supported by the standard editor, so you must use the advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="f3634-190">`ICloudBlob` (necesita una dirección de enlace "inout")</span><span class="sxs-lookup"><span data-stu-id="f3634-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="f3634-191">`CloudBlockBlob` (necesita una dirección de enlace "inout")</span><span class="sxs-lookup"><span data-stu-id="f3634-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="f3634-192">`CloudPageBlob` (necesita una dirección de enlace "inout")</span><span class="sxs-lookup"><span data-stu-id="f3634-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="f3634-193">`CloudAppendBlob` (necesita una dirección de enlace "inout")</span><span class="sxs-lookup"><span data-stu-id="f3634-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="f3634-194">Si se esperan blobs de texto, también puede realizar el enlace a un tipo `string` de .NET.</span><span class="sxs-lookup"><span data-stu-id="f3634-194">If text blobs are expected, you can also bind to a .NET `string` type.</span></span> <span data-ttu-id="f3634-195">Solo se recomienda hacerlo si los blobs son pequeños, ya que todos sus contenidos se cargan en memoria.</span><span class="sxs-lookup"><span data-stu-id="f3634-195">This is only recommended if the blob size is small, as the entire blob contents are loaded into memory.</span></span> <span data-ttu-id="f3634-196">Por lo general, es preferible usar un tipo `Stream` o `CloudBlockBlob`.</span><span class="sxs-lookup"><span data-stu-id="f3634-196">Generally, it is preferable to use a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="f3634-197">Ejemplo de desencadenador</span><span class="sxs-lookup"><span data-stu-id="f3634-197">Trigger sample</span></span>
<span data-ttu-id="f3634-198">Suponga que tiene el siguiente elemento function.json que define un desencadenador de Blob Storage:</span><span class="sxs-lookup"><span data-stu-id="f3634-198">Suppose you have the following function.json that defines a blob storage trigger:</span></span>

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

<span data-ttu-id="f3634-199">Consulte el ejemplo de código específico del lenguaje que registra el contenido de cada blob que se agrega al contenedor supervisado.</span><span class="sxs-lookup"><span data-stu-id="f3634-199">See the language-specific sample that logs the contents of each blob that is added to the monitored container.</span></span>

* [<span data-ttu-id="f3634-200">C#</span><span class="sxs-lookup"><span data-stu-id="f3634-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="f3634-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="f3634-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="f3634-202">Ejemplos de desencadenador de blobs en C#</span><span class="sxs-lookup"><span data-stu-id="f3634-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding to a CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="f3634-203">Ejemplo de desencadenador en Node.js</span><span class="sxs-lookup"><span data-stu-id="f3634-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="f3634-204">Uso de un enlace de salida de blob</span><span class="sxs-lookup"><span data-stu-id="f3634-204">Using a blob output binding</span></span>

<span data-ttu-id="f3634-205">En las funciones de .NET, debería usar un parámetro `out string` en la firma de la función o usar uno de los tipos de la siguiente lista.</span><span class="sxs-lookup"><span data-stu-id="f3634-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of the types in the following list.</span></span> <span data-ttu-id="f3634-206">En las funciones de Node.js, puede obtener acceso al blob de salida mediante `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="f3634-206">In Node.js functions, you access the output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="f3634-207">En las funciones de .NET, puede enviar a la salida cualquiera de los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="f3634-207">In .NET functions you can output to any of the following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="f3634-208">Ejemplo de desencadenador de cola con entrada y salida de blob</span><span class="sxs-lookup"><span data-stu-id="f3634-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="f3634-209">Suponga que tiene el siguiente elemento function.json, que define un [desencadenador de Queue Storage](functions-bindings-storage-queue.md) y una entrada y una salida de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f3634-209">Suppose you have the following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="f3634-210">Tenga en cuenta el uso de la propiedad de metadatos `queueTrigger`.</span><span class="sxs-lookup"><span data-stu-id="f3634-210">Notice the use of the `queueTrigger` metadata property.</span></span> <span data-ttu-id="f3634-211">en las propiedades de entrada y salida de blob `path`:</span><span class="sxs-lookup"><span data-stu-id="f3634-211">in the blob input and output `path` properties:</span></span>

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

<span data-ttu-id="f3634-212">Vea el ejemplo específico del lenguaje que copia el blob de entrada en el blob de salida.</span><span class="sxs-lookup"><span data-stu-id="f3634-212">See the language-specific sample that copies the input blob to the output blob.</span></span>

* [<span data-ttu-id="f3634-213">C#</span><span class="sxs-lookup"><span data-stu-id="f3634-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="f3634-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="f3634-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="f3634-215">Ejemplo de enlace de blob en C#</span><span class="sxs-lookup"><span data-stu-id="f3634-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input to output, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="f3634-216">Ejemplo de enlace de blob en Node.js</span><span class="sxs-lookup"><span data-stu-id="f3634-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input to output, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="f3634-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3634-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

