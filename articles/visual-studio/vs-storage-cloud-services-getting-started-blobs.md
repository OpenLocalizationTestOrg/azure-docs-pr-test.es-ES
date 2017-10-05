---
title: "Introducción al almacenamiento de blobs y los servicios conectados de Visual Studio (servicios en la nube) | Microsoft Docs"
description: "Cómo empezar a usar el almacenamiento de blobs de Azure en un proyecto de servicio en la nube en Visual Studio después de conectarse a una cuenta de almacenamiento mediante los servicios conectados de Visual Studio"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: cf14880c70f90b01c5dffbfe434150581c2ec33b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="78c4c-103">Introducción al almacenamiento de blobs de Azure y a los servicios conectados de Visual Studio (proyectos de servicios en la nube)</span><span class="sxs-lookup"><span data-stu-id="78c4c-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="78c4c-104">Información general</span><span class="sxs-lookup"><span data-stu-id="78c4c-104">Overview</span></span>
<span data-ttu-id="78c4c-105">En este artículo se describe cómo empezar a usar el almacenamiento de blobs de Azure después de haber creado o hecho referencia a una cuenta de almacenamiento de Azure mediante el cuadro de diálogo **Agregar servicios conectados** en un proyecto de servicios en la nube de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="78c4c-105">This article describes how to get started with Azure Blob Storage after you created or referenced an Azure Storage account by using the Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="78c4c-106">Le mostraremos cómo obtener acceder a contenedores de blob y cómo crearlos, además de cómo realizar tareas comunes como cargar, enumerar y descargar blobs.</span><span class="sxs-lookup"><span data-stu-id="78c4c-106">We'll show you how to access and create blob containers, and how to perform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="78c4c-107">Los ejemplos están escritos en C\# y usan la [biblioteca del cliente de Microsoft Azure Storage para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="78c4c-107">The samples are written in C\# and use the [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="78c4c-108">El almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados a los que puede obtenerse acceso desde cualquier lugar del mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="78c4c-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="78c4c-109">Un solo blob puede tener cualquier tamaño.</span><span class="sxs-lookup"><span data-stu-id="78c4c-109">A single blob can be any size.</span></span> <span data-ttu-id="78c4c-110">Los blobs pueden tener forma de imágenes, archivos de audio y vídeo, archivos sin procesar y archivos de documentos.</span><span class="sxs-lookup"><span data-stu-id="78c4c-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="78c4c-111">Al igual que los archivos residen en carpetas, los blobs de almacenamiento residen en contenedores.</span><span class="sxs-lookup"><span data-stu-id="78c4c-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="78c4c-112">Después de haber creado un almacenamiento, puede crear uno o varios contenedores en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="78c4c-112">After you have created a storage, you create one or more containers in the storage.</span></span> <span data-ttu-id="78c4c-113">Por ejemplo, en un almacenamiento llamado "Scrapbook", puede crear un contenedor llamado "images" para almacenar imágenes y otro llamado "audio" para almacenar archivos de audio.</span><span class="sxs-lookup"><span data-stu-id="78c4c-113">For example, in a storage called "Scrapbook," you can create containers in the storage called "images" to store pictures and another called "audio" to store audio files.</span></span> <span data-ttu-id="78c4c-114">Una vez creados los contenedores, puede cargar archivos de blob individuales a ellos.</span><span class="sxs-lookup"><span data-stu-id="78c4c-114">After you create the containers, you can upload individual blob files to them.</span></span>

