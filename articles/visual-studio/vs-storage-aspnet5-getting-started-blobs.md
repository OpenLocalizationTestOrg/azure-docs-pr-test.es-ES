---
title: "Introducción a Blob Storage y a los servicios conectados de Visual Studio (ASP.NET Core) | Microsoft Docs"
description: "Cómo empezar a usar Azure Blob Storage en un proyecto de ASP.NET Core de Visual Studio después de haber creado una cuenta de almacenamiento mediante los servicios conectados de Visual Studio"
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
ms.openlocfilehash: 2e8060b44c395ad7c24e7778c0ef65148a3a45de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a><span data-ttu-id="b34ff-103">Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET Core) (ASP.NET Core)</span><span class="sxs-lookup"><span data-stu-id="b34ff-103">Get started with Azure Blob storage and Visual Studio connected services (ASP.NET Core)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="b34ff-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b34ff-104">Overview</span></span>
<span data-ttu-id="b34ff-105">En este artículo se describe cómo empezar a usar Azure Blob Storage en Visual Studio después de haber creado o hecho referencia a una cuenta de Azure Storage en un proyecto de ASP.NET Core mediante el cuadro de diálogo Add Connected Services (Agregar servicios conectados) de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b34ff-105">This article describes how to get started using Azure Blob storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio Add Connected Services dialog.</span></span>

<span data-ttu-id="b34ff-106">El almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados a los que puede obtenerse acceso desde cualquier lugar del mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b34ff-106">Azure Blob storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="b34ff-107">Un solo blob puede tener cualquier tamaño.</span><span class="sxs-lookup"><span data-stu-id="b34ff-107">A single blob can be any size.</span></span> <span data-ttu-id="b34ff-108">Los blobs pueden tener forma de imágenes, archivos de audio y vídeo, archivos sin procesar y archivos de documentos.</span><span class="sxs-lookup"><span data-stu-id="b34ff-108">Blobs can be things like images, audio and video files, raw data, and document files.</span></span> <span data-ttu-id="b34ff-109">En este artículo se describe cómo empezar a usar Blob Storage después de crear una cuenta de Azure Storage desde el cuadro de diálogo **Add Connected Services** (Agregar servicios conectados) de Visual Studio en un proyecto de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="b34ff-109">This article describes how to get started with blob storage after you create an Azure storage account by using the Visual Studio **Add Connected Services** dialog in an ASP.NET Core project.</span></span>

<span data-ttu-id="b34ff-110">Al igual que los archivos residen en carpetas, los blobs de almacenamiento residen en contenedores.</span><span class="sxs-lookup"><span data-stu-id="b34ff-110">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="b34ff-111">Después de haber creado un almacenamiento, puede crear uno o varios contenedores en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b34ff-111">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="b34ff-112">Por ejemplo, en un almacenamiento llamado "Scrapbook", puede crear un contenedor llamado "images" para almacenar imágenes y otro llamado "audio" para almacenar archivos de audio.</span><span class="sxs-lookup"><span data-stu-id="b34ff-112">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="b34ff-113">Una vez creados los contenedores, puede cargar archivos de blob individuales a ellos.</span><span class="sxs-lookup"><span data-stu-id="b34ff-113">After you create the containers, you can upload individual blob files to them.</span></span> <span data-ttu-id="b34ff-114">Consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) para más información sobre la manipulación de blobs mediante programación.</span><span class="sxs-lookup"><span data-stu-id="b34ff-114">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) for more information on programmatically manipulating blobs.</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="b34ff-115">Contenedores de blobs de acceso en el código</span><span class="sxs-lookup"><span data-stu-id="b34ff-115">Access blob containers in code</span></span>
<span data-ttu-id="b34ff-116">Para obtener acceso mediante programación a los blobs en los proyectos de ASP.NET Core, es preciso agregar los elementos siguientes, si no están presentes aún.</span><span class="sxs-lookup"><span data-stu-id="b34ff-116">To programmatically access blobs in ASP.NET Core projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="b34ff-117">Agregue las siguientes declaraciones de espacio de nombres de código en la parte superior de todo archivo C# en el que desee obtener acceso al almacenamiento de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="b34ff-117">Add the following code namespace declarations to the top of any C# file in which you want to programmatically access Azure storage.</span></span>
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. <span data-ttu-id="b34ff-118">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b34ff-118">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="b34ff-119">Use el código siguiente para obtener la cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de la configuración del servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="b34ff-119">Use the following code to get your storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    <span data-ttu-id="b34ff-120">**NOTA:** use todo el código anterior delante del código que aparece en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="b34ff-120">**NOTE:** Use all of the above code in front of the code in the following sections.</span></span>
3. <span data-ttu-id="b34ff-121">Use un objeto **CloudBlobClient** para obtener una referencia **CloudBlobContainer** a un contenedor existente en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b34ff-121">Use a **CloudBlobClient** object to get a **CloudBlobContainer** reference to an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a><span data-ttu-id="b34ff-122">Crear un contenedor en código</span><span class="sxs-lookup"><span data-stu-id="b34ff-122">Create a container in code</span></span>
<span data-ttu-id="b34ff-123">También puede usar el **CloudBlobClient** para crear un contenedor en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="b34ff-123">You can also use the **CloudBlobClient** to create a container in your storage account.</span></span> <span data-ttu-id="b34ff-124">Tan solo tiene que agregar una llamada a **CreateIfNotExistsAsync** como en el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="b34ff-124">All you need to do is to add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference to a container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="b34ff-125">**NOTA:** las API que realizan llamadas a Azure Storage en ASP.NET Core son asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="b34ff-125">**NOTE:** The APIs that perform calls to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="b34ff-126">Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="b34ff-126">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="b34ff-127">El código siguiente supone que se están utilizando métodos de programación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="b34ff-127">The code below assumes async programming methods are being used.</span></span>

