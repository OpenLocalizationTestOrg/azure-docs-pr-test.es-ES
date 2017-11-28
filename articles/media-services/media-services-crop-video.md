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
# <a name="crop-videos-with-media-encoder-standard"></a><span data-ttu-id="038d2-103">Recorte de vídeos con Codificador multimedia estándar</span><span class="sxs-lookup"><span data-stu-id="038d2-103">Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="038d2-104">Puede utilizar medios codificador estándar (MES) toocrop la entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="038d2-104">You can use Media Encoder Standard (MES) toocrop your input video.</span></span> <span data-ttu-id="038d2-105">Recortar es el proceso de Hola para seleccionar una ventana rectangular en fotogramas de vídeo de Hola y codificación simplemente píxeles de hello dentro de esa ventana.</span><span class="sxs-lookup"><span data-stu-id="038d2-105">Cropping is hello process of selecting a rectangular window within hello video frame, and encoding just hello pixels within that window.</span></span> <span data-ttu-id="038d2-106">Hola después de diagrama le ayuda a ilustrar el proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="038d2-106">hello following diagram helps illustrate hello process.</span></span>

![Recortar un vídeo](./media/media-services-crop-video/media-services-crop-video01.png)

<span data-ttu-id="038d2-108">Imagine que tiene como entrada un vídeo que tenga una resolución de 1920 x 1080 píxeles (relación de aspecto 16:9), pero tiene barras de color negro (pillar cuadros) en hello izquierdo y derecho, por lo que solo una ventana de 4:3 o 1440 x 1080 píxeles contiene vídeo active.</span><span class="sxs-lookup"><span data-stu-id="038d2-108">Suppose you have as input a video that has a resolution of 1920x1080 pixels (16:9 aspect ratio), but has black bars (pillar boxes) at hello left and right, so that only a 4:3 window or 1440x1080 pixels contains active video.</span></span> <span data-ttu-id="038d2-109">Puede usar toocrop MES o editar out barras Hola negro y codificar la región de 1440 x 1080 Hola.</span><span class="sxs-lookup"><span data-stu-id="038d2-109">You can use MES toocrop or edit out hello black bars, and encode hello 1440x1080 region.</span></span>

<span data-ttu-id="038d2-110">Recortar en MES es una fase previa al procesamiento, por lo que aplican los parámetros de recorte de hello en el valor predeterminado de codificación de hello toohello vídeo de entrada original.</span><span class="sxs-lookup"><span data-stu-id="038d2-110">Cropping in MES is a pre-processing stage, so hello cropping parameters in hello encoding preset apply toohello original input video.</span></span> <span data-ttu-id="038d2-111">La codificación es una fase posterior, y configuración de ancho/alto de Hola aplica toohello *preprocesa* vídeo y no toohello de vídeo original.</span><span class="sxs-lookup"><span data-stu-id="038d2-111">Encoding is a subsequent stage, and hello width/height settings apply toohello *pre-processed* video, and not toohello original video.</span></span> <span data-ttu-id="038d2-112">Al diseñar sus valores preestablecidos necesita toodo Hola siguiente: (a) seleccione parámetros de recorte de hello basados en vídeo de entrada original de Hola y (b), seleccione su codificar la configuración en función de hello recortada vídeo.</span><span class="sxs-lookup"><span data-stu-id="038d2-112">When designing your preset you need toodo hello following: (a) select hello crop parameters based on hello original input video, and (b) select your encode settings based on hello cropped video.</span></span> <span data-ttu-id="038d2-113">Si no coinciden los codificar toohello configuración recorta el vídeo, la salida de hello no será tal como se esperaba.</span><span class="sxs-lookup"><span data-stu-id="038d2-113">If you do not match your encode settings toohello cropped video, hello output will not be as you expect.</span></span>

