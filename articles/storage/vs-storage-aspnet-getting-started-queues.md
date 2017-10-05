---
title: "Introducción a Azure Queue Storage y a Servicios conectados de Visual Studio (ASP.NET) | Microsoft Docs"
description: "Cómo empezar a usar Azure Queue Storage en un proyecto ASP.NET en Visual Studio después de conectarse a una cuenta de almacenamiento mediante Servicios conectados de Visual Studio"
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
ms.openlocfilehash: 76b0d5e270e16a317ce8a7b424c06c867b537a8e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="99e1e-103">Introducción a Azure Queue Storage y a Servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="99e1e-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="99e1e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="99e1e-104">Overview</span></span>

<span data-ttu-id="99e1e-105">Azure Queue Storage proporciona mensajería en la nube entre componentes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="99e1e-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="99e1e-106">A la hora de diseñar aplicaciones para escala, los componentes de las mismas suelen desacoplarse para poder escalarlos de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="99e1e-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="99e1e-107">El almacenamiento en cola ofrece mensajería asincrónica para la comunicación entre los componentes de las aplicaciones, independientemente de si se ejecutan en la nube, en el escritorio, en un servidor local o en un dispositivo móvil.</span><span class="sxs-lookup"><span data-stu-id="99e1e-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="99e1e-108">Además, este tipo de almacenamiento admite la administración de tareas asincrónicas y la creación de flujos de trabajo de procesos.</span><span class="sxs-lookup"><span data-stu-id="99e1e-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="99e1e-109">Este tutorial muestra cómo escribir código ASP.NET para algunos escenarios comunes mediante entidades de Azure Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="99e1e-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="99e1e-110">Estos escenarios incluyen tareas comunes como crear una cola de Azure y agregar, modificar, leer y eliminar mensajes de la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="99e1e-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="99e1e-111">Prerequisites</span></span>

