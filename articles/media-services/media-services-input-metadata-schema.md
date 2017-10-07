---
title: esquema de entrada de metadatos de servicios multimedia de aaaAzure | Documentos de Microsoft
description: "tema de Hello ofrezca una visión general del esquema de metadatos de entrada de servicios multimedia de Azure."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a><span data-ttu-id="05101-103">Metadatos de entrada</span><span class="sxs-lookup"><span data-stu-id="05101-103">Input Metadata</span></span>
<span data-ttu-id="05101-104">Un trabajo de codificación está asociado a un recurso de entrada (o activos) en el que desea tooperform algunas tareas de codificación.</span><span class="sxs-lookup"><span data-stu-id="05101-104">An encoding job is associated with an input asset (or assets) on which you want tooperform some encoding tasks.</span></span>  <span data-ttu-id="05101-105">Tras la finalización de una tarea, se produce un recurso de salida.</span><span class="sxs-lookup"><span data-stu-id="05101-105">Upon completion of a task, an output asset is produced.</span></span>  <span data-ttu-id="05101-106">Hola activo de salida contiene vídeo, audio, miniaturas, etc. activo de salida de hello también contiene un archivo con metadatos sobre el recurso de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-106">hello output asset contains video, audio, thumbnails, manifest, etc. hello output asset also contains a file with metadata about hello input asset.</span></span> <span data-ttu-id="05101-107">nombre del archivo XML de metadatos de hello Hello tiene Hola siguiendo el formato: &lt;id_recurso&gt;_metadata.xml (por ejemplo, 41114ad3-eb5e - 4c 57-8d 92-5354e2b7d4a4_metadata.xml), donde &lt;id_recurso&gt; es hello AssetId valor del recurso de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-107">hello name of hello metadata XML file has hello following format: &lt;asset_id&gt;_metadata.xml (for example, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), where &lt;asset_id&gt; is hello AssetId value of hello input asset.</span></span>  

