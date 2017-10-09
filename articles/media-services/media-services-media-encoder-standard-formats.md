---
title: "códecs y formatos estándar de codificador aaaMedia"
description: "En este tema se ofrece información general sobre los códecs y formatos de Estándar de codificador multimedia."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f334b1ce-2f56-4968-a019-f0a2b0016d9f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 51a67f372dff579383ffcfa988e8f4d38ad44a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-formats-and-codecs"></a>Códecs y formatos de Media Encoder Standard
Este documento contiene una lista de importación más comunes de Hola y formatos de archivo de exportación que puede usar con Media Encoder estándar.

## <a name="input-containerfile-formats"></a>Formatos de archivo/contenedor de entrada
| Formatos de archivo (extensiones de archivo) | Compatible |
| --- | --- | --- | --- |
| FLV (con códecs H.264 y AAC) (.flv) |yes |
| MXF    (.mxf) |Sí |
| GXF    (.gxf) |Sí |
| MPEG2-PS, MPEG2-TS, 3GP (.ts, .ps, .3gp, .3gpp, .mpg) |Sí |
| Windows Media Video (WMV)/ASF (.wmv, .asf) |Sí |
| AVI (sin comprimir de 8 bits/10 bits) (.avi) |Sí |
| MP4 (.mp4, .m4a, .m4v)/ISMV (.isma, .ismv) |Sí |
| [Microsoft Digital Video Recording(DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms) |Sí |
| Matroska/WebM (.mkv) |Sí |
| WAVE/WAV (.wav) |Sí |
| QuickTime (.mov) |Sí |

> [!NOTE]
> Anteriormente es una lista de extensiones de archivo hello más habituales. El Codificador multimedia estándar admite muchos más (por ejemplo: .m2ts, .mpeg2video, .qt). Si intenta tooencode un archivo y obtener un mensaje de error sobre no se admite el formato de hello, proporcione un comentarios [aquí](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/).
> 
> 

### <a name="audio-formats-in-input-containers"></a>Formatos de audio en contenedores de entrada
Media Encoder estándar admite Hola libros siguientes formatos de audio en contenedores de entrada:

* Archivos MXF, GXF y QuickTime que tengan pistas de audio con muestras de estéreo entrelazado o 5.1 

o

* Archivos MXF, GXF y QuickTime donde se lleva a audio hello como pistas PCM independientes pero la asignación de canal de hello (toostereo o 5.1) se puede deducir de los metadatos del archivo Hola

Tenga en cuenta que admiten para asignación de canal explícita/proporcionados por el usuario se proporcionará en hello futuro próximo.

## <a name="input-video-codecs"></a>Códecs de vídeo de entrada
| Códecs de vídeo de entrada | Compatible |
| --- | --- | --- | --- |
| AVC 8/10 bits, la too4:2:2, incluidos los AVCIntra |8 bits: 4:2:0 y 4:2:2 |
| Avid DNxHD (en MXF) |Sí |
| DVCPro/DVCProHD (en MXF) |Sí |
| Vídeo digital (DV) (en archivos AVI) |Sí |
| JPEG 2000 |Sí |
| MPEG-2 (perfil de too422 y de alto nivel, incluido el variantes como XDCAM, XDCAM HD, XDCAM IMX, CableLabs® y D10) |Perfil de too422 |
| MPEG-1 |Sí |
| VC-1/WMV9 |Sí |
| Canopus HQ/HQX |No |
| MPEG-4, parte 2 |Sí |
| [Theora](https://en.wikipedia.org/wiki/Theora) |Sí |
| YUV420 sin comprimir o intermedio |Sí |
| Apple ProRes 422 |Sí |
| Apple ProRes 422 LT |Sí |
| Apple ProRes 422 HQ |Sí |
| Apple ProRes Proxy |Sí |
| Apple ProRes 4444 |Sí |
| Apple ProRes 4444 XQ |Sí |

## <a name="input-audio-codecs"></a>Códecs de audio de entrada
| Códecs de audio de entrada | Compatible |
| --- | --- | --- | --- |
| AAC (AAC-LC, HE-AAC y AAC-HEv2; seguridad too5.1) |Sí |
| MPEG Layer 2 |Sí |
| MP3 (MPEG-1 Audio Layer 3) |Sí |
| Windows Media Audio |Sí |
| WAV/PCM |Sí |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |yes |
| [Opus](http://go.microsoft.com/fwlink/?LinkId=822667) |yes |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |yes |
| AMR (velocidad múltiple adaptable) |Sí |
| AES (SMPTE 331M y 302M, AES3-2003) |No |
| Dolby® E |No |
| Dolby® Digital (AC3) |No |
| Dolby® Digital Plus (E-AC3) |No |

## <a name="output-formats-and-codecs"></a>Códecs y formatos de salida
Hello en la tabla siguiente enumera Hola códecs y formatos de archivo que se admiten para la exportación.

| Formato de archivo | Códec de vídeo | Códec de audio |
| --- | --- | --- |
| MP4  <br/><br/>(incluidos los contenedores de MP4 de velocidad de bits múltiple) |H.264 (perfil alto, perfil principal y perfil de base de línea) |AAC-LC, HE-AAC v1, HE-AAC v2 |
| MPEG2-TS |H.264 (perfil alto, perfil principal y perfil de base de línea) |AAC-LC, HE-AAC v1, HE-AAC v2 |

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Consulte también
[Codificación de contenido a petición con Servicios multimedia de Azure](media-services-encode-asset.md)

[¿Cómo tooencode con Media Encoder estándar](media-services-dotnet-encode-with-media-encoder-standard.md)

