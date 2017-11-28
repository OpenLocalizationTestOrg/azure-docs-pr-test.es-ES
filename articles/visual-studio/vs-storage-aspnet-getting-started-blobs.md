---
title: aaaGet a trabajar con el almacenamiento de blobs de Azure y servicios conectados de Visual Studio (ASP.NET) | Documentos de Microsoft
description: "Cómo tooget iniciado mediante el almacenamiento de blobs de Azure en un proyecto de ASP.NET en Visual Studio después de conectar la cuenta de almacenamiento de tooa con servicios conectados de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraig
ms.openlocfilehash: 7b3e160da5bb95967ca4650b124afb8e867c03d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="9e73e-103">Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="9e73e-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="9e73e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9e73e-104">Overview</span></span>

<span data-ttu-id="9e73e-105">Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="9e73e-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="9e73e-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9e73e-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="9e73e-107">Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="9e73e-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="9e73e-108">Este tutorial muestra cómo código toowrite ASP.NET en algunos escenarios comunes con almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e73e-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="9e73e-109">Los escenarios incluyen la creación de un contenedor de blob y la carga, enumeración, descarga y eliminación de blobs.</span><span class="sxs-lookup"><span data-stu-id="9e73e-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="9e73e-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9e73e-110">Prerequisites</span></span>

