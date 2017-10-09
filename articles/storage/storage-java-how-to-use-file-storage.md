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
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>Desarrollo para Azure File Storage con Java
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>Acerca de este tutorial
Este tutorial demuestra conceptos básicos de hello del uso de aplicaciones de Java toodevelop o servicios que usan datos de archivos de toostore de almacenamiento de archivos de Azure. En este tutorial, crearemos una aplicación de consola simple y mostrar cómo tooperform acciones básicas con el almacenamiento de Java y archivos de Azure:

* Crear y eliminar recursos compartidos de Azure File
* Crear y eliminar directorios
* Enumerar los archivos y directorios de un recurso compartido de Azure File
* Cargar, descargar y eliminar un archivo

> [!Note]  
> Dado que puede tener acceso al almacenamiento de archivos de Azure a través de SMB, es posible toowrite aplicaciones simples que tienen acceso a recurso compartido de archivos de Azure de hello mediante clases de E/S de Java estándares de Hola. En este artículo se describe cómo las aplicaciones de toowrite que utilizan Hola SDK de Java de almacenamiento de Azure, que usa hello [API de REST de almacenamiento de archivos de Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure almacenamiento de archivos.

## <a name="create-a-java-application"></a>Creación de una aplicación Java
ejemplos de hello toobuild, necesitará Hola Java Development Kit (JDK) y [] Hola [SDK de almacenamiento de Azure para Java]. También deberá haber creado una cuenta de almacenamiento de Azure.

## <a name="setup-your-application-toouse-azure-file-storage"></a>Configurar el almacenamiento de Azure archivos de aplicación toouse
Hola toouse API, el almacenamiento de Azure agregar Hola después de la parte superior de toohello de instrucción del archivo de Java de Hola donde piensa tooaccess servicio de almacenamiento de hello en.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Configuración de una cadena de conexión de almacenamiento de Azure
toouse almacenamiento de archivos de Azure, debe tooconnect tooyour cuenta de almacenamiento Azure. Hello primer paso sería tooconfigure una cadena de conexión que vamos a usar cuenta de almacenamiento de tooconnect tooyour. Vamos a definir un toodo variable estática que.

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Reemplace your_storage_account_name y your_storage_account_key con valores reales de hello para la cuenta de almacenamiento.
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>Conexión de cuenta de almacenamiento de Azure tooan
cuenta de almacenamiento de tooconnect tooyour, necesita hello toouse **CloudStorageAccount** objeto, pasando una tooits de cadena de conexión **analizar** método.

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse** inicia una InvalidKeyException por lo que necesitará tooput dentro de un bloque try/catch bloquear.

## <a name="create-an-azure-file-share"></a>Creación de un recurso compartido de Azure File
Todos los archivos y directorios de Azure File Storage residen en un contenedor denominado **Share**. La cuenta de almacenamiento puede tener tantos recursos compartidos como los que permita la capacidad de su cuenta. recurso compartido de tooobtain acceso tooa y su contenido, deberá toouse un cliente de almacenamiento de archivos de Azure.

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

Utiliza el cliente de almacenamiento de archivos de Azure de hello, a continuación, puede obtener un recurso compartido tooa de referencia.

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually crear recurso compartido de hello, use hello **createIfNotExists** método del objeto de CloudFileShare Hola.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

En este momento, **compartir** contiene un recurso compartido de tooa de referencia denominado **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Eliminación de un recurso compartido de Azure File
Eliminar un recurso compartido se realiza mediante llamada hello **deleteIfExists** método en un objeto CloudFileShare. A continuación se facilita código de ejemplo que lo hace.

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

## <a name="create-a-directory"></a>Creación de directorios
También puede organizar el almacenamiento de información colocando archivos dentro de los subdirectorios en lugar de tener todos ellos en el directorio raíz de Hola. Almacenamiento de archivos de Azure le permite toocreate, tal y como hacen mucho directorios como la cuenta. código de Hello siguiente creará un subdirectorio denominado **sampledir** en el directorio raíz de Hola.

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

## <a name="delete-a-directory"></a>Eliminación de un directorio
Eliminar un directorio es una tarea bastante sencilla, aunque se debe tener en cuenta que no se puede eliminar un directorio que contenga archivos u otros directorios.

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar los archivos y directorios de un recurso compartido de Azure File
Obtener una lista de archivos y directorios dentro de un recurso compartido se realiza fácilmente mediante una llamada a **listFilesAndDirectories** en una referencia de CloudFileDirectory. método Hello devuelve una lista de objetos de ListFileItem que puede iterar en. Por ejemplo, hello código siguiente mostrará una lista de archivos y directorios dentro del directorio raíz de Hola.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Cargar un archivo
Un archivo de Azure recurso compartido contiene en hello muy menos, un directorio raíz donde los archivos pueden encontrarse. En esta sección, aprenderá cómo tooupload un archivo de almacenamiento local en hello raíz del directorio de un recurso compartido.

Hola primer paso para cargar un archivo es tooobtain un directorio de toohello de referencia en el que debe reside. Para ello, que realiza la llamada hello **getRootDirectoryReference** método del objeto de recurso compartido de Hola.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Ahora que tiene un directorio de raíz de referencia toohello del recurso compartido de hello, puede cargar un archivo en él mediante el siguiente código de hello.

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Descarga de un archivo
Uno de hello más frecuentan las operaciones que se llevará a cabo en el almacenamiento de archivos de Azure es archivos de toodownload. En el siguiente ejemplo de Hola, código de hello descarga SampleFile.txt y muestra su contenido.

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

## <a name="delete-a-file"></a>Eliminación de un archivo
Otra operación común de Azure File Storage es la eliminación de archivos. Hello código siguiente elimina un archivo denominado SampleFile.txt que se almacenan en un directorio denominado **sampledir**.

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

## <a name="next-steps"></a>Pasos siguientes
Si desea que toolearn más información acerca de otra API de almacenamiento de Azure, siga estos vínculos.

* [Centro de desarrolladores de Java](http://azure.microsoft.com/develop/java/)
* [SDK de almacenamiento de Azure para Java](https://github.com/azure/azure-storage-java)
* [SDK de almacenamiento de Azure para Android](https://github.com/azure/azure-storage-android)
* [Referencia del SDK del cliente de Azure Storage](http://dl.windowsazure.com/storage/javadoc/)
* [API de REST de servicios de Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](storage-use-azcopy.md)
