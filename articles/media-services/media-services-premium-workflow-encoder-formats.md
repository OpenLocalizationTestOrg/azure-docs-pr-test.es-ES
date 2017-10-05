---
title: "Códecs y formatos del Flujo de trabajo del Codificador multimedia premium | Microsoft Docs"
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
ms.openlocfilehash: e18de2adc9aac585d6890dd7b43a54f1a0ca177e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a><span data-ttu-id="fab47-103">Códecs y formatos de flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="fab47-103">Media Encoder Premium Workflow formats and codecs</span></span>
> [!NOTE]
> <span data-ttu-id="fab47-104">Si tiene preguntas sobre el codificador premium, envíe un correo a mepd en Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="fab47-104">For premium encoder questions, email mepd at Microsoft.com.</span></span>
> 
> <span data-ttu-id="fab47-105">El procesador multimedia del flujo de trabajo premium de Media Encoder del que se habla en este tema no está disponible en China.</span><span class="sxs-lookup"><span data-stu-id="fab47-105">Media Encoder Premium Workflow media processor discussed in this topic is not available in China.</span></span> 
> 
> 

<span data-ttu-id="fab47-106">Este documento contiene una lista de los formatos de archivo de entrada y salida y los códecs que son compatibles con la vista previa pública del **Flujo de trabajo del Codificador multimedia premium** .</span><span class="sxs-lookup"><span data-stu-id="fab47-106">This document contains a list of input and output file formats and codecs that are supported by the public preview version of the **Media Encoder Premium Workflow** encoder.</span></span>

