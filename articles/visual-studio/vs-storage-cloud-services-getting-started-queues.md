---
title: aaaGet a trabajar con Visual Studio y el almacenamiento de cola servicios conectados (servicios en la nube) | Documentos de Microsoft
description: "Cómo tooget iniciado mediante el almacenamiento de cola de Azure en un proyecto de servicio de nube en Visual Studio después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 1e90eeb826131cadca90dcb720c931fff5fedcb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="0e8af-103">Introducción al almacenamiento de colas de Azure y a los servicios conectados de Visual Studio (proyectos de servicios en la nube)</span><span class="sxs-lookup"><span data-stu-id="0e8af-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="0e8af-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0e8af-104">Overview</span></span>
<span data-ttu-id="0e8af-105">Este artículo describe cómo tooget iniciado mediante el almacenamiento de cola de Azure en Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure en un proyecto de servicios de nube mediante Visual Studio hello **agregar servicios conectados** cuadro de diálogo .</span><span class="sxs-lookup"><span data-stu-id="0e8af-105">This article describes how tooget started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="0e8af-106">Le mostraremos cómo toocreate una cola en el código.</span><span class="sxs-lookup"><span data-stu-id="0e8af-106">We'll show you how toocreate a queue in code.</span></span> <span data-ttu-id="0e8af-107">También le mostraremos cómo tooperform basic cola operaciones, como agregar, modificar, leer y eliminar mensajes de la cola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-107">We'll also show you how tooperform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="0e8af-108">ejemplos de Hello están escritos en código C# y usar hello [biblioteca de cliente de almacenamiento de Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e8af-108">hello samples are written in C# code and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="0e8af-109">Hola **agregar servicios conectados** operación instala tooaccess de paquetes de NuGet adecuado de hello almacenamiento de Azure en el proyecto y agrega la cadena de conexión de Hola para hello cuenta de almacenamiento tooyour archivos de configuración de proyecto.</span><span class="sxs-lookup"><span data-stu-id="0e8af-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

* <span data-ttu-id="0e8af-110">Consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) para más información sobre la manipulación de colas en el código.</span><span class="sxs-lookup"><span data-stu-id="0e8af-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="0e8af-111">Vea [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/) para información general sobre Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8af-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="0e8af-112">Vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/) para información general sobre los servicios en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8af-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="0e8af-113">Vea [ASP.NET](http://www.asp.net) para más información sobre la programación de aplicaciones ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="0e8af-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="0e8af-114">Almacenamiento de la cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0e8af-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="0e8af-115">Un mensaje de la cola solo puede estar too64 KB de tamaño y una cola puede contener millones de mensajes, seguridad toohello límite de capacidad total de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0e8af-115">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="0e8af-116">Acceso a colas en el código</span><span class="sxs-lookup"><span data-stu-id="0e8af-116">Access queues in code</span></span>
<span data-ttu-id="0e8af-117">las colas de tooaccess en los proyectos de servicios de nube de Visual Studio, necesita tooinclude Hola siguiente archivo de código fuente de tooany C# de elementos que tienen acceso a almacenamiento de la cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8af-117">tooaccess queues in Visual Studio Cloud Services projects, you need tooinclude hello following items tooany C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="0e8af-118">Asegúrese de incluyen declaraciones de espacios de nombres de hello en parte superior de hello del archivo hello C# estas **con** instrucciones.</span><span class="sxs-lookup"><span data-stu-id="0e8af-118">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="0e8af-119">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0e8af-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="0e8af-120">Hola de uso después de código tooget Hola su cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de información de configuración del servicio de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-120">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="0e8af-121">Obtener un **CloudQueueClient** tooreference Hola cola objetos en su cuenta de almacenamiento de objetos.</span><span class="sxs-lookup"><span data-stu-id="0e8af-121">Get a **CloudQueueClient** object tooreference hello queue objects in your storage account.</span></span>  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="0e8af-122">Obtener un **CloudQueue** tooreference una cola específica del objeto.</span><span class="sxs-lookup"><span data-stu-id="0e8af-122">Get a **CloudQueue** object tooreference a specific queue.</span></span>
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="0e8af-123">**Nota:** los Hola encima código frente a código de hello usan en hello siguiendo los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="0e8af-123">**NOTE:** Use all of hello above code in front of hello code in hello following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="0e8af-124">Creación de una cola en código</span><span class="sxs-lookup"><span data-stu-id="0e8af-124">Create a queue in code</span></span>
<span data-ttu-id="0e8af-125">cola de hello toocreate desde el código, basta con agregar una llamada demasiado**CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="0e8af-125">toocreate hello queue in code, just add a call too**CreateIfNotExists**.</span></span>

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="0e8af-126">Agregar una cola de mensajes tooa</span><span class="sxs-lookup"><span data-stu-id="0e8af-126">Add a message tooa queue</span></span>
<span data-ttu-id="0e8af-127">tooinsert un mensaje en una cola existente, cree un nuevo **CloudQueueMessage** objeto y, a continuación, llamada hello **AddMessage** método.</span><span class="sxs-lookup"><span data-stu-id="0e8af-127">tooinsert a message into an existing queue, create a new **CloudQueueMessage** object, then call hello **AddMessage** method.</span></span>

