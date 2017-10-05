---
title: Uso del almacenamiento de blobs de Azure con el SDK de WebJobs
description: "Obtenga información sobre cómo usar el almacenamiento de blobs de Azure con el SDK de WebJobs. Desencadene un proceso cuando un blob nuevo aparezca en un contenedor y controle los 'blobs dudosos'."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a><span data-ttu-id="b47d5-104">Uso del almacenamiento de blobs de Azure con el SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="b47d5-104">How to use Azure blob storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="b47d5-105">Información general</span><span class="sxs-lookup"><span data-stu-id="b47d5-105">Overview</span></span>
<span data-ttu-id="b47d5-106">Esta guía proporciona muestras de código de C# que muestran la manera de desencadenar un proceso cuando se crea o actualiza un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="b47d5-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="b47d5-107">Los ejemplos de código usan el [SDK de WebJobs](websites-dotnet-webjobs-sdk.md) versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="b47d5-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="b47d5-108">En el caso de ejemplos de código que muestran cómo crear blobs, consulte [Cómo usar el almacenamiento en cola de Azure con el SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="b47d5-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="b47d5-109">En la guía se supone que sabe [cómo crear un proyecto de WebJob en Visual Studio con cadenas de conexión que señalan a su cuenta de almacenamiento](websites-dotnet-webjobs-sdk-get-started.md) o a [varias cuentas de almacenamiento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="b47d5-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="b47d5-110"><a id="trigger"></a> Cómo desencadenar una función cuando se crea o actualiza un blob</span><span class="sxs-lookup"><span data-stu-id="b47d5-110"><a id="trigger"></a> How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="b47d5-111">Esta sección muestra cómo usar el atributo `BlobTrigger` .</span><span class="sxs-lookup"><span data-stu-id="b47d5-111">This section shows how to use the `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="b47d5-112">El SDK de WebJobs analiza los archivos de registro en busca de blobs nuevos o modificados.</span><span class="sxs-lookup"><span data-stu-id="b47d5-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="b47d5-113">Este proceso no se produce en tiempo real; podrían tardarse varios minutos o más en desencadenar una función después de crear el blob.</span><span class="sxs-lookup"><span data-stu-id="b47d5-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="b47d5-114">Además, los [registros de almacenamiento se crean como "el mejor esfuerzo"](https://msdn.microsoft.com/library/azure/hh343262.aspx) ; no hay ninguna garantía de que se capturarán todos los eventos.</span><span class="sxs-lookup"><span data-stu-id="b47d5-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="b47d5-115">En algunos casos, podrían faltar registros.</span><span class="sxs-lookup"><span data-stu-id="b47d5-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="b47d5-116">Si los límites de velocidad y confiabilidad de los desencadenadores de blobs no son aceptables para su aplicación, el método recomendado es crear un mensaje de cola al crear el blob y usar el atributo [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) en lugar del atributo `BlobTrigger` en la función que procesa el blob.</span><span class="sxs-lookup"><span data-stu-id="b47d5-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="b47d5-117">Único marcador de posición para el nombre de blob con extensión</span><span class="sxs-lookup"><span data-stu-id="b47d5-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="b47d5-118">El siguiente ejemplo de código copia blobs de texto que aparecen en el contenedor *input* al contenedor *output*:</span><span class="sxs-lookup"><span data-stu-id="b47d5-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="b47d5-119">El constructor de atributo toma un parámetro de cadena que especifica el nombre del contenedor y un marcador de posición para el nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="b47d5-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="b47d5-120">En este ejemplo, si se crea un blob llamado *Blob1.txt* en el contenedor *input*, la función crea un blob llamado *Blob1.txt* en el contenedor *output*.</span><span class="sxs-lookup"><span data-stu-id="b47d5-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span> 

