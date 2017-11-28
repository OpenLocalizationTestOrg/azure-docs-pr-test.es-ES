---
title: aaaGet a trabajar con almacenamiento de cola de Azure mediante .NET | Documentos de Microsoft
description: "Las colas de Azure proporcionan mensajería asincrónica confiable entre componentes de aplicaciones. La nube permite mensajería su tooscale de componentes de aplicación por separado."
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
ms.openlocfilehash: 36bbb40189a301cddbc2ded92d0623fa5e093eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a><span data-ttu-id="4fd64-104">Introducción al Almacenamiento en cola de Azure mediante .NET</span><span class="sxs-lookup"><span data-stu-id="4fd64-104">Get started with Azure Queue storage using .NET</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a><span data-ttu-id="4fd64-105">Información general</span><span class="sxs-lookup"><span data-stu-id="4fd64-105">Overview</span></span>
<span data-ttu-id="4fd64-106">El almacenamiento en cola de Azure proporciona mensajería en la nube entre componentes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="4fd64-106">Azure Queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="4fd64-107">A la hora de diseñar aplicaciones para escala, los componentes de las mismas suelen desacoplarse para poder escalarlos de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="4fd64-107">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="4fd64-108">Almacenamiento de cola ofrece mensajería asincrónica para la comunicación entre componentes de aplicaciones, si se están ejecutando en la nube de hello, en el escritorio de hello, en un servidor local o en un dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="4fd64-108">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="4fd64-109">Además, este tipo de almacenamiento admite la administración de tareas asincrónicas y la creación de flujos de trabajo de procesos.</span><span class="sxs-lookup"><span data-stu-id="4fd64-109">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="4fd64-110">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="4fd64-110">About this tutorial</span></span>
<span data-ttu-id="4fd64-111">Este tutorial muestra cómo código toowrite .NET en algunos escenarios comunes con almacenamiento en la cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd64-111">This tutorial shows how toowrite .NET code for some common scenarios using Azure Queue storage.</span></span> <span data-ttu-id="4fd64-112">Entre los escenarios descritos se incluyen los siguientes: creación y eliminación de colas y adición, lectura y eliminación de mensajes de la cola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-112">Scenarios covered include creating and deleting queues and adding, reading, and deleting queue messages.</span></span>

<span data-ttu-id="4fd64-113">**Estimado toocomplete de tiempo:** 45 minutos</span><span class="sxs-lookup"><span data-stu-id="4fd64-113">**Estimated time toocomplete:** 45 minutes</span></span>

<span data-ttu-id="4fd64-114">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="4fd64-114">**Prerequisities:**</span></span>

