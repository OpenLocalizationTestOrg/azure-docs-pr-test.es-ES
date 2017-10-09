---
title: aaaIntroduction tooAzure almacenamiento de blobs | Documentos de Microsoft
description: "Introducción tooAzure almacenamiento de blobs"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a><span data-ttu-id="a2260-103">Almacenamiento de tooBlob de introducción</span><span class="sxs-lookup"><span data-stu-id="a2260-103">Introduction tooBlob storage</span></span>

<span data-ttu-id="a2260-104">Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos de objeto no estructurados, como texto o datos binarios, que pueden tener acceso desde cualquier lugar Hola mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a2260-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="a2260-105">Puede usar datos de tooexpose de almacenamiento de Blob públicamente toohello world o datos de la aplicación toostore privada.</span><span class="sxs-lookup"><span data-stu-id="a2260-105">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="a2260-106">El almacenamiento de blobs suele usarse para realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="a2260-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="a2260-107">Servicio de imágenes o documentos directamente tooa explorador</span><span class="sxs-lookup"><span data-stu-id="a2260-107">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="a2260-108">Almacenamiento de archivos para acceso distribuido</span><span class="sxs-lookup"><span data-stu-id="a2260-108">Storing files for distributed access</span></span>
* <span data-ttu-id="a2260-109">Streaming de audio y vídeo</span><span class="sxs-lookup"><span data-stu-id="a2260-109">Streaming video and audio</span></span>
* <span data-ttu-id="a2260-110">Almacenamiento de datos para copia de seguridad y restauración, recuperación ante desastres y archivado</span><span class="sxs-lookup"><span data-stu-id="a2260-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="a2260-111">Almacenamiento de datos para el análisis en local o en un servicio hospedado de Azure</span><span class="sxs-lookup"><span data-stu-id="a2260-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="a2260-112">Conceptos del servicio BLOB</span><span class="sxs-lookup"><span data-stu-id="a2260-112">Blob service concepts</span></span>

<span data-ttu-id="a2260-113">Hola servicio Blob contiene Hola de los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="a2260-113">hello Blob service contains hello following components:</span></span>

![Arquitectura de blob](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="a2260-115">**Cuenta de almacenamiento:** todos los accesos tooAzure almacenamiento se realiza a través de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a2260-115">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="a2260-116">Esta cuenta de almacenamiento puede ser una **cuenta de almacenamiento de uso general** o una **cuenta de Blob Storage**, que sirve para almacenar objetos o blobs.</span><span class="sxs-lookup"><span data-stu-id="a2260-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="a2260-117">Para más información, consulte [Acerca de las cuentas de Azure Storage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a2260-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="a2260-118">**Contenedor**: un contenedor proporciona una agrupación de un conjunto de blobs.</span><span class="sxs-lookup"><span data-stu-id="a2260-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="a2260-119">Todos los blobs deben residir en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="a2260-119">All blobs must be in a container.</span></span> <span data-ttu-id="a2260-120">Además, una cuenta puede disponer de un número ilimitado de contenedores y</span><span class="sxs-lookup"><span data-stu-id="a2260-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="a2260-121">un contenedor puede almacenar un número ilimitado de blobs.</span><span class="sxs-lookup"><span data-stu-id="a2260-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="a2260-122">Tenga en cuenta que ese nombre de contenedor de hello debe estar en minúscula.</span><span class="sxs-lookup"><span data-stu-id="a2260-122">Note that hello container name must be lowercase.</span></span>

* <span data-ttu-id="a2260-123">**Blob:** archivo de cualquier tipo y tamaño.</span><span class="sxs-lookup"><span data-stu-id="a2260-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="a2260-124">Almacenamiento de Azure ofrece tres tipos de blobs: blobs en bloques, blobs en páginas y blobs en anexos.</span><span class="sxs-lookup"><span data-stu-id="a2260-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="a2260-125">*blobs en bloques* son ideales para almacenar archivos binarios o de texto, como documentos y archivos multimedia.</span><span class="sxs-lookup"><span data-stu-id="a2260-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="a2260-126">*Blobs en anexos* son similares blobs tooblock en que se compone de bloques, pero están optimizados para las operaciones de anexión, por lo que son útiles para escenarios de registro.</span><span class="sxs-lookup"><span data-stu-id="a2260-126">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="a2260-127">Un blob en bloques solo puede contener hasta too50, 000 bloques de too100 MB cada uno, hasta un tamaño total de ligeramente superior a 4,75 TB (100 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="a2260-127">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="a2260-128">Un blob en anexos solo puede contener hasta too50, 000 bloques de too4 MB cada uno, hasta un tamaño total de algo más de 195 GB (4 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="a2260-128">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="a2260-129">*Blobs de página* puede ser hasta too1 TB en tamaño y son más eficaces para las operaciones frecuentes de lectura/escritura.</span><span class="sxs-lookup"><span data-stu-id="a2260-129">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="a2260-130">Azure Virtual Machines usa blobs de páginas como discos de sistema operativo y de datos.</span><span class="sxs-lookup"><span data-stu-id="a2260-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="a2260-131">Para más información sobre la nomenclatura de contenedores y blobs, consulte [Asignación de nombres y referencias a contenedores, blobs y metadatos](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="a2260-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2260-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a2260-132">Next steps</span></span>

* [<span data-ttu-id="a2260-133">crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a2260-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="a2260-134">Introducción a Blob Storage con .NET</span><span class="sxs-lookup"><span data-stu-id="a2260-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)