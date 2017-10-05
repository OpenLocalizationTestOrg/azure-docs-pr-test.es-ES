---
title: "Introducción a Azure Queue Storage mediante .NET | Microsoft Docs"
description: "Las colas de Azure proporcionan mensajería asincrónica confiable entre componentes de aplicaciones. La mensajería en la nube permite que los componentes de las aplicaciones se escalen de forma independiente."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: aa292c1eb048444f988a641df44183312cf39d28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="f99de-104">Introducción al Almacenamiento en cola de Azure mediante .NET</span><span class="sxs-lookup"><span data-stu-id="f99de-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="f99de-105">Información general</span><span class="sxs-lookup"><span data-stu-id="f99de-105">Overview</span></span>
<span data-ttu-id="f99de-106">El almacenamiento en cola de Azure proporciona mensajería en la nube entre componentes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f99de-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="f99de-107">A la hora de diseñar aplicaciones para escala, los componentes de las mismas suelen desacoplarse para poder escalarlos de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="f99de-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="f99de-108">El almacenamiento en cola ofrece mensajería asincrónica para la comunicación entre los componentes de las aplicaciones, independientemente de si se ejecutan en la nube, en el escritorio, en un servidor local o en un dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="f99de-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="f99de-109">Además, este tipo de almacenamiento admite la administración de tareas asincrónicas y la creación de flujos de trabajo de procesos.</span><span class="sxs-lookup"><span data-stu-id="f99de-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="f99de-110">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="f99de-110">About this tutorial</span></span>
<span data-ttu-id="f99de-111">Este tutorial muestra cómo escribir código .NET para algunos escenarios comunes con el Almacenamiento en cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="f99de-111">This tutorial shows how to write .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="f99de-112">Entre los escenarios descritos se incluyen los siguientes: creación y eliminación de colas y adición, lectura y eliminación de mensajes de la cola.</span><span class="sxs-lookup"><span data-stu-id="f99de-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="f99de-113">**Tiempo estimado para completar:** 45 minutos</span><span class="sxs-lookup"><span data-stu-id="f99de-113">**Estimated time to complete:** 45 minutes</span></span>

