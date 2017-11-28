---
title: "Introducción a Queue Storage y los servicios conectados de Visual Studio (ASP.NET Core) | Microsoft Docs"
description: "Introducción al uso de Azure Queue Storage en un proyecto de ASP.NET Core en Visual Studio"
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
ms.openlocfilehash: 4622496544ce6e1057ac68a2e9946917573e997e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="9acef-103">Introducción a Queue Storage y a los servicios conectados de Visual Studio (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="9acef-103">Get started with queue storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="9acef-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9acef-104">Overview</span></span>
<span data-ttu-id="9acef-105">En este artículo se describe cómo empezar a usar Azure Queue Storage en Visual Studio después de crear una cuenta de Azure Storage en un proyecto de ASP.NET Core mediante el cuadro de diálogo **Add Connected Services** (Agregar servicios conectados) de Visual Studio, o después de hacer referencia a una.</span><span class="sxs-lookup"><span data-stu-id="9acef-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="9acef-106">La operación **Agregar servicios conectados** instala los paquetes de NuGet adecuados para tener acceso al almacenamiento de Azure en el proyecto y agrega la cadena de conexión de la cuenta de almacenamiento a los archivos de configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="9acef-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="9acef-107">El almacenamiento de cola de Azure es un servicio para almacenar grandes cantidades de mensajes a los que puede obtenerse acceso desde cualquier lugar del mundo a través de llamadas autenticadas con HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9acef-107">Azure queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="9acef-108">Un único mensaje en cola puede tener un tamaño de hasta 64 kilobytes (KB) y una cola puede contener millones de mensajes, hasta el límite de capacidad total de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9acef-108">A single queue message can be up to 64 kilobytes (KB) in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

<span data-ttu-id="9acef-109">Para comenzar, necesita crear una cola de Azure en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9acef-109">To get started, you first need to create an Azure queue in your storage account.</span></span> <span data-ttu-id="9acef-110">Le mostraremos cómo crear una cola en el código.</span><span class="sxs-lookup"><span data-stu-id="9acef-110">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="9acef-111">También le mostraremos cómo realizar operaciones básicas de cola, como agregar, modificar, leer y quitar mensajes de cola.</span><span class="sxs-lookup"><span data-stu-id="9acef-111">We'll also show you how to perform basic queue operations, such as adding, modifying, reading, and removing queue messages.</span></span> <span data-ttu-id="9acef-112">Los ejemplos están escritos en código C\# y usan la biblioteca del cliente de Azure Storage para .NET.</span><span class="sxs-lookup"><span data-stu-id="9acef-112">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="9acef-113">Para obtener más información acerca de ASP.NET, consulte [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="9acef-113">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

<span data-ttu-id="9acef-114">**NOTA**: Algunas de las API que realizan llamadas a Azure Storage en ASP.NET Core son asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="9acef-114">**NOTE:** Some of the APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="9acef-115">Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="9acef-115">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="9acef-116">El código siguiente supone que se están utilizando métodos de programación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="9acef-116">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="9acef-117">Consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](storage-dotnet-how-to-use-queues.md) para más información sobre la manipulación de colas mediante programación.</span><span class="sxs-lookup"><span data-stu-id="9acef-117">See [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md) for more information on programmatically manipulating queues.</span></span>
* <span data-ttu-id="9acef-118">Vea [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/) para información general sobre Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="9acef-118">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="9acef-119">Vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/) para información general sobre los servicios en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="9acef-119">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="9acef-120">Vea [ASP.NET](http://www.asp.net) para más información sobre la programación de aplicaciones ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9acef-120">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="9acef-121">Acceso a colas en el código</span><span class="sxs-lookup"><span data-stu-id="9acef-121">Access queues in code</span></span>
<span data-ttu-id="9acef-122">Para obtener acceso a las colas de los proyectos de ASP.NET Core, debe incluir los elementos siguientes en los archivos de origen de C# que tengan acceso a Azure Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="9acef-122">To access queues in ASP.NET Core projects, you need to include the following items to any C# source file that accesses Azure queue storage.</span></span>

1. <span data-ttu-id="9acef-123">Asegúrese de que las declaraciones del espacio de nombres de la parte superior del archivo de C# incluyen estas instrucciones **using** .</span><span class="sxs-lookup"><span data-stu-id="9acef-123">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="9acef-124">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9acef-124">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9acef-125">Use el código siguiente para obtener la cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de la configuración del servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="9acef-125">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="9acef-126">Obtenga un objeto **CloudTableClient** para hacer referencia a los objetos de cola en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9acef-126">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the CloudQueueClient object for the storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="9acef-127">Obtenga un objeto **CloudQueue** para hacer referencia a una cola específica.</span><span class="sxs-lookup"><span data-stu-id="9acef-127">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to the CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="9acef-128">**NOTA:** use todo el código anterior delante del código que aparece en las muestras siguientes.</span><span class="sxs-lookup"><span data-stu-id="9acef-128">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

### <a name="create-a-queue-in-code"></a><span data-ttu-id="9acef-129">Creación de una cola en código</span><span class="sxs-lookup"><span data-stu-id="9acef-129">Create a queue in code</span></span>
<span data-ttu-id="9acef-130">Para crear la cola de Azure en el código, solo tiene que agregar una llamada a **CreateIfNotExistsAsync**.</span><span class="sxs-lookup"><span data-stu-id="9acef-130">To create the Azure queue in code, just add a call to **CreateIfNotExistsAsync**.</span></span>

    // Create the CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="9acef-131">un mensaje a una cola</span><span class="sxs-lookup"><span data-stu-id="9acef-131">Add a message to a queue</span></span>
<span data-ttu-id="9acef-132">Para insertar un mensaje en una cola existente, cree un nuevo objeto **CloudQueueMessage** y luego llame al método **AddMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="9acef-132">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessageAsync** method.</span></span>

<span data-ttu-id="9acef-133">Se puede crear un objeto **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="9acef-133">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="9acef-134">Este es un ejemplo que inserta el mensaje "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="9acef-134">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="9acef-135">Leer un mensaje de una cola</span><span class="sxs-lookup"><span data-stu-id="9acef-135">Read a message in a queue</span></span>
<span data-ttu-id="9acef-136">Puede inspeccionar el mensaje situado al principio de una cola sin quitarlo de ella, llamando al método **PeekMessageAsync** .</span><span class="sxs-lookup"><span data-stu-id="9acef-136">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessageAsync** method.</span></span>

    // Peek the next message in the queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="9acef-137">Leer y eliminar un mensaje de una cola</span><span class="sxs-lookup"><span data-stu-id="9acef-137">Read and remove a message in a queue</span></span>
<span data-ttu-id="9acef-138">Su código puede quitar un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="9acef-138">Your code can remove (dequeue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="9acef-139">Llame a **GetMessageAsync** para obtener el mensaje siguiente de una cola.</span><span class="sxs-lookup"><span data-stu-id="9acef-139">Call **GetMessageAsync** to get the next message in a queue.</span></span> <span data-ttu-id="9acef-140">Un mensaje devuelto por **GetMessageAsync** se hace invisible a cualquier otro código de lectura de mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="9acef-140">A message returned from **GetMessageAsync** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="9acef-141">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="9acef-141">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="9acef-142">Para terminar de quitar el mensaje de la cola, llame a **DeleteMessageAsync**.</span><span class="sxs-lookup"><span data-stu-id="9acef-142">To finish removing the message from the queue, call **DeleteMessageAsync**.</span></span>

<span data-ttu-id="9acef-143">Este proceso extracción de un mensaje que consta de dos pasos garantiza que si su código no puede procesar un mensaje a causa de un error de hardware o software, otra instancia de su código puede obtener el mismo mensaje e intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="9acef-143">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="9acef-144">El código siguiente llama a **DeleteMessageAsync** justo después de procesar el mensaje.</span><span class="sxs-lookup"><span data-stu-id="9acef-144">The following code calls **DeleteMessageAsync** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process the message in less than 30 seconds.

    // Then delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a><span data-ttu-id="9acef-145">las opciones adicionales de los mensajes quitados de la cola</span><span class="sxs-lookup"><span data-stu-id="9acef-145">Leverage additional options for dequeuing messages</span></span>
<span data-ttu-id="9acef-146">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="9acef-146">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="9acef-147">En primer lugar, puede obtener un lote de mensajes (hasta 32).</span><span class="sxs-lookup"><span data-stu-id="9acef-147">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="9acef-148">En segundo lugar, puede establecer un tiempo de espera de la invisibilidad más largo o más corto para que el código disponga de más o menos tiempo para procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="9acef-148">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="9acef-149">El siguiente ejemplo de código utiliza el método **GetMessages** para obtener 20 mensajes en una llamada.</span><span class="sxs-lookup"><span data-stu-id="9acef-149">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="9acef-150">A continuación, procesa cada mensaje con un bucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="9acef-150">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="9acef-151">También establece el tiempo de espera de la invisibilidad en 5 minutos para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="9acef-151">It also sets the invisibility timeout to 5 minutes for each message.</span></span> <span data-ttu-id="9acef-152">Tenga en cuenta que los 5 minutos empiezan a contar para todos los mensajes al mismo tiempo, por lo que, después de pasar los 5 minutos desde la llamada a **GetMessages**, todos los mensajes que no se han eliminado volverán a estar visibles.</span><span class="sxs-lookup"><span data-stu-id="9acef-152">Note that the 5 minutes start for all messages at the same time, so after 5 minutes have passed after the call to **GetMessages**, any messages which have not been deleted become visible again.</span></span>

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-the-queue-length"></a><span data-ttu-id="9acef-153">la longitud de la cola</span><span class="sxs-lookup"><span data-stu-id="9acef-153">Get the queue length</span></span>
<span data-ttu-id="9acef-154">Puede obtener una estimación del número de mensajes existentes en una cola.</span><span class="sxs-lookup"><span data-stu-id="9acef-154">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="9acef-155">El método **FetchAttributes** solicita al servicio de cola la recuperación de los atributos de la cola, incluido el número de mensajes.</span><span class="sxs-lookup"><span data-stu-id="9acef-155">The **FetchAttributes** method asks the queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="9acef-156">La propiedad **ApproximateMethodCount** devuelve el último valor recuperado por el método **FetchAttributes**, sin llamar a Queue service.</span><span class="sxs-lookup"><span data-stu-id="9acef-156">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display the number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-queue-apis"></a><span data-ttu-id="9acef-157">Uso del patrón Async-Await con API de cola comunes</span><span class="sxs-lookup"><span data-stu-id="9acef-157">Use the Async-Await pattern with common queue APIs</span></span>
<span data-ttu-id="9acef-158">En este ejemplo se muestra cómo usar el patrón Async-Await con API de cola comunes.</span><span class="sxs-lookup"><span data-stu-id="9acef-158">This example shows how to use the Async-Await pattern with common queue APIs.</span></span> <span data-ttu-id="9acef-159">El ejemplo llama a la versión asincrónica de cada uno de los métodos determinados.</span><span class="sxs-lookup"><span data-stu-id="9acef-159">The sample calls the async version of each of the given methods.</span></span> <span data-ttu-id="9acef-160">Esto se puede ver con el postfijo de Async de cada método.</span><span class="sxs-lookup"><span data-stu-id="9acef-160">This can be seen by the Async post-fix of each method.</span></span> <span data-ttu-id="9acef-161">Cuando se usa un método asincrónico, el patrón Async-Await suspende la ejecución local hasta que se complete la llamada.</span><span class="sxs-lookup"><span data-stu-id="9acef-161">When an async method is used, the Async-Await pattern suspends local execution until the call is completed.</span></span> <span data-ttu-id="9acef-162">Este comportamiento permite que el subproceso actual realice otro trabajo que ayuda a evitar cuellos de botella en el rendimiento y mejora la capacidad de respuesta general de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9acef-162">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="9acef-163">Para más información sobre el uso del patrón Async-Await en. NET, consulte [Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="9acef-163">For more details on using the Async-Await pattern in .NET, see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to add to the queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue the message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete the message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a><span data-ttu-id="9acef-164">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="9acef-164">Delete a queue</span></span>
<span data-ttu-id="9acef-165">Para eliminar una cola y todos los mensajes contenidos en ella, llame al método **Delete** en el objeto de cola.</span><span class="sxs-lookup"><span data-stu-id="9acef-165">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();


## <a name="next-steps"></a><span data-ttu-id="9acef-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9acef-166">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