* <span data-ttu-id="78c4c-115">Para más información sobre la manipulación de blobs mediante programación, consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="78c4c-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="78c4c-116">Para una información general sobre Almacenamiento de Azure, consulte [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="78c4c-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="78c4c-117">Para información general sobre los servicios en la nube de Azure, vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="78c4c-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="78c4c-118">Para obtener más información acerca de la programación de aplicaciones ASP.NET, consulte [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="78c4c-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="78c4c-119">Contenedores de blobs de acceso en el código</span><span class="sxs-lookup"><span data-stu-id="78c4c-119">Access blob containers in code</span></span>
<span data-ttu-id="78c4c-120">Para obtener acceso mediante programación a los blobs de los proyectos del Servicio en la nube, deberá agregar los elementos siguientes, si no están presentes todavía.</span><span class="sxs-lookup"><span data-stu-id="78c4c-120">To programmatically access blobs in cloud service projects, you need to add the following items, if they're not already present.</span></span>

1. <span data-ttu-id="78c4c-121">Agregue las siguientes declaraciones de espacio de nombres de código en la parte superior de todo archivo C# en el que desee obtener acceso al Almacenamiento de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="78c4c-121">Add the following code namespace declarations to the top of any C# file in which you wish to programmatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="78c4c-122">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="78c4c-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="78c4c-123">Use el código siguiente para obtener la cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de la configuración del servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="78c4c-123">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="78c4c-124">Obtenga un objeto **CloudBlobClient** para hacer referencia a un contenedor existente en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="78c4c-124">Get a **CloudBlobClient** object to reference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="78c4c-125">Obtenga un objeto **CloudBlobContainer** para hacer referencia a un contenedor de blobs específico.</span><span class="sxs-lookup"><span data-stu-id="78c4c-125">Get a **CloudBlobContainer** object to reference a specific blob container.</span></span>
   
        // Get a reference to a container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="78c4c-126">Use todo el código que se muestra en el procedimiento anterior delante del código que se muestra en las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="78c4c-126">Use all of the code shown in the previous procedure in front of the code shown in the following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="78c4c-127">Crear un contenedor en código</span><span class="sxs-lookup"><span data-stu-id="78c4c-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="78c4c-128">Algunas API que realizan llamadas al almacenamiento de Azure en ASP.NET son asincrónicas.</span><span class="sxs-lookup"><span data-stu-id="78c4c-128">Some APIs that perform calls out to Azure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="78c4c-129">Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="78c4c-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="78c4c-130">En el código del siguiente ejemplo, se da por supuesto que se están usando métodos de programación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="78c4c-130">The code in the following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="78c4c-131">Para crear un contenedor en su cuenta de almacenamiento, lo único que hay que hacer es agregar una llamada a **CreateIfNotExistsAsync** como en el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="78c4c-131">To create a container in your storage account, all you need to do is add a call to **CreateIfNotExistsAsync** as in the following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="78c4c-132">Para poner los archivos del contenedor a disposición de todo el mundo, puede convertir el contenedor en público usando el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="78c4c-132">To make the files within the container available to everyone, you can set the container to be public by using the following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="78c4c-133">Cualquier usuario de Internet puede ver los blobs de los contenedores públicos, pero solo es posible modificarlos o eliminarlos si se dispone de la clave de acceso apropiada.</span><span class="sxs-lookup"><span data-stu-id="78c4c-133">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="78c4c-134">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="78c4c-134">Upload a blob into a container</span></span>
<span data-ttu-id="78c4c-135">El almacenamiento de Azure admite blobs en bloques y en páginas.</span><span class="sxs-lookup"><span data-stu-id="78c4c-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="78c4c-136">En la mayoría de los casos, se recomienda usar blobs en bloques.</span><span class="sxs-lookup"><span data-stu-id="78c4c-136">In the majority of cases, block blob is the recommended type to use.</span></span>