<span data-ttu-id="f99de-114">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="f99de-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="f99de-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f99de-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="f99de-116">Biblioteca de cliente de Almacenamiento de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="f99de-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="f99de-117">Administrador de configuración Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="f99de-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="f99de-118">Una [cuenta de almacenamiento de Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="f99de-118">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="f99de-119">Adición de directivas using</span><span class="sxs-lookup"><span data-stu-id="f99de-119">Add using directives</span></span>
<span data-ttu-id="f99de-120">Agregue las siguientes directivas `using` al principio del archivo `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="f99de-120">Add the following `using` directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="f99de-121">Análisis de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="f99de-121">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-queue-service-client"></a><span data-ttu-id="f99de-122">Creación del cliente del servicio Cola</span><span class="sxs-lookup"><span data-stu-id="f99de-122">Create the Queue service client</span></span>
<span data-ttu-id="f99de-123">La clase **CloudQueueClient** le permite recuperar las colas almacenadas en Almacenamiento en cola.</span><span class="sxs-lookup"><span data-stu-id="f99de-123">The **CloudQueueClient** class enables you to retrieve queues stored in Queue storage.</span></span> <span data-ttu-id="f99de-124">Esta es una forma de crear el cliente de servicio:</span><span class="sxs-lookup"><span data-stu-id="f99de-124">Here's one way to create the service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="f99de-125">Ahora ya puede escribir código que lee y escribe datos en el Almacenamiento en cola.</span><span class="sxs-lookup"><span data-stu-id="f99de-125">Now you are ready to write code that reads data from and writes data to Queue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="f99de-126">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="f99de-126">Create a queue</span></span>
<span data-ttu-id="f99de-127">En este ejemplo se muestra cómo crear una cola si todavía no existe:</span><span class="sxs-lookup"><span data-stu-id="f99de-127">This example shows how to create a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="f99de-128">un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="f99de-128">Insert a message into a queue</span></span>
<span data-ttu-id="f99de-129">Para insertar un mensaje en una cola existente, cree en primer lugar un nuevo **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="f99de-129">To insert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="f99de-130">A continuación, llame al método **AddMessage** .</span><span class="sxs-lookup"><span data-stu-id="f99de-130">Next, call the **AddMessage** method.</span></span> <span data-ttu-id="f99de-131">Se puede crear un valor de **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de **bytes**.</span><span class="sxs-lookup"><span data-stu-id="f99de-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="f99de-132">A continuación se muestra el código con el que se crea una cola (si no existe) y se inserta el mensaje "Hola, mundo":</span><span class="sxs-lookup"><span data-stu-id="f99de-132">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create the queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it to the queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-the-next-message"></a><span data-ttu-id="f99de-133">siguiente mensaje</span><span class="sxs-lookup"><span data-stu-id="f99de-133">Peek at the next message</span></span>
<span data-ttu-id="f99de-134">Puede inspeccionar el mensaje situado en la parte delantera de una cola, sin quitarlo de la cola, mediante una llamada al método **PeekMessage** .</span><span class="sxs-lookup"><span data-stu-id="f99de-134">You can peek at the message in the front of a queue without removing it from the queue by calling the **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at the next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="f99de-135">contenido de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="f99de-135">Change the contents of a queued message</span></span>
<span data-ttu-id="f99de-136">Puede cambiar el contenido de un mensaje local en la cola.</span><span class="sxs-lookup"><span data-stu-id="f99de-136">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="f99de-137">Si el mensaje representa una tarea de trabajo, puede usar esta característica para actualizar el estado de la tarea de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f99de-137">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="f99de-138">El siguiente código actualiza el mensaje de la cola con contenido nuevo y amplía el tiempo de espera de la visibilidad en 60 segundos más.</span><span class="sxs-lookup"><span data-stu-id="f99de-138">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="f99de-139">De este modo, se guarda el estado de trabajo asociado al mensaje y se le proporciona al cliente un minuto más para que siga elaborando el mensaje.</span><span class="sxs-lookup"><span data-stu-id="f99de-139">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="f99de-140">Esta técnica se puede utilizar para realizar un seguimiento de los flujos de trabajo de varios pasos en los mensajes en cola, sin que sea necesario volver a empezar desde el principio si se produce un error en un paso del proceso a causa de un error de hardware o software.</span><span class="sxs-lookup"><span data-stu-id="f99de-140">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="f99de-141">Normalmente, también mantendría un número de reintentos y, si el mensaje se intentara más de *n* veces, lo eliminaría.</span><span class="sxs-lookup"><span data-stu-id="f99de-141">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="f99de-142">Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.</span><span class="sxs-lookup"><span data-stu-id="f99de-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the message from the queue and update the message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-the-next-message"></a><span data-ttu-id="f99de-143">siguiente mensaje de la cola</span><span class="sxs-lookup"><span data-stu-id="f99de-143">De-queue the next message</span></span>
<span data-ttu-id="f99de-144">El código quita un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="f99de-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="f99de-145">Si llama a **GetMessage**, obtiene el siguiente mensaje en una cola.</span><span class="sxs-lookup"><span data-stu-id="f99de-145">When you call **GetMessage**, you get the next message in a queue.</span></span> <span data-ttu-id="f99de-146">Un mensaje devuelto por **GetMessage** se hace invisible a cualquier otro código de lectura de mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="f99de-146">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="f99de-147">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="f99de-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="f99de-148">Para acabar de quitar el mensaje de la cola, también debe llamar a **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="f99de-148">To finish removing the message from the queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="f99de-149">Este proceso de extracción de un mensaje que consta de dos pasos garantiza que si su código no puede procesar un mensaje a causa de un error de hardware o software, otra instancia de su código puede obtener el mismo mensaje e intentarlo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="f99de-149">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="f99de-150">El código llama a **DeleteMessage** justo después de que se haya procesado el mensaje.</span><span class="sxs-lookup"><span data-stu-id="f99de-150">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get the next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process the message in less than 30 seconds, and then delete the message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="f99de-151">Uso del patrón Async-Await con API comunes de almacenamiento de colas</span><span class="sxs-lookup"><span data-stu-id="f99de-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="f99de-152">En este ejemplo se muestra cómo usar el patrón Async-Await con API comunes de almacenamiento de colas.</span><span class="sxs-lookup"><span data-stu-id="f99de-152">This example shows how to use the Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="f99de-153">El ejemplo llama a la versión asincrónica de cada uno de los métodos indicados, tal como se puede ver por el sufijo *Async* de cada método.</span><span class="sxs-lookup"><span data-stu-id="f99de-153">The sample calls the asynchronous version of each of the given methods, as indicated by the *Async* suffix of each method.</span></span> <span data-ttu-id="f99de-154">Cuando se utiliza un método asincrónico, el patrón Async-Await suspende la ejecución local hasta que se completa la llamada.</span><span class="sxs-lookup"><span data-stu-id="f99de-154">When an async method is used, the async-await pattern suspends local execution until the call completes.</span></span> <span data-ttu-id="f99de-155">Este comportamiento permite que el subproceso actual realice otro trabajo, lo que ayuda a evitar cuellos de botella en el rendimiento y mejora la capacidad de respuesta general de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f99de-155">This behavior allows the current thread to do other work, which helps avoid performance bottlenecks and improves the overall responsiveness of your application.</span></span> <span data-ttu-id="f99de-156">Para más información sobre el uso del patrón Async-Await en. NET, consulte [Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="f99de-156">For more details on using the Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create the queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message to put in the queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue the message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue the message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete the message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="f99de-157">Uso de opciones adicionales para quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="f99de-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="f99de-158">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="f99de-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="f99de-159">En primer lugar, puede obtener un lote de mensajes (hasta 32).</span><span class="sxs-lookup"><span data-stu-id="f99de-159">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="f99de-160">En segundo lugar, puede establecer un tiempo de espera de la invisibilidad más largo o más corto para que el código disponga de más o menos tiempo para procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="f99de-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="f99de-161">El siguiente ejemplo de código utiliza el método **GetMessages** para obtener 20 mensajes en una llamada.</span><span class="sxs-lookup"><span data-stu-id="f99de-161">The following code example uses the **GetMessages** method to get 20 messages in one call.</span></span> <span data-ttu-id="f99de-162">A continuación, procesa cada mensaje con un bucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="f99de-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="f99de-163">También establece el tiempo de espera de la invisibilidad en cinco minutos para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="f99de-163">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="f99de-164">Tenga en cuenta que los 5 minutos empiezan a contar para todos los mensajes al mismo tiempo, por lo que después de pasar los 5 minutos desde la llamada a **GetMessages**, todos los mensajes que no se han eliminado volverán a estar visibles.</span><span class="sxs-lookup"><span data-stu-id="f99de-164">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-the-queue-length"></a><span data-ttu-id="f99de-165">la longitud de la cola</span><span class="sxs-lookup"><span data-stu-id="f99de-165">Get the queue length</span></span>
<span data-ttu-id="f99de-166">Puede obtener una estimación del número de mensajes existentes en una cola.</span><span class="sxs-lookup"><span data-stu-id="f99de-166">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="f99de-167">El método **FetchAttributes** solicita al servicio de cola la recuperación de los atributos de la cola, incluido el número de mensajes.</span><span class="sxs-lookup"><span data-stu-id="f99de-167">The **FetchAttributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="f99de-168">La propiedad **ApproximateMessageCount** devuelve el último valor recuperado por el método **FetchAttributes**, sin llamar a Queue service.</span><span class="sxs-lookup"><span data-stu-id="f99de-168">The **ApproximateMessageCount** property returns the last value retrieved by the **FetchAttributes** method, without calling the Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch the queue attributes.
queue.FetchAttributes();

// Retrieve the cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="f99de-169">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="f99de-169">Delete a queue</span></span>
<span data-ttu-id="f99de-170">Para eliminar una cola y todos los mensajes contenidos en ella, llame al método **Delete** en el objeto de cola.</span><span class="sxs-lookup"><span data-stu-id="f99de-170">To delete a queue and all the messages contained in it, call the **Delete** method on the queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference to a queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete the queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="f99de-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f99de-171">Next steps</span></span>
<span data-ttu-id="f99de-172">Ahora que está familiarizado con los aspectos básicos del almacenamiento de colas, utilice estos vínculos para obtener más información acerca de tareas de almacenamiento más complejas.</span><span class="sxs-lookup"><span data-stu-id="f99de-172">Now that you've learned the basics of Queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="f99de-173">Consulte la documentación de referencia del servicio de cola para obtener información detallada acerca de las API disponibles:</span><span class="sxs-lookup"><span data-stu-id="f99de-173">View the Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="f99de-174">Referencia de la biblioteca de clientes de almacenamiento para .NET</span><span class="sxs-lookup"><span data-stu-id="f99de-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="f99de-175">Referencia de API de REST</span><span class="sxs-lookup"><span data-stu-id="f99de-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="f99de-176">Aprenda a simplificar el código que escriba para trabajar con Almacenamiento de Azure mediante [SDK de WebJobs de Azure](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f99de-176">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="f99de-177">Consulte más guías de características para obtener información acerca de otras opciones del almacenamiento de datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="f99de-177">View more feature guides to learn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="f99de-178">[Introducción al Almacenamiento de tablas de Azure mediante .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) para almacenar datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="f99de-178">[Get started with Azure Table storage using .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) to store structured data.</span></span>
  * <span data-ttu-id="f99de-179">[Introducción al Almacenamiento de blobs de Azure mediante .NET](../blobs/storage-dotnet-how-to-use-blobs.md) para almacenar datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="f99de-179">[Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
  * <span data-ttu-id="f99de-180">Para almacenar datos relacionales, consulte [Conexión a SQL Database mediante .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md).</span><span class="sxs-lookup"><span data-stu-id="f99de-180">[Connect to SQL Database by using .NET (C#)](../../sql-database/sql-database-connect-query-dotnet-core.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
