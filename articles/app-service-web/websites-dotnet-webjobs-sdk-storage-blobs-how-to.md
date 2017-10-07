---
title: aaaHow toouse almacenamiento de blobs de Azure con hello SDK de WebJobs
description: "Obtenga información acerca de cómo toouse Azure blob storage con hello SDK de WebJobs. Desencadene un proceso cuando un blob nuevo aparezca en un contenedor y controle los 'blobs dudosos'."
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
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="747d3-104">¿Cómo toouse Azure blob storage con hello SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="747d3-104">How toouse Azure blob storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="747d3-105">Información general</span><span class="sxs-lookup"><span data-stu-id="747d3-105">Overview</span></span>
<span data-ttu-id="747d3-106">Esta guía proporciona C# de ejemplos de código que muestran cómo tootrigger un proceso cuando se crea o actualiza un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="747d3-106">This guide provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="747d3-107">uso de ejemplos de código de Hello [SDK de WebJobs](websites-dotnet-webjobs-sdk.md) versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="747d3-107">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="747d3-108">Para obtener ejemplos de código que muestran cómo toocreate blobs, vea [cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="747d3-108">For code samples that show how toocreate blobs, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="747d3-109">Guía de Hola se supone que sabe [cómo cadenas toocreate un proyecto WebJob en Visual Studio con una conexión de esa cuenta de almacenamiento de punto tooyour](websites-dotnet-webjobs-sdk-get-started.md) o demasiado[varias cuentas de almacenamiento](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="747d3-109">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="747d3-110"><a id="trigger"></a>¿Cómo tootrigger una función cuando se crea o actualiza un blob</span><span class="sxs-lookup"><span data-stu-id="747d3-110"><a id="trigger"></a> How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="747d3-111">Esta sección se muestra cómo toouse hello `BlobTrigger` atributo.</span><span class="sxs-lookup"><span data-stu-id="747d3-111">This section shows how toouse hello `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="747d3-112">Hola archivos de registro de SDK de WebJobs exámenes toowatch para blobs nuevos o modificados.</span><span class="sxs-lookup"><span data-stu-id="747d3-112">hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="747d3-113">Este proceso no es en tiempo real; una función podría no obtener activada hasta varios minutos o más una vez creado el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="747d3-113">This process is not real-time; a function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="747d3-114">Además, los [registros de almacenamiento se crean como "el mejor esfuerzo"](https://msdn.microsoft.com/library/azure/hh343262.aspx) ; no hay ninguna garantía de que se capturarán todos los eventos.</span><span class="sxs-lookup"><span data-stu-id="747d3-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="747d3-115">En algunos casos, podrían faltar registros.</span><span class="sxs-lookup"><span data-stu-id="747d3-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="747d3-116">Si las limitaciones de velocidad y la confiabilidad de Hola de desencadenadores de blob no son aceptables para la aplicación, Hola recomendado método es toocreate un mensaje de la cola al crear Hola blob y usar hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) atributo en lugar de Hola `BlobTrigger` atributo en función de Hola que procesa el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="747d3-116">If hello speed and reliability limitations of blob triggers are not acceptable for your application, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello `BlobTrigger` attribute on hello function that processes hello blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="747d3-117">Único marcador de posición para el nombre de blob con extensión</span><span class="sxs-lookup"><span data-stu-id="747d3-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="747d3-118">Hello siguiente ejemplo de código copia blobs de texto que aparecen en hello *entrada* contenedor toohello *salida* contenedor:</span><span class="sxs-lookup"><span data-stu-id="747d3-118">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="747d3-119">constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre del contenedor de Hola y un marcador de posición para el nombre del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="747d3-119">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="747d3-120">En este ejemplo, si un blob denominado *Blob1.txt* se crea en hello *entrada* contenedor, la función hello crea un blob denominado *Blob1.txt* en hello *salida*  contenedor.</span><span class="sxs-lookup"><span data-stu-id="747d3-120">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span> 

