---
title: "Introducción al almacenamiento de colas y los servicios conectados de Visual Studio (servicios en la nube) | Microsoft Docs"
description: "Cómo empezar a usar el almacenamiento de colas de Azure en un proyecto de servicio en la nube en Visual Studio, después de conectarse a una cuenta de almacenamiento mediante los servicios conectados de Visual Studio"
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
ms.openlocfilehash: 7a6e58a62b4cfbf99641559363dd0c860cdf8af2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="c9076-103">Introducción al almacenamiento de colas de Azure y a los servicios conectados de Visual Studio (proyectos de servicios en la nube)</span><span class="sxs-lookup"><span data-stu-id="c9076-103">Getting started with Azure Queue storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="c9076-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c9076-104">Overview</span></span>
<span data-ttu-id="c9076-105">En este artículo se describe cómo empezar a usar Azure Queue Storage en Visual Studio después de crear una cuenta de almacenamiento de Azure en un proyecto de servicios en la nube mediante el cuadro de diálogo **Agregar servicios conectados** de Visual Studio, o después hacer referencia a una.</span><span class="sxs-lookup"><span data-stu-id="c9076-105">This article describes how to get started using Azure Queue storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the  Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="c9076-106">Le mostraremos cómo crear una cola en el código.</span><span class="sxs-lookup"><span data-stu-id="c9076-106">We'll show you how to create a queue in code.</span></span> <span data-ttu-id="c9076-107">También le mostraremos cómo realizar operaciones básicas de cola, como agregar, modificar, leer y quitar mensajes de cola.</span><span class="sxs-lookup"><span data-stu-id="c9076-107">We'll also show you how to perform basic queue operations, such as adding, modifying, reading and removing queue messages.</span></span> <span data-ttu-id="c9076-108">Los ejemplos están escritos en código C# y usan la [biblioteca del cliente de almacenamiento de Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9076-108">The samples are written in C# code and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="c9076-109">La operación **Agregar servicios conectados** instala los paquetes de NuGet adecuados para tener acceso al almacenamiento de Azure en el proyecto y agrega la cadena de conexión para la cuenta de almacenamiento a los archivos de configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="c9076-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

