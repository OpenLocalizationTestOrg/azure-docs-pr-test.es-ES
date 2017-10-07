---
title: aaaGet a trabajar con el almacenamiento de blobs y Visual Studio servicios conectados (ASP.NET Core) | Documentos de Microsoft
description: "Cómo tooget a usar almacenamiento de blobs de Azure en un proyecto de Visual Studio ASP.NET Core después de haber creado una cuenta de almacenamiento mediante Visual Studio servicios conectados"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="71bf2-103">Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET Core) (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="71bf2-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="71bf2-104">Información general</span><span class="sxs-lookup"><span data-stu-id="71bf2-104">Overview</span></span>
<span data-ttu-id="71bf2-105">Este artículo describe cómo tooget iniciado mediante el almacenamiento de blobs de Azure en Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure en un proyecto de ASP.NET Core mediante el cuadro de diálogo de hello Visual Studio agregar servicios conectados.</span><span class="sxs-lookup"><span data-stu-id="71bf2-105">This article describes how tooget started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="71bf2-106">Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados que pueden tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="71bf2-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="71bf2-107">Un solo blob puede tener cualquier tamaño.</span><span class="sxs-lookup"><span data-stu-id="71bf2-107">A single blob can be any size.</span></span> <span data-ttu-id="71bf2-108">Los blobs pueden tener forma de imágenes, archivos de audio y vídeo, archivos sin procesar y archivos de documentos.</span><span class="sxs-lookup"><span data-stu-id="71bf2-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="71bf2-109">Este artículo describe cómo tooget a trabajar con almacenamiento de blobs después de crear una cuenta de almacenamiento de Azure mediante Visual Studio hello **agregar servicios conectados** cuadro de diálogo de un proyecto de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="71bf2-109">This article describes how tooget started with blob storage after you create an Azure storage account by using hello Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="71bf2-110">Al igual que los archivos residen en carpetas, los blobs de almacenamiento residen en contenedores.</span><span class="sxs-lookup"><span data-stu-id="71bf2-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="71bf2-111">Después de haber creado un almacenamiento, cree uno o varios contenedores en el almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="71bf2-111">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="71bf2-112">Por ejemplo, en un almacenamiento denominado "Álbum", puede crear contenedores de almacenamiento de hello denominado imágenes de toostore "imágenes" y otro denominado "audio" toostore archivos de audio.</span><span class="sxs-lookup"><span data-stu-id="71bf2-112">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="71bf2-113">Después de crear contenedores de hello, puede cargar toothem de archivos de blob individuales.</span><span class="sxs-lookup"><span data-stu-id="71bf2-113">After you create hello containers, you can upload individual blob files toothem.</span></span> <span data-ttu-id="71bf2-114">Consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) para más información sobre la manipulación de blobs mediante programación.</span><span class="sxs-lookup"><span data-stu-id="71bf2-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="71bf2-115">Contenedores de blobs de acceso en el código</span><span class="sxs-lookup"><span data-stu-id="71bf2-115">Access blob containers in code</span></span>
<span data-ttu-id="71bf2-116">tooprogrammatically acceda a blobs en proyectos de ASP.NET Core, deberá hello tooadd siguientes elementos, si no están presentes.</span><span class="sxs-lookup"><span data-stu-id="71bf2-116">tooprogrammatically access blobs in ASP.NET Core projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="71bf2-117">Agregar Hola sigue el principio de toohello de declaraciones de espacio de nombres de código de cualquier archivo de C# en el que desea acceso tooprogrammatically almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="71bf2-117">Add hello following code namespace declarations toohello top of any C# file in which you want tooprogrammatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="71bf2-118">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="71bf2-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="71bf2-119">Usar hello después código tooget su cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de información de configuración del servicio de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="71bf2-119">Use hello following code tooget your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="71bf2-120">**Nota:** los Hola encima código frente a código de hello usan en hello las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="71bf2-120">**NOTE:** Use all of hello above code in front of hello code in hello following sections.</span></span>
3. <span data-ttu-id="71bf2-121">Use un **CloudBlobClient** objeto tooget una **CloudBlobContainer** contenedor existente de referencia tooan en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="71bf2-121">Use a **CloudBlobClient** object tooget a **CloudBlobContainer** reference tooan existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="71bf2-122">Crear un contenedor en código</span><span class="sxs-lookup"><span data-stu-id="71bf2-122">Create a container in code</span></span>
<span data-ttu-id="71bf2-123">También puede usar hello **CloudBlobClient** toocreate un contenedor en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="71bf2-123">You can also use hello **CloudBlobClient** toocreate a container in your storage account.</span></span> <span data-ttu-id="71bf2-124">Todo lo que necesita toodo es demasiado tooadd una llamada**CreateIfNotExistsAsync** como en el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="71bf2-124">All you need toodo is tooadd a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="71bf2-125">**Nota:** hello las API que realizan llamadas tooAzure almacenamiento en ASP.NET Core son asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="71bf2-125">**NOTE:** hello APIs that perform calls tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="71bf2-126">Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="71bf2-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="71bf2-127">código de Hello siguiente se da por supuesto que se usan métodos de programación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="71bf2-127">hello code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="71bf2-128">toomake Hola archivos Hola contenedor disponibles tooeveryone, se puede establecer Hola contenedor toobe pública mediante Hola siguiente código.</span><span class="sxs-lookup"><span data-stu-id="71bf2-128">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="71bf2-129">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="71bf2-129">Upload a blob into a container</span></span>
<span data-ttu-id="71bf2-130">tooupload un archivo de blob en un contenedor, obtener una referencia de contenedor y usarlo tooget una referencia de blob.</span><span class="sxs-lookup"><span data-stu-id="71bf2-130">tooupload a blob file into a container, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="71bf2-131">Una vez que una referencia de blob, puede cargar todos los flujos de datos tooit Hola llamada **UploadFromStreamAsync** método.</span><span class="sxs-lookup"><span data-stu-id="71bf2-131">After you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="71bf2-132">Esta operación crea blob Hola si todavía no está presente, o lo sobrescribe si existe.</span><span class="sxs-lookup"><span data-stu-id="71bf2-132">This operation creates hello blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="71bf2-133">Hola siguiente ejemplo se muestra cómo tooupload un blob en un contenedor y se da por supuesto que el contenedor de hello ya se ha creado.</span><span class="sxs-lookup"><span data-stu-id="71bf2-133">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="71bf2-134">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="71bf2-134">List hello blobs in a container</span></span>
<span data-ttu-id="71bf2-135">blobs de hello toolist en un contenedor, primero hay que obtener una referencia de contenedor.</span><span class="sxs-lookup"><span data-stu-id="71bf2-135">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="71bf2-136">A continuación, puede llamar a del contenedor de hello **ListBlobsSegmentedAsync** blobs de método tooretrieve Hola y/o directorios dentro de él.</span><span class="sxs-lookup"><span data-stu-id="71bf2-136">You can then call hello container's **ListBlobsSegmentedAsync** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="71bf2-137">tooaccess Hola amplio conjunto de propiedades y métodos para un devuelto **IListBlobItem**, debe convertirlo tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="71bf2-137">tooaccess hello rich set of properties and methods for a returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="71bf2-138">Si no sabe que el blob de hello escriba, puede usar un toodetermine de comprobación de tipo que toocast a.</span><span class="sxs-lookup"><span data-stu-id="71bf2-138">If you don't know hello blob type, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="71bf2-139">Hola siguiente código muestra cómo tooretrieve y salida Hola URI de cada elemento en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="71bf2-139">hello following code demonstrates how tooretrieve and output hello URI of each item in a container.</span></span>

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
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
    } while (token != null);