<span data-ttu-id="05101-108">Si desea que el archivo de metadatos de hello tooexamine, puede crear un **SAS** localizador y descarga Hola ordenador tooyour de archivo.</span><span class="sxs-lookup"><span data-stu-id="05101-108">If you want tooexamine hello metadata file, you can create a **SAS** locator and download hello file tooyour local computer.</span></span> <span data-ttu-id="05101-109">Puede encontrar un ejemplo sobre cómo toocreate un localizador SAS y descargar un archivo [con hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="05101-109">You can find an example on how toocreate a SAS locator and download a file  [Using hello Media Services .NET SDK Extensions](media-services-dotnet-get-started.md).</span></span>  

<span data-ttu-id="05101-110">Este tema describen los elementos de Hola y tipos de esquema XML de Hola en los metadatos de entrada de hello (&lt;id_recurso&gt;_metadata.xml) se basa.</span><span class="sxs-lookup"><span data-stu-id="05101-110">This topic discusses hello elements and types of hello XML schema on which hello input metada (&lt;asset_id&gt;_metadata.xml) is based.</span></span>  <span data-ttu-id="05101-111">Para obtener información sobre el archivo hello que contiene metadatos sobre el recurso de salida de hello, consulte [metadatos de salida](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="05101-111">For information about hello file that contains metadata about hello output asset, see [Output Metadata](media-services-output-metadata-schema.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="05101-112">Puede encontrar Hola [código del esquema](media-services-input-metadata-schema.md#code) una [ejemplo XML](media-services-input-metadata-schema.md#xml) final Hola de este tema.</span><span class="sxs-lookup"><span data-stu-id="05101-112">You can find hello [Schema Code](media-services-input-metadata-schema.md#code) an [XML example](media-services-input-metadata-schema.md#xml) at hello end of this topic.</span></span>  
> 
> 

## <span data-ttu-id="05101-113"><a name="AssetFiles"></a> Elemento AssetFiles (elemento raíz)</span><span class="sxs-lookup"><span data-stu-id="05101-113"><a name="AssetFiles"></a> AssetFiles element (root element)</span></span>
<span data-ttu-id="05101-114">Contiene una colección de [elemento AssetFile](media-services-input-metadata-schema.md#AssetFile)s para el trabajo de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-114">Contains a collection of [AssetFile element](media-services-input-metadata-schema.md#AssetFile)s for hello encoding job.</span></span>  

<span data-ttu-id="05101-115">Ver un ejemplo XML al final de Hola de este tema: [ejemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="05101-115">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

| <span data-ttu-id="05101-116">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-116">Name</span></span> | <span data-ttu-id="05101-117">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05101-118">**AssetFile**</span><span class="sxs-lookup"><span data-stu-id="05101-118">**AssetFile**</span></span><br /><br /> <span data-ttu-id="05101-119">minOccurs="1" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="05101-119">minOccurs="1" maxOccurs="unbounded"</span></span> |<span data-ttu-id="05101-120">Un único elemento secundario.</span><span class="sxs-lookup"><span data-stu-id="05101-120">A single child element.</span></span> <span data-ttu-id="05101-121">Para más información, consulte [Elemento AssetFile](media-services-input-metadata-schema.md#AssetFile).</span><span class="sxs-lookup"><span data-stu-id="05101-121">For more information, see [AssetFile element](media-services-input-metadata-schema.md#AssetFile).</span></span> |

## <span data-ttu-id="05101-122"><a name="AssetFile"></a> Elemento AssetFile</span><span class="sxs-lookup"><span data-stu-id="05101-122"><a name="AssetFile"></a> AssetFile element</span></span>
 <span data-ttu-id="05101-123">Contiene atributos y elementos que describen un archivo de recursos.</span><span class="sxs-lookup"><span data-stu-id="05101-123">Contains attributes and elements that describe an asset file.</span></span>  

 <span data-ttu-id="05101-124">Ver un ejemplo XML al final de Hola de este tema: [ejemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="05101-124">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="05101-125">Attributes</span><span class="sxs-lookup"><span data-stu-id="05101-125">Attributes</span></span>
| <span data-ttu-id="05101-126">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-126">Name</span></span> | <span data-ttu-id="05101-127">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-127">Type</span></span> | <span data-ttu-id="05101-128">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-128">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-129">**Name**</span><span class="sxs-lookup"><span data-stu-id="05101-129">**Name**</span></span><br /><br /> <span data-ttu-id="05101-130">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-130">Required</span></span> |<span data-ttu-id="05101-131">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-131">**xs:string**</span></span> |<span data-ttu-id="05101-132">Nombre del archivo de recursos.</span><span class="sxs-lookup"><span data-stu-id="05101-132">Asset file name.</span></span> |
| <span data-ttu-id="05101-133">**Tamaño**</span><span class="sxs-lookup"><span data-stu-id="05101-133">**Size**</span></span><br /><br /> <span data-ttu-id="05101-134">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-134">Required</span></span> |<span data-ttu-id="05101-135">**xs:long**</span><span class="sxs-lookup"><span data-stu-id="05101-135">**xs:long**</span></span> |<span data-ttu-id="05101-136">Tamaño de archivo de recursos de hello en bytes.</span><span class="sxs-lookup"><span data-stu-id="05101-136">Size of hello asset file in bytes.</span></span> |
| <span data-ttu-id="05101-137">**Duration**</span><span class="sxs-lookup"><span data-stu-id="05101-137">**Duration**</span></span><br /><br /> <span data-ttu-id="05101-138">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-138">Required</span></span> |<span data-ttu-id="05101-139">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="05101-139">**xs:duration**</span></span> |<span data-ttu-id="05101-140">Duración de la reproducción del contenido.</span><span class="sxs-lookup"><span data-stu-id="05101-140">Content play back duration.</span></span> <span data-ttu-id="05101-141">Ejemplo: Duration="PT25M37.757S".</span><span class="sxs-lookup"><span data-stu-id="05101-141">Example: Duration="PT25M37.757S".</span></span> |
| <span data-ttu-id="05101-142">**NumberOfStreams**</span><span class="sxs-lookup"><span data-stu-id="05101-142">**NumberOfStreams**</span></span><br /><br /> <span data-ttu-id="05101-143">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-143">Required</span></span> |<span data-ttu-id="05101-144">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-144">**xs:int**</span></span> |<span data-ttu-id="05101-145">Número de secuencias en el archivo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-145">Number of streams in hello asset file.</span></span> |
| <span data-ttu-id="05101-146">**FormatNames**</span><span class="sxs-lookup"><span data-stu-id="05101-146">**FormatNames**</span></span><br /><br /> <span data-ttu-id="05101-147">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-147">Required</span></span> |<span data-ttu-id="05101-148">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-148">**xs:string**</span></span> |<span data-ttu-id="05101-149">Nombres de formatos.</span><span class="sxs-lookup"><span data-stu-id="05101-149">Format names.</span></span> |
| <span data-ttu-id="05101-150">**FormatVerboseNames**</span><span class="sxs-lookup"><span data-stu-id="05101-150">**FormatVerboseNames**</span></span><br /><br /> <span data-ttu-id="05101-151">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-151">Required</span></span> |<span data-ttu-id="05101-152">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-152">**xs:string**</span></span> |<span data-ttu-id="05101-153">Nombres detallados de formatos.</span><span class="sxs-lookup"><span data-stu-id="05101-153">Format verbose names.</span></span> |
| <span data-ttu-id="05101-154">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="05101-154">**StartTime**</span></span> |<span data-ttu-id="05101-155">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="05101-155">**xs:duration**</span></span> |<span data-ttu-id="05101-156">Hora de inicio del contenido.</span><span class="sxs-lookup"><span data-stu-id="05101-156">Content start time.</span></span> <span data-ttu-id="05101-157">Ejemplo: StartTime="PT2.669S".</span><span class="sxs-lookup"><span data-stu-id="05101-157">Example: StartTime="PT2.669S".</span></span> |
| <span data-ttu-id="05101-158">**OverallBitRate**</span><span class="sxs-lookup"><span data-stu-id="05101-158">**OverallBitRate**</span></span> |<span data-ttu-id="05101-159">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-159">**xs:int**</span></span> |<span data-ttu-id="05101-160">Velocidad de bits Media del archivo de recursos de hello en kbps.</span><span class="sxs-lookup"><span data-stu-id="05101-160">Average bitrate of hello asset file in kbps.</span></span> |

> [!NOTE]
> <span data-ttu-id="05101-161">Hola siguientes 4 elementos secundarios debe aparecer en una secuencia.</span><span class="sxs-lookup"><span data-stu-id="05101-161">hello following 4 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="05101-162">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="05101-162">Child elements</span></span>
| <span data-ttu-id="05101-163">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-163">Name</span></span> | <span data-ttu-id="05101-164">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-164">Type</span></span> | <span data-ttu-id="05101-165">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-166">**Programs**</span><span class="sxs-lookup"><span data-stu-id="05101-166">**Programs**</span></span><br /><br /> <span data-ttu-id="05101-167">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="05101-167">minOccurs="0"</span></span> | |<span data-ttu-id="05101-168">Colección de todos los [elemento Programs](media-services-input-metadata-schema.md#Programs) cuando es el archivo de recursos de hello en formato MPEG-TS.</span><span class="sxs-lookup"><span data-stu-id="05101-168">Collection of all [Programs element](media-services-input-metadata-schema.md#Programs) when hello asset file is in MPEG-TS format.</span></span> |
| <span data-ttu-id="05101-169">**VideoTracks**</span><span class="sxs-lookup"><span data-stu-id="05101-169">**VideoTracks**</span></span><br /><br /> <span data-ttu-id="05101-170">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="05101-170">minOccurs="0"</span></span> | |<span data-ttu-id="05101-171">Cada archivo de recursos físico puede contener cero o más pistas de vídeo intercaladas en un formato de contenedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="05101-171">Each physical asset file can contain zero or more video tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="05101-172">Este elemento contiene una colección de todos los [elemento VideoTracks](media-services-input-metadata-schema.md#VideoTracks) que forman parte del archivo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-172">This element contains a collection of all [VideoTracks element](media-services-input-metadata-schema.md#VideoTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="05101-173">**AudioTracks**</span><span class="sxs-lookup"><span data-stu-id="05101-173">**AudioTracks**</span></span><br /><br /> <span data-ttu-id="05101-174">minOccurs="0"</span><span class="sxs-lookup"><span data-stu-id="05101-174">minOccurs="0"</span></span> | |<span data-ttu-id="05101-175">Cada archivo de recursos físico puede contener cero o más pistas de audio intercaladas en un formato de contenedor adecuado.</span><span class="sxs-lookup"><span data-stu-id="05101-175">Each physical asset file can contain zero or more audio tracks interleaved into an appropriate container format.</span></span> <span data-ttu-id="05101-176">Este elemento contiene una colección de todos los [elemento AudioTracks](media-services-input-metadata-schema.md#AudioTracks) que forman parte del archivo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-176">This element contains a collection of all [AudioTracks element](media-services-input-metadata-schema.md#AudioTracks) that are part of hello asset file.</span></span> |
| <span data-ttu-id="05101-177">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="05101-177">**Metadata**</span></span><br /><br /> <span data-ttu-id="05101-178">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="05101-178">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="05101-179">MetadataType</span><span class="sxs-lookup"><span data-stu-id="05101-179">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="05101-180">Metadatos del archivo de recursos representados como cadenas de clave-valor.</span><span class="sxs-lookup"><span data-stu-id="05101-180">Asset file’s metadata represented as key\value strings.</span></span> <span data-ttu-id="05101-181">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="05101-181">For example:</span></span><br /><br /> <span data-ttu-id="05101-182">**&lt;Metadata key="language" value="eng" /&gt;**</span><span class="sxs-lookup"><span data-stu-id="05101-182">**&lt;Metadata key="language" value="eng" /&gt;**</span></span> |

## <span data-ttu-id="05101-183"><a name="TrackType"></a> TrackType</span><span class="sxs-lookup"><span data-stu-id="05101-183"><a name="TrackType"></a> TrackType</span></span>
<span data-ttu-id="05101-184">Ver un ejemplo XML al final de Hola de este tema: [ejemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="05101-184">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="05101-185">Attributes</span><span class="sxs-lookup"><span data-stu-id="05101-185">Attributes</span></span>
| <span data-ttu-id="05101-186">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-186">Name</span></span> | <span data-ttu-id="05101-187">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-187">Type</span></span> | <span data-ttu-id="05101-188">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-188">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-189">**Id**</span><span class="sxs-lookup"><span data-stu-id="05101-189">**Id**</span></span><br /><br /> <span data-ttu-id="05101-190">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-190">Required</span></span> |<span data-ttu-id="05101-191">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-191">**xs:int**</span></span> |<span data-ttu-id="05101-192">Índice de base cero de esta pista de audio o vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-192">Zero-based index of this audio or video track.</span></span><br /><br /> <span data-ttu-id="05101-193">Esto no es necesariamente ese hello trackid tal y como se utiliza en un archivo MP4.</span><span class="sxs-lookup"><span data-stu-id="05101-193">This is not necessarily that hello TrackID as used in an MP4 file.</span></span> |
| <span data-ttu-id="05101-194">**Codec**</span><span class="sxs-lookup"><span data-stu-id="05101-194">**Codec**</span></span> |<span data-ttu-id="05101-195">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-195">**xs:string**</span></span> |<span data-ttu-id="05101-196">Cadena de códec de pista de vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-196">Video track codec string.</span></span> |
| <span data-ttu-id="05101-197">**CodecLongName**</span><span class="sxs-lookup"><span data-stu-id="05101-197">**CodecLongName**</span></span> |<span data-ttu-id="05101-198">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-198">**xs:string**</span></span> |<span data-ttu-id="05101-199">Nombre largo del códec de pista de vídeo o audio.</span><span class="sxs-lookup"><span data-stu-id="05101-199">Audio or video track codec long name.</span></span> |
| <span data-ttu-id="05101-200">**TimeBase**</span><span class="sxs-lookup"><span data-stu-id="05101-200">**TimeBase**</span></span><br /><br /> <span data-ttu-id="05101-201">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-201">Required</span></span> |<span data-ttu-id="05101-202">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-202">**xs:string**</span></span> |<span data-ttu-id="05101-203">Base de tiempo.</span><span class="sxs-lookup"><span data-stu-id="05101-203">Time base.</span></span> <span data-ttu-id="05101-204">Ejemplo: TimeBase="1/48000"</span><span class="sxs-lookup"><span data-stu-id="05101-204">Example: TimeBase="1/48000"</span></span> |
| <span data-ttu-id="05101-205">**NumberOfFrames**</span><span class="sxs-lookup"><span data-stu-id="05101-205">**NumberOfFrames**</span></span> |<span data-ttu-id="05101-206">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-206">**xs:int**</span></span> |<span data-ttu-id="05101-207">Número de fotogramas (presente para pistas de vídeo).</span><span class="sxs-lookup"><span data-stu-id="05101-207">Number of frames (present for video tracks).</span></span> |
| <span data-ttu-id="05101-208">**StartTime**</span><span class="sxs-lookup"><span data-stu-id="05101-208">**StartTime**</span></span> |<span data-ttu-id="05101-209">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="05101-209">**xs:duration**</span></span> |<span data-ttu-id="05101-210">Hora de inicio de la pista.</span><span class="sxs-lookup"><span data-stu-id="05101-210">Track start time.</span></span> <span data-ttu-id="05101-211">Ejemplo: StartTime="PT2.669S"</span><span class="sxs-lookup"><span data-stu-id="05101-211">Example: StartTime="PT2.669S"</span></span> |
| <span data-ttu-id="05101-212">**Duration**</span><span class="sxs-lookup"><span data-stu-id="05101-212">**Duration**</span></span> |<span data-ttu-id="05101-213">**xs:duration**</span><span class="sxs-lookup"><span data-stu-id="05101-213">**xs:duration**</span></span> |<span data-ttu-id="05101-214">Duración de la pista.</span><span class="sxs-lookup"><span data-stu-id="05101-214">Track duration.</span></span> <span data-ttu-id="05101-215">Ejemplo: Duration="PTSampleFormat M37.757S".</span><span class="sxs-lookup"><span data-stu-id="05101-215">Example: Duration="PTSampleFormat M37.757S".</span></span> |

> [!NOTE]
> <span data-ttu-id="05101-216">Hola siguientes 2 elementos secundarios debe aparecer en una secuencia.</span><span class="sxs-lookup"><span data-stu-id="05101-216">hello following 2 child elements must appear in a sequence.</span></span>  
> 
> 

### <a name="child-elements"></a><span data-ttu-id="05101-217">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="05101-217">Child elements</span></span>
| <span data-ttu-id="05101-218">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-218">Name</span></span> | <span data-ttu-id="05101-219">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-219">Type</span></span> | <span data-ttu-id="05101-220">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-220">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-221">**Disposition**</span><span class="sxs-lookup"><span data-stu-id="05101-221">**Disposition**</span></span><br /><br /> <span data-ttu-id="05101-222">minOccurs="0" maxOccurs="1"</span><span class="sxs-lookup"><span data-stu-id="05101-222">minOccurs="0" maxOccurs="1"</span></span> |[<span data-ttu-id="05101-223">StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="05101-223">StreamDispositionType</span></span>](media-services-input-metadata-schema.md#StreamDispositionType) |<span data-ttu-id="05101-224">Contiene información de presentación (por ejemplo, si una determinada pista de audio es para espectadores con discapacidad visual).</span><span class="sxs-lookup"><span data-stu-id="05101-224">Contains presentation information (for example, whether a particular audio track is for visually impaired viewers).</span></span> |
| <span data-ttu-id="05101-225">**Metadata**</span><span class="sxs-lookup"><span data-stu-id="05101-225">**Metadata**</span></span><br /><br /> <span data-ttu-id="05101-226">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="05101-226">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="05101-227">MetadataType</span><span class="sxs-lookup"><span data-stu-id="05101-227">MetadataType</span></span>](media-services-input-metadata-schema.md#MetadataType) |<span data-ttu-id="05101-228">Cadenas de clave/valor genérico que pueden ser utilizado toohold una variedad de información.</span><span class="sxs-lookup"><span data-stu-id="05101-228">Generic key/value strings that can be used toohold a variety of information.</span></span> <span data-ttu-id="05101-229">Por ejemplo, key=”language” y value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="05101-229">For example, key=”language”, and value=”eng”.</span></span> |

## <span data-ttu-id="05101-230"><a name="AudioTrackType"></a> AudioTrackType (hereda de TrackType)</span><span class="sxs-lookup"><span data-stu-id="05101-230"><a name="AudioTrackType"></a> AudioTrackType (inherits from TrackType)</span></span>
 <span data-ttu-id="05101-231">**AudioTrackType** es un tipo complejo global que hereda de [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="05101-231">**AudioTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

 <span data-ttu-id="05101-232">tipo de Hello representa una determinada pista de audio en archivo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-232">hello type represents a specific audio track in hello asset file.</span></span>  

 <span data-ttu-id="05101-233">Ver un ejemplo XML al final de Hola de este tema: [ejemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="05101-233">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="05101-234">Attributes</span><span class="sxs-lookup"><span data-stu-id="05101-234">Attributes</span></span>
| <span data-ttu-id="05101-235">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-235">Name</span></span> | <span data-ttu-id="05101-236">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-236">Type</span></span> | <span data-ttu-id="05101-237">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-238">**SampleFormat**</span><span class="sxs-lookup"><span data-stu-id="05101-238">**SampleFormat**</span></span> |<span data-ttu-id="05101-239">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-239">**xs:string**</span></span> |<span data-ttu-id="05101-240">Formato de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="05101-240">Sample format.</span></span> |
| <span data-ttu-id="05101-241">**ChannelLayout**</span><span class="sxs-lookup"><span data-stu-id="05101-241">**ChannelLayout**</span></span> |<span data-ttu-id="05101-242">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-242">**xs:string**</span></span> |<span data-ttu-id="05101-243">Distribución de canales.</span><span class="sxs-lookup"><span data-stu-id="05101-243">Channel layout.</span></span> |
| <span data-ttu-id="05101-244">**Channels**</span><span class="sxs-lookup"><span data-stu-id="05101-244">**Channels**</span></span><br /><br /> <span data-ttu-id="05101-245">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-245">Required</span></span> |<span data-ttu-id="05101-246">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-246">**xs:int**</span></span> |<span data-ttu-id="05101-247">Número de canales de audio (0 o más).</span><span class="sxs-lookup"><span data-stu-id="05101-247">Number (0 or more) of audio channels.</span></span> |
| <span data-ttu-id="05101-248">**SamplingRate**</span><span class="sxs-lookup"><span data-stu-id="05101-248">**SamplingRate**</span></span><br /><br /> <span data-ttu-id="05101-249">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-249">Required</span></span> |<span data-ttu-id="05101-250">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-250">**xs:int**</span></span> |<span data-ttu-id="05101-251">Velocidad de muestreo de audio en muestras/s o Hz.</span><span class="sxs-lookup"><span data-stu-id="05101-251">Audio sampling rate in samples/sec or Hz.</span></span> |
| <span data-ttu-id="05101-252">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="05101-252">**Bitrate**</span></span> |<span data-ttu-id="05101-253">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-253">**xs:int**</span></span> |<span data-ttu-id="05101-254">Velocidad de bits de audio Media en bits por segundo, según los cálculos de archivo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-254">Average audio bit rate in bits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="05101-255">Carga de secuencias básicas de hello solo se contabiliza y sobrecarga de empaquetado de hello no se incluye en este recuento.</span><span class="sxs-lookup"><span data-stu-id="05101-255">Only hello elementary stream payload is counted, and hello packaging overhead is not included in this count.</span></span> |
| <span data-ttu-id="05101-256">**BitsPerSample**</span><span class="sxs-lookup"><span data-stu-id="05101-256">**BitsPerSample**</span></span> |<span data-ttu-id="05101-257">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-257">**xs:int**</span></span> |<span data-ttu-id="05101-258">Tipo de bits por muestra para el formato wFormatTag Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-258">Bits per sample for hello wFormatTag format type.</span></span> |

## <span data-ttu-id="05101-259"><a name="VideoTrackType"></a> VideoTrackType (hereda de TrackType)</span><span class="sxs-lookup"><span data-stu-id="05101-259"><a name="VideoTrackType"></a> VideoTrackType (inherits from TrackType)</span></span>
<span data-ttu-id="05101-260">**VideoTrackType** es un tipo complejo global que hereda de [TrackType](media-services-input-metadata-schema.md#TrackType).</span><span class="sxs-lookup"><span data-stu-id="05101-260">**VideoTrackType** is a global complex type that inherits from [TrackType](media-services-input-metadata-schema.md#TrackType).</span></span>  

<span data-ttu-id="05101-261">tipo de Hello representa una determinada pista de vídeo en el archivo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-261">hello type represents a specific video track in hello asset file.</span></span>  

<span data-ttu-id="05101-262">Ver un ejemplo XML al final de Hola de este tema: [ejemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="05101-262">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="05101-263">Attributes</span><span class="sxs-lookup"><span data-stu-id="05101-263">Attributes</span></span>
| <span data-ttu-id="05101-264">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-264">Name</span></span> | <span data-ttu-id="05101-265">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-265">Type</span></span> | <span data-ttu-id="05101-266">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-267">**FourCC**</span><span class="sxs-lookup"><span data-stu-id="05101-267">**FourCC**</span></span><br /><br /> <span data-ttu-id="05101-268">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-268">Required</span></span> |<span data-ttu-id="05101-269">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-269">**xs:string**</span></span> |<span data-ttu-id="05101-270">Código FourCC de códec de vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-270">Video codec FourCC code.</span></span> |
| <span data-ttu-id="05101-271">**Perfil**</span><span class="sxs-lookup"><span data-stu-id="05101-271">**Profile**</span></span> |<span data-ttu-id="05101-272">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-272">**xs:string**</span></span> |<span data-ttu-id="05101-273">Perfil de la pista de vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-273">Video track's profile.</span></span> |
| <span data-ttu-id="05101-274">**Level**</span><span class="sxs-lookup"><span data-stu-id="05101-274">**Level**</span></span> |<span data-ttu-id="05101-275">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-275">**xs:string**</span></span> |<span data-ttu-id="05101-276">Nivel de la pista de vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-276">Video track's level.</span></span> |
| <span data-ttu-id="05101-277">**PixelFormat**</span><span class="sxs-lookup"><span data-stu-id="05101-277">**PixelFormat**</span></span> |<span data-ttu-id="05101-278">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-278">**xs:string**</span></span> |<span data-ttu-id="05101-279">Formato de píxel de la pista de vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-279">Video track's pixel format.</span></span> |
| <span data-ttu-id="05101-280">**Width**</span><span class="sxs-lookup"><span data-stu-id="05101-280">**Width**</span></span><br /><br /> <span data-ttu-id="05101-281">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-281">Required</span></span> |<span data-ttu-id="05101-282">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-282">**xs:int**</span></span> |<span data-ttu-id="05101-283">Ancho del vídeo codificado en píxeles.</span><span class="sxs-lookup"><span data-stu-id="05101-283">Encoded video width in pixels.</span></span> |
| <span data-ttu-id="05101-284">**Height**</span><span class="sxs-lookup"><span data-stu-id="05101-284">**Height**</span></span><br /><br /> <span data-ttu-id="05101-285">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-285">Required</span></span> |<span data-ttu-id="05101-286">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-286">**xs:int**</span></span> |<span data-ttu-id="05101-287">Alto del vídeo codificado en píxeles.</span><span class="sxs-lookup"><span data-stu-id="05101-287">Encoded video height in pixels.</span></span> |
| <span data-ttu-id="05101-288">**DisplayAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="05101-288">**DisplayAspectRatioNumerator**</span></span><br /><br /> <span data-ttu-id="05101-289">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-289">Required</span></span> |<span data-ttu-id="05101-290">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="05101-290">**xs:double**</span></span> |<span data-ttu-id="05101-291">Numerador de la relación de aspecto de pantalla de vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-291">Video display aspect ratio numerator.</span></span> |
| <span data-ttu-id="05101-292">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="05101-292">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="05101-293">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-293">Required</span></span> |<span data-ttu-id="05101-294">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="05101-294">**xs:double**</span></span> |<span data-ttu-id="05101-295">Denominador de la relación de aspecto de pantalla de vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-295">Video display aspect ratio denominator.</span></span> |
| <span data-ttu-id="05101-296">**DisplayAspectRatioDenominator**</span><span class="sxs-lookup"><span data-stu-id="05101-296">**DisplayAspectRatioDenominator**</span></span><br /><br /> <span data-ttu-id="05101-297">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-297">Required</span></span> |<span data-ttu-id="05101-298">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="05101-298">**xs:double**</span></span> |<span data-ttu-id="05101-299">Numerador de la relación de aspecto de muestra de vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-299">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="05101-300">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="05101-300">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="05101-301">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="05101-301">**xs:double**</span></span> |<span data-ttu-id="05101-302">Numerador de la relación de aspecto de muestra de vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-302">Video sample aspect ratio numerator.</span></span> |
| <span data-ttu-id="05101-303">**SampleAspectRatioNumerator**</span><span class="sxs-lookup"><span data-stu-id="05101-303">**SampleAspectRatioNumerator**</span></span> |<span data-ttu-id="05101-304">**xs:double**</span><span class="sxs-lookup"><span data-stu-id="05101-304">**xs:double**</span></span> |<span data-ttu-id="05101-305">Denominador de la relación de aspecto de muestra de vídeo.</span><span class="sxs-lookup"><span data-stu-id="05101-305">Video sample aspect ratio denominator.</span></span> |
| <span data-ttu-id="05101-306">**FrameRate**</span><span class="sxs-lookup"><span data-stu-id="05101-306">**FrameRate**</span></span><br /><br /> <span data-ttu-id="05101-307">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-307">Required</span></span> |<span data-ttu-id="05101-308">**xs:decimal**</span><span class="sxs-lookup"><span data-stu-id="05101-308">**xs:decimal**</span></span> |<span data-ttu-id="05101-309">Velocidad de fotogramas de vídeo medida en formato .3f.</span><span class="sxs-lookup"><span data-stu-id="05101-309">Measured video frame rate in .3f format.</span></span> |
| <span data-ttu-id="05101-310">**Bitrate**</span><span class="sxs-lookup"><span data-stu-id="05101-310">**Bitrate**</span></span> |<span data-ttu-id="05101-311">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-311">**xs:int**</span></span> |<span data-ttu-id="05101-312">Velocidad de bits de vídeo Media en kilobits por segundo, según los cálculos de archivo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-312">Average video bit rate in kilobits per second, as calculated from hello asset file.</span></span> <span data-ttu-id="05101-313">Se contabiliza solo carga de secuencias básicas de hello y no se incluye la sobrecarga de empaquetado de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-313">Only hello elementary stream payload is counted, and hello packaging overhead is not included.</span></span> |
| <span data-ttu-id="05101-314">**MaxGOPBitrate**</span><span class="sxs-lookup"><span data-stu-id="05101-314">**MaxGOPBitrate**</span></span> |<span data-ttu-id="05101-315">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-315">**xs:int**</span></span> |<span data-ttu-id="05101-316">Velocidad de bits media máxima para GOP, en kilobits por segundo.</span><span class="sxs-lookup"><span data-stu-id="05101-316">Max GOP average bitrate for this video track, in kilobits per second.</span></span> |
| <span data-ttu-id="05101-317">**HasBFrames**</span><span class="sxs-lookup"><span data-stu-id="05101-317">**HasBFrames**</span></span> |<span data-ttu-id="05101-318">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-318">**xs:int**</span></span> |<span data-ttu-id="05101-319">Número de pista de vídeo de fotogramas B.</span><span class="sxs-lookup"><span data-stu-id="05101-319">Video track number of B frames.</span></span> |

## <span data-ttu-id="05101-320"><a name="MetadataType"></a> MetadataType</span><span class="sxs-lookup"><span data-stu-id="05101-320"><a name="MetadataType"></a> MetadataType</span></span>
<span data-ttu-id="05101-321">**MetadataType** es un tipo complejo global que describe los metadatos de un archivo de recursos como cadenas de clave-valor.</span><span class="sxs-lookup"><span data-stu-id="05101-321">**MetadataType** is a global complex type that describes metadata of an asset file as key/value strings.</span></span> <span data-ttu-id="05101-322">Por ejemplo, key=”language” y value=”eng”.</span><span class="sxs-lookup"><span data-stu-id="05101-322">For example, key=”language”, and value=”eng”.</span></span>  

<span data-ttu-id="05101-323">Ver un ejemplo XML al final de Hola de este tema: [ejemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="05101-323">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="05101-324">Attributes</span><span class="sxs-lookup"><span data-stu-id="05101-324">Attributes</span></span>
| <span data-ttu-id="05101-325">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-325">Name</span></span> | <span data-ttu-id="05101-326">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-326">Type</span></span> | <span data-ttu-id="05101-327">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-327">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-328">**key**</span><span class="sxs-lookup"><span data-stu-id="05101-328">**key**</span></span><br /><br /> <span data-ttu-id="05101-329">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-329">Required</span></span> |<span data-ttu-id="05101-330">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-330">**xs:string**</span></span> |<span data-ttu-id="05101-331">clave de Hola Hola par de clave/valor.</span><span class="sxs-lookup"><span data-stu-id="05101-331">hello key in hello key/value pair.</span></span> |
| <span data-ttu-id="05101-332">**value**</span><span class="sxs-lookup"><span data-stu-id="05101-332">**value**</span></span><br /><br /> <span data-ttu-id="05101-333">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-333">Required</span></span> |<span data-ttu-id="05101-334">**xs:string**</span><span class="sxs-lookup"><span data-stu-id="05101-334">**xs:string**</span></span> |<span data-ttu-id="05101-335">valor de Hola Hola par de clave/valor.</span><span class="sxs-lookup"><span data-stu-id="05101-335">hello value in hello key/value pair.</span></span> |

## <span data-ttu-id="05101-336"><a name="ProgramType"></a> ProgramType</span><span class="sxs-lookup"><span data-stu-id="05101-336"><a name="ProgramType"></a> ProgramType</span></span>
<span data-ttu-id="05101-337">**ProgramType** es un tipo complejo global que describe un programa.</span><span class="sxs-lookup"><span data-stu-id="05101-337">**ProgramType** is a global complex type that describes a program.</span></span>  

### <a name="attributes"></a><span data-ttu-id="05101-338">Atributos</span><span class="sxs-lookup"><span data-stu-id="05101-338">Attributes</span></span>
| <span data-ttu-id="05101-339">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-339">Name</span></span> | <span data-ttu-id="05101-340">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-340">Type</span></span> | <span data-ttu-id="05101-341">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-341">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-342">**ProgramId**</span><span class="sxs-lookup"><span data-stu-id="05101-342">**ProgramId**</span></span><br /><br /> <span data-ttu-id="05101-343">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-343">Required</span></span> |<span data-ttu-id="05101-344">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-344">**xs:int**</span></span> |<span data-ttu-id="05101-345">Id. del programa.</span><span class="sxs-lookup"><span data-stu-id="05101-345">Program Id</span></span> |
| <span data-ttu-id="05101-346">**NumberOfPrograms**</span><span class="sxs-lookup"><span data-stu-id="05101-346">**NumberOfPrograms**</span></span><br /><br /> <span data-ttu-id="05101-347">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-347">Required</span></span> |<span data-ttu-id="05101-348">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-348">**xs:int**</span></span> |<span data-ttu-id="05101-349">Número de programas.</span><span class="sxs-lookup"><span data-stu-id="05101-349">Number of programs.</span></span> |
| <span data-ttu-id="05101-350">**PmtPid**</span><span class="sxs-lookup"><span data-stu-id="05101-350">**PmtPid**</span></span><br /><br /> <span data-ttu-id="05101-351">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-351">Required</span></span> |<span data-ttu-id="05101-352">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-352">**xs:int**</span></span> |<span data-ttu-id="05101-353">Las tablas de mapa de programa (Pmt) contienen información acerca de los programas.</span><span class="sxs-lookup"><span data-stu-id="05101-353">Program Map Tables (PMTs) contain information about programs.</span></span>  <span data-ttu-id="05101-354">Para más información, consulte [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span><span class="sxs-lookup"><span data-stu-id="05101-354">For more information, see [PMt](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT).</span></span> |
| <span data-ttu-id="05101-355">**PcrPid**</span><span class="sxs-lookup"><span data-stu-id="05101-355">**PcrPid**</span></span><br /><br /> <span data-ttu-id="05101-356">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-356">Required</span></span> |<span data-ttu-id="05101-357">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-357">**xs:int**</span></span> |<span data-ttu-id="05101-358">Utilizado por el descodificador.</span><span class="sxs-lookup"><span data-stu-id="05101-358">Used by decoder.</span></span> <span data-ttu-id="05101-359">Para más información, consulte [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR).</span><span class="sxs-lookup"><span data-stu-id="05101-359">For more information, see [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR)</span></span> |
| <span data-ttu-id="05101-360">**StartPTS**</span><span class="sxs-lookup"><span data-stu-id="05101-360">**StartPTS**</span></span> |<span data-ttu-id="05101-361">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="05101-361">**xs: long**</span></span> |<span data-ttu-id="05101-362">Marca de tiempo de inicio de la presentación.</span><span class="sxs-lookup"><span data-stu-id="05101-362">Starting presentation time stamp.</span></span> |
| <span data-ttu-id="05101-363">**EndPTS**</span><span class="sxs-lookup"><span data-stu-id="05101-363">**EndPTS**</span></span> |<span data-ttu-id="05101-364">**xs: long**</span><span class="sxs-lookup"><span data-stu-id="05101-364">**xs: long**</span></span> |<span data-ttu-id="05101-365">Marca de tiempo de finalización de la presentación.</span><span class="sxs-lookup"><span data-stu-id="05101-365">Ending presentation time stamp.</span></span> |

## <span data-ttu-id="05101-366"><a name="StreamDispositionType"></a> StreamDispositionType</span><span class="sxs-lookup"><span data-stu-id="05101-366"><a name="StreamDispositionType"></a> StreamDispositionType</span></span>
<span data-ttu-id="05101-367">**StreamDispositionType** es un tipo complejo global que describe el flujo de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-367">**StreamDispositionType** is a global complex type that describes hello stream.</span></span>  

<span data-ttu-id="05101-368">Ver un ejemplo XML al final de Hola de este tema: [ejemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="05101-368">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="attributes"></a><span data-ttu-id="05101-369">Attributes</span><span class="sxs-lookup"><span data-stu-id="05101-369">Attributes</span></span>
| <span data-ttu-id="05101-370">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-370">Name</span></span> | <span data-ttu-id="05101-371">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-371">Type</span></span> | <span data-ttu-id="05101-372">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-372">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-373">**Valor predeterminado**</span><span class="sxs-lookup"><span data-stu-id="05101-373">**Default**</span></span><br /><br /> <span data-ttu-id="05101-374">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-374">Required</span></span> |<span data-ttu-id="05101-375">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-375">**xs:int**</span></span> |<span data-ttu-id="05101-376">Establecer este tooindicate de too1 de atributo se trata de presentación predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-376">Set this attribute too1 tooindicate this is hello default presentation.</span></span> |
| <span data-ttu-id="05101-377">**Dub**</span><span class="sxs-lookup"><span data-stu-id="05101-377">**Dub**</span></span><br /><br /> <span data-ttu-id="05101-378">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-378">Required</span></span> |<span data-ttu-id="05101-379">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-379">**xs:int**</span></span> |<span data-ttu-id="05101-380">Establezca esta propiedad este tooindicate too1 de atributo es Hola denominado presentación.</span><span class="sxs-lookup"><span data-stu-id="05101-380">Set this attribute too1 tooindicate this is hello dubbed presentation.</span></span> |
| <span data-ttu-id="05101-381">**Original**</span><span class="sxs-lookup"><span data-stu-id="05101-381">**Original**</span></span><br /><br /> <span data-ttu-id="05101-382">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-382">Required</span></span> |<span data-ttu-id="05101-383">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-383">**xs:int**</span></span> |<span data-ttu-id="05101-384">Establecer este tooindicate de too1 de atributo se trata de la presentación original de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-384">Set this attribute too1 tooindicate this is hello original presentation.</span></span> |
| <span data-ttu-id="05101-385">**Comment**</span><span class="sxs-lookup"><span data-stu-id="05101-385">**Comment**</span></span><br /><br /> <span data-ttu-id="05101-386">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-386">Required</span></span> |<span data-ttu-id="05101-387">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-387">**xs:int**</span></span> |<span data-ttu-id="05101-388">Establezca este tooindicate too1 de atributo esta pista contiene comentarios.</span><span class="sxs-lookup"><span data-stu-id="05101-388">Set this attribute too1 tooindicate this track contains commentary.</span></span> |
| <span data-ttu-id="05101-389">**Lyrics**</span><span class="sxs-lookup"><span data-stu-id="05101-389">**Lyrics**</span></span><br /><br /> <span data-ttu-id="05101-390">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-390">Required</span></span> |<span data-ttu-id="05101-391">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-391">**xs:int**</span></span> |<span data-ttu-id="05101-392">Establezca este tooindicate too1 de atributo esta pista contiene letras.</span><span class="sxs-lookup"><span data-stu-id="05101-392">Set this attribute too1 tooindicate this track contains lyrics.</span></span> |
| <span data-ttu-id="05101-393">**Karaoke**</span><span class="sxs-lookup"><span data-stu-id="05101-393">**Karaoke**</span></span><br /><br /> <span data-ttu-id="05101-394">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-394">Required</span></span> |<span data-ttu-id="05101-395">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-395">**xs:int**</span></span> |<span data-ttu-id="05101-396">Establezca esta propiedad este tooindicate too1 de atributo representa Hola pista de karaoke (música de fondo, sin voz).</span><span class="sxs-lookup"><span data-stu-id="05101-396">Set this attribute too1 tooindicate this represents hello karaoke track (background music, no vocals).</span></span> |
| <span data-ttu-id="05101-397">**Forced**</span><span class="sxs-lookup"><span data-stu-id="05101-397">**Forced**</span></span><br /><br /> <span data-ttu-id="05101-398">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-398">Required</span></span> |<span data-ttu-id="05101-399">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-399">**xs:int**</span></span> |<span data-ttu-id="05101-400">Establecer este tooindicate de too1 de atributo se trata de la presentación de hello forzada.</span><span class="sxs-lookup"><span data-stu-id="05101-400">Set this attribute too1 tooindicate this is hello forced presentation.</span></span> |
| <span data-ttu-id="05101-401">**HearingImpaired**</span><span class="sxs-lookup"><span data-stu-id="05101-401">**HearingImpaired**</span></span><br /><br /> <span data-ttu-id="05101-402">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-402">Required</span></span> |<span data-ttu-id="05101-403">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-403">**xs:int**</span></span> |<span data-ttu-id="05101-404">Establecer este tooindicate de too1 de atributo que esta pista es para personas con discapacidad auditiva Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-404">Set this attribute too1 tooindicate this track is for hello hearing impaired.</span></span> |
| <span data-ttu-id="05101-405">**VisualImpaired**</span><span class="sxs-lookup"><span data-stu-id="05101-405">**VisualImpaired**</span></span><br /><br /> <span data-ttu-id="05101-406">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-406">Required</span></span> |<span data-ttu-id="05101-407">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-407">**xs:int**</span></span> |<span data-ttu-id="05101-408">Establecer este tooindicate de too1 de atributo que esta pista es para personas con discapacidades visuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-408">Set this attribute too1 tooindicate this track is for hello visually impaired.</span></span> |
| <span data-ttu-id="05101-409">**CleanEffects**</span><span class="sxs-lookup"><span data-stu-id="05101-409">**CleanEffects**</span></span><br /><br /> <span data-ttu-id="05101-410">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-410">Required</span></span> |<span data-ttu-id="05101-411">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-411">**xs:int**</span></span> |<span data-ttu-id="05101-412">Establecer este tooindicate de too1 de atributo que esta pista contiene efectos de limpieza.</span><span class="sxs-lookup"><span data-stu-id="05101-412">Set this attribute too1 tooindicate this track has clean effects.</span></span> |
| <span data-ttu-id="05101-413">**AttachedPic**</span><span class="sxs-lookup"><span data-stu-id="05101-413">**AttachedPic**</span></span><br /><br /> <span data-ttu-id="05101-414">Obligatorio</span><span class="sxs-lookup"><span data-stu-id="05101-414">Required</span></span> |<span data-ttu-id="05101-415">**xs:int**</span><span class="sxs-lookup"><span data-stu-id="05101-415">**xs:int**</span></span> |<span data-ttu-id="05101-416">Establecer este tooindicate de too1 de atributo que esta pista contiene imágenes.</span><span class="sxs-lookup"><span data-stu-id="05101-416">Set this attribute too1 tooindicate this track has pictures.</span></span> |

## <span data-ttu-id="05101-417"><a name="Programs"></a> Elemento Programs</span><span class="sxs-lookup"><span data-stu-id="05101-417"><a name="Programs"></a> Programs element</span></span>
<span data-ttu-id="05101-418">Elemento contenedor con varios elementos **Program**.</span><span class="sxs-lookup"><span data-stu-id="05101-418">Wrapper element holding multiple **Program** elements.</span></span>  

### <a name="child-elements"></a><span data-ttu-id="05101-419">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="05101-419">Child elements</span></span>
| <span data-ttu-id="05101-420">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-420">Name</span></span> | <span data-ttu-id="05101-421">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-421">Type</span></span> | <span data-ttu-id="05101-422">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-422">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-423">**Program**</span><span class="sxs-lookup"><span data-stu-id="05101-423">**Program**</span></span><br /><br /> <span data-ttu-id="05101-424">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="05101-424">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="05101-425">ProgramType</span><span class="sxs-lookup"><span data-stu-id="05101-425">ProgramType</span></span>](media-services-input-metadata-schema.md#ProgramType) |<span data-ttu-id="05101-426">Para archivos de recursos que se encuentran en formato MPEG-TS, contiene información acerca de los programas en el archivo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-426">For asset files that are in MPEG-TS format, contains information about programs in hello asset file.</span></span> |

## <span data-ttu-id="05101-427"><a name="VideoTracks"></a> Elemento VideoTracks</span><span class="sxs-lookup"><span data-stu-id="05101-427"><a name="VideoTracks"></a> VideoTracks element</span></span>
 <span data-ttu-id="05101-428">Elemento contenedor con varios elementos **VideoTrack**.</span><span class="sxs-lookup"><span data-stu-id="05101-428">Wrapper element holding multiple **VideoTrack** elements.</span></span>  

 <span data-ttu-id="05101-429">Ver un ejemplo XML al final de Hola de este tema: [ejemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="05101-429">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="child-elements"></a><span data-ttu-id="05101-430">Elementos secundarios</span><span class="sxs-lookup"><span data-stu-id="05101-430">Child elements</span></span>
| <span data-ttu-id="05101-431">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-431">Name</span></span> | <span data-ttu-id="05101-432">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-432">Type</span></span> | <span data-ttu-id="05101-433">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-433">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-434">**VideoTrack**</span><span class="sxs-lookup"><span data-stu-id="05101-434">**VideoTrack**</span></span><br /><br /> <span data-ttu-id="05101-435">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="05101-435">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="05101-436">VideoTrackType (hereda de TrackType)</span><span class="sxs-lookup"><span data-stu-id="05101-436">VideoTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#VideoTrackType) |<span data-ttu-id="05101-437">Contiene información sobre las pistas de vídeo en el archivo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-437">Contains information about video tracks in hello asset file.</span></span> |

## <span data-ttu-id="05101-438"><a name="AudioTracks"></a> Elemento AudioTracks</span><span class="sxs-lookup"><span data-stu-id="05101-438"><a name="AudioTracks"></a> AudioTracks element</span></span>
 <span data-ttu-id="05101-439">Elemento contenedor con varios elementos **AudioTrack**.</span><span class="sxs-lookup"><span data-stu-id="05101-439">Wrapper element holding multiple **AudioTrack** elements.</span></span>  

 <span data-ttu-id="05101-440">Ver un ejemplo XML al final de Hola de este tema: [ejemplo XML](media-services-input-metadata-schema.md#xml).</span><span class="sxs-lookup"><span data-stu-id="05101-440">See an XML example at hello end of this topic: [XML example](media-services-input-metadata-schema.md#xml).</span></span>  

### <a name="elements"></a><span data-ttu-id="05101-441">Elementos</span><span class="sxs-lookup"><span data-stu-id="05101-441">elements</span></span>
| <span data-ttu-id="05101-442">Nombre</span><span class="sxs-lookup"><span data-stu-id="05101-442">Name</span></span> | <span data-ttu-id="05101-443">Tipo</span><span class="sxs-lookup"><span data-stu-id="05101-443">Type</span></span> | <span data-ttu-id="05101-444">Descripción</span><span class="sxs-lookup"><span data-stu-id="05101-444">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05101-445">**AudioTrack**</span><span class="sxs-lookup"><span data-stu-id="05101-445">**AudioTrack**</span></span><br /><br /> <span data-ttu-id="05101-446">minOccurs="0" maxOccurs="unbounded"</span><span class="sxs-lookup"><span data-stu-id="05101-446">minOccurs="0" maxOccurs="unbounded"</span></span> |[<span data-ttu-id="05101-447">AudioTrackType (hereda de TrackType)</span><span class="sxs-lookup"><span data-stu-id="05101-447">AudioTrackType (inherits from TrackType)</span></span>](media-services-input-metadata-schema.md#AudioTrackType) |<span data-ttu-id="05101-448">Contiene información sobre las pistas de audio en el archivo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-448">Contains information about audio tracks in hello asset file.</span></span> |

## <span data-ttu-id="05101-449"><a name="code"></a> Código del esquema</span><span class="sxs-lookup"><span data-stu-id="05101-449"><a name="code"></a> Schema Code</span></span>
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
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
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
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
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
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
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
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
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
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
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

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
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
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
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
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
    </xs:schema>  


## <span data-ttu-id="05101-450"><a name="xml"></a> Ejemplo de XML</span><span class="sxs-lookup"><span data-stu-id="05101-450"><a name="xml"></a> XML example</span></span>
<span data-ttu-id="05101-451">Hola aquí te mostramos un ejemplo de archivo de metadatos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="05101-451">hello following is an example of hello Input metadata file.</span></span>  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a><span data-ttu-id="05101-452">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="05101-452">Next steps</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="05101-453">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="05101-453">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

