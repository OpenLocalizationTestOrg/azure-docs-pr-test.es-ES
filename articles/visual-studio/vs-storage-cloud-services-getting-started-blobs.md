---
title: aaaGet a trabajar con el almacenamiento de blobs y Visual Studio servicios conectados (servicios en la nube) | Documentos de Microsoft
description: "Cómo tooget a usar almacenamiento de blobs de Azure en un proyecto de servicio de nube en Visual Studio después de conectar la cuenta de almacenamiento de tooa con Visual Studio servicios conectados"
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
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Introducción al almacenamiento de blobs de Azure y a los servicios conectados de Visual Studio (proyectos de servicios en la nube)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Información general
Este artículo describe cómo tooget se inicia con el almacenamiento de blobs de Azure tras crear o hace referencia a una cuenta de almacenamiento de Azure mediante Visual Studio hello **agregar servicios conectados** proyecto de servicios de cuadro de diálogo en una nube de Visual Studio. Le mostraremos cómo tooaccess y crear contenedores de blobs y cómo tooperform las tareas comunes como cargar, enumerar y descargar blobs. Hola ejemplos están escritos en C\# y usar hello [biblioteca de cliente de almacenamiento de Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados que pueden tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS. Un solo blob puede tener cualquier tamaño. Los blobs pueden tener forma de imágenes, archivos de audio y vídeo, archivos sin procesar y archivos de documentos.

Al igual que los archivos residen en carpetas, los blobs de almacenamiento residen en contenedores. Después de haber creado un almacenamiento, cree uno o varios contenedores en el almacenamiento de Hola. Por ejemplo, en un almacenamiento denominado "Álbum", puede crear contenedores de almacenamiento de hello denominado imágenes de toostore "imágenes" y otro denominado "audio" toostore archivos de audio. Después de crear contenedores de hello, puede cargar toothem de archivos de blob individuales.

