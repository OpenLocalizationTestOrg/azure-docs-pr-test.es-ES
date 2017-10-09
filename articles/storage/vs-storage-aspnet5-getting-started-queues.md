---
title: aaaGet a trabajar con Visual Studio y el almacenamiento de cola servicios conectados (ASP.NET Core) | Documentos de Microsoft
description: "Cómo tooget iniciado mediante el almacenamiento de cola de Azure en un proyecto de ASP.NET Core en Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 75adb7163827ab17ad89707051ff0e48dbae9c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="a1937-103">Introducción a Queue Storage y a los servicios conectados de Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="a1937-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="a1937-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a1937-104">Overview</span></span>
<span data-ttu-id="a1937-105">Este artículo describe cómo tooget iniciado mediante el almacenamiento de cola de Azure en Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure en un proyecto de ASP.NET Core mediante Visual Studio hello **agregar servicios conectados** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a1937-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="a1937-106">Hola **agregar servicios conectados** operación instala tooaccess de paquetes de NuGet adecuado de hello almacenamiento de Azure en el proyecto y agrega la cadena de conexión de Hola para hello cuenta de almacenamiento tooyour archivos de configuración de proyecto.</span><span class="sxs-lookup"><span data-stu-id="a1937-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="a1937-107">Almacenamiento de cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a1937-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="a1937-108">Un mensaje de la cola solo puede estar too64 kilobytes (KB) de tamaño y una cola puede contener millones de mensajes, seguridad toohello límite de capacidad total de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a1937-108">A single queue message can be up too64 kilobytes (KB) in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