[<span data-ttu-id="fab47-107">Códecs y formatos de entrada del flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="fab47-107">Media Encoder Premium Worflow Input Formats and Codecs</span></span>](#input_formats)

[<span data-ttu-id="fab47-108">Códecs y formatos de salida del flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="fab47-108">Media Encoder Premium Worflow Output Formats and Codecs</span></span>](#output_formats)

<span data-ttu-id="fab47-109">**Flujo de trabajo del Codificador multimedia premium** admite los subtítulos que se describen en [esta](#closed_captioning) sección.</span><span class="sxs-lookup"><span data-stu-id="fab47-109">**Media Encoder Premium Workflow** supports closed captioning described in [this](#closed_captioning) section.</span></span> 

## <span data-ttu-id="fab47-110"><a id="input_formats"></a>Códecs y formatos de entrada de flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="fab47-110"><a id="input_formats"></a>Media Encoder Premium Workflow Input Formats and Codecs</span></span>
<span data-ttu-id="fab47-111">En la sección siguiente se enumeran los códecs y formatos de archivo que admite este procesador multimedia como entrada.</span><span class="sxs-lookup"><span data-stu-id="fab47-111">The following section lists the codecs and file formats that this media processor supports as input.</span></span>

### <a name="input-containerfile-formats"></a><span data-ttu-id="fab47-112">Formatos de archivo/contenedor de entrada</span><span class="sxs-lookup"><span data-stu-id="fab47-112">Input Container/File Formats</span></span>
* <span data-ttu-id="fab47-113">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="fab47-113">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="fab47-114">MXF/SMPTE 377M</span><span class="sxs-lookup"><span data-stu-id="fab47-114">MXF/SMPTE 377M</span></span>
* <span data-ttu-id="fab47-115">GXF</span><span class="sxs-lookup"><span data-stu-id="fab47-115">GXF</span></span>
* <span data-ttu-id="fab47-116">Secuencias de transporte MPEG-2</span><span class="sxs-lookup"><span data-stu-id="fab47-116">MPEG-2 Transport Streams</span></span>
* <span data-ttu-id="fab47-117">Secuencias de programa MPEG-2</span><span class="sxs-lookup"><span data-stu-id="fab47-117">MPEG-2 Program Streams</span></span>
* <span data-ttu-id="fab47-118">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="fab47-118">MPEG-4/MP4</span></span>
* <span data-ttu-id="fab47-119">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="fab47-119">Windows Media/ASF</span></span>
* <span data-ttu-id="fab47-120">AVI (sin comprimir de 8 bits/10 bits)</span><span class="sxs-lookup"><span data-stu-id="fab47-120">AVI (Uncompressed 8bit/10bit)</span></span>

### <a name="input-video-codecs"></a><span data-ttu-id="fab47-121">Códecs de vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="fab47-121">Input Video Codecs</span></span>
* <span data-ttu-id="fab47-122">AVC 8 bits/10 bits, hasta 4:2:2, incluido AVCIntra</span><span class="sxs-lookup"><span data-stu-id="fab47-122">AVC 8-bit/10-bit, up to 4:2:2, including AVCIntra</span></span>
* <span data-ttu-id="fab47-123">Avid DNxHD (en MXF)</span><span class="sxs-lookup"><span data-stu-id="fab47-123">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="fab47-124">DVCPro/DVCProHD (en MXF)</span><span class="sxs-lookup"><span data-stu-id="fab47-124">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="fab47-125">JPEG2000</span><span class="sxs-lookup"><span data-stu-id="fab47-125">JPEG2000</span></span>
* <span data-ttu-id="fab47-126">MPEG-2 (hasta 422 Perfil y Nivel alto; incluidas variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® y D10)</span><span class="sxs-lookup"><span data-stu-id="fab47-126">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="fab47-127">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="fab47-127">MPEG-1</span></span>
* <span data-ttu-id="fab47-128">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="fab47-128">Windows Media Video/VC-1</span></span>

### <a name="input-audio-codecs"></a><span data-ttu-id="fab47-129">Códecs de audio de entrada</span><span class="sxs-lookup"><span data-stu-id="fab47-129">Input Audio Codecs</span></span>
* <span data-ttu-id="fab47-130">AES (SMPTE 331M y 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="fab47-130">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="fab47-131">Dolby® E</span><span class="sxs-lookup"><span data-stu-id="fab47-131">Dolby® E</span></span>
* <span data-ttu-id="fab47-132">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="fab47-132">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="fab47-133">AAC (AAC-LC, AAC-HE y AAC-HEv2; hasta 5.1)</span><span class="sxs-lookup"><span data-stu-id="fab47-133">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="fab47-134">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="fab47-134">MPEG Layer 2</span></span>
* <span data-ttu-id="fab47-135">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="fab47-135">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="fab47-136">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="fab47-136">Windows Media Audio</span></span>
* <span data-ttu-id="fab47-137">WAV/PCM</span><span class="sxs-lookup"><span data-stu-id="fab47-137">WAV/PCM</span></span>

## <span data-ttu-id="fab47-138"><a id="output_format"></a>Códecs y formatos de salida de flujo de trabajo del Codificador multimedia Premium</span><span class="sxs-lookup"><span data-stu-id="fab47-138"><a id="output_format"></a>Media Encoder Premium Workflow Output Formats and Codecs</span></span>
<span data-ttu-id="fab47-139">En la sección siguiente se enumeran los códecs y formatos de archivo que se admiten como salida de este procesador multimedia.</span><span class="sxs-lookup"><span data-stu-id="fab47-139">The following section lists the codecs and file formats that are supported as output from this media processor.</span></span>

### <a name="output-containerfile-formats"></a><span data-ttu-id="fab47-140">Formatos de archivo/contenedor de salida</span><span class="sxs-lookup"><span data-stu-id="fab47-140">Output Container/File Formats</span></span>
* <span data-ttu-id="fab47-141">Adobe® Flash® F4V</span><span class="sxs-lookup"><span data-stu-id="fab47-141">Adobe® Flash® F4V</span></span>
* <span data-ttu-id="fab47-142">MXF (OP1a, XDCAM y AS02)</span><span class="sxs-lookup"><span data-stu-id="fab47-142">MXF (OP1a, XDCAM and AS02)</span></span>
* <span data-ttu-id="fab47-143">DPP (incluido AS11)</span><span class="sxs-lookup"><span data-stu-id="fab47-143">DPP (including AS11)</span></span>
* <span data-ttu-id="fab47-144">GXF</span><span class="sxs-lookup"><span data-stu-id="fab47-144">GXF</span></span>
* <span data-ttu-id="fab47-145">MPEG-4/MP4</span><span class="sxs-lookup"><span data-stu-id="fab47-145">MPEG-4/MP4</span></span>
* <span data-ttu-id="fab47-146">Windows Media/ASF</span><span class="sxs-lookup"><span data-stu-id="fab47-146">Windows Media/ASF</span></span>
* <span data-ttu-id="fab47-147">AVI (sin comprimir de 8 bits/10 bits)</span><span class="sxs-lookup"><span data-stu-id="fab47-147">AVI (Uncompressed 8bit/10bit)</span></span>
* <span data-ttu-id="fab47-148">Formato de archivo de streaming con velocidad de transmisión adaptable (PIFF 1.3)</span><span class="sxs-lookup"><span data-stu-id="fab47-148">Smooth Streaming File Format (PIFF 1.3)</span></span>
* <span data-ttu-id="fab47-149">MPEG-TS</span><span class="sxs-lookup"><span data-stu-id="fab47-149">MPEG-TS</span></span> 

### <a name="output-video-codecs"></a><span data-ttu-id="fab47-150">Códecs de vídeo de salida</span><span class="sxs-lookup"><span data-stu-id="fab47-150">Output Video Codecs</span></span>
* <span data-ttu-id="fab47-151">AVC (H.264; 8 bits; hasta Perfil alto, Nivel 5.2; 4K Ultra HD; AVC Intra)</span><span class="sxs-lookup"><span data-stu-id="fab47-151">AVC (H.264; 8-bit; up to High Profile, Level 5.2; 4K Ultra HD; AVC Intra)</span></span>
* <span data-ttu-id="fab47-152">Avid DNxHD (en MXF)</span><span class="sxs-lookup"><span data-stu-id="fab47-152">Avid DNxHD (in MXF)</span></span>
* <span data-ttu-id="fab47-153">DVCPro/DVCProHD (en MXF)</span><span class="sxs-lookup"><span data-stu-id="fab47-153">DVCPro/DVCProHD (in MXF)</span></span>
* <span data-ttu-id="fab47-154">MPEG-2 (hasta 422 Perfil y Nivel alto; incluidas variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® y D10)</span><span class="sxs-lookup"><span data-stu-id="fab47-154">MPEG-2 (up to 422 Profile and High Level; including variants such as XDCAM, XDCAM HD, XDCAM IMX, CableLabs® and D10)</span></span>
* <span data-ttu-id="fab47-155">MPEG-1</span><span class="sxs-lookup"><span data-stu-id="fab47-155">MPEG-1</span></span>
* <span data-ttu-id="fab47-156">Windows Media Video/VC-1</span><span class="sxs-lookup"><span data-stu-id="fab47-156">Windows Media Video/VC-1</span></span>
* <span data-ttu-id="fab47-157">Creación de miniaturas JPEG</span><span class="sxs-lookup"><span data-stu-id="fab47-157">JPEG thumbnail creation</span></span>

### <a name="output-audio-codecs"></a><span data-ttu-id="fab47-158">Códecs de audio de salida</span><span class="sxs-lookup"><span data-stu-id="fab47-158">Output Audio Codecs</span></span>
* <span data-ttu-id="fab47-159">AES (SMPTE 331M y 302M, AES3-2003)</span><span class="sxs-lookup"><span data-stu-id="fab47-159">AES (SMPTE 331M and 302M, AES3-2003)</span></span>
* <span data-ttu-id="fab47-160">Dolby® Digital (AC3)</span><span class="sxs-lookup"><span data-stu-id="fab47-160">Dolby® Digital (AC3)</span></span>
* <span data-ttu-id="fab47-161">Dolby® Digital Plus (E-AC3) hasta 7.1</span><span class="sxs-lookup"><span data-stu-id="fab47-161">Dolby® Digital Plus (E-AC3) up to 7.1</span></span>
* <span data-ttu-id="fab47-162">AAC (AAC-LC, AAC-HE y AAC-HEv2; hasta 5.1)</span><span class="sxs-lookup"><span data-stu-id="fab47-162">AAC (AAC-LC, AAC-HE, and AAC-HEv2; up to 5.1)</span></span>
* <span data-ttu-id="fab47-163">MPEG Layer 2</span><span class="sxs-lookup"><span data-stu-id="fab47-163">MPEG Layer 2</span></span>
* <span data-ttu-id="fab47-164">MP3 (MPEG-1 Audio Layer 3)</span><span class="sxs-lookup"><span data-stu-id="fab47-164">MP3 (MPEG-1 Audio Layer 3)</span></span>
* <span data-ttu-id="fab47-165">Windows Media Audio</span><span class="sxs-lookup"><span data-stu-id="fab47-165">Windows Media Audio</span></span>

>[!NOTE]
><span data-ttu-id="fab47-166">Si utiliza la codificación en Dolby® Digital (AC3), la salida solo puede escribirse en un archivo ISO MP4.</span><span class="sxs-lookup"><span data-stu-id="fab47-166">If you encode to Dolby® Digital (AC3), the output can only be written into an ISO MP4 file.</span></span>

## <span data-ttu-id="fab47-167"><a id="closed_captioning"></a>Compatibilidad con subtítulos</span><span class="sxs-lookup"><span data-stu-id="fab47-167"><a id="closed_captioning"></a>Support for Closed Captioning</span></span>
<span data-ttu-id="fab47-168">En la entrada, el **flujo de trabajo del Codificador multimedia Premium** admite:</span><span class="sxs-lookup"><span data-stu-id="fab47-168">On ingest, **Media Encoder Premium Workflow** supports:</span></span>

1. <span data-ttu-id="fab47-169">Archivos SCC</span><span class="sxs-lookup"><span data-stu-id="fab47-169">SCC files</span></span>
2. <span data-ttu-id="fab47-170">Archivos SMPTE-TT</span><span class="sxs-lookup"><span data-stu-id="fab47-170">SMPTE-TT files</span></span>
3. <span data-ttu-id="fab47-171">CEA-608/CEA-708: llevados como datos de usuario (mensajes SEI de secuencias elementales H.264, ATSC/53 y SCTE20) o llevdosa como datos auxiliares en archivos MXF/GXF</span><span class="sxs-lookup"><span data-stu-id="fab47-171">CEA-608/CEA-708 – carried as user data (SEI messages of H.264 elementary streams, ATSC/53, SCTE20) or carried as ancillary data in MXF/GXF files</span></span>
4. <span data-ttu-id="fab47-172">Archivos de subtítulos STL</span><span class="sxs-lookup"><span data-stu-id="fab47-172">STL subtitle files</span></span>

<span data-ttu-id="fab47-173">En la salida, están disponibles las siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="fab47-173">On output, the following options are available:</span></span>

1. <span data-ttu-id="fab47-174">Traducción de CEA-608 a CEA-708</span><span class="sxs-lookup"><span data-stu-id="fab47-174">CEA-608 to CEA-708 translation</span></span>
2. <span data-ttu-id="fab47-175">Transferencia CEA-608/CEA-708 (incrustado en mensajes SEI de secuencias elementales de H.264 o transportado como datos auxiliares en archivos MXF)</span><span class="sxs-lookup"><span data-stu-id="fab47-175">CEA-608/CEA-708 pass through (embedded in SEI messages of H.264 elementary streams, or carried as ancillary data in MXF files)</span></span>
3. <span data-ttu-id="fab47-176">SCC</span><span class="sxs-lookup"><span data-stu-id="fab47-176">SCC</span></span>
4. <span data-ttu-id="fab47-177">Texto sincronizado SMPTE (de origen CEA-608 por SMPTE RP2052; incluida la creación de archivos DFXP)</span><span class="sxs-lookup"><span data-stu-id="fab47-177">SMPTE Timed Text (from source CEA-608 per SMPTE RP2052; including DFXP file creation)</span></span>
5. <span data-ttu-id="fab47-178">Archivo de subtítulos SRT</span><span class="sxs-lookup"><span data-stu-id="fab47-178">SRT Subtitle file</span></span>
6. <span data-ttu-id="fab47-179">Secuencias de subtítulos DVB</span><span class="sxs-lookup"><span data-stu-id="fab47-179">DVB subtitle streams</span></span>

<span data-ttu-id="fab47-180">Nota: no todos los formatos de salida anteriores se admiten para la entrega mediante streaming en Servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="fab47-180">Note: not all of the above output formats are supported for delivery via streaming in Azure Media Services.</span></span>

## <a name="known-issues"></a><span data-ttu-id="fab47-181">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="fab47-181">Known issues</span></span>
<span data-ttu-id="fab47-182">Si el vídeo de entrada no contiene subtítulos, el recurso de salida seguirá conteniendo un archivo TTML vacío.</span><span class="sxs-lookup"><span data-stu-id="fab47-182">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="fab47-183">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="fab47-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fab47-184">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="fab47-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