<span data-ttu-id="0e8af-128">Se puede crear un objeto **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="0e8af-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="0e8af-129">Este es un ejemplo que inserta el mensaje de saludo "¡Hello, World".</span><span class="sxs-lookup"><span data-stu-id="0e8af-129">Here is an example which inserts hello message 'Hello, World'.</span></span>

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="0e8af-130">Leer un mensaje de una cola</span><span class="sxs-lookup"><span data-stu-id="0e8af-130">Read a message in a queue</span></span>
<span data-ttu-id="0e8af-131">Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **PeekMessage** método.</span><span class="sxs-lookup"><span data-stu-id="0e8af-131">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="0e8af-132">Leer y eliminar un mensaje de una cola</span><span class="sxs-lookup"><span data-stu-id="0e8af-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="0e8af-133">Su código puede quitar un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="0e8af-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="0e8af-134">Llame a **GetMessage** siguiente mensaje de saludo de tooget en una cola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-134">Call **GetMessage** tooget hello next message in a queue.</span></span> <span data-ttu-id="0e8af-135">Un mensaje devuelto de **GetMessage** se convierte en invisible tooany otro código que lee mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-135">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="0e8af-136">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="0e8af-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="0e8af-137">toofinish quitar mensajes de bienvenida de cola de hello, llame a **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="0e8af-137">toofinish removing hello message from hello queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="0e8af-138">Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="0e8af-138">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="0e8af-139">Hola siguiente código llama **DeleteMessage** justo después de que se ha procesado el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="0e8af-139">hello following code calls **DeleteMessage** right after hello message has been processed.</span></span>

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a><span data-ttu-id="0e8af-140">Use opciones adicionales tooprocess y quitar mensajes en cola</span><span class="sxs-lookup"><span data-stu-id="0e8af-140">Use additional options tooprocess and remove queue messages</span></span>
<span data-ttu-id="0e8af-141">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="0e8af-142">Puede obtener un lote de mensajes (arriba too32).</span><span class="sxs-lookup"><span data-stu-id="0e8af-142">You can get a batch of messages (up too32).</span></span>
* <span data-ttu-id="0e8af-143">Puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="0e8af-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="0e8af-144">siguiente Hola código de ejemplo utiliza la **GetMessages** tooget 20 mensajes de método en una llamada.</span><span class="sxs-lookup"><span data-stu-id="0e8af-144">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="0e8af-145">A continuación, procesa cada mensaje con un bucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="0e8af-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="0e8af-146">También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="0e8af-146">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="0e8af-147">Tenga en cuenta que Hola 5 minutos se inicia para todos los mensajes en hello mismo tiempo, por lo que tras 5 minutos transcurridos desde la llamada de hello demasiado**GetMessages**, los mensajes que no se eliminaron estará visibles de nuevo.</span><span class="sxs-lookup"><span data-stu-id="0e8af-147">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="0e8af-148">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="0e8af-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a><span data-ttu-id="0e8af-149">Obtener la longitud de cola de Hola</span><span class="sxs-lookup"><span data-stu-id="0e8af-149">Get hello queue length</span></span>
<span data-ttu-id="0e8af-150">Puede obtener una estimación del número de Hola de mensajes en una cola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-150">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="0e8af-151">El **FetchAttributes** método pide al servicio de cola de Hola para recuperar los atributos de la cola de hello, incluido el número de mensajes de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-151">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="0e8af-152">Hola **ApproximateMethodCount** propiedad devuelve el valor última de hello recuperado por la **FetchAttributes** método sin llamar al servicio de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-152">hello **ApproximateMethodCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="0e8af-153">Usar hello asincrónicas Await patrón común de las API de cola de Azure</span><span class="sxs-lookup"><span data-stu-id="0e8af-153">Use hello Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="0e8af-154">Este ejemplo muestra cómo hello toouse asincrónicas Await patrón común de las API de cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8af-154">This example shows how toouse hello Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="0e8af-155">ejemplo de Hola llama versión de async Hola de cada uno de hello tiene métodos, esto puede verse por hello **Async** posteriores a la corrección de cada método.</span><span class="sxs-lookup"><span data-stu-id="0e8af-155">hello sample calls hello async version of each of hello given methods, this can be seen by hello **Async** post-fix of each method.</span></span> <span data-ttu-id="0e8af-156">Cuando un método asincrónico es Hola usado async-await patrón suspende la ejecución local hasta que se complete la llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-156">When an async method is used hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="0e8af-157">Este comportamiento permite Hola actual subproceso toodo otro trabajo que ayuda a evitar los cuellos de botella de rendimiento y aumenta la capacidad de respuesta general de la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-157">This behavior allows hello current thread toodo other work which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="0e8af-158">Para obtener más detalles sobre el uso de Hola patrón Async y Await en .NET vea [Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="0e8af-158">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="0e8af-159">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="0e8af-159">Delete a queue</span></span>
<span data-ttu-id="0e8af-160">toodelete una cola y todos los mensajes de Hola contenidos en él, llamada hello **eliminar** método hello en objetos de cola.</span><span class="sxs-lookup"><span data-stu-id="0e8af-160">toodelete a queue and all hello messages contained in it, call hello **Delete** method on hello queue object.</span></span>

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="0e8af-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e8af-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

