---
title: "Introducción a Azure Blob Storage | Microsoft Docs"
description: "Introducción a Azure Blob Storage"
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
ms.openlocfilehash: 051f1b37eab254d4ab4f806166ac8d0b8cab944d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-blob-storage"></a><span data-ttu-id="399f7-103">Introducción a Blob Storage</span><span class="sxs-lookup"><span data-stu-id="399f7-103">Introduction to Blob storage</span></span>

<span data-ttu-id="399f7-104">El Almacenamiento de blobs de Azure es un servicio para almacenar grandes cantidades de datos de objetos no estructurados, como texto o datos binarios, a los que puede acceder desde cualquier lugar del mundo a través de HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="399f7-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="399f7-105">Puede usar el almacenamiento de blobs para exponer datos públicamente o para almacenar datos de la aplicación de manera privada.</span><span class="sxs-lookup"><span data-stu-id="399f7-105">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span></span>

<span data-ttu-id="399f7-106">El almacenamiento de blobs suele usarse para realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="399f7-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="399f7-107">Servicio de imágenes o documentos directamente a un explorador</span><span class="sxs-lookup"><span data-stu-id="399f7-107">Serving images or documents directly to a browser</span></span>
* <span data-ttu-id="399f7-108">Almacenamiento de archivos para acceso distribuido</span><span class="sxs-lookup"><span data-stu-id="399f7-108">Storing files for distributed access</span></span>
* <span data-ttu-id="399f7-109">Streaming de audio y vídeo</span><span class="sxs-lookup"><span data-stu-id="399f7-109">Streaming video and audio</span></span>
* <span data-ttu-id="399f7-110">Almacenamiento de datos para copia de seguridad y restauración, recuperación ante desastres y archivado</span><span class="sxs-lookup"><span data-stu-id="399f7-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="399f7-111">Almacenamiento de datos para el análisis en local o en un servicio hospedado de Azure</span><span class="sxs-lookup"><span data-stu-id="399f7-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="399f7-112">Conceptos del servicio BLOB</span><span class="sxs-lookup"><span data-stu-id="399f7-112">Blob service concepts</span></span>

<span data-ttu-id="399f7-113">El servicio BLOB contiene los componentes siguientes:</span><span class="sxs-lookup"><span data-stu-id="399f7-113">The Blob service contains the following components:</span></span>

![Arquitectura de blob](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="399f7-115">**Cuenta de almacenamiento:** todo el acceso a Almacenamiento de Azure se realiza a través de una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="399f7-115">**Storage Account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="399f7-116">Esta cuenta de almacenamiento puede ser una **cuenta de almacenamiento de uso general** o una **cuenta de Blob Storage**, que sirve para almacenar objetos o blobs.</span><span class="sxs-lookup"><span data-stu-id="399f7-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="399f7-117">Para más información, consulte [Acerca de las cuentas de Azure Storage](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="399f7-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="399f7-118">**Contenedor**: un contenedor proporciona una agrupación de un conjunto de blobs.</span><span class="sxs-lookup"><span data-stu-id="399f7-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="399f7-119">Todos los blobs deben residir en un contenedor.</span><span class="sxs-lookup"><span data-stu-id="399f7-119">All blobs must be in a container.</span></span> <span data-ttu-id="399f7-120">Además, una cuenta puede disponer de un número ilimitado de contenedores y</span><span class="sxs-lookup"><span data-stu-id="399f7-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="399f7-121">un contenedor puede almacenar un número ilimitado de blobs.</span><span class="sxs-lookup"><span data-stu-id="399f7-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="399f7-122">Tenga en cuenta que el nombre del contenedor debe estar en minúsculas.</span><span class="sxs-lookup"><span data-stu-id="399f7-122">Note that the container name must be lowercase.</span></span>

* <span data-ttu-id="399f7-123">**Blob:** archivo de cualquier tipo y tamaño.</span><span class="sxs-lookup"><span data-stu-id="399f7-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="399f7-124">Almacenamiento de Azure ofrece tres tipos de blobs: blobs en bloques, blobs en páginas y blobs en anexos.</span><span class="sxs-lookup"><span data-stu-id="399f7-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="399f7-125">*blobs en bloques* son ideales para almacenar archivos binarios o de texto, como documentos y archivos multimedia.</span><span class="sxs-lookup"><span data-stu-id="399f7-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="399f7-126">*blobs en anexos* se parecen a los blobs en bloques porque se componen de bloques, pero están optimizados para las operaciones de anexión, por lo que son útiles para escenarios de registro.</span><span class="sxs-lookup"><span data-stu-id="399f7-126">*Append blobs* are similar to block blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="399f7-127">Un único blob en bloques puede contener un máximo de 50 000 bloques de hasta 100 MB cada uno, hasta un tamaño total de algo más de 4,75 GB (100 MB × 50 000).</span><span class="sxs-lookup"><span data-stu-id="399f7-127">A single block blob can contain up to 50,000 blocks of up to 100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="399f7-128">Un único blob en anexos puede contener un máximo de 50 000 bloques de hasta 4 MB cada uno, hasta un tamaño total de algo más de 195 GB (4 MB × 50 000).</span><span class="sxs-lookup"><span data-stu-id="399f7-128">A single append blob can contain up to 50,000 blocks of up to 4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="399f7-129">*blobs en páginas* pueden tener un tamaño de hasta 1 TB y son más eficaces para operaciones frecuentes de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="399f7-129">*Page blobs* can be up to 1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="399f7-130">Azure Virtual Machines usa blobs de páginas como discos de sistema operativo y de datos.</span><span class="sxs-lookup"><span data-stu-id="399f7-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="399f7-131">Para más información sobre la nomenclatura de contenedores y blobs, consulte [Asignación de nombres y referencias a contenedores, blobs y metadatos](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="399f7-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="399f7-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="399f7-132">Next steps</span></span>

* [<span data-ttu-id="399f7-133">Cree una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="399f7-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="399f7-134">Introducción a Blob Storage con .NET</span><span class="sxs-lookup"><span data-stu-id="399f7-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)