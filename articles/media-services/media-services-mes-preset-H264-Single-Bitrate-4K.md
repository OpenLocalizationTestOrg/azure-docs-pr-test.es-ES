---
title: Valores predeterminados de Media Encoder Standard para H264 Single Bitrate 4K - Azure | Microsoft Docs
description: "El tema proporciona información general sobre el valor predeterminado de tarea **H264 Single Bitrate 4K**."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 8e437aea-8193-49a0-9ff2-4fd391c80972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 64c68363d4ba89e9ebbcaca8ff45d12f771e3a8c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="h264-single-bitrate-4k"></a><span data-ttu-id="f73cd-103">H264 Single Bitrate 4K</span><span class="sxs-lookup"><span data-stu-id="f73cd-103">H264 Single Bitrate 4K</span></span>
<span data-ttu-id="f73cd-104">`Media Encoder Standard` define un conjunto de valores predeterminados de Encoding que puede usar al crear trabajos de Encoding.</span><span class="sxs-lookup"><span data-stu-id="f73cd-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="f73cd-105">Puede usar `preset name` para especificar en qué formato desea codificar el archivo multimedia.</span><span class="sxs-lookup"><span data-stu-id="f73cd-105">You can either use a `preset name` to specify into which format you would like to encode your media file.</span></span> <span data-ttu-id="f73cd-106">O bien, puede crear sus propios valores predeterminados basados en XML o JSON (mediante la codificación UTF-8 o UTF-16).</span><span class="sxs-lookup"><span data-stu-id="f73cd-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="f73cd-107">Después pasaría el valor predeterminado personalizado al codificador.</span><span class="sxs-lookup"><span data-stu-id="f73cd-107">You would then pass the custom preset to the encoder.</span></span> <span data-ttu-id="f73cd-108">Para obtener la lista de todos los nombres predeterminados admitidos por este codificador `Media Encoder Standard`, vea [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md) (Valores predeterminados de tarea para Media Encoder Standard).</span><span class="sxs-lookup"><span data-stu-id="f73cd-108">For the list of all the preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="f73cd-109">En este tema se muestra el valor predeterminado `H264 Single Bitrate 4K` en formato XML y JSON.</span><span class="sxs-lookup"><span data-stu-id="f73cd-109">This topic shows the `H264 Single Bitrate 4K` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="f73cd-110">Este valor predeterminado genera un único archivo MP4 con una velocidad de bits de 18 000 kbps y audio AAC estéreo.</span><span class="sxs-lookup"><span data-stu-id="f73cd-110">This preset produces a single MP4 file with a bitrate of 18000 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="f73cd-111">Para información detallada sobre el perfil, la velocidad de bits, la frecuencia de muestreo, etc., de este valor predeterminado, examine el código XML o JSON definido más adelante.</span><span class="sxs-lookup"><span data-stu-id="f73cd-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine the XML or JSON defined below.</span></span> <span data-ttu-id="f73cd-112">Para obtener explicaciones de lo que cada elemento significa en estos nombres predeterminados y los valores válidos para cada elemento, vea el tema sobre el [esquema de Media Encoder Standard](media-services-mes-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f73cd-112">For explanations of what each element in these presets means, and the valid values for each element, see the [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f73cd-113">Debe obtener el tipo de unidad reservada premium con codificación 4K.</span><span class="sxs-lookup"><span data-stu-id="f73cd-113">You should get the Premium reserved unit type with 4K encodes.</span></span> <span data-ttu-id="f73cd-114">Para obtener más información, consulte [Escalación de codificación](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span><span class="sxs-lookup"><span data-stu-id="f73cd-114">For more information, see [How to Scale Encoding](https://azure.microsoft.com/en-us/documentation/articles/media-services-portal-encoding-units).</span></span>  
  
 <span data-ttu-id="f73cd-115">XML</span><span class="sxs-lookup"><span data-stu-id="f73cd-115">XML</span></span>  
  
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
  
 <span data-ttu-id="f73cd-116">JSON</span><span class="sxs-lookup"><span data-stu-id="f73cd-116">JSON</span></span>  
  
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
