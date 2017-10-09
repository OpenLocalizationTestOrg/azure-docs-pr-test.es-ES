---
title: aaaGetting a trabajar con Visual Studio y el almacenamiento de cola servicios conectados (proyectos de trabajo Web) | Documentos de Microsoft
description: "Cómo tooget iniciado mediante el almacenamiento de cola de Azure en un proyecto WebJob después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 720e96fda734c31e1b1d68d4f95aa9531a20a3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="c47e3-103">Introducción al Almacenamiento de colas de Azure y servicios conectados de Visual Studio (proyectos de WebJobs)</span><span class="sxs-lookup"><span data-stu-id="c47e3-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="c47e3-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c47e3-104">Overview</span></span>
<span data-ttu-id="c47e3-105">Este artículo se describe cómo obtener iniciado mediante la cola de Azure Hola de almacenamiento en un proyecto WebJob de Azure de Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure mediante Visual Studio **agregar servicios conectados** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c47e3-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using hello Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="c47e3-106">Cuando agrega un proyecto de WebJob de tooa de cuenta de almacenamiento mediante el uso de Visual Studio hello **agregar servicios conectados** cuadro de diálogo, se han instalado paquetes de NuGet de almacenamiento de Azure adecuados de hello, referencias de hello adecuadas .NET son toohello agregado proyecto y cadenas de conexión para la cuenta de almacenamiento de Hola se actualizan en el archivo App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="c47e3-106">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet packages are installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>  

<span data-ttu-id="c47e3-107">Este artículo proporciona ejemplos de código de C# que muestran cómo toouse Hola versión del SDK de WebJobs de Azure 1.x con hello servicio de almacenamiento de cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="c47e3-107">This article provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure Queue storage service.</span></span>

