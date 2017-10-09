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
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Introducción al almacenamiento de colas de Azure y a los servicios conectados de Visual Studio (proyectos de servicios en la nube)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Información general
Este artículo describe cómo tooget iniciado mediante el almacenamiento de cola de Azure en Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure en un proyecto de servicios de nube mediante Visual Studio hello **agregar servicios conectados** cuadro de diálogo .

Le mostraremos cómo toocreate una cola en el código. También le mostraremos cómo tooperform basic cola operaciones, como agregar, modificar, leer y eliminar mensajes de la cola. ejemplos de Hello están escritos en código C# y usar hello [biblioteca de cliente de almacenamiento de Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Hola **agregar servicios conectados** operación instala tooaccess de paquetes de NuGet adecuado de hello almacenamiento de Azure en el proyecto y agrega la cadena de conexión de Hola para hello cuenta de almacenamiento tooyour archivos de configuración de proyecto.

* Consulte [Introducción al Almacenamiento en cola de Azure mediante .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) para más información sobre la manipulación de colas en el código.
* Vea [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/) para información general sobre Almacenamiento de Azure.
* Vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/) para información general sobre los servicios en la nube de Azure.
* Vea [ASP.NET](http://www.asp.net) para más información sobre la programación de aplicaciones ASP.NET.

Almacenamiento de la cola de Azure es un servicio para almacenar grandes cantidades de mensajes que pueden tener acceso desde cualquier lugar Hola mundo a través de llamadas autenticadas mediante HTTP o HTTPS. Un mensaje de la cola solo puede estar too64 KB de tamaño y una cola puede contener millones de mensajes, seguridad toohello límite de capacidad total de una cuenta de almacenamiento.

## <a name="access-queues-in-code"></a>Acceso a colas en el código
las colas de tooaccess en los proyectos de servicios de nube de Visual Studio, necesita tooinclude Hola siguiente archivo de código fuente de tooany C# de elementos que tienen acceso a almacenamiento de la cola de Azure.

1. Asegúrese de incluyen declaraciones de espacios de nombres de hello en parte superior de hello del archivo hello C# estas **con** instrucciones.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento. Hola de uso después de código tooget Hola su cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de información de configuración del servicio de Azure Hola.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Obtener un **CloudQueueClient** tooreference Hola cola objetos en su cuenta de almacenamiento de objetos.  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Obtener un **CloudQueue** tooreference una cola específica del objeto.
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Nota:** los Hola encima código frente a código de hello usan en hello siguiendo los ejemplos.

## <a name="create-a-queue-in-code"></a>Creación de una cola en código
cola de hello toocreate desde el código, basta con agregar una llamada demasiado**CreateIfNotExists**.

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a>Agregar una cola de mensajes tooa
tooinsert un mensaje en una cola existente, cree un nuevo **CloudQueueMessage** objeto y, a continuación, llamada hello **AddMessage** método.

Se puede crear un objeto **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.

Este es un ejemplo que inserta el mensaje de saludo "¡Hello, World".

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a>Leer un mensaje de una cola
Puede inspeccionar mensaje hello en la parte delantera de Hola de una cola sin quitarlo de la cola de Hola por Hola que realiza la llamada **PeekMessage** método.

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a>Leer y eliminar un mensaje de una cola
Su código puede quitar un mensaje de una cola en dos pasos.

1. Llame a **GetMessage** siguiente mensaje de saludo de tooget en una cola. Un mensaje devuelto de **GetMessage** se convierte en invisible tooany otro código que lee mensajes de esta cola. De forma predeterminada, este mensaje permanece invisible durante 30 segundos.
2. toofinish quitar mensajes de bienvenida de cola de hello, llame a **DeleteMessage**.

Este proceso de dos pasos de la eliminación de un mensaje garantiza que si se produce un error en el código tooprocess que puede obtener un mensaje debido a un error toohardware o software, otra instancia del código Hola mismo mensaje y vuelva a intentarlo. Hola siguiente código llama **DeleteMessage** justo después de que se ha procesado el mensaje de bienvenida.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a>Use opciones adicionales tooprocess y quitar mensajes en cola
Hay dos formas de personalizar la recuperación de mensajes de una cola.

* Puede obtener un lote de mensajes (arriba too32).
* Puede establecer un tiempo de espera de invisibilidad mayores o menores, lo que permite el código más o menos toofully tiempo procesar cada mensaje. siguiente Hola código de ejemplo utiliza la **GetMessages** tooget 20 mensajes de método en una llamada. A continuación, procesa cada mensaje con un bucle **foreach** . También establece los minutos de toofive de tiempo de espera de invisibilidad de Hola para cada mensaje. Tenga en cuenta que Hola 5 minutos se inicia para todos los mensajes en hello mismo tiempo, por lo que tras 5 minutos transcurridos desde la llamada de hello demasiado**GetMessages**, los mensajes que no se eliminaron estará visibles de nuevo.

Este es un ejemplo:

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a>Obtener la longitud de cola de Hola
Puede obtener una estimación del número de Hola de mensajes en una cola. El **FetchAttributes** método pide al servicio de cola de Hola para recuperar los atributos de la cola de hello, incluido el número de mensajes de Hola. Hola **ApproximateMethodCount** propiedad devuelve el valor última de hello recuperado por la **FetchAttributes** método sin llamar al servicio de cola de Hola.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a>Usar hello asincrónicas Await patrón común de las API de cola de Azure
Este ejemplo muestra cómo hello toouse asincrónicas Await patrón común de las API de cola de Azure. ejemplo de Hola llama versión de async Hola de cada uno de hello tiene métodos, esto puede verse por hello **Async** posteriores a la corrección de cada método. Cuando un método asincrónico es Hola usado async-await patrón suspende la ejecución local hasta que se complete la llamada de Hola. Este comportamiento permite Hola actual subproceso toodo otro trabajo que ayuda a evitar los cuellos de botella de rendimiento y aumenta la capacidad de respuesta general de la aplicación de Hola. Para obtener más detalles sobre el uso de Hola patrón Async y Await en .NET vea [Async y Await (C# y Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

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

## <a name="delete-a-queue"></a>Eliminación de una cola
toodelete una cola y todos los mensajes de Hola contenidos en él, llamada hello **eliminar** método hello en objetos de cola.

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