<span data-ttu-id="78c4c-137">Para cargar un archivo en un blob en bloques, obtenga una referencia de contenedor y utilícela para obtener una referencia de blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="78c4c-137">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="78c4c-138">Una vez que disponga de la referencia de blob, puede cargar cualquier secuencia de datos en ella llamando al método **UploadFromStream** .</span><span class="sxs-lookup"><span data-stu-id="78c4c-138">Once you have a blob reference, you can upload any stream of data to it by calling the **UploadFromStream** method.</span></span> <span data-ttu-id="78c4c-139">De este modo, se crea el blob si no existía anteriormente, o bien se sobrescribe si ya existía.</span><span class="sxs-lookup"><span data-stu-id="78c4c-139">This operation creates the blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="78c4c-140">En el siguiente ejemplo se muestra cómo cargar un blob en un contenedor creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="78c4c-140">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>

    // Retrieve a reference to a blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite the "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="78c4c-141">Enumerar los blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="78c4c-141">List the blobs in a container</span></span>
<span data-ttu-id="78c4c-142">Para enumerar los blobs de un contenedor, primero obtenga una referencia de contenedor.</span><span class="sxs-lookup"><span data-stu-id="78c4c-142">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="78c4c-143">A continuación, puede utilizar el método **ListBlobs** del contenedor para recuperar los blobs y los directorios que contiene.</span><span class="sxs-lookup"><span data-stu-id="78c4c-143">You can then use the container's **ListBlobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="78c4c-144">Para tener acceso a las numerosas propiedades y métodos de una lista **IListBlobItem** recuperada, debe convertir esta última en un objeto **CloudBlockBlob**, **CloudPageBlob** o **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="78c4c-144">To access the rich set of properties and methods for a  returned **IListBlobItem**, you must cast it to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="78c4c-145">Si se desconoce el tipo, puede realizar una comprobación de tipo para determinar el formato al que se debe convertir.</span><span class="sxs-lookup"><span data-stu-id="78c4c-145">If the type is unknown, you can use a type check to determine which to cast it to.</span></span> <span data-ttu-id="78c4c-146">El código siguiente demuestra cómo recuperar y consultar el URI de cada elemento del contenedor **photos** :</span><span class="sxs-lookup"><span data-stu-id="78c4c-146">The following code demonstrates how to retrieve and output the URI of each item in the **photos** container:</span></span>

    // Loop over items within the container and output the length and URI.
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

<span data-ttu-id="78c4c-147">Como se muestra en el ejemplo de código anterior, en el servicio BLOB los contenedores también incluyen directorios.</span><span class="sxs-lookup"><span data-stu-id="78c4c-147">As shown in the previous code sample, the blob service has the concept of directories within containers, as well.</span></span> <span data-ttu-id="78c4c-148">De este modo, es posible organizar los blobs en una estructura similar a la estructura de carpetas.</span><span class="sxs-lookup"><span data-stu-id="78c4c-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="78c4c-149">Por ejemplo, observe el siguiente conjunto de blobs en bloques incluidos en un contenedor denominado **photos**:</span><span class="sxs-lookup"><span data-stu-id="78c4c-149">For example, consider the following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="78c4c-150">Al llamar a **ListBlobs** en el contenedor (como en el ejemplo anterior), la lista que se obtenga contendrá objetos **CloudBlobDirectory** y **CloudBlockBlob** que representan los directorios y los blobs existentes en el nivel superior.</span><span class="sxs-lookup"><span data-stu-id="78c4c-150">When you call **ListBlobs** on the container (as in the previous sample), the collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="78c4c-151">Este es el resultado:</span><span class="sxs-lookup"><span data-stu-id="78c4c-151">Here is the resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="78c4c-152">También existe la opción de establecer el parámetro **UseFlatBlobListing** del método **ListBlobs** en **true**.</span><span class="sxs-lookup"><span data-stu-id="78c4c-152">Optionally, you can set the **UseFlatBlobListing** parameter of of the **ListBlobs** method to **true**.</span></span> <span data-ttu-id="78c4c-153">De este modo, todos los blobs aparecerían como **CloudBlockBlob**, con independencia del directorio.</span><span class="sxs-lookup"><span data-stu-id="78c4c-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="78c4c-154">Esta es la llamada a **ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="78c4c-154">Here is the call to **ListBlobs**:</span></span>

    // Loop over items within the container and output the length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="78c4c-155">y estos son los resultados:</span><span class="sxs-lookup"><span data-stu-id="78c4c-155">and here are the results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="78c4c-156">Para más información, consulte [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="78c4c-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="78c4c-157">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="78c4c-157">Download blobs</span></span>
