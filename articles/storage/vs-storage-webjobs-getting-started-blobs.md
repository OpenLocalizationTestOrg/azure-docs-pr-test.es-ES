---
title: aaaGet a trabajar con el almacenamiento de blobs y Visual Studio servicios conectados (proyectos de trabajo Web) | Documentos de Microsoft
description: "Servicios conectados cómo tooget a usar almacenamiento de blobs en un proyecto WebJob después de conectarse tooan almacenamiento de Azure mediante Visual Studio."
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
ms.openlocfilehash: cb2cecacbb1a59f093d5453a91fae33e0f279d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="4d7c2-103">Introducción al almacenamiento de blobs de Azure y servicios conectados de Visual Studio (proyectos de WebJobs)</span><span class="sxs-lookup"><span data-stu-id="4d7c2-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="4d7c2-104">Información general</span><span class="sxs-lookup"><span data-stu-id="4d7c2-104">Overview</span></span>
<span data-ttu-id="4d7c2-105">Este artículo proporciona C# de ejemplos de código que muestran cómo tootrigger un proceso cuando se crea o actualiza un blob de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-105">This article provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="4d7c2-106">ejemplos de código de Hello usan hello [SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk.md) versión 1.x.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="4d7c2-107">Cuando agrega un proyecto de WebJob de tooa de cuenta de almacenamiento mediante el uso de Visual Studio hello **agregar servicios conectados** cuadro de diálogo, paquetes de NuGet de almacenamiento de Azure apropiada de hello está instalado, las referencias adecuadas de .NET Hola son toohello agregado proyecto y cadenas de conexión para la cuenta de almacenamiento de Hola se actualizan en el archivo App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-107">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet package is installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="4d7c2-108">¿Cómo tootrigger una función cuando se crea o actualiza un blob</span><span class="sxs-lookup"><span data-stu-id="4d7c2-108">How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="4d7c2-109">Esta sección se muestra cómo hello toouse **BlobTrigger** atributo.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-109">This section shows how toouse hello **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="4d7c2-110">**Nota:** Hola archivos de registro de SDK de WebJobs exámenes toowatch para blobs nuevos o modificados.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-110">**Note:** hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="4d7c2-111">Este proceso es inherentemente lento; una función podría no obtener activada hasta varios minutos o más una vez creado el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-111">This process is inherently slow; a function might not get triggered until several minutes or longer after hello blob is created.</span></span>  <span data-ttu-id="4d7c2-112">Si la aplicación necesita tooprocess blobs inmediatamente, Hola recomendado método es toocreate un mensaje de la cola al crear Hola blob y usar hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) atributo en lugar de hello **BlobTrigger** atributo en función de Hola que procesa el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-112">If your application needs tooprocess blobs immediately, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello **BlobTrigger** attribute on hello function that processes hello blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="4d7c2-113">Único marcador de posición para el nombre de blob con extensión</span><span class="sxs-lookup"><span data-stu-id="4d7c2-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="4d7c2-114">Hello siguiente ejemplo de código copia blobs de texto que aparecen en hello *entrada* contenedor toohello *salida* contenedor:</span><span class="sxs-lookup"><span data-stu-id="4d7c2-114">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="4d7c2-115">constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre del contenedor de Hola y un marcador de posición para el nombre del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-115">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="4d7c2-116">En este ejemplo, si un blob denominado *Blob1.txt* se crea en hello *entrada* contenedor, la función hello crea un blob denominado *Blob1.txt* en hello *salida*  contenedor.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-116">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="4d7c2-117">Puede especificar un patrón de nombre con el marcador de posición de nombre de blob de hello, como se muestra en el siguiente ejemplo de código de hello:</span><span class="sxs-lookup"><span data-stu-id="4d7c2-117">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="4d7c2-118">Este código solo copia blobs con nombres que comienzan con "original-".</span><span class="sxs-lookup"><span data-stu-id="4d7c2-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="4d7c2-119">Por ejemplo, *original Blob1.txt* en hello *entrada* contenedor se copia demasiado*copia Blob1.txt* en hello *salida* contenedor.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-119">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="4d7c2-120">Si necesita toospecify un patrón de nombre para los nombres de blob que tienen las llaves en nombre de hello, doble llaves Hola.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-120">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="4d7c2-121">Por ejemplo, si desea toofind blobs hello *imágenes* contenedor que tienen nombres similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="4d7c2-121">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="4d7c2-122">use esto para el patrón:</span><span class="sxs-lookup"><span data-stu-id="4d7c2-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="4d7c2-123">En el ejemplo de Hola, Hola *nombre* sería el valor de marcador de posición *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-123">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="4d7c2-124">Separar marcadores de posición de extensión y nombre de blob</span><span class="sxs-lookup"><span data-stu-id="4d7c2-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="4d7c2-125">Hello cambios de ejemplo de código siguiente Hola extensión de archivo mientras realiza la copia blobs que aparecen en hello *entrada* contenedor toohello *salida* contenedor.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-125">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="4d7c2-126">código de Hello registra extensión Hola de hello *entrada* blob y establece la extensión de Hola de hello *salida* blob demasiado*.txt*.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-126">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <a name="types-that-you-can-bind-tooblobs"></a><span data-ttu-id="4d7c2-127">Tipos que se pueden enlazar tooblobs</span><span class="sxs-lookup"><span data-stu-id="4d7c2-127">Types that you can bind tooblobs</span></span>
<span data-ttu-id="4d7c2-128">Puede usar hello **BlobTrigger** atributo Hola siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="4d7c2-128">You can use hello **BlobTrigger** attribute on hello following types:</span></span>

