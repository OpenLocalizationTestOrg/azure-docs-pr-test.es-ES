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
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a>Introducción a Queue Storage y a los servicios conectados de Visual Studio (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Información general
Este artículo describe cómo tooget iniciado mediante el almacenamiento de cola de Azure en Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure en un proyecto de ASP.NET Core mediante Visual Studio hello **agregar servicios conectados** cuadro de diálogo. Hola **agregar servicios conectados** operación instala tooaccess de paquetes de NuGet adecuado de hello almacenamiento de Azure en el proyecto y agrega la cadena de conexión de Hola para hello cuenta de almacenamiento tooyour archivos de configuración de proyecto.

Almacenamiento de cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS. Un mensaje de la cola solo puede estar too64 kilobytes (KB) de tamaño y una cola puede contener millones de mensajes, seguridad toohello límite de capacidad total de una cuenta de almacenamiento.

tooget iniciado, primero debe toocreate una cola de Azure en su cuenta de almacenamiento. Le mostraremos cómo toocreate una cola en el código. También le mostraremos cómo tooperform basic cola operaciones, como agregar, modificar, leer y eliminar mensajes de la cola. Hola ejemplos están escritos en C\# código y utilizar Hola biblioteca de cliente de almacenamiento de Azure para. NET. Para obtener más información acerca de ASP.NET, consulte [ASP.NET](http://www.asp.net).

**Nota:** algunas de las API que realizan llamadas tooAzure almacenamiento en ASP.NET Core Hola son asincrónicas. Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información. código de Hello siguiente se da por supuesto que se usan métodos de programación asincrónica.

* Consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](storage-dotnet-how-to-use-queues.md) para más información sobre la manipulación de colas mediante programación.
* Vea [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/) para información general sobre Almacenamiento de Azure.
* Vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/) para información general sobre los servicios en la nube de Azure.
* Vea [ASP.NET](http://www.asp.net) para más información sobre la programación de aplicaciones ASP.NET.

## <a name="access-queues-in-code"></a>Acceso a colas en el código
colas de tooaccess de proyectos de ASP.NET Core, necesita tooinclude Hola siguiente archivo de código fuente de tooany C# de elementos que tiene acceso a almacenamiento de cola de Azure.

1. Asegúrese de incluyen declaraciones de espacios de nombres de hello en parte superior de hello del archivo hello C# estas **con** instrucciones.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento. Hola de uso después de código tooget Hola su cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de información de configuración del servicio de Azure Hola.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Obtener un **CloudQueueClient** tooreference Hola cola objetos en su cuenta de almacenamiento de objetos.  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Obtener un **CloudQueue** tooreference una cola específica del objeto.
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Nota:** los Hola encima código frente a código de hello usan en hello siguiendo los ejemplos.

### <a name="create-a-queue-in-code"></a>Creación de una cola en código
Hola toocreate cola de Azure en el código, basta con agregar una llamada demasiado**CreateIfNotExistsAsync**.

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a>Agregar una cola de mensajes tooa
tooinsert un mensaje en una cola existente, cree un nuevo **CloudQueueMessage** objeto y, a continuación, llamada hello **AddMessageAsync** método.

Se puede crear un objeto **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.

Este es un ejemplo que inserta el mensaje de saludo "¡Hello, World".

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a>Leer un mensaje de una cola
Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **PeekMessageAsync** método.

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a>Leer y eliminar un mensaje de una cola
Su código puede quitar un mensaje de una cola en dos pasos.

1. Llame a **GetMessageAsync** siguiente mensaje de saludo de tooget en una cola. Un mensaje devuelto de **GetMessageAsync** se convierte en invisible tooany otro código que lee mensajes de esta cola. De forma predeterminada, este mensaje permanece invisible durante 30 segundos.
2. toofinish quitar mensajes de bienvenida de cola de hello, llame a **DeleteMessageAsync**.

Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo. Hola siguiente código llama **DeleteMessageAsync** justo después de que se ha procesado el mensaje de bienvenida.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a>las opciones adicionales de los mensajes quitados de la cola
Hay dos formas de personalizar la recuperación de mensajes de una cola.
En primer lugar, puede obtener un lote de mensajes (arriba too32). En segundo lugar, puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje. siguiente Hola código de ejemplo utiliza la **GetMessages** tooget 20 mensajes de método en una llamada. A continuación, procesa cada mensaje con un bucle **foreach** . También establece los minutos de too5 de tiempo de espera de invisibilidad de Hola para cada mensaje. Tenga en cuenta que inicio de 5 minutos de Hola para todos los mensajes en hello mismo tiempo, por lo que tras 5 minutos transcurridos tras la llamada de hello demasiado**GetMessages**, los mensajes que no se eliminaron vuelven a ser visibles.

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a>Obtener la longitud de cola de Hola
Puede obtener una estimación del número de Hola de mensajes en una cola. El **FetchAttributes** método pide al servicio de cola de Hola para recuperar los atributos de la cola de hello, incluido el número de mensajes de Hola. Hola **ApproximateMethodCount** propiedad devuelve el valor última de hello recuperado por la **FetchAttributes** método sin llamar al servicio de cola de Hola.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a>Usar el patrón de hello asincrónicas Await con las API de cola común
Este ejemplo muestra cómo toouse Hola asincrónicas Await patrón con las API de cola común. versión de async de Hola Hola ejemplo llamadas de cada uno de hello tiene métodos. Esto puede verse por revisión posterior a la de hello asincrónico de cada método. Cuando se utiliza un método asincrónico, el patrón de Async y Await Hola suspende la ejecución local hasta que se complete la llamada de Hola. Este comportamiento permite Hola actual subproceso toodo otro trabajo que ayuda a evitar los cuellos de botella de rendimiento y aumenta la capacidad de respuesta general de la aplicación de Hola. Para obtener más detalles sobre el uso de hello patrón Async y Await en. NET, consulte [Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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
## <a name="delete-a-queue"></a>Eliminación de una cola
toodelete una cola y todos los mensajes de Hola contenidas en ella, llame a la **eliminar** método hello en objetos de cola.

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

