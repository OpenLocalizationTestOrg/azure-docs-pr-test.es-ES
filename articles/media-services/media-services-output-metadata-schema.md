---
title: esquema de metadatos de salida de servicios multimedia de aaaAzure | Documentos de Microsoft
description: "tema de Hello ofrezca una visión general del esquema de metadatos de salida de servicios multimedia de Azure."
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
ms.openlocfilehash: 7f07d6accbe0b171d0408b15d5e1e6b5afd6c367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="output-metadata"></a><span data-ttu-id="251f1-103">Metadatos de salida</span><span class="sxs-lookup"><span data-stu-id="251f1-103">Output Metadata</span></span>
## <a name="overview"></a><span data-ttu-id="251f1-104">Información general</span><span class="sxs-lookup"><span data-stu-id="251f1-104">Overview</span></span>
<span data-ttu-id="251f1-105">Un trabajo de codificación está asociado a un recurso de entrada (o activos) en el que desea tooperform algunas tareas de codificación.</span><span class="sxs-lookup"><span data-stu-id="251f1-105">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span> <span data-ttu-id="251f1-106">Por ejemplo, codificar una velocidad de bits MP4 adaptable tooH.264 MP4 de archivo establece; crear una vista en miniatura; Crear superposiciones.</span><span class="sxs-lookup"><span data-stu-id="251f1-106">For example, encode an MP4 file tooH.264 MP4 adaptive bitrate sets; create a thumbnail; create overlays.</span></span> <span data-ttu-id="251f1-107">Tras la finalización de una tarea, se produce un recurso de salida.</span><span class="sxs-lookup"><span data-stu-id="251f1-107">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="251f1-108">Hola activo de salida contiene vídeo, audio, miniaturas, etc. activo de salida de hello también contiene un archivo con metadatos sobre el recurso de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="251f1-108">hello output asset contains video, audio, thumbnails, etc. hello output asset also contains a file with metadata about hello output asset.</span></span> <span data-ttu-id="251f1-109">nombre del archivo XML de metadatos de hello Hello tiene Hola siguiendo el formato: &lt;nombre_archivo_origen&gt;_manifest.xml (por ejemplo, BigBuckBunny_manifest.xml).</span><span class="sxs-lookup"><span data-stu-id="251f1-109">hello name of hello metadata XML file has hello following format: &lt;source_file_name&gt;_manifest.xml (for example, BigBuckBunny_manifest.xml).</span></span>  

<span data-ttu-id="251f1-110">Si desea que el archivo de metadatos de hello tooexamine, puede crear un **SAS** localizador y descarga Hola ordenador tooyour de archivo.</span><span class="sxs-lookup"><span data-stu-id="251f1-110">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span>  

