---
title: "Audio de velocidad de bits única 4K aaaH264 5.1 | Documentos de Microsoft"
description: "Hola tema encontrará un resumen de Hola ** Audio de velocidad de bits única del H264 4K 5.1* * valor predefinido de tarea."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 72cb95ac-2cd6-4ef4-9938-8f22cea04920
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8ed5d85a0c58eaa9b076be667f4499659d90b19e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-4k-audio-51"></a><span data-ttu-id="99815-103">H264 Single Bitrate 4K Audio 5.1</span><span class="sxs-lookup"><span data-stu-id="99815-103">H264 Single Bitrate 4K Audio 5.1</span></span>
<span data-ttu-id="99815-104">`Media Encoder Standard` define un conjunto de valores predeterminados de Encoding que puede usar al crear trabajos de Encoding.</span><span class="sxs-lookup"><span data-stu-id="99815-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="99815-105">Puede utilizar un `preset name` toospecify en qué formato desea tooencode su archivo multimedia.</span><span class="sxs-lookup"><span data-stu-id="99815-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="99815-106">O bien, puede crear sus propios valores predeterminados basados en XML o JSON (mediante la codificación UTF-8 o UTF-16).</span><span class="sxs-lookup"><span data-stu-id="99815-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="99815-107">A continuación, pasaría codificador de hello toohello valores preestablecidos personalizados.</span><span class="sxs-lookup"><span data-stu-id="99815-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="99815-108">Para obtener lista de hello del programa Hola a todos los preestablecido nombres admitidos por este `Media Encoder Standard` codificador, vea [valores preestablecidos de tarea para Media Encoder estándar](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99815-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="99815-109">Este tema muestra hello `H264 Single Bitrate 4K Audio 5.1` preestablecido (en formato XML y JSON).</span><span class="sxs-lookup"><span data-stu-id="99815-109">This topic shows hello `H264 Single Bitrate 4K Audio 5.1` preset (in XML and JSON format).</span></span>  
  
 <span data-ttu-id="99815-110">Este valor predeterminado genera un único archivo MP4 con una velocidad de bits de 18 000 kbps y audio AAC 5.1.</span><span class="sxs-lookup"><span data-stu-id="99815-110">This preset produces a single MP4 file with a bitrate of 18000 kbps, and AAC 5.1 audio.</span></span> <span data-ttu-id="99815-111">Para obtener información detallada sobre el perfil, velocidad de bits, frecuencia de muestreo, etc. de este valor preestablecido, examine Hola XML o JSON definido más adelante.</span><span class="sxs-lookup"><span data-stu-id="99815-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="99815-112">Para explicaciones de cada elemento de qué significa y los valores válidos de Hola para cada elemento, vea hello [Media Encoder estándar esquema](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="99815-112">For explanations of what each element means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md).</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="99815-113">Debe obtener Hola Premium reservado codifica el tipo de unidad con 4K.</span><span class="sxs-lookup"><span data-stu-id="99815-113">You should get hello Premium reserved unit type with 4K encodes.</span></span> <span data-ttu-id="99815-114">Para obtener más información, consulte [cómo tooScale codificación](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span><span class="sxs-lookup"><span data-stu-id="99815-114">For more information, see [How tooScale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
 <span data-ttu-id="99815-115">XML</span><span class="sxs-lookup"><span data-stu-id="99815-115">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>18000</Bitrate>  
          <Width>3840</Width>  
          <Height>2160</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>18000</MaxBitrate>  
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
  
 <span data-ttu-id="99815-116">JSON</span><span class="sxs-lookup"><span data-stu-id="99815-116">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 18000,  
          "MaxBitrate": 18000,  
          "BufferWindow": "00:00:05",  
          "Width": 3840,  
          "Height": 2160,  
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