* [<span data-ttu-id="4fd64-115">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4fd64-115">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="4fd64-116">Biblioteca de cliente de Almacenamiento de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="4fd64-116">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="4fd64-117">Administrador de configuración Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="4fd64-117">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="4fd64-118">Una [cuenta de almacenamiento de Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="4fd64-118">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="4fd64-119">Adición de directivas using</span><span class="sxs-lookup"><span data-stu-id="4fd64-119">Add using directives</span></span>
<span data-ttu-id="4fd64-120">Agregue los siguiente hello `using` parte superior de toohello de directivas de hello `Program.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="4fd64-120">Add hello following `using` directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="4fd64-121">Analizar la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="4fd64-121">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a><span data-ttu-id="4fd64-122">Crear el cliente del servicio de cola de Hola</span><span class="sxs-lookup"><span data-stu-id="4fd64-122">Create hello Queue service client</span></span>
<span data-ttu-id="4fd64-123">Hola **CloudQueueClient** clase permite tooretrieve las colas almacenadas en almacenamiento de la cola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-123">hello **CloudQueueClient** class enables you tooretrieve queues stored in Queue storage.</span></span> <span data-ttu-id="4fd64-124">Este es el cliente del servicio de una manera toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="4fd64-124">Here's one way toocreate hello service client:</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
<span data-ttu-id="4fd64-125">Ahora está listo toowrite código que lee datos de y escribe datos tooQueue storage.</span><span class="sxs-lookup"><span data-stu-id="4fd64-125">Now you are ready toowrite code that reads data from and writes data tooQueue storage.</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="4fd64-126">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="4fd64-126">Create a queue</span></span>
<span data-ttu-id="4fd64-127">Este ejemplo se muestra cómo toocreate una cola si aún no existe:</span><span class="sxs-lookup"><span data-stu-id="4fd64-127">This example shows how toocreate a queue if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a><span data-ttu-id="4fd64-128">un mensaje en una cola</span><span class="sxs-lookup"><span data-stu-id="4fd64-128">Insert a message into a queue</span></span>
<span data-ttu-id="4fd64-129">tooinsert un mensaje en una cola existente, primero debe crear un nuevo **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="4fd64-129">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="4fd64-130">A continuación, llame a hello **AddMessage** método.</span><span class="sxs-lookup"><span data-stu-id="4fd64-130">Next, call hello **AddMessage** method.</span></span> <span data-ttu-id="4fd64-131">Se puede crear un valor de **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de **bytes**.</span><span class="sxs-lookup"><span data-stu-id="4fd64-131">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a **byte** array.</span></span> <span data-ttu-id="4fd64-132">Este es el código que crea una cola (si no existe) y el mensaje de bienvenida de inserciones "¡Hello, World":</span><span class="sxs-lookup"><span data-stu-id="4fd64-132">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="4fd64-133">Consultar mensajes de bienvenida del siguiente</span><span class="sxs-lookup"><span data-stu-id="4fd64-133">Peek at hello next message</span></span>
<span data-ttu-id="4fd64-134">Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **PeekMessage** método.</span><span class="sxs-lookup"><span data-stu-id="4fd64-134">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **PeekMessage** method.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="4fd64-135">Cambiar el contenido de Hola de un mensaje en cola</span><span class="sxs-lookup"><span data-stu-id="4fd64-135">Change hello contents of a queued message</span></span>
<span data-ttu-id="4fd64-136">Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-136">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="4fd64-137">Si el mensaje representa una tarea de trabajo, puede usar este tooupdate característica el estado de la tarea de trabajo de hello.</span><span class="sxs-lookup"><span data-stu-id="4fd64-137">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="4fd64-138">Hola siguiente código actualiza el mensaje de bienvenida de cola con nuevo contenido y conjuntos de Hola tooextend de tiempo de espera de visibilidad otro 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="4fd64-138">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="4fd64-139">Esto guarda el estado de Hola de trabajos asociados con el mensaje de bienvenida y proporciona a cliente hello otro toocontinue minuto trabajando en el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="4fd64-139">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="4fd64-140">Puede utilizar este flujos de trabajo de varios pasos de tootrack técnica sobre los mensajes en cola, sin necesidad de toostart a través de hello principio si se produce un error en un paso de procesamiento debido a un error toohardware o software.</span><span class="sxs-lookup"><span data-stu-id="4fd64-140">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="4fd64-141">Normalmente, se mantendría también un número de reintentos y si hello mensaje se vuelve a intentar más de  *n*  veces, debería eliminarla.</span><span class="sxs-lookup"><span data-stu-id="4fd64-141">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="4fd64-142">Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.</span><span class="sxs-lookup"><span data-stu-id="4fd64-142">This protects against a message that triggers an application error each time it is processed.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="4fd64-143">Eliminación de la cola mensajes de bienvenida del siguiente</span><span class="sxs-lookup"><span data-stu-id="4fd64-143">De-queue hello next message</span></span>
<span data-ttu-id="4fd64-144">El código quita un mensaje de una cola en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="4fd64-144">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="4fd64-145">Cuando se llama a **GetMessage**, obtendrá el siguiente mensaje de Hola en una cola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-145">When you call **GetMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="4fd64-146">Un mensaje devuelto de **GetMessage** se convierte en invisible tooany otro código que lee mensajes de esta cola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-146">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="4fd64-147">De forma predeterminada, este mensaje permanece invisible durante 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="4fd64-147">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="4fd64-148">toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a **DeleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="4fd64-148">toofinish removing hello message from hello queue, you must also call **DeleteMessage**.</span></span> <span data-ttu-id="4fd64-149">Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="4fd64-149">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="4fd64-150">Las llamadas de código **DeleteMessage** justo después de que se ha procesado el mensaje de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="4fd64-150">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a><span data-ttu-id="4fd64-151">Uso del patrón Async-Await con API comunes de almacenamiento de colas</span><span class="sxs-lookup"><span data-stu-id="4fd64-151">Use Async-Await pattern with common Queue storage APIs</span></span>
<span data-ttu-id="4fd64-152">Este ejemplo muestra cómo hello toouse asincrónicas Await patrón con las API de almacenamiento de cola común.</span><span class="sxs-lookup"><span data-stu-id="4fd64-152">This example shows how toouse hello Async-Await pattern with common Queue storage APIs.</span></span> <span data-ttu-id="4fd64-153">ejemplo de Hola a llama a Hola versión asincrónica de cada uno de hello tiene métodos, como se indica en hello *Async* sufijo de cada método.</span><span class="sxs-lookup"><span data-stu-id="4fd64-153">hello sample calls hello asynchronous version of each of hello given methods, as indicated by hello *Async* suffix of each method.</span></span> <span data-ttu-id="4fd64-154">Cuando se utiliza un método asincrónico, Hola async-await patrón suspende la ejecución local hasta que se complete la llamada de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-154">When an async method is used, hello async-await pattern suspends local execution until hello call completes.</span></span> <span data-ttu-id="4fd64-155">Este comportamiento permite Hola actual subproceso toodo otro trabajo, que ayuda a evitar los cuellos de botella de rendimiento y aumenta la capacidad de respuesta general de la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-155">This behavior allows hello current thread toodo other work, which helps avoid performance bottlenecks and improves hello overall responsiveness of your application.</span></span> <span data-ttu-id="4fd64-156">Para obtener más detalles sobre el uso de Hola patrón Async y Await en .NET vea [Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="4fd64-156">For more details on using hello Async-Await pattern in .NET see [Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span></span>

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="4fd64-157">Uso de opciones adicionales para quitar mensajes de la cola</span><span class="sxs-lookup"><span data-stu-id="4fd64-157">Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="4fd64-158">Hay dos formas de personalizar la recuperación de mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-158">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="4fd64-159">En primer lugar, puede obtener un lote de mensajes (arriba too32).</span><span class="sxs-lookup"><span data-stu-id="4fd64-159">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="4fd64-160">En segundo lugar, puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="4fd64-160">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="4fd64-161">siguiente Hola código de ejemplo utiliza la **GetMessages** tooget 20 mensajes de método en una llamada.</span><span class="sxs-lookup"><span data-stu-id="4fd64-161">hello following code example uses the **GetMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="4fd64-162">A continuación, procesa cada mensaje con un bucle **foreach** .</span><span class="sxs-lookup"><span data-stu-id="4fd64-162">Then it processes each message using a **foreach** loop.</span></span> <span data-ttu-id="4fd64-163">También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para cada mensaje.</span><span class="sxs-lookup"><span data-stu-id="4fd64-163">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="4fd64-164">Tenga en cuenta que Hola 5 minutos se inicia para todos los mensajes en hello mismo tiempo, por lo que tras 5 minutos transcurridos desde la llamada de hello demasiado**GetMessages**, los mensajes que no se eliminaron estará visibles de nuevo.</span><span class="sxs-lookup"><span data-stu-id="4fd64-164">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**GetMessages**, any messages which have not been deleted will become visible again.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a><span data-ttu-id="4fd64-165">Obtener la longitud de cola de Hola</span><span class="sxs-lookup"><span data-stu-id="4fd64-165">Get hello queue length</span></span>
<span data-ttu-id="4fd64-166">Puede obtener una estimación del número de Hola de mensajes en una cola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-166">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="4fd64-167">El **FetchAttributes** método pide al servicio de cola de Hola para recuperar los atributos de la cola de hello, incluido el número de mensajes de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-167">The **FetchAttributes** method asks hello Queue service to retrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="4fd64-168">Hola **ApproximateMessageCount** propiedad devuelve el valor última de hello recuperado por la **FetchAttributes** método sin llamar al servicio de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-168">hello **ApproximateMessageCount** property returns hello last value retrieved by the **FetchAttributes** method, without calling hello Queue service.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a><span data-ttu-id="4fd64-169">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="4fd64-169">Delete a queue</span></span>
<span data-ttu-id="4fd64-170">toodelete una cola y todos los mensajes de Hola contenidas en ella, llame a la **eliminar** método hello en objetos de cola.</span><span class="sxs-lookup"><span data-stu-id="4fd64-170">toodelete a queue and all hello messages contained in it, call the **Delete** method on hello queue object.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a><span data-ttu-id="4fd64-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4fd64-171">Next steps</span></span>
<span data-ttu-id="4fd64-172">Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn vínculos acerca de las tareas más complejas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="4fd64-172">Now that you've learned hello basics of Queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="4fd64-173">Ver la documentación de referencia de servicio de cola de Hola para obtener información detallada acerca de las API disponibles:</span><span class="sxs-lookup"><span data-stu-id="4fd64-173">View hello Queue service reference documentation for complete details about available APIs:</span></span>
  * [<span data-ttu-id="4fd64-174">Referencia de la biblioteca de clientes de almacenamiento para .NET</span><span class="sxs-lookup"><span data-stu-id="4fd64-174">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [<span data-ttu-id="4fd64-175">Referencia de API de REST</span><span class="sxs-lookup"><span data-stu-id="4fd64-175">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="4fd64-176">Obtenga información acerca de cómo código de hello toosimplify escribir toowork con el almacenamiento de Azure mediante el uso de hello [SDK de WebJobs de Azure](../app-service-web/websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4fd64-176">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md).</span></span>
* <span data-ttu-id="4fd64-177">Ver más características guías toolearn acerca de otras opciones para almacenar datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd64-177">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
  * <span data-ttu-id="4fd64-178">[Introducción al almacenamiento de tabla de Azure mediante .NET](storage-dotnet-how-to-use-tables.md) toostore datos estructurados.</span><span class="sxs-lookup"><span data-stu-id="4fd64-178">[Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) toostore structured data.</span></span>
  * <span data-ttu-id="4fd64-179">[Introducción al almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md) toostore datos no estructurados.</span><span class="sxs-lookup"><span data-stu-id="4fd64-179">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
  * <span data-ttu-id="4fd64-180">[Conectar tooSQL base de datos mediante el uso de .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore de datos relacionales.</span><span class="sxs-lookup"><span data-stu-id="4fd64-180">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