<span data-ttu-id="251f1-111">Este tema describen los elementos de Hola y tipos de esquema XML de Hola en los metadatos de salida de hello (&lt;nombre_archivo_origen&gt;_manifest.xml) se basa.</span><span class="sxs-lookup"><span data-stu-id="251f1-111">This topic discusses hello elements and types of hello XML schema on which hello output metada (&lt;source_file_name&gt;_manifest.xml) is based.</span></span> <span data-ttu-id="251f1-112">Para obtener información sobre el archivo hello que contiene metadatos sobre el recurso de entrada de hello, consulte [entrada metadatos](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="251f1-112">For information about hello file that contains metadata about hello input asset, see [Input Metadata](media-services-input-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="251f1-113">Puede encontrar código de esquema completo de Hola y ejemplo de XML al final de Hola de este tema.</span><span class="sxs-lookup"><span data-stu-id="251f1-113">You can find hello complete schema code and XML example at hello end of this topic.</span></span>  
>
>

## <span data-ttu-id="251f1-114"><a name="AssetFiles "></a> Elemento raíz AssetFiles</span><span class="sxs-lookup"><span data-stu-id="251f1-114"><a name="AssetFiles "></a> AssetFiles root element</span></span>
<span data-ttu-id="251f1-115">Colección de entradas de AssetFile para el trabajo de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f1-115">Collection of AssetFile entries for hello encoding job.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="251f1-116">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="251f1-116">Child elements</span></span>
| <span data-ttu-id="251f1-117">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-117">Name</span></span> | <span data-ttu-id="251f1-118">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="251f1-119">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="251f1-119">**AssetFile**</span></span><br/><br/> <span data-ttu-id="251f1-120">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="251f1-120">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="251f1-121">Un [AssetFile elemento](media-services-output-metadata-schema.md) que forma parte del programa Hola colección AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="251f1-121">An [AssetFile element](media-services-output-metadata-schema.md) that is part of hello AssetFiles collection.</span></span> |

## <span data-ttu-id="251f1-122"><a name="AssetFile "></a> Elemento AssetFile</span><span class="sxs-lookup"><span data-stu-id="251f1-122"><a name="AssetFile "></a> AssetFile element</span></span>
<span data-ttu-id="251f1-123">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="251f1-123">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="251f1-124">Atributos</span><span class="sxs-lookup"><span data-stu-id="251f1-124">Attributes</span></span>
| <span data-ttu-id="251f1-125">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-125">Name</span></span> | <span data-ttu-id="251f1-126">Tipo</span><span class="sxs-lookup"><span data-stu-id="251f1-126">Type</span></span> | <span data-ttu-id="251f1-127">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="251f1-128">**Name**</span><span class="sxs-lookup"><span data-stu-id="251f1-128">**Name**</span></span><br/><br/> <span data-ttu-id="251f1-129">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-129">Required</span></span> |<span data-ttu-id="251f1-130">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="251f1-130">**xs:string**</span></span> |<span data-ttu-id="251f1-131">nombre del archivo del recurso multimedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f1-131">hello media asset file name.</span></span> |
| <span data-ttu-id="251f1-132">**Tamaño**</span><span class="sxs-lookup"><span data-stu-id="251f1-132">**Size**</span></span><br/><br/> <span data-ttu-id="251f1-133">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-133">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-134">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-134">Required</span></span> |<span data-ttu-id="251f1-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="251f1-135">**xs:long**</span></span> |<span data-ttu-id="251f1-136">Tamaño de archivo de recursos de hello en bytes.</span><span class="sxs-lookup"><span data-stu-id="251f1-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="251f1-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="251f1-137">**Duration**</span></span><br/><br/> <span data-ttu-id="251f1-138">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-138">Required</span></span> |<span data-ttu-id="251f1-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="251f1-139">**xs:duration**</span></span> |<span data-ttu-id="251f1-140">Duración de la reproducción del contenido.</span><span class="sxs-lookup"><span data-stu-id="251f1-140">Content play back duration.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="251f1-141">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="251f1-141">Child elements</span></span>
| <span data-ttu-id="251f1-142">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-142">Name</span></span> | <span data-ttu-id="251f1-143">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="251f1-144">**Sources**</span><span class="sxs-lookup"><span data-stu-id="251f1-144">**Sources**</span></span> |<span data-ttu-id="251f1-145">Colección de archivos de entrada/origen multimedia, que se procesa en orden tooproduce este AssetFile.</span><span class="sxs-lookup"><span data-stu-id="251f1-145">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span> <span data-ttu-id="251f1-146">Para más información, consulte [Elemento Source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="251f1-146">For more information, see [Source element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="251f1-147">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="251f1-147">**VideoTracks**</span></span><br/><br/> <span data-ttu-id="251f1-148">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="251f1-148">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="251f1-149">Cada AssetFile físico puede contener cero o más pistas de vídeo intercaladas en un formato de contenedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="251f1-149">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="251f1-150">Se trata de una colección de Hola de todas esas pistas de vídeo.</span><span class="sxs-lookup"><span data-stu-id="251f1-150">This is hello collection of all those video tracks.</span></span> <span data-ttu-id="251f1-151">Para más información, consulte [Elemento VideoTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="251f1-151">For more information, see [VideoTracks element](media-services-output-metadata-schema.md).</span></span> |
| <span data-ttu-id="251f1-152">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="251f1-152">**AudioTracks**</span></span><br/><br/> <span data-ttu-id="251f1-153">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="251f1-153">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="251f1-154">Cada AssetFile físico puede contener cero o más pistas de audio intercaladas en un formato de contenedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="251f1-154">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="251f1-155">Se trata de una colección de Hola de todas esas pistas de audio.</span><span class="sxs-lookup"><span data-stu-id="251f1-155">This is hello collection of all those audio tracks.</span></span> <span data-ttu-id="251f1-156">Para más información, consulte [Elemento AudioTracks](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="251f1-156">For more information, see [AudioTracks element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="251f1-157"><a name="Sources "></a> Elemento Sources</span><span class="sxs-lookup"><span data-stu-id="251f1-157"><a name="Sources "></a> Sources element</span></span>
<span data-ttu-id="251f1-158">Colección de archivos de entrada/origen multimedia, que se procesa en orden tooproduce este AssetFile.</span><span class="sxs-lookup"><span data-stu-id="251f1-158">Collection of input/source media files, that was processed in order tooproduce this AssetFile.</span></span>  

<span data-ttu-id="251f1-159">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="251f1-159">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="251f1-160">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="251f1-160">Child elements</span></span>
| <span data-ttu-id="251f1-161">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-161">Name</span></span> | <span data-ttu-id="251f1-162">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-162">Description</span></span> |
| --- | --- |
| <span data-ttu-id="251f1-163">**Origen**</span><span class="sxs-lookup"><span data-stu-id="251f1-163">**Source**</span></span><br/><br/> <span data-ttu-id="251f1-164">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="251f1-164">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="251f1-165">Un archivo de entrada/origen que se usa al generar este recurso.</span><span class="sxs-lookup"><span data-stu-id="251f1-165">An input/source file used when generating this asset.</span></span> <span data-ttu-id="251f1-166">Para más información, consulte [Elemento Source](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="251f1-166">For more information see [Source element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="251f1-167"><a name="Source "></a> Elemento Source</span><span class="sxs-lookup"><span data-stu-id="251f1-167"><a name="Source "></a> Source element</span></span>
<span data-ttu-id="251f1-168">Un archivo de entrada/origen que se usa al generar este recurso.</span><span class="sxs-lookup"><span data-stu-id="251f1-168">An input/source file used when generating this asset.</span></span>  

<span data-ttu-id="251f1-169">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="251f1-169">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="251f1-170">Atributos</span><span class="sxs-lookup"><span data-stu-id="251f1-170">Attributes</span></span>
| <span data-ttu-id="251f1-171">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-171">Name</span></span> | <span data-ttu-id="251f1-172">Tipo</span><span class="sxs-lookup"><span data-stu-id="251f1-172">Type</span></span> | <span data-ttu-id="251f1-173">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-173">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="251f1-174">**Name**</span><span class="sxs-lookup"><span data-stu-id="251f1-174">**Name**</span></span><br/><br/> <span data-ttu-id="251f1-175">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-175">Required</span></span> |<span data-ttu-id="251f1-176">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="251f1-176">**xs:string**</span></span> |<span data-ttu-id="251f1-177">Nombre de archivo de origen de entrada.</span><span class="sxs-lookup"><span data-stu-id="251f1-177">Input source file name.</span></span> |

## <span data-ttu-id="251f1-178"><a name="VideoTracks "></a> Elemento VideoTracks</span><span class="sxs-lookup"><span data-stu-id="251f1-178"><a name="VideoTracks "></a> VideoTracks element</span></span>
<span data-ttu-id="251f1-179">Cada AssetFile físico puede contener cero o más pistas de vídeo intercaladas en un formato de contenedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="251f1-179">Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="251f1-180">Se trata de una colección de Hola de todas esas pistas de vídeo.</span><span class="sxs-lookup"><span data-stu-id="251f1-180">This is hello collection of all those video tracks.</span></span>  

<span data-ttu-id="251f1-181">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="251f1-181">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="251f1-182">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="251f1-182">Child elements</span></span>
| <span data-ttu-id="251f1-183">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-183">Name</span></span> | <span data-ttu-id="251f1-184">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-184">Description</span></span> |
| --- | --- |
| <span data-ttu-id="251f1-185">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="251f1-185">**VideoTrack**</span></span><br/><br/> <span data-ttu-id="251f1-186">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="251f1-186">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="251f1-187">Una pista de vídeo específica en el AssetFile principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f1-187">A specific video track in hello parent AssetFile.</span></span> <span data-ttu-id="251f1-188">Para más información, consulte [Elemento VideoTrack](media-services-output-metadata-schema.md#VideoTrack).</span><span class="sxs-lookup"><span data-stu-id="251f1-188">For more information, see [VideoTrack element](media-services-output-metadata-schema.md#VideoTrack).</span></span> |

## <span data-ttu-id="251f1-189"><a name="VideoTrack"></a> Elemento VideoTrack</span><span class="sxs-lookup"><span data-stu-id="251f1-189"><a name="VideoTrack"></a> VideoTrack element</span></span>
<span data-ttu-id="251f1-190">Una pista de vídeo específica en el AssetFile principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f1-190">A specific video track in hello parent AssetFile.</span></span>  

<span data-ttu-id="251f1-191">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="251f1-191">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="251f1-192">Atributos</span><span class="sxs-lookup"><span data-stu-id="251f1-192">Attributes</span></span>
| <span data-ttu-id="251f1-193">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-193">Name</span></span> | <span data-ttu-id="251f1-194">Tipo</span><span class="sxs-lookup"><span data-stu-id="251f1-194">Type</span></span> | <span data-ttu-id="251f1-195">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-195">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="251f1-196">**Id**</span><span class="sxs-lookup"><span data-stu-id="251f1-196">**Id**</span></span><br/><br/> <span data-ttu-id="251f1-197">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-197">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-198">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-198">Required</span></span> |<span data-ttu-id="251f1-199">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-199">**xs:int**</span></span> |<span data-ttu-id="251f1-200">Índice de base cero de esta pista de vídeo. **Nota:** esto no es necesariamente hello trackid tal y como se utiliza en un archivo MP4.</span><span class="sxs-lookup"><span data-stu-id="251f1-200">Zero-based index of this video track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="251f1-201">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="251f1-201">**FourCC**</span></span><br/><br/> <span data-ttu-id="251f1-202">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-202">Required</span></span> |<span data-ttu-id="251f1-203">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="251f1-203">**xs:string**</span></span> |<span data-ttu-id="251f1-204">Código FourCC de códec de vídeo.</span><span class="sxs-lookup"><span data-stu-id="251f1-204">Video codec FourCC code.</span></span> |
| <span data-ttu-id="251f1-205">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="251f1-205">**Profile**</span></span> |<span data-ttu-id="251f1-206">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="251f1-206">**xs:string**</span></span> |<span data-ttu-id="251f1-207">Perfil H264 (solo aplicable tooH264 códec).</span><span class="sxs-lookup"><span data-stu-id="251f1-207">H264 profile (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="251f1-208">**Level**</span><span class="sxs-lookup"><span data-stu-id="251f1-208">**Level**</span></span> |<span data-ttu-id="251f1-209">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="251f1-209">**xs:string**</span></span> |<span data-ttu-id="251f1-210">Nivel H264 (solo aplicable tooH264 códec).</span><span class="sxs-lookup"><span data-stu-id="251f1-210">H264 level (only applicable tooH264 codec).</span></span> |
| <span data-ttu-id="251f1-211">**Width**</span><span class="sxs-lookup"><span data-stu-id="251f1-211">**Width**</span></span><br/><br/> <span data-ttu-id="251f1-212">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-212">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-213">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-213">Required</span></span> |<span data-ttu-id="251f1-214">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-214">**xs:int**</span></span> |<span data-ttu-id="251f1-215">Ancho del vídeo codificado en píxeles.</span><span class="sxs-lookup"><span data-stu-id="251f1-215">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="251f1-216">**Height**</span><span class="sxs-lookup"><span data-stu-id="251f1-216">**Height**</span></span><br/><br/> <span data-ttu-id="251f1-217">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-217">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-218">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-218">Required</span></span> |<span data-ttu-id="251f1-219">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-219">**xs:int**</span></span> |<span data-ttu-id="251f1-220">Alto del vídeo codificado en píxeles.</span><span class="sxs-lookup"><span data-stu-id="251f1-220">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="251f1-221">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="251f1-221">**DisplayAspectRatioNumerator**</span></span><br/><br/> <span data-ttu-id="251f1-222">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-222">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-223">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-223">Required</span></span> |<span data-ttu-id="251f1-224">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="251f1-224">**xs:double**</span></span> |<span data-ttu-id="251f1-225">Numerador de la relación de aspecto de pantalla de vídeo.</span><span class="sxs-lookup"><span data-stu-id="251f1-225">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="251f1-226">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="251f1-226">**DisplayAspectRatioDenominator**</span></span><br/><br/> <span data-ttu-id="251f1-227">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-227">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-228">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-228">Required</span></span> |<span data-ttu-id="251f1-229">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="251f1-229">**xs:double**</span></span> |<span data-ttu-id="251f1-230">Denominador de la relación de aspecto de pantalla de vídeo.</span><span class="sxs-lookup"><span data-stu-id="251f1-230">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="251f1-231">**Framerate**</span><span class="sxs-lookup"><span data-stu-id="251f1-231">**Framerate**</span></span><br/><br/> <span data-ttu-id="251f1-232">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-232">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-233">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-233">Required</span></span> |<span data-ttu-id="251f1-234">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="251f1-234">**xs:decimal**</span></span> |<span data-ttu-id="251f1-235">Velocidad de fotogramas de vídeo medida en formato .3f.</span><span class="sxs-lookup"><span data-stu-id="251f1-235">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="251f1-236">**TargetFramerate**</span><span class="sxs-lookup"><span data-stu-id="251f1-236">**TargetFramerate**</span></span><br/><br/> <span data-ttu-id="251f1-237">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-237">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-238">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-238">Required</span></span> |<span data-ttu-id="251f1-239">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="251f1-239">**xs:decimal**</span></span> |<span data-ttu-id="251f1-240">Velocidad de fotogramas de vídeo de destino preestablecida en formato .3f.</span><span class="sxs-lookup"><span data-stu-id="251f1-240">Preset target video frame rate in .3f format.</span></span> |
| <span data-ttu-id="251f1-241">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="251f1-241">**Bitrate**</span></span><br/><br/> <span data-ttu-id="251f1-242">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-242">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-243">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-243">Required</span></span> |<span data-ttu-id="251f1-244">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-244">**xs:int**</span></span> |<span data-ttu-id="251f1-245">Velocidad de bits de vídeo Media en kilobits por segundo, según los cálculos de hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="251f1-245">Average video bit rate in kilobits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="251f1-246">Cuenta solo carga de secuencias básicas de hello y no incluye la sobrecarga de empaquetado de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f1-246">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="251f1-247">**TargetBitrate**</span><span class="sxs-lookup"><span data-stu-id="251f1-247">**TargetBitrate**</span></span><br/><br/> <span data-ttu-id="251f1-248">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-248">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-249">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-249">Required</span></span> |<span data-ttu-id="251f1-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-250">**xs:int**</span></span> |<span data-ttu-id="251f1-251">Destino de velocidad de bits Media para esta pista de vídeo, como se ha solicitado a través de hello valor predefinido de codificación, en kilobits por segundo.</span><span class="sxs-lookup"><span data-stu-id="251f1-251">Target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second.</span></span> |
| <span data-ttu-id="251f1-252">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="251f1-252">**MaxGOPBitrate**</span></span><br/><br/> <span data-ttu-id="251f1-253">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-253">minInclusive ="0"</span></span> |<span data-ttu-id="251f1-254">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-254">**xs:int**</span></span> |<span data-ttu-id="251f1-255">Velocidad de bits media máxima para GOP, en kilobits por segundo.</span><span class="sxs-lookup"><span data-stu-id="251f1-255">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |

## <span data-ttu-id="251f1-256"><a name="AudioTracks "></a> Elemento AudioTracks</span><span class="sxs-lookup"><span data-stu-id="251f1-256"><a name="AudioTracks "></a> AudioTracks element</span></span>
<span data-ttu-id="251f1-257">Cada AssetFile físico puede contener cero o más pistas de audio intercaladas en un formato de contenedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="251f1-257">Each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="251f1-258">Se trata de una colección de Hola de todas esas pistas de audio.</span><span class="sxs-lookup"><span data-stu-id="251f1-258">This is hello collection of all those audio tracks.</span></span>  

<span data-ttu-id="251f1-259">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="251f1-259">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="251f1-260">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="251f1-260">Child elements</span></span>
| <span data-ttu-id="251f1-261">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-261">Name</span></span> | <span data-ttu-id="251f1-262">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-262">Description</span></span> |
| --- | --- |
| <span data-ttu-id="251f1-263">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="251f1-263">**AudioTrack**</span></span><br/><br/> <span data-ttu-id="251f1-264">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="251f1-264">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="251f1-265">Una determinada pista de audio en AssetFile principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f1-265">A specific audio track in hello parent AssetFile.</span></span> <span data-ttu-id="251f1-266">Para más información, consulte [Elemento AudioTrack](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="251f1-266">For more information, see [AudioTrack element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="251f1-267"><a name="AudioTrack "></a> Elemento AudioTrack</span><span class="sxs-lookup"><span data-stu-id="251f1-267"><a name="AudioTrack "></a> AudioTrack element</span></span>
<span data-ttu-id="251f1-268">Una determinada pista de audio en AssetFile principal de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f1-268">A specific audio track in hello parent AssetFile.</span></span>  

<span data-ttu-id="251f1-269">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="251f1-269">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="251f1-270">Atributos</span><span class="sxs-lookup"><span data-stu-id="251f1-270">Attributes</span></span>
| <span data-ttu-id="251f1-271">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-271">Name</span></span> | <span data-ttu-id="251f1-272">Tipo</span><span class="sxs-lookup"><span data-stu-id="251f1-272">Type</span></span> | <span data-ttu-id="251f1-273">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-273">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="251f1-274">**Id**</span><span class="sxs-lookup"><span data-stu-id="251f1-274">**Id**</span></span><br/><br/> <span data-ttu-id="251f1-275">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-275">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-276">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-276">Required</span></span> |<span data-ttu-id="251f1-277">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-277">**xs:int**</span></span> |<span data-ttu-id="251f1-278">Índice de base cero de esta pista de audio. **Nota:** esto no es necesariamente hello trackid tal y como se utiliza en un archivo MP4.</span><span class="sxs-lookup"><span data-stu-id="251f1-278">Zero-based index of this audio track. **Note:**  This is not necessarily hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="251f1-279">**Codec**</span><span class="sxs-lookup"><span data-stu-id="251f1-279">**Codec**</span></span> |<span data-ttu-id="251f1-280">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="251f1-280">**xs:string**</span></span> |<span data-ttu-id="251f1-281">Cadena de códec de pista de audio.</span><span class="sxs-lookup"><span data-stu-id="251f1-281">Audio track codec string.</span></span> |
| <span data-ttu-id="251f1-282">**EncoderVersion**</span><span class="sxs-lookup"><span data-stu-id="251f1-282">**EncoderVersion**</span></span> |<span data-ttu-id="251f1-283">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="251f1-283">**xs:string**</span></span> |<span data-ttu-id="251f1-284">Cadena de versión de codificador opcional, requerida para EAC3.</span><span class="sxs-lookup"><span data-stu-id="251f1-284">Optional encoder version string, required for EAC3.</span></span> |
| <span data-ttu-id="251f1-285">**Channels**</span><span class="sxs-lookup"><span data-stu-id="251f1-285">**Channels**</span></span><br/><br/> <span data-ttu-id="251f1-286">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-286">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-287">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-287">Required</span></span> |<span data-ttu-id="251f1-288">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-288">**xs:int**</span></span> |<span data-ttu-id="251f1-289">Número de canales de audio.</span><span class="sxs-lookup"><span data-stu-id="251f1-289">Number of audio channels.</span></span> |
| <span data-ttu-id="251f1-290">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="251f1-290">**SamplingRate**</span></span><br/><br/> <span data-ttu-id="251f1-291">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-291">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-292">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-292">Required</span></span> |<span data-ttu-id="251f1-293">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-293">**xs:int**</span></span> |<span data-ttu-id="251f1-294">Velocidad de muestreo de audio en muestras/s o Hz.</span><span class="sxs-lookup"><span data-stu-id="251f1-294">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="251f1-295">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="251f1-295">**Bitrate**</span></span><br/><br/> <span data-ttu-id="251f1-296">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-296">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-297">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-297">Required</span></span> |<span data-ttu-id="251f1-298">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-298">**xs:int**</span></span> |<span data-ttu-id="251f1-299">Velocidad de bits de audio Media en bits por segundo, según los cálculos de hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="251f1-299">Average audio bit rate in bits per second, as calculated from hello AssetFile.</span></span> <span data-ttu-id="251f1-300">Cuenta solo carga de secuencias básicas de hello y no incluye la sobrecarga de empaquetado de Hola.</span><span class="sxs-lookup"><span data-stu-id="251f1-300">Counts only hello elementary stream payload, and does not include hello packaging overhead.</span></span> |
| <span data-ttu-id="251f1-301">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="251f1-301">**BitsPerSample**</span></span><br/><br/> <span data-ttu-id="251f1-302">minInclusive ="0"</span><span class="sxs-lookup"><span data-stu-id="251f1-302">minInclusive ="0"</span></span><br/><br/> <span data-ttu-id="251f1-303">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-303">Required</span></span> |<span data-ttu-id="251f1-304">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-304">**xs:int**</span></span> |<span data-ttu-id="251f1-305">Tipo de bits por muestra para el formato wFormatTag Hola.</span><span class="sxs-lookup"><span data-stu-id="251f1-305">Bits per sample for hello wFormatTag format type.</span></span> |

### <a name="child-elements"></a><span data-ttu-id="251f1-306">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="251f1-306">Child elements</span></span>
| <span data-ttu-id="251f1-307">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-307">Name</span></span> | <span data-ttu-id="251f1-308">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-308">Description</span></span> |
| --- | --- |
| <span data-ttu-id="251f1-309">**LoudnessMeteringResultParameters**</span><span class="sxs-lookup"><span data-stu-id="251f1-309">**LoudnessMeteringResultParameters**</span></span><br/><br/> <span data-ttu-id="251f1-310">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="251f1-310">minOccurs="0" maxOccurs="1"</span></span> |<span data-ttu-id="251f1-311">Parámetros de resultado de medición de la sonoridad.</span><span class="sxs-lookup"><span data-stu-id="251f1-311">Loudness metering result parameters.</span></span> <span data-ttu-id="251f1-312">Para más información, consulte [Elemento LoudnessMeteringResultParameters](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="251f1-312">For more information, see [LoudnessMeteringResultParameters element](media-services-output-metadata-schema.md).</span></span> |

## <span data-ttu-id="251f1-313"><a name="LoudnessMeteringResultParameters "></a> Elemento LoudnessMeteringResultParameters</span><span class="sxs-lookup"><span data-stu-id="251f1-313"><a name="LoudnessMeteringResultParameters "></a> LoudnessMeteringResultParameters element</span></span>
<span data-ttu-id="251f1-314">Parámetros de resultado de medición de la sonoridad.</span><span class="sxs-lookup"><span data-stu-id="251f1-314">Loudness metering result parameters.</span></span>  

<span data-ttu-id="251f1-315">Puede encontrar un ejemplo de XML en [Ejemplo de XML](media-services-output-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="251f1-315">You can find an XML example [XML example](media-services-output-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="251f1-316">Atributos</span><span class="sxs-lookup"><span data-stu-id="251f1-316">Attributes</span></span>
| <span data-ttu-id="251f1-317">Nombre</span><span class="sxs-lookup"><span data-stu-id="251f1-317">Name</span></span> | <span data-ttu-id="251f1-318">Tipo</span><span class="sxs-lookup"><span data-stu-id="251f1-318">Type</span></span> | <span data-ttu-id="251f1-319">Descripción</span><span class="sxs-lookup"><span data-stu-id="251f1-319">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="251f1-320">**DPLMVersionInformation**</span><span class="sxs-lookup"><span data-stu-id="251f1-320">**DPLMVersionInformation**</span></span> |<span data-ttu-id="251f1-321">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="251f1-321">**xs:string**</span></span> |<span data-ttu-id="251f1-322">Versión del kit de desarrollo de medición de sonoridad profesional **Dolby**.</span><span class="sxs-lookup"><span data-stu-id="251f1-322">**Dolby** professional loudness metering development kit version.</span></span> |
| <span data-ttu-id="251f1-323">**DialogNormalization**</span><span class="sxs-lookup"><span data-stu-id="251f1-323">**DialogNormalization**</span></span><br/><br/> <span data-ttu-id="251f1-324">minInclusive="-31" maxInclusive="-1"</span><span class="sxs-lookup"><span data-stu-id="251f1-324">minInclusive="-31" maxInclusive="-1"</span></span><br/><br/> <span data-ttu-id="251f1-325">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-325">Required</span></span> |<span data-ttu-id="251f1-326">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="251f1-326">**xs:int**</span></span> |<span data-ttu-id="251f1-327">DialogNormalization generado mediante DPLM, requerido si LoudnessMetering está establecido.</span><span class="sxs-lookup"><span data-stu-id="251f1-327">DialogNormalization generated through DPLM, required when LoudnessMetering is set</span></span> |
| <span data-ttu-id="251f1-328">**IntegratedLoudness**</span><span class="sxs-lookup"><span data-stu-id="251f1-328">**IntegratedLoudness**</span></span><br/><br/> <span data-ttu-id="251f1-329">minInclusive="-70" maxInclusive="10"</span><span class="sxs-lookup"><span data-stu-id="251f1-329">minInclusive="-70" maxInclusive="10"</span></span><br/><br/> <span data-ttu-id="251f1-330">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-330">Required</span></span> |<span data-ttu-id="251f1-331">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="251f1-331">**xs:float**</span></span> |<span data-ttu-id="251f1-332">Sonoridad integrada.</span><span class="sxs-lookup"><span data-stu-id="251f1-332">Integrated loudness</span></span> |
| <span data-ttu-id="251f1-333">**IntegratedLoudnessUnit**</span><span class="sxs-lookup"><span data-stu-id="251f1-333">**IntegratedLoudnessUnit**</span></span><br/><br/> <span data-ttu-id="251f1-334">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-334">Required</span></span> |<span data-ttu-id="251f1-335">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="251f1-335">**xs:string**</span></span> |<span data-ttu-id="251f1-336">Unidad de sonoridad integrada.</span><span class="sxs-lookup"><span data-stu-id="251f1-336">Integrated loudness unit.</span></span> |
| <span data-ttu-id="251f1-337">**IntegratedLoudnessGatingMethod**</span><span class="sxs-lookup"><span data-stu-id="251f1-337">**IntegratedLoudnessGatingMethod**</span></span><br/><br/> <span data-ttu-id="251f1-338">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-338">Required</span></span> |<span data-ttu-id="251f1-339">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="251f1-339">**xs:string**</span></span> |<span data-ttu-id="251f1-340">Identificador de acceso.</span><span class="sxs-lookup"><span data-stu-id="251f1-340">Gating identifier</span></span> |
| <span data-ttu-id="251f1-341">**IntegratedLoudnessSpeechPercentage**</span><span class="sxs-lookup"><span data-stu-id="251f1-341">**IntegratedLoudnessSpeechPercentage**</span></span><br/><br/> <span data-ttu-id="251f1-342">minInclusive ="0" maxInclusive="100"</span><span class="sxs-lookup"><span data-stu-id="251f1-342">minInclusive ="0" maxInclusive="100"</span></span> |<span data-ttu-id="251f1-343">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="251f1-343">**xs:float**</span></span> |<span data-ttu-id="251f1-344">Contenido de voz a través del programa Hola, como un porcentaje.</span><span class="sxs-lookup"><span data-stu-id="251f1-344">Speech content over hello program, as a percentage.</span></span> |
| <span data-ttu-id="251f1-345">**SamplePeak**</span><span class="sxs-lookup"><span data-stu-id="251f1-345">**SamplePeak**</span></span><br/><br/> <span data-ttu-id="251f1-346">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-346">Required</span></span> |<span data-ttu-id="251f1-347">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="251f1-347">**xs:float**</span></span> |<span data-ttu-id="251f1-348">Valor pico de ejemplo absoluto, desde el restablecimiento o desde la última vez que se desactivó, por canal.</span><span class="sxs-lookup"><span data-stu-id="251f1-348">Peak absolute sample value, since reset or since it was last cleared, per channel.</span></span>  <span data-ttu-id="251f1-349">Las unidades son dBFS.</span><span class="sxs-lookup"><span data-stu-id="251f1-349">Units are dBFS.</span></span> |
| <span data-ttu-id="251f1-350">**SamplePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="251f1-350">**SamplePeakUnit**</span></span><br/><br/> <span data-ttu-id="251f1-351">fixed="dBFS"</span><span class="sxs-lookup"><span data-stu-id="251f1-351">fixed="dBFS"</span></span><br/><br/> <span data-ttu-id="251f1-352">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-352">Required</span></span> |<span data-ttu-id="251f1-353">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="251f1-353">**xs:anySimpleType**</span></span> |<span data-ttu-id="251f1-354">Unidad pico de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="251f1-354">Sample peak unit.</span></span> |
| <span data-ttu-id="251f1-355">**TruePeak**</span><span class="sxs-lookup"><span data-stu-id="251f1-355">**TruePeak**</span></span><br/><br/> <span data-ttu-id="251f1-356">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-356">Required</span></span> |<span data-ttu-id="251f1-357">**xs:float**</span><span class="sxs-lookup"><span data-stu-id="251f1-357">**xs:float**</span></span> |<span data-ttu-id="251f1-358">Valor pico verdadero máximo, según ITU-R BS.1770-2, desde el restablecimiento o desde la última vez que se desactivó, por canal.</span><span class="sxs-lookup"><span data-stu-id="251f1-358">Maximum true peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.</span></span> <span data-ttu-id="251f1-359">Las unidades son dBTP.</span><span class="sxs-lookup"><span data-stu-id="251f1-359">Units are dBTP.</span></span> |
| <span data-ttu-id="251f1-360">**TruePeakUnit**</span><span class="sxs-lookup"><span data-stu-id="251f1-360">**TruePeakUnit**</span></span><br/><br/> <span data-ttu-id="251f1-361">fixed="dBTP"</span><span class="sxs-lookup"><span data-stu-id="251f1-361">fixed="dBTP"</span></span><br/><br/> <span data-ttu-id="251f1-362">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="251f1-362">Required</span></span> |<span data-ttu-id="251f1-363">**xs:anySimpleType**</span><span class="sxs-lookup"><span data-stu-id="251f1-363">**xs:anySimpleType**</span></span> |<span data-ttu-id="251f1-364">Unidad pico verdadera.</span><span class="sxs-lookup"><span data-stu-id="251f1-364">True peak unit.</span></span> |

## <a name="schema-code"></a><span data-ttu-id="251f1-365">Código del esquema</span><span class="sxs-lookup"><span data-stu-id="251f1-365">Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
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
                      <xs:documentation>Collection of input/source media files, that was processed in order tooproduce this AssetFile</xs:documentation>  
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
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
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
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via hello encoding preset, in kilobits per second</xs:documentation>  
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
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
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
                                      <xs:documentation>Speech content over hello program, as a percentage.</xs:documentation>  
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
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
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
                                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
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
                    <xs:documentation>hello media asset file name</xs:documentation>  
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



## <span data-ttu-id="251f1-366"><a name="xml"></a> Ejemplo de XML</span><span class="sxs-lookup"><span data-stu-id="251f1-366"><a name="xml"></a> XML example</span></span>
 <span data-ttu-id="251f1-367">Hola aquí te mostramos un ejemplo Hola metadatos del archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="251f1-367">hello following is an example of hello Output metadata file.</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="251f1-368">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="251f1-368">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="251f1-369">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="251f1-369">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
