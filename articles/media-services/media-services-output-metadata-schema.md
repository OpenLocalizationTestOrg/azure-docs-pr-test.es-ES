---
title: Esquema de metadatos de salida de Azure Media Services | Microsoft Docs
description: "En este tema se proporciona información general sobre el esquema de metadatos de salida de Azure Media Services."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: c175d359f93e7cd8cd73aa498ad8b71c4ec497f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="output-metadata"></a><span data-ttu-id="1a54a-103">Metadatos de salida</span><span class="sxs-lookup"><span data-stu-id="1a54a-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="1a54a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1a54a-104">Overview</span></span>
<span data-ttu-id="1a54a-105">Un trabajo de codificación está asociado a un recurso (o recursos) de entrada donde desea realizar algunas tareas de codificación.</span><span class="sxs-lookup"><span data-stu-id="1a54a-105">An encoding job is associated with an input asset (or assets) on which you want to perform some encoding tasks.</span></span> <span data-ttu-id="1a54a-106">Por ejemplo, codificar un archivo MP4 en conjuntos MP4 de velocidad de bits adaptable H.264; crear una miniatura; crear superposiciones.</span><span class="sxs-lookup"><span data-stu-id="1a54a-106">For example, encode an MP4 file to H.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="1a54a-107">Tras la finalización de una tarea, se produce un recurso de salida.</span><span class="sxs-lookup"><span data-stu-id="1a54a-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="1a54a-108">El recurso de salida contiene vídeo, audio, miniaturas, etc. El recurso de salida también contiene un archivo con metadatos sobre el recurso de salida.</span><span class="sxs-lookup"><span data-stu-id="1a54a-108">The output asset contains video, audio, thumbnails, etc. The output asset also contains a file with metadata about the output asset.</span></span> <span data-ttu-id="1a54a-109">El nombre del archivo XML de metadatos tiene el formato siguiente: &lt;nombre_de_archivo_de_origen&gt;_manifest.xml (por ejemplo, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="1a54a-109">The name of the metadata XML file has the following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="1a54a-110">Si desea examinar el archivo de metadatos, puede crear un localizador **SAS** y descargar el archivo en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="1a54a-110">If you want to examine the metadata file, you can create a **SAS** locator and download the file to your local computer.</span></span>  

