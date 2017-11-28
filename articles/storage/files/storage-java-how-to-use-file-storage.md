---
title: Desarrollo para Azure File Storage con Java | Microsoft Docs
description: Aprenda a desarrollar aplicaciones y servicios Java que usan Azure File Storage para almacenar datos de archivos.
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
ms.openlocfilehash: ce38944b9d5e663505c5808864ba61a5e2284f3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="eb428-103">Desarrollo para Azure File Storage con Java</span><span class="sxs-lookup"><span data-stu-id="eb428-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="eb428-104">Acerca de este tutorial</span><span class="sxs-lookup"><span data-stu-id="eb428-104">About this tutorial</span></span>
<span data-ttu-id="eb428-105">En este tutorial se muestran los aspectos básicos del uso de Java para desarrollar aplicaciones o servicios que usan Azure File Storage para almacenar datos de archivos.</span><span class="sxs-lookup"><span data-stu-id="eb428-105">This tutorial will demonstrate the basics of using Java to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="eb428-106">En este tutorial, se creará una aplicación de consola simple y se mostrará cómo realizar acciones básicas con Java y Azure File Storage:</span><span class="sxs-lookup"><span data-stu-id="eb428-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="eb428-107">Crear y eliminar recursos compartidos de Azure File</span><span class="sxs-lookup"><span data-stu-id="eb428-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="eb428-108">Crear y eliminar directorios</span><span class="sxs-lookup"><span data-stu-id="eb428-108">Create and delete directories</span></span>
* <span data-ttu-id="eb428-109">Enumerar los archivos y directorios de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="eb428-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="eb428-110">Cargar, descargar y eliminar un archivo</span><span class="sxs-lookup"><span data-stu-id="eb428-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="eb428-111">Dado que se puede tener acceso a Azure File Storage a través de SMB, es posible escribir aplicaciones sencillas que tengan acceso al recurso de Azure File mediante las clases estándar de E/S de Java.</span><span class="sxs-lookup"><span data-stu-id="eb428-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Java I/O classes.</span></span> <span data-ttu-id="eb428-112">En este artículo se describe cómo escribir aplicaciones que usan el SDK de Java de Azure Storage, que emplea la [API de REST de Azure File Storage](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) para comunicarse con Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="eb428-112">This article will describe how to write applications that use the Azure Storage Java SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="eb428-113">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="eb428-113">Create a Java application</span></span>
<span data-ttu-id="eb428-114">Para compilar las muestras, se necesitará el Kit de desarrollo de Java (JDK) y el [SDK de Almacenamiento de Azure para Java][].</span><span class="sxs-lookup"><span data-stu-id="eb428-114">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="eb428-115">También deberá haber creado una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="eb428-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-to-use-azure-file-storage"></a><span data-ttu-id="eb428-116">Configuración de la aplicación para usar Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="eb428-116">Setup your application to use Azure File storage</span></span>
<span data-ttu-id="eb428-117">Para utilizar las API de almacenamiento de Azure, agregue la siguiente instrucción al principio del archivo Java desde el que desea acceder al servicio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eb428-117">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="eb428-118">Configuración de una cadena de conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="eb428-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="eb428-119">Para usar Azure File Storage, necesita conectarse a la cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="eb428-119">To use Azure File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="eb428-120">El primer paso sería configurar una cadena de conexión que se utilizará para establecer la conexión con su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eb428-120">The first step would be to configure a connection string which we'll use to connect to your storage account.</span></span> <span data-ttu-id="eb428-121">Definamos una variable estática para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="eb428-121">Let's define a static variable to do that.</span></span>

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="eb428-122">Reemplace your_storage_account_name y your_storage_account_key por los valores reales de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="eb428-122">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="eb428-123">Conexión a una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="eb428-123">Connecting to an Azure storage account</span></span>
<span data-ttu-id="eb428-124">Para conectarse a su cuenta de almacenamiento, deberá usar el objeto **CloudStorageAccount**, pasando una cadena de conexión a su método de **análisis**.</span><span class="sxs-lookup"><span data-stu-id="eb428-124">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span></span>

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