* [<span data-ttu-id="99e1e-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99e1e-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="99e1e-113">Cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="99e1e-113">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="99e1e-114">Creación de un controlador MVC</span><span class="sxs-lookup"><span data-stu-id="99e1e-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="99e1e-115">En el **Explorador de soluciones**, haga clic con el botón derecho en **Controladores** y, en el menú contextual, seleccione **Agregar > Controlador**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Incorporación de un controlador a una aplicación de ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="99e1e-117">En el cuadro de diálogo **Agregar scaffold**, seleccione **Controlador MVC 5 - Vacío** y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especifique el tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="99e1e-119">En el cuadro de diálogo **Agregar controlador**, denomine *QueuesController* al controlador y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span></span>

    ![Asignación de nombre al controladorMVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="99e1e-121">Agregue las siguientes directivas *using* al archivo `QueuesController.cs`:</span><span class="sxs-lookup"><span data-stu-id="99e1e-121">Add the following *using* directives to the `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="99e1e-122">Creación de una cola</span><span class="sxs-lookup"><span data-stu-id="99e1e-122">Create a queue</span></span>

<span data-ttu-id="99e1e-123">Los siguientes pasos muestran cómo crear una cola:</span><span class="sxs-lookup"><span data-stu-id="99e1e-123">The following steps illustrate how to create a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="99e1e-124">En esta sección se da por supuesto que ha completado los pasos de [Configuración del entorno de desarrollo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="99e1e-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="99e1e-125">Abra el archivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="99e1e-125">Open the `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="99e1e-126">Agregue un método llamado **CreateQueue** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="99e1e-127">Dentro del método **CreateQueue**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="99e1e-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="99e1e-128">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="99e1e-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="99e1e-129">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="99e1e-130">Obtenga un objeto **CloudQueue** que representa una referencia al nombre de cola que desea.</span><span class="sxs-lookup"><span data-stu-id="99e1e-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span></span> <span data-ttu-id="99e1e-131">El método **CloudQueueClient.GetQueueReference** no hace ninguna solicitud en el almacenamiento de la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="99e1e-132">Se devuelve la referencia tanto si la cola existe como si no.</span><span class="sxs-lookup"><span data-stu-id="99e1e-132">The reference is returned whether or not the queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="99e1e-133">Llame a la **CloudQueue.CreateIfNotExists** método para crear la cola si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="99e1e-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span></span> <span data-ttu-id="99e1e-134">El método **CloudQueue.CreateIfNotExists** devuelve **true** si la cola no existe y se ha creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="99e1e-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span></span> <span data-ttu-id="99e1e-135">En caso contrario, se devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="99e1e-136">Actualice **ViewBag** con el nombre de la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-136">Update the **ViewBag** with the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="99e1e-137">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Colas** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="99e1e-138">En el cuadro de diálogo **Agregar vista**, escriba **CreateQueue** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="99e1e-139">Abra `CreateQueue.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="99e1e-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="99e1e-140">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="99e1e-141">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="99e1e-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="99e1e-142">Ejecute la aplicación y seleccione **Crear cola** para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="99e1e-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span></span>
  
    ![Crear cola](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="99e1e-144">Como se dijo anteriormente, el método **CloudQueue.CreateIfNotExists** devuelve **true** solo si la cola no existía pero se creó.</span><span class="sxs-lookup"><span data-stu-id="99e1e-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span></span> <span data-ttu-id="99e1e-145">Por lo tanto, si se ejecuta la aplicación cuando la cola existe, el método devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span></span> <span data-ttu-id="99e1e-146">Para ejecutar la aplicación varias veces, debe eliminar la cola antes de ejecutar la aplicación de nuevo.</span><span class="sxs-lookup"><span data-stu-id="99e1e-146">To run the app multiple times, you must delete the queue before running the app again.</span></span> <span data-ttu-id="99e1e-147">La eliminación de la cola puede realizarse a través del método **CloudQueue.Delete**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span></span> <span data-ttu-id="99e1e-148">También puede eliminar la cola mediante [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) o [el Explorador de Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="99e1e-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="99e1e-149">un mensaje a una cola</span><span class="sxs-lookup"><span data-stu-id="99e1e-149">Add a message to a queue</span></span>

<span data-ttu-id="99e1e-150">Una vez que se haya [creado una cola](#create-a-queue), puede agregar mensajes a dicha cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span></span> <span data-ttu-id="99e1e-151">En esta sección se explica cómo agregar un mensaje a una cola *test-queue*.</span><span class="sxs-lookup"><span data-stu-id="99e1e-151">This section walks you through adding a message to a queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="99e1e-152">Se da por supuesto que ha completado los pasos de [Configuración del entorno de desarrollo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="99e1e-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="99e1e-153">Abra el archivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="99e1e-153">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="99e1e-154">Agregue un método llamado **AddMessage** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="99e1e-155">Dentro del método **AddMessage**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="99e1e-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="99e1e-156">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="99e1e-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="99e1e-157">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="99e1e-158">Obtenga un objeto **CloudQueueContainer** que representa una referencia a la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="99e1e-159">Cree el objeto **CloudQueueMessage** que representa el mensaje que desea agregar a la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span></span> <span data-ttu-id="99e1e-160">Se puede crear un objeto **CloudQueueMessage** a partir de una cadena (en formato UTF-8) o de una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="99e1e-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="99e1e-161">Llame al método **CloudQueue.AddMessage** para agregar el mensaje a la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="99e1e-162">Cree y configure un par de propiedades **ViewBag** para su presentación en la vista.</span><span class="sxs-lookup"><span data-stu-id="99e1e-162">Create and set a couple of **ViewBag** properties for display in the view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="99e1e-163">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Colas** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="99e1e-164">En el cuadro de diálogo **Agregar vista**, escriba **AddMessage** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="99e1e-165">Abra `AddMessage.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="99e1e-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    The message '@ViewBag.Message' was added to the queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="99e1e-166">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="99e1e-167">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="99e1e-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="99e1e-168">Ejecute la aplicación y seleccione **Agregar mensaje** para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="99e1e-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span></span>
  
    ![Agregar mensaje](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="99e1e-170">Las dos secciones —[Lectura de un mensaje de una cola sin eliminarlo](#read-a-message-from-a-queue-without-removing-it) y [Lectura y eliminación de un mensaje de una cola](#read-and-remove-a-message-from-a-queue)— muestran cómo leer los mensajes de una cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span></span>    

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="99e1e-171">Lectura de un mensaje de una cola sin eliminarlo</span><span class="sxs-lookup"><span data-stu-id="99e1e-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="99e1e-172">En esta sección se muestra cómo inspeccionar un mensaje en cola (leer el primer mensaje sin eliminarlo).</span><span class="sxs-lookup"><span data-stu-id="99e1e-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="99e1e-173">Se da por supuesto que ha completado los pasos de [Configuración del entorno de desarrollo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="99e1e-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="99e1e-174">Abra el archivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="99e1e-174">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="99e1e-175">Agregue un método llamado **PeekMessage** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="99e1e-176">Dentro del método **PeekMessage**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="99e1e-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="99e1e-177">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="99e1e-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="99e1e-178">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="99e1e-179">Obtenga un objeto **CloudQueueContainer** que representa una referencia a la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="99e1e-180">Llame al método **CloudQueue.PeekMessage** para leer el primer mensaje de la cola sin quitarlo de ella.</span><span class="sxs-lookup"><span data-stu-id="99e1e-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="99e1e-181">Actualice **ViewBag** con dos valores: el nombre de la cola y el mensaje que se ha leído.</span><span class="sxs-lookup"><span data-stu-id="99e1e-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span></span> <span data-ttu-id="99e1e-182">El objeto **CloudQueueMessage** expone dos propiedades para obtener el valor del objeto: **CloudQueueMessage.AsBytes** y **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="99e1e-183">**AsString** (que se usa en este ejemplo) devuelve una cadena, mientras que **AsBytes** devuelve una matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="99e1e-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="99e1e-184">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Colas** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="99e1e-185">En el cuadro de diálogo **Agregar vista**, escriba **PeekMessage** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="99e1e-186">Abra `PeekMessage.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="99e1e-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="99e1e-187">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="99e1e-188">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="99e1e-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="99e1e-189">Ejecute la aplicación y seleccione **Inspeccionar mensaje** para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="99e1e-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span></span>
  
    ![Inspeccionar mensaje](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="99e1e-191">Lectura y eliminación de un mensaje de una cola</span><span class="sxs-lookup"><span data-stu-id="99e1e-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="99e1e-192">En esta sección, aprenderá a leer y eliminar un mensaje de una cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-192">In this section, you learn how to read and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="99e1e-193">Se da por supuesto que ha completado los pasos de [Configuración del entorno de desarrollo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="99e1e-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="99e1e-194">Abra el archivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="99e1e-194">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="99e1e-195">Agregue un método llamado **ReadMessage** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="99e1e-196">Dentro del método **ReadMessage**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="99e1e-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="99e1e-197">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="99e1e-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="99e1e-198">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="99e1e-199">Obtenga un objeto **CloudQueueContainer** que representa una referencia a la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="99e1e-200">Llame al método **CloudQueue.GetMessage** para leer el primer mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span></span> <span data-ttu-id="99e1e-201">El método **CloudQueue.GetMessage** hace que el mensaje sea invisible durante 30 segundos (de forma predeterminada) para cualquier otro código que lea mensajes de forma que ningún otro código pueda modificar o eliminar el mensaje mientras lo procesa.</span><span class="sxs-lookup"><span data-stu-id="99e1e-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span></span> <span data-ttu-id="99e1e-202">Para cambiar la cantidad de tiempo que el mensaje es invisible, modifique el parámetro **visibilityTimeout** que se pasa al método **CloudQueue.GetMessage**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible to other code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="99e1e-203">Llame al método **CloudQueueMessage.Delete** para eliminar el mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="99e1e-204">Actualice **ViewBag** con el mensaje eliminado y el nombre de la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="99e1e-205">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Colas** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="99e1e-206">En el cuadro de diálogo **Agregar vista**, escriba **ReadMessage** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="99e1e-207">Abra `ReadMessage.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="99e1e-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="99e1e-208">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="99e1e-209">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="99e1e-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="99e1e-210">Ejecute la aplicación y seleccione **Read/Delete message** (Leer/eliminar mensaje) para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="99e1e-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span></span>
  
    ![Leer y eliminar mensaje](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-the-queue-length"></a><span data-ttu-id="99e1e-212">la longitud de la cola</span><span class="sxs-lookup"><span data-stu-id="99e1e-212">Get the queue length</span></span>

<span data-ttu-id="99e1e-213">En esta sección se muestra cómo obtener la longitud de cola (número de mensajes).</span><span class="sxs-lookup"><span data-stu-id="99e1e-213">This section illustrates how to get the queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="99e1e-214">Se da por supuesto que ha completado los pasos de [Configuración del entorno de desarrollo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="99e1e-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="99e1e-215">Abra el archivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="99e1e-215">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="99e1e-216">Agregue un método llamado **GetQueueLength** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="99e1e-217">Dentro del método **ReadMessage**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="99e1e-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="99e1e-218">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="99e1e-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="99e1e-219">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="99e1e-220">Obtenga un objeto **CloudQueueContainer** que representa una referencia a la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="99e1e-221">Llame al método **CloudQueue.FetchAttributes** para recuperar los atributos de la cola (incluida su longitud).</span><span class="sxs-lookup"><span data-stu-id="99e1e-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="99e1e-222">Acceda a la propiedad **CloudQueue.ApproximateMessageCount** para obtener la longitud de la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="99e1e-223">Actualice **ViewBag** con el nombre de la cola y su longitud.</span><span class="sxs-lookup"><span data-stu-id="99e1e-223">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="99e1e-224">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Colas** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="99e1e-225">En el cuadro de diálogo **Agregar vista**, escriba **GetQueueLength** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="99e1e-226">Abra `GetQueueLengthMessage.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="99e1e-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    The queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="99e1e-227">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="99e1e-228">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="99e1e-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="99e1e-229">Ejecute la aplicación y seleccione **Get queue length** (Obtener la longitud de cola) para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="99e1e-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![longitud de la cola](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="99e1e-231">Eliminación de una cola</span><span class="sxs-lookup"><span data-stu-id="99e1e-231">Delete a queue</span></span>
<span data-ttu-id="99e1e-232">En esta sección se muestra cómo eliminar una cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-232">This section illustrates how to delete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="99e1e-233">Se da por supuesto que ha completado los pasos de [Configuración del entorno de desarrollo](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="99e1e-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="99e1e-234">Abra el archivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="99e1e-234">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="99e1e-235">Agregue un método llamado **DeleteQueue** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="99e1e-236">Dentro del método **DeleteQueue**, obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="99e1e-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="99e1e-237">Utilice el código siguiente para obtener la información de cuenta de almacenamiento y la cadena de conexión de almacenamiento de la configuración del servicio de Azure: (cambie *&lt;storage-account-name>*  por el nombre de la cuenta de Azure Storage a la que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="99e1e-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="99e1e-238">Obtenga un objeto **CloudQueueClient** que representa un cliente de servicio de cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="99e1e-239">Obtenga un objeto **CloudQueueContainer** que representa una referencia a la cola.</span><span class="sxs-lookup"><span data-stu-id="99e1e-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="99e1e-240">Llame al método **CloudQueue.Delete** para eliminar la cola representada por el objeto **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="99e1e-241">Actualice **ViewBag** con el nombre de la cola y su longitud.</span><span class="sxs-lookup"><span data-stu-id="99e1e-241">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="99e1e-242">En el **Explorador de soluciones**, expanda la carpeta **Vistas**, haga clic con el botón derecho en **Colas** y, en el menú contextual, seleccione **Agregar > Vista**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="99e1e-243">En el cuadro de diálogo **Agregar vista**, escriba **DeleteQueue** como nombre de vista y seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="99e1e-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="99e1e-244">Abra `DeleteQueue.cshtml` y modifíquelo de modo que se parezca al siguiente fragmento de código:</span><span class="sxs-lookup"><span data-stu-id="99e1e-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="99e1e-245">En el **Explorador de soluciones**, expanda la carpeta **Vistas->Compartido** y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="99e1e-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="99e1e-246">Después del último **Html.ActionLink**, agregue el siguiente **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="99e1e-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="99e1e-247">Ejecute la aplicación y seleccione **Get queue length** (Obtener la longitud de cola) para ver resultados similares a la siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="99e1e-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Eliminar cola](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="99e1e-249">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="99e1e-249">Next steps</span></span>
<span data-ttu-id="99e1e-250">Consulte más guías de características para obtener información acerca de otras opciones del almacenamiento de datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="99e1e-250">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="99e1e-251">Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="99e1e-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="99e1e-252">Introducción a Azure Table Storage y a Servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="99e1e-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