<span data-ttu-id="c47e3-108">Almacenamiento de la cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c47e3-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="c47e3-109">Un mensaje de la cola solo puede estar too64 KB de tamaño y una cola puede contener millones de mensajes, seguridad toohello límite de capacidad total de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c47e3-109">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span> <span data-ttu-id="c47e3-110">Consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](storage-dotnet-how-to-use-queues.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="c47e3-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="c47e3-111">Para obtener más información acerca de ASP.NET, consulte [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="c47e3-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="c47e3-112">¿Cómo tootrigger una función cuando se recibe un mensaje de la cola</span><span class="sxs-lookup"><span data-stu-id="c47e3-112">How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="c47e3-113">llama a una función que Hola SDK de WebJobs toowrite cuando se recibe un mensaje de la cola, utilice hello **QueueTrigger** atributo.</span><span class="sxs-lookup"><span data-stu-id="c47e3-113">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello **QueueTrigger** attribute.</span></span> <span data-ttu-id="c47e3-114">constructor de atributo de Hello toma un parámetro de cadena que especifica el nombre hello de hello cola toopoll.</span><span class="sxs-lookup"><span data-stu-id="c47e3-114">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="c47e3-115">toosee cómo tooset Hola nombre de la cola de forma dinámica, consulte [cómo tooset opciones de configuración](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c47e3-115">toosee how tooset hello queue name dynamically, check out [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="c47e3-116">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="c47e3-116">String queue messages</span></span>
<span data-ttu-id="c47e3-117">En el siguiente ejemplo de Hola, cola de hello contiene un mensaje de cadena, por lo que **QueueTrigger** es tooa aplicado parámetro de cadena denominado **logMessage** que incluye contenido de hello del mensaje de bienvenida de cola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-117">In hello following example, hello queue contains a string message, so **QueueTrigger** is applied tooa string parameter named **logMessage** which contains hello content of hello queue message.</span></span> <span data-ttu-id="c47e3-118">Hola función [escribe un toohello de mensaje de registro panel](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="c47e3-118">hello function [writes a log message toohello Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="c47e3-119">Además **cadena**, parámetro hello puede ser una matriz de bytes, un **CloudQueueMessage** objeto o un POCO que defina.</span><span class="sxs-lookup"><span data-stu-id="c47e3-119">Besides **string**, hello parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="c47e3-120">Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="c47e3-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c47e3-121">En el siguiente ejemplo de Hola, mensaje de bienvenida de cola contiene un valor JSON para un **BlobInformation** objeto que incluye un **BlobName** propiedad.</span><span class="sxs-lookup"><span data-stu-id="c47e3-121">In hello following example, hello queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="c47e3-122">Hola SDK automáticamente deserializa el objeto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-122">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="c47e3-123">Hola SDK utiliza hello [paquete NuGet de Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize y deserializar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="c47e3-123">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="c47e3-124">Si crea mensajes en cola en un programa que no utilice Hola SDK de WebJobs, puede escribir código como sigue toocreate un POCO de la cola de mensajes de ejemplo de Hola ese Hola que SDK puede analizar.</span><span class="sxs-lookup"><span data-stu-id="c47e3-124">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="c47e3-125">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="c47e3-125">Async functions</span></span>
<span data-ttu-id="c47e3-126">Hola después de la función asincrónica [escribe un panel de registro toohello](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="c47e3-126">hello following async function [writes a log toohello Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="c47e3-127">Funciones asincrónicas pueden tardar un [token de cancelación](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), tal y como se muestra en el siguiente ejemplo que copia un blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="c47e3-128">(Para obtener una explicación de hello **queueTrigger** marcador de posición, vea hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) sección.)</span><span class="sxs-lookup"><span data-stu-id="c47e3-128">(For an explanation of hello **queueTrigger** placeholder, see hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a><span data-ttu-id="c47e3-129">Atributo de tipos hello QueueTrigger funciona con</span><span class="sxs-lookup"><span data-stu-id="c47e3-129">Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="c47e3-130">Puede usar **QueueTrigger** con hello siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="c47e3-130">You can use **QueueTrigger** with hello following types:</span></span>

* <span data-ttu-id="c47e3-131">**cadena**</span><span class="sxs-lookup"><span data-stu-id="c47e3-131">**string**</span></span>
* <span data-ttu-id="c47e3-132">Un tipo de POCO serializado como JSON</span><span class="sxs-lookup"><span data-stu-id="c47e3-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="c47e3-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="c47e3-133">**byte[]**</span></span>
* <span data-ttu-id="c47e3-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="c47e3-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="c47e3-135">Algoritmo de sondeo</span><span class="sxs-lookup"><span data-stu-id="c47e3-135">Polling algorithm</span></span>
<span data-ttu-id="c47e3-136">Hola SDK implementa un efecto de hello tooreduce aleatorio algoritmo de retroceso exponencial de sondeo en los costos de transacciones de almacenamiento de cola inactiva.</span><span class="sxs-lookup"><span data-stu-id="c47e3-136">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="c47e3-137">Cuando se encuentra un mensaje, Hola SDK espera dos segundos y, a continuación, comprueba si otro mensaje; Cuando se encuentra ningún mensaje espera unos cuatro segundos antes de volver a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="c47e3-137">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="c47e3-138">Después de los intentos subsiguientes tooget un mensaje de la cola, tiempo de espera de hello continúa tooincrease hasta que alcanza el tiempo de espera máximo de hello, qué minuto de tooone los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="c47e3-138">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="c47e3-139">[Hello tiempo de espera máximo es configurable](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c47e3-139">[hello maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="c47e3-140">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="c47e3-140">Multiple instances</span></span>
<span data-ttu-id="c47e3-141">Si la aplicación web se ejecuta en varias instancias, una trabajos Web continuos se ejecuta en cada equipo e intentará toorun funciones y espere a que los desencadenadores cada máquina.</span><span class="sxs-lookup"><span data-stu-id="c47e3-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="c47e3-142">En algunos casos que esto puede provocar funciones toosome procesamiento Hola mismos datos dos veces, por lo que funciones deben ser idempotentes (escrito por lo llamar varias veces con hello no generan los mismos datos de entrada Duplicar resultados).</span><span class="sxs-lookup"><span data-stu-id="c47e3-142">In some scenarios this can lead toosome functions processing hello same data twice, so functions should be idempotent (written so that calling them repeatedly with hello same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="c47e3-143">Ejecución en paralelo</span><span class="sxs-lookup"><span data-stu-id="c47e3-143">Parallel execution</span></span>
<span data-ttu-id="c47e3-144">Si tiene varias funciones que escuchan en diferentes colas, Hola SDK llamará a ellos en paralelo cuando se reciben los mensajes al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="c47e3-144">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="c47e3-145">Hello mismo puede decirse cuando se reciben varios mensajes de una sola cola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-145">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="c47e3-146">De forma predeterminada, Hola SDK Obtiene un lote de 16 mensajes en cola a la vez y ejecuta la función hello que los procesa en paralelo.</span><span class="sxs-lookup"><span data-stu-id="c47e3-146">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="c47e3-147">[tamaño de lote de Hello es configurable](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c47e3-147">[hello batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="c47e3-148">Cuando se obtiene el número Hola procesando hacia abajo toohalf del tamaño de lote de hello, Hola SDK obtiene otro lote y empieza a procesar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="c47e3-148">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="c47e3-149">Por lo tanto, número máximo de Hola de mensajes simultáneos que se procesan por función es el tamaño del lote de una vez y Media Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-149">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="c47e3-150">Este límite aplica por separado tooeach función que tiene un **QueueTrigger** atributo.</span><span class="sxs-lookup"><span data-stu-id="c47e3-150">This limit applies separately tooeach function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="c47e3-151">Si no desea que la ejecución en paralelo para los mensajes recibidos en una cola, Establece too1 de tamaño de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-151">If you don't want parallel execution for messages received on one queue, set hello batch size too1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="c47e3-152">Obtener metadatos de cola o de mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="c47e3-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="c47e3-153">Puede obtener Hola siguientes propiedades del mensaje mediante la adición de la firma del método toohello parámetros:</span><span class="sxs-lookup"><span data-stu-id="c47e3-153">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="c47e3-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="c47e3-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="c47e3-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="c47e3-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="c47e3-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="c47e3-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="c47e3-157">**string** queueTrigger (contiene texto de mensaje)</span><span class="sxs-lookup"><span data-stu-id="c47e3-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="c47e3-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="c47e3-158">**string** id</span></span>
* <span data-ttu-id="c47e3-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="c47e3-159">**string** popReceipt</span></span>
* <span data-ttu-id="c47e3-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="c47e3-160">**int** dequeueCount</span></span>

<span data-ttu-id="c47e3-161">Si desea que toowork directamente con hello API de almacenamiento de Azure, también puede agregar un **CloudStorageAccount** parámetro.</span><span class="sxs-lookup"><span data-stu-id="c47e3-161">If you want toowork directly with hello Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="c47e3-162">Hello en el ejemplo siguiente se escribe todos este metadatos tooan información registro de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c47e3-162">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="c47e3-163">En el ejemplo de Hola, logMessage y queueTrigger contengan Hola Hola del mensaje de cola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-163">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

<span data-ttu-id="c47e3-164">Este es un registro de ejemplo escrito código de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c47e3-164">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="c47e3-165">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="c47e3-165">Graceful shutdown</span></span>
<span data-ttu-id="c47e3-166">Una función que se ejecuta en un trabajo Web continuo puede aceptar un **CancellationToken** parámetro que permite Hola sistema operativo toonotify Hola función cuando hello trabajo Web es sobre toobe terminada.</span><span class="sxs-lookup"><span data-stu-id="c47e3-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="c47e3-167">Puede usar este toomake notificación seguro función hello no finalizar inesperadamente de forma que deja los datos en un estado incoherente.</span><span class="sxs-lookup"><span data-stu-id="c47e3-167">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="c47e3-168">Hola siguiente ejemplo se muestra cómo toocheck de inminente finalización del trabajo Web en una función.</span><span class="sxs-lookup"><span data-stu-id="c47e3-168">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

<span data-ttu-id="c47e3-169">**Nota:** Hola panel no podría mostrar correctamente el estado de Hola y salida de funciones que se haya cerrado.</span><span class="sxs-lookup"><span data-stu-id="c47e3-169">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="c47e3-170">Para obtener más información, consulte [Cierre estable de WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="c47e3-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="c47e3-171">¿Cómo toocreate una cola de mensajes al procesar un mensaje de cola</span><span class="sxs-lookup"><span data-stu-id="c47e3-171">How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="c47e3-172">una función que crea un nuevo mensaje de cola, use hello toowrite **cola** atributo.</span><span class="sxs-lookup"><span data-stu-id="c47e3-172">toowrite a function that creates a new queue message, use hello **Queue** attribute.</span></span> <span data-ttu-id="c47e3-173">Al igual que **QueueTrigger**, se pasa el nombre de la cola de hello como una cadena o bien puede [establecer nombre de la cola de hello dinámicamente](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c47e3-173">Like **QueueTrigger**, you pass in hello queue name as a string or you can [set hello queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="c47e3-174">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="c47e3-174">String queue messages</span></span>
<span data-ttu-id="c47e3-175">Hola siguiendo el ejemplo de código asincrónico no crea un nuevo mensaje de cola en la cola de hello denominado "outputqueue" con hello igual contenido como mensaje de bienvenida de cola se recibió en cola Hola denominado "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="c47e3-175">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="c47e3-176">(En el caso de las funciones asincrónicas, use **IAsyncCollector<T>** como se muestra más adelante en esta sección).</span><span class="sxs-lookup"><span data-stu-id="c47e3-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="c47e3-177">Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="c47e3-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c47e3-178">tipo de un mensaje de la cola que contiene un POCO en lugar de una cadena, pase Hola POCO toocreate como un toohello de parámetro de salida **cola** constructor de atributos.</span><span class="sxs-lookup"><span data-stu-id="c47e3-178">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="c47e3-179">Hola SDK serializa automáticamente Hola objeto tooJSON.</span><span class="sxs-lookup"><span data-stu-id="c47e3-179">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="c47e3-180">Siempre se crea un mensaje de cola, incluso si el objeto de hello es null.</span><span class="sxs-lookup"><span data-stu-id="c47e3-180">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="c47e3-181">Crear varios mensajes o en funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="c47e3-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="c47e3-182">toocreate varios mensajes, asegúrese de tipo de parámetro de hello para la cola de salida de hello **ICollector<T>**  o **IAsyncCollector<T>**, tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-182">toocreate multiple messages, make hello parameter type for hello output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="c47e3-183">Cada mensaje de la cola se crea inmediatamente cuando hello **agregar** se llama al método.</span><span class="sxs-lookup"><span data-stu-id="c47e3-183">Each queue message is created immediately when hello **Add** method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="c47e3-184">Tipos de ese atributo de la cola de hello funciona con</span><span class="sxs-lookup"><span data-stu-id="c47e3-184">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="c47e3-185">Puede usar hello **cola** atributo Hola siguientes tipos de parámetro:</span><span class="sxs-lookup"><span data-stu-id="c47e3-185">You can use hello **Queue** attribute on hello following parameter types:</span></span>

* <span data-ttu-id="c47e3-186">**cadena** (crea la cola de mensajes si el valor del parámetro es distinto de null cuando finaliza la función hello)</span><span class="sxs-lookup"><span data-stu-id="c47e3-186">**out string** (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="c47e3-187">**out byte** (funciona como **cadena**)</span><span class="sxs-lookup"><span data-stu-id="c47e3-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="c47e3-188">**out CloudQueueMessage** (funciona como **cadena**)</span><span class="sxs-lookup"><span data-stu-id="c47e3-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="c47e3-189">**out POCO** (un tipo serializable, crea un mensaje con un objeto null si el parámetro hello es nulo cuando finaliza la función hello)</span><span class="sxs-lookup"><span data-stu-id="c47e3-189">**out POCO** (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* <span data-ttu-id="c47e3-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="c47e3-190">**ICollector**</span></span>
* <span data-ttu-id="c47e3-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="c47e3-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="c47e3-192">**CloudQueue** (para crear mensajes manualmente utilizando Hola API de almacenamiento de Azure directamente)</span><span class="sxs-lookup"><span data-stu-id="c47e3-192">**CloudQueue** (for creating messages manually using hello Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a><span data-ttu-id="c47e3-193">Utilizar atributos de SDK de WebJobs en el cuerpo de Hola de una función</span><span class="sxs-lookup"><span data-stu-id="c47e3-193">Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="c47e3-194">Si necesita toodo algunas funcionan en la función antes de usar como un atributo de SDK de WebJobs **cola**, **Blob**, o **tabla**, puede usar hello **IBinder** interfaz.</span><span class="sxs-lookup"><span data-stu-id="c47e3-194">If you need toodo some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use hello **IBinder** interface.</span></span>

<span data-ttu-id="c47e3-195">Hola siguiente ejemplo toma un mensaje de la cola de entrada y crea un nuevo mensaje con hello mismo contenido en una cola de salida.</span><span class="sxs-lookup"><span data-stu-id="c47e3-195">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="c47e3-196">nombre de cola de salida de Hello se establece por código Hola cuerpo de función hello.</span><span class="sxs-lookup"><span data-stu-id="c47e3-196">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="c47e3-197">Hola **IBinder** interfaz también se puede usar con hello **tabla** y **Blob** atributos.</span><span class="sxs-lookup"><span data-stu-id="c47e3-197">hello **IBinder** interface can also be used with hello **Table** and **Blob** attributes.</span></span>

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="c47e3-198">¿Cómo tooread y escritura de blobs y tablas al procesar un mensaje de cola</span><span class="sxs-lookup"><span data-stu-id="c47e3-198">How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="c47e3-199">Hola **Blob** y **tabla** atributos permiten tooread y escribir los blobs y tablas.</span><span class="sxs-lookup"><span data-stu-id="c47e3-199">hello **Blob** and **Table** attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="c47e3-200">ejemplos de Hello en esta sección aplican tooblobs.</span><span class="sxs-lookup"><span data-stu-id="c47e3-200">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="c47e3-201">Para obtener ejemplos de código que muestran cómo tootrigger procesa cuando se crean o actualizan los blobs, vea [cómo toouse Azure blob storage con hello SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)y para obtener ejemplos de código que leen y escriben las tablas, vea [cómo toouse tabla de Azure almacenamiento con hello SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="c47e3-201">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="c47e3-202">Mensajes en cola de cadena que desencadenan operaciones de blob</span><span class="sxs-lookup"><span data-stu-id="c47e3-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="c47e3-203">Para un mensaje de la cola que contiene una cadena, **queueTrigger** es un marcador de posición que se puede usar en hello **Blob** del atributo **blobPath** parámetro que contiene el contenido de Hola de mensaje de saludo.</span><span class="sxs-lookup"><span data-stu-id="c47e3-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in hello **Blob** attribute's **blobPath** parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="c47e3-204">Hello siguiente ejemplo se utiliza **flujo** objetos tooread y escritura de blobs.</span><span class="sxs-lookup"><span data-stu-id="c47e3-204">hello following example uses **Stream** objects tooread and write blobs.</span></span> <span data-ttu-id="c47e3-205">mensaje de bienvenida de cola es nombre Hola de un blob ubicado en hello textblobs contenedor.</span><span class="sxs-lookup"><span data-stu-id="c47e3-205">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="c47e3-206">Una copia de blob de hello con "-nuevo" anexado toohello nombre se crea en Hola mismo contenedor.</span><span class="sxs-lookup"><span data-stu-id="c47e3-206">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="c47e3-207">Hola **Blob** atributo constructor toma un **blobPath** parámetro que especifica el contenedor de Hola y el nombre de blob.</span><span class="sxs-lookup"><span data-stu-id="c47e3-207">hello **Blob** attribute constructor takes a **blobPath** parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="c47e3-208">Para obtener más información acerca de este marcador de posición, vea [cómo toouse Azure blob storage con hello SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="c47e3-208">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="c47e3-209">Cuando el atributo de hello decora un **flujo** objeto, otro parámetro de constructor especifica hello **FileAccess** modo como lectura, escritura o lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="c47e3-209">When hello attribute decorates a **Stream** object, another constructor parameter specifies hello **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="c47e3-210">Hello ejemplo siguiente se usa un **CloudBlockBlob** toodelete un blob del objeto.</span><span class="sxs-lookup"><span data-stu-id="c47e3-210">hello following example uses a **CloudBlockBlob** object toodelete a blob.</span></span> <span data-ttu-id="c47e3-211">mensaje de bienvenida de cola es nombre Hola de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-211">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="c47e3-212">Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="c47e3-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="c47e3-213">Para un POCO almacenado como JSON en el mensaje de bienvenida de cola, puede utilizar marcadores de posición que nombres de las propiedades del objeto de Hola Hola **cola** del atributo **blobPath** parámetro.</span><span class="sxs-lookup"><span data-stu-id="c47e3-213">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="c47e3-214">También puede utilizar nombres de propiedad de metadatos de cola como marcadores de posición.</span><span class="sxs-lookup"><span data-stu-id="c47e3-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="c47e3-215">Consulte [Obtener metadatos de cola o de mensaje en cola](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="c47e3-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="c47e3-216">Hello en el ejemplo siguiente se copia un blob nuevo de blob tooa con una extensión diferente.</span><span class="sxs-lookup"><span data-stu-id="c47e3-216">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="c47e3-217">mensaje de bienvenida de cola es un **BlobInformation** objeto que incluya **BlobName** y **BlobNameWithoutExtension** propiedades.</span><span class="sxs-lookup"><span data-stu-id="c47e3-217">hello queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="c47e3-218">nombres de propiedad de Hola se utilizan como marcadores de posición en la ruta de acceso de blob de Hola para hello **Blob** atributos.</span><span class="sxs-lookup"><span data-stu-id="c47e3-218">hello property names are used as placeholders in hello blob path for hello **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="c47e3-219">Hola SDK utiliza hello [paquete NuGet de Newtonsoft.Json](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize y deserializar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="c47e3-219">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="c47e3-220">Si crea mensajes en cola en un programa que no utilice Hola SDK de WebJobs, puede escribir código como sigue toocreate un POCO de la cola de mensajes de ejemplo de Hola ese Hola que SDK puede analizar.</span><span class="sxs-lookup"><span data-stu-id="c47e3-220">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="c47e3-221">Si necesita toodo algunas funcionan en la función antes de enlazar un objeto de tooan de blob, puede utilizar atributos de hello en el cuerpo de Hola de función de hello, tal y como se muestra en [atributos de usar el SDK de WebJobs en el cuerpo de Hola de una función](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="c47e3-221">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, as shown in [Use WebJobs SDK attributes in hello body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-hello-blob-attribute-with"></a><span data-ttu-id="c47e3-222">Tipos que puede usar Hola Blob de atributo con</span><span class="sxs-lookup"><span data-stu-id="c47e3-222">Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="c47e3-223">Hola **Blob** atributo se puede usar con hello siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="c47e3-223">hello **Blob** attribute can be used with hello following types:</span></span>

* <span data-ttu-id="c47e3-224">**Secuencia** (lectura o escritura, especificado mediante el parámetro de constructor de hello FileAccess)</span><span class="sxs-lookup"><span data-stu-id="c47e3-224">**Stream** (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* <span data-ttu-id="c47e3-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="c47e3-225">**TextReader**</span></span>
* <span data-ttu-id="c47e3-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="c47e3-226">**TextWriter**</span></span>
* <span data-ttu-id="c47e3-227">**string** (lectura)</span><span class="sxs-lookup"><span data-stu-id="c47e3-227">**string** (read)</span></span>
* <span data-ttu-id="c47e3-228">**cadena** (escribir; crea un blob solo si el parámetro de cadena de hello es distinto de null cuando la devolución de función hello)</span><span class="sxs-lookup"><span data-stu-id="c47e3-228">**out string** (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="c47e3-229">POCO (lectura)</span><span class="sxs-lookup"><span data-stu-id="c47e3-229">POCO (read)</span></span>
* <span data-ttu-id="c47e3-230">out POCO (escribir; siempre crea un blob, se crea como objeto null si POCO parámetro es null cuando la devolución de función hello)</span><span class="sxs-lookup"><span data-stu-id="c47e3-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="c47e3-231">**CloudBlobStream** (escritura)</span><span class="sxs-lookup"><span data-stu-id="c47e3-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="c47e3-232">**ICloudBlob** (lectura o escritura)</span><span class="sxs-lookup"><span data-stu-id="c47e3-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="c47e3-233">**CloudBlockBlob** (lectura o escritura)</span><span class="sxs-lookup"><span data-stu-id="c47e3-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="c47e3-234">**CloudPageBlob** (lectura o escritura)</span><span class="sxs-lookup"><span data-stu-id="c47e3-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-toohandle-poison-messages"></a><span data-ttu-id="c47e3-235">¿Cómo toohandle dudosos mensajes</span><span class="sxs-lookup"><span data-stu-id="c47e3-235">How toohandle poison messages</span></span>
<span data-ttu-id="c47e3-236">Se denominan mensajes cuyo contenido hace que una función toofail *mensajes dudosos*.</span><span class="sxs-lookup"><span data-stu-id="c47e3-236">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="c47e3-237">Cuando se produce un error en la función hello, mensaje de bienvenida de cola no se elimina y finalmente recoge nuevo, que producen Hola ciclo toobe repetido.</span><span class="sxs-lookup"><span data-stu-id="c47e3-237">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="c47e3-238">Hola SDK automáticamente puede interrumpir el ciclo de hello después de un número limitado de iteraciones, o puede hacerlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="c47e3-238">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="c47e3-239">Control automático de mensajes dudosos</span><span class="sxs-lookup"><span data-stu-id="c47e3-239">Automatic poison message handling</span></span>
<span data-ttu-id="c47e3-240">Hola SDK llamará a una función de seguridad too5 veces tooprocess un mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-240">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="c47e3-241">Si se produce un error en try quinto hello, mensaje de bienvenida es movida tooa cola de mensajes dudosos.</span><span class="sxs-lookup"><span data-stu-id="c47e3-241">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="c47e3-242">Puede ver cómo tooconfigure Hola número máximo de reintentos en [cómo opciones de configuración de tooset](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c47e3-242">You can see how tooconfigure hello maximum number of retries in [How tooset configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="c47e3-243">cola de mensajes dudosos Hola se denomina *{originalqueuename}*-dudoso.</span><span class="sxs-lookup"><span data-stu-id="c47e3-243">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="c47e3-244">Puede escribir una función tooprocess mensajes desde la cola de mensajes dudosos Hola registrarlos o enviar una notificación que se necesita atención manual.</span><span class="sxs-lookup"><span data-stu-id="c47e3-244">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="c47e3-245">Después de hello de ejemplo de Hola **CopyBlob** function no funcionará correctamente cuando un mensaje de la cola contiene el nombre de Hola de un blob que no existe.</span><span class="sxs-lookup"><span data-stu-id="c47e3-245">In hello following example hello **CopyBlob** function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="c47e3-246">Cuando esto ocurre, mensaje de saludo se mueve desde hello copyblobqueue toohello copyblobqueue dudosos cola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-246">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="c47e3-247">Hola **ProcessPoisonMessage** , a continuación, registros de Hola de mensajes dudosos.</span><span class="sxs-lookup"><span data-stu-id="c47e3-247">hello **ProcessPoisonMessage** then logs hello poison message.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

<span data-ttu-id="c47e3-248">Hello en la ilustración siguiente se muestra la salida de consola de estas funciones cuando se procesa un mensaje dudoso.</span><span class="sxs-lookup"><span data-stu-id="c47e3-248">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Salida de consola para el control de mensajes dudosos](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="c47e3-250">Control manual de mensajes dudosos</span><span class="sxs-lookup"><span data-stu-id="c47e3-250">Manual poison message handling</span></span>
<span data-ttu-id="c47e3-251">Puede obtener Hola número de veces que se ha detectado un mensaje para su procesamiento mediante la adición de un **int** parámetro denominado **dequeueCount** tooyour (función).</span><span class="sxs-lookup"><span data-stu-id="c47e3-251">You can get hello number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** tooyour function.</span></span> <span data-ttu-id="c47e3-252">También puede, a continuación, Hola de comprobación de recuento en el código de la función de eliminación de cola y realizar su propio control de mensajes dudosos al número de hello supera un umbral, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-252">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-tooset-configuration-options"></a><span data-ttu-id="c47e3-253">¿Cómo tooset las opciones de configuración</span><span class="sxs-lookup"><span data-stu-id="c47e3-253">How tooset configuration options</span></span>
<span data-ttu-id="c47e3-254">Puede usar hello **JobHostConfiguration** Hola de tipo tooset opciones de configuración siguientes:</span><span class="sxs-lookup"><span data-stu-id="c47e3-254">You can use hello **JobHostConfiguration** type tooset hello following configuration options:</span></span>

* <span data-ttu-id="c47e3-255">Establecer las cadenas de conexión de SDK de hello en el código.</span><span class="sxs-lookup"><span data-stu-id="c47e3-255">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="c47e3-256">Definir la configuración **QueueTrigger** como el número máximo de eliminaciones de la cola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="c47e3-257">Obtener nombres de cola a partir de la configuración.</span><span class="sxs-lookup"><span data-stu-id="c47e3-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="c47e3-258">Establecer cadenas de conexión de SDK en el código</span><span class="sxs-lookup"><span data-stu-id="c47e3-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="c47e3-259">Establecer las cadenas de conexión de SDK de hello en el código permite toouse sus propios nombres de cadena de conexión en archivos de configuración o las variables de entorno, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-259">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="c47e3-260">Configurar QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="c47e3-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="c47e3-261">Puede configurar Hola después de la configuración que se aplica el procesamiento de mensajes de cola de toohello:</span><span class="sxs-lookup"><span data-stu-id="c47e3-261">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="c47e3-262">número máximo de mensajes en cola que se recogen simultáneamente toobe ejecutada en paralelo de Hola (el valor predeterminado es 16).</span><span class="sxs-lookup"><span data-stu-id="c47e3-262">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="c47e3-263">Hola número máximo de reintentos antes de enviar un mensaje de cola de cola de mensajes dudosos tooa (el valor predeterminado es 5).</span><span class="sxs-lookup"><span data-stu-id="c47e3-263">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="c47e3-264">tiempo de espera máximo de Hello antes de volver a sondear cuando una cola está vacía (el valor predeterminado es 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="c47e3-264">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="c47e3-265">Hola siguiente ejemplo se muestra cómo tooconfigure esta configuración:</span><span class="sxs-lookup"><span data-stu-id="c47e3-265">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="c47e3-266">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="c47e3-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="c47e3-267">A veces desea toospecify un nombre de cola, un nombre de blob o contenedor o una tabla asígnele el nombre en código, en lugar de codificar de forma rígida.</span><span class="sxs-lookup"><span data-stu-id="c47e3-267">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="c47e3-268">Por ejemplo, puede querer toospecify nombre de cola de Hola para **QueueTrigger** en una variable de entorno o de archivo de configuración.</span><span class="sxs-lookup"><span data-stu-id="c47e3-268">For example, you might want toospecify hello queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="c47e3-269">Puede hacerlo pasando un **NameResolver** objeto toohello **JobHostConfiguration** tipo.</span><span class="sxs-lookup"><span data-stu-id="c47e3-269">You can do that by passing in a **NameResolver** object toohello **JobHostConfiguration** type.</span></span> <span data-ttu-id="c47e3-270">Incluir marcadores de posición especial entre signos de porcentaje (%) en los parámetros del constructor de atributo de SDK de WebJobs y su **NameResolver** código especifica Hola valores reales toobe usar en lugar de los marcadores de posición.</span><span class="sxs-lookup"><span data-stu-id="c47e3-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="c47e3-271">Por ejemplo, suponga que desea toouse una cola denominada logqueuetest en entorno de prueba de hello y una logqueueprod con nombre en producción.</span><span class="sxs-lookup"><span data-stu-id="c47e3-271">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="c47e3-272">En lugar de un nombre de cola codificado de forma rígida, desea que el nombre de Hola de toospecify de una entrada en hello **appSettings** colección que tendría el nombre de la cola real de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-272">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello **appSettings** collection that would have hello actual queue name.</span></span> <span data-ttu-id="c47e3-273">Si hello **appSettings** clave es logqueue, la función podría tener el aspecto como el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-273">If hello **appSettings** key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="c47e3-274">Su **NameResolver** clase, a continuación, pudo obtener el nombre de la cola de Hola de **appSettings** tal y como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c47e3-274">Your **NameResolver** class could then get hello queue name from **appSettings** as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="c47e3-275">Pasar hello **NameResolver** clase toohello **JobHost** objeto tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-275">You pass hello **NameResolver** class in toohello **JobHost** object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="c47e3-276">**Nota:** nombres de blob, cola y tabla son de resolver cada vez que se invoque una función, pero se resuelven los nombres de contenedor de blob solamente cuando se inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c47e3-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="c47e3-277">No se puede cambiar el nombre del contenedor de blob mientras se ejecuta el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-277">You can't change blob container name while hello job is running.</span></span>

## <a name="how-tootrigger-a-function-manually"></a><span data-ttu-id="c47e3-278">¿Cómo tootrigger una función manualmente</span><span class="sxs-lookup"><span data-stu-id="c47e3-278">How tootrigger a function manually</span></span>
<span data-ttu-id="c47e3-279">una función de tootrigger manualmente, use hello **llamar a** o **CallAsync** método en hello **JobHost** hello y objeto **NoAutomaticTrigger** atributo en función de hello, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-279">tootrigger a function manually, use hello **Call** or **CallAsync** method on hello **JobHost** object and hello **NoAutomaticTrigger** attribute on hello function, as shown in hello following example.</span></span>

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a name="how-toowrite-logs"></a><span data-ttu-id="c47e3-280">Funcionamiento de los registros toowrite</span><span class="sxs-lookup"><span data-stu-id="c47e3-280">How toowrite logs</span></span>
<span data-ttu-id="c47e3-281">Hola panel muestra los registros en dos lugares: Hola para hello trabajo Web y Hola página para una invocación de trabajo Web determinada.</span><span class="sxs-lookup"><span data-stu-id="c47e3-281">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Registros en la página del trabajo web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Registros en la página de invocación de la función](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="c47e3-284">Salida de métodos de consola que se llama en una función o en hello **Main()** método aparece en la página de panel de Hola de hello trabajo Web, no en la página de Hola para una invocación de método determinado.</span><span class="sxs-lookup"><span data-stu-id="c47e3-284">Output from Console methods that you call in a function or in hello **Main()** method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="c47e3-285">Resultado del objeto de TextWriter Hola que obtendrá de un parámetro en la firma del método aparece en la página de panel de Hola de una invocación de método.</span><span class="sxs-lookup"><span data-stu-id="c47e3-285">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="c47e3-286">Salida de la consola no puede ser la invocación del método determinado tooa vinculado porque Hola consola tiene un único subproceso, mientras que muchas de las funciones de trabajo pueden estar ejecutando en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="c47e3-286">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="c47e3-287">Por eso Hola SDK proporciona cada invocación de función con su propio objeto de escritor de inicio de sesión únicos.</span><span class="sxs-lookup"><span data-stu-id="c47e3-287">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="c47e3-288">toowrite [registros de seguimiento de la aplicación](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (crea registros marcados como información) y **Console.Error** (crea registros marcados como ERROR).</span><span class="sxs-lookup"><span data-stu-id="c47e3-288">toowrite [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="c47e3-289">Una alternativa es toouse [seguimiento o TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que proporciona Verbose, advertencia, y niveles de crítico en tooInfo de adición y Error.</span><span class="sxs-lookup"><span data-stu-id="c47e3-289">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="c47e3-290">Registros de seguimiento de la aplicación aparecen en archivos de registro en la aplicación web de hello, tablas de Azure, o blobs de Azure según cómo configure la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="c47e3-290">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="c47e3-291">Como ocurre con todos los resultados de la consola, registros de aplicación 100 más recientes de hello también aparecen en la página de panel de Hola de hello trabajo Web, no la página de Hola de una invocación de función.</span><span class="sxs-lookup"><span data-stu-id="c47e3-291">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="c47e3-292">Salida de la consola aparece en hello panel únicamente si se ejecuta el programa de hello en un trabajo Web de Azure, no si programa Hola se ejecuta localmente o en algún otro entorno.</span><span class="sxs-lookup"><span data-stu-id="c47e3-292">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="c47e3-293">Puede deshabilitar el registro estableciendo toonull de cadena de conexión de hello panel.</span><span class="sxs-lookup"><span data-stu-id="c47e3-293">You can disable logging by setting hello Dashboard connection string toonull.</span></span> <span data-ttu-id="c47e3-294">Para obtener más información, consulte [cómo tooset opciones de configuración](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="c47e3-294">For more information, see [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="c47e3-295">Hello en el ejemplo siguiente se muestra varias maneras de toowrite registros:</span><span class="sxs-lookup"><span data-stu-id="c47e3-295">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="c47e3-296">En el panel de SDK de WebJobs de hello, Hola salida de hello **TextWriter** se muestra cuando se desplace página toohello para un determinado invocación de función y seleccione objetos **alternar salida**:</span><span class="sxs-lookup"><span data-stu-id="c47e3-296">In hello WebJobs SDK Dashboard, hello output from hello **TextWriter** object shows up when you go toohello page for a particular function invocation and select **Toggle Output**:</span></span>

![Vínculo de invocación](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Registros en la página de invocación de la función](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="c47e3-299">En el panel de SDK de WebJobs de hello, líneas de hello 100 más reciente de la consola de salida mostrar una al ir a página toohello para hello trabajo Web (no de invocación de función hello) y seleccione **alternar salida**.</span><span class="sxs-lookup"><span data-stu-id="c47e3-299">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and select **Toggle Output**.</span></span>

![Toggle Output](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="c47e3-301">En un trabajo Web continuo, registros de aplicaciones se mostrarán en/datos/trabajos/continua/*{webjobname}*/job_log.txt en sistema de archivos de aplicación web de Hola.</span><span class="sxs-lookup"><span data-stu-id="c47e3-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="c47e3-302">En una aplicación Hola de blobs de Azure registros este aspecto: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write: Hola a todos!, 2014-09-26T21:01:13, Error, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.Error - Hola a todos!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out: Hola a todos!,</span><span class="sxs-lookup"><span data-stu-id="c47e3-302">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="c47e3-303">Y en un saludo de la tabla de Azure **Console.Out** y **Console.Error** registros tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="c47e3-303">And in an Azure table hello **Console.Out** and **Console.Error** logs look like this:</span></span>

![Registro de información en la tabla](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Registro de errores en la tabla](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="c47e3-306">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c47e3-306">Next steps</span></span>
<span data-ttu-id="c47e3-307">En este artículo ha proporcionado el código de ejemplos que muestran cómo toohandle escenarios comunes para trabajar con colas de Azure.</span><span class="sxs-lookup"><span data-stu-id="c47e3-307">This article has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="c47e3-308">Para obtener más información sobre cómo toouse WebJobs de Azure y Hola SDK de WebJobs, vea [recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="c47e3-308">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

