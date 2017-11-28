---
title: "aaaPerform avanzado de codificación mediante la personalización de valores preestablecidos MES | Documentos de Microsoft"
description: "Este tema muestra cómo tooperform avanzado de codificación mediante la personalización de Media Encoder estándar de valores preestablecidos de tarea."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="406c9-103">Codificación avanzada mediante la personalización de valores preestablecidos de MES</span><span class="sxs-lookup"><span data-stu-id="406c9-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="406c9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="406c9-104">Overview</span></span>

<span data-ttu-id="406c9-105">Este tema muestra cómo se configura toocustomize Media Encoder estándar.</span><span class="sxs-lookup"><span data-stu-id="406c9-105">This topic shows how toocustomize Media Encoder Standard presets.</span></span> <span data-ttu-id="406c9-106">Hola [codificación con Media Encoder estándar con valores preestablecidos personalizados](media-services-custom-mes-presets-with-dotnet.md) tema muestra cómo toouse .NET toocreate una codificación de tareas y un trabajo que se ejecuta esta tarea.</span><span class="sxs-lookup"><span data-stu-id="406c9-106">hello [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how toouse .NET toocreate an encoding task and a job that executes this task.</span></span> <span data-ttu-id="406c9-107">Después de personalizar un ajuste preestablecido, tarea de codificación de toohello de alimentación Hola valores preestablecidos personalizados.</span><span class="sxs-lookup"><span data-stu-id="406c9-107">Once you customize a preset, supply hello custom presets toohello encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="406c9-108">Si utiliza un ajuste preestablecido XML, asegúrese de seguro orden de Hola de toopreserve de elementos, como se muestra en los siguientes ejemplos XML (por ejemplo, KeyFrameInterval debe preceder SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="406c9-108">If using an XML preset, make sure toopreserve hello order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="406c9-109">En este tema, se muestran los valores preestablecidos personalizados Hola que llevan a cabo Hola después de tareas de codificación.</span><span class="sxs-lookup"><span data-stu-id="406c9-109">In this topic, hello custom presets that perform hello following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="406c9-110">Compatibilidad con tamaños relativos</span><span class="sxs-lookup"><span data-stu-id="406c9-110">Support for relative sizes</span></span>

<span data-ttu-id="406c9-111">Si desea generar vistas en miniatura, no es necesario tooalways especificar ancho de salida y el alto en píxeles.</span><span class="sxs-lookup"><span data-stu-id="406c9-111">When generating thumbnails, you do not need tooalways specify output width and height in pixels.</span></span> <span data-ttu-id="406c9-112">Puede especificar las credenciales en porcentajes, en el intervalo de hello [% 1, …, 100%].</span><span class="sxs-lookup"><span data-stu-id="406c9-112">You can specify them in percentages, in hello range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="406c9-113">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="406c9-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="406c9-114">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="406c9-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="406c9-115"><a id="thumbnails"></a>Generación de miniaturas</span><span class="sxs-lookup"><span data-stu-id="406c9-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="406c9-116">Esta sección se muestra cómo toocustomize un ajuste preestablecido que genera las miniaturas.</span><span class="sxs-lookup"><span data-stu-id="406c9-116">This section shows how toocustomize a preset that generates thumbnails.</span></span> <span data-ttu-id="406c9-117">Hello valor preestablecido definida a continuación contiene información sobre cómo desea que tooencode el archivo, así como información necesaria toogenerate miniaturas.</span><span class="sxs-lookup"><span data-stu-id="406c9-117">hello preset defined below contains information on how you want tooencode your file as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="406c9-118">Puede realizar cualquiera de valores preestablecidos MES de hello documentados [esto](media-services-mes-presets-overview.md) sección y agregue código que genera las miniaturas.</span><span class="sxs-lookup"><span data-stu-id="406c9-118">You can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="406c9-119">Hola **SceneChangeDetection** configuración Hola después preestablecido solo puede establecerse tootrue si va a codificar vídeo de velocidad de bits única tooa.</span><span class="sxs-lookup"><span data-stu-id="406c9-119">hello **SceneChangeDetection** setting in hello following preset can only be set tootrue if you are encoding tooa single  bitrate video.</span></span> <span data-ttu-id="406c9-120">Si va a codificar tooa velocidades de bits vídeo y establecer **SceneChangeDetection** tootrue, el codificador de hello devuelve un error.</span><span class="sxs-lookup"><span data-stu-id="406c9-120">If you are encoding tooa multi-bitrate video and set **SceneChangeDetection** tootrue, hello encoder returns an error.</span></span>  
>
>

<span data-ttu-id="406c9-121">Para obtener información sobre el esquema, consulte [este](media-services-mes-schema.md) tema.</span><span class="sxs-lookup"><span data-stu-id="406c9-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="406c9-122">Realizar seguro hello tooreview [consideraciones](#considerations) sección.</span><span class="sxs-lookup"><span data-stu-id="406c9-122">Make sure tooreview hello [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="406c9-123"><a id="json"></a>Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="406c9-123"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <span data-ttu-id="406c9-124"><a id="xml"></a>Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="406c9-124"><a id="xml"></a>XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="406c9-125">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="406c9-125">Considerations</span></span>

<span data-ttu-id="406c9-126">Hola siguientes consideraciones se aplica:</span><span class="sxs-lookup"><span data-stu-id="406c9-126">hello following considerations apply:</span></span>

* <span data-ttu-id="406c9-127">uso de Hola de marcas de tiempo explícito para el inicio/paso/intervalo supone que ese origen de entrada de hello es larga de 1 minuto como mínimo.</span><span class="sxs-lookup"><span data-stu-id="406c9-127">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="406c9-128">Los elementos Jpg/Png/BmpImage tienen atributos de cadena Start, Step y Range, que se pueden interpretar como:</span><span class="sxs-lookup"><span data-stu-id="406c9-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="406c9-129">Número de marco si son enteros no negativos, por ejemplo, Start: 120</span><span class="sxs-lookup"><span data-stu-id="406c9-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="406c9-130">Duración de toosource relativa si expresado como sufijo de %, por ejemplo "Start": "el 15%", o</span><span class="sxs-lookup"><span data-stu-id="406c9-130">Relative toosource duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="406c9-131">Marca de tiempo si se</span><span class="sxs-lookup"><span data-stu-id="406c9-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="406c9-132">por ejemplo, "Start" : "00:01:00"</span><span class="sxs-lookup"><span data-stu-id="406c9-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="406c9-133">Puede mezclar y hacer coincidir notaciones a su conveniencia.</span><span class="sxs-lookup"><span data-stu-id="406c9-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="406c9-134">Además, inicio también admite una Macro especial: {recomendados}, que intenta toodetermine Hola primer "interesante" marco de contenido de hello Nota: (paso y el intervalo se omiten al inicio se establece demasiado {mejor})</span><span class="sxs-lookup"><span data-stu-id="406c9-134">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="406c9-135">Valores predeterminados: Start:{Best}</span><span class="sxs-lookup"><span data-stu-id="406c9-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="406c9-136">Formato de salida debe toobe indicado de forma explícita para cada formato de imagen: Jpg o Png/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="406c9-136">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="406c9-137">Cuando está presente, MES coincide con la JpgVideo tooJpgFormat y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="406c9-137">When present, MES matches JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="406c9-138">OutputFormat presenta una nueva Macro específica de códecs de imagen: {Index}, que necesita toobe presente (una vez y solo una vez) para formatos de salida de imagen.</span><span class="sxs-lookup"><span data-stu-id="406c9-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="406c9-139"><a id="trim_video"></a>Recorte de un vídeo</span><span class="sxs-lookup"><span data-stu-id="406c9-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="406c9-140">Este conferencias de la sección acerca de cómo modificar el codificador de hello presintonías tooclip o recortar el vídeo de entrada de Hola donde hello entrada es un archivo mezzanine denominadas o a petición.</span><span class="sxs-lookup"><span data-stu-id="406c9-140">This section talks about modifying hello encoder presets tooclip or trim hello input video where hello input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="406c9-141">Hello codificador puede también tooclip usado o un activo, que es capturado o archivado desde una secuencia en directo de recorte: Hola detalles para este están disponibles en [este blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="406c9-141">hello encoder can also be used tooclip or trim an asset, which is captured or archived from a live stream – hello details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="406c9-142">tootrim sus vídeos, puede realizar cualquiera de valores preestablecidos MES de hello documentados [esto](media-services-mes-presets-overview.md) sección y modificar hello **orígenes** elemento (tal y como se muestra a continuación).</span><span class="sxs-lookup"><span data-stu-id="406c9-142">tootrim your videos, you can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and modify hello **Sources** element (as shown below).</span></span> <span data-ttu-id="406c9-143">valor de Hola de StartTime debe toomatch Hola absoluta las marcas de tiempo de vídeo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="406c9-143">hello value of StartTime needs toomatch hello absolute timestamps of hello input video.</span></span> <span data-ttu-id="406c9-144">Por ejemplo, si hello primer fotograma de vídeo de entrada de hello tiene una marca de tiempo de 12:00:10.000, StartTime debe tener al menos 12:00:10.000 y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="406c9-144">For example, if hello first frame of hello input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="406c9-145">En el ejemplo de Hola siguiente, se supone que el vídeo de entrada de hello tiene una marca de tiempo inicial de cero.</span><span class="sxs-lookup"><span data-stu-id="406c9-145">In hello example below, we assume that hello input video has a starting timestamp of zero.</span></span> <span data-ttu-id="406c9-146">**Orígenes** deberá colocarse al principio de Hola de hello presintonía.</span><span class="sxs-lookup"><span data-stu-id="406c9-146">**Sources** should be placed at hello beginning of hello preset.</span></span>

### <span data-ttu-id="406c9-147"><a id="json"></a>Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="406c9-147"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
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
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
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

### <a name="xml-preset"></a><span data-ttu-id="406c9-148">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="406c9-148">XML preset</span></span>
<span data-ttu-id="406c9-149">tootrim sus vídeos, puede realizar cualquiera de valores preestablecidos MES de hello documentados [aquí](media-services-mes-presets-overview.md) y modificar hello **orígenes** elemento (tal y como se muestra a continuación).</span><span class="sxs-lookup"><span data-stu-id="406c9-149">tootrim your videos, you can take any of hello MES presets documented [here](media-services-mes-presets-overview.md) and modify hello **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="406c9-150"><a id="overlay"></a>Creación de una superposición</span><span class="sxs-lookup"><span data-stu-id="406c9-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="406c9-151">Hola Media Encoder estándar permite toooverlay una imagen en un vídeo existente.</span><span class="sxs-lookup"><span data-stu-id="406c9-151">hello Media Encoder Standard allows you toooverlay an image onto an existing video.</span></span> <span data-ttu-id="406c9-152">Actualmente, se admite Hola siguientes formatos: png, jpg, gif y bmp.</span><span class="sxs-lookup"><span data-stu-id="406c9-152">Currently, hello following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="406c9-153">Hello valor preestablecido definida a continuación es un ejemplo básico de una superposición de vídeo.</span><span class="sxs-lookup"><span data-stu-id="406c9-153">hello preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="406c9-154">Además toodefining un archivo de valores preestablecidos, también tiene los servicios multimedia toolet saber qué archivo de recurso de hello es Hola superposición imagen y cuál es el archivo vídeo de origen de hello en el que desea toooverlay imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="406c9-154">In addition toodefining a preset file, you also have toolet Media Services know which file in hello asset is hello overlay image and which file is hello source video onto which you want toooverlay hello image.</span></span> <span data-ttu-id="406c9-155">archivo de vídeo de Hello tiene hello toobe **principal** archivo.</span><span class="sxs-lookup"><span data-stu-id="406c9-155">hello video file has toobe hello **primary** file.</span></span>

<span data-ttu-id="406c9-156">Si usas. NET, agregue Hola siguiendo dos funciones toohello .NET en el ejemplo se define en [esto](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tema.</span><span class="sxs-lookup"><span data-stu-id="406c9-156">If you are using .NET, add hello following two functions toohello .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="406c9-157">Hola **UploadMediaFilesFromFolder** función carga archivos desde una carpeta (por ejemplo, BigBuckBunny.mp4 y Image001.png) y conjuntos de Hola mp4 archivo toobe Hola archivo principal de hello recurso.</span><span class="sxs-lookup"><span data-stu-id="406c9-157">hello **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets hello mp4 file toobe hello primary file in hello asset.</span></span> <span data-ttu-id="406c9-158">Hola **EncodeWithOverlay** función usa el archivo preestablecido personalizado Hola que se pasó tooit (por ejemplo, hello preestablecido que se indica a continuación) toocreate Hola tarea de codificación.</span><span class="sxs-lookup"><span data-stu-id="406c9-158">hello **EncodeWithOverlay** function uses hello custom preset file that was passed tooit (for example, hello preset that follows) toocreate hello encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="406c9-159">Limitaciones actuales:</span><span class="sxs-lookup"><span data-stu-id="406c9-159">Current limitations:</span></span>
>
> <span data-ttu-id="406c9-160">no se admite el valor de opacidad de superposición de Hola.</span><span class="sxs-lookup"><span data-stu-id="406c9-160">hello overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="406c9-161">Su archivo de vídeo de origen y el archivo de imagen de superposición de hello tienen toobe en mismo activo de Hola y Hola conjunto de toobe de necesidades de archivo de vídeo como archivo principal de hello en este recurso.</span><span class="sxs-lookup"><span data-stu-id="406c9-161">Your source video file and hello overlay image file have toobe in hello same asset, and hello video file needs toobe set as hello primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="406c9-162">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="406c9-162">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
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
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="406c9-163">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="406c9-163">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <span data-ttu-id="406c9-164"><a id="silent_audio"></a>Inserción de una pista de audio silenciosa cuando la entrada no tiene audio</span><span class="sxs-lookup"><span data-stu-id="406c9-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="406c9-165">De forma predeterminada, si se envía un codificador de entrada toohello que solo no contiene vídeo, se oye ningún sonido, Hola activo de salida contiene archivos que contienen datos de solo vídeo.</span><span class="sxs-lookup"><span data-stu-id="406c9-165">By default, if you send an input toohello encoder that contains only video, and no audio, then hello output asset contains files that contain only video data.</span></span> <span data-ttu-id="406c9-166">Algunos reproductores no pueden tener toohandle tal flujos de salida.</span><span class="sxs-lookup"><span data-stu-id="406c9-166">Some players may not be able toohandle such output streams.</span></span> <span data-ttu-id="406c9-167">Puede usar este tooadd de codificador de hello configuración tooforce una salida de toohello silenciosa pista de audio en ese escenario.</span><span class="sxs-lookup"><span data-stu-id="406c9-167">You can use this setting tooforce hello encoder tooadd a silent audio track toohello output in that scenario.</span></span>

<span data-ttu-id="406c9-168">tooforce Hola codificador tooproduce un activo que contenga una pista de audio silenciosa cuando entrada no tiene oye ningún sonido, especifique el valor de "InsertSilenceIfNoAudio" Hola.</span><span class="sxs-lookup"><span data-stu-id="406c9-168">tooforce hello encoder tooproduce an asset that contains a silent audio track when input has no audio, specify hello "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="406c9-169">Puede realizar cualquiera de hello valores preestablecidos MES se documentan en [esto](media-services-mes-presets-overview.md) sección y realizar Hola después de modificación:</span><span class="sxs-lookup"><span data-stu-id="406c9-169">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="406c9-170">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="406c9-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="406c9-171">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="406c9-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="406c9-172"><a id="deinterlacing"></a>Deshabilitar el entrelazado automático</span><span class="sxs-lookup"><span data-stu-id="406c9-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="406c9-173">Los clientes no necesitan toodo nada si únicamente como Hola entrelazado toobe contenido automáticamente anular entrelazada.</span><span class="sxs-lookup"><span data-stu-id="406c9-173">Customers don’t need toodo anything if they like hello interlace contents toobe automatically de-interlaced.</span></span> <span data-ttu-id="406c9-174">Una vez automática Hola de entrelazado en hello (valor predeterminado) MES Hola automáticamente la detección de fotogramas entrelazados y solo anular interlaces fotogramas marcados como entrelazado.</span><span class="sxs-lookup"><span data-stu-id="406c9-174">When hello auto de-interlacing is on (default) hello MES does hello auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="406c9-175">Puede desactivar automáticamente Hola de entrelazado.</span><span class="sxs-lookup"><span data-stu-id="406c9-175">You can turn hello auto de-interlacing off.</span></span> <span data-ttu-id="406c9-176">Esta opción nos e recomienda.</span><span class="sxs-lookup"><span data-stu-id="406c9-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="406c9-177">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="406c9-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="406c9-178">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="406c9-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="406c9-179"><a id="audio_only"></a>Valores preestablecidos de solo audio</span><span class="sxs-lookup"><span data-stu-id="406c9-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="406c9-180">Esta sección muestra dos valores preestablecidos de MES de solo audio: Audio AAC y Audio AAC de buena calidad.</span><span class="sxs-lookup"><span data-stu-id="406c9-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="406c9-181">Audio AAC</span><span class="sxs-lookup"><span data-stu-id="406c9-181">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
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
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="406c9-182">Audio AAC de buena calidad</span><span class="sxs-lookup"><span data-stu-id="406c9-182">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="406c9-183"><a id="concatenate"></a>Concatenación de dos o más archivos de vídeo</span><span class="sxs-lookup"><span data-stu-id="406c9-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="406c9-184">Hello en el ejemplo siguiente se muestra cómo puede generar un valor preestablecido tooconcatenate dos o más archivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="406c9-184">hello following example illustrates how you can generate a preset tooconcatenate two or more video files.</span></span> <span data-ttu-id="406c9-185">escenario más común de Hello es cuando se desea tooadd un encabezado o un vídeo principal toohello de finalizador.</span><span class="sxs-lookup"><span data-stu-id="406c9-185">hello most common scenario is when you want tooadd a header or a trailer toohello main video.</span></span> <span data-ttu-id="406c9-186">Hola pensado uso resulta propiedades (resolución de vídeo, velocidad de fotogramas, número de pista de audio, etcetera) del recurso compartido de archivos de vídeo de Hola que se está editando juntos.</span><span class="sxs-lookup"><span data-stu-id="406c9-186">hello intended use is when hello video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="406c9-187">También debe tener cuidado no toomix vídeos de distintas velocidades de fotogramas o con un número diferente de pistas de audio.</span><span class="sxs-lookup"><span data-stu-id="406c9-187">You should take care not toomix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="406c9-188">Hello diseño actual de la característica de concatenación de hello espera ese Hola entrada clips de vídeo son coherentes en cuanto a la resolución, velocidad de fotogramas etcetera.</span><span class="sxs-lookup"><span data-stu-id="406c9-188">hello current design of hello concatenation feature expects that hello input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="406c9-189">Requisitos y consideraciones</span><span class="sxs-lookup"><span data-stu-id="406c9-189">Requirements and considerations</span></span>

* <span data-ttu-id="406c9-190">Los vídeos de entrada solo deberían tener una pista de audio.</span><span class="sxs-lookup"><span data-stu-id="406c9-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="406c9-191">Vídeos de entrada deben tener todos Hola misma velocidad de fotogramas.</span><span class="sxs-lookup"><span data-stu-id="406c9-191">Input videos should all have hello same frame rate.</span></span>
* <span data-ttu-id="406c9-192">Debe cargar los vídeos en activos independientes y establecer vídeos hello como archivo principal de Hola de cada recurso.</span><span class="sxs-lookup"><span data-stu-id="406c9-192">You must upload your videos into separate assets and set hello videos as hello primary file in each asset.</span></span>
* <span data-ttu-id="406c9-193">Necesita tooknow Hola que dure sus vídeos.</span><span class="sxs-lookup"><span data-stu-id="406c9-193">You need tooknow hello duration of your videos.</span></span>
* <span data-ttu-id="406c9-194">Hello preestablecidos ejemplos siguientes se supone que todos los vídeos de entrada de hello comience con una marca de tiempo de cero.</span><span class="sxs-lookup"><span data-stu-id="406c9-194">hello preset examples below assumes that all hello input videos start with a timestamp of zero.</span></span> <span data-ttu-id="406c9-195">Necesita toomodify Hola StartTime valores si los vídeos de hello tienen marca de tiempo inicial diferente, como sucede normalmente Hola con archivos de almacenamiento en vivo.</span><span class="sxs-lookup"><span data-stu-id="406c9-195">You need toomodify hello StartTime values if hello videos have different starting timestamp, as is typically hello case with live archives.</span></span>
* <span data-ttu-id="406c9-196">Hello valor preestablecido JSON hace que las referencias explícitas toohello AssetID valores Hola de recursos de entrada.</span><span class="sxs-lookup"><span data-stu-id="406c9-196">hello JSON preset makes explicit references toohello AssetID values of hello input assets.</span></span>
* <span data-ttu-id="406c9-197">código de ejemplo de Hola se da por supuesto que Hola preestablecido JSON se ha guardado el archivo local de tooa, por ejemplo, "C:\supportFiles\preset.json".</span><span class="sxs-lookup"><span data-stu-id="406c9-197">hello sample code assumes that hello JSON preset has been saved tooa local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="406c9-198">También se supone que se han creado dos recursos mediante la carga de archivos de vídeo de dos, y que sepan Hola valores AssetID resultantes.</span><span class="sxs-lookup"><span data-stu-id="406c9-198">It also assumes that two assets have been created by uploading two video files, and that you know hello resultant AssetID values.</span></span>
* <span data-ttu-id="406c9-199">Hola fragmento de código y JSON valor preestablecido muestra un ejemplo de la concatenación de dos archivos de vídeo.</span><span class="sxs-lookup"><span data-stu-id="406c9-199">hello code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="406c9-200">Se puede ampliar toomore que dos vídeos:</span><span class="sxs-lookup"><span data-stu-id="406c9-200">You can extend it toomore than two videos by:</span></span>

  1. <span data-ttu-id="406c9-201">Tarea que realiza la llamada. InputAssets.Add() tooadd varias veces más vídeos, en orden.</span><span class="sxs-lookup"><span data-stu-id="406c9-201">Calling task.InputAssets.Add() repeatedly tooadd more videos, in order.</span></span>
  2. <span data-ttu-id="406c9-202">Realizar correspondiente edita el elemento toohello "orígenes" Hola JSON, agregando más entradas en hello mismo orden.</span><span class="sxs-lookup"><span data-stu-id="406c9-202">Making corresponding edits toohello "Sources" element in hello JSON, by adding more entries, in hello same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="406c9-203">Código .NET</span><span class="sxs-lookup"><span data-stu-id="406c9-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="406c9-204">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="406c9-204">JSON preset</span></span>

<span data-ttu-id="406c9-205">Actualizar el valor preestablecido con identificadores de activos de Hola que desea tooconcatenate y con el segmento de tiempo adecuado de Hola para cada vídeo personalizado.</span><span class="sxs-lookup"><span data-stu-id="406c9-205">Update your custom preset with ids of hello assets that you want tooconcatenate, and with hello appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
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

## <span data-ttu-id="406c9-206"><a id="crop"></a>Recorte de vídeos con Codificador multimedia estándar</span><span class="sxs-lookup"><span data-stu-id="406c9-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="406c9-207">Vea hello [recortar vídeos con Media Encoder estándar](media-services-crop-video.md) tema.</span><span class="sxs-lookup"><span data-stu-id="406c9-207">See hello [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="406c9-208"><a id="no_video"></a>Inserción de una pista de vídeo cuando la entrada cuando no tiene vídeo</span><span class="sxs-lookup"><span data-stu-id="406c9-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="406c9-209">De forma predeterminada, si se envía un codificador toohello de entrada que contiene solo audio y no hay video, Hola activo de salida contiene archivos que contienen datos de solo audio.</span><span class="sxs-lookup"><span data-stu-id="406c9-209">By default, if you send an input toohello encoder that contains only audio, and no video, then hello output asset contains files that contain only audio data.</span></span> <span data-ttu-id="406c9-210">Algunos reproductores, incluido Azure Media Player (vea [esto](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) puede no ser capaz de toohandle dichos flujos.</span><span class="sxs-lookup"><span data-stu-id="406c9-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able toohandle such streams.</span></span> <span data-ttu-id="406c9-211">Puede usar este tooadd de codificador de configuración tooforce Hola una salida de la pista de vídeo monocromática toohello en ese escenario.</span><span class="sxs-lookup"><span data-stu-id="406c9-211">You can use this setting tooforce hello encoder tooadd a monochrome video track toohello output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="406c9-212">Al forzar Hola codificador tooinsert un tamaño de salida pista de vídeo aumenta Hola de hello activo de salida y, por tanto, Hola costos derivados de las tareas de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="406c9-212">Forcing hello encoder tooinsert an output video track increases hello size of hello output Asset, and thereby hello cost incurred for hello encoding Task.</span></span> <span data-ttu-id="406c9-213">Debe ejecutar las pruebas tooverify que este incremento resultante tiene solo un leve impacto en los cargos mensuales.</span><span class="sxs-lookup"><span data-stu-id="406c9-213">You should run tests tooverify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a><span data-ttu-id="406c9-214">Inserción de vídeo al solo Hola velocidades de bits bajas</span><span class="sxs-lookup"><span data-stu-id="406c9-214">Inserting video at only hello lowest bitrate</span></span>

<span data-ttu-id="406c9-215">Supongamos que usa una codificación de velocidad de bits múltiples preestablecido como ["H264 varias velocidades de bits 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode todo el catálogo de transmisión por secuencias, que contiene una mezcla de archivos de vídeo y archivos de solo audio de entrada.</span><span class="sxs-lookup"><span data-stu-id="406c9-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="406c9-216">En este escenario, cuando la entrada de hello no tiene ningún vídeo, puede que desee tooforce Hola codificador tooinsert un vídeo monocromática realizar el seguimiento en simplemente Hola velocidades de bits bajas, como opuesto tooinserting vídeo en cada velocidad de bits de salida.</span><span class="sxs-lookup"><span data-stu-id="406c9-216">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at just hello lowest bitrate, as opposed tooinserting video at every output bitrate.</span></span> <span data-ttu-id="406c9-217">tooachieve, necesita hello toouse **InsertBlackIfNoVideoBottomLayerOnly** marca.</span><span class="sxs-lookup"><span data-stu-id="406c9-217">tooachieve this, you need toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="406c9-218">Puede realizar cualquiera de hello valores preestablecidos MES se documentan en [esto](media-services-mes-presets-overview.md) sección y realizar Hola después de modificación:</span><span class="sxs-lookup"><span data-stu-id="406c9-218">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="406c9-219">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="406c9-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="406c9-220">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="406c9-220">XML preset</span></span>

<span data-ttu-id="406c9-221">Cuando se utiliza XML, utilice condición = "InsertBlackIfNoVideoBottomLayerOnly" como un atributo toohello **H264Video** elemento y condición = "InsertSilenceIfNoAudio" como un atributo demasiado**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="406c9-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="406c9-222">Inserción de vídeo con todas las velocidades de bits de salida</span><span class="sxs-lookup"><span data-stu-id="406c9-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="406c9-223">Supongamos que usa una codificación de velocidad de bits múltiples preestablecido como ["H264 varias velocidades de bits 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode todo el catálogo de transmisión por secuencias, que contiene una mezcla de archivos de vídeo y archivos de solo audio de entrada.</span><span class="sxs-lookup"><span data-stu-id="406c9-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="406c9-224">En este escenario, cuando la entrada de hello no tiene ningún vídeo, puede que desee tooforce Hola codificador tooinsert realizar un seguimiento de un vídeo monocromático a todas las velocidades de bits de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="406c9-224">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at all hello output bitrates.</span></span> <span data-ttu-id="406c9-225">Esto garantiza que el resultado de los activos son todo homogéneos con toonumber respecto de las pistas de vídeo y pistas de audio.</span><span class="sxs-lookup"><span data-stu-id="406c9-225">This ensures that your output Assets are all homogenous with respect toonumber of video tracks and audio tracks.</span></span> <span data-ttu-id="406c9-226">tooachieve, necesita toospecify Hola marca "InsertBlackIfNoVideo".</span><span class="sxs-lookup"><span data-stu-id="406c9-226">tooachieve this, you need toospecify hello "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="406c9-227">Puede realizar cualquiera de hello valores preestablecidos MES se documentan en [esto](media-services-mes-presets-overview.md) sección y realizar Hola después de modificación:</span><span class="sxs-lookup"><span data-stu-id="406c9-227">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="406c9-228">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="406c9-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="406c9-229">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="406c9-229">XML preset</span></span>

<span data-ttu-id="406c9-230">Cuando se utiliza XML, utilice condición = "InsertBlackIfNoVideo" como un atributo toohello **H264Video** elemento y condición = "InsertSilenceIfNoAudio" como un atributo demasiado**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="406c9-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <span data-ttu-id="406c9-231"><a id="rotate_video"></a>Girar un vídeo</span><span class="sxs-lookup"><span data-stu-id="406c9-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="406c9-232">Hola [Media Encoder estándar](media-services-dotnet-encode-with-media-encoder-standard.md) admite la rotación de ángulos de 0/90/180 y 270.</span><span class="sxs-lookup"><span data-stu-id="406c9-232">hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="406c9-233">comportamiento predeterminado de Hello es "Auto", donde intenta toodetect Hola rotación metadatos en el archivo de vídeo entrante hello y compensar para él.</span><span class="sxs-lookup"><span data-stu-id="406c9-233">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming video file and compensate for it.</span></span> <span data-ttu-id="406c9-234">Hola siguientes **orígenes** tooone de elemento de valores preestablecidos de hello definidos en [esto](media-services-mes-presets-overview.md) sección:</span><span class="sxs-lookup"><span data-stu-id="406c9-234">Include hello following **Sources** element tooone of hello presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="406c9-235">Valor preestablecido JSON</span><span class="sxs-lookup"><span data-stu-id="406c9-235">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="406c9-236">Valor preestablecido XML</span><span class="sxs-lookup"><span data-stu-id="406c9-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="406c9-237">Consulte también [esto](media-services-mes-schema.md#PreserveResolutionAfterRotation) tema para obtener más información sobre cómo codificador Hola interpreta la configuración de ancho y alto de Hola Hola predefinidos, cuando se activa la compensación de rotación.</span><span class="sxs-lookup"><span data-stu-id="406c9-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how hello encoder interprets hello Width and Height settings in hello preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="406c9-238">Puede usar Hola valor "0" tooindicate toohello codificador tooignore rotación metadatos, si están presentes en vídeo de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="406c9-238">You can use hello value "0" tooindicate toohello encoder tooignore rotation metadata, if present, in hello input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="406c9-239">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="406c9-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="406c9-240">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="406c9-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="406c9-241">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="406c9-241">See Also</span></span>
[<span data-ttu-id="406c9-242">Información general sobre la codificación de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="406c9-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
