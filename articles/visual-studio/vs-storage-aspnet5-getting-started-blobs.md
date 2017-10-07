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
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Introducción a Azure Blob Storage y los servicios conectados de Visual Studio (ASP.NET Core) (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Información general
Este artículo describe cómo tooget iniciado mediante el almacenamiento de blobs de Azure en Visual Studio después de haber creado o hace referencia a una cuenta de almacenamiento de Azure en un proyecto de ASP.NET Core mediante el cuadro de diálogo de hello Visual Studio agregar servicios conectados.

Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos no estructurados que pueden tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS. Un solo blob puede tener cualquier tamaño. Los blobs pueden tener forma de imágenes, archivos de audio y vídeo, archivos sin procesar y archivos de documentos. Este artículo describe cómo tooget a trabajar con almacenamiento de blobs después de crear una cuenta de almacenamiento de Azure mediante Visual Studio hello **agregar servicios conectados** cuadro de diálogo de un proyecto de ASP.NET Core.

Al igual que los archivos residen en carpetas, los blobs de almacenamiento residen en contenedores. Después de haber creado un almacenamiento, cree uno o varios contenedores en el almacenamiento de Hola. Por ejemplo, en un almacenamiento denominado "Álbum", puede crear contenedores de almacenamiento de hello denominado imágenes de toostore "imágenes" y otro denominado "audio" toostore archivos de audio. Después de crear contenedores de hello, puede cargar toothem de archivos de blob individuales. Consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) para más información sobre la manipulación de blobs mediante programación.

## <a name="access-blob-containers-in-code"></a>Contenedores de blobs de acceso en el código
tooprogrammatically acceda a blobs en proyectos de ASP.NET Core, deberá hello tooadd siguientes elementos, si no están presentes.

1. Agregar Hola sigue el principio de toohello de declaraciones de espacio de nombres de código de cualquier archivo de C# en el que desea acceso tooprogrammatically almacenamiento de Azure.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Obtenga un objeto **CloudStorageAccount** que represente la información de su cuenta de almacenamiento. Usar hello después código tooget su cadena de conexión de almacenamiento y la información de la cuenta de almacenamiento de información de configuración del servicio de Azure Hola.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **Nota:** los Hola encima código frente a código de hello usan en hello las secciones siguientes.
3. Use un **CloudBlobClient** objeto tooget una **CloudBlobContainer** contenedor existente de referencia tooan en su cuenta de almacenamiento.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Crear un contenedor en código
También puede usar hello **CloudBlobClient** toocreate un contenedor en la cuenta de almacenamiento. Todo lo que necesita toodo es demasiado tooadd una llamada**CreateIfNotExistsAsync** como en el siguiente código de hello:

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**Nota:** hello las API que realizan llamadas tooAzure almacenamiento en ASP.NET Core son asincrónicas. Vea [Programación asincrónica con Async y Await](http://msdn.microsoft.com/library/hh191443.aspx) para más información. código de Hello siguiente se da por supuesto que se usan métodos de programación asincrónica.

toomake Hola archivos Hola contenedor disponibles tooeveryone, se puede establecer Hola contenedor toobe pública mediante Hola siguiente código.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor
tooupload un archivo de blob en un contenedor, obtener una referencia de contenedor y usarlo tooget una referencia de blob. Una vez que una referencia de blob, puede cargar todos los flujos de datos tooit Hola llamada **UploadFromStreamAsync** método. Esta operación crea blob Hola si todavía no está presente, o lo sobrescribe si existe. Hola siguiente ejemplo se muestra cómo tooupload un blob en un contenedor y se da por supuesto que el contenedor de hello ya se ha creado.

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Lista de blobs de hello en un contenedor
blobs de hello toolist en un contenedor, primero hay que obtener una referencia de contenedor. A continuación, puede llamar a del contenedor de hello **ListBlobsSegmentedAsync** blobs de método tooretrieve Hola y/o directorios dentro de él. tooaccess Hola amplio conjunto de propiedades y métodos para un devuelto **IListBlobItem**, debe convertirlo tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** objeto. Si no sabe que el blob de hello escriba, puede usar un toodetermine de comprobación de tipo que toocast a. Hola siguiente código muestra cómo tooretrieve y salida Hola URI de cada elemento en un contenedor.

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

Hay de otros contenido de hello toolist de formas de un contenedor de blobs. Consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) para más información.

## <a name="download-a-blob"></a>Descarga de un blob
toodownload un blob, primero hay que obtener un blob de toohello de referencia y, a continuación, llamar a hello **DownloadToStreamAsync** método. Hello en el ejemplo siguiente se usa hello **DownloadToStreamAsync** método tootransfer Hola blob contenido tooa objeto stream que, a continuación, puede guardar como un archivo local.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

Hay otras maneras de BLOB toosave como archivos. Consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) para más información.

## <a name="delete-a-blob"></a>Eliminar un blob
toodelete un blob, primero hay que obtener un blob de toohello de referencia y, a continuación, llamar a hello **DeleteAsync** método en él.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

