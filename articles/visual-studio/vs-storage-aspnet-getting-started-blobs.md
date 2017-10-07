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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Información general

Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs. El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación. Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.

Este tutorial muestra cómo código toowrite ASP.NET en algunos escenarios comunes con almacenamiento de blobs de Azure. Los escenarios incluyen la creación de un contenedor de blob y la carga, enumeración, descarga y eliminación de blobs.

##<a name="prerequisites"></a>Requisitos previos

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Cuenta de Azure Storage](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Creación de un controlador MVC 

1. Hola **el Explorador de soluciones**, haga clic en **controladores**y, en el menú contextual de hello, seleccione **Agregar -> controlador**.

    ![Agregar una aplicación de ASP.NET MVC tooan de controlador](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. En hello **agregar scaffolding** cuadro de diálogo, seleccione **controlador de MVC 5 - vacío**y seleccione **agregar**.

    ![Especifique el tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. En hello **Agregar controlador** cuadro de diálogo, nombre del controlador que hello *BlobsController*y seleccione **agregar**.

    ![Controlador de MVC Hola de nombre](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. Agregue los siguiente hello *con* toohello directivas `BlobsController.cs` archivo:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>Creación de un contenedor de blobs

Un contenedor de blob es una jerarquía anidada de blobs y carpetas. Hello siguientes pasos muestran cómo toocreate un contenedor de blobs:

> [!NOTE]
> 
> Hello código en esta sección se da por supuesto que ha completado los pasos de hello en la sección de hello, [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `BlobsController.cs` archivo.

1. Agregue un método llamado **CreateBlobContainer** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de hello **CreateBlobContainer** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Usar hello siguientes código tooget Hola almacenamiento conexión cadena y almacenamiento de información de la cuenta de configuración de servicio de Azure Hola. (Cambiar  *&lt;nombre de cuenta de almacenamiento >* toohello nombre de cuenta de almacenamiento de Azure que está obteniendo acceso hello.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obtener un **CloudBlobContainer** objeto que representa un nombre de contenedor de blobs que se prefiera de toohello de referencia. Hola **CloudBlobClient.GetContainerReference** método no hace una solicitud en el almacenamiento de blobs. referencia de Hola se devuelve si existe el contenedor de blobs de Hola o no. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Llamar a hello **CloudBlobContainer.CreateIfNotExists** contenedor de hello toocreate del método si aún no existe. Hola **CloudBlobContainer.CreateIfNotExists** método **true** si Hola contenedor no existe y se haya creado correctamente. En caso contrario, se devuelve **false**.    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. Hola de actualización **ViewBag** con el nombre de Hola Hola del contenedor de blobs.

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **Blobs**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **CreateBlobContainer** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `CreateBlobContainer.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. Ejecute la aplicación hello y seleccione **crear contenedor de blobs** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![Creación de un contenedor de blobs](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    Como se mencionó anteriormente, Hola **CloudBlobContainer.CreateIfNotExists** método **true** sólo cuando el contenedor de hello no existe y se crea. Por lo tanto, si ejecuta la aplicación hello cuando existe el contenedor de hello, método hello devuelve **false**. aplicación de hello toorun varias veces, debe eliminar contenedor Hola antes de ejecutar la aplicación hello nuevo. Eliminar contenedor Hola puede hacerse a través de hello **CloudBlobContainer.Delete** método. También puede eliminar el contenedor de hello mediante hello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) o hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="upload-a-blob-into-a-blob-container"></a>Carga de un blob en un contenedor de blobs

Una vez que haya [creado un contenedor de blobs](#create-a-blob-container), puede cargar archivos en ese contenedor. Esta sección explica cómo cargar un contenedor de blobs de tooa de archivos local. pasos de Hello supone que ha creado un contenedor de blobs denominado *contenedor de blobs de prueba*. 

> [!NOTE]
> 
> Hello código en esta sección se da por supuesto que ha completado los pasos de hello en la sección de hello, [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `BlobsController.cs` archivo.

1. Agregue un método llamado **UploadBlob** que devuelve un **EmptyResult**.

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Dentro de hello **UploadBlob** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obtener un **CloudBlobContainer** objeto que representa un nombre de contenedor de blob de referencia toohello. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Como se explicó anteriormente, el almacenamiento de Azure es compatible con diferentes tipos de blob. tooretrieve un blob de página de referencia tooa, llamada hello **CloudBlobContainer.GetPageBlobReference** método. tooretrieve un blob en bloques referencia tooa, llamada hello **CloudBlobContainer.GetBlockBlobReference** método. Por lo general, blob en bloques es hello recomendada toouse de tipo. (Cambie < nombre de blob > * nombre toohello desea blob de hello toogive una vez cargado.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Una vez que tenga una referencia de blob, puede cargar cualquier tooit de flujo de datos mediante una llamada del objeto de referencia de hello blob **UploadFromStream** método. Hola **UploadFromStream** método crea blob Hola si no existe, o lo sobrescribe si existe. (Cambiar  *&lt;carga de archivos >* tooa completo archivo toohello de ruta de acceso que desee tooupload.)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **Blobs**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. Ejecute la aplicación hello y seleccione **cargar blob**.  
  
Hola sección - [enumerar blobs hello en un contenedor de blobs](#list-the-blobs-in-a-blob-container) -ilustra cómo hello toolist blobs en un contenedor de blobs.  

## <a name="list-hello-blobs-in-a-blob-container"></a>Enumerar los blobs de hello en un contenedor de blobs

Esta sección muestra cómo hello toolist blobs en un contenedor de blobs. hace referencia a código de ejemplo de Hola Hola *contenedor de blobs de prueba* creado en la sección de hello, [crear un contenedor de blobs](#create-a-blob-container).

> [!NOTE]
> 
> Hello código en esta sección se da por supuesto que ha completado los pasos de hello en la sección de hello, [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `BlobsController.cs` archivo.

1. Agregue un método llamado **ListBlobs** que devuelve un **ActionResult**.

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de hello **ListBlobs** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obtener un **CloudBlobContainer** objeto que representa un nombre de contenedor de blob de referencia toohello. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. los blobs de hello toolist en un contenedor de blobs, usar hello **CloudBlobContainer.ListBlobs** método. Hola **CloudBlobContainer.ListBlobs** método devuelve un **IListBlobItem** objeto conversiones tooa **CloudBlockBlob**, **CloudPageBlob**, o **CloudBlobDirectory** objeto. Hello fragmento de código siguiente enumera todos los blobs de hello en un contenedor de blobs. Cada blob es convertir toohello adecuado un objeto según su tipo y su nombre (o URI en caso de hello de un **CloudBlobDirectory**) se agrega la lista de tooa.

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

    En suma tooblobs, contenedores de blobs pueden contener directorios. Supongamos que tiene un contenedor de blob denominado *contenedor de blobs de prueba* con hello después de la jerarquía:

        foo.png
        dir1/bar.png
        dir2/baz.png

    Con hello anterior ejemplo de código, Hola **blobs** lista de cadenas contiene la siguiente toohello similar de valores:

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    Como puede ver, lista de hello incluye Hola solo entidades nivel superior; Hola no anidarlos (*bar.png* y *baz.png*). toolist todos Hola entidades dentro de un contenedor de blob, debe llamar a hello **CloudBlobContainer.ListBlobs** método y pase **true** para hello **useFlatBlobListing** parámetro.    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    Hola configuración **useFlatBlobListing** parámetro demasiado**true** devuelve una lista plana de todas las entidades en el contenedor de blobs de Hola y produce Hola siguientes resultados:

        foo.png
        dir1/bar.png
        dir2/baz.png

1. Hola **el Explorador de soluciones**, expanda hello **vistas** carpeta, haga clic en **Blobs**y en el menú contextual de hello, seleccione **Agregar -> vista**.

1. En hello **agregar vista** cuadro de diálogo, escriba **ListBlobs** de nombre de la vista de Hola y seleccione **agregar**.

1. Abra `ListBlobs.cshtml`y modifíquelo para que se parezca al siguiente fragmento de código de hello:

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

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. Ejecute la aplicación hello y seleccione **enumerar blobs** toosee resultados similar toohello siguiente captura de pantalla:
  
    ![Lista de blobs](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>Descargar blobs

Esta sección muestra cómo toodownload un blob y, o bien hacer persistente toolocal almacenamiento o lectura Hola contenido en una cadena. hace referencia a código de ejemplo de Hola Hola *contenedor de blobs de prueba* creado en la sección de hello, [crear un contenedor de blobs](#create-a-blob-container).

1. Abra hello `BlobsController.cs` archivo.

1. Agregue un método llamado **DownloadBlob** que devuelve un **ActionResult**.

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Dentro de hello **DownloadBlob** método, obtener una **CloudStorageAccount** objeto que representa la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obtener un **CloudBlobContainer** objeto que representa un nombre de contenedor de blob de referencia toohello. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Obtenga un objeto de referencia de blob mediante una llamada al método **CloudBlobContainer.GetBlockBlobReference** o **CloudBlobContainer.GetPageBlobReference**. (Cambiar  *&lt;nombre del blob >* toohello nombre de blob de Hola que se va a descargar.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. toodownload un blob, use hello **CloudBlockBlob.DownloadToStream** o **CloudPageBlob.DownloadToStream** método, según el tipo de blob de Hola. Hello fragmento de código siguiente utiliza hello **CloudBlockBlob.DownloadToStream** tootransfer método objeto de secuencia de tooa de contenido de un blob que conserva, a continuación, tooa de archivo local: (cambio  *&lt;nombre de archivo local >* toohello completo de nombre de archivo que representa donde desea blob Hola descargó.) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. Ejecute la aplicación hello y seleccione **descarga blob** blob de hello toodownload. blob de Hello especificado en hello **CloudBlobContainer.GetBlockBlobReference** llamada al método descarga ubicación toohello especificar Hola **File.OpenWrite** llamada al método. 

## <a name="delete-blobs"></a>Eliminar blobs

Hello siguientes pasos muestran cómo toodelete un blob:

> [!NOTE]
> 
> Hello código en esta sección se da por supuesto que ha completado los pasos de hello en la sección de hello, [configurar el entorno de desarrollo de hello](#set-up-the-development-environment). 

1. Abra hello `BlobsController.cs` archivo.

1. Agregue un método llamado **DeleteBlob** que devuelve un **ActionResult**.

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento. Siguiente de Hola de uso de código tooget Hola almacenamiento cadena y almacenamiento cuenta información de conexión de configuración de servicio de Azure de hello: (cambio  *&lt;nombre de cuenta de almacenamiento >* toohello nombre del programa Hola a almacenamiento de Azure cuenta de que está obteniendo acceso.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenga un objeto **CloudTableClient** que representa un cliente de servicio de blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obtener un **CloudBlobContainer** objeto que representa un nombre de contenedor de blob de referencia toohello. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Obtenga un objeto de referencia de blob mediante una llamada al método **CloudBlobContainer.GetBlockBlobReference** o **CloudBlobContainer.GetPageBlobReference**. (Cambiar  *&lt;nombre del blob >* toohello nombre de blob de Hola que va a eliminar.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. Hola **el Explorador de soluciones**, expanda hello **vistas -> Shared** carpeta y abra `_Layout.cshtml`.

1. Después de hello última **Html.ActionLink**, agregue los siguientes hello **Html.ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. Ejecute la aplicación hello y seleccione **Delete blob** blob de hello toodelete especificado en hello **CloudBlobContainer.GetBlockBlobReference** llamada al método. 

## <a name="next-steps"></a>Pasos siguientes
Ver más características guías toolearn acerca de otras opciones para almacenar datos en Azure.

  * [Introducción a Azure Table Storage y a Servicios conectados de Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
  * [Introducción a Azure Queue Storage y a Servicios conectados de Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-queues.md)
