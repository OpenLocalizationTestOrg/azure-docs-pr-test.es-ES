---
title: almacenamiento de blobs de toouse aaaHow (almacenamiento de objetos) de C++ | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
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
ms.openlocfilehash: e63df4683e5c10c9f8fbe4106c655df61be0e1a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-c"></a><span data-ttu-id="af513-103">¿Cómo toouse almacenamiento de blobs de C++</span><span class="sxs-lookup"><span data-stu-id="af513-103">How toouse Blob Storage from C++</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="af513-104">Información general</span><span class="sxs-lookup"><span data-stu-id="af513-104">Overview</span></span>
<span data-ttu-id="af513-105">Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="af513-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="af513-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="af513-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="af513-107">Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="af513-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="af513-108">Esta guía demuestra cómo tooperform escenarios comunes con Hola servicio de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="af513-108">This guide will demonstrate how tooperform common scenarios using hello Azure Blob storage service.</span></span> <span data-ttu-id="af513-109">ejemplos de Hello están escritos en C++ y usar hello [biblioteca de cliente de almacenamiento de Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="af513-109">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="af513-110">Hello escenarios descritos se incluyen **cargar**, **enumerar**, **descargar**, y **eliminar** blobs.</span><span class="sxs-lookup"><span data-stu-id="af513-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span>  

> [!NOTE]
> <span data-ttu-id="af513-111">Destinos de esta guía Hola biblioteca de cliente de almacenamiento de Azure para C++ versión 1.0.0 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="af513-111">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="af513-112">Hola recomienda versión es la biblioteca de cliente de almacenamiento 2.2.0, que está disponible a través de [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="af513-112">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="af513-113">Creación de una aplicación de C++</span><span class="sxs-lookup"><span data-stu-id="af513-113">Create a C++ application</span></span>
<span data-ttu-id="af513-114">En esta guía, usará las características de almacenamiento que se pueden ejecutar en una aplicación C++.</span><span class="sxs-lookup"><span data-stu-id="af513-114">In this guide, you will use storage features which can be run within a C++ application.</span></span>  

<span data-ttu-id="af513-115">toodo por lo tanto, necesitará tooinstall Hola biblioteca de cliente de almacenamiento de Azure para C++ y crear una cuenta de almacenamiento de Azure en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="af513-115">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>   

<span data-ttu-id="af513-116">Hola tooinstall biblioteca de cliente de almacenamiento de Azure para C++, puede usar Hola siguientes métodos:</span><span class="sxs-lookup"><span data-stu-id="af513-116">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="af513-117">**Linux:** seguir instrucciones Hola de hello [biblioteca de cliente de almacenamiento de Azure para C++ Léame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="af513-117">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="af513-118">**Windows:** en Visual Studio, haga clic en **Herramientas &gt; Administrador de paquetes de NuGet &gt; Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="af513-118">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="af513-119">Escriba lo siguiente Hola de comandos en hello [consola de administrador de paquetes de NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="af513-119">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>  
  
     <span data-ttu-id="af513-120">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="af513-120">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-blob-storage"></a><span data-ttu-id="af513-121">Configurar el almacenamiento de blobs de aplicación tooaccess</span><span class="sxs-lookup"><span data-stu-id="af513-121">Configure your application tooaccess Blob Storage</span></span>
<span data-ttu-id="af513-122">Agregue el siguiente Hola incluye la parte superior de toohello de las instrucciones del archivo de C++ de hello en el que desea toouse Hola almacenamiento de Azure API tooaccess blobs:</span><span class="sxs-lookup"><span data-stu-id="af513-122">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess blobs:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/blob.h>
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="af513-123">Configuración de una cadena de conexión de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="af513-123">Setup an Azure storage connection string</span></span>
<span data-ttu-id="af513-124">Un cliente de almacenamiento de Azure usa un extremos de toostore de cadena de conexión de almacenamiento y las credenciales para tener acceso a los servicios de administración de datos.</span><span class="sxs-lookup"><span data-stu-id="af513-124">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="af513-125">Cuando se ejecuta en una aplicación cliente, debe proporcionar la cadena de conexión de almacenamiento de Hola Hola siguiendo el formato, utilizando el nombre de Hola de su clave de acceso almacenamiento hello y cuenta de almacenamiento para cuenta de almacenamiento Hola Hola [Portal de Azure](https://portal.azure.com)para hello *AccountName* y *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="af513-125">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="af513-126">Para obtener información sobre las cuentas de almacenamiento y las claves de acceso, consulte [Acerca de las cuentas de almacenamiento de Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="af513-126">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span> <span data-ttu-id="af513-127">Este ejemplo muestra cómo se puede declarar una cadena de conexión de campo estático toohold hello:</span><span class="sxs-lookup"><span data-stu-id="af513-127">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="af513-128">tootest la aplicación en el equipo local de Windows, puede usar Microsoft Azure hello [emulador de almacenamiento](../storage-use-emulator.md) que se instala con hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="af513-128">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="af513-129">emulador de almacenamiento de Hello es una utilidad que simula los servicios de Blob, cola y tabla de hello disponibles en Azure en su equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="af513-129">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="af513-130">Hello en el ejemplo siguiente se muestra cómo se puede declarar un emulador de almacenamiento local de campo estático toohold Hola conexión cadena tooyour:</span><span class="sxs-lookup"><span data-stu-id="af513-130">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="af513-131">emulador de almacenamiento de Azure de hello toostart, seleccione hello **iniciar** Hola o presionen **Windows** clave.</span><span class="sxs-lookup"><span data-stu-id="af513-131">toostart hello Azure storage emulator, Select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="af513-132">Comience a escribir **emulador de almacenamiento de Azure**y seleccione **emulador de almacenamiento de Microsoft Azure** de lista de Hola de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="af513-132">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="af513-133">Hello en los ejemplos siguientes se supone que ha usado uno de estos cadena de conexión de almacenamiento de dos métodos tooget Hola.</span><span class="sxs-lookup"><span data-stu-id="af513-133">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="af513-134">Recuperación de la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="af513-134">Retrieve your connection string</span></span>
<span data-ttu-id="af513-135">Puede usar hello **cloud_storage_account** clase toorepresent información de su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="af513-135">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="af513-136">tooretrieve información de cadena de conexión de almacenamiento de hello de la cuenta de almacenamiento, puede utilizar hello **analizar** método.</span><span class="sxs-lookup"><span data-stu-id="af513-136">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="af513-137">A continuación, obtener una referencia tooa **cloud_blob_client** clase puesto que permite tooretrieve objetos que representan contenedores y blobs almacenados en el servicio de almacenamiento Blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="af513-137">Next, get a reference tooa **cloud_blob_client** class as it allows you tooretrieve objects that represent containers and blobs stored within hello Blob Storage Service.</span></span> <span data-ttu-id="af513-138">Hello código siguiente se crea un **cloud_blob_client** objeto mediante el objeto de cuenta de almacenamiento Hola recuperamos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="af513-138">hello following code creates a **cloud_blob_client** object using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();  
```

## <a name="how-to-create-a-container"></a><span data-ttu-id="af513-139">Cómo crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="af513-139">How to: Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="af513-140">Este ejemplo se muestra cómo toocreate un contenedor si aún no existe:</span><span class="sxs-lookup"><span data-stu-id="af513-140">This example shows how toocreate a container if it does not already exist:</span></span>  

```cpp
try
{
    // Retrieve storage account from connection string.
    azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

    // Create hello blob client.
    azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

    // Retrieve a reference tooa container.
    azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

    // Create hello container if it doesn't already exist.
    container.create_if_not_exists();
}
catch (const std::exception& e)
{
    std::wcout << U("Error: ") << e.what() << std::endl;
}  
```

<span data-ttu-id="af513-141">De forma predeterminada, Hola nuevo contenedor es privado y debe especificar los blobs de toodownload clave de acceso de almacenamiento de este contenedor.</span><span class="sxs-lookup"><span data-stu-id="af513-141">By default, hello new container is private and you must specify your storage access key toodownload blobs from this container.</span></span> <span data-ttu-id="af513-142">Si desea que toomake Hola archivos (BLOB) en hello contenedor disponibles tooeveryone, puede establecer Hola contenedor toobe público mediante el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="af513-142">If you want toomake hello files (blobs) within hello container available tooeveryone, you can set hello container toobe public using hello following code:</span></span>  

```cpp
// Make hello blob container publicly accessible.
azure::storage::blob_container_permissions permissions;
permissions.set_public_access(azure::storage::blob_container_public_access_type::blob);
container.upload_permissions(permissions);  
```

<span data-ttu-id="af513-143">Todos los usuarios de hello Internet pueden ver los blobs en un contenedor público, pero puede modificar o eliminarlos únicamente si tiene la clave de acceso adecuado de Hola.</span><span class="sxs-lookup"><span data-stu-id="af513-143">Anyone on hello Internet can see blobs in a public container, but you can modify or delete them only if you have hello appropriate access key.</span></span>  

## <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="af513-144">Cómo cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="af513-144">How to: Upload a blob into a container</span></span>
<span data-ttu-id="af513-145">El almacenamiento de blobs de Azure admite blobs en bloques y en páginas.</span><span class="sxs-lookup"><span data-stu-id="af513-145">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="af513-146">En la mayoría de los casos Hola blob en bloques es hello recomendada toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="af513-146">In hello majority of cases, block blob is hello recommended type toouse.</span></span>  

<span data-ttu-id="af513-147">tooupload un blob en bloques archivo tooa, obtener una referencia de contenedor y usarlo tooget una referencia de blob de bloque.</span><span class="sxs-lookup"><span data-stu-id="af513-147">tooupload a file tooa block blob, get a container reference and use it tooget a block blob reference.</span></span> <span data-ttu-id="af513-148">Una vez que tenga una referencia de blob, puede cargar todos los flujos de datos tooit Hola llamada **upload_from_stream** método.</span><span class="sxs-lookup"><span data-stu-id="af513-148">Once you have a blob reference, you can upload any stream of data tooit by calling hello **upload_from_stream** method.</span></span> <span data-ttu-id="af513-149">Esta operación creará blob Hola si no existe previamente o sobrescribir si existe.</span><span class="sxs-lookup"><span data-stu-id="af513-149">This operation will create hello blob if it didn't previously exist, or overwrite it if it does exist.</span></span> <span data-ttu-id="af513-150">Hola siguiente ejemplo se muestra cómo tooupload un blob en un contenedor y se da por supuesto que el contenedor de hello ya se ha creado.</span><span class="sxs-lookup"><span data-stu-id="af513-150">hello following example shows how tooupload a blob into a container and assumes that hello container was already created.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Create or overwrite hello "my-blob-1" blob with contents from a local file.
concurrency::streams::istream input_stream = concurrency::streams::file_stream<uint8_t>::open_istream(U("DataFile.txt")).get();
blockBlob.upload_from_stream(input_stream);
input_stream.close().wait();

// Create or overwrite hello "my-blob-2" and "my-blob-3" blobs with contents from text.
// Retrieve a reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob blob2 = container.get_block_blob_reference(U("my-blob-2"));
blob2.upload_text(U("more text"));

// Retrieve a reference tooa blob named "my-blob-3".
azure::storage::cloud_block_blob blob3 = container.get_block_blob_reference(U("my-directory/my-sub-directory/my-blob-3"));
blob3.upload_text(U("other text"));  
```

<span data-ttu-id="af513-151">Como alternativa, puede usar hello **upload_from_file** tooupload método un blob en bloques archivo tooa.</span><span class="sxs-lookup"><span data-stu-id="af513-151">Alternatively, you can use hello **upload_from_file** method tooupload a file tooa block blob.</span></span>

## <a name="how-to-list-hello-blobs-in-a-container"></a><span data-ttu-id="af513-152">Cómo: enumerar los blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="af513-152">How to: List hello blobs in a container</span></span>
<span data-ttu-id="af513-153">blobs de hello toolist en un contenedor, primero hay que obtener una referencia de contenedor.</span><span class="sxs-lookup"><span data-stu-id="af513-153">toolist hello blobs in a container, first get a container reference.</span></span> <span data-ttu-id="af513-154">A continuación, puede usar del contenedor de hello **list_blobs** blobs de método tooretrieve Hola y/o directorios dentro de él.</span><span class="sxs-lookup"><span data-stu-id="af513-154">You can then use hello container's **list_blobs** method tooretrieve hello blobs and/or directories within it.</span></span> <span data-ttu-id="af513-155">tooaccess Hola amplio conjunto de propiedades y métodos para un devuelto **list_blob_item**, debe llamar a hello **list_blob_item.as_blob** método tooget una **cloud_blob** objeto, o hello **list_blob.as_directory** tooget método un objeto cloud_blob_directory.</span><span class="sxs-lookup"><span data-stu-id="af513-155">tooaccess hello rich set of properties and methods for a returned **list_blob_item**, you must call hello **list_blob_item.as_blob** method tooget a  **cloud_blob** object, or hello **list_blob.as_directory** method tooget a  cloud_blob_directory object.</span></span> <span data-ttu-id="af513-156">Hello código siguiente muestra cómo tooretrieve y salida Hola URI de cada elemento de hello **mi contenedor de ejemplo** contenedor:</span><span class="sxs-lookup"><span data-stu-id="af513-156">hello following code demonstrates how tooretrieve and output hello URI of each item in hello **my-sample-container** container:</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
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

<span data-ttu-id="af513-157">Para obtener más información sobre cómo enumerar las operaciones, consulte [Enumeración de recursos de almacenamiento de Azure en C++](../storage-c-plus-plus-enumeration.md).</span><span class="sxs-lookup"><span data-stu-id="af513-157">For more details on listing operations, see [List Azure Storage Resources in C++](../storage-c-plus-plus-enumeration.md).</span></span>

## <a name="how-to-download-blobs"></a><span data-ttu-id="af513-158">Cómo descargar blobs</span><span class="sxs-lookup"><span data-stu-id="af513-158">How to: Download blobs</span></span>
<span data-ttu-id="af513-159">blobs toodownload, recuperar primero una referencia de blob y, a continuación, llamar a hello **download_to_stream** método.</span><span class="sxs-lookup"><span data-stu-id="af513-159">toodownload blobs, first retrieve a blob reference and then call hello **download_to_stream** method.</span></span> <span data-ttu-id="af513-160">Hello en el ejemplo siguiente se usa hello **download_to_stream** método tootransfer Hola blob contenido tooa objeto stream que, a continuación, puede conservar tooa de archivos local.</span><span class="sxs-lookup"><span data-stu-id="af513-160">hello following example uses hello **download_to_stream** method tootransfer hello blob contents tooa stream object that you can then persist tooa local file.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Save blob contents tooa file.
concurrency::streams::container_buffer<std::vector<uint8_t>> buffer;
concurrency::streams::ostream output_stream(buffer);
blockBlob.download_to_stream(output_stream);

std::ofstream outfile("DownloadBlobFile.txt", std::ofstream::binary);
std::vector<unsigned char>& data = buffer.collection();

outfile.write((char *)&data[0], buffer.size());
outfile.close();  
```

<span data-ttu-id="af513-161">Como alternativa, puede usar hello **download_to_file** contenido de hello toodownload de método de un archivo de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="af513-161">Alternatively, you can use hello **download_to_file** method toodownload hello contents of a blob tooa file.</span></span>
<span data-ttu-id="af513-162">Además, también puede utilizar hello **download_text** contenido de hello toodownload de método de un blob como una cadena de texto.</span><span class="sxs-lookup"><span data-stu-id="af513-162">In addition, you can also use hello **download_text** method toodownload hello contents of a blob as a text string.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-2".
azure::storage::cloud_block_blob text_blob = container.get_block_blob_reference(U("my-blob-2"));

// Download hello contents of a blog as a text string.
utility::string_t text = text_blob.download_text();
```

## <a name="how-to-delete-blobs"></a><span data-ttu-id="af513-163">Cómo eliminar blobs</span><span class="sxs-lookup"><span data-stu-id="af513-163">How to: Delete blobs</span></span>
<span data-ttu-id="af513-164">toodelete un blob, primero hay que obtener una referencia de blob y, a continuación, llamar a hello **delete_blob** método en él.</span><span class="sxs-lookup"><span data-stu-id="af513-164">toodelete a blob, first get a blob reference and then call hello **delete_blob** method on it.</span></span>  

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello blob client.
azure::storage::cloud_blob_client blob_client = storage_account.create_cloud_blob_client();

// Retrieve a reference tooa previously created container.
azure::storage::cloud_blob_container container = blob_client.get_container_reference(U("my-sample-container"));

// Retrieve reference tooa blob named "my-blob-1".
azure::storage::cloud_block_blob blockBlob = container.get_block_blob_reference(U("my-blob-1"));

// Delete hello blob.
blockBlob.delete_blob();
```

## <a name="next-steps"></a><span data-ttu-id="af513-165">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af513-165">Next steps</span></span>
<span data-ttu-id="af513-166">Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de blobs, siga estas toolearn de vínculos más sobre el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="af513-166">Now that you've learned hello basics of blob storage, follow these links toolearn more about Azure Storage.</span></span>  

* [<span data-ttu-id="af513-167">¿Cómo toouse almacenamiento de cola desde C++</span><span class="sxs-lookup"><span data-stu-id="af513-167">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="af513-168">¿Cómo toouse almacenamiento de tablas de C++</span><span class="sxs-lookup"><span data-stu-id="af513-168">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="af513-169">Enumeración de los recursos de almacenamiento de Azure en C++</span><span class="sxs-lookup"><span data-stu-id="af513-169">List Azure Storage Resources in C++</span></span>](../storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="af513-170">Referencia de la biblioteca de clientes de almacenamiento para C++</span><span class="sxs-lookup"><span data-stu-id="af513-170">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="af513-171">Documentación de Almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="af513-171">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="af513-172">Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola</span><span class="sxs-lookup"><span data-stu-id="af513-172">Transfer data with hello AzCopy command-line utility</span></span>](../storage-use-azcopy.md)

