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
# <a name="get-started-with-azure-blob-storage-using-net"></a>Introducción al Almacenamiento de blobs de Azure mediante .NET

[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs. El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación. Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.

### <a name="about-this-tutorial"></a>Acerca de este tutorial
Este tutorial muestra cómo código toowrite .NET en algunos escenarios comunes con almacenamiento de blobs de Azure. Entre los escenarios descritos se incluyen cargar, enumerar, descargar y eliminar blobs.

**Requisitos previos:**

* [Microsoft Visual Studio](https://www.visualstudio.com/)
* [Biblioteca de cliente de Almacenamiento de Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Administrador de configuración Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Una [cuenta de almacenamiento de Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Más ejemplos
Para ver ejemplos adicionales con el almacenamiento de blobs, consulte [Introducción a almacenamiento de blobs de Azure en .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/). Puede descargar la aplicación de ejemplo de Hola y ejecutarlo o examinar el código de hello en GitHub.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Adición de directivas using
Agregue Hola siguiente **con** arriba toohello de directivas de hello `Program.cs` archivo:

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a>Analizar la cadena de conexión de Hola
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a>Crear el cliente del servicio Blob Hola
Hola **CloudBlobClient** clase le permite tooretrieve contenedores y blobs almacenados en almacenamiento de blobs. Este es el cliente del servicio de una manera toocreate hello:

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
Ahora está listo toowrite código que lee datos de y escribe datos tooBlob storage.

## <a name="create-a-container"></a>Crear un contenedor
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Este ejemplo se muestra cómo toocreate un contenedor si aún no existe:

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

De forma predeterminada, el nuevo contenedor de hello es privada, lo que significa que debe especificar los blobs de toodownload clave de acceso de almacenamiento de este contenedor. Si desea toomake archivos Hola Hola contenedor disponibles tooeveryone, puede establecer Hola contenedor toobe público mediante el siguiente código de hello:

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Todos los usuarios de hello Internet pueden ver los blobs en un contenedor público. Sin embargo, puede modificar o eliminarlos únicamente si tiene la clave de acceso de cuenta adecuada de Hola o una firma de acceso compartido.

## <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor
El almacenamiento de blobs de Azure admite blobs en bloques y en páginas.  En la mayoría de los casos, blob en bloques es hello recomendada toouse de tipo.

tooupload un blob en bloques archivo tooa, obtener una referencia de contenedor y usarlo tooget una referencia de blob de bloque. Una vez que tenga una referencia de blob, puede cargar todos los flujos de datos tooit Hola llamada **UploadFromStream** método. Esta operación crea blob Hola si no existía anteriormente, o lo sobrescribe si existe.

Hola siguiente ejemplo se muestra cómo tooupload un blob en un contenedor y se da por supuesto que el contenedor de hello ya se ha creado.

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

## <a name="list-hello-blobs-in-a-container"></a>Lista de blobs de hello en un contenedor
blobs de hello toolist en un contenedor, primero hay que obtener una referencia de contenedor. A continuación, puede usar del contenedor de hello **ListBlobs** blobs de método tooretrieve Hola y/o directorios dentro de él. tooaccess Hola amplio conjunto de propiedades y métodos para un devuelto **IListBlobItem**, debe convertirlo tooa **CloudBlockBlob**, **CloudPageBlob**, o  **CloudBlobDirectory** objeto. Si el tipo de hello es desconocido, puede usar un toodetermine de comprobación de tipo que toocast a. Hello código siguiente muestra cómo tooretrieve y salida Hola URI de cada elemento de hello _fotos_ contenedor:

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

Mediante la inclusión de la información de la ruta de acceso en los nombres de blobs se puede crear una estructura de directorios virtuales que puede organizar y recorrer, tal como lo haría en un sistema de archivos tradicional. estructura de directorios de Hello es virtual solo--Hola sólo recursos disponibles en el almacenamiento de blobs son contenedores y blobs. Sin embargo, ofrece la biblioteca de cliente de almacenamiento de hello un **CloudBlobDirectory** objeto de directorio virtual de toorefer tooa y simplificar el proceso Hola de trabajar con los blobs que se organizan de esta manera.

Por ejemplo, considere la posibilidad de hello siguiente conjunto de blobs en bloques en un contenedor denominado *fotos*:

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

Cuando se llama a **ListBlobs** en hello *fotos* contenedor (como en Hola anterior fragmento de código), se devuelve una lista jerárquica. Contiene **CloudBlobDirectory** y **CloudBlockBlob** objetos, que representan directorios de Hola y blobs en el contenedor de hello, respectivamente. resultado de Hello tiene el siguiente aspecto:

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

Si lo desea, puede establecer hello **UseFlatBlobListing** parámetro de hello **ListBlobs** método **true**. En este caso, cada blob en contenedor de Hola se devuelve como un **CloudBlockBlob** objeto. Hola llamada demasiado**ListBlobs** tooreturn una lista plana tiene el siguiente aspecto:

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

y los resultados de hello tiene este aspecto:

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

## <a name="download-blobs"></a>Descargar blobs
blobs toodownload, recuperar primero una referencia de blob y, a continuación, llamar a hello **DownloadToStream** método. Hello en el ejemplo siguiente se usa hello **DownloadToStream** método tootransfer Hola blob contenido tooa objeto stream que, a continuación, puede conservar tooa de archivos local.

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

También puede usar hello **DownloadToStream** contenido de hello toodownload de método de un blob como una cadena de texto.

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

## <a name="delete-blobs"></a>Eliminar blobs
toodelete un blob, primero hay que obtener una referencia de blob y, a continuación, llame a la **eliminar** método en él.

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

## <a name="list-blobs-in-pages-asynchronously"></a>Enumerar blobs en páginas de forma asincrónica
Si estás anunciando un gran número de blobs o desea toocontrol Hola número de resultados que devuelven en una sola operación de lista, puede enumerar blobs en páginas de resultados. Este ejemplo muestra cómo tooreturn da como resultado páginas de forma asincrónica, por lo que no la ejecución se bloquea mientras se esperaba tooreturn un gran conjunto de resultados.

Este ejemplo muestra una lista plana de blobs, pero también puede realizar una lista jerárquica, establecer hello _useFlatBlobListing_ parámetro de hello **ListBlobsSegmentedAsync** too_false_ de método.

Como método de ejemplo de Hola llama a un método asincrónico, deben ir precedida por hello _async_ (palabra clave) y debe devolver un **tarea** objeto. Hola await palabra clave especificada para hello **ListBlobsSegmentedAsync** método suspende la ejecución del método de ejemplo hello hasta que se complete la tarea de la lista de hello.

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

## <a name="writing-tooan-append-blob"></a>Escritura tooan anexar blob
Un blob en anexos se optimiza para las operaciones de anexado, como el registro. Como un blob en bloques, un blob en anexos está formado por bloques, pero cuando se agrega un nuevo blob en bloques tooan anexado, siempre es toohello anexado final del blob de Hola. No se puede actualizar o eliminar un bloque existente en un blob en anexos. Identificadores de bloque de Hola para un blob en anexos no se exponen como sirven como un blob en bloques.

Cada bloque de un blob en anexos puede tener un tamaño diferente, la tooa máximo de 4 MB, y un blob en anexos puede incluir un máximo de 50.000 bloques. tamaño máximo de Hola de un blob en anexos, por tanto, es un poco más de 195 GB (4 MB X 50.000 bloques).

ejemplo de Hola siguiente crea un nuevo blob en anexos y anexa algunos tooit de datos, simular una operación de registro simple.

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

Vea [descripción Blobs en bloques, Blobs de página y anexar Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) para obtener más información acerca de las diferencias de hello entre tipos de hello tres de blobs.

## <a name="managing-security-for-blobs"></a>Administración de la seguridad para blobs
De forma predeterminada, el almacenamiento de Azure protege los datos mediante la limitación de propietario de la cuenta toohello acceso, que está en posesión de claves de acceso de cuenta de hello. Si necesita datos de blob de tooshare en su cuenta de almacenamiento, es importante toodo así sin comprometer la seguridad de Hola de las claves de acceso de cuenta. Además, puede cifrar tooensure de datos de blob que es seguro pasar a través de la conexión de Hola y el almacenamiento de Azure.

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a>Controlar el acceso a los datos tooblob
De forma predeterminada, los datos de blob de hello en su cuenta de almacenamiento son accesible sólo propietario de la cuenta toostorage. Autenticar las solicitudes en el almacenamiento de blobs requiere la clave de acceso de cuenta de hello de forma predeterminada. Sin embargo, quizá prefiera toomake ciertos usuarios disponibles tooother de datos de blob. Tiene dos opciones:

* **Acceso anónimo:** puede hacer que un contenedor o sus blobs estén públicamente disponibles para el acceso anónimo. Vea [administrar toocontainers de acceso de lectura anónimo y los blobs](storage-manage-access-to-resources.md) para obtener más información.
* **Firmas de acceso compartido:** puede proporcionar a los clientes con una firma de acceso compartido (SAS), que proporciona acceso delegado tooa recursos en la cuenta de almacenamiento con los permisos que especifican y a través de un intervalo que especifique. Consulte [Uso de firmas de acceso compartido (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para más información.

### <a name="encrypting-blob-data"></a>Cifrado de datos Blob
Almacenamiento de Azure admite el cifrado de datos de blob en el cliente de Hola y en el servidor de hello:

* **Cifrado en el cliente:** Hola biblioteca cliente de almacenamiento para .NET admite el cifrado de los datos dentro de las aplicaciones cliente antes de cargar tooAzure almacenamiento y descifrar los datos mientras se descargaba toohello cliente. biblioteca de Hello también admite la integración con el almacén de claves de Azure para administración de claves de cuenta de almacenamiento. Consulte [Cifrado del lado de cliente y Almacén de claves de Azure para el Almacenamiento de Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para más información. Consulte también [Tutorial: Cifrado y descifrado de blobs en Almacenamiento de Microsoft Azure con Almacén de claves de Azure](storage-encrypt-decrypt-blobs-key-vault.md).
* **Cifrado en el servidor**: Almacenamiento de Azure ahora admite el cifrado en el servidor. Consulte [Cifrado del servicio Almacenamiento de Azure para datos en reposo (versión preliminar)](../common/storage-service-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de blobs, siga estas toolearn de vínculos más.

### <a name="microsoft-azure-storage-explorer"></a>Explorador de almacenamiento de Microsoft Azure
* [Explorador de almacenamiento de Azure de Microsoft (MASE)](../../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.

### <a name="blob-storage-samples"></a>Ejemplos de Almacenamiento de blobs
* [Introducción a almacenamiento de blobs de Azure en .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Referencia de Almacenamiento de blobs
* [Referencia de la biblioteca de clientes de almacenamiento para .NET](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [Referencia de API de REST](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>Guías conceptuales
* [Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Introducción al Almacenamiento de archivos para .NET](../files/storage-dotnet-how-to-use-files.md)
* [¿Cómo toouse Azure blob storage con hello SDK de WebJobs](../../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