* Para más información sobre la manipulación de blobs mediante programación, consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).
* Para una información general sobre Almacenamiento de Azure, consulte [Documentación sobre Almacenamiento](https://azure.microsoft.com/documentation/services/storage/).
* Para información general sobre los servicios en la nube de Azure, vea [Documentación sobre Servicios en la nube](https://azure.microsoft.com/documentation/services/cloud-services/).
* Para obtener más información acerca de la programación de aplicaciones ASP.NET, consulte [ASP.NET](http://www.asp.net).

## <a name="access-blob-containers-in-code"></a>Contenedores de blobs de acceso en el código
tooprogrammatically acceda a blobs en proyectos de servicios de nube, debe hello tooadd siguientes elementos, si no están presentes.

1. Agregar Hola después de la parte superior de las declaraciones toohello espacio de nombres de código de cualquier archivo de C# en el que desea acceso tooprogrammatically almacenamiento de Azure.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento. Hola de uso después de código tooget Hola su cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de información de configuración del servicio de Azure Hola.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. Obtener un **CloudBlobClient** tooreference un contenedor existente en su cuenta de almacenamiento del objeto.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. Obtener un **CloudBlobContainer** objeto tooreference un contenedor de blob en cuestión.
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> Utilizar todo el código de hello mostrado en el procedimiento anterior de hello frente a código de hello mostrado en hello las secciones siguientes.
> 
> 

## <a name="create-a-container-in-code"></a>Crear un contenedor en código
> [!NOTE]
> Algunas API que realizan llamadas tooAzure almacenamiento en ASP.NET es asincrónica. Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información. código de Hello en el siguiente ejemplo de Hola se da por supuesto que está usando métodos de programación asincrónica.
> 
> 

toocreate un contenedor en la cuenta de almacenamiento, todo lo que necesita toodo se agregue una llamada demasiado**CreateIfNotExistsAsync** como en el siguiente código de hello:

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


toomake Hola archivos Hola contenedor disponibles tooeveryone, se puede establecer Hola contenedor toobe pública mediante Hola siguiente código.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Todos los usuarios de hello Internet pueden ver los blobs en un contenedor público, pero puede modificar o eliminarlos únicamente si tiene la clave de acceso adecuado de Hola.

## <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor
El almacenamiento de Azure admite blobs en bloques y en páginas. En la mayoría de los casos Hola blob en bloques es hello recomendada toouse de tipo.

tooupload un blob en bloques archivo tooa, obtener una referencia de contenedor y usarlo tooget una referencia de blob de bloque. Una vez que tenga una referencia de blob, puede cargar todos los flujos de datos tooit Hola llamada **UploadFromStream** método. Esta operación crea blob Hola si no existía anteriormente, o lo sobrescribe si existe. Hola siguiente ejemplo se muestra cómo tooupload un blob en un contenedor y se da por supuesto que el contenedor de hello ya se ha creado.

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Lista de blobs de hello en un contenedor
blobs de hello toolist en un contenedor, primero hay que obtener una referencia de contenedor. A continuación, puede usar del contenedor de hello **ListBlobs** blobs de método tooretrieve Hola y/o directorios dentro de él. tooaccess Hola amplio conjunto de propiedades y métodos para un devuelto **IListBlobItem**, debe convertirlo tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** objeto. Si el tipo de hello es desconocido, puede usar un toodetermine de comprobación de tipo que toocast a. Hello código siguiente muestra cómo tooretrieve y salida Hola URI de cada elemento de hello **fotos** contenedor:

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

Como se muestra en el ejemplo de código anterior de hello, servicio de blob de hello tiene el concepto de Hola de directorios dentro de contenedores, así. De este modo, es posible organizar los blobs en una estructura similar a la estructura de carpetas. Por ejemplo, considere la posibilidad de hello siguiente conjunto de blobs en bloques en un contenedor denominado **fotos**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

Cuando se llama a **ListBlobs** contenedor hello (como en el ejemplo anterior de hello), colección de hello devuelta contiene **CloudBlobDirectory** y **CloudBlockBlob** objetos que representa los directorios de Hola y blobs incluidos en el nivel superior de Hola. Este es el resultado de hello:

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


Si lo desea, puede establecer hello **UseFlatBlobListing** parámetro de Hola **ListBlobs** método **true**. De este modo, todos los blobs aparecerían como **CloudBlockBlob**, con independencia del directorio. Aquí es llamada Hola demasiado**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

y estos son los resultados de hello:

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

Para más información, consulte [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).

## <a name="download-blobs"></a>Descargar blobs
blobs toodownload, recuperar primero una referencia de blob y, a continuación, llamar a hello **DownloadToStream** método. Hello en el ejemplo siguiente se usa hello **DownloadToStream** método tootransfer Hola blob contenido tooa objeto stream que, a continuación, puede conservar tooa de archivos local.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

También puede usar hello **DownloadToStream** contenido de hello toodownload de método de un blob como una cadena de texto.

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>Eliminar blobs
toodelete un blob, primero hay que obtener una referencia de blob y, a continuación, llame a la **eliminar** método.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>Enumerar blobs en páginas de forma asincrónica
Si estás anunciando un gran número de blobs o desea toocontrol Hola número de resultados que devuelven en una sola operación de lista, puede enumerar blobs en páginas de resultados. Este ejemplo muestra cómo tooreturn da como resultado páginas de forma asincrónica, por lo que no la ejecución se bloquea mientras se esperaba tooreturn un gran conjunto de resultados.

Este ejemplo muestra una lista plana de blobs, pero también puede realizar una lista jerárquica, establecer hello **useFlatBlobListing** parámetro de hello **ListBlobsSegmentedAsync** método demasiado **false**.

Como método de ejemplo de Hola llama a un método asincrónico, deben ir precedida por hello **async** (palabra clave) y debe devolver un **tarea** objeto. Hola await palabra clave especificada para hello **ListBlobsSegmentedAsync** método suspende la ejecución del método de ejemplo hello hasta que se complete la tarea de la lista de hello.

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

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

