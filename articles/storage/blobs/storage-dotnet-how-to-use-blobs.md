---
title: aaaGet a trabajar con el almacenamiento de blobs de Azure (almacenamiento de objetos) mediante .NET | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 3df0cf14b69d85cdc2f62cc3c8b901be102fa026
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a><span data-ttu-id="09e0f-103">Introducción al Almacenamiento de blobs de Azure mediante .NET</span><span class="sxs-lookup"><span data-stu-id="09e0f-103">Get started with Azure Blob storage using .NET</span></span>

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

<span data-ttu-id="09e0f-104">Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="09e0f-104">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="09e0f-105">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="09e0f-105">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="09e0f-106">Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="09e0f-106">Blob storage is also referred tooas object storage.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="09e0f-107">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="09e0f-107">About this tutorial</span></span>
<span data-ttu-id="09e0f-108">Este tutorial muestra cómo código toowrite .NET en algunos escenarios comunes con almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="09e0f-108">This tutorial shows how toowrite .NET code for some common scenarios using Azure Blob storage.</span></span> <span data-ttu-id="09e0f-109">Entre los escenarios descritos se incluyen cargar, enumerar, descargar y eliminar blobs.</span><span class="sxs-lookup"><span data-stu-id="09e0f-109">Scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

<span data-ttu-id="09e0f-110">**Requisitos previos:**</span><span class="sxs-lookup"><span data-stu-id="09e0f-110">**Prerequisites:**</span></span>

