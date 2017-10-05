---
title: Formato del archivo de propiedades y metadatos de Azure Import/Export | Microsoft Docs
description: "Obtenga información sobre cómo especificar metadatos y propiedades para uno o más blobs que forman parte de un trabajo de importación o exportación."
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
ms.openlocfilehash: 3f728ad94cdcbd32092b677f11a737ae91376720
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="0ea91-103">Formato del archivo de propiedades y metadatos de Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="0ea91-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="0ea91-104">Puede especificar metadatos y propiedades para uno o más blobs como parte de un trabajo de importación o exportación.</span><span class="sxs-lookup"><span data-stu-id="0ea91-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="0ea91-105">Para establecer los metadatos o las propiedades para blobs que se crean como parte de un trabajo de importación, proporcione un archivo de metadatos o propiedades en la unidad de disco duro que contiene los datos que se van a importar.</span><span class="sxs-lookup"><span data-stu-id="0ea91-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span></span> <span data-ttu-id="0ea91-106">Para un trabajo de exportación, los metadatos y las propiedades se escriben en un archivo de metadatos o propiedades que se incluye en la unidad de disco duro que se le devuelve.</span><span class="sxs-lookup"><span data-stu-id="0ea91-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="0ea91-107">Formato del archivo de metadatos</span><span class="sxs-lookup"><span data-stu-id="0ea91-107">Metadata file format</span></span>  
<span data-ttu-id="0ea91-108">El formato de un archivo de metadatos es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ea91-108">The format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="0ea91-109">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="0ea91-109">XML Element</span></span>|<span data-ttu-id="0ea91-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="0ea91-110">Type</span></span>|<span data-ttu-id="0ea91-111">Descripción</span><span class="sxs-lookup"><span data-stu-id="0ea91-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="0ea91-112">Elemento raíz</span><span class="sxs-lookup"><span data-stu-id="0ea91-112">Root element</span></span>|<span data-ttu-id="0ea91-113">Elemento raíz del archivo de metadatos.</span><span class="sxs-lookup"><span data-stu-id="0ea91-113">The root element of the metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="0ea91-114">string</span><span class="sxs-lookup"><span data-stu-id="0ea91-114">String</span></span>|<span data-ttu-id="0ea91-115">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0ea91-115">Optional.</span></span> <span data-ttu-id="0ea91-116">El elemento XML especifica el nombre de los metadatos para el blob y su valor especifica el valor de la configuración de metadatos.</span><span class="sxs-lookup"><span data-stu-id="0ea91-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="0ea91-117">Formato de archivo de propiedades</span><span class="sxs-lookup"><span data-stu-id="0ea91-117">Properties file format</span></span>  
<span data-ttu-id="0ea91-118">El formato de un archivo de propiedades es el siguiente:</span><span class="sxs-lookup"><span data-stu-id="0ea91-118">The format of a properties file is as follows:</span></span>  
  
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
  
|<span data-ttu-id="0ea91-119">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="0ea91-119">XML Element</span></span>|<span data-ttu-id="0ea91-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="0ea91-120">Type</span></span>|<span data-ttu-id="0ea91-121">Descripción</span><span class="sxs-lookup"><span data-stu-id="0ea91-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="0ea91-122">Elemento raíz</span><span class="sxs-lookup"><span data-stu-id="0ea91-122">Root element</span></span>|<span data-ttu-id="0ea91-123">Elemento raíz del archivo de propiedades.</span><span class="sxs-lookup"><span data-stu-id="0ea91-123">The root element of the properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="0ea91-124">string</span><span class="sxs-lookup"><span data-stu-id="0ea91-124">String</span></span>|<span data-ttu-id="0ea91-125">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0ea91-125">Optional.</span></span> <span data-ttu-id="0ea91-126">Hora de la última modificación del blob.</span><span class="sxs-lookup"><span data-stu-id="0ea91-126">The last-modified time for the blob.</span></span> <span data-ttu-id="0ea91-127">Solo para trabajos de exportación.</span><span class="sxs-lookup"><span data-stu-id="0ea91-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="0ea91-128">string</span><span class="sxs-lookup"><span data-stu-id="0ea91-128">String</span></span>|<span data-ttu-id="0ea91-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0ea91-129">Optional.</span></span> <span data-ttu-id="0ea91-130">Valor ETag del blob.</span><span class="sxs-lookup"><span data-stu-id="0ea91-130">The blob's ETag value.</span></span> <span data-ttu-id="0ea91-131">Solo para trabajos de exportación.</span><span class="sxs-lookup"><span data-stu-id="0ea91-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="0ea91-132">string</span><span class="sxs-lookup"><span data-stu-id="0ea91-132">String</span></span>|<span data-ttu-id="0ea91-133">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0ea91-133">Optional.</span></span> <span data-ttu-id="0ea91-134">Tamaño del blob en bytes.</span><span class="sxs-lookup"><span data-stu-id="0ea91-134">The size of the blob in bytes.</span></span> <span data-ttu-id="0ea91-135">Solo para trabajos de exportación.</span><span class="sxs-lookup"><span data-stu-id="0ea91-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="0ea91-136">string</span><span class="sxs-lookup"><span data-stu-id="0ea91-136">String</span></span>|<span data-ttu-id="0ea91-137">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0ea91-137">Optional.</span></span> <span data-ttu-id="0ea91-138">Tipo de contenido del blob.</span><span class="sxs-lookup"><span data-stu-id="0ea91-138">The content type of the blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="0ea91-139">string</span><span class="sxs-lookup"><span data-stu-id="0ea91-139">String</span></span>|<span data-ttu-id="0ea91-140">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0ea91-140">Optional.</span></span> <span data-ttu-id="0ea91-141">Hash MD5 del blob.</span><span class="sxs-lookup"><span data-stu-id="0ea91-141">The blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="0ea91-142">String</span><span class="sxs-lookup"><span data-stu-id="0ea91-142">String</span></span>|<span data-ttu-id="0ea91-143">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0ea91-143">Optional.</span></span> <span data-ttu-id="0ea91-144">Codificación del contenido del blob.</span><span class="sxs-lookup"><span data-stu-id="0ea91-144">The blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="0ea91-145">string</span><span class="sxs-lookup"><span data-stu-id="0ea91-145">String</span></span>|<span data-ttu-id="0ea91-146">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0ea91-146">Optional.</span></span> <span data-ttu-id="0ea91-147">Idioma del contenido del blob.</span><span class="sxs-lookup"><span data-stu-id="0ea91-147">The blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="0ea91-148">String</span><span class="sxs-lookup"><span data-stu-id="0ea91-148">String</span></span>|<span data-ttu-id="0ea91-149">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0ea91-149">Optional.</span></span> <span data-ttu-id="0ea91-150">Cadena de control de caché para el blob.</span><span class="sxs-lookup"><span data-stu-id="0ea91-150">The cache control string for the blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="0ea91-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ea91-151">Next steps</span></span>

<span data-ttu-id="0ea91-152">Vea [Set Blob Properties](/rest/api/storageservices/set-blob-properties) (Establecer propiedades del blob), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) (Establecer metadatos del blob) y [Setting and Retrieving Properties and Metadata for Blob Resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Configuración y recuperación de propiedades y metadatos para los recursos del blob) para consultar reglas detalladas sobre cómo establecer propiedades y metadatos del blob.</span><span class="sxs-lookup"><span data-stu-id="0ea91-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
