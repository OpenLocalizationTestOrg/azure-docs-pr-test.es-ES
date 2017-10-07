---
title: "valores preestablecidos de aaaTask de MES (Media Encoder estándar) | Documentos de Microsoft"
description: "Hola tema proporciona y visión general de valores preestablecidos de tarea para el MES (Media Encoder estándar)."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f243ed1c-ac9c-4300-a5f7-f092cf9853b9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 56e098d6d8c8f84031421ec59f087f20370ba111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="task-presets-for-mes-media-encoder-standard"></a>Valores preestablecidos de las tareas de MES (Media Encoder Standard)

**Media Encoder Standard** define un conjunto de valores predeterminados de Encoding que puede usar al crear trabajos de Encoding. Se recomienda hello toouse "Transmisión por secuencias adaptativa" preestablecido si desea tooencode un vídeo para streaming con servicios multimedia. Cuando se especifica este valor preestablecido, Media Encoder Standard [generará automáticamente una escalera de velocidad de bits](media-services-autogen-bitrate-ladder-with-mes.md). 

Sin embargo, si tiene un valor predeterminado de codificación de toocustomize, debe realizar una de hello codificación valores preestablecidos definidos en esta sección como plantilla para la configuración personalizada. Para obtener una explicación de cada elemento de qué en estos medios de valores predefinidos y los valores válidos de Hola para cada elemento, vea hello [Media Encoder estándar esquema](media-services-mes-schema.md) tema.  
  
> [!NOTE]
>  Cuando se usa un valor preestablecido para codifica de 4k, debería obtener hello `S3` reservado del tipo de unidad. Para obtener más información, consulte [cómo tooScale codificación](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).  
  