<span data-ttu-id="eb428-125">**CloudStorageAccount.parse** produce una InvalidKeyException, por lo que deberá colocarla dentro de un bloque try/catch.</span><span class="sxs-lookup"><span data-stu-id="eb428-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="eb428-126">Creación de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="eb428-126">Create an Azure File share</span></span>
<span data-ttu-id="eb428-127">Todos los archivos y directorios de Azure File Storage residen en un contenedor denominado **Share**.</span><span class="sxs-lookup"><span data-stu-id="eb428-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="eb428-128">La cuenta de almacenamiento puede tener tantos recursos compartidos como los que permita la capacidad de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="eb428-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="eb428-129">Para obtener acceso a un recurso compartido y su contenido, debe usar un cliente de Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="eb428-129">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="eb428-130">Con dicho cliente, puede obtener luego una referencia a un recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="eb428-130">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="eb428-131">Para crear el recurso compartido, utilice el método **createIfNotExists** del objeto CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="eb428-131">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="eb428-132">En este punto, **share** contiene una referencia a un recurso compartido denominado **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="eb428-132">At this point, **share** holds a reference to a share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="eb428-133">Eliminación de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="eb428-133">Delete an Azure File share</span></span>
<span data-ttu-id="eb428-134">Para eliminar un recurso compartido es necesario efectuar una llamada al método **deleteIfExists** en un objeto CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="eb428-134">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="eb428-135">A continuación se facilita código de ejemplo que lo hace.</span><span class="sxs-lookup"><span data-stu-id="eb428-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference to the file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="eb428-136">Creación de directorios</span><span class="sxs-lookup"><span data-stu-id="eb428-136">Create a directory</span></span>
<span data-ttu-id="eb428-137">También puede organizar el almacenamiento colocando archivos dentro de los subdirectorios en lugar de mantenerlos a todos en el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="eb428-137">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="eb428-138">Azure File Storage le permite crear tantos directorios como permita su cuenta.</span><span class="sxs-lookup"><span data-stu-id="eb428-138">Azure File storage allows you to create as much directories as your account will allow.</span></span> <span data-ttu-id="eb428-139">El código siguiente creará un subdirectorio denominado **sampledir** bajo el directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="eb428-139">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="eb428-140">Eliminación de un directorio</span><span class="sxs-lookup"><span data-stu-id="eb428-140">Delete a directory</span></span>
<span data-ttu-id="eb428-141">Eliminar un directorio es una tarea bastante sencilla, aunque se debe tener en cuenta que no se puede eliminar un directorio que contenga archivos u otros directorios.</span><span class="sxs-lookup"><span data-stu-id="eb428-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory you want to delete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete the directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="eb428-142">Enumerar los archivos y directorios de un recurso compartido de Azure File</span><span class="sxs-lookup"><span data-stu-id="eb428-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="eb428-143">Obtener una lista de archivos y directorios dentro de un recurso compartido se realiza fácilmente mediante una llamada a **listFilesAndDirectories** en una referencia de CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="eb428-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="eb428-144">El método devuelve una lista de objetos ListFileItem en los que puede efectuar la iteración.</span><span class="sxs-lookup"><span data-stu-id="eb428-144">The method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="eb428-145">Por ejemplo, el siguiente código enumerará archivos y directorios dentro del directorio raíz.</span><span class="sxs-lookup"><span data-stu-id="eb428-145">As an example, the following code will list files and directories inside the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="eb428-146">Cargar un archivo</span><span class="sxs-lookup"><span data-stu-id="eb428-146">Upload a file</span></span>
<span data-ttu-id="eb428-147">Un recurso compartido de Azure File contiene como mínimo un directorio raíz donde pueden residir los archivos.</span><span class="sxs-lookup"><span data-stu-id="eb428-147">An Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="eb428-148">En esta sección, aprenderá cómo cargar un archivo del almacenamiento local en el directorio raíz de un recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="eb428-148">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="eb428-149">El primer paso para cargar un archivo es obtener una referencia al directorio donde debe residir.</span><span class="sxs-lookup"><span data-stu-id="eb428-149">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="eb428-150">Para ello, llame al método **getRootDirectoryReference** del objeto del recurso compartido.</span><span class="sxs-lookup"><span data-stu-id="eb428-150">You do this by calling the **getRootDirectoryReference** method of the share object.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="eb428-151">Ahora que tiene una referencia al directorio raíz del recurso compartido, puede cargar un archivo en él utilizando el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="eb428-151">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span></span>

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="eb428-152">Descarga de un archivo</span><span class="sxs-lookup"><span data-stu-id="eb428-152">Download a file</span></span>
<span data-ttu-id="eb428-153">Una de las operaciones más frecuentes que se llevará a cabo en Azure File Storage es la descarga de archivos.</span><span class="sxs-lookup"><span data-stu-id="eb428-153">One of the more frequent operations you will perform against Azure File storage is to download files.</span></span> <span data-ttu-id="eb428-154">En el ejemplo siguiente, el código descarga el archivo SampleFile.txt y muestra su contenido.</span><span class="sxs-lookup"><span data-stu-id="eb428-154">In the following example, the code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the directory that contains the file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference to the file you want to download
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write the contents of the file to the console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="eb428-155">Eliminación de un archivo</span><span class="sxs-lookup"><span data-stu-id="eb428-155">Delete a file</span></span>
<span data-ttu-id="eb428-156">Otra operación común de Azure File Storage es la eliminación de archivos.</span><span class="sxs-lookup"><span data-stu-id="eb428-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="eb428-157">El código siguiente elimina un archivo denominado SampleFile.txt que se almacena en un directorio denominado **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="eb428-157">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory where the file to be deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="eb428-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eb428-158">Next steps</span></span>
<span data-ttu-id="eb428-159">Si desea obtener más información acerca de otras API de almacenamiento de Azure, siga estos vínculos.</span><span class="sxs-lookup"><span data-stu-id="eb428-159">If you would like to learn more about other Azure storage APIs, follow these links.</span></span>

* <span data-ttu-id="eb428-160">[Azure para desarrolladores de Java](/java/azure)/)</span><span class="sxs-lookup"><span data-stu-id="eb428-160">[Azure for Java developers](/java/azure)/)</span></span>
* [<span data-ttu-id="eb428-161">SDK de almacenamiento de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="eb428-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="eb428-162">SDK de almacenamiento de Azure para Android</span><span class="sxs-lookup"><span data-stu-id="eb428-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="eb428-163">Referencia del SDK del cliente de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="eb428-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="eb428-164">API de REST de servicios de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="eb428-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="eb428-165">Blog del equipo de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="eb428-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="eb428-166">[Transferencia de datos con la utilidad en línea de comandos AzCopy](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span><span class="sxs-lookup"><span data-stu-id="eb428-166">[Transfer data with the AzCopy Command-Line Utility](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)</span></span>