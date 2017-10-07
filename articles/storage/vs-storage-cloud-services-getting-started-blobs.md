---
title: aaaGet a trabajar con el almacenamiento de blobs y Visual Studio servicios conectados (servicios en la nube) | Documentos de Microsoft
description: "Cómo tooget a usar almacenamiento de blobs de Azure en un proyecto de servicio de nube en Visual Studio después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 62fb7fcff0a90008859ebe23755f13ef0555e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="fb851-103">Introducción al almacenamiento de blobs de Azure y a los servicios conectados de Visual Studio (proyectos de servicios en la nube)</span><span class="sxs-lookup"><span data-stu-id="fb851-103">Get started with Azure Blob Storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="fb851-104">Información general</span><span class="sxs-lookup"><span data-stu-id="fb851-104">Overview</span></span>
<span data-ttu-id="fb851-105">Este artículo describe cómo tooget se inicia con el almacenamiento de blobs de Azure tras crear o hace referencia a una cuenta de almacenamiento de Azure mediante Visual Studio hello **agregar servicios conectados** proyecto de servicios de cuadro de diálogo en una nube de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fb851-105">This article describes how tooget started with Azure Blob Storage after you created or referenced an Azure Storage account by using hello Visual Studio **Add Connected Services** dialog in a Visual Studio cloud services project.</span></span> <span data-ttu-id="fb851-106">Le mostraremos cómo tooaccess y crear contenedores de blobs y cómo tooperform las tareas comunes como cargar, enumerar y descargar blobs.</span><span class="sxs-lookup"><span data-stu-id="fb851-106">We'll show you how tooaccess and create blob containers, and how tooperform common tasks like uploading, listing, and downloading blobs.</span></span> <span data-ttu-id="fb851-107">Hola ejemplos están escritos en C\# y usar hello [biblioteca de cliente de almacenamiento de Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb851-107">hello samples are written in C\# and use hello [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="fb851-108">Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados que pueden tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fb851-108">Azure Blob Storage is a service for storing large amounts of unstructured data that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="fb851-109">Un solo blob puede tener cualquier tamaño.</span><span class="sxs-lookup"><span data-stu-id="fb851-109">A single blob can be any size.</span></span> <span data-ttu-id="fb851-110">Los blobs pueden tener forma de imágenes, archivos de audio y vídeo, archivos sin procesar y archivos de documentos.</span><span class="sxs-lookup"><span data-stu-id="fb851-110">Blobs can be things like images, audio and video files, raw data, and document files.</span></span>

<span data-ttu-id="fb851-111">Al igual que los archivos residen en carpetas, los blobs de almacenamiento residen en contenedores.</span><span class="sxs-lookup"><span data-stu-id="fb851-111">Just as files live in folders, storage blobs live in containers.</span></span> <span data-ttu-id="fb851-112">Después de haber creado un almacenamiento, cree uno o varios contenedores en el almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb851-112">After you have created a storage, you create one or more containers in hello storage.</span></span> <span data-ttu-id="fb851-113">Por ejemplo, en un almacenamiento denominado "Álbum", puede crear contenedores de almacenamiento de hello denominado imágenes de toostore "imágenes" y otro denominado "audio" toostore archivos de audio.</span><span class="sxs-lookup"><span data-stu-id="fb851-113">For example, in a storage called "Scrapbook," you can create containers in hello storage called "images" toostore pictures and another called "audio" toostore audio files.</span></span> <span data-ttu-id="fb851-114">Después de crear contenedores de hello, puede cargar toothem de archivos de blob individuales.</span><span class="sxs-lookup"><span data-stu-id="fb851-114">After you create hello containers, you can upload individual blob files toothem.</span></span>