<span data-ttu-id="a1937-109">tooget iniciado, primero debe toocreate una cola de Azure en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a1937-109">tooget started, you first need toocreate an Azure queue in your storage account.</span></span> <span data-ttu-id="a1937-110">Le mostraremos cómo toocreate una cola en el código.</span><span class="sxs-lookup"><span data-stu-id="a1937-110">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="a1937-111">También le mostraremos cómo tooperform basic cola operaciones, como agregar, modificar, leer y eliminar mensajes de la cola.</span><span class="sxs-lookup"><span data-stu-id="a1937-111">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="a1937-112">Hola ejemplos están escritos en C\# código y utilizar Hola biblioteca de cliente de almacenamiento de Azure para. NET.</span><span class="sxs-lookup"><span data-stu-id="a1937-112">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="a1937-113">Para obtener más información acerca de ASP.NET, consulte [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="a1937-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="a1937-114">**Nota:** algunas de las API que realizan llamadas tooAzure almacenamiento en ASP.NET Core Hola son asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="a1937-114">**NOTE:** Some of hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="a1937-115">Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="a1937-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="a1937-116">código de Hello siguiente se da por supuesto que se usan métodos de programación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="a1937-116">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="a1937-117">Consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](storage-dotnet-how-to-use-queues.md) para más información sobre la manipulación de colas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="a1937-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="a1937-118">Vea [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/) para información general sobre Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1937-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="a1937-119">Vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/) para información general sobre los servicios en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1937-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="a1937-120">Vea [ASP.NET](http://www.asp.net) para más información sobre la programación de aplicaciones ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a1937-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="a1937-121">Acceso a colas en el código</span><span class="sxs-lookup"><span data-stu-id="a1937-121">Access queues in code</span></span>
<span data-ttu-id="a1937-122">colas de tooaccess de proyectos de ASP.NET Core, necesita tooinclude Hola siguiente archivo de código fuente de tooany C# de elementos que tiene acceso a almacenamiento de cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="a1937-122">tooaccess queues in ASP.NET Core projects, you need tooinclude hello following items tooany C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="a1937-123">Asegúrese de incluyen declaraciones de espacios de nombres de hello en parte superior de hello del archivo hello C# estas **con** instrucciones.</span><span class="sxs-lookup"><span data-stu-id="a1937-123">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="a1937-124">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a1937-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="a1937-125">Hola de uso después de código tooget Hola su cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de información de configuración del servicio de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="a1937-125">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="a1937-126">Obtener un **CloudQueueClient** tooreference Hola cola objetos en su cuenta de almacenamiento de objetos.</span><span class="sxs-lookup"><span data-stu-id="a1937-126">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="a1937-127">Obtener un **CloudQueue** tooreference una cola específica del objeto.</span><span class="sxs-lookup"><span data-stu-id="a1937-127">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="a1937-128">**Nota:** los Hola encima código frente a código de hello usan en hello siguiendo los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="a1937-128">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="a1937-129">Creación de una cola en código</span><span class="sxs-lookup"><span data-stu-id="a1937-129">Create a queue in code</span></span>
<span data-ttu-id="a1937-130">Hola toocreate cola de Azure en el código, basta con agregar una llamada demasiado**CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="a1937-130">toocreate hello Azure queue in code, just add a call too**CreateIfNotExistsAsync**.</span></span>

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="a1937-131">Agregar una cola de mensajes tooa</span><span class="sxs-lookup"><span data-stu-id="a1937-131">Add a message tooa queue</span></span>
<span data-ttu-id="a1937-132">tooinsert un mensaje en una cola existente, cree un nuevo **CloudQueueMessage** objeto y, a continuación, llamada hello **AddMessageAsync** método.</span><span class="sxs-lookup"><span data-stu-id="a1937-132">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessageAsync** method.</span></span>

<span data-ttu-id="a1937-133">Se puede crear un objeto **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="a1937-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="a1937-134">Este es un ejemplo que inserta el mensaje de saludo "¡Hello, World".</span><span class="sxs-lookup"><span data-stu-id="a1937-134">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="a1937-135">Leer un mensaje de una cola</span><span class="sxs-lookup"><span data-stu-id="a1937-135">Read a message in a queue</span></span>
<span data-ttu-id="a1937-136">Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **PeekMessageAsync** método.</span><span class="sxs-lookup"><span data-stu-id="a1937-136">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessageAsync** method.</span></span>

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="a1937-137">Leer y eliminar un mensaje de una cola</span><span class="sxs-lookup"><span data-stu-id="a1937-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="a1937-138">Su código puede quitar un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="a1937-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="a1937-139">Llame a **GetMessageAsync** siguiente mensaje de saludo de tooget en una cola.</span><span class="sxs-lookup"><span data-stu-id="a1937-139">Call **GetMessageAsync** tooget hello next message in a queue.</span></span> <span data-ttu-id="a1937-140">Un mensaje devuelto de **GetMessageAsync** se convierte en invisible tooany otro código que lee mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="a1937-140">A message returned from **GetMessageAsync** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="a1937-141">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="a1937-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="a1937-142">toofinish quitar mensajes de bienvenida de cola de hello, llame a **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="a1937-142">toofinish removing hello message from hello queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="a1937-143">Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="a1937-143">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="a1937-144">Hola siguiente código llama **DeleteMessageAsync** justo después de que se ha procesado el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="a1937-144">hello following code calls **DeleteMessageAsync** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="a1937-145">las opciones adicionales de los mensajes quitados de la cola</span><span class="sxs-lookup"><span data-stu-id="a1937-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="a1937-146">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="a1937-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="a1937-147">En primer lugar, puede obtener un lote de mensajes (arriba too32).</span><span class="sxs-lookup"><span data-stu-id="a1937-147">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="a1937-148">En segundo lugar, puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="a1937-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="a1937-149">siguiente Hola código de ejemplo utiliza la **GetMessages** tooget 20 mensajes de método en una llamada.</span><span class="sxs-lookup"><span data-stu-id="a1937-149">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="a1937-150">A continuación, procesa cada mensaje con un bucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="a1937-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="a1937-151">También establece los minutos de too5 de tiempo de espera de invisibilidad de Hola para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="a1937-151">It also sets hello invisibility timeout too5 minutes for each message.</span></span> <span data-ttu-id="a1937-152">Tenga en cuenta que inicio de 5 minutos de Hola para todos los mensajes en hello mismo tiempo, por lo que tras 5 minutos transcurridos tras la llamada de hello demasiado**GetMessages**, los mensajes que no se eliminaron vuelven a ser visibles.</span><span class="sxs-lookup"><span data-stu-id="a1937-152">Note that hello 5 minutes start for all messages at hello same time, so after 5 minutes have passed after hello call too**GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="a1937-153">Obtener la longitud de cola de Hola</span><span class="sxs-lookup"><span data-stu-id="a1937-153">Get hello queue length</span></span>
<span data-ttu-id="a1937-154">Puede obtener una estimación del número de Hola de mensajes en una cola.</span><span class="sxs-lookup"><span data-stu-id="a1937-154">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="a1937-155">El **FetchAttributes** método pide al servicio de cola de Hola para recuperar los atributos de la cola de hello, incluido el número de mensajes de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1937-155">The **FetchAttributes** method asks hello queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="a1937-156">Hola **ApproximateMethodCount** propiedad devuelve el valor última de hello recuperado por la **FetchAttributes** método sin llamar al servicio de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1937-156">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="a1937-157">Usar el patrón de hello asincrónicas Await con las API de cola común</span><span class="sxs-lookup"><span data-stu-id="a1937-157">Use hello Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="a1937-158">Este ejemplo muestra cómo toouse Hola asincrónicas Await patrón con las API de cola común.</span><span class="sxs-lookup"><span data-stu-id="a1937-158">This example shows how toouse hello Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="a1937-159">versión de async de Hola Hola ejemplo llamadas de cada uno de hello tiene métodos.</span><span class="sxs-lookup"><span data-stu-id="a1937-159">hello sample calls hello async version of each of hello given methods.</span></span> <span data-ttu-id="a1937-160">Esto puede verse por revisión posterior a la de hello asincrónico de cada método.</span><span class="sxs-lookup"><span data-stu-id="a1937-160">This can be seen by hello Async post-fix of each method.</span></span> <span data-ttu-id="a1937-161">Cuando se utiliza un método asincrónico, el patrón de Async y Await Hola suspende la ejecución local hasta que se complete la llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1937-161">When an async method is used, hello Async-Await pattern suspends local execution until hello call is completed.</span></span> <span data-ttu-id="a1937-162">Este comportamiento permite Hola actual subproceso toodo otro trabajo que ayuda a evitar los cuellos de botella de rendimiento y aumenta la capacidad de respuesta general de la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a1937-162">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="a1937-163">Para obtener más detalles sobre el uso de hello patrón Async y Await en. NET, consulte [Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="a1937-163">For more details on using hello Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="a1937-164">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="a1937-164">Delete a queue</span></span>
<span data-ttu-id="a1937-165">toodelete una cola y todos los mensajes de Hola contenidas en ella, llame a la **eliminar** método hello en objetos de cola.</span><span class="sxs-lookup"><span data-stu-id="a1937-165">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="a1937-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1937-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

