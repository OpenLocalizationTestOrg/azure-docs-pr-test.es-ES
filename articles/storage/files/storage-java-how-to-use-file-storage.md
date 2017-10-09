---
title: aaaDevelop para el almacenamiento de archivos de Azure con Java | Documentos de Microsoft
description: "Obtenga información acerca de cómo las aplicaciones de Java de toodevelop y servicios que usen toostore de almacenamiento de archivos de Azure datos de archivos."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: be71a946604da8af0130f101f2eb6135c5e08abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="273a0-103">Desarrollo para Azure File Storage con Java</span><span class="sxs-lookup"><span data-stu-id="273a0-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="273a0-104">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="273a0-104">About this tutorial</span></span>
<span data-ttu-id="273a0-105">Este tutorial demuestra conceptos básicos de hello del uso de aplicaciones de Java toodevelop o servicios que usan datos de archivos de toostore de almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="273a0-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="273a0-106">En este tutorial, crearemos una aplicación de consola simple y mostrar cómo tooperform acciones básicas con el almacenamiento de Java y archivos de Azure:</span><span class="sxs-lookup"><span data-stu-id="273a0-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="273a0-107">Crear y eliminar recursos compartidos de Azure File</span><span class="sxs-lookup"><span data-stu-id="273a0-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="273a0-108">Crear y eliminar directorios</span><span class="sxs-lookup"><span data-stu-id="273a0-108">Create and delete directories</span></span>
* <span data-ttu-id="273a0-109">Enumerar los archivos y directorios de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="273a0-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="273a0-110">Cargar, descargar y eliminar un archivo</span><span class="sxs-lookup"><span data-stu-id="273a0-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="273a0-111">Dado que puede tener acceso al almacenamiento de archivos de Azure a través de SMB, es posible toowrite aplicaciones simples que tienen acceso a recurso compartido de archivos de Azure de hello mediante clases de E/S de Java estándares de Hola.</span><span class="sxs-lookup"><span data-stu-id="273a0-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="273a0-112">En este artículo se describe cómo las aplicaciones de toowrite que utilizan Hola SDK de Java de almacenamiento de Azure, que usa hello [API de REST de almacenamiento de archivos de Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure almacenamiento de archivos.</span><span class="sxs-lookup"><span data-stu-id="273a0-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="273a0-113">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="273a0-113">Create a Java application</span></span>
<span data-ttu-id="273a0-114">ejemplos de hello toobuild, necesitará Hola Java Development Kit (JDK) y [] Hola [SDK de almacenamiento de Azure para Java].</span><span class="sxs-lookup"><span data-stu-id="273a0-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="273a0-115">También deberá haber creado una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="273a0-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="273a0-116">Configurar el almacenamiento de Azure archivos de aplicación toouse</span><span class="sxs-lookup"><span data-stu-id="273a0-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="273a0-117">Hola toouse API, el almacenamiento de Azure agregar Hola después de la parte superior de toohello de instrucción del archivo de Java de Hola donde piensa tooaccess servicio de almacenamiento de hello en.</span><span class="sxs-lookup"><span data-stu-id="273a0-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="273a0-118">Configuración de una cadena de conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="273a0-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="273a0-119">toouse almacenamiento de archivos de Azure, debe tooconnect tooyour cuenta de almacenamiento Azure.</span><span class="sxs-lookup"><span data-stu-id="273a0-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="273a0-120">Hello primer paso sería tooconfigure una cadena de conexión que vamos a usar cuenta de almacenamiento de tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="273a0-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="273a0-121">Vamos a definir un toodo variable estática que.</span><span class="sxs-lookup"><span data-stu-id="273a0-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="273a0-122">Reemplace your_storage_account_name y your_storage_account_key con valores reales de hello para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="273a0-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="273a0-123">Conexión de cuenta de almacenamiento de Azure tooan</span><span class="sxs-lookup"><span data-stu-id="273a0-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="273a0-124">cuenta de almacenamiento de tooconnect tooyour, necesita hello toouse **CloudStorageAccount** objeto, pasando una tooits de cadena de conexión **analizar** método.</span><span class="sxs-lookup"><span data-stu-id="273a0-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="273a0-125">**CloudStorageAccount.parse** inicia una InvalidKeyException por lo que necesitará tooput dentro de un bloque try/catch bloquear.</span><span class="sxs-lookup"><span data-stu-id="273a0-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="273a0-126">Creación de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="273a0-126">Create an Azure File share</span></span>
<span data-ttu-id="273a0-127">Todos los archivos y directorios de Azure File Storage residen en un contenedor denominado **Share**.</span><span class="sxs-lookup"><span data-stu-id="273a0-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="273a0-128">La cuenta de almacenamiento puede tener tantos recursos compartidos como los que permita la capacidad de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="273a0-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="273a0-129">recurso compartido de tooobtain acceso tooa y su contenido, deberá toouse un cliente de almacenamiento de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="273a0-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="273a0-130">Utiliza el cliente de almacenamiento de archivos de Azure de hello, a continuación, puede obtener un recurso compartido tooa de referencia.</span><span class="sxs-lookup"><span data-stu-id="273a0-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="273a0-131">tooactually crear recurso compartido de hello, use hello **createIfNotExists** método del objeto de CloudFileShare Hola.</span><span class="sxs-lookup"><span data-stu-id="273a0-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="273a0-132">En este momento, **compartir** contiene un recurso compartido de tooa de referencia denominado **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="273a0-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="273a0-133">Eliminación de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="273a0-133">Delete an Azure File share</span></span>
<span data-ttu-id="273a0-134">Eliminar un recurso compartido se realiza mediante llamada hello **deleteIfExists** método en un objeto CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="273a0-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="273a0-135">A continuación se facilita código de ejemplo que lo hace.</span><span class="sxs-lookup"><span data-stu-id="273a0-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="273a0-136">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="273a0-136">Create a directory</span></span>
<span data-ttu-id="273a0-137">También puede organizar el almacenamiento de información colocando archivos dentro de los subdirectorios en lugar de tener todos ellos en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="273a0-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="273a0-138">Almacenamiento de archivos de Azure le permite toocreate, tal y como hacen mucho directorios como la cuenta.</span><span class="sxs-lookup"><span data-stu-id="273a0-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="273a0-139">código de Hello siguiente creará un subdirectorio denominado **sampledir** en el directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="273a0-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="273a0-140">Eliminación de un directorio</span><span class="sxs-lookup"><span data-stu-id="273a0-140">Delete a directory</span></span>
<span data-ttu-id="273a0-141">Eliminar un directorio es una tarea bastante sencilla, aunque se debe tener en cuenta que no se puede eliminar un directorio que contenga archivos u otros directorios.</span><span class="sxs-lookup"><span data-stu-id="273a0-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="273a0-142">Enumerar los archivos y directorios de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="273a0-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="273a0-143">Obtener una lista de archivos y directorios dentro de un recurso compartido se realiza fácilmente mediante una llamada a **listFilesAndDirectories** en una referencia de CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="273a0-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="273a0-144">método Hello devuelve una lista de objetos de ListFileItem que puede iterar en.</span><span class="sxs-lookup"><span data-stu-id="273a0-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="273a0-145">Por ejemplo, hello código siguiente mostrará una lista de archivos y directorios dentro del directorio raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="273a0-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="273a0-146">Cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="273a0-146">Upload a file</span></span>
<span data-ttu-id="273a0-147">Un archivo de Azure recurso compartido contiene en hello muy menos, un directorio raíz donde los archivos pueden encontrarse.</span><span class="sxs-lookup"><span data-stu-id="273a0-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="273a0-148">En esta sección, aprenderá cómo tooupload un archivo de almacenamiento local en hello raíz del directorio de un recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="273a0-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="273a0-149">Hola primer paso para cargar un archivo es tooobtain un directorio de toohello de referencia en el que debe reside.</span><span class="sxs-lookup"><span data-stu-id="273a0-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="273a0-150">Para ello, que realiza la llamada hello **getRootDirectoryReference** método del objeto de recurso compartido de Hola.</span><span class="sxs-lookup"><span data-stu-id="273a0-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="273a0-151">Ahora que tiene un directorio de raíz de referencia toohello del recurso compartido de hello, puede cargar un archivo en él mediante el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="273a0-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="273a0-152">Descarga de un archivo</span><span class="sxs-lookup"><span data-stu-id="273a0-152">Download a file</span></span>
<span data-ttu-id="273a0-153">Uno de hello más frecuentan las operaciones que se llevará a cabo en el almacenamiento de archivos de Azure es archivos de toodownload.</span><span class="sxs-lookup"><span data-stu-id="273a0-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="273a0-154">En el siguiente ejemplo de Hola, código de hello descarga SampleFile.txt y muestra su contenido.</span><span class="sxs-lookup"><span data-stu-id="273a0-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="273a0-155">Eliminación de un archivo</span><span class="sxs-lookup"><span data-stu-id="273a0-155">Delete a file</span></span>
<span data-ttu-id="273a0-156">Otra operación común de Azure File Storage es la eliminación de archivos.</span><span class="sxs-lookup"><span data-stu-id="273a0-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="273a0-157">Hello código siguiente elimina un archivo denominado SampleFile.txt que se almacenan en un directorio denominado **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="273a0-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="273a0-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="273a0-158">Next steps</span></span>
<span data-ttu-id="273a0-159">Si desea que toolearn más información acerca de otra API de almacenamiento de Azure, siga estos vínculos.</span><span class="sxs-lookup"><span data-stu-id="273a0-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* <span data-ttu-id="273a0-160">[Azure para desarrolladores de Java](/java/azure)/)</span><span class="sxs-lookup"><span data-stu-id="273a0-160">[Azure for Java developers](/java/azure)/)</span></span>
* [<span data-ttu-id="273a0-161">SDK de almacenamiento de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="273a0-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="273a0-162">SDK de almacenamiento de Azure para Android</span><span class="sxs-lookup"><span data-stu-id="273a0-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="273a0-163">Referencia del SDK del cliente de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="273a0-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="273a0-164">API de REST de servicios de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="273a0-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="273a0-165">Blog del equipo de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="273a0-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="273a0-166">[Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span><span class="sxs-lookup"><span data-stu-id="273a0-166">[Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span></span>