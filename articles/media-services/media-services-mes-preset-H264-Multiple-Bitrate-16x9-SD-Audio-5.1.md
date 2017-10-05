---
title: H264 Multiple Bitrate 16x9 SD Audio 5.1 | Microsoft Docs
description: "El tema proporciona información general sobre el valor predeterminado de tarea **H264 Multiple Bitrate 16x9 SD Audio 5.1**."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 35007ed3-8b01-44ec-9d1e-1714c7e697e9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 52b8c9073f89279cb4509bcdf872ef0d6d1d709b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="h264-multiple-bitrate-16x9-sd-audio-51"></a><span data-ttu-id="1957f-103">H264 Multiple Bitrate 16x9 SD Audio 5.1</span><span class="sxs-lookup"><span data-stu-id="1957f-103">H264 Multiple Bitrate 16x9 SD Audio 5.1</span></span>
<span data-ttu-id="1957f-104">`Media Encoder Standard` define un conjunto de valores predeterminados de Encoding que puede usar al crear trabajos de Encoding.</span><span class="sxs-lookup"><span data-stu-id="1957f-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="1957f-105">Puede usar `preset name` para especificar en qué formato desea codificar el archivo multimedia.</span><span class="sxs-lookup"><span data-stu-id="1957f-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="1957f-106">O bien, puede crear sus propios valores predeterminados basados en XML o JSON (mediante la codificación UTF-8 o UTF-16).</span><span class="sxs-lookup"><span data-stu-id="1957f-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="1957f-107">Después pasaría el valor predeterminado personalizado al codificador.</span><span class="sxs-lookup"><span data-stu-id="1957f-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="1957f-108">Para obtener la lista de todos los nombres predeterminados admitidos por este codificador `Media Encoder Standard`, vea [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md) (Valores predeterminados de tarea para Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="1957f-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="1957f-109">En este tema se muestra el valor predeterminado `H264 Multiple Bitrate 16x9 SD Audio 5.1` en formato XML y JSON.</span><span class="sxs-lookup"><span data-stu-id="1957f-109">This topic shows the `H264 Multiple Bitrate 16x9 SD Audio 5.1` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="1957f-110">Este valor predeterminado genera un conjunto de 5 archivos MP4 alineados con GOP, que abarcan desde 1900 kbps hasta 400 kbps y audio AAC 5.1.</span><span class="sxs-lookup"><span data-stu-id="1957f-110">This preset produces a set of 5 GOP-aligned MP4 files, ranging from 1900 kbps to 400 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="1957f-111">Para información detallada sobre el perfil, la velocidad de bits, la frecuencia de muestreo, etc. de este valor predeterminado, examine el código XML o JSON definido más adelante.</span><span class="sxs-lookup"><span data-stu-id="1957f-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="1957f-112">Para obtener explicaciones de lo que cada elemento significa y los valores válidos para cada elemento, vea el tema sobre el [esquema de Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="1957f-112">For explanations of what each element means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="1957f-113">Cuando se modifiquen los valores `Width` y `Height` en las capas, asegúrese de que la relación de aspecto no cambia.</span><span class="sxs-lookup"><span data-stu-id="1957f-113">When modifying the `Width` and `Height` values across layers, make sure that the aspect ratio remains consistent.</span></span> <span data-ttu-id="1957f-114">Por ejemplo: 1920x1080, 1280x720, 1080x576 y 640x360.</span><span class="sxs-lookup"><span data-stu-id="1957f-114">For example: 1920x1080, 1280x720, 1080x576, 640x360.</span></span> <span data-ttu-id="1957f-115">No debe utilizar una combinación de relaciones de aspecto, como 1280x720, 720x480 y 640x360.</span><span class="sxs-lookup"><span data-stu-id="1957f-115">You should not use a mixture of aspect ratios, such as: 1280x720, 720x480, 640x360.</span></span>  
  
 <span data-ttu-id="1957f-116">XML</span><span class="sxs-lookup"><span data-stu-id="1957f-116">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>1900</Bitrate>  
          <Width>848</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>1900</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>1300</Bitrate>  
          <Width>848</Width>  
          <Height>480</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>1300</MaxBitrate>  
        </H264Layer>  
        <H264Layer>  
          <Bitrate>900</Bitrate>  
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
          <MaxBitrate>900</MaxBitrate>  
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
          <Width>432</Width>  
          <Height>240</Height>  
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
      <Chapters />  
    </H264Video>  
    <AACAudio>  
      <Profile>AACLC</Profile>  
      <Channels>6</Channels>  
      <SamplingRate>48000</SamplingRate>  
      <Bitrate>384</Bitrate>  
    </AACAudio>  
  </Encoding>  
  <Outputs>  
    <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">  
      <MP4Format />  
    </Output>  
  </Outputs>  
</Preset>  
```  
  
 <span data-ttu-id="1957f-117">JSON</span><span class="sxs-lookup"><span data-stu-id="1957f-117">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 1900,  
          "MaxBitrate": 1900,  
          "BufferWindow": "00:00:05",  
          "Width": 848,  
          "Height": 480,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        },  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 1300,  
          "MaxBitrate": 1300,  
          "BufferWindow": "00:00:05",  
          "Width": 848,  
          "Height": 480,  
          "BFrames": 3,  
          "ReferenceFrames": 3,  
          "AdaptiveBFrame": true,  
          "Type": "H264Layer",  
          "FrameRate": "0/1"  
        },  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 900,  
          "MaxBitrate": 900,  
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
          "Width": 432,  
          "Height": 240,  
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
      "Channels": 6,  
      "SamplingRate": 48000,  
      "Bitrate": 384,  
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
```
