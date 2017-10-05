---
title: "Recorte de vídeos con Media Encoder Standard - Azure | Microsoft Docs"
description: "Este artículo muestra cómo recortar vídeos con el Codificador multimedia estándar."
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
ms.openlocfilehash: 60d0ce14a271fcbe698559da95ca011cb888b221
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="02b14-103">Recorte de vídeos con Codificador multimedia estándar</span><span class="sxs-lookup"><span data-stu-id="02b14-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="02b14-104">Puede utilizar el Codificador multimedia estándar (MES) para recortar el vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="02b14-104">You can use Media Encoder Standard (MES) to crop your input video.</span></span> <span data-ttu-id="02b14-105">Recortar es el proceso que consiste en la selección de una ventana rectangular en el fotograma de vídeo y la codificación solo de los píxeles que están dentro de esa ventana.</span><span class="sxs-lookup"><span data-stu-id="02b14-105">Cropping is the process of selecting a rectangular window within the video frame, and encoding just the pixels within that window.</span></span> <span data-ttu-id="02b14-106">El diagrama siguiente puede ayudarle a ilustrar el proceso.</span><span class="sxs-lookup"><span data-stu-id="02b14-106">The following diagram helps illustrate the process.</span></span>

![Recortar un vídeo](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="02b14-108">Suponga que tiene como entrada un vídeo con una resolución de 1920 x 1080 píxeles (relación de aspecto 16:9), pero que tiene barras negras (formato pillarbox) a izquierda y derecha, por lo que sólo una ventana de 4:3 o 1440 x 1080 píxeles contiene vídeo activo.</span><span class="sxs-lookup"><span data-stu-id="02b14-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at the left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="02b14-109">Puede usar el MES para recortar o editar las barras negras y codificar la región de 1440 x 1080 píxeles.</span><span class="sxs-lookup"><span data-stu-id="02b14-109">You can use MES to crop or edit out the black bars, and encode the 1440x1080 region.</span></span>

<span data-ttu-id="02b14-110">Recortar en MES es una fase previa al procesamiento, por ello, los parámetros de recorte del valor predeterminado de codificación se aplican al vídeo de entrada original.</span><span class="sxs-lookup"><span data-stu-id="02b14-110">Cropping in MES is a pre-processing stage, so the cropping parameters in the encoding preset apply to the original input video.</span></span> <span data-ttu-id="02b14-111">La codificación es una fase posterior y los valores de anchura y altura se aplicarán al vídeo *previamente procesado* y no al vídeo original.</span><span class="sxs-lookup"><span data-stu-id="02b14-111">Encoding is a subsequent stage, and the width/height settings apply to the *pre-processed* video, and not to the original video.</span></span> <span data-ttu-id="02b14-112">Al diseñar el valor predeterminado debe hacer lo siguiente: (a) seleccione los parámetros de recorte basándose en el vídeo de entrada original y (b), seleccione la configuración de codificación basándose en el vídeo recortado.</span><span class="sxs-lookup"><span data-stu-id="02b14-112">When designing your preset you need to do the following: (a) select the crop parameters based on the original input video, and (b) select your encode settings based on the cropped video.</span></span> <span data-ttu-id="02b14-113">Si no coincide la configuración de la codificación con el vídeo recortado, el resultado no será el esperado.</span><span class="sxs-lookup"><span data-stu-id="02b14-113">If you do not match your encode settings to the cropped video, the output will not be as you expect.</span></span>

<span data-ttu-id="02b14-114">El [siguiente](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tema muestra cómo crear un trabajo de codificación con el MES y cómo especificar un valor predeterminado personalizado para la tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="02b14-114">The [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how to create an encoding job with MES and how to specify a custom preset for the encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="02b14-115">Creación de un valor predeterminado personalizado</span><span class="sxs-lookup"><span data-stu-id="02b14-115">Creating a custom preset</span></span>
<span data-ttu-id="02b14-116">En el ejemplo que aparece en el diagrama:</span><span class="sxs-lookup"><span data-stu-id="02b14-116">In the example shown in the diagram:</span></span>

1. <span data-ttu-id="02b14-117">La entrada original es 1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="02b14-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="02b14-118">Debe recortarse a una salida de 1440 x 1080, centrada en el marco de entrada</span><span class="sxs-lookup"><span data-stu-id="02b14-118">It needs to be cropped to an output of 1440x1080, which is centered in the input frame</span></span>
3. <span data-ttu-id="02b14-119">Esto significa un desplazamiento X (1920 – 1440) / 2 = 240 y un desplazamiento Y de cero</span><span class="sxs-lookup"><span data-stu-id="02b14-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="02b14-120">La anchura y altura del rectángulo de recorte son 1440 y 1080, respectivamente</span><span class="sxs-lookup"><span data-stu-id="02b14-120">The Width and Height of the Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="02b14-121">En la fase de codificación, la ASK producirá tres capas, con resoluciones de 1440 x 1080, 960 x 720 y 480 x 360, respectivamente</span><span class="sxs-lookup"><span data-stu-id="02b14-121">In the encode stage, the ask is to produce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="02b14-122">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="02b14-122">JSON preset</span></span>
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="02b14-123">Restricciones en el recorte</span><span class="sxs-lookup"><span data-stu-id="02b14-123">Restrictions on cropping</span></span>
<span data-ttu-id="02b14-124">La función de recorte está pensada para ser manual.</span><span class="sxs-lookup"><span data-stu-id="02b14-124">The cropping feature is meant to be manual.</span></span> <span data-ttu-id="02b14-125">Debe cargar el vídeo de entrada en una herramienta de edición apropiada que le permita seleccionar los fotogramas de interés, colocar el cursor para determinar los desplazamientos del rectángulo de recorte y determinar el valor predeterminado de codificación que se ajusta a ese determinado vídeo, etc. Esta característica no está pensada para habilitar cosas como: detección automática y eliminación de bordes negros en formato letterbox o pillarbox en el vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="02b14-125">You would need to load your input video into a suitable editing tool that lets you select frames of interest, position the cursor to determine offsets for the cropping rectangle, to determine the encoding preset that is tuned for that particular video, etc. This feature is not meant to enable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="02b14-126">Se aplican las siguientes restricciones a la característica de recorte.</span><span class="sxs-lookup"><span data-stu-id="02b14-126">Following constraints apply to the cropping feature.</span></span> <span data-ttu-id="02b14-127">Si estos no se cumplen, la tarea de codificación puede producir un error o generar una salida inesperada.</span><span class="sxs-lookup"><span data-stu-id="02b14-127">If these are not met, the encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="02b14-128">Las coordenadas y el tamaño del rectángulo de recorte deben ajustarse al vídeo de entrada</span><span class="sxs-lookup"><span data-stu-id="02b14-128">The co-ordinates and size of the Crop rectangle have to fit within the input video</span></span>
2. <span data-ttu-id="02b14-129">Como se mencionó anteriormente, la anchura y altura de la configuración de codificación se tienen que corresponder con el vídeo recortado</span><span class="sxs-lookup"><span data-stu-id="02b14-129">As mentioned above, the Width & Height in the encode settings have to correspond to the cropped video</span></span>
3. <span data-ttu-id="02b14-130">El recorte se aplica a vídeos capturados en modo horizontal (es decir, no es aplicable a los vídeos grabados con un smartphone sujeto verticalmente o en modo vertical)</span><span class="sxs-lookup"><span data-stu-id="02b14-130">Cropping applies to videos captured in landscape mode (i.e. not applicable to videos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="02b14-131">Funciona mejor con vídeo progresivo capturado con píxeles cuadrados</span><span class="sxs-lookup"><span data-stu-id="02b14-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="02b14-132">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="02b14-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="02b14-133">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="02b14-133">Next step</span></span>
<span data-ttu-id="02b14-134">Consulte las rutas de aprendizaje de los Servicios multimedia de Azure para conocer las magníficas características ofrecidas por AMS.</span><span class="sxs-lookup"><span data-stu-id="02b14-134">See Azure Media Services learning paths to help you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
