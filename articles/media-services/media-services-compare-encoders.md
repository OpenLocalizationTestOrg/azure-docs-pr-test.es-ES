---
title: "aaaComparison de Azure en codificadores de medios de petición | Documentos de Microsoft"
description: "En este tema se compara las capacidades de codificación de Hola de ** Media Encoder estándar ** y ** Media Encoder Premium flujo de trabajo **."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: a79437c0-4832-423a-bca8-82632b2c47cc
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: ee04ad10d8e7c5f4f3c6e91e9b7679c2aba82c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-on-demand-media-encoders"></a>Comparación de codificadores multimedia a petición de Azure

En este tema se compara las capacidades de codificación de Hola de **Media Encoder estándar** y **flujo de trabajo de Premium de codificación de medios**.

## <a name="video-and-audio-processing-capabilities"></a>Funcionalidades de procesamiento de vídeo y audio

Hello en la tabla siguiente compara la funcionalidad de hello entre medios codificador estándar (MES) y el flujo de trabajo de Premium de codificador multimedia (MEPW). 

|Capacidad|Media Encoder Estándar|Flujo de trabajo de Media Encoder Premium|
|---|---|---|
|Aplicación de la lógica condicional durante la codificación<br/>(por ejemplo, si la entrada de hello está HD, a continuación, codificar audio 5.1)|No|Sí|
|Subtítulos (CC)|No|[Sí](media-services-premium-workflow-encoder-formats.md#closed_captioning)|
|[Corrección de volumen profesional Dolby®](http://www.dolby.com/us/en/technologies/dolby-professional-loudness-solutions.pdf)<br/> con Dialogue Intelligence™|No|Sí|
|Deshacer entrelazado, telecine inverso|Básica|Calidad de difusión|
|Detectar y quitar bordes negros <br/>(formato pillarbox y formato letterbox)|No|Sí|
|Generación de miniaturas|[Sí](media-services-dotnet-generate-thumbnail-with-mes.md)|[Sí](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)|
|Recorte y unión de vídeos|[Sí](media-services-advanced-encoding-with-mes.md#trim_video)|Sí|
|Superposiciones de audio o vídeo|[Sí](media-services-advanced-encoding-with-mes.md#overlay)|[Sí](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-1--overlay-an-image-on-top-of-the-video)|
|Superposiciones de gráficos|De orígenes de imagen|De orígenes de imagen y texto|
|Varias pistas de idiomas de audio|Limitado|[Sí](media-services-media-encoder-premium-workflow-multiplefilesinput.md#example-2--multiple-audio-language-encoding)|

## <a id="billing"></a>Medidor de facturación usado por cada codificador
| Nombre de procesador multimedia | Precios aplicables | Notas |
| --- | --- | --- |
| **Media Encoder Estándar** |ENCODER |Codificación se cobrará tareas en función de la duración total de hello, en minutos, de todos los archivos de medios de hello generados como resultado, con velocidad de hello especificado [aquí][1], en la columna de CODIFICADOR de Hola. |
| **Flujo de trabajo del Codificador multimedia** |CODIFICADOR PREMIUM |Codificación se cobrará tareas en función de la duración total de hello, en minutos, de todos los archivos de medios de hello generados como resultado, con velocidad de hello especificado [aquí][1], en la columna de hello CODIFICADOR PREMIUM. |

## <a name="input-containerfile-formats"></a>Formatos de archivo/contenedor de entrada
| Formatos de archivo/contenedor de entrada | Media Encoder Estándar | Flujo de trabajo del Codificador multimedia |
| --- | --- | --- |
| Adobe® Flash® F4V |Sí |Sí |
| MXF/SMPTE 377M |Sí |Sí |
| GXF |Sí |Sí |
| Secuencias de transporte MPEG-2 |Sí |Sí |
| Secuencias de programa MPEG-2 |Sí |Sí |
| MPEG-4/MP4 |Sí |Sí |
| Windows Media/ASF |Sí |Sí |
| AVI (sin comprimir de 8 bits/10 bits) |Sí |Sí |
| 3GPP/3GPP2 |Sí |No |
| Formato de archivo de streaming con velocidad de transmisión adaptable (PIFF 1.3) |Sí |No |
| [Microsoft Digital Video Recording(DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) |Sí |No |
| Matroska/WebM |Sí |No |
| QuickTime (.mov) |Sí |No |

## <a name="input-video-codecs"></a>Códecs de vídeo de entrada
| Códecs de vídeo de entrada | Media Encoder Estándar | Flujo de trabajo del Codificador multimedia |
| --- | --- | --- |
| AVC 8/10 bits, la too4:2:2, incluidos los AVCIntra |8 bits: 4:2:0 y 4:2:2 |Sí |
| Avid DNxHD (en MXF) |Sí |Sí |
| DVCPro/DVCProHD (en MXF) |Sí |Sí |
| JPEG2000 |Sí |Sí |
| MPEG-2 (perfil de too422 y de alto nivel, incluido el variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® y D10) |Perfil de too422 |Sí |
| MPEG-1 |Sí |Sí |
| Windows Media Video/VC-1 |Sí |Sí |
| Canopus HQ/HQX |No |No |
| MPEG-4, parte 2 |Sí |No |
| [Theora](https://en.wikipedia.org/wiki/Theora) |Sí |No |
| Apple ProRes 422 |Sí |No |
| Apple ProRes 422 LT |Sí |No |
| Apple ProRes 422 HQ |Sí |No |
| Apple ProRes Proxy |Sí |No |
| Apple ProRes 4444 |Sí |No |
| Apple ProRes 4444 XQ |Sí |No |

## <a name="input-audio-codecs"></a>Códecs de audio de entrada
| Códecs de audio de entrada | Media Encoder Estándar | Flujo de trabajo del Codificador multimedia |
| --- | --- | --- |
| AES (SMPTE 331M y 302M, AES3-2003) |No |Sí |
| Dolby® E |No |Sí |
| Dolby® Digital (AC3) |No |Sí |
| Dolby® Digital Plus (E-AC3) |No |Sí |
| AAC (AAC-LC, HE-AAC y AAC-HEv2; seguridad too5.1) |Sí |Sí |
| MPEG Layer 2 |Sí |Sí |
| MP3 (MPEG-1 Audio Layer 3) |Sí |Sí |
| Windows Media Audio |Sí |Sí |
| WAV/PCM |Sí |Sí |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |Sí |No |
| [Opus](https://en.wikipedia.org/wiki/Opus_\(audio_format\)) |yes |No |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |Sí |No |

## <a name="output-containerfile-formats"></a>Formatos de archivo/contenedor de salida
| Formatos de archivo/contenedor de salida | Media Encoder Estándar | Flujo de trabajo del Codificador multimedia |
| --- | --- | --- |
| Adobe® Flash® F4V |No |Sí |
| MXF (OP1a, XDCAM y AS02) |No |Sí |
| DPP (incluido AS11) |No |Sí |
| GXF |No |Sí |
| MPEG-4/MP4 |Sí |Sí |
| MPEG-TS |Sí |Sí |
| Windows Media/ASF |No |Sí |
| AVI (sin comprimir de 8 bits/10 bits) |No |Sí |
| Formato de archivo de streaming con velocidad de transmisión adaptable (PIFF 1.3) |No |Sí |

## <a name="output-video-codecs"></a>Códecs de vídeo de salida
| Códecs de vídeo de salida | Media Encoder Estándar | Flujo de trabajo del Codificador multimedia |
| --- | --- | --- |
| AVC (H.264; 8 bits; una copia de seguridad tooHigh perfil, nivel 5.2; HD Ultra de 4K; Dentro de AVC) |Solo 8 bits 4:2:0 |Sí |
| Avid DNxHD (en MXF) |No |Sí |
| MPEG-2 (perfil de too422 y de alto nivel, incluido el variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® y D10) |No |Sí |
| MPEG-1 |No |Sí |
| Windows Media Video/VC-1 |No |Sí |
| Creación de miniaturas JPEG |Sí |Sí |
| Creación de miniaturas PNG |Sí |Sí |
| Creación de miniaturas BMP |Sí |No |

## <a name="output-audio-codecs"></a>Códecs de audio de salida
| Códecs de audio de salida | Media Encoder Estándar | Flujo de trabajo del Codificador multimedia |
| --- | --- | --- |
| AES (SMPTE 331M y 302M, AES3-2003) |No |Sí |
| Dolby® Digital (AC3) |No |Sí |
| Dolby® Digital Plus (E-AC3) seguridad too7.1 |No |Sí |
| AAC (AAC-LC, HE-AAC y AAC-HEv2; seguridad too5.1) |Sí |Sí |
| MPEG Layer 2 |No |Sí |
| MP3 (MPEG-1 Audio Layer 3) |No |Sí |
| Windows Media Audio |No |Sí |

>[!NOTE]
>Si codifica tooDolby® Digital (AC3), salida de hello solo se puede escribir en un archivo ISO MP4.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Artículos relacionados
* [Realización de tareas de codificación avanzadas mediante la personalización de valores preestablecidos de Media Encoder Estándar](media-services-custom-mes-presets-with-dotnet.md)
* [Cuotas y limitaciones](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
