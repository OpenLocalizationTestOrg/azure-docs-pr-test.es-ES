---
title: aaaHow toouse el almacenamiento de blobs de Azure (almacenamiento de objetos) de Python | Documentos de Microsoft
description: Almacenar datos no estructurados en la nube de hello con almacenamiento de blobs de Azure (almacenamiento de objetos).
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
ms.openlocfilehash: 8f9ca93e52b030384e28a739d2f1c6b610be094a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a><span data-ttu-id="588fc-103">¿Cómo toouse almacenamiento de blobs de Azure de Python</span><span class="sxs-lookup"><span data-stu-id="588fc-103">How toouse Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="588fc-104">Información general</span><span class="sxs-lookup"><span data-stu-id="588fc-104">Overview</span></span>
<span data-ttu-id="588fc-105">Almacenamiento de blobs de Azure es un servicio que almacena los datos no estructurados en la nube de hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="588fc-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="588fc-106">El Almacenamiento de blobs puede almacenar cualquier tipo de datos binarios o texto, como un documento, un archivo multimedia o un instalador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="588fc-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="588fc-107">Almacenamiento de blobs también es un almacenamiento de objetos de tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="588fc-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="588fc-108">En este artículo le mostrará cómo tooperform escenarios comunes con almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="588fc-108">This article will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="588fc-109">ejemplos de Hello están escritos en Python y usar hello [SDK de almacenamiento de Microsoft Azure para Python].</span><span class="sxs-lookup"><span data-stu-id="588fc-109">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="588fc-110">escenarios de Hello descritos incluyen cargar, enumerar, descargar y eliminación de blobs.</span><span class="sxs-lookup"><span data-stu-id="588fc-110">hello scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="588fc-111">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="588fc-111">Create a container</span></span>
<span data-ttu-id="588fc-112">En función de tipo hello de blob que desearía toouse, cree un **BlockBlobService**, **AppendBlobService**, o **PageBlobService** objeto.</span><span class="sxs-lookup"><span data-stu-id="588fc-112">Based on hello type of blob you would like toouse, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="588fc-113">Hola siguiente de código utiliza un **BlockBlobService** objeto.</span><span class="sxs-lookup"><span data-stu-id="588fc-113">hello following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="588fc-114">Agregue los siguiente Hola cerca de parte superior de Hola de cualquier archivo de Python en el que desea acceso tooprogrammatically almacenamiento de blobs de bloque de Azure.</span><span class="sxs-lookup"><span data-stu-id="588fc-114">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="588fc-115">Hello código siguiente se crea un **BlockBlobService** objeto mediante la clave de cuenta y el nombre de la cuenta del almacenamiento Hola.</span><span class="sxs-lookup"><span data-stu-id="588fc-115">hello following code creates a **BlockBlobService** object using hello storage account name and account key.</span></span>  <span data-ttu-id="588fc-116">Reemplace 'myaccount' y 'mykey' por la clave y el nombre de cuenta.</span><span class="sxs-lookup"><span data-stu-id="588fc-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="588fc-117">En el siguiente ejemplo de código de hello, puede usar un **BlockBlobService** contenedor Hola de objetos de toocreate si no existe.</span><span class="sxs-lookup"><span data-stu-id="588fc-117">In hello following code example, you can use a **BlockBlobService** object toocreate hello container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="588fc-118">De forma predeterminada, nuevo contenedor de hello es privado, por lo que debe especificar la clave de acceso de almacenamiento (como hizo anteriormente) blobs toodownload de este contenedor.</span><span class="sxs-lookup"><span data-stu-id="588fc-118">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span> <span data-ttu-id="588fc-119">Si desea toomake blobs Hola Hola contenedor disponibles tooeveryone, puede crear contenedor de Hola y pasar el nivel de acceso público de hello mediante el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="588fc-119">If you want toomake hello blobs within hello container available tooeveryone, you can create hello container and pass hello public access level using hello following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="588fc-120">Como alternativa, puede modificar un contenedor después de haber creado mediante el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="588fc-120">Alternatively, you can modify a container after you have created it using hello following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="588fc-121">Después de este cambio, todos los usuarios de hello Internet pueden ver los blobs en un contenedor público, pero solo puede modificar o eliminarlos.</span><span class="sxs-lookup"><span data-stu-id="588fc-121">After this change, anyone on hello Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="588fc-122">Cargar un blob en un contenedor</span><span class="sxs-lookup"><span data-stu-id="588fc-122">Upload a blob into a container</span></span>
<span data-ttu-id="588fc-123">toocreate un blob en bloques y los datos de carga, use hello **crear\_blob\_de\_ruta de acceso**, **crear\_blob\_de\_flujo**, **crear\_blob\_de\_bytes** o **crear\_blob\_de\_texto** métodos.</span><span class="sxs-lookup"><span data-stu-id="588fc-123">toocreate a block blob and upload data, use hello **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="588fc-124">Son métodos de alto nivel que realizan Hola de fragmentación es necesario cuando el tamaño de Hola de datos de hello supera los 64 MB.</span><span class="sxs-lookup"><span data-stu-id="588fc-124">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="588fc-125">**crear\_blob\_de\_ruta de acceso** cargas Hola contenido de un archivo de ruta de acceso especificada de hello, y **crear\_blob\_de\_flujo** cargas Hola contenido a partir de una secuencia o archivo ya abierta.</span><span class="sxs-lookup"><span data-stu-id="588fc-125">**create\_blob\_from\_path** uploads hello contents of a file from hello specified path, and **create\_blob\_from\_stream** uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="588fc-126">**crear\_blob\_de\_bytes** carga una matriz de bytes, y **crear\_blob\_de\_texto** carga Hola especificado valor de texto mediante Hola especifica codificación (valor predeterminado es tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="588fc-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="588fc-127">Hello en el ejemplo siguiente se carga contenido Hola de hello **sunset.png** archivo en hello **myblob** blob.</span><span class="sxs-lookup"><span data-stu-id="588fc-127">hello following example uploads hello contents of hello **sunset.png** file into hello **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="588fc-128">Lista de blobs de hello en un contenedor</span><span class="sxs-lookup"><span data-stu-id="588fc-128">List hello blobs in a container</span></span>
<span data-ttu-id="588fc-129">blobs de hello toolist en un contenedor, use hello **lista\_blobs** método.</span><span class="sxs-lookup"><span data-stu-id="588fc-129">toolist hello blobs in a container, use hello **list\_blobs** method.</span></span> <span data-ttu-id="588fc-130">Este método devuelve un generador.</span><span class="sxs-lookup"><span data-stu-id="588fc-130">This method returns a generator.</span></span> <span data-ttu-id="588fc-131">Hello código siguiente genera hello **nombre** de cada blob en una consola de toohello de contenedor.</span><span class="sxs-lookup"><span data-stu-id="588fc-131">hello following code outputs hello **name** of each blob in a container toohello console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="588fc-132">Descargar blobs</span><span class="sxs-lookup"><span data-stu-id="588fc-132">Download blobs</span></span>
<span data-ttu-id="588fc-133">toodownload datos de un blob, utilice **obtener\_blob\_a\_ruta de acceso**, **obtener\_blob\_a\_flujo**, **obtener\_blob\_a\_bytes**, o **obtener\_blob\_a\_texto**.</span><span class="sxs-lookup"><span data-stu-id="588fc-133">toodownload data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="588fc-134">Son métodos de alto nivel que realizan Hola de fragmentación es necesario cuando el tamaño de Hola de datos de hello supera los 64 MB.</span><span class="sxs-lookup"><span data-stu-id="588fc-134">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="588fc-135">Hello en el ejemplo siguiente se muestra cómo utilizar **obtener\_blob\_a\_ruta de acceso** contenido de hello toodownload de hello **myblob** blob y almacenar toohello **fuera sunset.png** archivo.</span><span class="sxs-lookup"><span data-stu-id="588fc-135">hello following example demonstrates using **get\_blob\_to\_path** toodownload hello contents of hello **myblob** blob and store it toohello **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="588fc-136">Eliminar un blob</span><span class="sxs-lookup"><span data-stu-id="588fc-136">Delete a blob</span></span>
<span data-ttu-id="588fc-137">Por último, llame un blob, toodelete **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="588fc-137">Finally, toodelete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="588fc-138">Escritura tooan anexar blob</span><span class="sxs-lookup"><span data-stu-id="588fc-138">Writing tooan append blob</span></span>
<span data-ttu-id="588fc-139">Un blob en anexos se optimiza para las operaciones de anexado, como el registro.</span><span class="sxs-lookup"><span data-stu-id="588fc-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="588fc-140">Como un blob en bloques, un blob en anexos está formado por bloques, pero cuando se agrega un nuevo blob en bloques tooan anexado, siempre es toohello anexado final del blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="588fc-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="588fc-141">No se puede actualizar o eliminar un bloque existente en un blob en anexos.</span><span class="sxs-lookup"><span data-stu-id="588fc-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="588fc-142">Identificadores de bloque de Hola para un blob en anexos no se exponen como sirven como un blob en bloques.</span><span class="sxs-lookup"><span data-stu-id="588fc-142">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="588fc-143">Cada bloque de un blob en anexos puede tener un tamaño diferente, la tooa máximo de 4 MB, y un blob en anexos puede incluir un máximo de 50.000 bloques.</span><span class="sxs-lookup"><span data-stu-id="588fc-143">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="588fc-144">tamaño máximo de Hola de un blob en anexos, por tanto, es un poco más de 195 GB (4 MB X 50.000 bloques).</span><span class="sxs-lookup"><span data-stu-id="588fc-144">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="588fc-145">ejemplo de Hola siguiente crea un nuevo blob en anexos y anexa algunos tooit de datos, simular una operación de registro simple.</span><span class="sxs-lookup"><span data-stu-id="588fc-145">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="588fc-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="588fc-146">Next steps</span></span>
<span data-ttu-id="588fc-147">Ahora que ha aprendido conceptos básicos de Hola de almacenamiento de blobs, siga estas toolearn de vínculos más.</span><span class="sxs-lookup"><span data-stu-id="588fc-147">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="588fc-148">Centro para desarrolladores de Python</span><span class="sxs-lookup"><span data-stu-id="588fc-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="588fc-149">API de REST de servicios de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="588fc-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="588fc-150">[Blog del equipo de almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="588fc-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="588fc-151">[SDK de almacenamiento de Microsoft Azure para Python]</span><span class="sxs-lookup"><span data-stu-id="588fc-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog del equipo de almacenamiento de Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[SDK de almacenamiento de Microsoft Azure para Python]: https://github.com/Azure/azure-storage-python
