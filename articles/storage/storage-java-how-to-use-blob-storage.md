---
title: Uso de Azure Blob Storage (almacenamiento de objetos) en Java | Microsoft Docs
description: Almacene datos no estructurados en la nube con Almacenamiento de blobs (objetos) de Azure.
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
ms.openlocfilehash: b8a4eca600b458802a7a23851bb80ea4da2664ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-java"></a><span data-ttu-id="1cce7-103">Uso del almacenamiento de blobs de Java</span><span class="sxs-lookup"><span data-stu-id="1cce7-103">How to use Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="1cce7-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1cce7-104">Overview</span></span>
<span data-ttu-id="1cce7-105">Almacenamiento de blobs de Azure es un servicio que almacena datos no estructurados en la nube como objetos o blobs.</span><span class="sxs-lookup"><span data-stu-id="1cce7-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="1cce7-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1cce7-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="1cce7-107">El Almacenamiento de blobs a veces se conoce como "almacenamiento de objetos".</span><span class="sxs-lookup"><span data-stu-id="1cce7-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="1cce7-108">Este artículo le muestra cómo realizar algunas tareas comunes con Almacenamiento de blobs de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1cce7-108">This article will show you how to perform common scenarios using the Microsoft Azure Blob storage.</span></span> <span data-ttu-id="1cce7-109">Los ejemplos están escritos en Java y utilizan el [SDK de Azure Storage para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="1cce7-109">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="1cce7-110">Entre los escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="1cce7-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="1cce7-111">Para obtener más información sobre los blobs, consulte la sección [Pasos siguientes](#Next-Steps) .</span><span class="sxs-lookup"><span data-stu-id="1cce7-111">For more information on blobs, see the [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="1cce7-112">hay un SDK disponible para los desarrolladores que usen el almacenamiento de Azure en dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="1cce7-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="1cce7-113">Para obtener más información, vea el [SDK de Azure Storage para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="1cce7-113">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="1cce7-114">Creación de una aplicación Java</span><span class="sxs-lookup"><span data-stu-id="1cce7-114">Create a Java application</span></span>
<span data-ttu-id="1cce7-115">En este artículo usará funciones del almacenamiento que puede ejecutar en una aplicación Java localmente, o bien mediante código a través de un rol web o de un rol de trabajo de Azure.</span><span class="sxs-lookup"><span data-stu-id="1cce7-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="1cce7-116">Para ello, deberá instalar el Kit de desarrollo de Java (JDK) y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="1cce7-116">To do so, you will need to install the Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="1cce7-117">Después, deberá verificar que su sistema de desarrollo satisface los requisitos mínimos y las dependencias que se indican en el repositorio del [SDK de Azure Storage para Java][Azure Storage SDK for Java] en GitHub.</span><span class="sxs-lookup"><span data-stu-id="1cce7-117">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="1cce7-118">Si su sistema cumple esos requisitos, puede seguir las instrucciones para descargar e instalar las bibliotecas de almacenamiento de Azure para Java en su sistema desde ese repositorio.</span><span class="sxs-lookup"><span data-stu-id="1cce7-118">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="1cce7-119">Cuando haya completado esas tareas, podrá crear una aplicación Java que use los ejemplos de este artículo.</span><span class="sxs-lookup"><span data-stu-id="1cce7-119">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="1cce7-120">Configuración de su aplicación para obtener acceso al almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="1cce7-120">Configure your application to access Blob storage</span></span>
<span data-ttu-id="1cce7-121">Agregue las siguientes instrucciones de importación al principio del archivo Java en el que desea usar las API de Almacenamiento de Azure para obtener acceso a los blobs.</span><span class="sxs-lookup"><span data-stu-id="1cce7-121">Add the following import statements to the top of the Java file where you want to use the Azure Storage APIs to access blobs.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="1cce7-122">Configuración de una cadena de conexión de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="1cce7-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="1cce7-123">Un cliente de Almacenamiento de Azure usa una cadena de conexión de almacenamiento para almacenar extremos y credenciales con el fin de obtener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="1cce7-123">An Azure Storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="1cce7-124">Al ejecutarse en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento en el siguiente formato, usando el nombre de su cuenta de almacenamiento y la clave de acceso principal de la cuenta de almacenamiento que se muestra en [Azure Portal](https://portal.azure.com) para los valores *AccountName* y *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="1cce7-124">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="1cce7-125">En el ejemplo a continuación se muestra cómo puede declarar un campo estático para mantener la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="1cce7-125">The following example shows how you can declare a static field to hold the connection string.</span></span>

```java
// Define the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="1cce7-126">En una aplicación que se esté ejecutando en un rol de Microsoft Azure, esta cadena se puede almacenar en el archivo de configuración de servicio, *ServiceConfiguration.cscfg*, y se puede obtener acceso a él con una llamada al método **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="1cce7-126">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="1cce7-127">A continuación, se muestra un ejemplo de cómo obtener la cadena de conexión desde un elemento de **configuración** denominado *StorageConnectionString* en el archivo de configuración de servicio.</span><span class="sxs-lookup"><span data-stu-id="1cce7-127">The following example gets the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="1cce7-128">En los ejemplos siguientes se supone que usó uno de estos dos métodos para obtener la cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="1cce7-128">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="1cce7-129">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="1cce7-129">Create a container</span></span>
<span data-ttu-id="1cce7-130">Los objetos **CloudBlobClient** le permiten obtener objetos de referencia para los contenedores y los blobs.</span><span class="sxs-lookup"><span data-stu-id="1cce7-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="1cce7-131">El siguiente código crea un objeto **CloudBlobClient** .</span><span class="sxs-lookup"><span data-stu-id="1cce7-131">The following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="1cce7-132">Existen otras maneras de crear objetos **CloudStorageAccount**. Para más información, consulte **CloudStorageAccount** en la [Referencia del SDK del cliente de Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="1cce7-132">There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="1cce7-133">Utilice el objeto **CloudBlobClient** para obtener una referencia al contenedor que desea utilizar.</span><span class="sxs-lookup"><span data-stu-id="1cce7-133">Use the **CloudBlobClient** object to get a reference to the container you want to use.</span></span> <span data-ttu-id="1cce7-134">Puede crear el contenedor si no existe con el método **createIfNotExists** , que devolverá el contenedor existente.</span><span class="sxs-lookup"><span data-stu-id="1cce7-134">You can create the container if it doesn't exist with the **createIfNotExists** method, which will otherwise return the existing container.</span></span> <span data-ttu-id="1cce7-135">De manera predeterminada, el nuevo contenedor es privado, por lo que tiene que especificar su clave de acceso de almacenamiento (como hizo anteriormente) para descargar blobs de él.</span><span class="sxs-lookup"><span data-stu-id="1cce7-135">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference to a container.
    // The container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create the container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="1cce7-136">Opcional: configure un contenedor para acceso público.</span><span class="sxs-lookup"><span data-stu-id="1cce7-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="1cce7-137">Los permisos de un contenedor están configurados para acceso privado de forma predeterminada, pero puede configurarlos fácilmente para permitir acceso público de solo lectura a todos los usuarios de Internet:</span><span class="sxs-lookup"><span data-stu-id="1cce7-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions to allow public, read-only access for all users on the Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in the permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set the permissions on the container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="1cce7-138">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="1cce7-138">Upload a blob into a container</span></span>
<span data-ttu-id="1cce7-139">Para cargar un archivo en un blob, obtenga una referencia de contenedor y utilícela para obtener una referencia de blob.</span><span class="sxs-lookup"><span data-stu-id="1cce7-139">To upload a file to a blob, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="1cce7-140">Una vez tenga una referencia de blob, puede cargar cualquier flujo mediante una llamada de carga en la referencia del blob.</span><span class="sxs-lookup"><span data-stu-id="1cce7-140">Once you have a blob reference, you can upload any stream by calling upload on the blob reference.</span></span> <span data-ttu-id="1cce7-141">De este modo, se creará el blob si no existe, o bien se sobrescribirá si ya existe.</span><span class="sxs-lookup"><span data-stu-id="1cce7-141">This operation will create the blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="1cce7-142">El siguiente ejemplo de código muestra esto y presupone que ya se ha creado el contenedor.</span><span class="sxs-lookup"><span data-stu-id="1cce7-142">The following code sample shows this, and assumes that the container has already been created.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define the path to a local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite the "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="1cce7-143">Enumerar los blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="1cce7-143">List the blobs in a container</span></span>
<span data-ttu-id="1cce7-144">Para enumerar los blobs de un contenedor, obtenga primero una referencia del contenedor del mismo modo que al cargar un blob.</span><span class="sxs-lookup"><span data-stu-id="1cce7-144">To list the blobs in a container, first get a container reference like you did to upload a blob.</span></span> <span data-ttu-id="1cce7-145">Puede usar el método **listBlobs** del contenedor con un bucle **for**.</span><span class="sxs-lookup"><span data-stu-id="1cce7-145">You can use the container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="1cce7-146">El código siguiente ofrece el Uri de todos los blobs de un contenedor a la consola.</span><span class="sxs-lookup"><span data-stu-id="1cce7-146">The following code outputs the Uri of each blob in a container to the console.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within the container and output the URI to each of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="1cce7-147">Puede asignar nombre a los blobs incluyendo información de ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="1cce7-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="1cce7-148">De este modo crea una estructura de directorios virtuales que puede organizar y recorrer tal como lo haría en un sistema de archivos tradicional.</span><span class="sxs-lookup"><span data-stu-id="1cce7-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="1cce7-149">Tenga en cuenta que la estructura de directorios es solo virtual: los únicos recursos disponibles en el almacenamiento de blobs son contenedores y blobs.</span><span class="sxs-lookup"><span data-stu-id="1cce7-149">Note that the directory structure is virtual only - the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="1cce7-150">Sin embargo, la biblioteca de clientes ofrece un objeto **CloudBlobDirectory** para hacer referencia a un directorio virtual y simplificar el proceso de trabajo con blobs organizados de este modo.</span><span class="sxs-lookup"><span data-stu-id="1cce7-150">However, the client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="1cce7-151">Por ejemplo, puede disponer de un contenedor con el nombre "photos", en el que puede cargar blobs con los nombres "rootphoto1", "2010/photo1", "2010/photo2" y "2011/photo1".</span><span class="sxs-lookup"><span data-stu-id="1cce7-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="1cce7-152">De esta forma, se crean los directorios virtuales "2010" y "2011" dentro del contenedor "photos".</span><span class="sxs-lookup"><span data-stu-id="1cce7-152">This would create the virtual directories "2010" and "2011" within the "photos" container.</span></span> <span data-ttu-id="1cce7-153">Al llamar a **listBlobs** en el contenedor "photos", la recopilación devuelta contendrá objetos **CloudBlobDirectory** y **CloudBlob** que representan los directorios y los blobs que existen en el nivel superior.</span><span class="sxs-lookup"><span data-stu-id="1cce7-153">When you call **listBlobs** on the "photos" container, the collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="1cce7-154">En este caso, se devolverán los directorios "2010" y "2011" y la foto "rootphoto1".</span><span class="sxs-lookup"><span data-stu-id="1cce7-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="1cce7-155">Puede utilizar el operador **instanceof** para distinguir estos objetos.</span><span class="sxs-lookup"><span data-stu-id="1cce7-155">You can use the **instanceof** operator to distinguish these objects.</span></span>

<span data-ttu-id="1cce7-156">Opcionalmente, puede pasar parámetros al método **listBlobs** con el parámetro **useFlatBlobListing** establecido en "true".</span><span class="sxs-lookup"><span data-stu-id="1cce7-156">Optionally, you can pass in parameters to the **listBlobs** method with the **useFlatBlobListing** parameter set to true.</span></span> <span data-ttu-id="1cce7-157">De este modo, se devuelven todos los blobs con independencia del directorio.</span><span class="sxs-lookup"><span data-stu-id="1cce7-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="1cce7-158">Para obtener más información, consulte **CloudBlobContainer.listBlobs** en la [Referencia del SDK del cliente de Azure Storage].</span><span class="sxs-lookup"><span data-stu-id="1cce7-158">For more information, see **CloudBlobContainer.listBlobs** in the [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="1cce7-159">Descarga de un blob</span><span class="sxs-lookup"><span data-stu-id="1cce7-159">Download a blob</span></span>
<span data-ttu-id="1cce7-160">Para descargar blobs, siga los mismos pasos que realizó para cargar un blob con el fin de obtener una referencia de blob.</span><span class="sxs-lookup"><span data-stu-id="1cce7-160">To download blobs, follow the same steps as you did for uploading a blob in order to get a blob reference.</span></span> <span data-ttu-id="1cce7-161">En el ejemplo de carga, llamó a la función upload en el objeto del blob.</span><span class="sxs-lookup"><span data-stu-id="1cce7-161">In the uploading example, you called upload on the blob object.</span></span> <span data-ttu-id="1cce7-162">En el siguiente ejemplo, llame a la función download para transferir los contenidos del blob a un objeto de secuencia como un **FileOutputStream** que puede utilizar para conservar el blob en un archivo local.</span><span class="sxs-lookup"><span data-stu-id="1cce7-162">In the following example, call download to transfer the blob contents to a stream object such as a **FileOutputStream** that you can use to persist the blob to a local file.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in the container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If the item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download the item and save it to a file with the same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="1cce7-163">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="1cce7-163">Delete a blob</span></span>
<span data-ttu-id="1cce7-164">Para eliminar un blob, obtenga una referencia del blob y llame a la función **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="1cce7-164">To delete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference to a blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete the blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="1cce7-165">un contenedor de blobs</span><span class="sxs-lookup"><span data-stu-id="1cce7-165">Delete a blob container</span></span>
<span data-ttu-id="1cce7-166">Por último, para eliminar un contenedor de blobs, obtenga una referencia al contenedor de blobs y llame a la función **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="1cce7-166">Finally, to delete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete the blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="1cce7-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1cce7-167">Next steps</span></span>
<span data-ttu-id="1cce7-168">Ahora que está familiarizado con los aspectos básicos del almacenamiento de blobs, use estos vínculos para obtener más información acerca de tareas de almacenamiento más complejas.</span><span class="sxs-lookup"><span data-stu-id="1cce7-168">Now that you've learned the basics of Blob storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="1cce7-169">[SDK de Azure Storage para Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="1cce7-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="1cce7-170">[Referencia del SDK del cliente de Azure Storage][Referencia del SDK del cliente de Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="1cce7-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="1cce7-171">[API de REST de Azure Storage][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="1cce7-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="1cce7-172">[Blog del equipo de Azure Storage][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="1cce7-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="1cce7-173">Para más información, consulte también el [Centro de desarrolladores de Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="1cce7-173">For more information, see also the [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="1cce7-174">[Referencia del SDK del cliente de Azure Storage]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="1cce7-174">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
