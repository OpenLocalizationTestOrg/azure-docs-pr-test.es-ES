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
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="0bf7d-103">Introducción a Azure Queue Storage y a Servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="0bf7d-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="0bf7d-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0bf7d-104">Overview</span></span>

<span data-ttu-id="0bf7d-105">Azure Queue Storage proporciona mensajería en la nube entre componentes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="0bf7d-106">A la hora de diseñar aplicaciones para escala, los componentes de las mismas suelen desacoplarse para poder escalarlos de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="0bf7d-107">Almacenamiento de cola ofrece mensajería asincrónica para la comunicación entre componentes de aplicaciones, si se están ejecutando en la nube de hello, en el escritorio de hello, en un servidor local o en un dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="0bf7d-108">Además, este tipo de almacenamiento admite la administración de tareas asincrónicas y la creación de flujos de trabajo de procesos.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="0bf7d-109">Este tutorial muestra cómo código toowrite ASP.NET en algunos escenarios comunes con las entidades de almacenamiento de cola de Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="0bf7d-110">Estos escenarios incluyen tareas comunes como crear una cola de Azure y agregar, modificar, leer y eliminar mensajes de la cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="0bf7d-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0bf7d-111">Prerequisites</span></span>

* [<span data-ttu-id="0bf7d-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0bf7d-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="0bf7d-113">Cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0bf7d-113">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="0bf7d-114">Creación de un controlador MVC</span><span class="sxs-lookup"><span data-stu-id="0bf7d-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="0bf7d-115">Hola **el Explorador de soluciones**, haga clic en **controladores**y, en el menú contextual de hello, seleccione **Agregar -> controlador**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Agregar una aplicación de ASP.NET MVC tooan de controlador](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="0bf7d-117">En hello **agregar scaffolding** cuadro de diálogo, seleccione **controlador de MVC 5 - vacío**y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especifique el tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="0bf7d-119">En hello **Agregar controlador** cuadro de diálogo, nombre del controlador que hello *QueuesController*y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![Controlador de MVC Hola de nombre](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="0bf7d-121">Agregue los siguiente hello *con* toohello directivas `QueuesController.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="0bf7d-122">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="0bf7d-122">Create a queue</span></span>

<span data-ttu-id="0bf7d-123">Hello siguientes pasos muestran cómo toocreate una cola:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="0bf7d-124">En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="0bf7d-125">Abra hello `QueuesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="0bf7d-126">Agregue un método llamado **CreateQueue** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="0bf7d-127">Dentro de hello **CreateQueue** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="0bf7d-128">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="0bf7d-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="0bf7d-129">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="0bf7d-130">Obtener un **CloudQueue** objeto que representa un nombre de referencia toohello cola deseada.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="0bf7d-131">Hola **CloudQueueClient.GetQueueReference** método no hace una solicitud en el almacenamiento de la cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="0bf7d-132">referencia de Hola se devuelve si existe la cola de Hola o no.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="0bf7d-133">Llamar a hello **CloudQueue.CreateIfNotExists** cola de hello toocreate del método si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="0bf7d-134">Hola **CloudQueue.CreateIfNotExists** método **true** si Hola cola no existe y se haya creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="0bf7d-135">En caso contrario, se devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="0bf7d-136">Hola de actualización **ViewBag** por nombre de Hola de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="0bf7d-137">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="0bf7d-138">En hello **agregar vista** cuadro de diálogo, escriba **CreateQueue** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="0bf7d-139">Abra `CreateQueue.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="0bf7d-140">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="0bf7d-141">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="0bf7d-142">Ejecute la aplicación hello y seleccione **Crear cola** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![Crear cola](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="0bf7d-144">Tal y como se mencionó anteriormente, Hola **CloudQueue.CreateIfNotExists** método **true** sólo cuando la cola de hello no existe y se crea.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="0bf7d-145">Por lo tanto, si ejecuta la aplicación hello cuando existe la cola de hello, método hello devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="0bf7d-146">aplicación de hello toorun varias veces, debe eliminar Hola cola antes de ejecutar la aplicación hello nuevo.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="0bf7d-147">Eliminar cola Hola puede hacerse a través de hello **CloudQueue.Delete** método.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="0bf7d-148">También puede eliminar la cola de hello utilizando hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="0bf7d-149">Agregar una cola de mensajes tooa</span><span class="sxs-lookup"><span data-stu-id="0bf7d-149">Add a message tooa queue</span></span>

<span data-ttu-id="0bf7d-150">Una vez que se haya [crea una cola](#create-a-queue), puede agregar la cola de mensajes toothat.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="0bf7d-151">En esta sección se explica cómo agregar una cola de mensajes de tooa *cola de prueba*.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="0bf7d-152">En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="0bf7d-153">Abra hello `QueuesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="0bf7d-154">Agregue un método llamado **AddMessage** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="0bf7d-155">Dentro de hello **AddMessage** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="0bf7d-156">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="0bf7d-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="0bf7d-157">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="0bf7d-158">Obtener un **CloudQueueContainer** objeto que representa una cola de toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="0bf7d-159">Crear hello **CloudQueueMessage** objeto que representa el mensaje de bienvenida de la que desee tooadd toohello cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="0bf7d-160">Se puede crear un objeto **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="0bf7d-161">Llamar a hello **CloudQueue.AddMessage** cola de mensaje toohello de método tooadd Hola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="0bf7d-162">Crear y establecer un par de **ViewBag** propiedades para su presentación en la vista de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="0bf7d-163">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="0bf7d-164">En hello **agregar vista** cuadro de diálogo, escriba **AddMessage** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="0bf7d-165">Abra `AddMessage.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="0bf7d-166">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="0bf7d-167">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="0bf7d-168">Ejecute la aplicación hello y seleccione **Agregar mensaje** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![Agregar mensaje](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="0bf7d-170">Hola dos secciones - [leer un mensaje de una cola sin eliminarlo](#read-a-message-from-a-queue-without-removing-it) y [lectura y quitar un mensaje de una cola](#read-and-remove-a-message-from-a-queue) -ilustran cómo tooread mensajes desde una cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="0bf7d-171">Lectura de un mensaje de una cola sin eliminarlo</span><span class="sxs-lookup"><span data-stu-id="0bf7d-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="0bf7d-172">Esta sección se muestra cómo toopeek en un mensaje en cola (lectura Hola primer mensaje sin eliminarlo).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="0bf7d-173">En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="0bf7d-174">Abra hello `QueuesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="0bf7d-175">Agregue un método llamado **PeekMessage** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="0bf7d-176">Dentro de hello **PeekMessage** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="0bf7d-177">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="0bf7d-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="0bf7d-178">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="0bf7d-179">Obtener un **CloudQueueContainer** objeto que representa una cola de toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="0bf7d-180">Llamar a hello **CloudQueue.PeekMessage** método tooread Hola primer mensaje Hola cola sin quitarlo de la cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="0bf7d-181">Hola de actualización **ViewBag** con dos valores: nombre de la cola de Hola y mensaje de saludo que se ha leído.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="0bf7d-182">Hola **CloudQueueMessage** objeto expone dos propiedades para obtener el valor del objeto de hello: **CloudQueueMessage.AsBytes** y **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="0bf7d-183">**AsString** (que se usa en este ejemplo) devuelve una cadena, mientras que **AsBytes** devuelve una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="0bf7d-184">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="0bf7d-185">En hello **agregar vista** cuadro de diálogo, escriba **PeekMessage** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="0bf7d-186">Abra `PeekMessage.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="0bf7d-187">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="0bf7d-188">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="0bf7d-189">Ejecute la aplicación hello y seleccione **Peek message** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![Inspeccionar mensaje](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="0bf7d-191">Lectura y eliminación de un mensaje de una cola</span><span class="sxs-lookup"><span data-stu-id="0bf7d-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="0bf7d-192">En esta sección, aprenderá cómo tooread y quitar un mensaje de una cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="0bf7d-193">En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="0bf7d-194">Abra hello `QueuesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="0bf7d-195">Agregue un método llamado **ReadMessage** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="0bf7d-196">Dentro de hello **ReadMessage** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="0bf7d-197">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="0bf7d-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="0bf7d-198">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="0bf7d-199">Obtener un **CloudQueueContainer** objeto que representa una cola de toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="0bf7d-200">Llamar a hello **CloudQueue.GetMessage** método tooread Hola primer mensaje Hola cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="0bf7d-201">Hola **CloudQueue.GetMessage** método realiza Hola otro código leer los mensajes para que puedan modificar o eliminar el mensaje de Hola durante el procesamiento de ningún otro código de mensaje invisible para tooany de 30 segundos (de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="0bf7d-202">cantidad de hello toochange de mensaje de saludo de tiempo es invisible, modifique hello **visibilityTimeout** parámetro que se pasa toohello **CloudQueue.GetMessage** método.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="0bf7d-203">Llamar a hello **CloudQueueMessage.Delete** mensaje de saludo de método toodelete de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="0bf7d-204">Hola de actualización **ViewBag** con hello mensaje eliminado y Hola nombre de cola de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="0bf7d-205">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="0bf7d-206">En hello **agregar vista** cuadro de diálogo, escriba **ReadMessage** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="0bf7d-207">Abra `ReadMessage.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

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

1. <span data-ttu-id="0bf7d-208">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="0bf7d-209">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="0bf7d-210">Ejecute la aplicación hello y seleccione **mensaje de lectura y eliminación** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![Leer y eliminar mensaje](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="0bf7d-212">Obtener la longitud de cola de Hola</span><span class="sxs-lookup"><span data-stu-id="0bf7d-212">Get hello queue length</span></span>

<span data-ttu-id="0bf7d-213">Esta sección muestra cómo tooget Hola longitud de cola (número de mensajes).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="0bf7d-214">En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="0bf7d-215">Abra hello `QueuesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="0bf7d-216">Agregue un método llamado **GetQueueLength** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="0bf7d-217">Dentro de hello **ReadMessage** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="0bf7d-218">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="0bf7d-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="0bf7d-219">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="0bf7d-220">Obtener un **CloudQueueContainer** objeto que representa una cola de toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="0bf7d-221">Llamar a hello **CloudQueue.FetchAttributes** atributos de la cola de método tooretrieve Hola (incluida su longitud).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="0bf7d-222">Hola acceso **CloudQueue.ApproximateMessageCount** longitud de la cola de propiedad tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="0bf7d-223">Hola de actualización **ViewBag** por nombre de Hola de cola de Hola y su longitud.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="0bf7d-224">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="0bf7d-225">En hello **agregar vista** cuadro de diálogo, escriba **GetQueueLength** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="0bf7d-226">Abra `GetQueueLengthMessage.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="0bf7d-227">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="0bf7d-228">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="0bf7d-229">Ejecute la aplicación hello y seleccione **obtener la longitud de cola** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![longitud de la cola](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="0bf7d-231">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="0bf7d-231">Delete a queue</span></span>
<span data-ttu-id="0bf7d-232">Esta sección se muestra cómo toodelete una cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="0bf7d-233">En esta sección se da por supuesto que ha completado los pasos de hello [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="0bf7d-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="0bf7d-234">Abra hello `QueuesController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="0bf7d-235">Agregue un método llamado **DeleteQueue** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="0bf7d-236">Dentro de hello **DeleteQueue** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="0bf7d-237">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="0bf7d-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="0bf7d-238">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="0bf7d-239">Obtener un **CloudQueueContainer** objeto que representa una cola de toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="0bf7d-240">Llamar a hello **CloudQueue.Delete** cola de hello toodelete método representado por hello **CloudQueue** objeto.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="0bf7d-241">Hola de actualización **ViewBag** por nombre de Hola de cola de Hola y su longitud.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="0bf7d-242">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **colas**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="0bf7d-243">En hello **agregar vista** cuadro de diálogo, escriba **DeleteQueue** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="0bf7d-244">Abra `DeleteQueue.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="0bf7d-245">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="0bf7d-246">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="0bf7d-247">Ejecute la aplicación hello y seleccione **obtener la longitud de cola** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="0bf7d-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Eliminar cola](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="0bf7d-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0bf7d-249">Next steps</span></span>
<span data-ttu-id="0bf7d-250">Ver más características guías toolearn acerca de otras opciones para almacenar datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="0bf7d-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="0bf7d-251">Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="0bf7d-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="0bf7d-252">Introducción a Azure Table Storage y a Servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="0bf7d-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
