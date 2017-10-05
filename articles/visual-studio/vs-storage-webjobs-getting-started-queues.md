---
title: "Introducción al almacenamiento de colas y servicios conectados de Visual Studio (proyectos de WebJobs) | Microsoft Docs"
description: "Cómo empezar a usar el almacenamiento de colas de Azure en un proyecto de WebJob después de conectarse a una cuenta de almacenamiento con los servicios conectados de Visual Studio."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: ef40db782114bfdaa02dafeabcfc6da6c41423e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="40c50-103">Introducción al Almacenamiento de colas de Azure y servicios conectados de Visual Studio (proyectos de WebJobs)</span><span class="sxs-lookup"><span data-stu-id="40c50-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="40c50-104">Información general</span><span class="sxs-lookup"><span data-stu-id="40c50-104">Overview</span></span>
<span data-ttu-id="40c50-105">En este artículo se describe cómo empezar a usar Azure Queue Storage en un proyecto de WebJobs de Azure de Visual Studio después de crear una cuenta de almacenamiento de Azure o hacer referencia a ella con el cuadro de diálogo **Agregar servicios conectados** de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="40c50-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using the Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="40c50-106">Al agregar una cuenta de almacenamiento a un proyecto de WebJobs con el cuadro de diálogo **Agregar servicios conectados** de Visual Studio, se instalan los paquetes de NuGet de Almacenamiento de Azure adecuados, se agregan las referencias de .NET adecuadas al proyecto y se actualizan las cadenas de conexión para la cuenta de almacenamiento en el archivo App.config.</span><span class="sxs-lookup"><span data-stu-id="40c50-106">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet packages are installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>  

<span data-ttu-id="40c50-107">En este artículo se ofrecen ejemplos de código C# que muestran cómo usar la versión 1.x del SDK de WebJobs de Azure con el servicio Almacenamiento de colas de Azure.</span><span class="sxs-lookup"><span data-stu-id="40c50-107">This article provides C# code samples that show how to use the Azure WebJobs SDK version 1.x with the Azure Queue storage service.</span></span>