* [<span data-ttu-id="9e73e-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e73e-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="9e73e-112">Cuenta de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="9e73e-112">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="9e73e-113">Creación de un controlador MVC</span><span class="sxs-lookup"><span data-stu-id="9e73e-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="9e73e-114">Hola **el Explorador de soluciones**, haga clic en **controladores**y, en el menú contextual de hello, seleccione **Agregar -> controlador**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Agregar una aplicación de ASP.NET MVC tooan de controlador](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="9e73e-116">En hello **agregar scaffolding** cuadro de diálogo, seleccione **controlador de MVC 5 - vacío**y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especifique el tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="9e73e-118">En hello **Agregar controlador** cuadro de diálogo, nombre del controlador que hello *BlobsController*y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![Controlador de MVC Hola de nombre](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="9e73e-120">Agregue los siguiente hello *con* toohello directivas `BlobsController.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="9e73e-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="9e73e-121">Creación de un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="9e73e-121">Create a blob container</span></span>

<span data-ttu-id="9e73e-122">Un contenedor de blob es una jerarquía anidada de blobs y carpetas.</span><span class="sxs-lookup"><span data-stu-id="9e73e-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="9e73e-123">Hello siguientes pasos muestran cómo toocreate un contenedor de blobs:</span><span class="sxs-lookup"><span data-stu-id="9e73e-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="9e73e-124">Hello código en esta sección se da por supuesto que ha completado los pasos de hello en la sección de hello, [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="9e73e-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="9e73e-125">Abra hello `BlobsController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="9e73e-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="9e73e-126">Agregue un método llamado **CreateBlobContainer** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="9e73e-127">Dentro de hello **CreateBlobContainer** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9e73e-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9e73e-128">Usar hello siguientes código tooget Hola almacenamiento conexión cadena y almacenamiento de información de la cuenta de configuración de servicio de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="9e73e-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="9e73e-129">(Cambiar  *&lt;nombre de cuenta de almacenamiento >* toohello nombre de cuenta de almacenamiento de Azure que está obteniendo acceso hello.)</span><span class="sxs-lookup"><span data-stu-id="9e73e-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="9e73e-130">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de blob.</span><span class="sxs-lookup"><span data-stu-id="9e73e-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="9e73e-131">Obtener un **CloudBlobContainer** objeto que representa un nombre de contenedor de blobs que se prefiera de toohello de referencia.</span><span class="sxs-lookup"><span data-stu-id="9e73e-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="9e73e-132">Hola **CloudBlobClient.GetContainerReference** método no hace una solicitud en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="9e73e-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="9e73e-133">referencia de Hola se devuelve si existe el contenedor de blobs de Hola o no.</span><span class="sxs-lookup"><span data-stu-id="9e73e-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="9e73e-134">Llamar a hello **CloudBlobContainer.CreateIfNotExists** contenedor de hello toocreate del método si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="9e73e-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="9e73e-135">Hola **CloudBlobContainer.CreateIfNotExists** método **true** si Hola contenedor no existe y se haya creado correctamente.</span><span class="sxs-lookup"><span data-stu-id="9e73e-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="9e73e-136">En caso contrario, se devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="9e73e-137">Hola de actualización **ViewBag** con el nombre de Hola Hola del contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="9e73e-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="9e73e-138">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **Blobs**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="9e73e-139">En hello **agregar vista** cuadro de diálogo, escriba **CreateBlobContainer** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="9e73e-140">Abra `CreateBlobContainer.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="9e73e-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="9e73e-141">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9e73e-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="9e73e-142">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="9e73e-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="9e73e-143">Ejecute la aplicación hello y seleccione **crear contenedor de blobs** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="9e73e-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![Creación de un contenedor de blobs](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="9e73e-145">Como se mencionó anteriormente, Hola **CloudBlobContainer.CreateIfNotExists** método **true** sólo cuando el contenedor de hello no existe y se crea.</span><span class="sxs-lookup"><span data-stu-id="9e73e-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="9e73e-146">Por lo tanto, si ejecuta la aplicación hello cuando existe el contenedor de hello, método hello devuelve **false**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="9e73e-147">aplicación de hello toorun varias veces, debe eliminar contenedor Hola antes de ejecutar la aplicación hello nuevo.</span><span class="sxs-lookup"><span data-stu-id="9e73e-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="9e73e-148">Eliminar contenedor Hola puede hacerse a través de hello **CloudBlobContainer.Delete** método.</span><span class="sxs-lookup"><span data-stu-id="9e73e-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="9e73e-149">También puede eliminar el contenedor de hello mediante hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="9e73e-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="9e73e-150">Carga de un blob en un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="9e73e-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="9e73e-151">Una vez que haya [creado un contenedor de blobs](#create-a-blob-container), puede cargar archivos en ese contenedor.</span><span class="sxs-lookup"><span data-stu-id="9e73e-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="9e73e-152">Esta sección explica cómo cargar un contenedor de blobs de tooa de archivos local.</span><span class="sxs-lookup"><span data-stu-id="9e73e-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="9e73e-153">pasos de Hello supone que ha creado un contenedor de blobs denominado *contenedor de blobs de prueba*.</span><span class="sxs-lookup"><span data-stu-id="9e73e-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="9e73e-154">Hello código en esta sección se da por supuesto que ha completado los pasos de hello en la sección de hello, [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="9e73e-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="9e73e-155">Abra hello `BlobsController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="9e73e-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="9e73e-156">Agregue un método llamado **UploadBlob** que devuelve un **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="9e73e-157">Dentro de hello **UploadBlob** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9e73e-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9e73e-158">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="9e73e-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="9e73e-159">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de blob.</span><span class="sxs-lookup"><span data-stu-id="9e73e-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="9e73e-160">Obtener un **CloudBlobContainer** objeto que representa un nombre de contenedor de blob de referencia toohello.</span><span class="sxs-lookup"><span data-stu-id="9e73e-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="9e73e-161">Como se explicó anteriormente, el almacenamiento de Azure es compatible con diferentes tipos de blob.</span><span class="sxs-lookup"><span data-stu-id="9e73e-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="9e73e-162">tooretrieve un blob de página de referencia tooa, llamada hello **CloudBlobContainer.GetPageBlobReference** método.</span><span class="sxs-lookup"><span data-stu-id="9e73e-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="9e73e-163">tooretrieve un blob en bloques referencia tooa, llamada hello **CloudBlobContainer.GetBlockBlobReference** método.</span><span class="sxs-lookup"><span data-stu-id="9e73e-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="9e73e-164">Por lo general, blob en bloques es hello recomendada toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="9e73e-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="9e73e-165">(Cambie < nombre de blob > * nombre toohello desea blob de hello toogive una vez cargado.)</span><span class="sxs-lookup"><span data-stu-id="9e73e-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="9e73e-166">Una vez que tenga una referencia de blob, puede cargar cualquier tooit de flujo de datos mediante una llamada del objeto de referencia de hello blob **UploadFromStream** método.</span><span class="sxs-lookup"><span data-stu-id="9e73e-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="9e73e-167">Hola **UploadFromStream** método crea blob Hola si no existe, o lo sobrescribe si existe.</span><span class="sxs-lookup"><span data-stu-id="9e73e-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="9e73e-168">(Cambiar  *&lt;carga de archivos >* tooa completo archivo toohello de ruta de acceso que desee tooupload.)</span><span class="sxs-lookup"><span data-stu-id="9e73e-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="9e73e-169">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **Blobs**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="9e73e-170">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9e73e-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="9e73e-171">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="9e73e-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="9e73e-172">Ejecute la aplicación hello y seleccione **cargar blob**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="9e73e-173">Hola sección - [enumerar blobs hello en un contenedor de blobs](#list-the-blobs-in-a-blob-container) -ilustra cómo hello toolist blobs en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="9e73e-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="9e73e-174">Enumerar los blobs de hello en un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="9e73e-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="9e73e-175">Esta sección muestra cómo hello toolist blobs en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="9e73e-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="9e73e-176">hace referencia a código de ejemplo de Hola Hola *contenedor de blobs de prueba* creado en la sección de hello, [crear un contenedor de blobs](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="9e73e-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="9e73e-177">Hello código en esta sección se da por supuesto que ha completado los pasos de hello en la sección de hello, [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="9e73e-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="9e73e-178">Abra hello `BlobsController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="9e73e-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="9e73e-179">Agregue un método llamado **ListBlobs** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="9e73e-180">Dentro de hello **ListBlobs** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9e73e-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9e73e-181">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="9e73e-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="9e73e-182">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de blob.</span><span class="sxs-lookup"><span data-stu-id="9e73e-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="9e73e-183">Obtener un **CloudBlobContainer** objeto que representa un nombre de contenedor de blob de referencia toohello.</span><span class="sxs-lookup"><span data-stu-id="9e73e-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="9e73e-184">los blobs de hello toolist en un contenedor de blobs, usar hello **CloudBlobContainer.ListBlobs** método.</span><span class="sxs-lookup"><span data-stu-id="9e73e-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="9e73e-185">Hola **CloudBlobContainer.ListBlobs** método devuelve un **IListBlobItem** objeto conversiones tooa **CloudBlockBlob**, **CloudPageBlob**, o **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="9e73e-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="9e73e-186">Hello fragmento de código siguiente enumera todos los blobs de hello en un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="9e73e-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="9e73e-187">Cada blob es convertir toohello adecuado un objeto según su tipo y su nombre (o URI en caso de hello de un **CloudBlobDirectory**) se agrega la lista de tooa.</span><span class="sxs-lookup"><span data-stu-id="9e73e-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    <span data-ttu-id="9e73e-188">En suma tooblobs, contenedores de blobs pueden contener directorios.</span><span class="sxs-lookup"><span data-stu-id="9e73e-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="9e73e-189">Supongamos que tiene un contenedor de blob denominado *contenedor de blobs de prueba* con hello después de la jerarquía:</span><span class="sxs-lookup"><span data-stu-id="9e73e-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="9e73e-190">Con hello anterior ejemplo de código, Hola **blobs** lista de cadenas contiene la siguiente toohello similar de valores:</span><span class="sxs-lookup"><span data-stu-id="9e73e-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="9e73e-191">Como puede ver, lista de hello incluye Hola solo entidades nivel superior; Hola no anidarlos (*bar.png* y *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="9e73e-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="9e73e-192">toolist todos Hola entidades dentro de un contenedor de blob, debe llamar a hello **CloudBlobContainer.ListBlobs** método y pase **true** para hello **useFlatBlobListing** parámetro.</span><span class="sxs-lookup"><span data-stu-id="9e73e-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="9e73e-193">Hola configuración **useFlatBlobListing** parámetro demasiado**true** devuelve una lista plana de todas las entidades en el contenedor de blobs de Hola y produce Hola siguientes resultados:</span><span class="sxs-lookup"><span data-stu-id="9e73e-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="9e73e-194">Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **Blobs**y en el menú contextual de hello, seleccione **Agregar -> vista**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="9e73e-195">En hello **agregar vista** cuadro de diálogo, escriba **ListBlobs** de nombre de la vista de Hola y seleccione **agregar**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="9e73e-196">Abra `ListBlobs.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:</span><span class="sxs-lookup"><span data-stu-id="9e73e-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. <span data-ttu-id="9e73e-197">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9e73e-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="9e73e-198">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="9e73e-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="9e73e-199">Ejecute la aplicación hello y seleccione **enumerar blobs** toosee resultados similar toohello siguiente captura de pantalla:</span><span class="sxs-lookup"><span data-stu-id="9e73e-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![Lista de blobs](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="9e73e-201">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="9e73e-201">Download blobs</span></span>

<span data-ttu-id="9e73e-202">Esta sección muestra cómo toodownload un blob y, o bien hacer persistente toolocal almacenamiento o lectura Hola contenido en una cadena.</span><span class="sxs-lookup"><span data-stu-id="9e73e-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="9e73e-203">hace referencia a código de ejemplo de Hola Hola *contenedor de blobs de prueba* creado en la sección de hello, [crear un contenedor de blobs](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="9e73e-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="9e73e-204">Abra hello `BlobsController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="9e73e-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="9e73e-205">Agregue un método llamado **DownloadBlob** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="9e73e-206">Dentro de hello **DownloadBlob** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9e73e-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9e73e-207">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="9e73e-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="9e73e-208">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de blob.</span><span class="sxs-lookup"><span data-stu-id="9e73e-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="9e73e-209">Obtener un **CloudBlobContainer** objeto que representa un nombre de contenedor de blob de referencia toohello.</span><span class="sxs-lookup"><span data-stu-id="9e73e-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="9e73e-210">Obtenga un objeto de referencia de blob mediante una llamada al método **CloudBlobContainer.GetBlockBlobReference** o **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="9e73e-211">(Cambiar  *&lt;nombre del blob >* toohello nombre de blob de Hola que se va a descargar.)</span><span class="sxs-lookup"><span data-stu-id="9e73e-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="9e73e-212">toodownload un blob, use hello **CloudBlockBlob.DownloadToStream** o **CloudPageBlob.DownloadToStream** método, según el tipo de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="9e73e-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="9e73e-213">Hello fragmento de código siguiente utiliza hello **CloudBlockBlob.DownloadToStream** tootransfer método objeto de secuencia de tooa de contenido de un blob que conserva, a continuación, tooa de archivo local: (cambio  *&lt;nombre de archivo local >* toohello completo de nombre de archivo que representa donde desea blob Hola descargó.)</span><span class="sxs-lookup"><span data-stu-id="9e73e-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="9e73e-214">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9e73e-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="9e73e-215">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="9e73e-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="9e73e-216">Ejecute la aplicación hello y seleccione **descarga blob** blob de hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="9e73e-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="9e73e-217">blob de Hello especificado en hello **CloudBlobContainer.GetBlockBlobReference** llamada al método descarga ubicación toohello especificar Hola **File.OpenWrite** llamada al método.</span><span class="sxs-lookup"><span data-stu-id="9e73e-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="9e73e-218">Eliminar blobs</span><span class="sxs-lookup"><span data-stu-id="9e73e-218">Delete blobs</span></span>

<span data-ttu-id="9e73e-219">Hello siguientes pasos muestran cómo toodelete un blob:</span><span class="sxs-lookup"><span data-stu-id="9e73e-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="9e73e-220">Hello código en esta sección se da por supuesto que ha completado los pasos de hello en la sección de hello, [configurar el entorno de desarrollo de hello](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="9e73e-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="9e73e-221">Abra hello `BlobsController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="9e73e-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="9e73e-222">Agregue un método llamado **DeleteBlob** que devuelve un **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="9e73e-223">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9e73e-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9e73e-224">Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)</span><span class="sxs-lookup"><span data-stu-id="9e73e-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="9e73e-225">Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de blob.</span><span class="sxs-lookup"><span data-stu-id="9e73e-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="9e73e-226">Obtener un **CloudBlobContainer** objeto que representa un nombre de contenedor de blob de referencia toohello.</span><span class="sxs-lookup"><span data-stu-id="9e73e-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="9e73e-227">Obtenga un objeto de referencia de blob mediante una llamada al método **CloudBlobContainer.GetBlockBlobReference** o **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="9e73e-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="9e73e-228">(Cambiar  *&lt;nombre del blob >* toohello nombre de blob de Hola que va a eliminar.)</span><span class="sxs-lookup"><span data-stu-id="9e73e-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="9e73e-229">Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="9e73e-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="9e73e-230">Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="9e73e-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="9e73e-231">Ejecute la aplicación hello y seleccione **Delete blob** blob de hello toodelete especificado en hello **CloudBlobContainer.GetBlockBlobReference** llamada al método.</span><span class="sxs-lookup"><span data-stu-id="9e73e-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9e73e-232">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9e73e-232">Next steps</span></span>
<span data-ttu-id="9e73e-233">Ver más características guías toolearn acerca de otras opciones para almacenar datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="9e73e-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="9e73e-234">Introducción a Azure Table Storage y a Servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="9e73e-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="9e73e-235">Introducción a Azure Queue Storage y a Servicios conectados de Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="9e73e-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](vs-storage-aspnet-getting-started-queues.md)
