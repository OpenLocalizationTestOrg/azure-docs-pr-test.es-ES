---
title: Uso de Azure Blob Storage (almacenamiento de objetos) en Python | Microsoft Docs
description: Almacene datos no estructurados en la nube con Almacenamiento de blobs (objetos) de Azure.
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 968814db9496fd410162d482191592c8a56101f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-from-python"></a><span data-ttu-id="ca494-103">Uso del almacenamiento de blobs de Azure desde Python</span><span class="sxs-lookup"><span data-stu-id="ca494-103">How to use Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="ca494-104">Información general</span><span class="sxs-lookup"><span data-stu-id="ca494-104">Overview</span></span>
<span data-ttu-id="ca494-105">Almacenamiento de blobs de Azure es un servicio que almacena datos no estructurados en la nube como objetos o blobs.</span><span class="sxs-lookup"><span data-stu-id="ca494-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="ca494-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ca494-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="ca494-107">El Almacenamiento de blobs a veces se conoce como "almacenamiento de objetos".</span><span class="sxs-lookup"><span data-stu-id="ca494-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="ca494-108">Este artículo le muestra cómo realizar algunas tareas comunes con el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="ca494-108">This article will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="ca494-109">Los ejemplos están escritos en Python y usan el [SDK de Almacenamiento de Microsoft Azure para Python].</span><span class="sxs-lookup"><span data-stu-id="ca494-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="ca494-110">Entre los escenarios descritos se incluyen cargar, enumerar, descargar y eliminar blobs.</span><span class="sxs-lookup"><span data-stu-id="ca494-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="ca494-111">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="ca494-111">Create a container</span></span>
<span data-ttu-id="ca494-112">Según el tipo de blob que desee usar, cree un objeto **BlockBlobService**, **AppendBlobService** o **PageBlobService**.</span><span class="sxs-lookup"><span data-stu-id="ca494-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="ca494-113">El código siguiente usa un objeto **BlockBlobService** .</span><span class="sxs-lookup"><span data-stu-id="ca494-113">The following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="ca494-114">Agregue lo siguiente cerca de la parte superior de todo archivo Python en el que desee obtener acceso al almacenamiento de blobs en bloques de Azure mediante programación.</span><span class="sxs-lookup"><span data-stu-id="ca494-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="ca494-115">El código siguiente crea un objeto **BlockBlobService** usando la clave de la cuenta y el nombre de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ca494-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span></span>  <span data-ttu-id="ca494-116">Reemplace 'myaccount' y 'mykey' por la clave y el nombre de cuenta.</span><span class="sxs-lookup"><span data-stu-id="ca494-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="ca494-117">En el siguiente ejemplo de código, puede usar un objeto **BlockBlobService** para crear el contenedor si no existe.</span><span class="sxs-lookup"><span data-stu-id="ca494-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="ca494-118">De manera predeterminada, el nuevo contenedor es privado, por lo que tiene que especificar su clave de acceso de almacenamiento (como hizo anteriormente) para descargar blobs de él.</span><span class="sxs-lookup"><span data-stu-id="ca494-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span> <span data-ttu-id="ca494-119">Si desea poner los blobs del contenedor a disposición de todo el mundo, puede crear el contenedor y pasar al nivel de acceso público usando el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="ca494-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="ca494-120">También tiene la posibilidad de modificar un contenedor después de haberlo creado mediante el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="ca494-120">Alternatively, you can modify a container after you have created it using the following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="ca494-121">Después de este cambio, cualquier usuario de Internet podrá ver los blobs de los contenedores públicos, pero solo usted podrá modificarlos o eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="ca494-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="ca494-122">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="ca494-122">Upload a blob into a container</span></span>
<span data-ttu-id="ca494-123">Para crear un blob en bloques y cargar datos, use los métodos **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** o **create\_blob\_from\_text**.</span><span class="sxs-lookup"><span data-stu-id="ca494-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="ca494-124">Se trata de métodos de alto nivel que realizan la fragmentación necesaria cuando el tamaño de los datos supera los 64 MB.</span><span class="sxs-lookup"><span data-stu-id="ca494-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="ca494-125">**create\_blob\_from\_path** carga el contenido de un archivo de la ruta de acceso especificada, y **create\_blob\_from\_stream** carga el contenido de una transmisión o archivo ya abierto.</span><span class="sxs-lookup"><span data-stu-id="ca494-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="ca494-126">**create\_blob\_from\_bytes** carga una matriz de bytes, y **create\_blob\_from\_text** carga el valor de texto especificado con la codificación especificada (el valor predeterminado es UTF-8).</span><span class="sxs-lookup"><span data-stu-id="ca494-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="ca494-127">En el siguiente ejemplo se carga el contenido del archivo **sunset.png** en el blob **myblob**.</span><span class="sxs-lookup"><span data-stu-id="ca494-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="ca494-128">Enumerar los blobs de un contenedor</span><span class="sxs-lookup"><span data-stu-id="ca494-128">List the blobs in a container</span></span>
<span data-ttu-id="ca494-129">Para enumerar los blobs de un contenedor, use el método **list\_blobs**.</span><span class="sxs-lookup"><span data-stu-id="ca494-129">To list the blobs in a container, use the **list\_blobs** method.</span></span> <span data-ttu-id="ca494-130">Este método devuelve un generador.</span><span class="sxs-lookup"><span data-stu-id="ca494-130">This method returns a generator.</span></span> <span data-ttu-id="ca494-131">El código siguiente ofrece el **nombre** de todos los blobs de un contenedor a la consola.</span><span class="sxs-lookup"><span data-stu-id="ca494-131">The following code outputs the **name** of each blob in a container to the console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="ca494-132">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="ca494-132">Download blobs</span></span>
<span data-ttu-id="ca494-133">Para descargar datos de un blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, o **get\_blob\_to\_text**.</span><span class="sxs-lookup"><span data-stu-id="ca494-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="ca494-134">Se trata de métodos de alto nivel que realizan la fragmentación necesaria cuando el tamaño de los datos supera los 64 MB.</span><span class="sxs-lookup"><span data-stu-id="ca494-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="ca494-135">En el ejemplo siguiente se muestra cómo usar **get\_blob\_to\_path** para descargar el contenido del blob **myblob** blob y almacenarlo en el archivo **out-sunset.png**.</span><span class="sxs-lookup"><span data-stu-id="ca494-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="ca494-136">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="ca494-136">Delete a blob</span></span>
<span data-ttu-id="ca494-137">Finalmente, para eliminar un blob, llame a **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="ca494-137">Finally, to delete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="ca494-138">Escritura en un blob en anexos</span><span class="sxs-lookup"><span data-stu-id="ca494-138">Writing to an append blob</span></span>
<span data-ttu-id="ca494-139">Un blob en anexos se optimiza para las operaciones de anexado, como el registro.</span><span class="sxs-lookup"><span data-stu-id="ca494-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="ca494-140">Como un blob en bloques, un blob en anexos se compone también de bloques, pero en el caso del blob en anexos cuando se agrega un nuevo bloque, siempre se anexa al final del blob.</span><span class="sxs-lookup"><span data-stu-id="ca494-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="ca494-141">No se puede actualizar o eliminar un bloque existente en un blob en anexos.</span><span class="sxs-lookup"><span data-stu-id="ca494-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="ca494-142">Los identificadores de bloque para un blob en anexos no está expuestos como lo están en el caso de los blobs en bloques.</span><span class="sxs-lookup"><span data-stu-id="ca494-142">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="ca494-143">Cada bloque en un blob en anexos puede tener un tamaño diferente, hasta un máximo de 4 MB y el blob puede incluir un máximo de 50.000 bloques.</span><span class="sxs-lookup"><span data-stu-id="ca494-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="ca494-144">El tamaño máximo de un blob en anexos es, por tanto, ligeramente superior a 195 GB (4 MB X 50.000 bloques).</span><span class="sxs-lookup"><span data-stu-id="ca494-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="ca494-145">El ejemplo siguiente crea un nuevo blob en anexos y le anexa algunos datos, para simular una operación de registro simple.</span><span class="sxs-lookup"><span data-stu-id="ca494-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# The same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="ca494-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ca494-146">Next steps</span></span>
<span data-ttu-id="ca494-147">Ahora que está familiarizado con los aspectos básicos del Almacenamiento de blobs, siga estos vínculos para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="ca494-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="ca494-148">Centro para desarrolladores de Python</span><span class="sxs-lookup"><span data-stu-id="ca494-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="ca494-149">API de REST de servicios de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="ca494-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="ca494-150">[Blog del equipo de almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="ca494-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="ca494-151">[SDK de Almacenamiento de Microsoft Azure para Python]</span><span class="sxs-lookup"><span data-stu-id="ca494-151">[Microsoft Azure Storage SDK for Python]</span></span>

<span data-ttu-id="ca494-152">[Blog del equipo de almacenamiento de Azure]: http://blogs.msdn.com/b/windowsazurestorage/</span><span class="sxs-lookup"><span data-stu-id="ca494-152">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/</span></span>
<span data-ttu-id="ca494-153">[SDK de Almacenamiento de Microsoft Azure para Python]: https://github.com/Azure/azure-storage-python</span><span class="sxs-lookup"><span data-stu-id="ca494-153">[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python</span></span>
