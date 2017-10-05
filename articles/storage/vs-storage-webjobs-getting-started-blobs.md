---
title: "Introducción al almacenamiento de blobs y servicios conectados de Visual Studio (proyectos de WebJobs) | Microsoft Docs"
description: "Cómo empezar a usar el almacenamiento de blobs en un proyecto de WebJob después de conectarse a un almacenamiento de Azure con los servicios conectados de Visual Studio."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 7fec890590302a99bbc96f46f24ae440c041580c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="db96c-103">Introducción al almacenamiento de blobs de Azure y servicios conectados de Visual Studio (proyectos de WebJobs)</span><span class="sxs-lookup"><span data-stu-id="db96c-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="db96c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="db96c-104">Overview</span></span>
<span data-ttu-id="db96c-105">En esta guía se proporcionan muestras de código C# que muestran cómo desencadenar un proceso cuando se crea o actualiza un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="db96c-105">This article provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="db96c-106">Los ejemplos de código usan el [SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="db96c-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="db96c-107">Al agregar una cuenta de almacenamiento a un proyecto de WebJobs con el cuadro de diálogo **Agregar servicios conectados** de Visual Studio, se instala el paquete de NuGet de Almacenamiento de Azure adecuado, se agregan las referencias de .NET adecuadas al proyecto y se actualizan las cadenas de conexión para la cuenta de almacenamiento en el archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="db96c-107">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet package is installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>

## <a name="how-to-trigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="db96c-108">Cómo desencadenar una función cuando se crea o actualiza un blob</span><span class="sxs-lookup"><span data-stu-id="db96c-108">How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="db96c-109">En esta sección se muestra cómo usar el atributo **BlobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="db96c-109">This section shows how to use the **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="db96c-110">**Nota:** el SDK de WebJobs analiza los archivos de registro para inspeccionar los blobs nuevos o modificados.</span><span class="sxs-lookup"><span data-stu-id="db96c-110">**Note:** The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="db96c-111">Este proceso es lento por naturaleza; podría no desencadenarse una función hasta varios minutos o más después de haberse creado el blob.</span><span class="sxs-lookup"><span data-stu-id="db96c-111">This process is inherently slow; a function might not get triggered until several minutes or longer after the blob is created.</span></span>  <span data-ttu-id="db96c-112">Si su aplicación necesita procesar inmediatamente los blobs, el método recomendado es crear un mensaje en cola al crear el blob y usar el atributo [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) en lugar del atributo **BlobTrigger** en la función que procesa el blob.</span><span class="sxs-lookup"><span data-stu-id="db96c-112">If your application needs to process blobs immediately, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the **BlobTrigger** attribute on the function that processes the blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="db96c-113">Único marcador de posición para el nombre de blob con extensión</span><span class="sxs-lookup"><span data-stu-id="db96c-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="db96c-114">El siguiente ejemplo de código copia blobs de texto que aparecen en el contenedor *input* al contenedor *output*:</span><span class="sxs-lookup"><span data-stu-id="db96c-114">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="db96c-115">El constructor de atributo toma un parámetro de cadena que especifica el nombre del contenedor y un marcador de posición para el nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="db96c-115">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="db96c-116">En este ejemplo, si se crea un blob llamado *Blob1.txt* en el contenedor *input*, la función crea un blob llamado *Blob1.txt* en el contenedor *output*.</span><span class="sxs-lookup"><span data-stu-id="db96c-116">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="db96c-117">Puede especificar un patrón de nombre con el marcador de posición de nombre de blob, como se muestra en el siguiente ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="db96c-117">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="db96c-118">Este código solo copia blobs con nombres que comienzan con "original-".</span><span class="sxs-lookup"><span data-stu-id="db96c-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="db96c-119">Por ejemplo, *original-Blob1.txt* en el contenedor *input* se copia en *copy- Blob1.txt* en el contenedor *output*.</span><span class="sxs-lookup"><span data-stu-id="db96c-119">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="db96c-120">Si necesita especificar un patrón de nombre para nombres de blob que contienen llaves en el nombre, duplique las llaves.</span><span class="sxs-lookup"><span data-stu-id="db96c-120">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="db96c-121">Por ejemplo, si desea encontrar blobs en el contenedor *images* que tengan nombres como este:</span><span class="sxs-lookup"><span data-stu-id="db96c-121">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="db96c-122">use esto para el patrón:</span><span class="sxs-lookup"><span data-stu-id="db96c-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="db96c-123">En el ejemplo, el valor de marcador de posición *name* sería *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="db96c-123">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="db96c-124">Separar marcadores de posición de extensión y nombre de blob</span><span class="sxs-lookup"><span data-stu-id="db96c-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="db96c-125">El siguiente ejemplo de código cambia la extensión de archivo cuando copia los blobs que aparecen en el contenedor *input* al contenedor *output*.</span><span class="sxs-lookup"><span data-stu-id="db96c-125">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="db96c-126">El código registra la extensión del blob *input* y establece la extensión del blob *output* en *.txt*.</span><span class="sxs-lookup"><span data-stu-id="db96c-126">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <a name="types-that-you-can-bind-to-blobs"></a><span data-ttu-id="db96c-127">Tipos que puede enlazar a blobs</span><span class="sxs-lookup"><span data-stu-id="db96c-127">Types that you can bind to blobs</span></span>
<span data-ttu-id="db96c-128">Puede usar el atributo **BlobTrigger** en los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="db96c-128">You can use the **BlobTrigger** attribute on the following types:</span></span>

