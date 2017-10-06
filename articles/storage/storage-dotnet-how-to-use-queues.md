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
# <a name="get-started-with-azure-queue-storage-using-net"></a>Introducción al Almacenamiento en cola de Azure mediante .NET
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Información general
El almacenamiento en cola de Azure proporciona mensajería en la nube entre componentes de aplicaciones. A la hora de diseñar aplicaciones para escala, los componentes de las mismas suelen desacoplarse para poder escalarlos de forma independiente. Almacenamiento de cola ofrece mensajería asincrónica para la comunicación entre componentes de aplicaciones, si se están ejecutando en la nube de hello, en el escritorio de hello, en un servidor local o en un dispositivo móvil. Además, este tipo de almacenamiento admite la administración de tareas asincrónicas y la creación de flujos de trabajo de procesos.

### <a name="about-this-tutorial"></a>Acerca de este tutorial
Este tutorial muestra cómo código toowrite .NET en algunos escenarios comunes con almacenamiento en la cola de Azure. Entre los escenarios descritos se incluyen los siguientes: creación y eliminación de colas y adición, lectura y eliminación de mensajes de la cola.

**Estimado toocomplete de tiempo:** 45 minutos

**Requisitos previos:**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Biblioteca de cliente de Almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Administrador de configuración Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Una [cuenta de almacenamiento de Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Adición de directivas using
Agregue los siguiente hello `using` parte superior de toohello de directivas de hello `Program.cs` archivo:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>Analizar la cadena de conexión de Hola
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>Crear el cliente del servicio de cola de Hola
Hola **CloudQueueClient** clase permite tooretrieve las colas almacenadas en almacenamiento de la cola. Este es el cliente del servicio de una manera toocreate hello:

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
Ahora está listo toowrite código que lee datos de y escribe datos tooQueue storage.

## <a name="create-a-queue"></a>Creación de una cola
Este ejemplo se muestra cómo toocreate una cola si aún no existe:

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

## <a name="insert-a-message-into-a-queue"></a>un mensaje en una cola
tooinsert un mensaje en una cola existente, primero debe crear un nuevo **CloudQueueMessage**. A continuación, llame a hello **AddMessage** método. Se puede crear un valor de **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de **bytes**. Este es el código que crea una cola (si no existe) y el mensaje de bienvenida de inserciones "¡Hello, World":

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

## <a name="peek-at-hello-next-message"></a>Consultar mensajes de bienvenida del siguiente
Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **PeekMessage** método.

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

## <a name="change-hello-contents-of-a-queued-message"></a>Cambiar el contenido de Hola de un mensaje en cola
Puede cambiar el contenido de Hola de un mensaje en lugar de en la cola de Hola. Si el mensaje representa una tarea de trabajo, puede usar este tooupdate característica el estado de la tarea de trabajo de hello. Hola siguiente código actualiza el mensaje de bienvenida de cola con nuevo contenido y conjuntos de Hola tooextend de tiempo de espera de visibilidad otro 60 segundos. Esto guarda el estado de Hola de trabajos asociados con el mensaje de bienvenida y proporciona a cliente hello otro toocontinue minuto trabajando en el mensaje de bienvenida. Puede utilizar este flujos de trabajo de varios pasos de tootrack técnica sobre los mensajes en cola, sin necesidad de toostart a través de hello principio si se produce un error en un paso de procesamiento debido a un error toohardware o software. Normalmente, se mantendría también un número de reintentos y si hello mensaje se vuelve a intentar más de  *n*  veces, debería eliminarla. Esto proporciona protección frente a un mensaje que produce un error en la aplicación cada vez que se procesa.

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

## <a name="de-queue-hello-next-message"></a>Eliminación de la cola mensajes de bienvenida del siguiente
El código quita un mensaje de una cola en dos pasos. Cuando se llama a **GetMessage**, obtendrá el siguiente mensaje de Hola en una cola. Un mensaje devuelto de **GetMessage** se convierte en invisible tooany otro código que lee mensajes de esta cola. De forma predeterminada, este mensaje permanece invisible durante 30 segundos. toofinish al quitar el mensaje de saludo de cola de hello, también debe llamar a **DeleteMessage**. Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo. Las llamadas de código **DeleteMessage** justo después de que se ha procesado el mensaje de bienvenida.

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

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Uso del patrón Async-Await con API comunes de almacenamiento de colas
Este ejemplo muestra cómo hello toouse asincrónicas Await patrón con las API de almacenamiento de cola común. ejemplo de Hola a llama a Hola versión asincrónica de cada uno de hello tiene métodos, como se indica en hello *Async* sufijo de cada método. Cuando se utiliza un método asincrónico, Hola async-await patrón suspende la ejecución local hasta que se complete la llamada de Hola. Este comportamiento permite Hola actual subproceso toodo otro trabajo, que ayuda a evitar los cuellos de botella de rendimiento y aumenta la capacidad de respuesta general de la aplicación de Hola. Para obtener más detalles sobre el uso de Hola patrón Async y Await en .NET vea [Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>Uso de opciones adicionales para quitar mensajes de la cola
Hay dos formas de personalizar la recuperación de mensajes de una cola.
En primer lugar, puede obtener un lote de mensajes (arriba too32). En segundo lugar, puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje. siguiente Hola código de ejemplo utiliza la **GetMessages** tooget 20 mensajes de método en una llamada. A continuación, procesa cada mensaje con un bucle **foreach** . También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para cada mensaje. Tenga en cuenta que Hola 5 minutos se inicia para todos los mensajes en hello mismo tiempo, por lo que tras 5 minutos transcurridos desde la llamada de hello demasiado**GetMessages**, los mensajes que no se eliminaron estará visibles de nuevo.

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

## <a name="get-hello-queue-length"></a>Obtener la longitud de cola de Hola
Puede obtener una estimación del número de Hola de mensajes en una cola. El **FetchAttributes** método pide al servicio de cola de Hola para recuperar los atributos de la cola de hello, incluido el número de mensajes de Hola. Hola **ApproximateMessageCount** propiedad devuelve el valor última de hello recuperado por la **FetchAttributes** método sin llamar al servicio de cola de Hola.

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

## <a name="delete-a-queue"></a>Eliminación de una cola
toodelete una cola y todos los mensajes de Hola contenidas en ella, llame a la **eliminar** método hello en objetos de cola.

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
    

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de la cola, siga estos toolearn vínculos acerca de las tareas más complejas de almacenamiento.

* Ver la documentación de referencia de servicio de cola de Hola para obtener información detallada acerca de las API disponibles:
  * [Referencia de la biblioteca de clientes de almacenamiento para .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [Referencia de API de REST](http://msdn.microsoft.com/library/azure/dd179355)
* Obtenga información acerca de cómo código de hello toosimplify escribir toowork con el almacenamiento de Azure mediante el uso de hello [SDK de WebJobs de Azure](../app-service-web/websites-dotnet-webjobs-sdk.md).
* Ver más características guías toolearn acerca de otras opciones para almacenar datos en Azure.
  * [Introducción al almacenamiento de tabla de Azure mediante .NET](storage-dotnet-how-to-use-tables.md) toostore datos estructurados.
  * [Introducción al almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md) toostore datos no estructurados.
  * [Conectar tooSQL base de datos mediante el uso de .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore de datos relacionales.

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
