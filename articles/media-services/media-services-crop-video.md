---
title: "aaaHow toocrop vídeos con Media Encoder Standard - Azure | Documentos de Microsoft"
description: "Este artículo se muestra cómo toocrop vídeos con Media Encoder estándar."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 7628f674-2005-4531-8b61-d7a4f53e46ba
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/09/2017
ms.author: anilmur;juliako;
ms.openlocfilehash: 2b4ac3d96228b93c890a38c57c4913988de1e8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a>Recorte de vídeos con Codificador multimedia estándar
Puede utilizar medios codificador estándar (MES) toocrop la entrada de vídeo. Recortar es el proceso de Hola para seleccionar una ventana rectangular en fotogramas de vídeo de Hola y codificación simplemente píxeles de hello dentro de esa ventana. Hola después de diagrama le ayuda a ilustrar el proceso de Hola.

![Recortar un vídeo](./media/media-services-crop-video/media-services-crop-video01.png)

Imagine que tiene como entrada un vídeo que tenga una resolución de 1920 x 1080 píxeles (relación de aspecto 16:9), pero tiene barras de color negro (pillar cuadros) en hello izquierdo y derecho, por lo que solo una ventana de 4:3 o 1440 x 1080 píxeles contiene vídeo active. Puede usar toocrop MES o editar out barras Hola negro y codificar la región de 1440 x 1080 Hola.

Recortar en MES es una fase previa al procesamiento, por lo que aplican los parámetros de recorte de hello en el valor predeterminado de codificación de hello toohello vídeo de entrada original. La codificación es una fase posterior, y configuración de ancho/alto de Hola aplica toohello *preprocesa* vídeo y no toohello de vídeo original. Al diseñar sus valores preestablecidos necesita toodo Hola siguiente: (a) seleccione parámetros de recorte de hello basados en vídeo de entrada original de Hola y (b), seleccione su codificar la configuración en función de hello recortada vídeo. Si no coinciden los codificar toohello configuración recorta el vídeo, la salida de hello no será tal como se esperaba.

Hola [siguiente](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tema muestra cómo toocreate un trabajo de codificación con el MES y cómo toospecify personalizado preestablecido para Hola tarea de codificación. 

## <a name="creating-a-custom-preset"></a>Creación de un valor predeterminado personalizado
En el ejemplo de Hola que se muestra en el diagrama de hello:

1. La entrada original es 1920 x 1080
2. Necesita toobe recorta tooan salida de 1440 x 1080, que se centra en el marco de entrada de Hola
3. Esto significa un desplazamiento X (1920 – 1440) / 2 = 240 y un desplazamiento Y de cero
4. Hola ancho y alto del rectángulo de recorte de hello son 1440 y 1080, respectivamente
5. Hola fase de codificación, hello solicitar es tooproduce tres capas, son resoluciones 1440 x 1080, 960 x 720 y 480 x 360, respectivamente

### <a name="json-preset"></a>Valor preestablecido JSON
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "Crop": {
                "X": 240,
                "Y": 0,
                "Width": 1440,
                "Height": 1080
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1440,
              "Height": 1080,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1250,
              "MaxBitrate": 1250,
              "BufferWindow": "00:00:05",
              "Width": 480,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


## <a name="restrictions-on-cropping"></a>Restricciones en el recorte
el objetivo de Hello recortar característica es toobe manual. Deberá tooload la entrada de vídeo en una herramienta de edición adecuada que permite seleccionar las tramas de interés, coloque Hola cursor toodetermine desplazamientos para recortar el rectángulo de hello, toodetermine Hola valor preestablecido de codificación que se ajusta para que ese etcetera de vídeo determinado. Esta característica no se pretende tooenable cosas como: la detección automática y eliminación de bordes negros panorámica/pantalla normal en la entrada de vídeo.

Las restricciones siguientes aplican toohello recortar la característica. Si no se cumplen estas, Hola codificar tareas pueden producir errores o generar un resultado inesperado.

1. Hello las coordenadas y el tamaño del rectángulo de recorte de hello tienen toofit dentro de vídeo de entrada de Hola
2. Como se mencionó anteriormente, Hola ancho y alto en hello codifican valores tienen toohello toocorrespond recorta vídeo
3. Recortar aplica toovideos capturada en modo horizontal (es decir, no es aplicable toovideos registrados con un smartphone mantenida verticalmente o en modo vertical)
4. Funciona mejor con vídeo progresivo capturado con píxeles cuadrados

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a>Paso siguiente
Vea servicios de multimedia de Azure toohelp de rutas de acceso que conozcas excelentes características que ofrece AMS de aprendizaje.  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