<span data-ttu-id="b34ff-128">Para poner los archivos del contenedor a disposición de todo el mundo, puede convertir el contenedor en público usando el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="b34ff-128">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="b34ff-129">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="b34ff-129">Upload a blob into a container</span></span>
<span data-ttu-id="b34ff-130">Para cargar un archivo de blob en un contenedor, obtenga una referencia de contenedor y utilícela para obtener una referencia de blob.</span><span class="sxs-lookup"><span data-stu-id="b34ff-130">To upload a blob file into a container, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="b34ff-131">Una vez que disponga de la referencia de blob, puede cargar cualquier secuencia de datos en ella llamando al método **UploadFromStreamAsync** .</span><span class="sxs-lookup"><span data-stu-id="b34ff-131">After you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStreamAsync** method.</span></span> <span data-ttu-id="b34ff-132">Esta operación crea el blob, en caso de que no existe, o lo sobrescribe si ya existe.</span><span class="sxs-lookup"><span data-stu-id="b34ff-132">This operation creates the blob if it's not already there, or overwrites it if it does exist.</span></span> <span data-ttu-id="b34ff-133">En el siguiente ejemplo se muestra cómo cargar un blob en un contenedor creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b34ff-133">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Get a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with the contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="b34ff-134">Enumerar los blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="b34ff-134">List the blobs in a container</span></span>
<span data-ttu-id="b34ff-135">Para enumerar los blobs de un contenedor, primero obtenga una referencia de contenedor.</span><span class="sxs-lookup"><span data-stu-id="b34ff-135">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="b34ff-136">A continuación, llame al método **ListBlobsSegmentedAsync** del contenedor para recuperar los blobs o los directorios que contiene.</span><span class="sxs-lookup"><span data-stu-id="b34ff-136">You can then call the container's **ListBlobsSegmentedAsync** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="b34ff-137">Para acceder a las numerosas propiedades y métodos de una lista **IListBlobItem** recuperada, debe convertir esta última en un objeto **CloudBlockBlob**, **CloudPageBlob** o **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="b34ff-137">To access the rich set of properties and methods for a returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="b34ff-138">Si no conoce el tipo de blob, puede utilizar un comprobador de tipos para determinar a cuál se debe convertir.</span><span class="sxs-lookup"><span data-stu-id="b34ff-138">If you don't know the blob type, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="b34ff-139">El código siguiente demuestra cómo recuperar y consultar el URI de cada elemento del contenedor.</span><span class="sxs-lookup"><span data-stu-id="b34ff-139">The following code demonstrates how to retrieve and output the URI of each item in a container.</span></span>

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

<span data-ttu-id="b34ff-140">Hay otras maneras de enumerar el contenido de un contenedor de blobs.</span><span class="sxs-lookup"><span data-stu-id="b34ff-140">There are others ways to list the contents of a blob container.</span></span> <span data-ttu-id="b34ff-141">Consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) para más información.</span><span class="sxs-lookup"><span data-stu-id="b34ff-141">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) for more information.</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="b34ff-142">Descarga de un blob</span><span class="sxs-lookup"><span data-stu-id="b34ff-142">Download a blob</span></span>
<span data-ttu-id="b34ff-143">Para descargar un blob, primero obtenga una referencia al blob y luego llame al método **DownloadToStreamAsync** .</span><span class="sxs-lookup"><span data-stu-id="b34ff-143">To download a blob, first get a reference to the blob, and then call the **DownloadToStreamAsync** method.</span></span> <span data-ttu-id="b34ff-144">En el siguiente ejemplo se usa el método **DownloadToStreamAsync** para transferir el contenido del blob a un objeto de secuencia que luego puede guardar como archivo local.</span><span class="sxs-lookup"><span data-stu-id="b34ff-144">The following example uses the **DownloadToStreamAsync** method to transfer the blob contents to a stream object that you can then save as a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save the blob contents to a file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

<span data-ttu-id="b34ff-145">Hay otras maneras de guardar blobs como archivos.</span><span class="sxs-lookup"><span data-stu-id="b34ff-145">There are other ways to save blobs as files.</span></span> <span data-ttu-id="b34ff-146">Consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) para más información.</span><span class="sxs-lookup"><span data-stu-id="b34ff-146">See [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) for more information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="b34ff-147">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="b34ff-147">Delete a blob</span></span>
<span data-ttu-id="b34ff-148">Para eliminar un blob, obtenga primero una referencia al blob y, a continuación, llame al método **DeleteAsync** .</span><span class="sxs-lookup"><span data-stu-id="b34ff-148">To delete a blob, first get a reference to the blob, and then call the **DeleteAsync** method on it.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a><span data-ttu-id="b34ff-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b34ff-149">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

