---
title: "flujo de trabajo de codificación Premium aaaMedia formatos y códecs | Documentos de Microsoft"
description: "En este tema se proporciona información general de códecs y formatos de formatos de flujo de trabajo de Media Encoder premium."
services: media-services
documentationcenter: 
author: juliako
manager: erik43
editor: 
ms.assetid: b197fce8-3b9b-4189-8d08-486810c0426f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;anilmur
ms.openlocfilehash: e781384ca8f08926f00c83b6710fd413ce2a3e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="107da-103">Códecs y formatos de flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="107da-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="107da-104">Si tiene preguntas sobre el codificador premium, envíe un correo a mepd en Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="107da-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="107da-105">El procesador multimedia del flujo de trabajo premium de Media Encoder del que se habla en este tema no está disponible en China.</span><span class="sxs-lookup"><span data-stu-id="107da-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="107da-106">Este documento contiene una lista de formatos de archivo de entrada y salida y códecs que son compatibles con la versión de vista previa pública de Hola de hello **flujo de trabajo de Premium de codificación de medios** codificador.</span><span class="sxs-lookup"><span data-stu-id="107da-106">This document contains a list of input and output file formats and codecs that are supported by hello public preview version of hello **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="107da-107">Códecs y formatos de entrada del flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="107da-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="107da-108">Códecs y formatos de salida del flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="107da-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="107da-109">**Flujo de trabajo del Codificador multimedia premium** admite los subtítulos que se describen en [esta](#closed_captioning) sección.</span><span class="sxs-lookup"><span data-stu-id="107da-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="107da-110"><a id="input_formats"></a>Códecs y formatos de entrada de flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="107da-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="107da-111">Hola siguiente sección enumera Hola códecs y formatos de archivo que es compatible con este procesador multimedia como entrada.</span><span class="sxs-lookup"><span data-stu-id="107da-111">hello following section lists hello codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="107da-112">Formatos de archivo/contenedor de entrada</span><span class="sxs-lookup"><span data-stu-id="107da-112">Input Container/File Formats</span></span>
* <span data-ttu-id="107da-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="107da-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="107da-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="107da-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="107da-115">GXF</span><span class="sxs-lookup"><span data-stu-id="107da-115">GXF</span></span>
* <span data-ttu-id="107da-116">Secuencias de transporte MPEG-2</span><span class="sxs-lookup"><span data-stu-id="107da-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="107da-117">Secuencias de programa MPEG-2</span><span class="sxs-lookup"><span data-stu-id="107da-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="107da-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="107da-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="107da-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="107da-119">Windows Media/ASF</span></span>
* <span data-ttu-id="107da-120">AVI (sin comprimir de 8 bits/10 bits)</span><span class="sxs-lookup"><span data-stu-id="107da-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="107da-121">Códecs de vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="107da-121">Input Video Codecs</span></span>
* <span data-ttu-id="107da-122">AVC 8/10 bits, la too4:2:2, incluidos los AVCIntra</span><span class="sxs-lookup"><span data-stu-id="107da-122">AVC 8-bit/10-bit, up too4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="107da-123">Avid DNxHD (en MXF)</span><span class="sxs-lookup"><span data-stu-id="107da-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="107da-124">DVCPro/DVCProHD (en MXF)</span><span class="sxs-lookup"><span data-stu-id="107da-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="107da-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="107da-125">JPEG2000</span></span>
* <span data-ttu-id="107da-126">MPEG-2 (perfil de too422 y de alto nivel, incluido el variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® y D10)</span><span class="sxs-lookup"><span data-stu-id="107da-126">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="107da-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="107da-127">MPEG-1</span></span>
* <span data-ttu-id="107da-128">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="107da-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="107da-129">Códecs de audio de entrada</span><span class="sxs-lookup"><span data-stu-id="107da-129">Input Audio Codecs</span></span>
* <span data-ttu-id="107da-130">AES (SMPTE 331M y 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="107da-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="107da-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="107da-131">Dolby® E</span></span>
* <span data-ttu-id="107da-132">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="107da-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="107da-133">AAC (AAC-LC, HE-AAC y AAC-HEv2; seguridad too5.1)</span><span class="sxs-lookup"><span data-stu-id="107da-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="107da-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="107da-134">MPEG Layer 2</span></span>
* <span data-ttu-id="107da-135">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="107da-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="107da-136">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="107da-136">Windows Media Audio</span></span>
* <span data-ttu-id="107da-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="107da-137">WAV/PCM</span></span>

## <span data-ttu-id="107da-138"><a id="output_format"></a>Códecs y formatos de salida de flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="107da-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="107da-139">Hello siguiente sección enumeran Hola códecs y formatos de archivo que se admiten como resultado de este procesador multimedia.</span><span class="sxs-lookup"><span data-stu-id="107da-139">hello following section lists hello codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="107da-140">Formatos de archivo/contenedor de salida</span><span class="sxs-lookup"><span data-stu-id="107da-140">Output Container/File Formats</span></span>
* <span data-ttu-id="107da-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="107da-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="107da-142">MXF (OP1a, XDCAM y AS02)</span><span class="sxs-lookup"><span data-stu-id="107da-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="107da-143">DPP (incluido AS11)</span><span class="sxs-lookup"><span data-stu-id="107da-143">DPP (including AS11)</span></span>
* <span data-ttu-id="107da-144">GXF</span><span class="sxs-lookup"><span data-stu-id="107da-144">GXF</span></span>
* <span data-ttu-id="107da-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="107da-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="107da-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="107da-146">Windows Media/ASF</span></span>
* <span data-ttu-id="107da-147">AVI (sin comprimir de 8 bits/10 bits)</span><span class="sxs-lookup"><span data-stu-id="107da-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="107da-148">Formato de archivo de streaming con velocidad de transmisión adaptable (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="107da-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="107da-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="107da-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="107da-150">Códecs de vídeo de salida</span><span class="sxs-lookup"><span data-stu-id="107da-150">Output Video Codecs</span></span>
* <span data-ttu-id="107da-151">AVC (H.264; 8 bits; una copia de seguridad tooHigh perfil, nivel 5.2; HD Ultra de 4K; Dentro de AVC)</span><span class="sxs-lookup"><span data-stu-id="107da-151">AVC (H.264; 8-bit; up tooHigh Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="107da-152">Avid DNxHD (en MXF)</span><span class="sxs-lookup"><span data-stu-id="107da-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="107da-153">DVCPro/DVCProHD (en MXF)</span><span class="sxs-lookup"><span data-stu-id="107da-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="107da-154">MPEG-2 (perfil de too422 y de alto nivel, incluido el variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® y D10)</span><span class="sxs-lookup"><span data-stu-id="107da-154">MPEG-2 (up too422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="107da-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="107da-155">MPEG-1</span></span>
* <span data-ttu-id="107da-156">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="107da-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="107da-157">Creación de miniaturas JPEG</span><span class="sxs-lookup"><span data-stu-id="107da-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="107da-158">Códecs de audio de salida</span><span class="sxs-lookup"><span data-stu-id="107da-158">Output Audio Codecs</span></span>
* <span data-ttu-id="107da-159">AES (SMPTE 331M y 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="107da-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="107da-160">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="107da-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="107da-161">Dolby® Digital Plus (E-AC3) seguridad too7.1</span><span class="sxs-lookup"><span data-stu-id="107da-161">Dolby® Digital Plus (E-AC3) up too7.1</span></span>
* <span data-ttu-id="107da-162">AAC (AAC-LC, HE-AAC y AAC-HEv2; seguridad too5.1)</span><span class="sxs-lookup"><span data-stu-id="107da-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up too5.1)</span></span>
* <span data-ttu-id="107da-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="107da-163">MPEG Layer 2</span></span>
* <span data-ttu-id="107da-164">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="107da-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="107da-165">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="107da-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="107da-166">Si codifica tooDolby® Digital (AC3), salida de hello solo se puede escribir en un archivo ISO MP4.</span><span class="sxs-lookup"><span data-stu-id="107da-166">If you encode tooDolby® Digital (AC3), hello output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="107da-167"><a id="closed_captioning"></a>Compatibilidad con subtítulos</span><span class="sxs-lookup"><span data-stu-id="107da-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="107da-168">En la entrada, el **flujo de trabajo del Codificador multimedia Premium** admite:</span><span class="sxs-lookup"><span data-stu-id="107da-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="107da-169">Archivos SCC</span><span class="sxs-lookup"><span data-stu-id="107da-169">SCC files</span></span>
2. <span data-ttu-id="107da-170">Archivos SMPTE-TT</span><span class="sxs-lookup"><span data-stu-id="107da-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="107da-171">CEA-608/CEA-708: llevados como datos de usuario (mensajes SEI de secuencias elementales H.264, ATSC/53 y SCTE20) o llevdosa como datos auxiliares en archivos MXF/GXF</span><span class="sxs-lookup"><span data-stu-id="107da-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="107da-172">Archivos de subtítulos STL</span><span class="sxs-lookup"><span data-stu-id="107da-172">STL subtitle files</span></span>

<span data-ttu-id="107da-173">En la salida, Hola siguientes opciones está disponible:</span><span class="sxs-lookup"><span data-stu-id="107da-173">On output, hello following options are available:</span></span>

1. <span data-ttu-id="107da-174">608 CEA 708 tooCEA traducción</span><span class="sxs-lookup"><span data-stu-id="107da-174">CEA-608 tooCEA-708 translation</span></span>
2. <span data-ttu-id="107da-175">Transferencia CEA-608/CEA-708 (incrustado en mensajes SEI de secuencias elementales de H.264 o transportado como datos auxiliares en archivos MXF)</span><span class="sxs-lookup"><span data-stu-id="107da-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="107da-176">SCC</span><span class="sxs-lookup"><span data-stu-id="107da-176">SCC</span></span>
4. <span data-ttu-id="107da-177">Texto sincronizado SMPTE (de origen CEA-608 por SMPTE RP2052; incluida la creación de archivos DFXP)</span><span class="sxs-lookup"><span data-stu-id="107da-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="107da-178">Archivo de subtítulos SRT</span><span class="sxs-lookup"><span data-stu-id="107da-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="107da-179">Secuencias de subtítulos DVB</span><span class="sxs-lookup"><span data-stu-id="107da-179">DVB subtitle streams</span></span>

<span data-ttu-id="107da-180">Nota: no todas de hello por encima de los formatos de salida se admiten para la entrega a través de streaming de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="107da-180">Note: not all of hello above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="107da-181">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="107da-181">Known issues</span></span>
<span data-ttu-id="107da-182">Si el vídeo de entrada no contiene subtítulos, Hola salida que activos todavía contendrá un archivo TTML vacío.</span><span class="sxs-lookup"><span data-stu-id="107da-182">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="107da-183">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="107da-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="107da-184">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="107da-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