* <span data-ttu-id="c9076-110">Consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) para más información sobre la manipulación de colas en el código.</span><span class="sxs-lookup"><span data-stu-id="c9076-110">See [Get started with Azure Queue storage using .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) for more information on manipulating queues in code.</span></span>
* <span data-ttu-id="c9076-111">Vea [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/) para información general sobre Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9076-111">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="c9076-112">Vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/) para información general sobre los servicios en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9076-112">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="c9076-113">Vea [ASP.NET](http://www.asp.net) para más información sobre la programación de aplicaciones ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c9076-113">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

<span data-ttu-id="c9076-114">El almacenamiento en cola de Azure es un servicio para almacenar grandes cantidades de mensajes a los que puede obtenerse acceso desde cualquier lugar del mundo a través de llamadas autenticadas con HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c9076-114">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="c9076-115">Un único mensaje en cola puede tener un tamaño de hasta 64 KB y una cola puede contener millones de mensajes, hasta el límite de capacidad total de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c9076-115">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="access-queues-in-code"></a><span data-ttu-id="c9076-116">Acceso a colas en el código</span><span class="sxs-lookup"><span data-stu-id="c9076-116">Access queues in code</span></span>
<span data-ttu-id="c9076-117">Para obtener acceso a las colas en los proyectos de Servicios en la nube de Visual Studio, debe incluir los elementos siguientes en los archivos de código fuente de C# que tengan acceso al almacenamiento de colas de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9076-117">To access queues in Visual Studio Cloud Services projects, you need to include the following items to any C# source file that access Azure Queue storage.</span></span>

1. <span data-ttu-id="c9076-118">Asegúrese de que las declaraciones del espacio de nombres de la parte superior del archivo de C# incluyen estas instrucciones **using** .</span><span class="sxs-lookup"><span data-stu-id="c9076-118">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. <span data-ttu-id="c9076-119">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c9076-119">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="c9076-120">Use el código siguiente para obtener la cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de la configuración del servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9076-120">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. <span data-ttu-id="c9076-121">Obtenga un objeto **CloudTableClient** para hacer referencia a los objetos de cola en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c9076-121">Get a **CloudQueueClient** object to reference the queue objects in your storage account.</span></span>  
   
        // Create the queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. <span data-ttu-id="c9076-122">Obtenga un objeto **CloudQueue** para hacer referencia a una cola específica.</span><span class="sxs-lookup"><span data-stu-id="c9076-122">Get a **CloudQueue** object to reference a specific queue.</span></span>
   
        // Get a reference to a queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

<span data-ttu-id="c9076-123">**NOTA:** use todo el código anterior delante del código que aparece en las muestras siguientes.</span><span class="sxs-lookup"><span data-stu-id="c9076-123">**NOTE:** Use all of the above code in front of the code in the following samples.</span></span>

## <a name="create-a-queue-in-code"></a><span data-ttu-id="c9076-124">Creación de una cola en código</span><span class="sxs-lookup"><span data-stu-id="c9076-124">Create a queue in code</span></span>
<span data-ttu-id="c9076-125">Para crear la cola en el código, simplemente agregue una llamada a **CreateIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="c9076-125">To create the queue in code, just add a call to **CreateIfNotExists**.</span></span>

    // Create the CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="c9076-126">un mensaje a una cola</span><span class="sxs-lookup"><span data-stu-id="c9076-126">Add a message to a queue</span></span>
<span data-ttu-id="c9076-127">Para insertar un mensaje en una cola existente, cree un nuevo objeto **CloudQueueMessage** y luego llame al método **AddMessage**.</span><span class="sxs-lookup"><span data-stu-id="c9076-127">To insert a message into an existing queue, create a new **CloudQueueMessage** object, then call the **AddMessage** method.</span></span>

<span data-ttu-id="c9076-128">Se puede crear un objeto **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="c9076-128">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="c9076-129">Este es un ejemplo que inserta el mensaje "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="c9076-129">Here is an example which inserts the message 'Hello, World'.</span></span>

    // Create a message and add it to the queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a><span data-ttu-id="c9076-130">Leer un mensaje de una cola</span><span class="sxs-lookup"><span data-stu-id="c9076-130">Read a message in a queue</span></span>
<span data-ttu-id="c9076-131">Puede inspeccionar el mensaje situado en la parte delantera de una cola, sin quitarlo de la cola, mediante una llamada al método **PeekMessage** .</span><span class="sxs-lookup"><span data-stu-id="c9076-131">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

    // Peek at the next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a><span data-ttu-id="c9076-132">Leer y eliminar un mensaje de una cola</span><span class="sxs-lookup"><span data-stu-id="c9076-132">Read and remove a message in a queue</span></span>
<span data-ttu-id="c9076-133">Su código puede quitar un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="c9076-133">Your code can remove (de-queue) a message from a queue in two steps.</span></span>

1. <span data-ttu-id="c9076-134">Llame a **GetMessage** para obtener el siguiente mensaje en una cola.</span><span class="sxs-lookup"><span data-stu-id="c9076-134">Call **GetMessage** to get the next message in a queue.</span></span> <span data-ttu-id="c9076-135">Un mensaje devuelto por **GetMessage** se hace invisible a cualquier otro código de lectura de mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="c9076-135">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="c9076-136">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="c9076-136">By default, this message stays invisible for 30 seconds.</span></span>
2. <span data-ttu-id="c9076-137">Para terminar de quitar el mensaje de la cola, llame a **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="c9076-137">To finish removing the message from the queue, call **DeleteMessage**.</span></span>

<span data-ttu-id="c9076-138">Este proceso extracción de un mensaje que consta de dos pasos garantiza que si su código no puede procesar un mensaje a causa de un error de hardware o software, otra instancia de su código puede obtener el mismo mensaje e intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c9076-138">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="c9076-139">El código siguiente llama a **DeleteMessage** justo después de haber procesado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="c9076-139">The following code calls **DeleteMessage** right after the message has been processed.</span></span>

    // Get the next message in the queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process the message in less than 30 seconds

    // Then delete the message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-to-process-and-remove-queue-messages"></a><span data-ttu-id="c9076-140">Uso de opciones adicionales para procesar y quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="c9076-140">Use additional options to process and remove queue messages</span></span>
<span data-ttu-id="c9076-141">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="c9076-141">There are two ways you can customize message retrieval from a queue.</span></span>

* <span data-ttu-id="c9076-142">Puede obtener un lote de mensajes (hasta 32).</span><span class="sxs-lookup"><span data-stu-id="c9076-142">You can get a batch of messages (up to 32).</span></span>
* <span data-ttu-id="c9076-143">En segundo lugar, puede establecer un tiempo de espera de la invisibilidad más largo o más corto para que el código disponga de más o menos tiempo para procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="c9076-143">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="c9076-144">El siguiente ejemplo de código utiliza el método **GetMessages** para obtener 20 mensajes en una llamada.</span><span class="sxs-lookup"><span data-stu-id="c9076-144">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="c9076-145">A continuación, procesa cada mensaje con un bucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="c9076-145">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="c9076-146">También establece el tiempo de espera de la invisibilidad en cinco minutos para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="c9076-146">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="c9076-147">Tenga en cuenta que los 5 minutos empiezan a contar para todos los mensajes al mismo tiempo, por lo que después de pasar los 5 minutos desde la llamada a **GetMessages**, todos los mensajes que no se han eliminado volverán a estar visibles.</span><span class="sxs-lookup"><span data-stu-id="c9076-147">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

<span data-ttu-id="c9076-148">Este es un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c9076-148">Here's an example:</span></span>

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete the message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-the-queue-length"></a><span data-ttu-id="c9076-149">la longitud de la cola</span><span class="sxs-lookup"><span data-stu-id="c9076-149">Get the queue length</span></span>
<span data-ttu-id="c9076-150">Puede obtener una estimación del número de mensajes existentes en una cola.</span><span class="sxs-lookup"><span data-stu-id="c9076-150">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="c9076-151">El método **FetchAttributes** solicita al servicio de cola la recuperación de los atributos de la cola, incluido el número de mensajes.</span><span class="sxs-lookup"><span data-stu-id="c9076-151">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="c9076-152">La propiedad **ApproximateMethodCount** devuelve el último valor recuperado por el método **FetchAttributes**, sin llamar a Queue service.</span><span class="sxs-lookup"><span data-stu-id="c9076-152">The **ApproximateMethodCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

    // Fetch the queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve the cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-the-async-await-pattern-with-common-azure-queue-apis"></a><span data-ttu-id="c9076-153">Uso del patrón Async-Await con las API de Cola de Azure comunes</span><span class="sxs-lookup"><span data-stu-id="c9076-153">Use the Async-Await Pattern with common Azure Queue APIs</span></span>
<span data-ttu-id="c9076-154">En este ejemplo se muestra cómo usar el patrón Async-Await con las API de Cola de Azure comunes.</span><span class="sxs-lookup"><span data-stu-id="c9076-154">This example shows how to use the Async-Await pattern with common Azure Queue APIs.</span></span> <span data-ttu-id="c9076-155">El ejemplo llama a la versión asincrónica de cada uno de los métodos determinados, esto se puede ver en la corrección de **Async** posterior de cada método.</span><span class="sxs-lookup"><span data-stu-id="c9076-155">The sample calls the async version of each of the given methods, this can be seen by the **Async** post-fix of each method.</span></span> <span data-ttu-id="c9076-156">Cuando se utiliza un método asincrónico, el patrón Async-Await suspende la ejecución local hasta que se complete la llamada.</span><span class="sxs-lookup"><span data-stu-id="c9076-156">When an async method is used the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="c9076-157">Este comportamiento permite que el subproceso actual realice otro trabajo que ayuda a evitar cuellos de botella en el rendimiento y mejora la capacidad de respuesta general de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9076-157">This behavior allows the current thread to do other work which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="c9076-158">Para más información sobre el uso del patrón Async-Await en. NET, consulte [Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9076-158">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

    // Create a message to put in the queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add the message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue the message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete the message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a><span data-ttu-id="c9076-159">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="c9076-159">Delete a queue</span></span>
<span data-ttu-id="c9076-160">Para eliminar una cola y todos los mensajes contenidos en ella, llame al método **Delete** en el objeto de cola.</span><span class="sxs-lookup"><span data-stu-id="c9076-160">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

    // Delete the queue.
    messageQueue.Delete();

## <a name="next-steps"></a><span data-ttu-id="c9076-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9076-161">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

