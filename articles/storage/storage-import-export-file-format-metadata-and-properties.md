---
title: "formato de archivo de importación y exportación de metadatos y propiedades de aaaAzure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toospecify metadatos y propiedades de uno o más blobs que forman parte de una importación o exportación de trabajo."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="cc28c-103">Formato del archivo de propiedades y metadatos de Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="cc28c-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="cc28c-104">Puede especificar metadatos y propiedades para uno o más blobs como parte de un trabajo de importación o exportación.</span><span class="sxs-lookup"><span data-stu-id="cc28c-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="cc28c-105">tooset metadatos o propiedades de blobs que se crean como parte de un trabajo de importación, proporcione un archivo de metadatos o propiedades en unidad de disco duro de Hola que contiene Hola datos toobe importado.</span><span class="sxs-lookup"><span data-stu-id="cc28c-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="cc28c-106">Para un trabajo de exportación, metadatos y propiedades se escriben tooa archivo de metadatos o las propiedades que se incluye en la unidad de disco duro de hello devuelve tooyou.</span><span class="sxs-lookup"><span data-stu-id="cc28c-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="cc28c-107">Formato del archivo de metadatos</span><span class="sxs-lookup"><span data-stu-id="cc28c-107">Metadata file format</span></span>  
<span data-ttu-id="cc28c-108">formato de Hola de un archivo de metadatos es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="cc28c-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="cc28c-109">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="cc28c-109">XML Element</span></span>|<span data-ttu-id="cc28c-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="cc28c-110">Type</span></span>|<span data-ttu-id="cc28c-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="cc28c-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="cc28c-112">Elemento raíz</span><span class="sxs-lookup"><span data-stu-id="cc28c-112">Root element</span></span>|<span data-ttu-id="cc28c-113">elemento raíz de Hello del archivo de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc28c-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="cc28c-114">String</span><span class="sxs-lookup"><span data-stu-id="cc28c-114">String</span></span>|<span data-ttu-id="cc28c-115">Opcional.</span><span class="sxs-lookup"><span data-stu-id="cc28c-115">Optional.</span></span> <span data-ttu-id="cc28c-116">elemento XML de Hello especifica el nombre de Hola de metadatos de hello para el blob de Hola y su valor especifica el valor de Hola de configuración de metadatos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc28c-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="cc28c-117">Formato de archivo de propiedades</span><span class="sxs-lookup"><span data-stu-id="cc28c-117">Properties file format</span></span>  
<span data-ttu-id="cc28c-118">formato de Hola de un archivo de propiedades es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="cc28c-118">hello format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="cc28c-119">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="cc28c-119">XML Element</span></span>|<span data-ttu-id="cc28c-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="cc28c-120">Type</span></span>|<span data-ttu-id="cc28c-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="cc28c-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="cc28c-122">Elemento raíz</span><span class="sxs-lookup"><span data-stu-id="cc28c-122">Root element</span></span>|<span data-ttu-id="cc28c-123">elemento raíz de Hola de archivo de propiedades de hello.</span><span class="sxs-lookup"><span data-stu-id="cc28c-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="cc28c-124">String</span><span class="sxs-lookup"><span data-stu-id="cc28c-124">String</span></span>|<span data-ttu-id="cc28c-125">Opcional.</span><span class="sxs-lookup"><span data-stu-id="cc28c-125">Optional.</span></span> <span data-ttu-id="cc28c-126">hora de última modificación de Hello para el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc28c-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="cc28c-127">Solo para trabajos de exportación.</span><span class="sxs-lookup"><span data-stu-id="cc28c-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="cc28c-128">string</span><span class="sxs-lookup"><span data-stu-id="cc28c-128">String</span></span>|<span data-ttu-id="cc28c-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="cc28c-129">Optional.</span></span> <span data-ttu-id="cc28c-130">Hola valor ETag del blob.</span><span class="sxs-lookup"><span data-stu-id="cc28c-130">hello blob's ETag value.</span></span> <span data-ttu-id="cc28c-131">Solo para trabajos de exportación.</span><span class="sxs-lookup"><span data-stu-id="cc28c-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="cc28c-132">string</span><span class="sxs-lookup"><span data-stu-id="cc28c-132">String</span></span>|<span data-ttu-id="cc28c-133">Opcional.</span><span class="sxs-lookup"><span data-stu-id="cc28c-133">Optional.</span></span> <span data-ttu-id="cc28c-134">tamaño de Hello del blob de hello en bytes.</span><span class="sxs-lookup"><span data-stu-id="cc28c-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="cc28c-135">Solo para trabajos de exportación.</span><span class="sxs-lookup"><span data-stu-id="cc28c-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="cc28c-136">string</span><span class="sxs-lookup"><span data-stu-id="cc28c-136">String</span></span>|<span data-ttu-id="cc28c-137">Opcional.</span><span class="sxs-lookup"><span data-stu-id="cc28c-137">Optional.</span></span> <span data-ttu-id="cc28c-138">tipo de contenido de Hola de blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc28c-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="cc28c-139">String</span><span class="sxs-lookup"><span data-stu-id="cc28c-139">String</span></span>|<span data-ttu-id="cc28c-140">Opcional.</span><span class="sxs-lookup"><span data-stu-id="cc28c-140">Optional.</span></span> <span data-ttu-id="cc28c-141">Hola hash MD5 del blob.</span><span class="sxs-lookup"><span data-stu-id="cc28c-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="cc28c-142">String</span><span class="sxs-lookup"><span data-stu-id="cc28c-142">String</span></span>|<span data-ttu-id="cc28c-143">Opcional.</span><span class="sxs-lookup"><span data-stu-id="cc28c-143">Optional.</span></span> <span data-ttu-id="cc28c-144">Hola contenido del blob de codificación.</span><span class="sxs-lookup"><span data-stu-id="cc28c-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="cc28c-145">String</span><span class="sxs-lookup"><span data-stu-id="cc28c-145">String</span></span>|<span data-ttu-id="cc28c-146">Opcional.</span><span class="sxs-lookup"><span data-stu-id="cc28c-146">Optional.</span></span> <span data-ttu-id="cc28c-147">Hola idioma del contenido del blob.</span><span class="sxs-lookup"><span data-stu-id="cc28c-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="cc28c-148">String</span><span class="sxs-lookup"><span data-stu-id="cc28c-148">String</span></span>|<span data-ttu-id="cc28c-149">Opcional.</span><span class="sxs-lookup"><span data-stu-id="cc28c-149">Optional.</span></span> <span data-ttu-id="cc28c-150">cadena de control de caché de Hello para el blob de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc28c-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="cc28c-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cc28c-151">Next steps</span></span>

<span data-ttu-id="cc28c-152">Vea [Set Blob Properties](/rest/api/storageservices/set-blob-properties) (Establecer propiedades del blob), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) (Establecer metadatos del blob) y [Setting and Retrieving Properties and Metadata for Blob Resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Configuración y recuperación de propiedades y metadatos para los recursos del blob) para consultar reglas detalladas sobre cómo establecer propiedades y metadatos del blob.</span><span class="sxs-lookup"><span data-stu-id="cc28c-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
