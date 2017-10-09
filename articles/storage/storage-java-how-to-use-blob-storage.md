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
# <a name="how-toouse-blob-storage-from-java"></a><span data-ttu-id="ddcda-103">¿Cómo toouse almacenamiento de blobs desde Java</span><span class="sxs-lookup"><span data-stu-id="ddcda-103">How toouse Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="ddcda-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ddcda-104">Overview</span></span>
<span data-ttu-id="ddcda-105">Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="ddcda-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="ddcda-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ddcda-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="ddcda-107">Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="ddcda-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="ddcda-108">En este artículo le mostrará cómo tooperform escenarios comunes con Hola almacenamiento de blobs de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ddcda-108">This article will show you how tooperform common scenarios using hello Microsoft Azure Blob storage.</span></span> <span data-ttu-id="ddcda-109">ejemplos de Hello están escritos en Java y usar hello [almacenamiento de Azure SDK para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="ddcda-109">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="ddcda-110">Hello escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="ddcda-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="ddcda-111">Para obtener más información sobre los blobs, vea hello [pasos](#Next-Steps) sección.</span><span class="sxs-lookup"><span data-stu-id="ddcda-111">For more information on blobs, see hello [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="ddcda-112">hay un SDK disponible para los desarrolladores que usen el almacenamiento de Azure en dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="ddcda-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="ddcda-113">Para obtener más información, vea hello [SDK de almacenamiento de Azure para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="ddcda-113">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="ddcda-114">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="ddcda-114">Create a Java application</span></span>
<span data-ttu-id="ddcda-115">En este artículo usará funciones del almacenamiento que puede ejecutar en una aplicación Java localmente, o bien mediante código a través de un rol web o de un rol de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="ddcda-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="ddcda-116">toodo por lo tanto, necesitará tooinstall Hola Java Development Kit (JDK) y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="ddcda-116">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="ddcda-117">Una vez que lo ha hecho, necesitará tooverify que el sistema de desarrollo cumple los requisitos mínimos de Hola y dependencias que se enumeran en hello [almacenamiento de Azure SDK para Java] [ Azure Storage SDK for Java] repositorio en GitHub.</span><span class="sxs-lookup"><span data-stu-id="ddcda-117">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="ddcda-118">Si su sistema cumple estos requisitos, puede seguir las instrucciones de Hola para descargar e instalar Hola bibliotecas de almacenamiento de Azure para Java en el sistema de ese repositorio.</span><span class="sxs-lookup"><span data-stu-id="ddcda-118">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="ddcda-119">Una vez haya completado estas tareas, será capaz de toocreate una aplicación Java que utiliza los ejemplos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="ddcda-119">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="ddcda-120">Configurar el almacenamiento de blobs de aplicación tooaccess</span><span class="sxs-lookup"><span data-stu-id="ddcda-120">Configure your application tooaccess Blob storage</span></span>
<span data-ttu-id="ddcda-121">Agregar Hola después de la parte superior de toohello de instrucciones de importación del archivo de Java de hello en el que desea toouse hello las API de almacenamiento de Azure tooaccess blobs.</span><span class="sxs-lookup"><span data-stu-id="ddcda-121">Add hello following import statements toohello top of hello Java file where you want toouse hello Azure Storage APIs tooaccess blobs.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="ddcda-122">Configuración de una cadena de conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ddcda-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="ddcda-123">Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="ddcda-123">An Azure Storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="ddcda-124">Cuando se ejecuta en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato, con nombre de hello de la cuenta de almacenamiento y Hola clave de acceso principal para cuenta de almacenamiento Hola Hola [portal de Azure](https://portal.azure.com)para hello *AccountName* y *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="ddcda-124">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="ddcda-125">Hello en el ejemplo siguiente se muestra cómo se puede declarar una cadena de conexión de campo estático toohold Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcda-125">hello following example shows how you can declare a static field toohold hello connection string.</span></span>

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="ddcda-126">En una aplicación en ejecución dentro de un rol en Microsoft Azure, esta cadena puede almacenarse en el archivo de configuración del servicio de hello *ServiceConfiguration.cscfg*y puede tener acceso mediante una llamada a toohello  **RoleEnvironment.getConfigurationSettings** método.</span><span class="sxs-lookup"><span data-stu-id="ddcda-126">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="ddcda-127">Hello en el ejemplo siguiente se obtiene la cadena de conexión Hola un **configuración** elemento denominado *StorageConnectionString* en el archivo de configuración de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcda-127">hello following example gets hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="ddcda-128">Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcda-128">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="ddcda-129">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="ddcda-129">Create a container</span></span>
<span data-ttu-id="ddcda-130">Los objetos **CloudBlobClient** le permiten obtener objetos de referencia para los contenedores y los blobs.</span><span class="sxs-lookup"><span data-stu-id="ddcda-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="ddcda-131">Hello código siguiente se crea un **CloudBlobClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="ddcda-131">hello following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="ddcda-132">Hay otras formas toocreate **CloudStorageAccount** objetos; para obtener más información, vea **CloudStorageAccount** en hello [referencia de SDK de cliente de almacenamiento de Azure].</span><span class="sxs-lookup"><span data-stu-id="ddcda-132">There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="ddcda-133">Hola de uso **CloudBlobClient** tooget un contenedor de toohello de referencia que desee toouse del objeto.</span><span class="sxs-lookup"><span data-stu-id="ddcda-133">Use hello **CloudBlobClient** object tooget a reference toohello container you want toouse.</span></span> <span data-ttu-id="ddcda-134">Puede crear el contenedor de hello si no existe con hello **createIfNotExists** método, que en caso contrario, devolverá el contenedor existente Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcda-134">You can create hello container if it doesn't exist with hello **createIfNotExists** method, which will otherwise return hello existing container.</span></span> <span data-ttu-id="ddcda-135">De forma predeterminada, nuevo contenedor de hello es privado, por lo que debe especificar la clave de acceso de almacenamiento (como hizo anteriormente) blobs toodownload de este contenedor.</span><span class="sxs-lookup"><span data-stu-id="ddcda-135">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span>

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

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="ddcda-136">Opcional: configure un contenedor para acceso público.</span><span class="sxs-lookup"><span data-stu-id="ddcda-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="ddcda-137">Permisos del contenedor están configurados para el acceso privado de forma predeterminada, pero puede configurar con facilidad permisos tooallow público, de solo lectura acceso de un contenedor para todos los usuarios en hello Internet:</span><span class="sxs-lookup"><span data-stu-id="ddcda-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions tooallow public, read-only access for all users on hello Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="ddcda-138">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="ddcda-138">Upload a blob into a container</span></span>
<span data-ttu-id="ddcda-139">tooupload un blob de tooa de archivo, obtener una referencia de contenedor y usarlo tooget una referencia de blob.</span><span class="sxs-lookup"><span data-stu-id="ddcda-139">tooupload a file tooa blob, get a container reference and use it tooget a blob reference.</span></span> <span data-ttu-id="ddcda-140">Una vez que tenga una referencia de blob, puede cargar cualquier flujo mediante una llamada a cargar en la referencia de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcda-140">Once you have a blob reference, you can upload any stream by calling upload on hello blob reference.</span></span> <span data-ttu-id="ddcda-141">Esta operación creará blob Hola si no existe, o sobrescribir si existe.</span><span class="sxs-lookup"><span data-stu-id="ddcda-141">This operation will create hello blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="ddcda-142">Hola siguiendo el ejemplo de código muestra cómo hacerlo y supone que el contenedor de hello ya se ha creado.</span><span class="sxs-lookup"><span data-stu-id="ddcda-142">hello following code sample shows this, and assumes that hello container has already been created.</span></span>

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

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="ddcda-143">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="ddcda-143">List hello blobs in a container</span></span>
<span data-ttu-id="ddcda-144">blobs de hello toolist en un contenedor, obtenga primero una referencia de contenedor como hizo tooupload un blob.</span><span class="sxs-lookup"><span data-stu-id="ddcda-144">toolist hello blobs in a container, first get a container reference like you did tooupload a blob.</span></span> <span data-ttu-id="ddcda-145">Puede usar del contenedor de hello **listBlobs** método con un **para** bucle.</span><span class="sxs-lookup"><span data-stu-id="ddcda-145">You can use hello container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="ddcda-146">Hello código siguiente genera Hola Uri de cada blob en una consola de toohello de contenedor.</span><span class="sxs-lookup"><span data-stu-id="ddcda-146">hello following code outputs hello Uri of each blob in a container toohello console.</span></span>

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

<span data-ttu-id="ddcda-147">Puede asignar nombre a los blobs incluyendo información de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="ddcda-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="ddcda-148">De este modo crea una estructura de directorios virtuales que puede organizar y recorrer tal como lo haría en un sistema de archivos tradicional.</span><span class="sxs-lookup"><span data-stu-id="ddcda-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="ddcda-149">Tenga en cuenta que solo es virtual estructura de directorios de hello, hello únicamente los recursos disponibles en el almacenamiento de blobs son contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="ddcda-149">Note that hello directory structure is virtual only - hello only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="ddcda-150">Sin embargo, la biblioteca de cliente hello ofrece un **CloudBlobDirectory** objeto de directorio virtual de toorefer tooa y simplificar el proceso Hola de trabajar con los blobs que se organizan de esta manera.</span><span class="sxs-lookup"><span data-stu-id="ddcda-150">However, hello client library offers a **CloudBlobDirectory** object toorefer tooa virtual directory and simplify hello process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="ddcda-151">Por ejemplo, puede disponer de un contenedor con el nombre "photos", en el que puede cargar blobs con los nombres "rootphoto1", "2010/photo1", "2010/photo2" y "2011/photo1".</span><span class="sxs-lookup"><span data-stu-id="ddcda-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="ddcda-152">Esto crearía Hola directorios virtuales "2010" y "2011" en el contenedor de "fotos" Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcda-152">This would create hello virtual directories "2010" and "2011" within hello "photos" container.</span></span> <span data-ttu-id="ddcda-153">Cuando se llama a **listBlobs** en el contenedor de "fotos" Hola, colección Hola devuelta contendrá **CloudBlobDirectory** y **CloudBlob** objetos que representan Hola los directorios y blobs incluidos en el nivel superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcda-153">When you call **listBlobs** on hello "photos" container, hello collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing hello directories and blobs contained at hello top level.</span></span> <span data-ttu-id="ddcda-154">En este caso, se devolverán los directorios "2010" y "2011" y la foto "rootphoto1".</span><span class="sxs-lookup"><span data-stu-id="ddcda-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="ddcda-155">Puede usar hello **instanceof** operador toodistinguish estos objetos.</span><span class="sxs-lookup"><span data-stu-id="ddcda-155">You can use hello **instanceof** operator toodistinguish these objects.</span></span>

<span data-ttu-id="ddcda-156">Si lo desea, puede pasar parámetros toohello **listBlobs** método con hello **useFlatBlobListing** parámetro establece tootrue.</span><span class="sxs-lookup"><span data-stu-id="ddcda-156">Optionally, you can pass in parameters toohello **listBlobs** method with hello **useFlatBlobListing** parameter set tootrue.</span></span> <span data-ttu-id="ddcda-157">De este modo, se devuelven todos los blobs con independencia del directorio.</span><span class="sxs-lookup"><span data-stu-id="ddcda-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="ddcda-158">Para obtener más información, consulte **CloudBlobContainer.listBlobs** en hello [referencia de SDK de cliente de almacenamiento de Azure].</span><span class="sxs-lookup"><span data-stu-id="ddcda-158">For more information, see **CloudBlobContainer.listBlobs** in hello [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="ddcda-159">Descarga de un blob</span><span class="sxs-lookup"><span data-stu-id="ddcda-159">Download a blob</span></span>
<span data-ttu-id="ddcda-160">los blobs toodownload, siga Hola mismo pasos tal y como lo hizo para cargar un blob en orden tooget una referencia de blob.</span><span class="sxs-lookup"><span data-stu-id="ddcda-160">toodownload blobs, follow hello same steps as you did for uploading a blob in order tooget a blob reference.</span></span> <span data-ttu-id="ddcda-161">En cargar ejemplo Hola se llamó carga en el objeto de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="ddcda-161">In hello uploading example, you called upload on hello blob object.</span></span> <span data-ttu-id="ddcda-162">En el siguiente ejemplo de Hola, llame al objeto de flujo de descarga tootransfer Hola blob contenido tooa como un **clase FileOutputStream** que puede usar el archivo local de toopersist hello blob tooa.</span><span class="sxs-lookup"><span data-stu-id="ddcda-162">In hello following example, call download tootransfer hello blob contents tooa stream object such as a **FileOutputStream** that you can use toopersist hello blob tooa local file.</span></span>

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

## <a name="delete-a-blob"></a><span data-ttu-id="ddcda-163">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="ddcda-163">Delete a blob</span></span>
<span data-ttu-id="ddcda-164">toodelete un blob, obtener un blob de referencia y llame a **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="ddcda-164">toodelete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="ddcda-165">un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="ddcda-165">Delete a blob container</span></span>
<span data-ttu-id="ddcda-166">Por último, toodelete un contenedor de blobs, obtener un blob de referencia de contenedor y llame a **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="ddcda-166">Finally, toodelete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ddcda-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ddcda-167">Next steps</span></span>
<span data-ttu-id="ddcda-168">Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de blobs, siga estas toolearn vínculos acerca de las tareas más complejas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ddcda-168">Now that you've learned hello basics of Blob storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="ddcda-169">[SDK de Azure Storage para Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="ddcda-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="ddcda-170">[referencia de SDK de cliente de almacenamiento de Azure][referencia de SDK de cliente de almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="ddcda-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="ddcda-171">[API de REST de Azure Storage][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="ddcda-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="ddcda-172">[Blog del equipo de Azure Storage][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="ddcda-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="ddcda-173">Para obtener más información, vea también hello [Centro para desarrolladores de Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="ddcda-173">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referencia de SDK de cliente de almacenamiento de Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
