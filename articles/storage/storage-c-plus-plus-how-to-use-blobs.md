---
title: Uso de Blob Storage (almacenamiento de objetos) en C++ | Microsoft Docs
description: Almacene datos no estructurados en la nube con Almacenamiento de blobs (objetos) de Azure.
services: storage
documentationcenter: .net
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 53844120-1c48-4e2f-8f77-5359ed0147a4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 3f28fbee4e267ab6962e2f73af5af6461cc16448
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-blob-storage-from-c"></a><span data-ttu-id="c938e-103">Cómo usar el almacenamiento de blobs de C++</span><span class="sxs-lookup"><span data-stu-id="c938e-103">How to use Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="c938e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c938e-104">Overview</span></span>
<span data-ttu-id="c938e-105">Almacenamiento de blobs de Azure es un servicio que almacena datos no estructurados en la nube como objetos o blobs.</span><span class="sxs-lookup"><span data-stu-id="c938e-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="c938e-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="c938e-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="c938e-107">El Almacenamiento de blobs a veces se conoce como "almacenamiento de objetos".</span><span class="sxs-lookup"><span data-stu-id="c938e-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="c938e-108">Esta guía demuestra cómo realizar algunas tareas comunes a través del servicio de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="c938e-108">This guide will demonstrate how to perform common scenarios using the Azure Blob storage service.</span></span> <span data-ttu-id="c938e-109">Los ejemplos están escritos en C++ y usan la [biblioteca de cliente de almacenamiento de Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="c938e-109">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="c938e-110">Entre los escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="c938e-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="c938e-111">Esta guía se destina a la biblioteca de cliente de almacenamiento de Azure para C++, versión 1.0.0 y posteriores.</span><span class="sxs-lookup"><span data-stu-id="c938e-111">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="c938e-112">La versión recomendada es la biblioteca de cliente de almacenamiento 2.2.0, que se encuentra disponible a través de [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="c938e-112">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="c938e-113">Creación de una aplicación de C++</span><span class="sxs-lookup"><span data-stu-id="c938e-113">Create a C++ application</span></span>
<span data-ttu-id="c938e-114">En esta guía, usará las características de almacenamiento que se pueden ejecutar en una aplicación C++.</span><span class="sxs-lookup"><span data-stu-id="c938e-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="c938e-115">Para ello, deberá instalar la biblioteca de cliente de almacenamiento de Azure para C++ y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c938e-115">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="c938e-116">Para instalar la biblioteca de cliente de almacenamiento de Azure para C++, puede usar los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c938e-116">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="c938e-117">**Linux:** siga las instrucciones indicadas en la página [Léame de la biblioteca de cliente de almacenamiento de Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="c938e-117">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="c938e-118">**Windows:** en Visual Studio, haga clic en **Herramientas > Administrador de paquetes de NuGet > Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="c938e-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="c938e-119">Escriba el siguiente comando en la [Consola del Administrador de paquetes de NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="c938e-119">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="c938e-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="c938e-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="c938e-121">Configuración de su aplicación para obtener acceso al almacenamiento de blobs</span><span class="sxs-lookup"><span data-stu-id="c938e-121">Configure your application to access Blob Storage</span></span>
<span data-ttu-id="c938e-122">Agregue las siguientes instrucciones include en la parte superior del archivo C++ en el que desea usar las API de almacenamiento de Azure para obtener acceso a los blobs:</span><span class="sxs-lookup"><span data-stu-id="c938e-122">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="c938e-123">Configuración de una cadena de conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c938e-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="c938e-124">Un cliente de almacenamiento de Azure utiliza una cadena de conexión de almacenamiento para almacenar extremos y credenciales con el fin de obtener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="c938e-124">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="c938e-125">Al ejecutarse en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento en el siguiente formato, usando el nombre de su cuenta de almacenamiento y la clave de acceso de almacenamiento de la cuenta de almacenamiento que se muestra en [Azure Portal](https://portal.azure.com) para los valores *AccountName* y *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="c938e-125">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="c938e-126">Para obtener información sobre las cuentas de almacenamiento y las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="c938e-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="c938e-127">En este ejemplo se muestra cómo puede declarar un campo estático para mantener la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="c938e-127">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="c938e-128">Para probar la aplicación en el equipo local de Windows, puede usar Microsoft Azure [Storage Emulator](storage-use-emulator.md) que se instala con [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c938e-128">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="c938e-129">El emulador de almacenamiento es una utilidad que simula los servicios Blob, Cola y Tabla disponibles en Azure en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="c938e-129">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="c938e-130">En el ejemplo siguiente se muestra cómo puede declarar un campo estático para mantener la cadena de conexión en el emulador de almacenamiento local:</span><span class="sxs-lookup"><span data-stu-id="c938e-130">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="c938e-131">Para iniciar Azure Storage Emulator, seleccione el botón **Inicio** o pulse la tecla **Windows**.</span><span class="sxs-lookup"><span data-stu-id="c938e-131">To start the Azure storage emulator, Select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="c938e-132">Comience a escribir **Azure Storage Emulator** y seleccione **Emulador de Microsoft Azure Storage** en la lista de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c938e-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="c938e-133">En los ejemplos siguientes se supone que usó uno de estos dos métodos para obtener la cadena de conexión de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c938e-133">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="c938e-134">Recuperación de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="c938e-134">Retrieve your connection string</span></span>
<span data-ttu-id="c938e-135">Puede usar la clase **cloud_storage_account** para representar la información de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c938e-135">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="c938e-136">Para recuperar la información de la cuenta de almacenamiento a partir de la cadena de conexión de almacenamiento, puede usar el método **parse** .</span><span class="sxs-lookup"><span data-stu-id="c938e-136">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="c938e-137">A continuación, obtenga una referencia a una clase **cloud_blob_client**, ya que le permite recuperar objetos que representan contenedores y blobs almacenados en el servicio Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c938e-137">Next, get a reference to a **cloud_blob_client** class as it allows you to retrieve objects that represent containers and blobs stored within the Blob Storage Service.</span></span> <span data-ttu-id="c938e-138">El código siguiente crea un objeto **cloud_blob_client** usando el objeto de cuenta de almacenamiento recuperado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="c938e-138">The following code creates a **cloud_blob_client** object using the storage account object we retrieved above:</span></span>  

```cpp
// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="c938e-139">Cómo crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="c938e-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="c938e-140">En este ejemplo se muestra cómo crear un contenedor si todavía no existe:</span><span class="sxs-lookup"><span data-stu-id="c938e-140">This example shows how to create a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create the blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference to a container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create the container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="c938e-141">De manera predeterminada, el nuevo contenedor es privado y debe especificar su clave de acceso de almacenamiento para descargar blobs de él.</span><span class="sxs-lookup"><span data-stu-id="c938e-141">By default, the new container is private and you must specify your storage access key to download blobs from this container.</span></span> <span data-ttu-id="c938e-142">Si desea poner los archivos (blobs) del contenedor a disposición de todo el mundo, puede convertir el contenedor en público usando el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="c938e-142">If you want to make the files (blobs) within the container available to everyone, you can set the container to be public using the following code:</span></span>  

```cpp
// Make the blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="c938e-143">Cualquier usuario de Internet puede ver los blobs de los contenedores públicos, pero solo es posible modificarlos o eliminarlos si se dispone de la clave de acceso apropiada.</span><span class="sxs-lookup"><span data-stu-id="c938e-143">Anyone on the Internet can see blobs in a public container, but you can modify or delete them only if you have the appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="c938e-144">Cómo cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="c938e-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="c938e-145">El almacenamiento de blobs de Azure admite blobs en bloques y en páginas.</span><span class="sxs-lookup"><span data-stu-id="c938e-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="c938e-146">En la mayoría de los casos, se recomienda usar blobs en bloques.</span><span class="sxs-lookup"><span data-stu-id="c938e-146">In the majority of cases, block blob is the recommended type to use.</span></span>  

<span data-ttu-id="c938e-147">Para cargar un archivo en un blob en bloques, obtenga una referencia de contenedor y utilícela para obtener una referencia de blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="c938e-147">To upload a file to a block blob, get a container reference and use it to get a block blob reference.</span></span> <span data-ttu-id="c938e-148">Una vez que disponga de la referencia de blob, puede cargar cualquier flujo de datos en ella llamando al método **upload_from_stream**.</span><span class="sxs-lookup"><span data-stu-id="c938e-148">Once you have a blob reference, you can upload any stream of data to it by calling the **upload_from_stream** method.</span></span> <span data-ttu-id="c938e-149">De este modo, se creará el blob si no existía anteriormente, o bien se sobrescribirá si ya existía.</span><span class="sxs-lookup"><span data-stu-id="c938e-149">This operation will create the blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="c938e-150">En el siguiente ejemplo se muestra cómo cargar un blob en un contenedor creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c938e-150">The following example shows how to upload a blob into a container and assumes that the container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite the "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite the "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference to a blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="c938e-151">Como alternativa, puede usar el método **upload_from_file** para cargar un archivo en un blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="c938e-151">Alternatively, you can use the **upload_from_file** method to upload a file to a block blob.</span></span>

## <a name="how-to-list-the-blobs-in-a-container"></a><span data-ttu-id="c938e-152">Cómo enumerar los blobs en un contenedor</span><span class="sxs-lookup"><span data-stu-id="c938e-152">How to: List the blobs in a container</span></span>
<span data-ttu-id="c938e-153">Para enumerar los blobs de un contenedor, primero obtenga una referencia de contenedor.</span><span class="sxs-lookup"><span data-stu-id="c938e-153">To list the blobs in a container, first get a container reference.</span></span> <span data-ttu-id="c938e-154">A continuación, puede usar el método **list_blobs** del contenedor para recuperar los blobs y los directorios que contiene.</span><span class="sxs-lookup"><span data-stu-id="c938e-154">You can then use the container's **list_blobs** method to retrieve the blobs and/or directories within it.</span></span> <span data-ttu-id="c938e-155">Para obtener acceso al conjunto completo de propiedades y métodos de un elemento **list_blob_item** devuelto, debe realizar una llamada al método **list_blob_item.as_blob** para obtener un objeto **cloud_blob** o al método **list_blob.as_directory** para obtener un objeto cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="c938e-155">To access the rich set of properties and methods for a returned **list_blob_item**, you must call the **list_blob_item.as_blob** method to get a  **cloud_blob** object, or the **list_blob.as_directory** method to get a  cloud_blob_directory object.</span></span> <span data-ttu-id="c938e-156">El código siguiente muestra cómo recuperar y consultar el URI de cada elemento del contenedor **my-sample-container** :</span><span class="sxs-lookup"><span data-stu-id="c938e-156">The following code demonstrates how to retrieve and output the URI of each item in the **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Output URI of each item.
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        std::wcout << U("Blob: ") << it->as_blob().uri().primary_uri().to_string() << std::endl;
    }
    else
    {
        std::wcout << U("Directory: ") << it->as_directory().uri().primary_uri().to_string() << std::endl;
    }
}
```

<span data-ttu-id="c938e-157">Para obtener más información sobre cómo enumerar las operaciones, consulte [Enumeración de recursos de almacenamiento de Azure en C++](storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="c938e-157">For more details on listing operations, see [List Azure Storage Resources in C++](storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="c938e-158">Cómo descargar blobs</span><span class="sxs-lookup"><span data-stu-id="c938e-158">How to: Download blobs</span></span>
<span data-ttu-id="c938e-159">Para descargar blobs, primero recupere una referencia de blob y, a continuación, llame al método **download_to_stream**.</span><span class="sxs-lookup"><span data-stu-id="c938e-159">To download blobs, first retrieve a blob reference and then call the **download_to_stream** method.</span></span> <span data-ttu-id="c938e-160">En el siguiente ejemplo, se usa el método **download_to_stream** para transferir el contenido del blob a un objeto de flujo que, a continuación, puede guardar en un archivo local.</span><span class="sxs-lookup"><span data-stu-id="c938e-160">The following example uses the **download_to_stream** method to transfer the blob contents to a stream object that you can then persist to a local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents to a file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="c938e-161">Como alternativa, puede usar el método **download_to_file** para descargar el contenido de un blob en un archivo.</span><span class="sxs-lookup"><span data-stu-id="c938e-161">Alternatively, you can use the **download_to_file** method to download the contents of a blob to a file.</span></span>
<span data-ttu-id="c938e-162">También puede usar el método **download_text** para descargar el contenido de un blob en forma de cadena de texto.</span><span class="sxs-lookup"><span data-stu-id="c938e-162">In addition, you can also use the **download_text** method to download the contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download the contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="c938e-163">Cómo eliminar blobs</span><span class="sxs-lookup"><span data-stu-id="c938e-163">How to: Delete blobs</span></span>
<span data-ttu-id="c938e-164">Para eliminar un blob, primero obtenga una referencia de blob y, a continuación, llame al método **delete_blob** en ella.</span><span class="sxs-lookup"><span data-stu-id="c938e-164">To delete a blob, first get a blob reference and then call the **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference to a previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference to a blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete the blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="c938e-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c938e-165">Next steps</span></span>
<span data-ttu-id="c938e-166">Ahora que está familiarizado con los aspectos básicos del almacenamiento de blobs, siga estos vínculos para obtener más información sobre Almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="c938e-166">Now that you've learned the basics of blob storage, follow these links to learn more about Azure Storage.</span></span>  

* [<span data-ttu-id="c938e-167">Cómo usar el almacenamiento de colas de C++</span><span class="sxs-lookup"><span data-stu-id="c938e-167">How to use Queue Storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="c938e-168">Cómo usar el almacenamiento de tablas de C++</span><span class="sxs-lookup"><span data-stu-id="c938e-168">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="c938e-169">Enumeración de los recursos de almacenamiento de Azure en C++</span><span class="sxs-lookup"><span data-stu-id="c938e-169">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="c938e-170">Referencia de la biblioteca de clientes de almacenamiento para C++</span><span class="sxs-lookup"><span data-stu-id="c938e-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="c938e-171">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="c938e-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="c938e-172">Introducción a la utilidad de línea de comandos AzCopy</span><span class="sxs-lookup"><span data-stu-id="c938e-172">Transfer data with the AzCopy command-line utility</span></span>](storage-use-azcopy.md)