<span data-ttu-id="78c4c-158">Para descargar blobs, primero recupere una referencia de blob y, a continuación, llame al método **DownloadToStream** .</span><span class="sxs-lookup"><span data-stu-id="78c4c-158">To download blobs, first retrieve a blob reference and then call the **DownloadToStream** method.</span></span> <span data-ttu-id="78c4c-159">En el siguiente ejemplo, se usa el método **DownloadToStream** para transferir el contenido del blob a un objeto de secuencia que, a continuación, puede guardar en un archivo local.</span><span class="sxs-lookup"><span data-stu-id="78c4c-159">The following example uses the **DownloadToStream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>

    // Get a reference to a blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents to a file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="78c4c-160">También puede usar el método **DownloadToStream** para descargar el contenido de un blob en forma de cadena de texto.</span><span class="sxs-lookup"><span data-stu-id="78c4c-160">You can also use the **DownloadToStream** method to download the contents of a blob as a text string.</span></span>

    // Get a reference to a blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="78c4c-161">Eliminar blobs</span><span class="sxs-lookup"><span data-stu-id="78c4c-161">Delete blobs</span></span>
<span data-ttu-id="78c4c-162">Para eliminar un blob, obtenga primero una referencia de blob y luego llame al método **Delete** .</span><span class="sxs-lookup"><span data-stu-id="78c4c-162">To delete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference to a blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete the blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="78c4c-163">Enumerar blobs en páginas de forma asincrónica</span><span class="sxs-lookup"><span data-stu-id="78c4c-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="78c4c-164">Si enumera un gran número de blobs o desea controlar el número de resultados que devuelve en una operación de listado, puede enumerar blobs en páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="78c4c-164">If you are listing a large number of blobs, or you want to control the number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="78c4c-165">En este ejemplo se muestra cómo devolver resultados en páginas asincrónicamente de forma que la ejecución no se bloquee mientras se espera a devolver un conjunto grande de resultados.</span><span class="sxs-lookup"><span data-stu-id="78c4c-165">This example shows how to return results in pages asynchronously, so that execution is not blocked while waiting to return a large set of results.</span></span>

<span data-ttu-id="78c4c-166">En este ejemplo se muestra un listado de blobs plano, pero también puede realizar un listado jerárquico si establece el parámetro **useFlatBlobListing** del método **ListBlobsSegmentedAsync** en **false**.</span><span class="sxs-lookup"><span data-stu-id="78c4c-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting the **useFlatBlobListing** parameter of the **ListBlobsSegmentedAsync** method to **false**.</span></span>

<span data-ttu-id="78c4c-167">Dado que el método de ejemplo llama a un método asincrónico, debe ir precedido por la palabra clave **async** y debe devolver un objeto **Task**.</span><span class="sxs-lookup"><span data-stu-id="78c4c-167">Because the sample method calls an asynchronous method, it must be prefaced with the **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="78c4c-168">La palabra clave await especificada para el método **ListBlobsSegmentedAsync** suspende la ejecución del método de ejemplo hasta que la tarea de enumeración se completa.</span><span class="sxs-lookup"><span data-stu-id="78c4c-168">The await keyword specified for the **ListBlobsSegmentedAsync** method suspends execution of the sample method until the listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs to the console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate the result segment returned, while the continuation token is non-null.
        // When the continuation token is null, the last page has been returned and execution can exit the loop.
        do
        {
            // This overload allows control of the page size. You can return all remaining results by passing null for the maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get the continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a><span data-ttu-id="78c4c-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78c4c-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