* <span data-ttu-id="db96c-129">**cadena**</span><span class="sxs-lookup"><span data-stu-id="db96c-129">**string**</span></span>
* <span data-ttu-id="db96c-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="db96c-130">**TextReader**</span></span>
* <span data-ttu-id="db96c-131">**Stream**</span><span class="sxs-lookup"><span data-stu-id="db96c-131">**Stream**</span></span>
* <span data-ttu-id="db96c-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="db96c-132">**ICloudBlob**</span></span>
* <span data-ttu-id="db96c-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="db96c-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="db96c-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="db96c-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="db96c-135">Otros tipos deserializados por [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="db96c-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="db96c-136">Si quiere trabajar directamente con la cuenta de almacenamiento de Azure, también puede agregar un parámetro **CloudStorageAccount** a la firma del método.</span><span class="sxs-lookup"><span data-stu-id="db96c-136">If you want to work directly with the Azure storage account, you can also add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-to-string"></a><span data-ttu-id="db96c-137">Obtención del contenido del blob de texto enlazando a la cadena</span><span class="sxs-lookup"><span data-stu-id="db96c-137">Getting text blob content by binding to string</span></span>
<span data-ttu-id="db96c-138">Si se esperan blobs de texto, se puede aplicar **BlobTrigger** a un parámetro **string**.</span><span class="sxs-lookup"><span data-stu-id="db96c-138">If text blobs are expected, **BlobTrigger** can be applied to a **string** parameter.</span></span> <span data-ttu-id="db96c-139">El siguiente ejemplo de código enlaza un blob de texto a un parámetro **string** llamado **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="db96c-139">The following code sample binds a text blob to a **string** parameter named **logMessage**.</span></span> <span data-ttu-id="db96c-140">La función usa ese parámetro para escribir el contenido del blob en el panel del SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="db96c-140">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="db96c-141">Obtención del contenido del blob serializado mediante el uso de ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="db96c-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="db96c-142">El siguiente ejemplo de código usa una clase que implementa **ICloudBlobStreamBinder** para permitir que el atributo **BlobTrigger** vincule un blob al tipo **WebImage**.</span><span class="sxs-lookup"><span data-stu-id="db96c-142">The following code sample uses a class that implements **ICloudBlobStreamBinder** to enable the **BlobTrigger** attribute to bind a blob to the **WebImage** type.</span></span>

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK",
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

<span data-ttu-id="db96c-143">El código de enlace **WebImage** se ofrece en una clase **WebImageBinder** que deriva de **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="db96c-143">The **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input,
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="how-to-handle-poison-blobs"></a><span data-ttu-id="db96c-144">Cómo administrar los blobs dudosos</span><span class="sxs-lookup"><span data-stu-id="db96c-144">How to handle poison blobs</span></span>
<span data-ttu-id="db96c-145">Cuando una función **BlobTrigger** genera un error, el SDK le llama de nuevo en el caso de que se hubiese producido por un error transitorio.</span><span class="sxs-lookup"><span data-stu-id="db96c-145">When a **BlobTrigger** function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="db96c-146">Si el error se produce debido al contenido del blob, la función presentará un error cada vez que intente procesar el blob.</span><span class="sxs-lookup"><span data-stu-id="db96c-146">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="db96c-147">De manera predeterminada, el SDK llama una función hasta cinco veces para un blob determinado.</span><span class="sxs-lookup"><span data-stu-id="db96c-147">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="db96c-148">Si el quinto intento falla, el SDK agrega un mensaje a una cola llamada *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="db96c-148">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="db96c-149">Es posible configurar el número máximo de reintentos.</span><span class="sxs-lookup"><span data-stu-id="db96c-149">The maximum number of retries is configurable.</span></span> <span data-ttu-id="db96c-150">Se usa la misma configuración [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) para controlar los blobs dudosos y los mensajes de cola dudosos.</span><span class="sxs-lookup"><span data-stu-id="db96c-150">The same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="db96c-151">El mensaje de cola para los blobs dudosos es un objeto JSON que contiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="db96c-151">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="db96c-152">FunctionId (con el formato *{nombre de WebJob}*.Functions.*{nombre de función}*, por ejemplo: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="db96c-152">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="db96c-153">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="db96c-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="db96c-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="db96c-154">ContainerName</span></span>
* <span data-ttu-id="db96c-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="db96c-155">BlobName</span></span>
* <span data-ttu-id="db96c-156">ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="db96c-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="db96c-157">En el siguiente ejemplo de código, la función **CopyBlob** tiene un código que hace que presente un error cada vez que se la llama.</span><span class="sxs-lookup"><span data-stu-id="db96c-157">In the following code sample, the **CopyBlob** function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="db96c-158">Una vez que el SDK la llama por el número máximo de reintentos, se crea un mensaje en la cola de blobs dudosos y la función **LogPoisonBlob** procesa ese mensaje.</span><span class="sxs-lookup"><span data-stu-id="db96c-158">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the **LogPoisonBlob** function.</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

<span data-ttu-id="db96c-159">El SDK deserializa automáticamente el mensaje JSON.</span><span class="sxs-lookup"><span data-stu-id="db96c-159">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="db96c-160">Esta es la clase **PoisonBlobMessage** :</span><span class="sxs-lookup"><span data-stu-id="db96c-160">Here is the **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="db96c-161">Algoritmo de sondeo de blobs</span><span class="sxs-lookup"><span data-stu-id="db96c-161">Blob polling algorithm</span></span>
<span data-ttu-id="db96c-162">El SDK de WebJobs examina todos los contenedores especificados por los atributos **BlobTrigger** en el inicio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="db96c-162">The WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="db96c-163">En una cuenta de almacenamiento de gran tamaño, este análisis puede demorar un tiempo, por lo que podría pasar mucho tiempo antes de que se encuentren blobs nuevos y que se ejecuten las funciones **BlobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="db96c-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="db96c-164">Para detectar blobs nuevos o cambiados después del inicio de la aplicación, el SDK lee de manera periódica de los registros de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="db96c-164">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="db96c-165">Los registros de blobs se almacenan en búfer y solo se escriben físicamente cada diez minutos aproximadamente, por lo que puede haber un retraso importante una vez que se crea o actualiza un blob antes de que la función **BlobTrigger** correspondiente se ejecute.</span><span class="sxs-lookup"><span data-stu-id="db96c-165">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="db96c-166">Existe una excepción para los blobs que crea mediante el uso del atributo **Blob** .</span><span class="sxs-lookup"><span data-stu-id="db96c-166">There is an exception for blobs that you create by using the **Blob** attribute.</span></span> <span data-ttu-id="db96c-167">Cuando el SDK de WebJobs crea un blob nuevo, pasa el blob nuevo inmediatamente a cualquier función **BlobTrigger** coincidente.</span><span class="sxs-lookup"><span data-stu-id="db96c-167">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching **BlobTrigger** functions.</span></span> <span data-ttu-id="db96c-168">Por tanto, si tiene una cadena de entradas y salidas categorizadas como blob, el SDK puede procesarlas de manera eficaz.</span><span class="sxs-lookup"><span data-stu-id="db96c-168">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="db96c-169">Pero si desea baja latencia de ejecución para sus funciones de procesamiento de blobs para blobs que se crean o actualizan mediante otros medios, se recomienda usar **QueueTrigger** en lugar de **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="db96c-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="db96c-170">Recepciones de blobs</span><span class="sxs-lookup"><span data-stu-id="db96c-170">Blob receipts</span></span>
<span data-ttu-id="db96c-171">El SDK de WebJobs se asegura de que ninguna función **BlobTrigger** se llame más de una vez para el mismo blob nuevo o actualizado.</span><span class="sxs-lookup"><span data-stu-id="db96c-171">The WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="db96c-172">Para hacerlo, mantiene *recepciones de blobs* para determinar si se ha procesado alguna versión de blob determinada.</span><span class="sxs-lookup"><span data-stu-id="db96c-172">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="db96c-173">Las recepciones de blobs se almacenan en un contenedor llamado *azure-webjobs-hosts* en la cuenta de almacenamiento de Azure que especifica la cadena de conexión AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="db96c-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="db96c-174">Una recepción de blobs tiene la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="db96c-174">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="db96c-175">La función que se llamó para el blob ("*{nombre de WebJob}*.Functions.*{nombre de función}*", por ejemplo: "WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="db96c-175">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="db96c-176">El nombre del contenedor</span><span class="sxs-lookup"><span data-stu-id="db96c-176">The container name</span></span>
* <span data-ttu-id="db96c-177">El tipo de blob ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="db96c-177">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="db96c-178">El nombre del blob</span><span class="sxs-lookup"><span data-stu-id="db96c-178">The blob name</span></span>
* <span data-ttu-id="db96c-179">ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="db96c-179">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="db96c-180">Si desea forzar el reprocesamiento de un blob, puede eliminar manualmente la recepción de blob de ese blob desde el contenedor *azure-webjobs-hosts* .</span><span class="sxs-lookup"><span data-stu-id="db96c-180">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-the-queues-article"></a><span data-ttu-id="db96c-181">Temas relacionados tratados en el artículo sobre colas</span><span class="sxs-lookup"><span data-stu-id="db96c-181">Related topics covered by the queues article</span></span>
<span data-ttu-id="db96c-182">Para obtener información sobre cómo controlar el procesamiento de blobs desencadenado por un mensaje de cola o para ver los escenarios de SDK de WebJobs no específicos para el procesamiento de blobs, consulte [Cómo usar el almacenamiento de cola de Azure con el SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="db96c-182">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="db96c-183">Los temas relacionados tratados en ese artículo incluyen:</span><span class="sxs-lookup"><span data-stu-id="db96c-183">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="db96c-184">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="db96c-184">Async functions</span></span>
* <span data-ttu-id="db96c-185">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="db96c-185">Multiple instances</span></span>
* <span data-ttu-id="db96c-186">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="db96c-186">Graceful shutdown</span></span>
* <span data-ttu-id="db96c-187">Utilizar atributos del SDK de WebJobs en el cuerpo de una función</span><span class="sxs-lookup"><span data-stu-id="db96c-187">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="db96c-188">Establecer las cadenas de conexión de SDK en el código.</span><span class="sxs-lookup"><span data-stu-id="db96c-188">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="db96c-189">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="db96c-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="db96c-190">Configure **MaxDequeueCount** para el control de blobs dudosos.</span><span class="sxs-lookup"><span data-stu-id="db96c-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="db96c-191">Desencadenar una función manualmente</span><span class="sxs-lookup"><span data-stu-id="db96c-191">Trigger a function manually</span></span>
* <span data-ttu-id="db96c-192">Escribir registros</span><span class="sxs-lookup"><span data-stu-id="db96c-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="db96c-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="db96c-193">Next steps</span></span>
<span data-ttu-id="db96c-194">En este artículo se ofrecen ejemplos de código que muestran cómo tratar escenarios comunes para trabajar con blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="db96c-194">This article has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="db96c-195">Para más información acerca de cómo usar el SDK de WebJobs y WebJobs de Azure, consulte [Recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="db96c-195">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