* [<span data-ttu-id="09e0f-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09e0f-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/)
* [<span data-ttu-id="09e0f-112">Biblioteca de cliente de Almacenamiento de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="09e0f-112">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="09e0f-113">Administrador de configuración Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="09e0f-113">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* <span data-ttu-id="09e0f-114">Una [cuenta de almacenamiento de Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="09e0f-114">An [Azure storage account](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="09e0f-115">Más ejemplos</span><span class="sxs-lookup"><span data-stu-id="09e0f-115">More samples</span></span>
<span data-ttu-id="09e0f-116">Para ver ejemplos adicionales con el almacenamiento de blobs, consulte [Introducción a almacenamiento de blobs de Azure en .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="09e0f-116">For additional examples using Blob storage, see [Getting Started with Azure Blob Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span> <span data-ttu-id="09e0f-117">Puede descargar la aplicación de ejemplo de Hola y ejecutarlo o examinar el código de hello en GitHub.</span><span class="sxs-lookup"><span data-stu-id="09e0f-117">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="09e0f-118">Adición de directivas using</span><span class="sxs-lookup"><span data-stu-id="09e0f-118">Add using directives</span></span>
<span data-ttu-id="09e0f-119">Agregue Hola siguiente **con** arriba toohello de directivas de hello `Program.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="09e0f-119">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="09e0f-120">Analizar la cadena de conexión de Hola</span><span class="sxs-lookup"><span data-stu-id="09e0f-120">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a><span data-ttu-id="09e0f-121">Crear el cliente del servicio Blob Hola</span><span class="sxs-lookup"><span data-stu-id="09e0f-121">Create hello Blob service client</span></span>
<span data-ttu-id="09e0f-122">Hola **CloudBlobClient** clase le permite tooretrieve contenedores y blobs almacenados en almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="09e0f-122">hello **CloudBlobClient** class enables you tooretrieve containers and blobs stored in Blob storage.</span></span> <span data-ttu-id="09e0f-123">Este es el cliente del servicio de una manera toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="09e0f-123">Here's one way toocreate hello service client:</span></span>

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
<span data-ttu-id="09e0f-124">Ahora está listo toowrite código que lee datos de y escribe datos tooBlob storage.</span><span class="sxs-lookup"><span data-stu-id="09e0f-124">Now you are ready toowrite code that reads data from and writes data tooBlob storage.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="09e0f-125">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="09e0f-125">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="09e0f-126">Este ejemplo se muestra cómo toocreate un contenedor si aún no existe:</span><span class="sxs-lookup"><span data-stu-id="09e0f-126">This example shows how toocreate a container if it does not already exist:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

<span data-ttu-id="09e0f-127">De forma predeterminada, el nuevo contenedor de hello es privada, lo que significa que debe especificar los blobs de toodownload clave de acceso de almacenamiento de este contenedor.</span><span class="sxs-lookup"><span data-stu-id="09e0f-127">By default, hello new container is private, meaning that you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="09e0f-128">Si desea toomake archivos Hola Hola contenedor disponibles tooeveryone, puede establecer Hola contenedor toobe público mediante el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="09e0f-128">If you want toomake hello files within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

<span data-ttu-id="09e0f-129">Todos los usuarios de hello Internet pueden ver los blobs en un contenedor público.</span><span class="sxs-lookup"><span data-stu-id="09e0f-129">Anyone on hello Internet can see blobs in a public container.</span></span> <span data-ttu-id="09e0f-130">Sin embargo, puede modificar o eliminarlos únicamente si tiene la clave de acceso de cuenta adecuada de Hola o una firma de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="09e0f-130">However, you can modify or delete them only if you have hello appropriate account access key or a shared access signature.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="09e0f-131">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="09e0f-131">Upload a blob into a container</span></span>
<span data-ttu-id="09e0f-132">El almacenamiento de blobs de Azure admite blobs en bloques y en páginas.</span><span class="sxs-lookup"><span data-stu-id="09e0f-132">Azure Blob Storage supports block blobs and page blobs.</span></span>  <span data-ttu-id="09e0f-133">En la mayoría de los casos, blob en bloques es hello recomendada toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="09e0f-133">In most cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="09e0f-134">tooupload un blob en bloques archivo tooa, obtener una referencia de contenedor y usarlo tooget una referencia de blob de bloque.</span><span class="sxs-lookup"><span data-stu-id="09e0f-134">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="09e0f-135">Una vez que tenga una referencia de blob, puede cargar todos los flujos de datos tooit Hola llamada **UploadFromStream** método.</span><span class="sxs-lookup"><span data-stu-id="09e0f-135">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="09e0f-136">Esta operación crea blob Hola si no existía anteriormente, o lo sobrescribe si existe.</span><span class="sxs-lookup"><span data-stu-id="09e0f-136">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span>

<span data-ttu-id="09e0f-137">Hola siguiente ejemplo se muestra cómo tooupload un blob en un contenedor y se da por supuesto que el contenedor de hello ya se ha creado.</span><span class="sxs-lookup"><span data-stu-id="09e0f-137">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="09e0f-138">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="09e0f-138">List hello blobs in a container</span></span>
<span data-ttu-id="09e0f-139">blobs de hello toolist en un contenedor, primero hay que obtener una referencia de contenedor.</span><span class="sxs-lookup"><span data-stu-id="09e0f-139">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="09e0f-140">A continuación, puede usar del contenedor de hello **ListBlobs** blobs de método tooretrieve Hola y/o directorios dentro de él.</span><span class="sxs-lookup"><span data-stu-id="09e0f-140">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="09e0f-141">tooaccess Hola amplio conjunto de propiedades y métodos para un devuelto **IListBlobItem**, debe convertirlo tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="09e0f-141">tooaccess hello  rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="09e0f-142">Si el tipo de hello es desconocido, puede usar un toodetermine de comprobación de tipo que toocast a.</span><span class="sxs-lookup"><span data-stu-id="09e0f-142">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="09e0f-143">Hello código siguiente muestra cómo tooretrieve y salida Hola URI de cada elemento de hello _fotos_ contenedor:</span><span class="sxs-lookup"><span data-stu-id="09e0f-143">hello following code demonstrates how tooretrieve and output hello URI of each item in hello _photos_ container:</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, false))
{
    if (item.GetType() == typeof(CloudBlockBlob))
    {
        CloudBlockBlob blob = (CloudBlockBlob)item;

        Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);

    }
    else if (item.GetType() == typeof(CloudPageBlob))
    {
        CloudPageBlob pageBlob = (CloudPageBlob)item;

        Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);

    }
    else if (item.GetType() == typeof(CloudBlobDirectory))
    {
        CloudBlobDirectory directory = (CloudBlobDirectory)item;

        Console.WriteLine("Directory: {0}", directory.Uri);
    }
}
```

<span data-ttu-id="09e0f-144">Mediante la inclusión de la información de la ruta de acceso en los nombres de blobs se puede crear una estructura de directorios virtuales que puede organizar y recorrer, tal como lo haría en un sistema de archivos tradicional.</span><span class="sxs-lookup"><span data-stu-id="09e0f-144">By including path information in blob names, you can create a virtual directory structure you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="09e0f-145">estructura de directorios de Hello es virtual solo--Hola sólo recursos disponibles en el almacenamiento de blobs son contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="09e0f-145">hello directory structure is virtual only--hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="09e0f-146">Sin embargo, ofrece la biblioteca de cliente de almacenamiento de hello un **CloudBlobDirectory** objeto de directorio virtual de toorefer tooa y simplificar el proceso Hola de trabajar con los blobs que se organizan de esta manera.</span><span class="sxs-lookup"><span data-stu-id="09e0f-146">However, hello storage client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="09e0f-147">Por ejemplo, considere la posibilidad de hello siguiente conjunto de blobs en bloques en un contenedor denominado *fotos*:</span><span class="sxs-lookup"><span data-stu-id="09e0f-147">For example, consider hello following set of block blobs in a container named *photos*:</span></span>

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

<span data-ttu-id="09e0f-148">Cuando se llama a **ListBlobs** en hello *fotos* contenedor (como en Hola anterior fragmento de código), se devuelve una lista jerárquica.</span><span class="sxs-lookup"><span data-stu-id="09e0f-148">When you call **ListBlobs** on hello *photos* container (as in hello preceding code snippet), a hierarchical listing is returned.</span></span> <span data-ttu-id="09e0f-149">Contiene **CloudBlobDirectory** y **CloudBlockBlob** objetos, que representan directorios de Hola y blobs en el contenedor de hello, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="09e0f-149">It contains both **CloudBlobDirectory** and **CloudBlockBlob** objects, representing hello directories and blobs in hello container, respectively.</span></span> <span data-ttu-id="09e0f-150">resultado de Hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="09e0f-150">hello resulting output looks like:</span></span>

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

<span data-ttu-id="09e0f-151">Si lo desea, puede establecer hello **UseFlatBlobListing** parámetro de hello **ListBlobs** método **true**.</span><span class="sxs-lookup"><span data-stu-id="09e0f-151">Optionally, you can set hello **UseFlatBlobListing** parameter of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="09e0f-152">En este caso, cada blob en contenedor de Hola se devuelve como un **CloudBlockBlob** objeto.</span><span class="sxs-lookup"><span data-stu-id="09e0f-152">In this case, every blob in hello container is returned as a **CloudBlockBlob** object.</span></span> <span data-ttu-id="09e0f-153">Hola llamada demasiado**ListBlobs** tooreturn una lista plana tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="09e0f-153">hello call too**ListBlobs** tooreturn a flat listing looks like this:</span></span>

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

<span data-ttu-id="09e0f-154">y los resultados de hello tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="09e0f-154">and hello results look like this:</span></span>

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a><span data-ttu-id="09e0f-155">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="09e0f-155">Download blobs</span></span>
<span data-ttu-id="09e0f-156">blobs toodownload, recuperar primero una referencia de blob y, a continuación, llamar a hello **DownloadToStream** método.</span><span class="sxs-lookup"><span data-stu-id="09e0f-156">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="09e0f-157">Hello en el ejemplo siguiente se usa hello **DownloadToStream** método tootransfer Hola blob contenido tooa objeto stream que, a continuación, puede conservar tooa de archivos local.</span><span class="sxs-lookup"><span data-stu-id="09e0f-157">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

<span data-ttu-id="09e0f-158">También puede usar hello **DownloadToStream** contenido de hello toodownload de método de un blob como una cadena de texto.</span><span class="sxs-lookup"><span data-stu-id="09e0f-158">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a><span data-ttu-id="09e0f-159">Eliminar blobs</span><span class="sxs-lookup"><span data-stu-id="09e0f-159">Delete blobs</span></span>
<span data-ttu-id="09e0f-160">toodelete un blob, primero hay que obtener una referencia de blob y, a continuación, llame a la **eliminar** método en él.</span><span class="sxs-lookup"><span data-stu-id="09e0f-160">toodelete a blob, first get a blob reference and then call the **Delete** method on it.</span></span>

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="09e0f-161">Enumerar blobs en páginas de forma asincrónica</span><span class="sxs-lookup"><span data-stu-id="09e0f-161">List blobs in pages asynchronously</span></span>
<span data-ttu-id="09e0f-162">Si estás anunciando un gran número de blobs o desea toocontrol Hola número de resultados que devuelven en una sola operación de lista, puede enumerar blobs en páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="09e0f-162">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="09e0f-163">Este ejemplo muestra cómo tooreturn da como resultado páginas de forma asincrónica, por lo que no la ejecución se bloquea mientras se esperaba tooreturn un gran conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="09e0f-163">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="09e0f-164">Este ejemplo muestra una lista plana de blobs, pero también puede realizar una lista jerárquica, establecer hello _useFlatBlobListing_ parámetro de hello **ListBlobsSegmentedAsync** too_false_ de método.</span><span class="sxs-lookup"><span data-stu-id="09e0f-164">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello _useFlatBlobListing_ parameter of hello **ListBlobsSegmentedAsync** method too_false_.</span></span>

<span data-ttu-id="09e0f-165">Como método de ejemplo de Hola llama a un método asincrónico, deben ir precedida por hello _async_ (palabra clave) y debe devolver un **tarea** objeto.</span><span class="sxs-lookup"><span data-stu-id="09e0f-165">Because hello sample method calls an asynchronous method, it must be prefaced with hello _async_ keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="09e0f-166">Hola await palabra clave especificada para hello **ListBlobsSegmentedAsync** método suspende la ejecución del método de ejemplo hello hasta que se complete la tarea de la lista de hello.</span><span class="sxs-lookup"><span data-stu-id="09e0f-166">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
        resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
        if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
        foreach (var blobItem in resultSegment.Results)
        {
            Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
        }
        Console.WriteLine();

        //Get hello continuation token.
        continuationToken = resultSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="09e0f-167">Escritura tooan anexar blob</span><span class="sxs-lookup"><span data-stu-id="09e0f-167">Writing tooan append blob</span></span>
<span data-ttu-id="09e0f-168">Un blob en anexos se optimiza para las operaciones de anexado, como el registro.</span><span class="sxs-lookup"><span data-stu-id="09e0f-168">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="09e0f-169">Como un blob en bloques, un blob en anexos está formado por bloques, pero cuando se agrega un nuevo blob en bloques tooan anexado, siempre es toohello anexado final del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="09e0f-169">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="09e0f-170">No se puede actualizar o eliminar un bloque existente en un blob en anexos.</span><span class="sxs-lookup"><span data-stu-id="09e0f-170">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="09e0f-171">Identificadores de bloque de Hola para un blob en anexos no se exponen como sirven como un blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="09e0f-171">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="09e0f-172">Cada bloque de un blob en anexos puede tener un tamaño diferente, la tooa máximo de 4 MB, y un blob en anexos puede incluir un máximo de 50.000 bloques.</span><span class="sxs-lookup"><span data-stu-id="09e0f-172">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="09e0f-173">tamaño máximo de Hola de un blob en anexos, por tanto, es un poco más de 195 GB (4 MB X 50.000 bloques).</span><span class="sxs-lookup"><span data-stu-id="09e0f-173">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="09e0f-174">ejemplo de Hola siguiente crea un nuevo blob en anexos y anexa algunos tooit de datos, simular una operación de registro simple.</span><span class="sxs-lookup"><span data-stu-id="09e0f-174">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

<span data-ttu-id="09e0f-175">Vea [descripción Blobs en bloques, Blobs de página y anexar Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) para obtener más información acerca de las diferencias de hello entre tipos de hello tres de blobs.</span><span class="sxs-lookup"><span data-stu-id="09e0f-175">See [Understanding Block Blobs, Page Blobs, and Append Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) for more information about hello differences between hello three types of blobs.</span></span>

## <a name="managing-security-for-blobs"></a><span data-ttu-id="09e0f-176">Administración de la seguridad para blobs</span><span class="sxs-lookup"><span data-stu-id="09e0f-176">Managing security for blobs</span></span>
<span data-ttu-id="09e0f-177">De forma predeterminada, el almacenamiento de Azure protege los datos mediante la limitación de propietario de la cuenta toohello acceso, que está en posesión de claves de acceso de cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="09e0f-177">By default, Azure Storage keeps your data secure by limiting access toohello account owner, who is in possession of hello account access keys.</span></span> <span data-ttu-id="09e0f-178">Si necesita datos de blob de tooshare en su cuenta de almacenamiento, es importante toodo así sin comprometer la seguridad de Hola de las claves de acceso de cuenta.</span><span class="sxs-lookup"><span data-stu-id="09e0f-178">When you need tooshare blob data in your storage account, it is important toodo so without compromising hello security of your account access keys.</span></span> <span data-ttu-id="09e0f-179">Además, puede cifrar tooensure de datos de blob que es seguro pasar a través de la conexión de Hola y el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="09e0f-179">Additionally, you can encrypt blob data tooensure that it is secure going over hello wire and in Azure Storage.</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a><span data-ttu-id="09e0f-180">Controlar el acceso a los datos tooblob</span><span class="sxs-lookup"><span data-stu-id="09e0f-180">Controlling access tooblob data</span></span>
<span data-ttu-id="09e0f-181">De forma predeterminada, los datos de blob de hello en su cuenta de almacenamiento son accesible sólo propietario de la cuenta toostorage.</span><span class="sxs-lookup"><span data-stu-id="09e0f-181">By default, hello blob data in your storage account is accessible only toostorage account owner.</span></span> <span data-ttu-id="09e0f-182">Autenticar las solicitudes en el almacenamiento de blobs requiere la clave de acceso de cuenta de hello de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="09e0f-182">Authenticating requests against Blob storage requires hello account access key by default.</span></span> <span data-ttu-id="09e0f-183">Sin embargo, quizá prefiera toomake ciertos usuarios disponibles tooother de datos de blob.</span><span class="sxs-lookup"><span data-stu-id="09e0f-183">However, you may wish toomake certain blob data available tooother users.</span></span> <span data-ttu-id="09e0f-184">Tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="09e0f-184">You have two options:</span></span>

* <span data-ttu-id="09e0f-185">**Acceso anónimo:** puede hacer que un contenedor o sus blobs estén públicamente disponibles para el acceso anónimo.</span><span class="sxs-lookup"><span data-stu-id="09e0f-185">**Anonymous access:** You can make a container or its blobs publicly available for anonymous access.</span></span> <span data-ttu-id="09e0f-186">Vea [administrar toocontainers de acceso de lectura anónimo y los blobs](storage-manage-access-to-resources.md) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="09e0f-186">See [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="09e0f-187">**Firmas de acceso compartido:** puede proporcionar a los clientes con una firma de acceso compartido (SAS), que proporciona acceso delegado tooa recursos en la cuenta de almacenamiento con los permisos que especifican y a través de un intervalo que especifique.</span><span class="sxs-lookup"><span data-stu-id="09e0f-187">**Shared access signatures:** You can provide clients with a shared access signature (SAS), which provides delegated access tooa resource in your storage account, with permissions that you specify and over an interval that you specify.</span></span> <span data-ttu-id="09e0f-188">Consulte [Uso de firmas de acceso compartido (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para más información.</span><span class="sxs-lookup"><span data-stu-id="09e0f-188">See [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

### <a name="encrypting-blob-data"></a><span data-ttu-id="09e0f-189">Cifrado de datos Blob</span><span class="sxs-lookup"><span data-stu-id="09e0f-189">Encrypting blob data</span></span>
<span data-ttu-id="09e0f-190">Almacenamiento de Azure admite el cifrado de datos de blob en el cliente de Hola y en el servidor de hello:</span><span class="sxs-lookup"><span data-stu-id="09e0f-190">Azure Storage supports encrypting blob data both at hello client and on hello server:</span></span>

* <span data-ttu-id="09e0f-191">**Cifrado en el cliente:** Hola biblioteca cliente de almacenamiento para .NET admite el cifrado de los datos dentro de las aplicaciones cliente antes de cargar tooAzure almacenamiento y descifrar los datos mientras se descargaba toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="09e0f-191">**Client-side encryption:** hello Storage Client Library for .NET supports encrypting data within client applications before uploading tooAzure Storage, and decrypting data while downloading toohello client.</span></span> <span data-ttu-id="09e0f-192">biblioteca de Hello también admite la integración con el almacén de claves de Azure para administración de claves de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="09e0f-192">hello library also supports integration with Azure Key Vault for storage account key management.</span></span> <span data-ttu-id="09e0f-193">Consulte [Cifrado del lado de cliente y Almacén de claves de Azure para el Almacenamiento de Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para más información.</span><span class="sxs-lookup"><span data-stu-id="09e0f-193">See [Client-Side Encryption with .NET for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span> <span data-ttu-id="09e0f-194">Consulte también [Tutorial: Cifrado y descifrado de blobs en Almacenamiento de Microsoft Azure con Almacén de claves de Azure](storage-encrypt-decrypt-blobs-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="09e0f-194">Also see [Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md).</span></span>
* <span data-ttu-id="09e0f-195">**Cifrado en el servidor**: Almacenamiento de Azure ahora admite el cifrado en el servidor.</span><span class="sxs-lookup"><span data-stu-id="09e0f-195">**Server-side encryption**: Azure Storage now supports server-side encryption.</span></span> <span data-ttu-id="09e0f-196">Consulte [Cifrado del servicio Almacenamiento de Azure para datos en reposo (versión preliminar)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="09e0f-196">See [Azure Storage Service Encryption for Data at Rest (Preview)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09e0f-197">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="09e0f-197">Next steps</span></span>
<span data-ttu-id="09e0f-198">Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de blobs, siga estas toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="09e0f-198">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

### <a name="microsoft-azure-storage-explorer"></a><span data-ttu-id="09e0f-199">Explorador de almacenamiento de Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="09e0f-199">Microsoft Azure Storage Explorer</span></span>
* <span data-ttu-id="09e0f-200">[Explorador de almacenamiento de Azure de Microsoft (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.</span><span class="sxs-lookup"><span data-stu-id="09e0f-200">[Microsoft Azure Storage Explorer (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

### <a name="blob-storage-samples"></a><span data-ttu-id="09e0f-201">Ejemplos de Almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="09e0f-201">Blob storage samples</span></span>
* [<span data-ttu-id="09e0f-202">Introducción a almacenamiento de blobs de Azure en .NET</span><span class="sxs-lookup"><span data-stu-id="09e0f-202">Getting Started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a><span data-ttu-id="09e0f-203">Referencia de Almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="09e0f-203">Blob storage reference</span></span>
* [<span data-ttu-id="09e0f-204">Referencia de la biblioteca de clientes de almacenamiento para .NET</span><span class="sxs-lookup"><span data-stu-id="09e0f-204">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [<span data-ttu-id="09e0f-205">Referencia de API de REST</span><span class="sxs-lookup"><span data-stu-id="09e0f-205">REST API reference</span></span>](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a><span data-ttu-id="09e0f-206">Guías conceptuales</span><span class="sxs-lookup"><span data-stu-id="09e0f-206">Conceptual guides</span></span>
* [<span data-ttu-id="09e0f-207">Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola</span><span class="sxs-lookup"><span data-stu-id="09e0f-207">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="09e0f-208">Introducción al Almacenamiento de archivos para .NET</span><span class="sxs-lookup"><span data-stu-id="09e0f-208">Get started with File storage for .NET</span></span>](../files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="09e0f-209">¿Cómo toouse Azure blob storage con hello SDK de WebJobs</span><span class="sxs-lookup"><span data-stu-id="09e0f-209">How toouse Azure blob storage with hello WebJobs SDK</span></span>](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