* <span data-ttu-id="fb851-115">Para más información sobre la manipulación de blobs mediante programación, consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="fb851-115">For more information on programmatically manipulating blobs, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md).</span></span>
* <span data-ttu-id="fb851-116">Para una información general sobre Almacenamiento de Azure, consulte [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="fb851-116">For general information about Azure Storage, see [Storage documentation](https://azure.microsoft.com/documentation/services/storage/).</span></span>
* <span data-ttu-id="fb851-117">Para información general sobre los servicios en la nube de Azure, vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="fb851-117">For general information about Azure Cloud Services, see [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/).</span></span>
* <span data-ttu-id="fb851-118">Para obtener más información acerca de la programación de aplicaciones ASP.NET, consulte [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="fb851-118">For more information about programming ASP.NET applications, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="access-blob-containers-in-code"></a><span data-ttu-id="fb851-119">Contenedores de blobs de acceso en el código</span><span class="sxs-lookup"><span data-stu-id="fb851-119">Access blob containers in code</span></span>
<span data-ttu-id="fb851-120">tooprogrammatically acceda a blobs en proyectos de servicios de nube, debe hello tooadd siguientes elementos, si no están presentes.</span><span class="sxs-lookup"><span data-stu-id="fb851-120">tooprogrammatically access blobs in cloud service projects, you need tooadd hello following items, if they're not already present.</span></span>

1. <span data-ttu-id="fb851-121">Agregar Hola después de la parte superior de las declaraciones toohello espacio de nombres de código de cualquier archivo de C# en el que desea acceso tooprogrammatically almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb851-121">Add hello following code namespace declarations toohello top of any C# file in which you wish tooprogrammatically access Azure Storage.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="fb851-122">Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="fb851-122">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="fb851-123">Hola de uso después de código tooget Hola su cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de información de configuración del servicio de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="fb851-123">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. <span data-ttu-id="fb851-124">Obtener un **CloudBlobClient** tooreference un contenedor existente en su cuenta de almacenamiento del objeto.</span><span class="sxs-lookup"><span data-stu-id="fb851-124">Get a **CloudBlobClient** object tooreference an existing container in your storage account.</span></span>
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. <span data-ttu-id="fb851-125">Obtener un **CloudBlobContainer** objeto tooreference un contenedor de blob en cuestión.</span><span class="sxs-lookup"><span data-stu-id="fb851-125">Get a **CloudBlobContainer** object tooreference a specific blob container.</span></span>
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> <span data-ttu-id="fb851-126">Utilizar todo el código de hello mostrado en el procedimiento anterior de hello frente a código de hello mostrado en hello las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="fb851-126">Use all of hello code shown in hello previous procedure in front of hello code shown in hello following sections.</span></span>
> 
> 

## <a name="create-a-container-in-code"></a><span data-ttu-id="fb851-127">Crear un contenedor en código</span><span class="sxs-lookup"><span data-stu-id="fb851-127">Create a container in code</span></span>
> [!NOTE]
> <span data-ttu-id="fb851-128">Algunas API que realizan llamadas tooAzure almacenamiento en ASP.NET es asincrónica.</span><span class="sxs-lookup"><span data-stu-id="fb851-128">Some APIs that perform calls out tooAzure Storage in ASP.NET are asynchronous.</span></span> <span data-ttu-id="fb851-129">Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información.</span><span class="sxs-lookup"><span data-stu-id="fb851-129">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="fb851-130">código de Hello en el siguiente ejemplo de Hola se da por supuesto que está usando métodos de programación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="fb851-130">hello code in hello following example assumes that you are using async programming methods.</span></span>
> 
> 

<span data-ttu-id="fb851-131">toocreate un contenedor en la cuenta de almacenamiento, todo lo que necesita toodo se agregue una llamada demasiado**CreateIfNotExistsAsync** como en el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="fb851-131">toocreate a container in your storage account, all you need toodo is add a call too**CreateIfNotExistsAsync** as in hello following code:</span></span>

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


<span data-ttu-id="fb851-132">toomake Hola archivos Hola contenedor disponibles tooeveryone, se puede establecer Hola contenedor toobe pública mediante Hola siguiente código.</span><span class="sxs-lookup"><span data-stu-id="fb851-132">toomake hello files within hello container available tooeveryone, you can set hello container toobe public by using hello following code.</span></span>

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


<span data-ttu-id="fb851-133">Todos los usuarios de hello Internet pueden ver los blobs en un contenedor público, pero puede modificar o eliminarlos únicamente si tiene la clave de acceso adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb851-133">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="fb851-134">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="fb851-134">Upload a blob into a container</span></span>
<span data-ttu-id="fb851-135">El almacenamiento de Azure admite blobs en bloques y en páginas.</span><span class="sxs-lookup"><span data-stu-id="fb851-135">Azure Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="fb851-136">En la mayoría de los casos Hola blob en bloques es hello recomendada toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="fb851-136">In hello majority of cases, block blob is hello recommended type toouse.</span></span>

<span data-ttu-id="fb851-137">tooupload un blob en bloques archivo tooa, obtener una referencia de contenedor y usarlo tooget una referencia de blob de bloque.</span><span class="sxs-lookup"><span data-stu-id="fb851-137">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="fb851-138">Una vez que tenga una referencia de blob, puede cargar todos los flujos de datos tooit Hola llamada **UploadFromStream** método.</span><span class="sxs-lookup"><span data-stu-id="fb851-138">Once you have a blob reference, you can upload any stream of data tooit by calling hello **UploadFromStream** method.</span></span> <span data-ttu-id="fb851-139">Esta operación crea blob Hola si no existía anteriormente, o lo sobrescribe si existe.</span><span class="sxs-lookup"><span data-stu-id="fb851-139">This operation creates hello blob if it didn't previously exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="fb851-140">Hola siguiente ejemplo se muestra cómo tooupload un blob en un contenedor y se da por supuesto que el contenedor de hello ya se ha creado.</span><span class="sxs-lookup"><span data-stu-id="fb851-140">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="fb851-141">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="fb851-141">List hello blobs in a container</span></span>
<span data-ttu-id="fb851-142">blobs de hello toolist en un contenedor, primero hay que obtener una referencia de contenedor.</span><span class="sxs-lookup"><span data-stu-id="fb851-142">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="fb851-143">A continuación, puede usar del contenedor de hello **ListBlobs** blobs de método tooretrieve Hola y/o directorios dentro de él.</span><span class="sxs-lookup"><span data-stu-id="fb851-143">You can then use hello container's **ListBlobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="fb851-144">tooaccess Hola amplio conjunto de propiedades y métodos para un devuelto **IListBlobItem**, debe convertirlo tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="fb851-144">tooaccess hello rich set of properties and methods for a  returned **IListBlobItem**, you must cast it tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="fb851-145">Si el tipo de hello es desconocido, puede usar un toodetermine de comprobación de tipo que toocast a.</span><span class="sxs-lookup"><span data-stu-id="fb851-145">If hello type is unknown, you can use a type check toodetermine which toocast it to.</span></span> <span data-ttu-id="fb851-146">Hello código siguiente muestra cómo tooretrieve y salida Hola URI de cada elemento de hello **fotos** contenedor:</span><span class="sxs-lookup"><span data-stu-id="fb851-146">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **photos** container:</span></span>

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

<span data-ttu-id="fb851-147">Como se muestra en el ejemplo de código anterior de hello, servicio de blob de hello tiene el concepto de Hola de directorios dentro de contenedores, así.</span><span class="sxs-lookup"><span data-stu-id="fb851-147">As shown in hello previous code sample, hello blob service has hello concept of directories within containers, as well.</span></span> <span data-ttu-id="fb851-148">De este modo, es posible organizar los blobs en una estructura similar a la estructura de carpetas.</span><span class="sxs-lookup"><span data-stu-id="fb851-148">This is so that you can organize your blobs in a more folder-like structure.</span></span> <span data-ttu-id="fb851-149">Por ejemplo, considere la posibilidad de hello siguiente conjunto de blobs en bloques en un contenedor denominado **fotos**:</span><span class="sxs-lookup"><span data-stu-id="fb851-149">For example, consider hello following set of block blobs in a container named **photos**:</span></span>

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

<span data-ttu-id="fb851-150">Cuando se llama a **ListBlobs** contenedor hello (como en el ejemplo anterior de hello), colección de hello devuelta contiene **CloudBlobDirectory** y **CloudBlockBlob** objetos que representa los directorios de Hola y blobs incluidos en el nivel superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="fb851-150">When you call **ListBlobs** on hello container (as in hello previous sample), hello collection returned contains **CloudBlobDirectory** and **CloudBlockBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="fb851-151">Este es el resultado de hello:</span><span class="sxs-lookup"><span data-stu-id="fb851-151">Here is hello resulting output:</span></span>

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


<span data-ttu-id="fb851-152">Si lo desea, puede establecer hello **UseFlatBlobListing** parámetro de Hola **ListBlobs** método **true**.</span><span class="sxs-lookup"><span data-stu-id="fb851-152">Optionally, you can set hello **UseFlatBlobListing** parameter of of hello **ListBlobs** method to **true**.</span></span> <span data-ttu-id="fb851-153">De este modo, todos los blobs aparecerían como **CloudBlockBlob**, con independencia del directorio.</span><span class="sxs-lookup"><span data-stu-id="fb851-153">This results in every blob being returned as a **CloudBlockBlob**, regardless of directory.</span></span> <span data-ttu-id="fb851-154">Aquí es llamada Hola demasiado**ListBlobs**:</span><span class="sxs-lookup"><span data-stu-id="fb851-154">Here is hello call too**ListBlobs**:</span></span>

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

<span data-ttu-id="fb851-155">y estos son los resultados de hello:</span><span class="sxs-lookup"><span data-stu-id="fb851-155">and here are hello results:</span></span>

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

<span data-ttu-id="fb851-156">Para más información, consulte [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span><span class="sxs-lookup"><span data-stu-id="fb851-156">For more information, see [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).</span></span>

## <a name="download-blobs"></a><span data-ttu-id="fb851-157">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="fb851-157">Download blobs</span></span>
<span data-ttu-id="fb851-158">blobs toodownload, recuperar primero una referencia de blob y, a continuación, llamar a hello **DownloadToStream** método.</span><span class="sxs-lookup"><span data-stu-id="fb851-158">toodownload blobs, first retrieve a blob reference and then call hello **DownloadToStream** method.</span></span> <span data-ttu-id="fb851-159">Hello en el ejemplo siguiente se usa hello **DownloadToStream** método tootransfer Hola blob contenido tooa objeto stream que, a continuación, puede conservar tooa de archivos local.</span><span class="sxs-lookup"><span data-stu-id="fb851-159">hello following example uses hello **DownloadToStream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

<span data-ttu-id="fb851-160">También puede usar hello **DownloadToStream** contenido de hello toodownload de método de un blob como una cadena de texto.</span><span class="sxs-lookup"><span data-stu-id="fb851-160">You can also use hello **DownloadToStream** method toodownload hello contents of a blob as a text string.</span></span>

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a><span data-ttu-id="fb851-161">Eliminar blobs</span><span class="sxs-lookup"><span data-stu-id="fb851-161">Delete blobs</span></span>
<span data-ttu-id="fb851-162">toodelete un blob, primero hay que obtener una referencia de blob y, a continuación, llame a la **eliminar** método.</span><span class="sxs-lookup"><span data-stu-id="fb851-162">toodelete a blob, first get a blob reference and then call the **Delete** method.</span></span>

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a><span data-ttu-id="fb851-163">Enumerar blobs en páginas de forma asincrónica</span><span class="sxs-lookup"><span data-stu-id="fb851-163">List blobs in pages asynchronously</span></span>
<span data-ttu-id="fb851-164">Si estás anunciando un gran número de blobs o desea toocontrol Hola número de resultados que devuelven en una sola operación de lista, puede enumerar blobs en páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="fb851-164">If you are listing a large number of blobs, or you want toocontrol hello number of results you return in one listing operation, you can list blobs in pages of results.</span></span> <span data-ttu-id="fb851-165">Este ejemplo muestra cómo tooreturn da como resultado páginas de forma asincrónica, por lo que no la ejecución se bloquea mientras se esperaba tooreturn un gran conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="fb851-165">This example shows how tooreturn results in pages asynchronously, so that execution is not blocked while waiting tooreturn a large set of results.</span></span>

<span data-ttu-id="fb851-166">Este ejemplo muestra una lista plana de blobs, pero también puede realizar una lista jerárquica, establecer hello **useFlatBlobListing** parámetro de hello **ListBlobsSegmentedAsync** método demasiado **false**.</span><span class="sxs-lookup"><span data-stu-id="fb851-166">This example shows a flat blob listing, but you can also perform a hierarchical listing, by setting hello **useFlatBlobListing** parameter of hello **ListBlobsSegmentedAsync** method too**false**.</span></span>

<span data-ttu-id="fb851-167">Como método de ejemplo de Hola llama a un método asincrónico, deben ir precedida por hello **async** (palabra clave) y debe devolver un **tarea** objeto.</span><span class="sxs-lookup"><span data-stu-id="fb851-167">Because hello sample method calls an asynchronous method, it must be prefaced with hello **async** keyword, and it must return a **Task** object.</span></span> <span data-ttu-id="fb851-168">Hola await palabra clave especificada para hello **ListBlobsSegmentedAsync** método suspende la ejecución del método de ejemplo hello hasta que se complete la tarea de la lista de hello.</span><span class="sxs-lookup"><span data-stu-id="fb851-168">hello await keyword specified for hello **ListBlobsSegmentedAsync** method suspends execution of hello sample method until hello listing task completes.</span></span>

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
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

## <a name="next-steps"></a><span data-ttu-id="fb851-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb851-169">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