Cuando se trabaja con Media Encoder Standard, la rotación está habilitada de forma predeterminada. Si se ha registrado el vídeo en un smartphone u otro dispositivo móvil en modo vertical, a continuación, estos valores, de forma predeterminada, girará ellos tooLandscape modo anterior tooencoding (a diferencia de, al trabajar con el Codificador multimedia de Azure, donde la rotación de vídeo es una operación manual, como se documenta en [esto](http://azure.microsoft.com/blog/2014/08/21/advanced-encoding-features-in-azure-media-encoder/) blog, junto a "Vídeo giro").  
  
Valores predefinidos disponibles:  
  
 [Velocidad de bits múltiple H264 1080p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-1080p-Audio-5.1.md) produce un conjunto de 8 archivos MP4 alineados con GOP, que abarcan de 6000 kbps too400 kbps y audio AAC 5.1.  
  
 [Velocidad de bits múltiple del H264 1080p](media-services-mes-preset-H264-Multiple-Bitrate-1080p.md) produce un conjunto de 8 archivos MP4 alineados con GOP, que abarcan de 6000 kbps too400 kbps y audio AAC estéreo.  
  
 [H264 varias velocidades de bits 16 x 9 para iOS](media-services-mes-preset-H264-Multiple-Bitrate-16x9-for-iOS.md) produce un conjunto de 8 archivos MP4 alineados con GOP, comprendido entre 8500 kbps too200 kbps y audio AAC estéreo.  
  
 [Velocidad de bits múltiple del H264 16 x 9 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD-Audio-5.1.md) produce un conjunto de 5 archivos MP4 alineados con GOP, comprendida entre 1900 kbps too400 kbps y audio AAC 5.1.  
  
 [Velocidad de bits múltiple del H264 16 x 9 SD](media-services-mes-preset-H264-Multiple-Bitrate-16x9-SD.md) produce un conjunto de 5 archivos MP4 alineados con GOP, comprendida entre 1900 kbps too400 kbps y audio AAC estéreo.  
  
 [Velocidad de bits múltiple del H264 4K Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4K-Audio-5.1.md) genera un conjunto de 12 archivos MP4 alineados con GOP, comprendido entre 20000 kbps too1000 kbps y audio AAC 5.1.  
  
 [Velocidad de bits múltiple del H264 4K](media-services-mes-preset-H264-Multiple-Bitrate-4K.md) genera un conjunto de 12 archivos MP4 alineados con GOP, comprendido entre 20000 kbps too1000 kbps y audio AAC estéreo.  
  
 [H264 varias velocidades de bits 4 x 3 para iOS](media-services-mes-preset-H264-Multiple-Bitrate-4x3-for-iOS.md) produce un conjunto de 8 archivos MP4 alineados con GOP, comprendido entre 8500 kbps too200 kbps y audio AAC estéreo.  
  
 [Velocidad de bits múltiple del H264 4 x 3 SD Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD-Audio-5.1.md) produce un conjunto de 5 archivos MP4 alineados con GOP, comprendido entre 1600 kbps too400 kbps y audio AAC 5.1.  
  
 [Velocidad de bits múltiple del H264 4 x 3 SD](media-services-mes-preset-H264-Multiple-Bitrate-4x3-SD.md) produce un conjunto de 5 archivos MP4 alineados con GOP, comprendido entre 1600 kbps too400 kbps y audio AAC estéreo.  
  
 [Velocidad de bits múltiple H264 720p Audio 5.1](media-services-mes-preset-H264-Multiple-Bitrate-720p-Audio-5.1.md) genera un conjunto de 6 archivos MP4 alineados con GOP, que abarcan de 3400 kbps too400 kbps y audio AAC 5.1.  
  
 [H264 varias velocidades de bits 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) genera un conjunto de 6 archivos MP4 alineados con GOP, que abarcan de 3400 kbps too400 kbps y audio AAC estéreo.  
  
 [H264 Single Bitrate 1080p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-1080p-Audio-5.1.md) genera un único archivo MP4 con una velocidad de bits de 6750 kbps y audio AAC 5.1.  
  
 [H264 Single Bitrate 1080p](media-services-mes-preset-H264-Single-Bitrate-1080p.md) genera un único archivo MP4 con una velocidad de bits de 6750 kbps y audio AAC estéreo.  
  
 [H264 Single Bitrate 4K Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4K-Audio-5.1.md) genera un único archivo MP4 con una velocidad de bits de 18 000 kbps y audio AAC 5.1.  
  
 [H264 Single Bitrate 4K](media-services-mes-preset-H264-Single-Bitrate-4K.md) genera un único archivo MP4 con una velocidad de bits de 18 000 kbps y audio AAC estéreo.  
  
 [H264 Single Bitrate 4x3 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-4x3-SD-Audio-5.1.md) genera un único archivo MP4 con una velocidad de bits de 1800 kbps y audio AAC 5.1.  
  
 [H264 Single Bitrate 4x3 SD](media-services-mes-preset-H264-Single-Bitrate-4x3-SD.md) genera un único archivo MP4 con una velocidad de bits de 1800 kbps y audio AAC estéreo.  
  
 [H264 Single Bitrate 16x9 SD Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-16x9-SD-Audio-5.1.md) genera un único archivo MP4 con una velocidad de bits de 2200 kbps y audio AAC 5.1.  
  
 [H264 Single Bitrate 16x9 SD](media-services-mes-preset-H264-Single-Bitrate-16x9-SD.md) genera un único archivo MP4 con una velocidad de bits de 2200 kbps y audio AAC estéreo.  
  
 [H264 Single Bitrate 720p Audio 5.1](media-services-mes-preset-H264-Single-Bitrate-720p-Audio-5.1.md) genera un único archivo MP4 con una velocidad de bits de 4500 kbps y audio AAC 5.1.  
  
 [H264 Single Bitrate 720p for Android](media-services-mes-preset-H264-Single-Bitrate-720p-for-Android.md) genera un único archivo MP4 con una velocidad de bits de 2000 kbps y audio AAC estéreo.  
  
 [H264 Single Bitrate 720p](media-services-mes-preset-H264-Single-Bitrate-720p.md) genera un único archivo MP4 con una velocidad de bits de 4500 kbps y audio AAC estéreo.  
  
 [H264 Single Bitrate High Quality SD for Android](media-services-mes-preset-H264-Single-Bitrate-High-Quality-SD-for-Android.md) genera un único archivo MP4 con una velocidad de bits de 500 kbps y audio AAC estéreo.  
  
 [H264 Single Bitrate Low Quality SD for Android](media-services-mes-preset-H264-Single-Bitrate-Low-Quality-SD-for-Android.md) genera un único archivo MP4 con una velocidad de bits de 56 kbps y audio AAC estéreo.  
  
 Para obtener más información vea codificadores de servicios relacionados tooMedia, [codificación a petición con servicios multimedia de Azure](https://azure.microsoft.com/en-us/documentation/articles/media-services-encode-asset/).
