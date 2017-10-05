---
title: "Introducción y comparación de codificadores multimedia a petición de Azure | Microsoft Docs"
description: "En este tema se proporciona información general y una comparación de los codificadores multimedia a petición de Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 538a6ab60168735c2626a93cdeedd8d4999a6efc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="f9d0b-103">Información general y comparación de codificadores multimedia a petición de Azure</span><span class="sxs-lookup"><span data-stu-id="f9d0b-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="f9d0b-104">Información general sobre la codificación</span><span class="sxs-lookup"><span data-stu-id="f9d0b-104">Encoding overview</span></span>
<span data-ttu-id="f9d0b-105">Servicios multimedia de Azure ofrece varias opciones para la codificación de medios en la nube.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-105">Azure Media Services provides multiple options for the encoding of media in the cloud.</span></span>

<span data-ttu-id="f9d0b-106">Cuando comience con Servicios multimedia, es importante comprender la diferencia entre códecs y formatos de archivo.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-106">When starting out with Media Services, it is important to understand the difference between codecs and file formats.</span></span>
<span data-ttu-id="f9d0b-107">Los códecs son el software que implementa los algoritmos de compresión/descompresión, mientras que los formatos de archivo son contenedores que contienen el vídeo comprimido.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-107">Codecs are the software that implements the compression/decompression algorithms whereas file formats are containers that hold the compressed video.</span></span>

<span data-ttu-id="f9d0b-108">Media Services proporciona empaquetado dinámico que permite entregar contenido codificado MP4 de velocidad de bits adaptable o Smooth Streaming en formatos de streaming admitidos por Media Services (MPEG-DASH, HLS y Smooth Streaming) sin tener que volver a realizar el empaquetamiento en estos formatos de streaming.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-108">Media Services provides dynamic packaging which allows you to deliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having to re-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="f9d0b-109">Cuando se crea la cuenta de AMS, se agrega un punto de conexión de streaming **predeterminado** a la cuenta en estado **Stopped** (Detenido).</span><span class="sxs-lookup"><span data-stu-id="f9d0b-109">When your AMS account is created a **default** streaming endpoint is added to your account in the **Stopped** state.</span></span> <span data-ttu-id="f9d0b-110">Para iniciar la transmisión del contenido y aprovechar el empaquetado dinámico y el cifrado dinámico, el punto de conexión de streaming desde el que va a transmitir el contenido debe estar en estado **Running** (En ejecución).</span><span class="sxs-lookup"><span data-stu-id="f9d0b-110">To start streaming your content and take advantage of dynamic packaging and dynamic encryption, the streaming endpoint from which you want to stream content has to be in the **Running** state.</span></span> <span data-ttu-id="f9d0b-111">Para aprovecharse de los [paquetes dinámicos](media-services-dynamic-packaging-overview.md), deberá hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f9d0b-111">To take advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need to do the following:</span></span>
>
><span data-ttu-id="f9d0b-112">Además, codifique su archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptable o archivos Smooth Streaming de velocidad de bits adaptable (los pasos de codificación se muestran más adelante en este tutorial).</span><span class="sxs-lookup"><span data-stu-id="f9d0b-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (the encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="f9d0b-113">Servicios multimedia admite los siguientes codificadores a petición que se describen en este artículo:</span><span class="sxs-lookup"><span data-stu-id="f9d0b-113">Media Services supports the following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="f9d0b-114">Media Encoder Estándar</span><span class="sxs-lookup"><span data-stu-id="f9d0b-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="f9d0b-115">Flujo de trabajo del Codificador multimedia</span><span class="sxs-lookup"><span data-stu-id="f9d0b-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="f9d0b-116">En este artículo se ofrece una breve introducción a los codificadores multimedia a petición y se proporcionan vínculos a artículos con información más detallada.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-116">This article gives a brief overview of on demand media encoders and provides links to articles that give more detailed information.</span></span> <span data-ttu-id="f9d0b-117">También se proporciona una comparación de los codificadores.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-117">The topic also provides comparison of the encoders.</span></span>