<span data-ttu-id="1a54a-111">En este tema se describen los elementos y los tipos del esquema XML en que se basan los metadatos de salida (&lt;nombre_de_archivo_de_origen&gt;_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="1a54a-111">This topic discusses the elements and types of the XML schema on which the output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="1a54a-112">Para información acerca del archivo que contiene metadatos sobre el recurso de entada, consulte [Input Metadata](media-services-input-metadata-schema.md) (Metadatos de entrada).</span><span class="sxs-lookup"><span data-stu-id="1a54a-112">For information about the file that contains metadata about the input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="1a54a-113">Puede encontrar el código del esquema completo y un ejemplo de XML al final de este tema.</span><span class="sxs-lookup"><span data-stu-id="1a54a-113">You can find the complete schema code and XML example at the end of this topic.</span></span>  
>
>

## <span data-ttu-id="1a54a-114"><a name="AssetFiles "></a> Elemento raíz AssetFiles</span><span class="sxs-lookup"><span data-stu-id="1a54a-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="1a54a-115">Colección de entradas AssetFile para el trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="1a54a-115">Collection of AssetFile entries for the encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="1a54a-116">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="1a54a-116">Child elements</span></span>
| <span data-ttu-id="1a54a-117">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-117">Name</span></span> | <span data-ttu-id="1a54a-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a54a-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="1a54a-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="1a54a-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="1a54a-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="1a54a-121">Un [elemento AssetFile](media-services-output-metadata-schema.md) que forma parte de la colección de AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="1a54a-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of the AssetFiles collection.</span></span> |

## <span data-ttu-id="1a54a-122"><a name="AssetFile "></a> Elemento AssetFile</span><span class="sxs-lookup"><span data-stu-id="1a54a-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="1a54a-123">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="1a54a-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="1a54a-124">Atributos</span><span class="sxs-lookup"><span data-stu-id="1a54a-124">Attributes</span></span>
| <span data-ttu-id="1a54a-125">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-125">Name</span></span> | <span data-ttu-id="1a54a-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a54a-126">Type</span></span> | <span data-ttu-id="1a54a-127">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a54a-128">**Name**</span><span class="sxs-lookup"><span data-stu-id="1a54a-128">**Name**</span></span><br/><br/> <span data-ttu-id="1a54a-129">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-129">Required</span></span> |<span data-ttu-id="1a54a-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="1a54a-130">**xs:string**</span></span> |<span data-ttu-id="1a54a-131">Nombre del archivo de recursos multimedia.</span><span class="sxs-lookup"><span data-stu-id="1a54a-131">The media asset file name.</span></span> |
| <span data-ttu-id="1a54a-132">**Tamaño**</span><span class="sxs-lookup"><span data-stu-id="1a54a-132">**Size**</span></span><br/><br/> <span data-ttu-id="1a54a-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-134">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-134">Required</span></span> |<span data-ttu-id="1a54a-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="1a54a-135">**xs:long**</span></span> |<span data-ttu-id="1a54a-136">Tamaño del archivo de recursos en bytes.</span><span class="sxs-lookup"><span data-stu-id="1a54a-136">Size of the asset file in bytes.</span></span> |
| <span data-ttu-id="1a54a-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="1a54a-137">**Duration**</span></span><br/><br/> <span data-ttu-id="1a54a-138">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-138">Required</span></span> |<span data-ttu-id="1a54a-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="1a54a-139">**xs:duration**</span></span> |<span data-ttu-id="1a54a-140">Duración de la reproducción del contenido.</span><span class="sxs-lookup"><span data-stu-id="1a54a-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="1a54a-141">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="1a54a-141">Child elements</span></span>
| <span data-ttu-id="1a54a-142">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-142">Name</span></span> | <span data-ttu-id="1a54a-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a54a-144">**Sources**</span><span class="sxs-lookup"><span data-stu-id="1a54a-144">**Sources**</span></span> |<span data-ttu-id="1a54a-145">Colección de archivos multimedia de entrada/origen, que se procesa para producir este AssetFile.</span><span class="sxs-lookup"><span data-stu-id="1a54a-145">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span> <span data-ttu-id="1a54a-146">Para más información, consulte [Elemento Source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="1a54a-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="1a54a-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="1a54a-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="1a54a-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="1a54a-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="1a54a-149">Cada AssetFile físico puede contener cero o más pistas de vídeo intercaladas en un formato de contenedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="1a54a-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="1a54a-150">Se trata de la colección de todas esas pistas de vídeo.</span><span class="sxs-lookup"><span data-stu-id="1a54a-150">This is the collection of all those video tracks.</span></span> <span data-ttu-id="1a54a-151">Para más información, consulte [Elemento VideoTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="1a54a-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="1a54a-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="1a54a-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="1a54a-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="1a54a-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="1a54a-154">Cada AssetFile físico puede contener cero o más pistas de audio intercaladas en un formato de contenedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="1a54a-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="1a54a-155">Se trata de la colección de todas esas pistas de audio.</span><span class="sxs-lookup"><span data-stu-id="1a54a-155">This is the collection of all those audio tracks.</span></span> <span data-ttu-id="1a54a-156">Para más información, consulte [Elemento AudioTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="1a54a-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="1a54a-157"><a name="Sources "></a> Elemento Sources</span><span class="sxs-lookup"><span data-stu-id="1a54a-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="1a54a-158">Colección de archivos multimedia de entrada/origen, que se procesa para producir este AssetFile.</span><span class="sxs-lookup"><span data-stu-id="1a54a-158">Collection of input/source media files, that was processed in order to produce this AssetFile.</span></span>  

<span data-ttu-id="1a54a-159">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="1a54a-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="1a54a-160">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="1a54a-160">Child elements</span></span>
| <span data-ttu-id="1a54a-161">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-161">Name</span></span> | <span data-ttu-id="1a54a-162">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a54a-163">**Origen**</span><span class="sxs-lookup"><span data-stu-id="1a54a-163">**Source**</span></span><br/><br/> <span data-ttu-id="1a54a-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="1a54a-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="1a54a-165">Un archivo de entrada/origen que se usa al generar este recurso.</span><span class="sxs-lookup"><span data-stu-id="1a54a-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="1a54a-166">Para más información, consulte [Elemento Source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="1a54a-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="1a54a-167"><a name="Source "></a> Elemento Source</span><span class="sxs-lookup"><span data-stu-id="1a54a-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="1a54a-168">Un archivo de entrada/origen que se usa al generar este recurso.</span><span class="sxs-lookup"><span data-stu-id="1a54a-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="1a54a-169">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="1a54a-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="1a54a-170">Atributos</span><span class="sxs-lookup"><span data-stu-id="1a54a-170">Attributes</span></span>
| <span data-ttu-id="1a54a-171">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-171">Name</span></span> | <span data-ttu-id="1a54a-172">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a54a-172">Type</span></span> | <span data-ttu-id="1a54a-173">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a54a-174">**Name**</span><span class="sxs-lookup"><span data-stu-id="1a54a-174">**Name**</span></span><br/><br/> <span data-ttu-id="1a54a-175">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-175">Required</span></span> |<span data-ttu-id="1a54a-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="1a54a-176">**xs:string**</span></span> |<span data-ttu-id="1a54a-177">Nombre de archivo de origen de entrada.</span><span class="sxs-lookup"><span data-stu-id="1a54a-177">Input source file name.</span></span> |

## <span data-ttu-id="1a54a-178"><a name="VideoTracks "></a> Elemento VideoTracks</span><span class="sxs-lookup"><span data-stu-id="1a54a-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="1a54a-179">Cada AssetFile físico puede contener cero o más pistas de vídeo intercaladas en un formato de contenedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="1a54a-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="1a54a-180">Se trata de la colección de todas esas pistas de vídeo.</span><span class="sxs-lookup"><span data-stu-id="1a54a-180">This is the collection of all those video tracks.</span></span>  

<span data-ttu-id="1a54a-181">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="1a54a-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="1a54a-182">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="1a54a-182">Child elements</span></span>
| <span data-ttu-id="1a54a-183">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-183">Name</span></span> | <span data-ttu-id="1a54a-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a54a-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="1a54a-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="1a54a-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="1a54a-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="1a54a-187">Una determinada pista de vídeo en el AssetFile primario.</span><span class="sxs-lookup"><span data-stu-id="1a54a-187">A specific video track in the parent AssetFile.</span></span> <span data-ttu-id="1a54a-188">Para más información, consulte [Elemento VideoTrack](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="1a54a-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="1a54a-189"><a name="VideoTrack"></a> Elemento VideoTrack</span><span class="sxs-lookup"><span data-stu-id="1a54a-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="1a54a-190">Una determinada pista de vídeo en el AssetFile primario.</span><span class="sxs-lookup"><span data-stu-id="1a54a-190">A specific video track in the parent AssetFile.</span></span>  

<span data-ttu-id="1a54a-191">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="1a54a-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="1a54a-192">Atributos</span><span class="sxs-lookup"><span data-stu-id="1a54a-192">Attributes</span></span>
| <span data-ttu-id="1a54a-193">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-193">Name</span></span> | <span data-ttu-id="1a54a-194">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a54a-194">Type</span></span> | <span data-ttu-id="1a54a-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a54a-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="1a54a-196">**Id**</span></span><br/><br/> <span data-ttu-id="1a54a-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-198">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-198">Required</span></span> |<span data-ttu-id="1a54a-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-199">**xs:int**</span></span> |<span data-ttu-id="1a54a-200">Índice de base cero de esta pista de vídeo. **Nota:** No es necesariamente el elemento TrackID que se usa en un archivo MP4.</span><span class="sxs-lookup"><span data-stu-id="1a54a-200">Zero-based index of this video track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="1a54a-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="1a54a-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="1a54a-202">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-202">Required</span></span> |<span data-ttu-id="1a54a-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="1a54a-203">**xs:string**</span></span> |<span data-ttu-id="1a54a-204">Código FourCC de códec de vídeo.</span><span class="sxs-lookup"><span data-stu-id="1a54a-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="1a54a-205">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="1a54a-205">**Profile**</span></span> |<span data-ttu-id="1a54a-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="1a54a-206">**xs:string**</span></span> |<span data-ttu-id="1a54a-207">Perfil de H264 (solo es aplicable al códec H264).</span><span class="sxs-lookup"><span data-stu-id="1a54a-207">H264 profile (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="1a54a-208">**Level**</span><span class="sxs-lookup"><span data-stu-id="1a54a-208">**Level**</span></span> |<span data-ttu-id="1a54a-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="1a54a-209">**xs:string**</span></span> |<span data-ttu-id="1a54a-210">Nivel de H264 (solo es aplicable al códec H264).</span><span class="sxs-lookup"><span data-stu-id="1a54a-210">H264 level (only applicable to H264 codec).</span></span> |
| <span data-ttu-id="1a54a-211">**Width**</span><span class="sxs-lookup"><span data-stu-id="1a54a-211">**Width**</span></span><br/><br/> <span data-ttu-id="1a54a-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-213">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-213">Required</span></span> |<span data-ttu-id="1a54a-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-214">**xs:int**</span></span> |<span data-ttu-id="1a54a-215">Ancho del vídeo codificado en píxeles.</span><span class="sxs-lookup"><span data-stu-id="1a54a-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="1a54a-216">**Height**</span><span class="sxs-lookup"><span data-stu-id="1a54a-216">**Height**</span></span><br/><br/> <span data-ttu-id="1a54a-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-218">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-218">Required</span></span> |<span data-ttu-id="1a54a-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-219">**xs:int**</span></span> |<span data-ttu-id="1a54a-220">Alto del vídeo codificado en píxeles.</span><span class="sxs-lookup"><span data-stu-id="1a54a-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="1a54a-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="1a54a-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="1a54a-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-223">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-223">Required</span></span> |<span data-ttu-id="1a54a-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="1a54a-224">**xs:double**</span></span> |<span data-ttu-id="1a54a-225">Numerador de la relación de aspecto de pantalla de vídeo.</span><span class="sxs-lookup"><span data-stu-id="1a54a-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="1a54a-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="1a54a-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="1a54a-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-228">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-228">Required</span></span> |<span data-ttu-id="1a54a-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="1a54a-229">**xs:double**</span></span> |<span data-ttu-id="1a54a-230">Denominador de la relación de aspecto de pantalla de vídeo.</span><span class="sxs-lookup"><span data-stu-id="1a54a-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="1a54a-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="1a54a-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="1a54a-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-233">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-233">Required</span></span> |<span data-ttu-id="1a54a-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="1a54a-234">**xs:decimal**</span></span> |<span data-ttu-id="1a54a-235">Velocidad de fotogramas de vídeo medida en formato .3f.</span><span class="sxs-lookup"><span data-stu-id="1a54a-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="1a54a-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="1a54a-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="1a54a-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-238">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-238">Required</span></span> |<span data-ttu-id="1a54a-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="1a54a-239">**xs:decimal**</span></span> |<span data-ttu-id="1a54a-240">Velocidad de fotogramas de vídeo de destino preestablecida en formato .3f.</span><span class="sxs-lookup"><span data-stu-id="1a54a-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="1a54a-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="1a54a-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="1a54a-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-243">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-243">Required</span></span> |<span data-ttu-id="1a54a-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-244">**xs:int**</span></span> |<span data-ttu-id="1a54a-245">Velocidad de bits de vídeo media en kilobits por segundo, según los cálculos de AssetFile.</span><span class="sxs-lookup"><span data-stu-id="1a54a-245">Average video bit rate in kilobits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="1a54a-246">Solo cuenta la carga de transmisión básica y no incluye la sobrecarga de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="1a54a-246">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="1a54a-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="1a54a-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="1a54a-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-249">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-249">Required</span></span> |<span data-ttu-id="1a54a-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-250">**xs:int**</span></span> |<span data-ttu-id="1a54a-251">Velocidad de bits media de destino para esta pista de vídeo, tal como se ha solicitado mediante la codificación preestablecida, en kilobits por segundo.</span><span class="sxs-lookup"><span data-stu-id="1a54a-251">Target average bitrate for this video track, as requested via the encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="1a54a-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="1a54a-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="1a54a-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-253">minInclusive ="0"</span></span> |<span data-ttu-id="1a54a-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-254">**xs:int**</span></span> |<span data-ttu-id="1a54a-255">Velocidad de bits media máxima para GOP, en kilobits por segundo.</span><span class="sxs-lookup"><span data-stu-id="1a54a-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="1a54a-256"><a name="AudioTracks "></a> Elemento AudioTracks</span><span class="sxs-lookup"><span data-stu-id="1a54a-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="1a54a-257">Cada AssetFile físico puede contener cero o más pistas de audio intercaladas en un formato de contenedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="1a54a-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="1a54a-258">Se trata de la colección de todas esas pistas de audio.</span><span class="sxs-lookup"><span data-stu-id="1a54a-258">This is the collection of all those audio tracks.</span></span>  

<span data-ttu-id="1a54a-259">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="1a54a-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="1a54a-260">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="1a54a-260">Child elements</span></span>
| <span data-ttu-id="1a54a-261">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-261">Name</span></span> | <span data-ttu-id="1a54a-262">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a54a-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="1a54a-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="1a54a-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="1a54a-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="1a54a-265">Una determinada pista de audio en el AssetFile primario.</span><span class="sxs-lookup"><span data-stu-id="1a54a-265">A specific audio track in the parent AssetFile.</span></span> <span data-ttu-id="1a54a-266">Para más información, consulte [Elemento AudioTrack](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="1a54a-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="1a54a-267"><a name="AudioTrack "></a> Elemento AudioTrack</span><span class="sxs-lookup"><span data-stu-id="1a54a-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="1a54a-268">Una determinada pista de audio en el AssetFile primario.</span><span class="sxs-lookup"><span data-stu-id="1a54a-268">A specific audio track in the parent AssetFile.</span></span>  

<span data-ttu-id="1a54a-269">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="1a54a-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="1a54a-270">Atributos</span><span class="sxs-lookup"><span data-stu-id="1a54a-270">Attributes</span></span>
| <span data-ttu-id="1a54a-271">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-271">Name</span></span> | <span data-ttu-id="1a54a-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a54a-272">Type</span></span> | <span data-ttu-id="1a54a-273">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a54a-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="1a54a-274">**Id**</span></span><br/><br/> <span data-ttu-id="1a54a-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-276">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-276">Required</span></span> |<span data-ttu-id="1a54a-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-277">**xs:int**</span></span> |<span data-ttu-id="1a54a-278">Índice de base cero de esta pista de audio. **Nota:** No es necesariamente el elemento TrackID que se usa en un archivo MP4.</span><span class="sxs-lookup"><span data-stu-id="1a54a-278">Zero-based index of this audio track. **Note:**  This is not necessarily the TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="1a54a-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="1a54a-279">**Codec**</span></span> |<span data-ttu-id="1a54a-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="1a54a-280">**xs:string**</span></span> |<span data-ttu-id="1a54a-281">Cadena de códec de pista de audio.</span><span class="sxs-lookup"><span data-stu-id="1a54a-281">Audio track codec string.</span></span> |
| <span data-ttu-id="1a54a-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="1a54a-282">**EncoderVersion**</span></span> |<span data-ttu-id="1a54a-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="1a54a-283">**xs:string**</span></span> |<span data-ttu-id="1a54a-284">Cadena de versión de codificador opcional, requerida para EAC3.</span><span class="sxs-lookup"><span data-stu-id="1a54a-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="1a54a-285">**Channels**</span><span class="sxs-lookup"><span data-stu-id="1a54a-285">**Channels**</span></span><br/><br/> <span data-ttu-id="1a54a-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-287">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-287">Required</span></span> |<span data-ttu-id="1a54a-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-288">**xs:int**</span></span> |<span data-ttu-id="1a54a-289">Número de canales de audio.</span><span class="sxs-lookup"><span data-stu-id="1a54a-289">Number of audio channels.</span></span> |
| <span data-ttu-id="1a54a-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="1a54a-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="1a54a-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-292">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-292">Required</span></span> |<span data-ttu-id="1a54a-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-293">**xs:int**</span></span> |<span data-ttu-id="1a54a-294">Velocidad de muestreo de audio en muestras/s o Hz.</span><span class="sxs-lookup"><span data-stu-id="1a54a-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="1a54a-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="1a54a-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="1a54a-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-297">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-297">Required</span></span> |<span data-ttu-id="1a54a-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-298">**xs:int**</span></span> |<span data-ttu-id="1a54a-299">Velocidad de bits de audio media en bits por segundo, según los cálculos de AssetFile.</span><span class="sxs-lookup"><span data-stu-id="1a54a-299">Average audio bit rate in bits per second, as calculated from the AssetFile.</span></span> <span data-ttu-id="1a54a-300">Solo cuenta la carga de transmisión básica y no incluye la sobrecarga de empaquetado.</span><span class="sxs-lookup"><span data-stu-id="1a54a-300">Counts only the elementary stream payload, and does not include the packaging overhead.</span></span> |
| <span data-ttu-id="1a54a-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="1a54a-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="1a54a-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="1a54a-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="1a54a-303">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-303">Required</span></span> |<span data-ttu-id="1a54a-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-304">**xs:int**</span></span> |<span data-ttu-id="1a54a-305">Bits por muestra para el tipo de formato wFormatTag.</span><span class="sxs-lookup"><span data-stu-id="1a54a-305">Bits per sample for the wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="1a54a-306">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="1a54a-306">Child elements</span></span>
| <span data-ttu-id="1a54a-307">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-307">Name</span></span> | <span data-ttu-id="1a54a-308">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a54a-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="1a54a-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="1a54a-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="1a54a-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="1a54a-311">Parámetros de resultado de medición de la sonoridad.</span><span class="sxs-lookup"><span data-stu-id="1a54a-311">Loudness metering result parameters.</span></span> <span data-ttu-id="1a54a-312">Para más información, consulte [Elemento LoudnessMeteringResultParameters](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="1a54a-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="1a54a-313"><a name="LoudnessMeteringResultParameters "></a> Elemento LoudnessMeteringResultParameters</span><span class="sxs-lookup"><span data-stu-id="1a54a-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="1a54a-314">Parámetros de resultado de medición de la sonoridad.</span><span class="sxs-lookup"><span data-stu-id="1a54a-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="1a54a-315">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="1a54a-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="1a54a-316">Atributos</span><span class="sxs-lookup"><span data-stu-id="1a54a-316">Attributes</span></span>
| <span data-ttu-id="1a54a-317">Nombre</span><span class="sxs-lookup"><span data-stu-id="1a54a-317">Name</span></span> | <span data-ttu-id="1a54a-318">Tipo</span><span class="sxs-lookup"><span data-stu-id="1a54a-318">Type</span></span> | <span data-ttu-id="1a54a-319">Descripción</span><span class="sxs-lookup"><span data-stu-id="1a54a-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1a54a-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="1a54a-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="1a54a-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="1a54a-321">**xs:string**</span></span> |<span data-ttu-id="1a54a-322">Versión del kit de desarrollo de medición de sonoridad profesional **Dolby**.</span><span class="sxs-lookup"><span data-stu-id="1a54a-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="1a54a-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="1a54a-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="1a54a-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="1a54a-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="1a54a-325">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-325">Required</span></span> |<span data-ttu-id="1a54a-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="1a54a-326">**xs:int**</span></span> |<span data-ttu-id="1a54a-327">DialogNormalization generado mediante DPLM, requerido si LoudnessMetering está establecido.</span><span class="sxs-lookup"><span data-stu-id="1a54a-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="1a54a-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="1a54a-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="1a54a-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="1a54a-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="1a54a-330">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-330">Required</span></span> |<span data-ttu-id="1a54a-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="1a54a-331">**xs:float**</span></span> |<span data-ttu-id="1a54a-332">Sonoridad integrada.</span><span class="sxs-lookup"><span data-stu-id="1a54a-332">Integrated loudness</span></span> |
| <span data-ttu-id="1a54a-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="1a54a-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="1a54a-334">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-334">Required</span></span> |<span data-ttu-id="1a54a-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="1a54a-335">**xs:string**</span></span> |<span data-ttu-id="1a54a-336">Unidad de sonoridad integrada.</span><span class="sxs-lookup"><span data-stu-id="1a54a-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="1a54a-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="1a54a-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="1a54a-338">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-338">Required</span></span> |<span data-ttu-id="1a54a-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="1a54a-339">**xs:string**</span></span> |<span data-ttu-id="1a54a-340">Identificador de acceso.</span><span class="sxs-lookup"><span data-stu-id="1a54a-340">Gating identifier</span></span> |
| <span data-ttu-id="1a54a-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="1a54a-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="1a54a-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="1a54a-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="1a54a-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="1a54a-343">**xs:float**</span></span> |<span data-ttu-id="1a54a-344">Contenido de voz sobre el programa, en forma de porcentaje.</span><span class="sxs-lookup"><span data-stu-id="1a54a-344">Speech content over the program, as a percentage.</span></span> |
| <span data-ttu-id="1a54a-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="1a54a-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="1a54a-346">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-346">Required</span></span> |<span data-ttu-id="1a54a-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="1a54a-347">**xs:float**</span></span> |<span data-ttu-id="1a54a-348">Valor pico de ejemplo absoluto, desde el restablecimiento o desde la última vez que se desactivó, por canal.</span><span class="sxs-lookup"><span data-stu-id="1a54a-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="1a54a-349">Las unidades son dBFS.</span><span class="sxs-lookup"><span data-stu-id="1a54a-349">Units are dBFS.</span></span> |
| <span data-ttu-id="1a54a-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="1a54a-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="1a54a-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="1a54a-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="1a54a-352">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-352">Required</span></span> |<span data-ttu-id="1a54a-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="1a54a-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="1a54a-354">Unidad pico de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="1a54a-354">Sample peak unit.</span></span> |
| <span data-ttu-id="1a54a-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="1a54a-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="1a54a-356">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-356">Required</span></span> |<span data-ttu-id="1a54a-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="1a54a-357">**xs:float**</span></span> |<span data-ttu-id="1a54a-358">Valor pico verdadero máximo, según ITU-R BS.1770-2, desde el restablecimiento o desde la última vez que se desactivó, por canal.</span><span class="sxs-lookup"><span data-stu-id="1a54a-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="1a54a-359">Las unidades son dBTP.</span><span class="sxs-lookup"><span data-stu-id="1a54a-359">Units are dBTP.</span></span> |
| <span data-ttu-id="1a54a-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="1a54a-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="1a54a-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="1a54a-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="1a54a-362">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="1a54a-362">Required</span></span> |<span data-ttu-id="1a54a-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="1a54a-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="1a54a-364">Unidad pico verdadera.</span><span class="sxs-lookup"><span data-stu-id="1a54a-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="1a54a-365">Código del esquema</span><span class="sxs-lookup"><span data-stu-id="1a54a-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for the encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order to produce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this video track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Width" use="required">  
                              <xs:annotation>  
                                <xs:documentation>encoded video width in pixels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Height" use="required">  
                              <xs:annotation>  
                                <xs:documentation>encoded video height in pixels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:double">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:double">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Framerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via the encoding preset, in kilobits per second</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="MaxGOPBitrate">  
                              <xs:annotation>  
                                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over the program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Channels" use="required">  
                              <xs:annotation>  
                                <xs:documentation>number of audio channels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="SamplingRate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>the media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <span data-ttu-id="1a54a-366"><a name="xml"></a> Ejemplo de XML</span><span class="sxs-lookup"><span data-stu-id="1a54a-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="1a54a-367">A continuación, sigue un ejemplo del archivo de metadatos de salida.</span><span class="sxs-lookup"><span data-stu-id="1a54a-367">The following is an example of the Output metadata file.</span></span>  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="1a54a-368">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a54a-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1a54a-369">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="1a54a-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]