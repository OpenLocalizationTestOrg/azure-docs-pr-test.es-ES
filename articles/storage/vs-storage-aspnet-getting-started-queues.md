---
title: aaaGet a trabajar con almacenamiento de cola de Azure y servicios conectados de Visual Studio (ASP.NET) | Documentos de Microsoft
description: "Cómo tooget iniciado mediante el almacenamiento de cola de Azure en un proyecto de ASP.NET en Visual Studio después de conectar la cuenta de almacenamiento de tooa con servicios conectados de Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: tarcher
ms.openlocfilehash: a9d6ecb1e8d61d75f59658d0ea3fa63d26fd7354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>Introducción a Azure Queue Storage y a Servicios conectados de Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Información general

Azure Queue Storage proporciona mensajería en la nube entre componentes de aplicaciones. A la hora de diseñar aplicaciones para escala, los componentes de las mismas suelen desacoplarse para poder escalarlos de forma independiente. Almacenamiento de cola ofrece mensajería asincrónica para la comunicación entre componentes de aplicaciones, si se están ejecutando en la nube de hello, en el escritorio de hello, en un servidor local o en un dispositivo móvil. Además, este tipo de almacenamiento admite la administración de tareas asincrónicas y la creación de flujos de trabajo de procesos.

Este tutorial muestra cómo código toowrite ASP.NET en algunos escenarios comunes con las entidades de almacenamiento de cola de Azure. Estos escenarios incluyen tareas comunes como crear una cola de Azure y agregar, modificar, leer y eliminar mensajes de la cola.