<span data-ttu-id="747d3-121">Puede especificar un patrón de nombre con el marcador de posición de nombre de blob de hello, como se muestra en el siguiente ejemplo de código de hello:</span><span class="sxs-lookup"><span data-stu-id="747d3-121">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="747d3-122">Este código solo copia blobs con nombres que comienzan con "original-".</span><span class="sxs-lookup"><span data-stu-id="747d3-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="747d3-123">Por ejemplo, *original Blob1.txt* en hello *entrada* contenedor se copia demasiado*copia Blob1.txt* en hello *salida* contenedor.</span><span class="sxs-lookup"><span data-stu-id="747d3-123">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="747d3-124">Si necesita toospecify un patrón de nombre para los nombres de blob que tienen las llaves en nombre de hello, doble llaves Hola.</span><span class="sxs-lookup"><span data-stu-id="747d3-124">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="747d3-125">Por ejemplo, si desea toofind blobs hello *imágenes* contenedor que tienen nombres similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="747d3-125">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="747d3-126">use esto para el patrón:</span><span class="sxs-lookup"><span data-stu-id="747d3-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="747d3-127">En el ejemplo de Hola, Hola *nombre* sería el valor de marcador de posición *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="747d3-127">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="747d3-128">Separar marcadores de posición de extensión y nombre de blob</span><span class="sxs-lookup"><span data-stu-id="747d3-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="747d3-129">Hello cambios de ejemplo de código siguiente Hola extensión de archivo mientras realiza la copia blobs que aparecen en hello *entrada* contenedor toohello *salida* contenedor.</span><span class="sxs-lookup"><span data-stu-id="747d3-129">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="747d3-130">código de Hello registra extensión Hola de hello *entrada* blob y establece la extensión de Hola de hello *salida* blob demasiado*.txt*.</span><span class="sxs-lookup"><span data-stu-id="747d3-130">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <span data-ttu-id="747d3-131"><a id="types"></a>Tipos que se pueden enlazar tooblobs</span><span class="sxs-lookup"><span data-stu-id="747d3-131"><a id="types"></a> Types that you can bind tooblobs</span></span>
<span data-ttu-id="747d3-132">Puede usar hello `BlobTrigger` atributo Hola siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="747d3-132">You can use hello `BlobTrigger` attribute on hello following types:</span></span>

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
* <span data-ttu-id="747d3-133">Otros tipos deserializados por [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="747d3-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="747d3-134">Si desea que toowork directamente con hello cuenta de almacenamiento de Azure, también puede agregar un `CloudStorageAccount` firma del método toohello parámetro.</span><span class="sxs-lookup"><span data-stu-id="747d3-134">If you want toowork directly with hello Azure storage account, you can also add a `CloudStorageAccount` parameter toohello method signature.</span></span>

<span data-ttu-id="747d3-135">Para obtener ejemplos, vea hello [blob código de enlace en el repositorio de sdk de webjobs de azure de hello en GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="747d3-135">For examples, see hello [blob binding code in hello azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="747d3-136"><a id="string"></a>Obtener contenido de blob de texto toostring de enlace</span><span class="sxs-lookup"><span data-stu-id="747d3-136"><a id="string"></a> Getting text blob content by binding toostring</span></span>
<span data-ttu-id="747d3-137">Si se esperan que los blobs de texto, `BlobTrigger` puede ser aplicada tooa `string` parámetro.</span><span class="sxs-lookup"><span data-stu-id="747d3-137">If text blobs are expected, `BlobTrigger` can be applied tooa `string` parameter.</span></span> <span data-ttu-id="747d3-138">ejemplo de código siguiente Hello enlaza un tooa de blob de texto `string` parámetro denominado `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="747d3-138">hello following code sample binds a text blob tooa `string` parameter named `logMessage`.</span></span> <span data-ttu-id="747d3-139">función Hello utiliza ese contenido de parámetro toowrite Hola de hello blob toohello panel de SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="747d3-139">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="747d3-140"><a id="icbsb"></a> Obtención del contenido del blob serializado mediante el uso de ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="747d3-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="747d3-141">Hello ejemplo de código siguiente utiliza una clase que implementa `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` toobind toohello de un blob de atributo `WebImage` tipo.</span><span class="sxs-lookup"><span data-stu-id="747d3-141">hello following code sample uses a class that implements `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` attribute toobind a blob toohello `WebImage` type.</span></span>

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

<span data-ttu-id="747d3-142">Hola `WebImage` código de enlace se proporciona en un `WebImageBinder` clase que deriva de `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="747d3-142">hello `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a><span data-ttu-id="747d3-143">Obteniendo ruta de acceso de blob de Hola para hello desencadenar blob</span><span class="sxs-lookup"><span data-stu-id="747d3-143">Getting hello blob path for hello triggering blob</span></span>
<span data-ttu-id="747d3-144">tooget Hola contenedor y nombres de blob del blob de Hola que desencadenó la función hello, incluyen un `blobTrigger` parámetro en la firma de la función hello de cadena.</span><span class="sxs-lookup"><span data-stu-id="747d3-144">tooget hello container name and blob name of hello blob that has triggered hello function, include a `blobTrigger` string parameter in hello function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="747d3-145"><a id="poison"></a>¿Cómo toohandle dudosos blobs</span><span class="sxs-lookup"><span data-stu-id="747d3-145"><a id="poison"></a> How toohandle poison blobs</span></span>
<span data-ttu-id="747d3-146">Cuando un `BlobTrigger` produce un error de la función, Hola SDK lo llama una vez más, en caso de error de hello fue provocado por un error transitorio.</span><span class="sxs-lookup"><span data-stu-id="747d3-146">When a `BlobTrigger` function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="747d3-147">Si se produce un error de hello en contenido de Hola de blob de hello, se produce un error en la función hello cada vez que trata de blob de hello tooprocess.</span><span class="sxs-lookup"><span data-stu-id="747d3-147">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="747d3-148">De forma predeterminada, Hola SDK llama a una función too5 horas para un blob determinado.</span><span class="sxs-lookup"><span data-stu-id="747d3-148">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="747d3-149">Si se produce un error en try quinto hello, Hola SDK agrega una cola de tooa de mensaje denominada *webjobs-blobtrigger-dudosos*.</span><span class="sxs-lookup"><span data-stu-id="747d3-149">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="747d3-150">Hola número máximo de reintentos es configurable.</span><span class="sxs-lookup"><span data-stu-id="747d3-150">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="747d3-151">Hola mismo [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) configuración se utiliza para el control de mensajes dudosos blob y control de mensajes de la cola de mensajes dudosos.</span><span class="sxs-lookup"><span data-stu-id="747d3-151">hello same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="747d3-152">mensaje de la cola de Hola para blobs dudosos es un objeto JSON que contiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="747d3-152">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="747d3-153">FunctionId (en formato de hello *{nombre del trabajo Web}*. Las funciones. *{Nombre de la función}*, por ejemplo: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="747d3-153">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="747d3-154">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="747d3-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="747d3-155">ContainerName</span><span class="sxs-lookup"><span data-stu-id="747d3-155">ContainerName</span></span>
* <span data-ttu-id="747d3-156">BlobName</span><span class="sxs-lookup"><span data-stu-id="747d3-156">BlobName</span></span>
* <span data-ttu-id="747d3-157">ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="747d3-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="747d3-158">En los siguientes Hola ejemplo de código, hello `CopyBlob` función tiene código que causa toofail cada vez que se llama.</span><span class="sxs-lookup"><span data-stu-id="747d3-158">In hello following code sample, hello `CopyBlob` function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="747d3-159">Después de hello SDK lo llama para el número máximo de Hola de reintentos, se crea un mensaje en cola de mensajes dudosos blob hello y ese mensaje sea procesado por hello `LogPoisonBlob` función.</span><span class="sxs-lookup"><span data-stu-id="747d3-159">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="747d3-160">Hola SDK automáticamente deserializa el mensaje de bienvenida de JSON.</span><span class="sxs-lookup"><span data-stu-id="747d3-160">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="747d3-161">Aquí es hello `PoisonBlobMessage` clase:</span><span class="sxs-lookup"><span data-stu-id="747d3-161">Here is hello `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="747d3-162"><a id="polling"></a> Algoritmo de sondeo de blobs</span><span class="sxs-lookup"><span data-stu-id="747d3-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="747d3-163">Hola SDK de WebJobs examina todos los contenedores especificados por `BlobTrigger` atributos al iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="747d3-163">hello WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="747d3-164">En una cuenta de almacenamiento de gran tamaño, este análisis puede demorar un tiempo, por lo que podría pasar mucho tiempo antes de que se encuentren blobs nuevos y que se ejecuten las funciones `BlobTrigger` .</span><span class="sxs-lookup"><span data-stu-id="747d3-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="747d3-165">toodetect blobs nuevos o modificados después de iniciarse la aplicación, los registros de hello que SDK lee periódicamente Hola almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="747d3-165">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="747d3-166">Hello registros del blob se almacenan en búfer y que sólo obtengan físicamente escribir cada 10 minutos o por lo tanto, por lo que puede haber un retraso importante después de un blob se crea o se actualiza antes de hello correspondiente `BlobTrigger` se ejecuta la función.</span><span class="sxs-lookup"><span data-stu-id="747d3-166">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="747d3-167">Hay una excepción para los blobs que creas mediante hello `Blob` atributo.</span><span class="sxs-lookup"><span data-stu-id="747d3-167">There is an exception for blobs that you create by using hello `Blob` attribute.</span></span> <span data-ttu-id="747d3-168">Cuando Hola SDK de WebJobs crea un nuevo blob, pasa inmediatamente nuevo blob en hello tooany coincidencia `BlobTrigger` funciones.</span><span class="sxs-lookup"><span data-stu-id="747d3-168">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching `BlobTrigger` functions.</span></span> <span data-ttu-id="747d3-169">Por lo tanto, si tiene una cadena de blob entradas y salidas, Hola SDK pueda procesarlos eficazmente.</span><span class="sxs-lookup"><span data-stu-id="747d3-169">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="747d3-170">Pero si desea baja latencia de ejecución para sus funciones de procesamiento de blobs para blobs que se crean o actualizan mediante otros medios, se recomienda usar `QueueTrigger` en lugar de `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="747d3-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="747d3-171"><a id="receipts"></a> Recepciones de blobs</span><span class="sxs-lookup"><span data-stu-id="747d3-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="747d3-172">Hola SDK de WebJobs asegura de que ningún `BlobTrigger` función obtiene llama más de una vez para hello mismo nuevo o actualiza el blob.</span><span class="sxs-lookup"><span data-stu-id="747d3-172">hello WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="747d3-173">Esto consigue mediante mantener *blob confirmaciones* en orden toodetermine si se ha procesado una versión determinada de blob.</span><span class="sxs-lookup"><span data-stu-id="747d3-173">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="747d3-174">Confirmaciones de BLOB se almacenan en un contenedor denominado *hosts de webjobs de azure* de cuenta de almacenamiento de Azure Hola especificado por la cadena de conexión de AzureWebJobsStorage Hola.</span><span class="sxs-lookup"><span data-stu-id="747d3-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="747d3-175">Una confirmación de blob tiene Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="747d3-175">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="747d3-176">Hola función a la que se llamó para el blob de hello ("*{nombre del trabajo Web}*. Las funciones. *{Nombre de la función}*", por ejemplo:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="747d3-176">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="747d3-177">nombre del contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="747d3-177">hello container name</span></span>
* <span data-ttu-id="747d3-178">tipo de blob de Hello ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="747d3-178">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="747d3-179">nombre del blob Hola</span><span class="sxs-lookup"><span data-stu-id="747d3-179">hello blob name</span></span>
* <span data-ttu-id="747d3-180">Hola ETag (un identificador de versión de blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="747d3-180">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="747d3-181">Si desea volver a procesar tooforce de un blob, puede eliminar manualmente el recibo de blob de Hola para dicho blob de hello *hosts de webjobs de azure* contenedor.</span><span class="sxs-lookup"><span data-stu-id="747d3-181">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="747d3-182"><a id="queues"></a>Temas relacionados cubiertos por artículo de colas de Hola</span><span class="sxs-lookup"><span data-stu-id="747d3-182"><a id="queues"></a>Related topics covered by hello queues article</span></span>
<span data-ttu-id="747d3-183">Para obtener información acerca de cómo el procesamiento de blob toohandle desencadenada por un mensaje de la cola, o de trabajos Web escenarios SDK no tooblob específica de procesamiento, vea [cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="747d3-183">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="747d3-184">Temas relacionados que se tratan en dicho artículo Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="747d3-184">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="747d3-185">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="747d3-185">Async functions</span></span>
* <span data-ttu-id="747d3-186">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="747d3-186">Multiple instances</span></span>
* <span data-ttu-id="747d3-187">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="747d3-187">Graceful shutdown</span></span>
* <span data-ttu-id="747d3-188">Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función</span><span class="sxs-lookup"><span data-stu-id="747d3-188">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="747d3-189">Establecer las cadenas de conexión de SDK de hello en el código.</span><span class="sxs-lookup"><span data-stu-id="747d3-189">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="747d3-190">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="747d3-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="747d3-191">Configurar `MaxDequeueCount` para el control de blobs dudosos.</span><span class="sxs-lookup"><span data-stu-id="747d3-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="747d3-192">Desencadenar una función manualmente</span><span class="sxs-lookup"><span data-stu-id="747d3-192">Trigger a function manually</span></span>
* <span data-ttu-id="747d3-193">Escribir registros</span><span class="sxs-lookup"><span data-stu-id="747d3-193">Write logs</span></span>

## <span data-ttu-id="747d3-194"><a id="nextsteps"></a> Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="747d3-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="747d3-195">Esta guía proporciona ejemplos de código que muestran cómo los blobs toohandle escenarios comunes para trabajar con Azure.</span><span class="sxs-lookup"><span data-stu-id="747d3-195">This guide has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="747d3-196">Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [Azure trabajos Web recomienda recursos](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="747d3-196">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