* <span data-ttu-id="4d7c2-129">**cadena**</span><span class="sxs-lookup"><span data-stu-id="4d7c2-129">**string**</span></span>
* <span data-ttu-id="4d7c2-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="4d7c2-130">**TextReader**</span></span>
* <span data-ttu-id="4d7c2-131">**Stream**</span><span class="sxs-lookup"><span data-stu-id="4d7c2-131">**Stream**</span></span>
* <span data-ttu-id="4d7c2-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="4d7c2-132">**ICloudBlob**</span></span>
* <span data-ttu-id="4d7c2-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="4d7c2-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="4d7c2-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="4d7c2-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="4d7c2-135">Otros tipos deserializados por [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="4d7c2-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="4d7c2-136">Si desea que toowork directamente con hello cuenta de almacenamiento de Azure, también puede agregar un **CloudStorageAccount** firma del método toohello parámetro.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-136">If you want toowork directly with hello Azure storage account, you can also add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-toostring"></a><span data-ttu-id="4d7c2-137">Obtener contenido de blob de texto toostring de enlace</span><span class="sxs-lookup"><span data-stu-id="4d7c2-137">Getting text blob content by binding toostring</span></span>
<span data-ttu-id="4d7c2-138">Si se esperan que los blobs de texto, **BlobTrigger** puede ser aplicada tooa **cadena** parámetro.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-138">If text blobs are expected, **BlobTrigger** can be applied tooa **string** parameter.</span></span> <span data-ttu-id="4d7c2-139">ejemplo de código siguiente Hello enlaza un tooa de blob de texto **cadena** parámetro denominado **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-139">hello following code sample binds a text blob tooa **string** parameter named **logMessage**.</span></span> <span data-ttu-id="4d7c2-140">función Hello utiliza ese contenido de parámetro toowrite Hola de hello blob toohello panel de SDK de WebJobs.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-140">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="4d7c2-141">Obtención del contenido del blob serializado mediante el uso de ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="4d7c2-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="4d7c2-142">Hello ejemplo de código siguiente utiliza una clase que implementa **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** toobind toohello de un blob de atributo **WebImage** tipo.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-142">hello following code sample uses a class that implements **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** attribute toobind a blob toohello **WebImage** type.</span></span>

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

<span data-ttu-id="4d7c2-143">Hola **WebImage** código de enlace se proporciona en un **WebImageBinder** clase que deriva de **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-143">hello **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-toohandle-poison-blobs"></a><span data-ttu-id="4d7c2-144">¿Cómo toohandle dudosos blobs</span><span class="sxs-lookup"><span data-stu-id="4d7c2-144">How toohandle poison blobs</span></span>
<span data-ttu-id="4d7c2-145">Cuando un **BlobTrigger** produce un error de la función, Hola SDK lo llama una vez más, en caso de error de hello fue provocado por un error transitorio.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-145">When a **BlobTrigger** function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="4d7c2-146">Si se produce un error de hello en contenido de Hola de blob de hello, se produce un error en la función hello cada vez que trata de blob de hello tooprocess.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-146">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="4d7c2-147">De forma predeterminada, Hola SDK llama a una función too5 horas para un blob determinado.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-147">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="4d7c2-148">Si se produce un error en try quinto hello, Hola SDK agrega una cola de tooa de mensaje denominada *webjobs-blobtrigger-dudosos*.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-148">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="4d7c2-149">Hola número máximo de reintentos es configurable.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-149">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="4d7c2-150">Hola mismo [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) configuración se utiliza para el control de mensajes dudosos blob y control de mensajes de la cola de mensajes dudosos.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-150">hello same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="4d7c2-151">mensaje de la cola de Hola para blobs dudosos es un objeto JSON que contiene Hola propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="4d7c2-151">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="4d7c2-152">FunctionId (en formato de hello *{nombre del trabajo Web}*. Las funciones. *{Nombre de la función}*, por ejemplo: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="4d7c2-152">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="4d7c2-153">BlobType ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="4d7c2-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="4d7c2-154">ContainerName</span><span class="sxs-lookup"><span data-stu-id="4d7c2-154">ContainerName</span></span>
* <span data-ttu-id="4d7c2-155">BlobName</span><span class="sxs-lookup"><span data-stu-id="4d7c2-155">BlobName</span></span>
* <span data-ttu-id="4d7c2-156">ETag (un identificador de la versión del blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="4d7c2-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="4d7c2-157">En los siguientes Hola ejemplo de código, hello **CopyBlob** función tiene código que causa toofail cada vez que se llama.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-157">In hello following code sample, hello **CopyBlob** function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="4d7c2-158">Después de hello SDK lo llama para el número máximo de Hola de reintentos, se crea un mensaje en cola de mensajes dudosos blob hello y ese mensaje sea procesado por hello **LogPoisonBlob** (función).</span><span class="sxs-lookup"><span data-stu-id="4d7c2-158">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="4d7c2-159">Hola SDK automáticamente deserializa el mensaje de bienvenida de JSON.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-159">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="4d7c2-160">Aquí es hello **PoisonBlobMessage** clase:</span><span class="sxs-lookup"><span data-stu-id="4d7c2-160">Here is hello **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="4d7c2-161">Algoritmo de sondeo de blobs</span><span class="sxs-lookup"><span data-stu-id="4d7c2-161">Blob polling algorithm</span></span>
<span data-ttu-id="4d7c2-162">Hola SDK de WebJobs examina todos los contenedores especificados por **BlobTrigger** atributos al iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-162">hello WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="4d7c2-163">En una cuenta de almacenamiento de gran tamaño, este análisis puede demorar un tiempo, por lo que podría pasar mucho tiempo antes de que se encuentren blobs nuevos y que se ejecuten las funciones **BlobTrigger** .</span><span class="sxs-lookup"><span data-stu-id="4d7c2-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="4d7c2-164">toodetect blobs nuevos o modificados después de iniciarse la aplicación, los registros de hello que SDK lee periódicamente Hola almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-164">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="4d7c2-165">Hello registros del blob se almacenan en búfer y que sólo obtengan físicamente escribir cada 10 minutos o por lo tanto, por lo que puede haber un retraso importante después de un blob se crea o se actualiza antes de hello correspondiente **BlobTrigger** se ejecuta la función.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-165">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="4d7c2-166">Hay una excepción para los blobs que creas mediante hello **Blob** atributo.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-166">There is an exception for blobs that you create by using hello **Blob** attribute.</span></span> <span data-ttu-id="4d7c2-167">Cuando Hola SDK de WebJobs crea un nuevo blob, pasa inmediatamente nuevo blob en hello coincidencia tooany **BlobTrigger** funciones.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-167">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching **BlobTrigger** functions.</span></span> <span data-ttu-id="4d7c2-168">Por lo tanto, si tiene una cadena de blob entradas y salidas, Hola SDK pueda procesarlos eficazmente.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-168">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="4d7c2-169">Pero si desea baja latencia de ejecución para sus funciones de procesamiento de blobs para blobs que se crean o actualizan mediante otros medios, se recomienda usar **QueueTrigger** en lugar de **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="4d7c2-170">Recepciones de blobs</span><span class="sxs-lookup"><span data-stu-id="4d7c2-170">Blob receipts</span></span>
<span data-ttu-id="4d7c2-171">Hola SDK de WebJobs asegura de que ninguna **BlobTrigger** función obtiene llama más de una vez para hello mismo nuevo o actualiza el blob.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-171">hello WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="4d7c2-172">Esto consigue mediante mantener *blob confirmaciones* en orden toodetermine si se ha procesado una versión determinada de blob.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-172">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="4d7c2-173">Confirmaciones de BLOB se almacenan en un contenedor denominado *hosts de webjobs de azure* de cuenta de almacenamiento de Azure Hola especificado por la cadena de conexión de AzureWebJobsStorage Hola.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="4d7c2-174">Una confirmación de blob tiene Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="4d7c2-174">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="4d7c2-175">Hola función a la que se llamó para el blob de hello ("*{nombre del trabajo Web}*. Las funciones. *{Nombre de la función}*", por ejemplo:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="4d7c2-175">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="4d7c2-176">nombre del contenedor de Hola</span><span class="sxs-lookup"><span data-stu-id="4d7c2-176">hello container name</span></span>
* <span data-ttu-id="4d7c2-177">tipo de blob de Hello ("BlockBlob" o "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="4d7c2-177">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="4d7c2-178">nombre del blob Hola</span><span class="sxs-lookup"><span data-stu-id="4d7c2-178">hello blob name</span></span>
* <span data-ttu-id="4d7c2-179">Hola ETag (un identificador de versión de blob, por ejemplo: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="4d7c2-179">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="4d7c2-180">Si desea volver a procesar tooforce de un blob, puede eliminar manualmente el recibo de blob de Hola para dicho blob de hello *hosts de webjobs de azure* contenedor.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-180">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-hello-queues-article"></a><span data-ttu-id="4d7c2-181">Temas relacionados cubiertos por artículo de colas de Hola</span><span class="sxs-lookup"><span data-stu-id="4d7c2-181">Related topics covered by hello queues article</span></span>
<span data-ttu-id="4d7c2-182">Para obtener información acerca de cómo el procesamiento de blob toohandle desencadenada por un mensaje de la cola, o de trabajos Web escenarios SDK no tooblob específica de procesamiento, vea [cómo toouse Azure cola de almacenamiento con hello SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="4d7c2-182">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="4d7c2-183">Temas relacionados que se tratan en dicho artículo Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="4d7c2-183">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="4d7c2-184">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="4d7c2-184">Async functions</span></span>
* <span data-ttu-id="4d7c2-185">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="4d7c2-185">Multiple instances</span></span>
* <span data-ttu-id="4d7c2-186">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="4d7c2-186">Graceful shutdown</span></span>
* <span data-ttu-id="4d7c2-187">Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función</span><span class="sxs-lookup"><span data-stu-id="4d7c2-187">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="4d7c2-188">Establecer las cadenas de conexión de SDK de hello en el código.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-188">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="4d7c2-189">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="4d7c2-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="4d7c2-190">Configure **MaxDequeueCount** para el control de blobs dudosos.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="4d7c2-191">Desencadenar una función manualmente</span><span class="sxs-lookup"><span data-stu-id="4d7c2-191">Trigger a function manually</span></span>
* <span data-ttu-id="4d7c2-192">Escribir registros</span><span class="sxs-lookup"><span data-stu-id="4d7c2-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d7c2-193">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4d7c2-193">Next steps</span></span>
<span data-ttu-id="4d7c2-194">En este artículo se proporciona ejemplos de código que muestran cómo los blobs toohandle escenarios comunes para trabajar con Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7c2-194">This article has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="4d7c2-195">Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="4d7c2-195">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

