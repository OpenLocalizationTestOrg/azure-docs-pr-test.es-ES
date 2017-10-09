---
title: aaaHow toouse (almacenamiento de objetos) de almacenamiento de blobs de Azure en Java | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 6dd6efdf688161c32b9d73a65fa7f3a98f2fad74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a>¿Cómo toouse almacenamiento de blobs desde Java
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Información general
Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs. El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación. Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.

En este artículo le mostrará cómo tooperform escenarios comunes con Hola almacenamiento de blobs de Microsoft Azure. ejemplos de Hello están escritos en Java y usar hello [almacenamiento de Azure SDK para Java][Azure Storage SDK for Java]. Hello escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs. Para obtener más información sobre los blobs, vea hello [pasos](#Next-Steps) sección.

> [!NOTE]
> hay un SDK disponible para los desarrolladores que usen el almacenamiento de Azure en dispositivos Android. Para obtener más información, vea hello [SDK de almacenamiento de Azure para Android][Azure Storage SDK for Android].
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Creación de una aplicación Java
En este artículo usará funciones del almacenamiento que puede ejecutar en una aplicación Java localmente, o bien mediante código a través de un rol web o de un rol de trabajo de Azure.

toodo por lo tanto, necesitará tooinstall Hola Java Development Kit (JDK) y crear una cuenta de almacenamiento de Azure en su suscripción de Azure. Una vez que lo ha hecho, necesitará tooverify que el sistema de desarrollo cumple los requisitos mínimos de Hola y dependencias que se enumeran en hello [almacenamiento de Azure SDK para Java] [ Azure Storage SDK for Java] repositorio en GitHub. Si su sistema cumple estos requisitos, puede seguir las instrucciones de Hola para descargar e instalar Hola bibliotecas de almacenamiento de Azure para Java en el sistema de ese repositorio. Una vez haya completado estas tareas, será capaz de toocreate una aplicación Java que utiliza los ejemplos de hello en este artículo.

## <a name="configure-your-application-tooaccess-blob-storage"></a>Configurar el almacenamiento de blobs de aplicación tooaccess
Agregar Hola después de la parte superior de toohello de instrucciones de importación del archivo de Java de hello en el que desea toouse hello las API de almacenamiento de Azure tooaccess blobs.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configuración de una cadena de conexión de Almacenamiento de Azure
Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos. Cuando se ejecuta en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato, con nombre de hello de la cuenta de almacenamiento y Hola clave de acceso principal para cuenta de almacenamiento Hola Hola [portal de Azure](https://portal.azure.com)para hello *AccountName* y *AccountKey* valores. Hello en el ejemplo siguiente se muestra cómo se puede declarar una cadena de conexión de campo estático toohold Hola.

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

En una aplicación en ejecución dentro de un rol en Microsoft Azure, esta cadena puede almacenarse en el archivo de configuración del servicio de hello *ServiceConfiguration.cscfg*y puede tener acceso mediante una llamada a toohello  **RoleEnvironment.getConfigurationSettings** método. Hello en el ejemplo siguiente se obtiene la cadena de conexión Hola un **configuración** elemento denominado *StorageConnectionString* en el archivo de configuración de servicio de Hola.

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.

## <a name="create-a-container"></a>Crear un contenedor
Los objetos **CloudBlobClient** le permiten obtener objetos de referencia para los contenedores y los blobs. Hello código siguiente se crea un **CloudBlobClient** objeto.

> [!NOTE]
> Hay otras formas toocreate **CloudStorageAccount** objetos; para obtener más información, vea **CloudStorageAccount** en hello [referencia de SDK de cliente de almacenamiento de Azure].
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Hola de uso **CloudBlobClient** tooget un contenedor de toohello de referencia que desee toouse del objeto. Puede crear el contenedor de hello si no existe con hello **createIfNotExists** método, que en caso contrario, devolverá el contenedor existente Hola. De forma predeterminada, nuevo contenedor de hello es privado, por lo que debe especificar la clave de acceso de almacenamiento (como hizo anteriormente) blobs toodownload de este contenedor.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>Opcional: configure un contenedor para acceso público.
Permisos del contenedor están configurados para el acceso privado de forma predeterminada, pero puede configurar con facilidad permisos tooallow público, de solo lectura acceso de un contenedor para todos los usuarios en hello Internet:

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>Cargar un blob en un contenedor
tooupload un blob de tooa de archivo, obtener una referencia de contenedor y usarlo tooget una referencia de blob. Una vez que tenga una referencia de blob, puede cargar cualquier flujo mediante una llamada a cargar en la referencia de blob de Hola. Esta operación creará blob Hola si no existe, o sobrescribir si existe. Hola siguiendo el ejemplo de código muestra cómo hacerlo y supone que el contenedor de hello ya se ha creado.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a>Lista de blobs de hello en un contenedor
blobs de hello toolist en un contenedor, obtenga primero una referencia de contenedor como hizo tooupload un blob. Puede usar del contenedor de hello **listBlobs** método con un **para** bucle. Hello código siguiente genera Hola Uri de cada blob en una consola de toohello de contenedor.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Puede asignar nombre a los blobs incluyendo información de ruta de acceso. De este modo crea una estructura de directorios virtuales que puede organizar y recorrer tal como lo haría en un sistema de archivos tradicional. Tenga en cuenta que solo es virtual estructura de directorios de hello, hello únicamente los recursos disponibles en el almacenamiento de blobs son contenedores y blobs. Sin embargo, la biblioteca de cliente hello ofrece un **CloudBlobDirectory** objeto de directorio virtual de toorefer tooa y simplificar el proceso Hola de trabajar con los blobs que se organizan de esta manera.

Por ejemplo, puede disponer de un contenedor con el nombre "photos", en el que puede cargar blobs con los nombres "rootphoto1", "2010/photo1", "2010/photo2" y "2011/photo1". Esto crearía Hola directorios virtuales "2010" y "2011" en el contenedor de "fotos" Hola. Cuando se llama a **listBlobs** en el contenedor de "fotos" Hola, colección Hola devuelta contendrá **CloudBlobDirectory** y **CloudBlob** objetos que representan Hola los directorios y blobs incluidos en el nivel superior de Hola. En este caso, se devolverán los directorios "2010" y "2011" y la foto "rootphoto1". Puede usar hello **instanceof** operador toodistinguish estos objetos.

Si lo desea, puede pasar parámetros toohello **listBlobs** método con hello **useFlatBlobListing** parámetro establece tootrue. De este modo, se devuelven todos los blobs con independencia del directorio. Para obtener más información, consulte **CloudBlobContainer.listBlobs** en hello [referencia de SDK de cliente de almacenamiento de Azure].

## <a name="download-a-blob"></a>Descarga de un blob
los blobs toodownload, siga Hola mismo pasos tal y como lo hizo para cargar un blob en orden tooget una referencia de blob. En cargar ejemplo Hola se llamó carga en el objeto de blob de Hola. En el siguiente ejemplo de Hola, llame al objeto de flujo de descarga tootransfer Hola blob contenido tooa como un **clase FileOutputStream** que puede usar el archivo local de toopersist hello blob tooa.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>Eliminar un blob
toodelete un blob, obtener un blob de referencia y llame a **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>un contenedor de blobs
Por último, toodelete un contenedor de blobs, obtener un blob de referencia de contenedor y llame a **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de blobs, siga estas toolearn vínculos acerca de las tareas más complejas de almacenamiento.

* [SDK de Azure Storage para Java][Azure Storage SDK for Java]
* [referencia de SDK de cliente de almacenamiento de Azure][referencia de SDK de cliente de almacenamiento de Azure]
* [API de REST de Azure Storage][Azure Storage REST API]
* [Blog del equipo de Azure Storage][Azure Storage Team Blog]

Para obtener más información, vea también hello [Centro para desarrolladores de Java](/develop/java/).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referencia de SDK de cliente de almacenamiento de Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