<span data-ttu-id="71bf2-140">Hay de otros contenido de hello toolist de formas de un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="71bf2-140">There are others ways toolist hello contents of a blob container.</span></span> <span data-ttu-id="71bf2-141">Consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) para más información.</span><span class="sxs-lookup"><span data-stu-id="71bf2-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="71bf2-142">Descarga de un blob</span><span class="sxs-lookup"><span data-stu-id="71bf2-142">Download a blob</span></span>
<span data-ttu-id="71bf2-143">toodownload un blob, primero hay que obtener un blob de toohello de referencia y, a continuación, llamar a hello **DownloadToStreamAsync** método.</span><span class="sxs-lookup"><span data-stu-id="71bf2-143">toodownload a blob, first get a reference toohello blob, and then call hello **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="71bf2-144">Hello en el ejemplo siguiente se usa hello **DownloadToStreamAsync** método tootransfer Hola blob contenido tooa objeto stream que, a continuación, puede guardar como un archivo local.</span><span class="sxs-lookup"><span data-stu-id="71bf2-144">hello following example uses hello **DownloadToStreamAsync** method tootransfer hello blob contents tooa stream object that you can then save as a local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="71bf2-145">Hay otras maneras de BLOB toosave como archivos.</span><span class="sxs-lookup"><span data-stu-id="71bf2-145">There are other ways toosave blobs as files.</span></span> <span data-ttu-id="71bf2-146">Consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) para más información.</span><span class="sxs-lookup"><span data-stu-id="71bf2-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="71bf2-147">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="71bf2-147">Delete a blob</span></span>
<span data-ttu-id="71bf2-148">toodelete un blob, primero hay que obtener un blob de toohello de referencia y, a continuación, llamar a hello **DeleteAsync** método en él.</span><span class="sxs-lookup"><span data-stu-id="71bf2-148">toodelete a blob, first get a reference toohello blob, and then call hello **DeleteAsync** method on it.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="71bf2-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="71bf2-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

