---
title: "velocidad de bits única del aaaH264 Media Encoder estándar preestablecido - 720p Azure | Documentos de Microsoft"
description: "Hola tema encontrará un resumen de Hola ** velocidad de bits única H264 720 p ** valor predefinido de tarea."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: f66da66c-9f21-441d-8038-51e3094e9307
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 38229713b4c88cd78acbd597870bfa144f10ae1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-720p"></a><span data-ttu-id="cd226-103">H264 Single Bitrate 720p</span><span class="sxs-lookup"><span data-stu-id="cd226-103">H264 Single Bitrate 720p</span></span>
<span data-ttu-id="cd226-104">`Media Encoder Standard` define un conjunto de valores predeterminados de Encoding que puede usar al crear trabajos de Encoding.</span><span class="sxs-lookup"><span data-stu-id="cd226-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="cd226-105">Puede utilizar un `preset name` toospecify en qué formato desea tooencode su archivo multimedia.</span><span class="sxs-lookup"><span data-stu-id="cd226-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="cd226-106">O bien, puede crear sus propios valores predeterminados basados en XML o JSON (mediante la codificación UTF-8 o UTF-16).</span><span class="sxs-lookup"><span data-stu-id="cd226-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="cd226-107">A continuación, pasaría codificador de hello toohello valores preestablecidos personalizados.</span><span class="sxs-lookup"><span data-stu-id="cd226-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="cd226-108">Para obtener lista de hello del programa Hola a todos los preestablecido nombres admitidos por este `Media Encoder Standard` codificador, vea [valores preestablecidos de tarea para Media Encoder estándar](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd226-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="cd226-109">Este tema muestra hello `H264 Single Bitrate 720p` preestablecido en formato XML y JSON.</span><span class="sxs-lookup"><span data-stu-id="cd226-109">This topic shows hello `H264 Single Bitrate 720p` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="cd226-110">Este valor predeterminado genera un único archivo MP4 con una velocidad de bits de 4500 kbps y audio AAC estéreo.</span><span class="sxs-lookup"><span data-stu-id="cd226-110">This preset produces a single MP4 file with a bitrate of 4500 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="cd226-111">Para obtener información detallada sobre el perfil, velocidad de bits, frecuencia de muestreo, etc. de este valor preestablecido, examine Hola XML o JSON definido más adelante.</span><span class="sxs-lookup"><span data-stu-id="cd226-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="cd226-112">Para obtener una explicación de cada elemento de qué en estos medios de valores predefinidos y los valores válidos de Hola para cada elemento, vea hello [Media Encoder estándar esquema](media-services-mes-schema.md) tema.</span><span class="sxs-lookup"><span data-stu-id="cd226-112">For explanations of what each element in these presets means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="cd226-113">XML</span><span class="sxs-lookup"><span data-stu-id="cd226-113">XML</span></span>  
  
```  
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
      <Chapters />  
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
```  
  
 <span data-ttu-id="cd226-114">JSON</span><span class="sxs-lookup"><span data-stu-id="cd226-114">JSON</span></span>  
  
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
          "Bitrate": 4500,  
          "MaxBitrate": 4500,  
          "BufferWindow": "00:00:05",  
          "Width": 1280,  
          "Height": 720,  
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
```