<span data-ttu-id="40c50-108">El almacenamiento en cola de Azure es un servicio para almacenar grandes cantidades de mensajes a los que puede obtenerse acceso desde cualquier lugar del mundo a través de llamadas autenticadas con HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="40c50-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="40c50-109">Un único mensaje en cola puede tener un tamaño de hasta 64 KB y una cola puede contener millones de mensajes, hasta el límite de capacidad total de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="40c50-109">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span> <span data-ttu-id="40c50-110">Consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="40c50-110">See [Get started with Azure Queue Storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="40c50-111">Para obtener más información acerca de ASP.NET, consulte [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="40c50-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-to-trigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="40c50-112">Desencadenar una función cuando se recibe un mensaje de cola</span><span class="sxs-lookup"><span data-stu-id="40c50-112">How to trigger a function when a queue message is received</span></span>
<span data-ttu-id="40c50-113">Para escribir una función que el SDK de WebJobs llama cuando se recibe un mensaje en cola, use el atributo **QueueTrigge** .</span><span class="sxs-lookup"><span data-stu-id="40c50-113">To write a function that the WebJobs SDK calls when a queue message is received, use the **QueueTrigger** attribute.</span></span> <span data-ttu-id="40c50-114">El constructor de atributo toma un parámetro de cadena que especifica el nombre de la cola para sondear.</span><span class="sxs-lookup"><span data-stu-id="40c50-114">The attribute constructor takes a string parameter that specifies the name of the queue to poll.</span></span> <span data-ttu-id="40c50-115">Para ver cómo establecer dinámicamente el nombre de la cola, consulte [Establecimiento de opciones de configuración](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="40c50-115">To see how to set the queue name dynamically, check out [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="40c50-116">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="40c50-116">String queue messages</span></span>
<span data-ttu-id="40c50-117">En el ejemplo siguiente, la cola contiene un mensaje de cadena, por lo que **QueueTrigger** se aplica a un parámetro de cadena llamado **logMessage** que tiene el contenido del mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="40c50-117">In the following example, the queue contains a string message, so **QueueTrigger** is applied to a string parameter named **logMessage** which contains the content of the queue message.</span></span> <span data-ttu-id="40c50-118">La función [escribe un mensaje de registro en el panel](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="40c50-118">The function [writes a log message to the Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="40c50-119">Además de **string**, el parámetro puede ser una matriz de bytes, un objeto **CloudQueueMessage** o un objeto POCO que defina.</span><span class="sxs-lookup"><span data-stu-id="40c50-119">Besides **string**, the parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="40c50-120">Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="40c50-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="40c50-121">En el ejemplo siguiente, el mensaje de cola contiene JSON para un objeto **BlobInformation** que incluye una propiedad **BlobName**.</span><span class="sxs-lookup"><span data-stu-id="40c50-121">In the following example, the queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="40c50-122">El SDK automáticamente deserializa el objeto.</span><span class="sxs-lookup"><span data-stu-id="40c50-122">The SDK automatically deserializes the object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers to blob: " + blobInfo.BlobName);
        }

<span data-ttu-id="40c50-123">El SDK usa el [paquete Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) para serializar y deserializar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="40c50-123">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="40c50-124">Si crea mensajes en cola en un programa que no usa el SDK de WebJobs, puede escribir código similar al siguiente ejemplo para crear un mensaje en cola POCO que pueda analizar el SDK.</span><span class="sxs-lookup"><span data-stu-id="40c50-124">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="40c50-125">Funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="40c50-125">Async functions</span></span>
<span data-ttu-id="40c50-126">La siguiente función async [escribe un registro en el panel](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="40c50-126">The following async function [writes a log to the Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="40c50-127">Las funciones asincrónicas pueden tomar un [token de cancelación](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), como se muestra en el siguiente ejemplo, que copia un blob.</span><span class="sxs-lookup"><span data-stu-id="40c50-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in the following example which copies a blob.</span></span> <span data-ttu-id="40c50-128">(Para obtener una explicación del marcador de posición **queueTrigger** , consulte la sección [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) ).</span><span class="sxs-lookup"><span data-stu-id="40c50-128">(For an explanation of the **queueTrigger** placeholder, see the [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-the-queuetrigger-attribute-works-with"></a><span data-ttu-id="40c50-129">Tipos con los que funciona el atributo QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="40c50-129">Types the QueueTrigger attribute works with</span></span>
<span data-ttu-id="40c50-130">Puede usar **QueueTrigger** con los tipos siguientes:</span><span class="sxs-lookup"><span data-stu-id="40c50-130">You can use **QueueTrigger** with the following types:</span></span>

* <span data-ttu-id="40c50-131">**cadena**</span><span class="sxs-lookup"><span data-stu-id="40c50-131">**string**</span></span>
* <span data-ttu-id="40c50-132">Un tipo de POCO serializado como JSON</span><span class="sxs-lookup"><span data-stu-id="40c50-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="40c50-133">**byte[]**</span><span class="sxs-lookup"><span data-stu-id="40c50-133">**byte[]**</span></span>
* <span data-ttu-id="40c50-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="40c50-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="40c50-135">Algoritmo de sondeo</span><span class="sxs-lookup"><span data-stu-id="40c50-135">Polling algorithm</span></span>
<span data-ttu-id="40c50-136">El SDK implementa un algoritmo de interrupción exponencial aleatorio para reducir el efecto del sondeo de cola inactiva en los costos de transacción de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="40c50-136">The SDK implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="40c50-137">Cuando se encuentra un mensaje, el SDK espera dos segundos y, a continuación, comprueba si hay otro mensaje; cuando no se encuentra ningún mensaje, espera unos cuatro segundos antes de intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="40c50-137">When a message is found, the SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="40c50-138">Después de varios intentos fallidos para obtener un mensaje de la cola, el tiempo de espera sigue aumentando hasta que alcanza el tiempo de espera máximo, predeterminado en un minuto.</span><span class="sxs-lookup"><span data-stu-id="40c50-138">After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.</span></span> <span data-ttu-id="40c50-139">[El tiempo de espera máximo es configurable](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="40c50-139">[The maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="40c50-140">Varias instancias</span><span class="sxs-lookup"><span data-stu-id="40c50-140">Multiple instances</span></span>
<span data-ttu-id="40c50-141">Si la aplicación web se ejecuta en varias instancias, un WebJobs continuo se ejecuta en cada máquina y estas, a su vez, esperarán a los desencadenadores e intentarán ejecutar funciones.</span><span class="sxs-lookup"><span data-stu-id="40c50-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt to run functions.</span></span> <span data-ttu-id="40c50-142">En algunos escenarios puede ocurrir que algunas funciones procesen los mismos datos dos veces, por lo que las funciones deben ser idempotentes (escritas de tal forma que al llamarlas repetidamente con los mismos datos de entrada no se generen resultados duplicados).</span><span class="sxs-lookup"><span data-stu-id="40c50-142">In some scenarios this can lead to some functions processing the same data twice, so functions should be idempotent (written so that calling them repeatedly with the same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="40c50-143">Ejecución en paralelo</span><span class="sxs-lookup"><span data-stu-id="40c50-143">Parallel execution</span></span>
<span data-ttu-id="40c50-144">Si tiene varias funciones escuchando en diferentes colas, el SDK las llamará en paralelo cuando se reciban mensajes simultáneamente.</span><span class="sxs-lookup"><span data-stu-id="40c50-144">If you have multiple functions listening on different queues, the SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="40c50-145">Esto también se da cuando se reciben varios mensajes de una sola cola.</span><span class="sxs-lookup"><span data-stu-id="40c50-145">The same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="40c50-146">De forma predeterminada, el SDK obtiene un lote de 16 mensajes de la cola a la vez y ejecuta la función que se procesa en paralelo.</span><span class="sxs-lookup"><span data-stu-id="40c50-146">By default, the SDK gets a batch of 16 queue messages at a time and executes the function that processes them in parallel.</span></span> <span data-ttu-id="40c50-147">[El tamaño del lote es configurable](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="40c50-147">[The batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="40c50-148">Cuando el número que se está procesando llegue a la mitad del tamaño del lote, el SDK obtiene otro lote y empieza a procesar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="40c50-148">When the number being processed gets down to half of the batch size, the SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="40c50-149">Por lo tanto, el número máximo de mensajes simultáneos que se procesan por función es uno y medio por el tamaño del lote.</span><span class="sxs-lookup"><span data-stu-id="40c50-149">Therefore the maximum number of concurrent messages being processed per function is one and a half times the batch size.</span></span> <span data-ttu-id="40c50-150">Este límite se aplica por separado para cada función que tenga un atributo **QueueTrigger** .</span><span class="sxs-lookup"><span data-stu-id="40c50-150">This limit applies separately to each function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="40c50-151">Si no desea la ejecución en paralelo de los mensajes en una cola, establezca el tamaño del lote en 1.</span><span class="sxs-lookup"><span data-stu-id="40c50-151">If you don't want parallel execution for messages received on one queue, set the batch size to 1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="40c50-152">Obtener metadatos de cola o de mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="40c50-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="40c50-153">Puede obtener las siguientes propiedades de mensaje agregando parámetros a la firma del método:</span><span class="sxs-lookup"><span data-stu-id="40c50-153">You can get the following message properties by adding parameters to the method signature:</span></span>

* <span data-ttu-id="40c50-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="40c50-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="40c50-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="40c50-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="40c50-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="40c50-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="40c50-157">**string** queueTrigger (contiene texto de mensaje)</span><span class="sxs-lookup"><span data-stu-id="40c50-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="40c50-158">**string** id</span><span class="sxs-lookup"><span data-stu-id="40c50-158">**string** id</span></span>
* <span data-ttu-id="40c50-159">**string** popReceipt</span><span class="sxs-lookup"><span data-stu-id="40c50-159">**string** popReceipt</span></span>
* <span data-ttu-id="40c50-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="40c50-160">**int** dequeueCount</span></span>

<span data-ttu-id="40c50-161">Si desea trabajar directamente con la API de almacenamiento de Azure, también puede agregar un parámetro **CloudStorageAccount** .</span><span class="sxs-lookup"><span data-stu-id="40c50-161">If you want to work directly with the Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="40c50-162">En el siguiente ejemplo escribirá todos estos metadatos en un registro de aplicación de información.</span><span class="sxs-lookup"><span data-stu-id="40c50-162">The following example writes all of this metadata to an INFO application log.</span></span> <span data-ttu-id="40c50-163">En el ejemplo, logMessage y queueTrigger contienen el contenido del mensaje en cola.</span><span class="sxs-lookup"><span data-stu-id="40c50-163">In the example, both logMessage and queueTrigger contain the content of the queue message.</span></span>

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

<span data-ttu-id="40c50-164">Este es un registro de ejemplo escrito por el código de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="40c50-164">Here is a sample log written by the sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="40c50-165">Apagado correcto</span><span class="sxs-lookup"><span data-stu-id="40c50-165">Graceful shutdown</span></span>
<span data-ttu-id="40c50-166">Una función que se ejecuta en un WebJob continuo puede aceptar un parámetro **CancellationToken** que permite al sistema operativo notificar a la función cuando el WebJob está a punto de terminar.</span><span class="sxs-lookup"><span data-stu-id="40c50-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables the operating system to notify the function when the WebJob is about to be terminated.</span></span> <span data-ttu-id="40c50-167">Puede utilizar esta notificación para asegurarse de que la función no se termina inesperadamente en una forma que deje los datos en un estado incoherente.</span><span class="sxs-lookup"><span data-stu-id="40c50-167">You can use this notification to make sure the function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="40c50-168">En el ejemplo siguiente se muestra cómo comprobar la finalización de WebJob inminente en una función.</span><span class="sxs-lookup"><span data-stu-id="40c50-168">The following example shows how to check for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="40c50-169">**Nota:** el Panel puede no mostrar correctamente el estado y la salida de funciones que se hayan cerrado.</span><span class="sxs-lookup"><span data-stu-id="40c50-169">**Note:** The Dashboard might not correctly show the status and output of functions that have been shut down.</span></span>

<span data-ttu-id="40c50-170">Para obtener más información, consulte [Cierre estable de WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="40c50-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-to-create-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="40c50-171">Creación de un mensaje de cola al procesar un mensaje de cola</span><span class="sxs-lookup"><span data-stu-id="40c50-171">How to create a queue message while processing a queue message</span></span>
<span data-ttu-id="40c50-172">Para escribir una función que crea un mensaje en cola nuevo, use el atributo **Queue** .</span><span class="sxs-lookup"><span data-stu-id="40c50-172">To write a function that creates a new queue message, use the **Queue** attribute.</span></span> <span data-ttu-id="40c50-173">Al igual que **QueueTrigger**, pasa el nombre de cola como una cadena o puede [establecer el nombre de la cola dinámicamente](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="40c50-173">Like **QueueTrigger**, you pass in the queue name as a string or you can [set the queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="40c50-174">Mensajes en cola de cadena</span><span class="sxs-lookup"><span data-stu-id="40c50-174">String queue messages</span></span>
<span data-ttu-id="40c50-175">El siguiente ejemplo de código no asincrónico crea un mensaje en cola nuevo en la cola llamada "outputqueue", con el mismo contenido que el mensaje en cola recibido en la cola llamada "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="40c50-175">The following non-async code sample creates a new queue message in the queue named "outputqueue" with the same content as the queue message received in the queue named "inputqueue".</span></span> <span data-ttu-id="40c50-176">(En el caso de las funciones asincrónicas, use **IAsyncCollector<T>** como se muestra más adelante en esta sección).</span><span class="sxs-lookup"><span data-stu-id="40c50-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="40c50-177">Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="40c50-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="40c50-178">Para crear un mensaje en cola que contiene un objeto POCO en lugar de una cadena, pase el tipo POCO como un parámetro de salida al constructor de atributo **Queue** .</span><span class="sxs-lookup"><span data-stu-id="40c50-178">To create a queue message that contains a POCO rather than a string, pass the POCO type as an output parameter to the **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="40c50-179">El SDK serializa automáticamente el objeto a JSON.</span><span class="sxs-lookup"><span data-stu-id="40c50-179">The SDK automatically serializes the object to JSON.</span></span> <span data-ttu-id="40c50-180">Siempre se crea un mensaje en cola, incluso si el objeto es null.</span><span class="sxs-lookup"><span data-stu-id="40c50-180">A queue message is always created, even if the object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="40c50-181">Crear varios mensajes o en funciones asincrónicas</span><span class="sxs-lookup"><span data-stu-id="40c50-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="40c50-182">Para crear varios mensajes, convierta el tipo de parámetro para la cola de salida **ICollector<T>** o **IAsyncCollector<T>**, como se muestra en el siguiente ejemplo.</span><span class="sxs-lookup"><span data-stu-id="40c50-182">To create multiple messages, make the parameter type for the output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in the following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="40c50-183">Cada mensaje de cola se crea inmediatamente cuando se llama al método **Add** .</span><span class="sxs-lookup"><span data-stu-id="40c50-183">Each queue message is created immediately when the **Add** method is called.</span></span>

### <a name="types-that-the-queue-attribute-works-with"></a><span data-ttu-id="40c50-184">Tipos con los que funciona el atributo Queue</span><span class="sxs-lookup"><span data-stu-id="40c50-184">Types that the Queue attribute works with</span></span>
<span data-ttu-id="40c50-185">Puede usar el atributo **Queue** en los siguientes tipos de parámetro:</span><span class="sxs-lookup"><span data-stu-id="40c50-185">You can use the **Queue** attribute on the following parameter types:</span></span>

* <span data-ttu-id="40c50-186">**out string** (crea un mensaje en cola si el valor de parámetro es no nulo cuando termina la función)</span><span class="sxs-lookup"><span data-stu-id="40c50-186">**out string** (creates queue message if parameter value is non-null when the function ends)</span></span>
* <span data-ttu-id="40c50-187">**out byte** (funciona como **cadena**)</span><span class="sxs-lookup"><span data-stu-id="40c50-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="40c50-188">**out CloudQueueMessage** (funciona como **cadena**)</span><span class="sxs-lookup"><span data-stu-id="40c50-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="40c50-189">**out POCO** (un tipo serializable, crea un mensaje con un objeto nulo si el parámetro es nulo cuando termina la función)</span><span class="sxs-lookup"><span data-stu-id="40c50-189">**out POCO** (a serializable type, creates a message with a null object if the paramter is null when the function ends)</span></span>
* <span data-ttu-id="40c50-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="40c50-190">**ICollector**</span></span>
* <span data-ttu-id="40c50-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="40c50-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="40c50-192">**CloudQueue** (para crear manualmente mensajes usando directamente la API de Almacenamiento de Azure)</span><span class="sxs-lookup"><span data-stu-id="40c50-192">**CloudQueue** (for creating messages manually using the Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-the-body-of-a-function"></a><span data-ttu-id="40c50-193">Utilizar atributos del SDK de WebJobs en el cuerpo de una función</span><span class="sxs-lookup"><span data-stu-id="40c50-193">Use WebJobs SDK attributes in the body of a function</span></span>
<span data-ttu-id="40c50-194">Si necesita realizar algún trabajo en la función antes de usar un atributo del SDK de WebJobs como **Queue**, **Blob** o **Table**, puede usar la interfaz **IBinder**.</span><span class="sxs-lookup"><span data-stu-id="40c50-194">If you need to do some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use the **IBinder** interface.</span></span>

<span data-ttu-id="40c50-195">En el siguiente ejemplo se toma un mensaje de la cola de entrada y se crea un mensaje nuevo con el mismo contenido en una cola de salida.</span><span class="sxs-lookup"><span data-stu-id="40c50-195">The following example takes an input queue message and creates a new message with the same content in an output queue.</span></span> <span data-ttu-id="40c50-196">El nombre de la cola de salida se establece por el código en el cuerpo de la función.</span><span class="sxs-lookup"><span data-stu-id="40c50-196">The output queue name is set by code in the body of the function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="40c50-197">La interfaz **IBinder** también puede usarse con los atributos **Table** y **Blob**.</span><span class="sxs-lookup"><span data-stu-id="40c50-197">The **IBinder** interface can also be used with the **Table** and **Blob** attributes.</span></span>

## <a name="how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="40c50-198">Lectura y escritura de blobs y tablas al procesar un mensaje de cola</span><span class="sxs-lookup"><span data-stu-id="40c50-198">How to read and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="40c50-199">Los atributos **Blob** y **Table** permiten leer y escribir los blobs y tablas.</span><span class="sxs-lookup"><span data-stu-id="40c50-199">The **Blob** and **Table** attributes enable you to read and write blobs and tables.</span></span> <span data-ttu-id="40c50-200">Los ejemplos en esta sección se aplican a los blobs.</span><span class="sxs-lookup"><span data-stu-id="40c50-200">The samples in this section apply to blobs.</span></span> <span data-ttu-id="40c50-201">Para ejemplos de código que muestran cómo desencadenar procesos cuando se crean o actualizan los blobs, consulte [Uso de Azure Blob Storage con el SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), y para obtener ejemplos de código que leen y escriben tablas, consulte [Cómo usar Azure Table Storage con el SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="40c50-201">For code samples that show how to trigger processes when blobs are created or updated, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How to use Azure table storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="40c50-202">Mensajes en cola de cadena que desencadenan operaciones de blob</span><span class="sxs-lookup"><span data-stu-id="40c50-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="40c50-203">Para un mensaje de cola que contiene una cadena, **queueTrigger** es un marcador de posición que se puede usar en el parámetro **blobPath** del atributo **Blob** que tiene el contenido del mensaje.</span><span class="sxs-lookup"><span data-stu-id="40c50-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in the **Blob** attribute's **blobPath** parameter that contains the contents of the message.</span></span>

<span data-ttu-id="40c50-204">El ejemplo siguiente usa objetos **Stream** para leer y escribir blobs.</span><span class="sxs-lookup"><span data-stu-id="40c50-204">The following example uses **Stream** objects to read and write blobs.</span></span> <span data-ttu-id="40c50-205">El mensaje en cola es el nombre de un blob ubicado en el contenedor textblobs.</span><span class="sxs-lookup"><span data-stu-id="40c50-205">The queue message is the name of a blob located in the textblobs container.</span></span> <span data-ttu-id="40c50-206">Se creará una copia del blob con "-new" anexado al nombre en el mismo contenedor.</span><span class="sxs-lookup"><span data-stu-id="40c50-206">A copy of the blob with "-new" appended to the name is created in the same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="40c50-207">El constructor de atributo **Blob** toma un parámetro **blobPath** que especifica el nombre del contenedor y el nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="40c50-207">The **Blob** attribute constructor takes a **blobPath** parameter that specifies the container and blob name.</span></span> <span data-ttu-id="40c50-208">Para más información acerca de este marcador de posición, consulte [Uso del almacenamiento de blobs de Azure con el SDK de WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="40c50-208">For more information about this placeholder, see [How to use Azure blob storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="40c50-209">Cuando el atributo representa a un objeto **Stream**, otro parámetro de constructor especifica el modo **FileAccess** como lectura, escritura o lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="40c50-209">When the attribute decorates a **Stream** object, another constructor parameter specifies the **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="40c50-210">En el ejemplo siguiente se usa un objeto **CloudBlockBlob** para eliminar un blob.</span><span class="sxs-lookup"><span data-stu-id="40c50-210">The following example uses a **CloudBlockBlob** object to delete a blob.</span></span> <span data-ttu-id="40c50-211">El mensaje en cola es el nombre del blob.</span><span class="sxs-lookup"><span data-stu-id="40c50-211">The queue message is the name of the blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="40c50-212">Mensajes en cola POCO [(objeto CRL estándar](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))</span><span class="sxs-lookup"><span data-stu-id="40c50-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="40c50-213">Para un objeto POCO almacenado como JSON en el mensaje de la cola, puede usar marcadores de posición que asignen nombre a propiedades del objeto en el parámetro **blobPath** del atributo **Queue**.</span><span class="sxs-lookup"><span data-stu-id="40c50-213">For a POCO stored as JSON in the queue message, you can use placeholders that name properties of the object in the **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="40c50-214">También puede utilizar nombres de propiedad de metadatos de cola como marcadores de posición.</span><span class="sxs-lookup"><span data-stu-id="40c50-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="40c50-215">Consulte [Obtener metadatos de cola o de mensaje en cola](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="40c50-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="40c50-216">El ejemplo siguiente copia un blob a un blob nuevo con una extensión distinta.</span><span class="sxs-lookup"><span data-stu-id="40c50-216">The following example copies a blob to a new blob with a different extension.</span></span> <span data-ttu-id="40c50-217">El mensaje de la cola es un objeto **BlobInformation** que incluye las propiedades **BlobName** y **BlobNameWithoutExtension**.</span><span class="sxs-lookup"><span data-stu-id="40c50-217">The queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="40c50-218">Los nombres de propiedad se usan como marcadores de posición en la ruta de acceso del blob para los atributos **Blob** .</span><span class="sxs-lookup"><span data-stu-id="40c50-218">The property names are used as placeholders in the blob path for the **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="40c50-219">El SDK usa el [paquete Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) para serializar y deserializar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="40c50-219">The SDK uses the [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) to serialize and deserialize messages.</span></span> <span data-ttu-id="40c50-220">Si crea mensajes en cola en un programa que no usa el SDK de WebJobs, puede escribir código similar al siguiente ejemplo para crear un mensaje en cola POCO que pueda analizar el SDK.</span><span class="sxs-lookup"><span data-stu-id="40c50-220">If you create queue messages in a program that doesn't use the WebJobs SDK, you can write code like the following example to create a POCO queue message that the SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="40c50-221">Si necesita realizar algún trabajo en la función antes de enlazar un blob a un objeto, puede usar el atributo en el cuerpo de la función, como se ha mostrado en [Utilizar atributos del SDK de WebJobs en el cuerpo de una función](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="40c50-221">If you need to do some work in your function before binding a blob to an object, you can use the attribute in the body of the function, as shown in [Use WebJobs SDK attributes in the body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-the-blob-attribute-with"></a><span data-ttu-id="40c50-222">Tipos con los que puede usar el atributo Blob</span><span class="sxs-lookup"><span data-stu-id="40c50-222">Types you can use the Blob attribute with</span></span>
<span data-ttu-id="40c50-223">El atributo **Blob** se puede usar con los siguientes tipos:</span><span class="sxs-lookup"><span data-stu-id="40c50-223">The **Blob** attribute can be used with the following types:</span></span>

* <span data-ttu-id="40c50-224">**Stream** (lectura o escritura, especificado según el uso del parámetro del constructor FileAccess)</span><span class="sxs-lookup"><span data-stu-id="40c50-224">**Stream** (read or write, specified by using the FileAccess constructor parameter)</span></span>
* <span data-ttu-id="40c50-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="40c50-225">**TextReader**</span></span>
* <span data-ttu-id="40c50-226">**TextWriter**</span><span class="sxs-lookup"><span data-stu-id="40c50-226">**TextWriter**</span></span>
* <span data-ttu-id="40c50-227">**string** (lectura)</span><span class="sxs-lookup"><span data-stu-id="40c50-227">**string** (read)</span></span>
* <span data-ttu-id="40c50-228">**out string** (escritura; crea un blob solo si el parámetro de cadena es no nulo cuando se devuelve la función)</span><span class="sxs-lookup"><span data-stu-id="40c50-228">**out string** (write; creates a blob only if the string parameter is non-null when the function returns)</span></span>
* <span data-ttu-id="40c50-229">POCO (lectura)</span><span class="sxs-lookup"><span data-stu-id="40c50-229">POCO (read)</span></span>
* <span data-ttu-id="40c50-230">out POCO (escritura; siempre crea un blob, crea como objeto nulo si el parámetro POCO es nulo cuando se devuelve la función)</span><span class="sxs-lookup"><span data-stu-id="40c50-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when the function returns)</span></span>
* <span data-ttu-id="40c50-231">**CloudBlobStream** (escritura)</span><span class="sxs-lookup"><span data-stu-id="40c50-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="40c50-232">**ICloudBlob** (lectura o escritura)</span><span class="sxs-lookup"><span data-stu-id="40c50-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="40c50-233">**CloudBlockBlob** (lectura o escritura)</span><span class="sxs-lookup"><span data-stu-id="40c50-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="40c50-234">**CloudPageBlob** (lectura o escritura)</span><span class="sxs-lookup"><span data-stu-id="40c50-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-to-handle-poison-messages"></a><span data-ttu-id="40c50-235">Control de mensajes dudosos</span><span class="sxs-lookup"><span data-stu-id="40c50-235">How to handle poison messages</span></span>
<span data-ttu-id="40c50-236">Los mensajes cuyo contenido produce un error de una función se denominan *mensajes dudosos*.</span><span class="sxs-lookup"><span data-stu-id="40c50-236">Messages whose content causes a function to fail are called *poison messages*.</span></span> <span data-ttu-id="40c50-237">Cuando se produce un error en la función, el mensaje de la cola no se elimina y se recoge de nuevo, provocando que el ciclo se repita.</span><span class="sxs-lookup"><span data-stu-id="40c50-237">When the function fails, the queue message is not deleted and eventually is picked up again, causing the cycle to be repeated.</span></span> <span data-ttu-id="40c50-238">El SDK puede interrumpir automáticamente el ciclo después de un número limitado de iteraciones, o puede hacerlo usted manualmente.</span><span class="sxs-lookup"><span data-stu-id="40c50-238">The SDK can automatically interrupt the cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="40c50-239">Control automático de mensajes dudosos</span><span class="sxs-lookup"><span data-stu-id="40c50-239">Automatic poison message handling</span></span>
<span data-ttu-id="40c50-240">El SDK llamará a una función hasta 5 veces para procesar un mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="40c50-240">The SDK will call a function up to 5 times to process a queue message.</span></span> <span data-ttu-id="40c50-241">Si se produce un error en el quinta intento, el mensaje se mueve a una cola de mensajes dudosos.</span><span class="sxs-lookup"><span data-stu-id="40c50-241">If the fifth try fails, the message is moved to a poison queue.</span></span> <span data-ttu-id="40c50-242">Puede ver cómo configurar el número máximo de reintentos en [Establecimiento de opciones de configuración](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="40c50-242">You can see how to configure the maximum number of retries in [How to set configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="40c50-243">La cola de mensajes dudosos se denomina *{originalqueuename}*-poison.</span><span class="sxs-lookup"><span data-stu-id="40c50-243">The poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="40c50-244">Puede escribir una función para procesar los mensajes desde la cola de mensajes dudosos registrándolos o enviando una notificación indicando que se necesita atención manual.</span><span class="sxs-lookup"><span data-stu-id="40c50-244">You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="40c50-245">En el siguiente ejemplo la función **CopyBlob** generará un error cuando un mensaje de cola contenga el nombre de un blob que no existe.</span><span class="sxs-lookup"><span data-stu-id="40c50-245">In the following example the **CopyBlob** function will fail when a queue message contains the name of a blob that doesn't exist.</span></span> <span data-ttu-id="40c50-246">Cuando esto ocurre, el mensaje se mueve desde la cola de copyblobqueue a la cola copyblobqueue-poison.</span><span class="sxs-lookup"><span data-stu-id="40c50-246">When that happens, the message is moved from the copyblobqueue queue to the copyblobqueue-poison queue.</span></span> <span data-ttu-id="40c50-247">Después, **ProcessPoisonMessage** registra el mensaje dudoso.</span><span class="sxs-lookup"><span data-stu-id="40c50-247">The **ProcessPoisonMessage** then logs the poison message.</span></span>

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
            logger.WriteLine("Failed to copy blob, name=" + blobName);
        }

<span data-ttu-id="40c50-248">La ilustración siguiente muestra la salida de consola de estas funciones cuando se procesa un mensaje dudoso.</span><span class="sxs-lookup"><span data-stu-id="40c50-248">The following illustration shows console output from these functions when a poison message is processed.</span></span>

![Salida de consola para el control de mensajes dudosos](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="40c50-250">Control manual de mensajes dudosos</span><span class="sxs-lookup"><span data-stu-id="40c50-250">Manual poison message handling</span></span>
<span data-ttu-id="40c50-251">Puede obtener el número de veces que se ha recogido un mensaje para el procesamiento agregando un parámetro **int** llamado **dequeueCount** a la función.</span><span class="sxs-lookup"><span data-stu-id="40c50-251">You can get the number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** to your function.</span></span> <span data-ttu-id="40c50-252">Puede consultar el recuento de eliminación de cola en el código de función y realizar su propio control de mensajes dudosos cuando el número supere un umbral, tal y como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="40c50-252">You can then check the dequeue count in function code and perform your own poison message handling when the number exceeds a threshold, as shown in the following example.</span></span>

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed to copy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-to-set-configuration-options"></a><span data-ttu-id="40c50-253">Establecimiento de opciones de configuración</span><span class="sxs-lookup"><span data-stu-id="40c50-253">How to set configuration options</span></span>
<span data-ttu-id="40c50-254">Puede usar el tipo **JobHostConfiguration** para establecer las opciones de configuración siguientes:</span><span class="sxs-lookup"><span data-stu-id="40c50-254">You can use the **JobHostConfiguration** type to set the following configuration options:</span></span>

* <span data-ttu-id="40c50-255">Establecer las cadenas de conexión de SDK en el código.</span><span class="sxs-lookup"><span data-stu-id="40c50-255">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="40c50-256">Definir la configuración **QueueTrigger** como el número máximo de eliminaciones de la cola.</span><span class="sxs-lookup"><span data-stu-id="40c50-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="40c50-257">Obtener nombres de cola a partir de la configuración.</span><span class="sxs-lookup"><span data-stu-id="40c50-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="40c50-258">Establecimiento de cadenas de conexión del SDK en código</span><span class="sxs-lookup"><span data-stu-id="40c50-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="40c50-259">Configurar las cadenas de conexión de SDK en el código permite utilizar sus propios nombres de cadena de conexión en archivos de configuración o las variables de entorno, como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="40c50-259">Setting the SDK connection strings in code enables you to use your own connection string names in configuration files or environment variables, as shown in the following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="40c50-260">Configurar QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="40c50-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="40c50-261">Puede configurar los siguientes valores, que se aplican para el procesamiento de mensajes de la cola:</span><span class="sxs-lookup"><span data-stu-id="40c50-261">You can configure the following settings that apply to the queue message processing:</span></span>

* <span data-ttu-id="40c50-262">El número máximo de mensajes en cola que se recogen simultáneamente para ejecutarse en paralelo (el valor predeterminado es 16).</span><span class="sxs-lookup"><span data-stu-id="40c50-262">The maximum number of queue messages that are picked up simultaneously to be executed in parallel (default is 16).</span></span>
* <span data-ttu-id="40c50-263">El número máximo de reintentos antes de enviar un mensaje de la cola a una cola de mensajes dudosos (el valor predeterminado es 5).</span><span class="sxs-lookup"><span data-stu-id="40c50-263">The maximum number of retries before a queue message is sent to a poison queue (default is 5).</span></span>
* <span data-ttu-id="40c50-264">El tiempo de espera máximo antes de volver a sondear cuando una cola está vacía (el valor predeterminado es 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="40c50-264">The maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="40c50-265">En el ejemplo siguiente se muestra cómo configurar estas opciones:</span><span class="sxs-lookup"><span data-stu-id="40c50-265">The following example shows how to configure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="40c50-266">Establecer valores para los parámetros del constructor del SDK de WebJobs en el código</span><span class="sxs-lookup"><span data-stu-id="40c50-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="40c50-267">En ocasiones, deseará especificar un nombre de cola, un contenedor o nombre de blob o un nombre de cola en el código en lugar de codificarlo.</span><span class="sxs-lookup"><span data-stu-id="40c50-267">Sometimes you want to specify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="40c50-268">Por ejemplo, es posible que desee especificar el nombre de la cola para **QueueTrigger** en un archivo de configuración o una variable de entorno.</span><span class="sxs-lookup"><span data-stu-id="40c50-268">For example, you might want to specify the queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="40c50-269">Puede hacerlo pasando un objeto **NameResolver** para el tipo **JobHostConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="40c50-269">You can do that by passing in a **NameResolver** object to the **JobHostConfiguration** type.</span></span> <span data-ttu-id="40c50-270">Incluya marcadores de posición especiales rodeados de signos de porcentaje (%) en los parámetros del constructor de atributos del SDK de WebJobs y el código **NameResolver** especifica los valores reales que se usarán en lugar de esos marcadores de posición.</span><span class="sxs-lookup"><span data-stu-id="40c50-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies the actual values to be used in place of those placeholders.</span></span>

<span data-ttu-id="40c50-271">Por ejemplo, suponga que desea usar una cola denominada logqueuetest en el entorno de prueba y un logqueueprod denominado en producción.</span><span class="sxs-lookup"><span data-stu-id="40c50-271">For example, suppose you want to use a queue named logqueuetest in the test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="40c50-272">En lugar de un nombre de cola codificado de forma rígida, desea especificar el nombre de una entrada en la colección **appSettings** que tendría el nombre de cola real.</span><span class="sxs-lookup"><span data-stu-id="40c50-272">Instead of a hard-coded queue name, you want to specify the name of an entry in the **appSettings** collection that would have the actual queue name.</span></span> <span data-ttu-id="40c50-273">Si la clave **appSettings** es logqueue, la función podría ser similar al ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="40c50-273">If the **appSettings** key is logqueue, your function could look like the following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="40c50-274">La clase **NameResolver** podría entonces obtener el nombre de la cola de **appSettings** como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="40c50-274">Your **NameResolver** class could then get the queue name from **appSettings** as shown in the following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="40c50-275">Pasa la clase **NameResolver** en el objeto **JobHost** tal y como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="40c50-275">You pass the **NameResolver** class in to the **JobHost** object as shown in the following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="40c50-276">**Nota** : los nombres de cola, tabla y blob se resuelven cada vez que se llama a una función, pero los nombres de contenedores de blobs solo se resuelven cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="40c50-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when the application starts.</span></span> <span data-ttu-id="40c50-277">No puede cambiar el nombre del contenedor de blobs mientras el trabajo está en ejecución.</span><span class="sxs-lookup"><span data-stu-id="40c50-277">You can't change blob container name while the job is running.</span></span>

## <a name="how-to-trigger-a-function-manually"></a><span data-ttu-id="40c50-278">Desencadenar una función manualmente</span><span class="sxs-lookup"><span data-stu-id="40c50-278">How to trigger a function manually</span></span>
<span data-ttu-id="40c50-279">Para desencadenar una función manualmente, use el método **Call** o **CallAsync** en el objeto **JobHost** y el atributo **NoAutomaticTrigger** en la función, tal y como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="40c50-279">To trigger a function manually, use the **Call** or **CallAsync** method on the **JobHost** object and the **NoAutomaticTrigger** attribute on the function, as shown in the following example.</span></span>

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

## <a name="how-to-write-logs"></a><span data-ttu-id="40c50-280">Escritura de registros</span><span class="sxs-lookup"><span data-stu-id="40c50-280">How to write logs</span></span>
<span data-ttu-id="40c50-281">El Panel muestra registros en dos lugares: la página del trabajo web y la página de una invocación de trabajo web en especial.</span><span class="sxs-lookup"><span data-stu-id="40c50-281">The Dashboard shows logs in two places: the page for the WebJob, and the page for a particular WebJob invocation.</span></span>

![Registros en la página del trabajo web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Registros en la página de invocación de la función](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="40c50-284">El resultado de los métodos de consola que llama en una función o en el método **Main()** aparece en la página Panel del WebJob y no en la página de una invocación de método en especial.</span><span class="sxs-lookup"><span data-stu-id="40c50-284">Output from Console methods that you call in a function or in the **Main()** method appears in the Dashboard page for the WebJob, not in the page for a particular method invocation.</span></span> <span data-ttu-id="40c50-285">El resultado del objeto TextWriter que obtiene a partir de un parámetro en la firma del método aparece en la página Panel de una invocación de un método.</span><span class="sxs-lookup"><span data-stu-id="40c50-285">Output from the TextWriter object that you get from a parameter in your method signature appears in the Dashboard page for a method invocation.</span></span>

<span data-ttu-id="40c50-286">El resultado de la consola no se puede vincular a una invocación de método en especial, porque la consola tiene un solo subproceso, mientras que muchas funciones de trabajo se pueden ejecutar al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="40c50-286">Console output can't be linked to a particular method invocation because the Console is single-threaded, while many job functions may be running at the same time.</span></span> <span data-ttu-id="40c50-287">Esta es la razón por la que el SDK proporciona a cada invocación de función su objeto escritor de registros único.</span><span class="sxs-lookup"><span data-stu-id="40c50-287">That's why the  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="40c50-288">Para escribir [registros de seguimiento de aplicación](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (crea registros marcados como INFO) y **Console.Error** (crea registros marcados como ERROR).</span><span class="sxs-lookup"><span data-stu-id="40c50-288">To write [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="40c50-289">Una alternativa es usar [Trace o TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), que proporciona niveles de Modo detallado, Advertencia y Críticos, además de Info y Error.</span><span class="sxs-lookup"><span data-stu-id="40c50-289">An alternative is to use [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition to Info and Error.</span></span> <span data-ttu-id="40c50-290">Los registros de seguimiento de aplicaciones aparecen en los archivos de registro de la aplicación web, tablas de Azure o blobs de Azure, dependiendo de cómo se configuró la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="40c50-290">Application tracing logs appear in the web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="40c50-291">Como ocurre en todos los resultados de la consola, los 100 registros de aplicación más recientes también aparecen en la página Panel para el trabajo web, no en la página para una innovación de función.</span><span class="sxs-lookup"><span data-stu-id="40c50-291">As is true of all Console output, the most recent 100 application logs also appear in the Dashboard page for the WebJob, not the page for a function invocation.</span></span>

<span data-ttu-id="40c50-292">El resultado de la consola aparece en el Panel solo si el programa se ejecuta en un Azure WebJob, no si el programa se ejecuta localmente o en algún otro entorno.</span><span class="sxs-lookup"><span data-stu-id="40c50-292">Console output appears in the Dashboard only if the program is running in an Azure WebJob, not if the program is running locally or in some other environment.</span></span>

<span data-ttu-id="40c50-293">Para deshabilitar el registro estableciendo la cadena de conexión del panel en null.</span><span class="sxs-lookup"><span data-stu-id="40c50-293">You can disable logging by setting the Dashboard connection string to null.</span></span> <span data-ttu-id="40c50-294">Para más información, consulte [Establecimiento de opciones de configuración](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="40c50-294">For more information, see [How to set Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="40c50-295">En el ejemplo siguiente se muestran varias maneras de escribir registros:</span><span class="sxs-lookup"><span data-stu-id="40c50-295">The following example shows several ways to write logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="40c50-296">En el panel del SDK de WebJobs, la salida del objeto **TextWriter** aparece cuando va a la página para una invocación de función determinada y selecciona **Alternar salida**:</span><span class="sxs-lookup"><span data-stu-id="40c50-296">In the WebJobs SDK Dashboard, the output from the **TextWriter** object shows up when you go to the page for a particular function invocation and select **Toggle Output**:</span></span>

![Vínculo de invocación](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Registros en la página de invocación de la función](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="40c50-299">En el panel del SDK de WebJobs, las 100 líneas más recientes de los resultados de la consola aparecen cuando va a la página de WebJob (no de la invocación de función) y selecciona **Toggle Output**(Alternar salida).</span><span class="sxs-lookup"><span data-stu-id="40c50-299">In the WebJobs SDK Dashboard, the most recent 100 lines of Console output show up when you go to the page for the WebJob (not for the function invocation) and select **Toggle Output**.</span></span>

![Toggle Output](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="40c50-301">En un WebJob continuo, los registros de aplicación aparecen en /data/jobs/continuous/*{nombrewebjob}*/job_log.txt en el sistema de archivos de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="40c50-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in the web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="40c50-302">En un blob de Azure  el aspecto de los registros de aplicación es similar al siguiente: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span><span class="sxs-lookup"><span data-stu-id="40c50-302">In an Azure blob the application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="40c50-303">Y en una tabla de Azure, los registros **Console.Out** y **Console.Error** tienen el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="40c50-303">And in an Azure table the **Console.Out** and **Console.Error** logs look like this:</span></span>

![Registro de información en la tabla](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Registro de errores en la tabla](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="40c50-306">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="40c50-306">Next steps</span></span>
<span data-ttu-id="40c50-307">En este artículo se han proporcionado ejemplos de código que muestran cómo tratar escenarios comunes para trabajar con colas de Azure.</span><span class="sxs-lookup"><span data-stu-id="40c50-307">This article has provided code samples that show how to handle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="40c50-308">Para más información acerca de cómo usar el SDK de WebJobs y WebJobs de Azure, consulte [Recursos de documentación de WebJobs de Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="40c50-308">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