>[!NOTE]
><span data-ttu-id="f9d0b-118">De forma predeterminada cada cuenta de Servicios multimedia puede tener una tarea de codificación activa a la vez.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="f9d0b-119">Puede reservar unidades de codificación que permiten la ejecución simultánea de varias tareas de codificación, una para cada unidad reservada de codificación que ha adquirido.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-119">You can reserve encoding units that allow you to have multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="f9d0b-120">Para obtener información, consulte [Escalado de unidades de codificación](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9d0b-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="f9d0b-121">Media Encoder Estándar</span><span class="sxs-lookup"><span data-stu-id="f9d0b-121">Media Encoder Standard</span></span>
### <a name="how-to-use"></a><span data-ttu-id="f9d0b-122">Modo de uso</span><span class="sxs-lookup"><span data-stu-id="f9d0b-122">How to use</span></span>
[<span data-ttu-id="f9d0b-123">Codificación con Codificador multimedia estándar</span><span class="sxs-lookup"><span data-stu-id="f9d0b-123">How to encode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="f9d0b-124">Formatos</span><span class="sxs-lookup"><span data-stu-id="f9d0b-124">Formats</span></span>
[<span data-ttu-id="f9d0b-125">Códecs y formatos</span><span class="sxs-lookup"><span data-stu-id="f9d0b-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="f9d0b-126">Valores preestablecidos</span><span class="sxs-lookup"><span data-stu-id="f9d0b-126">Presets</span></span>
<span data-ttu-id="f9d0b-127">Codificador multimedia estándar se configura mediante uno de los valores preestablecidos descritos [aquí](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="f9d0b-127">Media Encoder Standard is configured using one of the encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="f9d0b-128">Metadatos de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="f9d0b-128">Input and output metadata</span></span>
<span data-ttu-id="f9d0b-129">[Aquí](media-services-input-metadata-schema.md)se describen los metadatos de entrada de los codificadores.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-129">The encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="f9d0b-130">[Aquí](media-services-output-metadata-schema.md)se describen los metadatos de salida de los codificadores.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-130">The encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="f9d0b-131">Generación de miniaturas</span><span class="sxs-lookup"><span data-stu-id="f9d0b-131">Generate thumbnails</span></span>
<span data-ttu-id="f9d0b-132">Para más información, consulte [Generación de miniaturas](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="f9d0b-132">For information, see [How to generate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="f9d0b-133">Recorte de vídeos</span><span class="sxs-lookup"><span data-stu-id="f9d0b-133">Trim videos (clipping)</span></span>
<span data-ttu-id="f9d0b-134">Para más información, consulte [Recorte de un vídeo](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="f9d0b-134">For information, see [How to trim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="f9d0b-135">Creación de superposiciones</span><span class="sxs-lookup"><span data-stu-id="f9d0b-135">Create overlays</span></span>
<span data-ttu-id="f9d0b-136">Para más información, consulte [Creación de una superposición](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="f9d0b-136">For information, see [How to create overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="f9d0b-137">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="f9d0b-137">See also</span></span>
[<span data-ttu-id="f9d0b-138">El blog de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="f9d0b-138">The Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="f9d0b-139">Flujo de trabajo del Codificador multimedia</span><span class="sxs-lookup"><span data-stu-id="f9d0b-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="f9d0b-140">Información general</span><span class="sxs-lookup"><span data-stu-id="f9d0b-140">Overview</span></span>
[<span data-ttu-id="f9d0b-141">Introducción de la codificación Premium en Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="f9d0b-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a><span data-ttu-id="f9d0b-142">Modo de uso</span><span class="sxs-lookup"><span data-stu-id="f9d0b-142">How to use</span></span>
<span data-ttu-id="f9d0b-143">El flujo de trabajo del Codificador multimedia Premium se configura mediante flujos de trabajo complejos.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="f9d0b-144">Los archivos de flujo de trabajo pueden crearse y actualizarse con la herramienta [Diseñador de flujo de trabajo](media-services-workflow-designer.md) .</span><span class="sxs-lookup"><span data-stu-id="f9d0b-144">Workflow files could be created and updated using the [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="f9d0b-145">Uso de la codificación Premium en Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="f9d0b-145">How to Use Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="f9d0b-146">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="f9d0b-146">Known issues</span></span>
<span data-ttu-id="f9d0b-147">Si el vídeo de entrada no contiene subtítulos, el recurso de salida seguirá conteniendo un archivo TTML vacío.</span><span class="sxs-lookup"><span data-stu-id="f9d0b-147">If your input video does not contain closed captioning, the output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="f9d0b-148">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="f9d0b-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f9d0b-149">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="f9d0b-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="f9d0b-150">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="f9d0b-150">Related articles</span></span>
* [<span data-ttu-id="f9d0b-151">Realización de tareas de codificación avanzadas mediante la personalización de valores preestablecidos de Media Encoder Estándar</span><span class="sxs-lookup"><span data-stu-id="f9d0b-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="f9d0b-152">Cuotas y limitaciones</span><span class="sxs-lookup"><span data-stu-id="f9d0b-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
