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
# <a name="develop-for-azure-file-storage-with-java"></a>Desarrollo para Azure File Storage con Java
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>Acerca de este tutorial
En este tutorial se muestran los aspectos básicos del uso de Java para desarrollar aplicaciones o servicios que usan Azure File Storage para almacenar datos de archivos. En este tutorial, se creará una aplicación de consola simple y se mostrará cómo realizar acciones básicas con Java y Azure File Storage:

* Crear y eliminar recursos compartidos de Azure File
* Crear y eliminar directorios
* Enumerar los archivos y directorios de un recurso compartido de Azure File
* Cargar, descargar y eliminar un archivo

> [!Note]  
> Dado que se puede tener acceso a Azure File Storage a través de SMB, es posible escribir aplicaciones sencillas que tengan acceso al recurso de Azure File mediante las clases estándar de E/S de Java. En este artículo se describe cómo escribir aplicaciones que usan el SDK de Java de Azure Storage, que emplea la [API de REST de Azure File Storage](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) para comunicarse con Azure File Storage.

## <a name="create-a-java-application"></a>Creación de una aplicación Java
Para compilar las muestras, se necesitará el Kit de desarrollo de Java (JDK) y el [SDK de Almacenamiento de Azure para Java][]. También deberá haber creado una cuenta de almacenamiento de Azure.

## <a name="setup-your-application-to-use-azure-file-storage"></a>Configuración de la aplicación para usar Azure File Storage
Para utilizar las API de almacenamiento de Azure, agregue la siguiente instrucción al principio del archivo Java desde el que desea acceder al servicio de almacenamiento.

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Configuración de una cadena de conexión de almacenamiento de Azure
Para usar Azure File Storage, necesita conectarse a la cuenta de almacenamiento de Azure. El primer paso sería configurar una cadena de conexión que se utilizará para establecer la conexión con su cuenta de almacenamiento. Definamos una variable estática para hacerlo.

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Reemplace your_storage_account_name y your_storage_account_key por los valores reales de la cuenta de almacenamiento.
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a>Conexión a una cuenta de almacenamiento de Azure
Para conectarse a su cuenta de almacenamiento, deberá usar el objeto **CloudStorageAccount**, pasando una cadena de conexión a su método de **análisis**.

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

**CloudStorageAccount.parse** produce una InvalidKeyException, por lo que deberá colocarla dentro de un bloque try/catch.

## <a name="create-an-azure-file-share"></a>Creación de un recurso compartido de Azure File
Todos los archivos y directorios de Azure File Storage residen en un contenedor denominado **Share**. La cuenta de almacenamiento puede tener tantos recursos compartidos como los que permita la capacidad de su cuenta. Para obtener acceso a un recurso compartido y su contenido, debe usar un cliente de Azure File Storage.

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

Con dicho cliente, puede obtener luego una referencia a un recurso compartido.

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

Para crear el recurso compartido, utilice el método **createIfNotExists** del objeto CloudFileShare.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

En este punto, **share** contiene una referencia a un recurso compartido denominado **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Eliminación de un recurso compartido de Azure File
Para eliminar un recurso compartido es necesario efectuar una llamada al método **deleteIfExists** en un objeto CloudFileShare. A continuación se facilita código de ejemplo que lo hace.

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

## <a name="create-a-directory"></a>Creación de directorios
También puede organizar el almacenamiento colocando archivos dentro de los subdirectorios en lugar de mantenerlos a todos en el directorio raíz. Azure File Storage le permite crear tantos directorios como permita su cuenta. El código siguiente creará un subdirectorio denominado **sampledir** bajo el directorio raíz.

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

## <a name="delete-a-directory"></a>Eliminación de un directorio
Eliminar un directorio es una tarea bastante sencilla, aunque se debe tener en cuenta que no se puede eliminar un directorio que contenga archivos u otros directorios.

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar los archivos y directorios de un recurso compartido de Azure File
Obtener una lista de archivos y directorios dentro de un recurso compartido se realiza fácilmente mediante una llamada a **listFilesAndDirectories** en una referencia de CloudFileDirectory. El método devuelve una lista de objetos ListFileItem en los que puede efectuar la iteración. Por ejemplo, el siguiente código enumerará archivos y directorios dentro del directorio raíz.

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Cargar un archivo
Un recurso compartido de Azure File contiene como mínimo un directorio raíz donde pueden residir los archivos. En esta sección, aprenderá cómo cargar un archivo del almacenamiento local en el directorio raíz de un recurso compartido.

El primer paso para cargar un archivo es obtener una referencia al directorio donde debe residir. Para ello, llame al método **getRootDirectoryReference** del objeto del recurso compartido.

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Ahora que tiene una referencia al directorio raíz del recurso compartido, puede cargar un archivo en él utilizando el código siguiente.

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Descarga de un archivo
Una de las operaciones más frecuentes que se llevará a cabo en Azure File Storage es la descarga de archivos. En el ejemplo siguiente, el código descarga el archivo SampleFile.txt y muestra su contenido.

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

## <a name="delete-a-file"></a>Eliminación de un archivo
Otra operación común de Azure File Storage es la eliminación de archivos. El código siguiente elimina un archivo denominado SampleFile.txt que se almacena en un directorio denominado **sampledir**.

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

## <a name="next-steps"></a>Pasos siguientes
Si desea obtener más información acerca de otras API de almacenamiento de Azure, siga estos vínculos.

* [Azure para desarrolladores de Java](/java/azure)/)
* [SDK de almacenamiento de Azure para Java](https://github.com/azure/azure-storage-java)
* [SDK de almacenamiento de Azure para Android](https://github.com/azure/azure-storage-android)
* [Referencia del SDK del cliente de Azure Storage](http://dl.windowsazure.com/storage/javadoc/)
* [API de REST de servicios de Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Transferencia de datos con la utilidad en línea de comandos AzCopy](../common/storage-use-azcopy.md* [Troubleshooting Azure File storage problems - Windows](storage-troubleshoot-windows-file-connection-problems.md)
)