<span data-ttu-id="038d2-114">Hola [siguiente](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tema muestra cómo toocreate un trabajo de codificación con el MES y cómo toospecify personalizado preestablecido para Hola tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="038d2-114">hello [following](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic shows how toocreate an encoding job with MES and how toospecify a custom preset for hello encoding task.</span></span> 

## <a name="creating-a-custom-preset"></a><span data-ttu-id="038d2-115">Creación de un valor predeterminado personalizado</span><span class="sxs-lookup"><span data-stu-id="038d2-115">Creating a custom preset</span></span>
<span data-ttu-id="038d2-116">En el ejemplo de Hola que se muestra en el diagrama de hello:</span><span class="sxs-lookup"><span data-stu-id="038d2-116">In hello example shown in hello diagram:</span></span>

1. <span data-ttu-id="038d2-117">La entrada original es 1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="038d2-117">Original input is 1920x1080</span></span>
2. <span data-ttu-id="038d2-118">Necesita toobe recorta tooan salida de 1440 x 1080, que se centra en el marco de entrada de Hola</span><span class="sxs-lookup"><span data-stu-id="038d2-118">It needs toobe cropped tooan output of 1440x1080, which is centered in hello input frame</span></span>
3. <span data-ttu-id="038d2-119">Esto significa un desplazamiento X (1920 – 1440) / 2 = 240 y un desplazamiento Y de cero</span><span class="sxs-lookup"><span data-stu-id="038d2-119">This means an X offset of (1920 – 1440)/2 = 240, and a Y offset of zero</span></span>
4. <span data-ttu-id="038d2-120">Hola ancho y alto del rectángulo de recorte de hello son 1440 y 1080, respectivamente</span><span class="sxs-lookup"><span data-stu-id="038d2-120">hello Width and Height of hello Crop rectangle are 1440 and 1080, respectively</span></span>
5. <span data-ttu-id="038d2-121">Hola fase de codificación, hello solicitar es tooproduce tres capas, son resoluciones 1440 x 1080, 960 x 720 y 480 x 360, respectivamente</span><span class="sxs-lookup"><span data-stu-id="038d2-121">In hello encode stage, hello ask is tooproduce three layers, are resolutions 1440x1080, 960x720 and 480x360, respectively</span></span>

### <a name="json-preset"></a><span data-ttu-id="038d2-122">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="038d2-122">JSON preset</span></span>
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


## <a name="restrictions-on-cropping"></a><span data-ttu-id="038d2-123">Restricciones en el recorte</span><span class="sxs-lookup"><span data-stu-id="038d2-123">Restrictions on cropping</span></span>
<span data-ttu-id="038d2-124">el objetivo de Hello recortar característica es toobe manual.</span><span class="sxs-lookup"><span data-stu-id="038d2-124">hello cropping feature is meant toobe manual.</span></span> <span data-ttu-id="038d2-125">Deberá tooload la entrada de vídeo en una herramienta de edición adecuada que permite seleccionar las tramas de interés, coloque Hola cursor toodetermine desplazamientos para recortar el rectángulo de hello, toodetermine Hola valor preestablecido de codificación que se ajusta para que ese etcetera de vídeo determinado. Esta característica no se pretende tooenable cosas como: la detección automática y eliminación de bordes negros panorámica/pantalla normal en la entrada de vídeo.</span><span class="sxs-lookup"><span data-stu-id="038d2-125">You would need tooload your input video into a suitable editing tool that lets you select frames of interest, position hello cursor toodetermine offsets for hello cropping rectangle, toodetermine hello encoding preset that is tuned for that particular video, etc. This feature is not meant tooenable things like: automatic detection and removal of black letterbox/pillarbox borders in your input video.</span></span>

<span data-ttu-id="038d2-126">Las restricciones siguientes aplican toohello recortar la característica.</span><span class="sxs-lookup"><span data-stu-id="038d2-126">Following constraints apply toohello cropping feature.</span></span> <span data-ttu-id="038d2-127">Si no se cumplen estas, Hola codificar tareas pueden producir errores o generar un resultado inesperado.</span><span class="sxs-lookup"><span data-stu-id="038d2-127">If these are not met, hello encode Task can fail, or produce an unexpected output.</span></span>

1. <span data-ttu-id="038d2-128">Hello las coordenadas y el tamaño del rectángulo de recorte de hello tienen toofit dentro de vídeo de entrada de Hola</span><span class="sxs-lookup"><span data-stu-id="038d2-128">hello co-ordinates and size of hello Crop rectangle have toofit within hello input video</span></span>
2. <span data-ttu-id="038d2-129">Como se mencionó anteriormente, Hola ancho y alto en hello codifican valores tienen toohello toocorrespond recorta vídeo</span><span class="sxs-lookup"><span data-stu-id="038d2-129">As mentioned above, hello Width & Height in hello encode settings have toocorrespond toohello cropped video</span></span>
3. <span data-ttu-id="038d2-130">Recortar aplica toovideos capturada en modo horizontal (es decir, no es aplicable toovideos registrados con un smartphone mantenida verticalmente o en modo vertical)</span><span class="sxs-lookup"><span data-stu-id="038d2-130">Cropping applies toovideos captured in landscape mode (i.e. not applicable toovideos recorded with a smartphone held vertically or in portrait mode)</span></span>
4. <span data-ttu-id="038d2-131">Funciona mejor con vídeo progresivo capturado con píxeles cuadrados</span><span class="sxs-lookup"><span data-stu-id="038d2-131">Works best with progressive video captured with square pixels</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="038d2-132">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="038d2-132">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-step"></a><span data-ttu-id="038d2-133">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="038d2-133">Next step</span></span>
<span data-ttu-id="038d2-134">Vea servicios de multimedia de Azure toohelp de rutas de acceso que conozcas excelentes características que ofrece AMS de aprendizaje.</span><span class="sxs-lookup"><span data-stu-id="038d2-134">See Azure Media Services learning paths toohelp you learn about great features offered by AMS.</span></span>  

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]