##<a name="prerequisites"></a>Requisitos previos

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Cuenta de Azure Storage](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Creación de un controlador MVC 

1. Hola **el Explorador de soluciones**, haga clic en **controladores**y, en el menú contextual de hello, seleccione **Agregar -> controlador**.

    ![Agregar una aplicación de ASP.NET MVC tooan de controlador](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. En hello **agregar scaffolding** cuadro de diálogo, seleccione **controlador de MVC 5 - vacío**y seleccione **agregar**.

    ![Especifique el tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. En hello **Agregar controlador** cuadro de diálogo, nombre del controlador que hello *QueuesController*y seleccione **agregar**.

    ![Controlador de MVC Hola de nombre](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. Agregue los siguiente hello *con* toohello directivas `QueuesController.cs` archivo:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>Creación de una cola

Hello siguientes pasos muestran cómo toocreate una cola:

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `QueuesController.cs` archivo. 

1. Agregue un método llamado **CreateQueue** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de hello **CreateQueue** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. Obtener un **CloudQueue** objeto que representa un nombre de referencia toohello cola deseada. Hola **CloudQueueClient.GetQueueReference** método no hace una solicitud en el almacenamiento de la cola. referencia de Hola se devuelve si existe la cola de Hola o no. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Llamar a hello **CloudQueue.CreateIfNotExists** cola de hello toocreate del método si aún no existe. Hola **CloudQueue.CreateIfNotExists** método **true** si Hola cola no existe y se haya creado correctamente. En caso contrario, se devuelve **false**.    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. Hola de actualización **ViewBag** por nombre de Hola de cola de Hola.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **CreateQueue** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `CreateQueue.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. Ejecute la aplicación hello y seleccione **Crear cola** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![Crear cola](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    Tal y como se mencionó anteriormente, Hola **CloudQueue.CreateIfNotExists** método **true** sólo cuando la cola de hello no existe y se crea. Por lo tanto, si ejecuta la aplicación hello cuando existe la cola de hello, método hello devuelve **false**. aplicación de hello toorun varias veces, debe eliminar Hola cola antes de ejecutar la aplicación hello nuevo. Eliminar cola Hola puede hacerse a través de hello **CloudQueue.Delete** método. También puede eliminar la cola de hello utilizando hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-a-message-tooa-queue"></a>Agregar una cola de mensajes tooa

Una vez que se haya [crea una cola](#create-a-queue), puede agregar la cola de mensajes toothat. En esta sección se explica cómo agregar una cola de mensajes de tooa *cola de prueba*. 

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `QueuesController.cs` archivo.

1. Agregue un método llamado **AddMessage** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de hello **AddMessage** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obtener un **CloudQueueContainer** objeto que representa una cola de toohello de referencia. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Crear hello **CloudQueueMessage** objeto que representa el mensaje de bienvenida de la que desee tooadd toohello cola. Se puede crear un objeto **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. Llamar a hello **CloudQueue.AddMessage** cola de mensaje toohello de método tooadd Hola.

    ```csharp
    queue.AddMessage(message);
    ```

1. Crear y establecer un par de **ViewBag** propiedades para su presentación en la vista de Hola.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **AddMessage** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `AddMessage.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. Ejecute la aplicación hello y seleccione **Agregar mensaje** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![Agregar mensaje](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

Hola dos secciones - [leer un mensaje de una cola sin eliminarlo](#read-a-message-from-a-queue-without-removing-it) y [lectura y quitar un mensaje de una cola](#read-and-remove-a-message-from-a-queue) -ilustran cómo tooread mensajes desde una cola.  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>Lectura de un mensaje de una cola sin eliminarlo

Esta sección se muestra cómo toopeek en un mensaje en cola (lectura Hola primer mensaje sin eliminarlo).  

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `QueuesController.cs` archivo.

1. Agregue un método llamado **PeekMessage** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de hello **PeekMessage** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obtener un **CloudQueueContainer** objeto que representa una cola de toohello de referencia. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Llamar a hello **CloudQueue.PeekMessage** método tooread Hola primer mensaje Hola cola sin quitarlo de la cola de Hola. 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. Hola de actualización **ViewBag** con dos valores: nombre de la cola de Hola y mensaje de saludo que se ha leído. Hola **CloudQueueMessage** objeto expone dos propiedades para obtener el valor del objeto de hello: **CloudQueueMessage.AsBytes** y **CloudQueueMessage.AsString**. **AsString** (que se usa en este ejemplo) devuelve una cadena, mientras que **AsBytes** devuelve una matriz de bytes.

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **PeekMessage** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `PeekMessage.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. Ejecute la aplicación hello y seleccione **Peek message** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![Inspeccionar mensaje](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>Lectura y eliminación de un mensaje de una cola

En esta sección, aprenderá cómo tooread y quitar un mensaje de una cola.   

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `QueuesController.cs` archivo.

1. Agregue un método llamado **ReadMessage** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de hello **ReadMessage** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obtener un **CloudQueueContainer** objeto que representa una cola de toohello de referencia. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Llamar a hello **CloudQueue.GetMessage** método tooread Hola primer mensaje Hola cola. Hola **CloudQueue.GetMessage** método realiza Hola otro código leer los mensajes para que puedan modificar o eliminar el mensaje de Hola durante el procesamiento de ningún otro código de mensaje invisible para tooany de 30 segundos (de forma predeterminada). cantidad de hello toochange de mensaje de saludo de tiempo es invisible, modifique hello **visibilityTimeout** parámetro que se pasa toohello **CloudQueue.GetMessage** método.

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. Llamar a hello **CloudQueueMessage.Delete** mensaje de saludo de método toodelete de cola de Hola.

    ```csharp
    queue.DeleteMessage(message);
    ```

1. Hola de actualización **ViewBag** con hello mensaje eliminado y Hola nombre de cola de Hola.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **ReadMessage** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `ReadMessage.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. Ejecute la aplicación hello y seleccione **mensaje de lectura y eliminación** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![Leer y eliminar mensaje](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>Obtener la longitud de cola de Hola

Esta sección muestra cómo tooget Hola longitud de cola (número de mensajes). 

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `QueuesController.cs` archivo.

1. Agregue un método llamado **GetQueueLength** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de hello **ReadMessage** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obtener un **CloudQueueContainer** objeto que representa una cola de toohello de referencia. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Llamar a hello **CloudQueue.FetchAttributes** atributos de la cola de método tooretrieve Hola (incluida su longitud). 

    ```csharp
    queue.FetchAttributes();
    ```

6. Hola acceso **CloudQueue.ApproximateMessageCount** longitud de la cola de propiedad tooget Hola.
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. Hola de actualización **ViewBag** por nombre de Hola de cola de Hola y su longitud.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **GetQueueLength** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `GetQueueLengthMessage.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. Ejecute la aplicación hello y seleccione **obtener la longitud de cola** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![longitud de la cola](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>Eliminación de una cola
Esta sección se muestra cómo toodelete una cola. 

> [!NOTE]
> 
> En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `QueuesController.cs` archivo.

1. Agregue un método llamado **DeleteQueue** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de hello **DeleteQueue** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obtener un **CloudQueueContainer** objeto que representa una cola de toohello de referencia. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Llamar a hello **CloudQueue.Delete** cola de hello toodelete método representado por hello **CloudQueue** objeto.

    ```csharp
    queue.Delete();
    ```

1. Hola de actualización **ViewBag** por nombre de Hola de cola de Hola y su longitud.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **DeleteQueue** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `DeleteQueue.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. Ejecute la aplicación hello y seleccione **obtener la longitud de cola** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![Eliminar cola](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>Pasos siguientes
Ver más características guías toolearn acerca de otras opciones para almacenar datos en Azure.

  * [Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET)](./vs-storage-aspnet-getting-started-blobs.md)
  * [Introducción a Azure Table Storage y a Servicios conectados de Visual Studio (ASP.NET)](./vs-storage-aspnet-getting-started-tables.md)
