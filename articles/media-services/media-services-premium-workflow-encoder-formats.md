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
# <a name="media-encoder-premium-workflow-formats-and-codecs"></a>Códecs y formatos de flujo de trabajo del Codificador multimedia Premium
> [!NOTE]
> Si tiene preguntas sobre el codificador premium, envíe un correo a mepd en Microsoft.com.
> 
> El procesador multimedia del flujo de trabajo premium de Media Encoder del que se habla en este tema no está disponible en China. 
> 
> 

Este documento contiene una lista de formatos de archivo de entrada y salida y códecs que son compatibles con la versión de vista previa pública de Hola de hello **flujo de trabajo de Premium de codificación de medios** codificador.

[Códecs y formatos de entrada del flujo de trabajo del Codificador multimedia Premium](#input_formats)

[Códecs y formatos de salida del flujo de trabajo del Codificador multimedia Premium](#output_formats)

**Flujo de trabajo del Codificador multimedia premium** admite los subtítulos que se describen en [esta](#closed_captioning) sección. 

## <a id="input_formats"></a>Códecs y formatos de entrada de flujo de trabajo del Codificador multimedia Premium
Hola siguiente sección enumera Hola códecs y formatos de archivo que es compatible con este procesador multimedia como entrada.

### <a name="input-containerfile-formats"></a>Formatos de archivo/contenedor de entrada
* Adobe® Flash® F4V
* MXF/SMPTE 377M
* GXF
* Secuencias de transporte MPEG-2
* Secuencias de programa MPEG-2
* MPEG-4/MP4
* Windows Media/ASF
* AVI (sin comprimir de 8 bits/10 bits)

### <a name="input-video-codecs"></a>Códecs de vídeo de entrada
* AVC 8/10 bits, la too4:2:2, incluidos los AVCIntra
* Avid DNxHD (en MXF)
* DVCPro/DVCProHD (en MXF)
* JPEG2000
* MPEG-2 (perfil de too422 y de alto nivel, incluido el variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® y D10)
* MPEG-1
* Windows Media Video/VC-1

### <a name="input-audio-codecs"></a>Códecs de audio de entrada
* AES (SMPTE 331M y 302M, AES3-2003)
* Dolby® E
* Dolby® Digital (AC3)
* AAC (AAC-LC, HE-AAC y AAC-HEv2; seguridad too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Windows Media Audio
* WAV/PCM

## <a id="output_format"></a>Códecs y formatos de salida de flujo de trabajo del Codificador multimedia Premium
Hello siguiente sección enumeran Hola códecs y formatos de archivo que se admiten como resultado de este procesador multimedia.

### <a name="output-containerfile-formats"></a>Formatos de archivo/contenedor de salida
* Adobe® Flash® F4V
* MXF (OP1a, XDCAM y AS02)
* DPP (incluido AS11)
* GXF
* MPEG-4/MP4
* Windows Media/ASF
* AVI (sin comprimir de 8 bits/10 bits)
* Formato de archivo de streaming con velocidad de transmisión adaptable (PIFF 1.3)
* MPEG-TS 

### <a name="output-video-codecs"></a>Códecs de vídeo de salida
* AVC (H.264; 8 bits; una copia de seguridad tooHigh perfil, nivel 5.2; HD Ultra de 4K; Dentro de AVC)
* Avid DNxHD (en MXF)
* DVCPro/DVCProHD (en MXF)
* MPEG-2 (perfil de too422 y de alto nivel, incluido el variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® y D10)
* MPEG-1
* Windows Media Video/VC-1
* Creación de miniaturas JPEG

### <a name="output-audio-codecs"></a>Códecs de audio de salida
* AES (SMPTE 331M y 302M, AES3-2003)
* Dolby® Digital (AC3)
* Dolby® Digital Plus (E-AC3) seguridad too7.1
* AAC (AAC-LC, HE-AAC y AAC-HEv2; seguridad too5.1)
* MPEG Layer 2
* MP3 (MPEG-1 Audio Layer 3)
* Windows Media Audio

>[!NOTE]
>Si codifica tooDolby® Digital (AC3), salida de hello solo se puede escribir en un archivo ISO MP4.

## <a id="closed_captioning"></a>Compatibilidad con subtítulos
En la entrada, el **flujo de trabajo del Codificador multimedia Premium** admite:

1. Archivos SCC
2. Archivos SMPTE-TT
3. CEA-608/CEA-708: llevados como datos de usuario (mensajes SEI de secuencias elementales H.264, ATSC/53 y SCTE20) o llevdosa como datos auxiliares en archivos MXF/GXF
4. Archivos de subtítulos STL

En la salida, Hola siguientes opciones está disponible:

1. 608 CEA 708 tooCEA traducción
2. Transferencia CEA-608/CEA-708 (incrustado en mensajes SEI de secuencias elementales de H.264 o transportado como datos auxiliares en archivos MXF)
3. SCC
4. Texto sincronizado SMPTE (de origen CEA-608 por SMPTE RP2052; incluida la creación de archivos DFXP)
5. Archivo de subtítulos SRT
6. Secuencias de subtítulos DVB

Nota: no todas de hello por encima de los formatos de salida se admiten para la entrega a través de streaming de servicios multimedia de Azure.

## <a name="known-issues"></a>Problemas conocidos
Si el vídeo de entrada no contiene subtítulos, Hola salida que activos todavía contendrá un archivo TTML vacío. 

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