<span data-ttu-id="b47d5-121">Puede especificar un patrón de nombre con el marcador de posición de nombre de blob, como se muestra en el siguiente ejemplo de código:</span><span class="sxs-lookup"><span data-stu-id="b47d5-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="b47d5-122">Este código solo copia blobs con nombres que comienzan con "original-".</span><span class="sxs-lookup"><span data-stu-id="b47d5-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="b47d5-123">Por ejemplo, *original-Blob1.txt* en el contenedor *input* se copia en *copy- Blob1.txt* en el contenedor *output*.</span><span class="sxs-lookup"><span data-stu-id="b47d5-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="b47d5-124">Si necesita especificar un patrón de nombre para nombres de blob que contienen llaves en el nombre, duplique las llaves.</span><span class="sxs-lookup"><span data-stu-id="b47d5-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="b47d5-125">Por ejemplo, si desea encontrar blobs en el contenedor *images* que tengan nombres como este:</span><span class="sxs-lookup"><span data-stu-id="b47d5-125">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="b47d5-126">use esto para el patrón:</span><span class="sxs-lookup"><span data-stu-id="b47d5-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="b47d5-127">En el ejemplo, el valor de marcador de posición *name* sería *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="b47d5-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="b47d5-128">Separar marcadores de posición de extensión y nombre de blob</span><span class="sxs-lookup"><span data-stu-id="b47d5-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="b47d5-129">El siguiente ejemplo de código cambia la extensión de archivo cuando copia los blobs que aparecen en el contenedor *input* al contenedor *output*.</span><span class="sxs-lookup"><span data-stu-id="b47d5-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="b47d5-130">El código registra la extensión del blob *input* y establece la extensión del blob *output* en *.txt*.</span><span class="sxs-lookup"><span data-stu-id="b47d5-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <span data-ttu-id="b47d5-131"><a id="types"></a> Tipos que puede enlazar a blobs</span><span class="sxs-lookup"><span data-stu-id="b47d5-131"><a id="types"></a> Types that you can bind to blobs</span></span>
<span data-ttu-id="b47d5-132">Puede utilizar el atributo `BlobTrigger` en los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="b47d5-132">You can use the `BlobTrigger` attribute on the following types:</span></span>

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="b47d5-133">Otros tipos deserializados por [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="b47d5-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="b47d5-134">Si desea trabajar directamente con la cuenta de almacenamiento de Azure, también puede agregar un parámetro `CloudStorageAccount` a la firma del método.</span><span class="sxs-lookup"><span data-stu-id="b47d5-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span></span>

<span data-ttu-id="b47d5-135">Para ver ejemplos, consulte el [código de enlace de blob en el repositorio azure-webjobs-sdk en GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="b47d5-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="b47d5-136"><a id="string"></a> Obtención del contenido del blob de texto enlazando a la cadena</span><span class="sxs-lookup"><span data-stu-id="b47d5-136"><a id="string"></a> Getting text blob content by binding to string</span></span>
<span data-ttu-id="b47d5-137">Si se esperan blobs de texto, se puede aplicar `BlobTrigger` a un parámetro `string`.</span><span class="sxs-lookup"><span data-stu-id="b47d5-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span></span> <span data-ttu-id="b47d5-138">El siguiente ejemplo de código enlaza un blob de texto a un parámetro `string` llamado `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="b47d5-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span></span> <span data-ttu-id="b47d5-139">La función usa ese parámetro para escribir el contenido del blob en el panel del SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="b47d5-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="b47d5-140"><a id="icbsb"></a> Obtención del contenido del blob serializado mediante el uso de ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="b47d5-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="b47d5-141">El siguiente ejemplo de código usa una clase que implementa `ICloudBlobStreamBinder` para permitir que el atributo `BlobTrigger` vincule un blob al tipo `WebImage`.</span><span class="sxs-lookup"><span data-stu-id="b47d5-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span></span>

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

<span data-ttu-id="b47d5-142">El código de enlace `WebImage` se proporciona en una clase `WebImageBinder` que deriva de `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="b47d5-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-the-blob-path-for-the-triggering-blob"></a><span data-ttu-id="b47d5-143">Obtención de la ruta de acceso del blob de desencadenamiento</span><span class="sxs-lookup"><span data-stu-id="b47d5-143">Getting the blob path for the triggering blob</span></span>
<span data-ttu-id="b47d5-144">Para obtener el nombre del contenedor y el del blob que desencadenó la función, incluya un parámetro de cadena `blobTrigger` en la firma de función.</span><span class="sxs-lookup"><span data-stu-id="b47d5-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="b47d5-145"><a id="poison"></a> Cómo administrar los blobs dudosos</span><span class="sxs-lookup"><span data-stu-id="b47d5-145"><a id="poison"></a> How to handle poison blobs</span></span>
<span data-ttu-id="b47d5-146">Cuando una función `BlobTrigger` presenta un error, el SDK vuelve a llamarla, en caso de que se hubiese producido por un error transitorio.</span><span class="sxs-lookup"><span data-stu-id="b47d5-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="b47d5-147">Si el error se produce debido al contenido del blob, la función presentará un error cada vez que intente procesar el blob.</span><span class="sxs-lookup"><span data-stu-id="b47d5-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="b47d5-148">De manera predeterminada, el SDK llama una función hasta cinco veces para un blob determinado.</span><span class="sxs-lookup"><span data-stu-id="b47d5-148">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="b47d5-149">Si el quinto intento falla, el SDK agrega un mensaje a una cola llamada *webjobs-blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="b47d5-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="b47d5-150">Es posible configurar el número máximo de reintentos.</span><span class="sxs-lookup"><span data-stu-id="b47d5-150">The maximum number of retries is configurable.</span></span> <span data-ttu-id="b47d5-151">Se usa la misma configuración [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) para controlar los blobs dudosos y los mensajes de cola dudosos.</span><span class="sxs-lookup"><span data-stu-id="b47d5-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="b47d5-152">El mensaje de cola para los blobs dudosos es un objeto JSON que contiene las siguientes propiedades:</span><span class="sxs-lookup"><span data-stu-id="b47d5-152">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="b47d5-153">FunctionId (con el formato *{nombre de WebJob}*.Functions.*{nombre de función}*, por ejemplo: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="b47d5-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="b47d5-154">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="b47d5-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="b47d5-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="b47d5-155">ContainerName</span></span>
* <span data-ttu-id="b47d5-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="b47d5-156">BlobName</span></span>
* <span data-ttu-id="b47d5-157">ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="b47d5-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="b47d5-158">En el siguiente ejemplo de código, la función `CopyBlob` tiene un código que hace que presente un error cada vez que se la llama.</span><span class="sxs-lookup"><span data-stu-id="b47d5-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="b47d5-159">Una vez que el SDK la llama por el número máximo de reintentos, se crea un mensaje en la cola de blobs dudosos y la función `LogPoisonBlob` procesa ese mensaje.</span><span class="sxs-lookup"><span data-stu-id="b47d5-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="b47d5-160">El SDK deserializa automáticamente el mensaje JSON.</span><span class="sxs-lookup"><span data-stu-id="b47d5-160">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="b47d5-161">Esta es la clase `PoisonBlobMessage` :</span><span class="sxs-lookup"><span data-stu-id="b47d5-161">Here is the `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="b47d5-162"><a id="polling"></a> Algoritmo de sondeo de blobs</span><span class="sxs-lookup"><span data-stu-id="b47d5-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="b47d5-163">El SDK de WebJobs examina todos los contenedores especificados por los atributos `BlobTrigger` en el inicio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b47d5-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="b47d5-164">En una cuenta de almacenamiento de gran tamaño, este análisis puede demorar un tiempo, por lo que podría pasar mucho tiempo antes de que se encuentren blobs nuevos y que se ejecuten las funciones `BlobTrigger` .</span><span class="sxs-lookup"><span data-stu-id="b47d5-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="b47d5-165">Para detectar blobs nuevos o cambiados después del inicio de la aplicación, el SDK lee de manera periódica de los registros de almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="b47d5-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="b47d5-166">Los registros de blobs se almacenan en búfer y solo se escriben físicamente cada diez minutos aproximadamente, por lo que puede haber un retraso importante una vez que se crea o actualiza un blob antes de que la función `BlobTrigger` correspondiente se ejecute.</span><span class="sxs-lookup"><span data-stu-id="b47d5-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="b47d5-167">Existe una excepción para los blobs que crea mediante el uso del atributo `Blob` .</span><span class="sxs-lookup"><span data-stu-id="b47d5-167">There is an exception for blobs that you create by using the `Blob` attribute.</span></span> <span data-ttu-id="b47d5-168">Cuando el SDK de WebJobs crea un blob nuevo, pasa el blob nuevo inmediatamente a cualquier función `BlobTrigger` coincidente.</span><span class="sxs-lookup"><span data-stu-id="b47d5-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span></span> <span data-ttu-id="b47d5-169">Por tanto, si tiene una cadena de entradas y salidas categorizadas como blob, el SDK puede procesarlas de manera eficaz.</span><span class="sxs-lookup"><span data-stu-id="b47d5-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="b47d5-170">Pero si desea baja latencia de ejecución para sus funciones de procesamiento de blobs para blobs que se crean o actualizan mediante otros medios, se recomienda usar `QueueTrigger` en lugar de `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="b47d5-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="b47d5-171"><a id="receipts"></a> Recepciones de blobs</span><span class="sxs-lookup"><span data-stu-id="b47d5-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="b47d5-172">El SDK de WebJobs se asegura de que ninguna función `BlobTrigger` se llame más de una vez para el mismo blob nuevo o actualizado.</span><span class="sxs-lookup"><span data-stu-id="b47d5-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="b47d5-173">Para hacerlo, mantiene *recepciones de blobs* para determinar si se ha procesado alguna versión de blob determinada.</span><span class="sxs-lookup"><span data-stu-id="b47d5-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="b47d5-174">Las recepciones de blobs se almacenan en un contenedor llamado *azure-webjobs-hosts* en la cuenta de almacenamiento de Azure que especifica la cadena de conexión AzureWebJobsStorage.</span><span class="sxs-lookup"><span data-stu-id="b47d5-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="b47d5-175">Una recepción de blobs tiene la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="b47d5-175">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="b47d5-176">La función que se llamó para el blob ("*{nombre de WebJob}*.Functions.*{nombre de función}*", por ejemplo: "WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="b47d5-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="b47d5-177">El nombre del contenedor</span><span class="sxs-lookup"><span data-stu-id="b47d5-177">The container name</span></span>
* <span data-ttu-id="b47d5-178">El tipo de blob ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="b47d5-178">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="b47d5-179">El nombre del blob</span><span class="sxs-lookup"><span data-stu-id="b47d5-179">The blob name</span></span>
* <span data-ttu-id="b47d5-180">ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="b47d5-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="b47d5-181">Si desea forzar el reprocesamiento de un blob, puede eliminar manualmente la recepción de blob de ese blob desde el contenedor *azure-webjobs-hosts* .</span><span class="sxs-lookup"><span data-stu-id="b47d5-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="b47d5-182"><a id="queues"></a>Temas relacionados tratados en el artículo sobre colas</span><span class="sxs-lookup"><span data-stu-id="b47d5-182"><a id="queues"></a>Related topics covered by the queues article</span></span>
<span data-ttu-id="b47d5-183">Para obtener información sobre cómo controlar el procesamiento de blobs desencadenado por un mensaje de cola o para ver los escenarios de SDK de WebJobs no específicos para el procesamiento de blobs, consulte [Cómo usar el almacenamiento de cola de Azure con el SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="b47d5-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="b47d5-184">Los temas relacionados tratados en ese artículo incluyen:</span><span class="sxs-lookup"><span data-stu-id="b47d5-184">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="b47d5-185">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="b47d5-185">Async functions</span></span>
* <span data-ttu-id="b47d5-186">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="b47d5-186">Multiple instances</span></span>
* <span data-ttu-id="b47d5-187">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="b47d5-187">Graceful shutdown</span></span>
* <span data-ttu-id="b47d5-188">Utilizar atributos del SDK de WebJobs en el cuerpo de una función</span><span class="sxs-lookup"><span data-stu-id="b47d5-188">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="b47d5-189">Establecer las cadenas de conexión de SDK en el código.</span><span class="sxs-lookup"><span data-stu-id="b47d5-189">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="b47d5-190">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="b47d5-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="b47d5-191">Configurar `MaxDequeueCount` para el control de blobs dudosos.</span><span class="sxs-lookup"><span data-stu-id="b47d5-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="b47d5-192">Desencadenar una función manualmente</span><span class="sxs-lookup"><span data-stu-id="b47d5-192">Trigger a function manually</span></span>
* <span data-ttu-id="b47d5-193">Escribir registros</span><span class="sxs-lookup"><span data-stu-id="b47d5-193">Write logs</span></span>

## <span data-ttu-id="b47d5-194"><a id="nextsteps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b47d5-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="b47d5-195">En esta guía se han proporcionado ejemplos de código que muestran cómo controlar los escenarios comunes para trabajar con blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="b47d5-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="b47d5-196">Para obtener más información acerca de cómo usar el SDK de WebJobs y WebJobs de Azure, consulte [Recursos de WebJobs de Azure recomendados](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="b47d5-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

