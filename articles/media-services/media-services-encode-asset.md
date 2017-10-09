---
title: "aaaOverview y comparación de Azure en exigen codificadores multimedia | Documentos de Microsoft"
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
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a><span data-ttu-id="9c5da-103">Información general y comparación de codificadores multimedia a petición de Azure</span><span class="sxs-lookup"><span data-stu-id="9c5da-103">Overview and comparison of Azure on demand media encoders</span></span>
## <a name="encoding-overview"></a><span data-ttu-id="9c5da-104">Información general sobre la codificación</span><span class="sxs-lookup"><span data-stu-id="9c5da-104">Encoding overview</span></span>
<span data-ttu-id="9c5da-105">Servicios multimedia de Azure proporciona varias opciones para la codificación de Hola de medios en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c5da-105">Azure Media Services provides multiple options for hello encoding of media in hello cloud.</span></span>

<span data-ttu-id="9c5da-106">Al iniciar la con los servicios multimedia, es importante toounderstand Hola diferencia entre códecs y formatos de archivo.</span><span class="sxs-lookup"><span data-stu-id="9c5da-106">When starting out with Media Services, it is important toounderstand hello difference between codecs and file formats.</span></span>
<span data-ttu-id="9c5da-107">Los códecs son software Hola que implementa los algoritmos de compresión y descompresión de hello, mientras que los formatos de archivo son contenedores que alojan el vídeo comprimido de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c5da-107">Codecs are hello software that implements hello compression/decompression algorithms whereas file formats are containers that hold hello compressed video.</span></span>

<span data-ttu-id="9c5da-108">Servicios multimedia proporciona empaquetado dinámico que permite toodeliver la velocidad de bits adaptativa MP4 o Smooth Streaming con codificación de contenido de transmisión por secuencias formatos admitidos por los servicios multimedia (MPEG DASH, HLS, Smooth Streaming) sin necesidad de toore-package en estos formatos de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="9c5da-108">Media Services provides dynamic packaging which allows you toodeliver your adaptive bitrate MP4 or Smooth Streaming encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) without you having toore-package into these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="9c5da-109">Cuando se crea la cuenta de AMS un **predeterminado** extremo de streaming se agrega la cuenta tooyour Hola **detenido** estado.</span><span class="sxs-lookup"><span data-stu-id="9c5da-109">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="9c5da-110">toostart transmisión por secuencias el contenido y beneficiarse del empaquetado dinámico y cifrado dinámico, Hola extremo de streaming desde el que desea el contenido de toostream tiene toobe Hola **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="9c5da-110">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> <span data-ttu-id="9c5da-111">aprovechar tootake [empaquetado dinámico](media-services-dynamic-packaging-overview.md), necesita toodo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="9c5da-111">tootake advantage of [dynamic packaging](media-services-dynamic-packaging-overview.md), you need toodo hello following:</span></span>
>
><span data-ttu-id="9c5da-112">Además, codificar el archivo de origen en un conjunto de archivos MP4 de velocidad de bits adaptativa o archivos de Smooth Streaming de velocidad de bits adaptativa (más adelante en este tutorial se muestran los pasos de codificación de hello).</span><span class="sxs-lookup"><span data-stu-id="9c5da-112">Also, encode your source file into a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files (hello encoding steps are demonstrated later in this tutorial).</span></span>

<span data-ttu-id="9c5da-113">Servicios multimedia admite siguientes de hello en los codificadores de petición que se describen en este artículo:</span><span class="sxs-lookup"><span data-stu-id="9c5da-113">Media Services supports hello following on demand encoders that are described in this article:</span></span>

* [<span data-ttu-id="9c5da-114">Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="9c5da-114">Media Encoder Standard</span></span>](media-services-encode-asset.md#media-encoder-standard)
* [<span data-ttu-id="9c5da-115">Flujo de trabajo premium de codificación de medios</span><span class="sxs-lookup"><span data-stu-id="9c5da-115">Media Encoder Premium Workflow</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)

<span data-ttu-id="9c5da-116">Este artículo ofrece una breve introducción a petición codificadores de medios y proporciona tooarticles de vínculos que proporcionan información más detallada.</span><span class="sxs-lookup"><span data-stu-id="9c5da-116">This article gives a brief overview of on demand media encoders and provides links tooarticles that give more detailed information.</span></span> <span data-ttu-id="9c5da-117">tema de Hello también proporciona la comparación de codificadores de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c5da-117">hello topic also provides comparison of hello encoders.</span></span>

>[!NOTE]
><span data-ttu-id="9c5da-118">De forma predeterminada cada cuenta de Servicios multimedia puede tener una tarea de codificación activa a la vez.</span><span class="sxs-lookup"><span data-stu-id="9c5da-118">By default each Media Services account can have one active encoding task at a time.</span></span> <span data-ttu-id="9c5da-119">Puede reservar unidades de codificación que le permiten toohave ejecución simultánea, uno para cada unidad reservada de codificación que se adquieren varias tareas de codificación.</span><span class="sxs-lookup"><span data-stu-id="9c5da-119">You can reserve encoding units that allow you toohave multiple encoding tasks running concurrently, one for each encoding reserved unit you purchase.</span></span> <span data-ttu-id="9c5da-120">Para obtener información, consulte [Escalado de unidades de codificación](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c5da-120">For information, see [Scaling encoding units](media-services-scale-media-processing-overview.md).</span></span>

## <a name="media-encoder-standard"></a><span data-ttu-id="9c5da-121">Media Encoder Estándar</span><span class="sxs-lookup"><span data-stu-id="9c5da-121">Media Encoder Standard</span></span>
### <a name="how-toouse"></a><span data-ttu-id="9c5da-122">Cómo toouse</span><span class="sxs-lookup"><span data-stu-id="9c5da-122">How toouse</span></span>
[<span data-ttu-id="9c5da-123">¿Cómo tooencode con Media Encoder estándar</span><span class="sxs-lookup"><span data-stu-id="9c5da-123">How tooencode with Media Encoder Standard</span></span>](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a><span data-ttu-id="9c5da-124">Formatos</span><span class="sxs-lookup"><span data-stu-id="9c5da-124">Formats</span></span>
[<span data-ttu-id="9c5da-125">Códecs y formatos</span><span class="sxs-lookup"><span data-stu-id="9c5da-125">Formats and codecs</span></span>](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a><span data-ttu-id="9c5da-126">Valores preestablecidos</span><span class="sxs-lookup"><span data-stu-id="9c5da-126">Presets</span></span>
<span data-ttu-id="9c5da-127">Media Encoder estándar se configura mediante uno de los valores predefinidos del codificador Hola descritos [aquí](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="9c5da-127">Media Encoder Standard is configured using one of hello encoder presets described [here](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).</span></span>

### <a name="input-and-output-metadata"></a><span data-ttu-id="9c5da-128">Metadatos de entrada y salida</span><span class="sxs-lookup"><span data-stu-id="9c5da-128">Input and output metadata</span></span>
<span data-ttu-id="9c5da-129">Hello codificadores metadatos de entrada se describen [aquí](media-services-input-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9c5da-129">hello encoders input metadata is described [here](media-services-input-metadata-schema.md).</span></span>

<span data-ttu-id="9c5da-130">Hello metadatos de salida de los codificadores se describen [aquí](media-services-output-metadata-schema.md).</span><span class="sxs-lookup"><span data-stu-id="9c5da-130">hello encoders output metadata is described [here](media-services-output-metadata-schema.md).</span></span>

### <a name="generate-thumbnails"></a><span data-ttu-id="9c5da-131">Generación de miniaturas</span><span class="sxs-lookup"><span data-stu-id="9c5da-131">Generate thumbnails</span></span>
<span data-ttu-id="9c5da-132">Para obtener información, consulte [cómo miniaturas de toogenerate utilizando Media Encoder estándar](media-services-advanced-encoding-with-mes.md#thumbnails).</span><span class="sxs-lookup"><span data-stu-id="9c5da-132">For information, see [How toogenerate thumbnails using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).</span></span>

### <a name="trim-videos-clipping"></a><span data-ttu-id="9c5da-133">Recorte de vídeos</span><span class="sxs-lookup"><span data-stu-id="9c5da-133">Trim videos (clipping)</span></span>
<span data-ttu-id="9c5da-134">Para obtener información, consulte [cómo vídeos de tootrim con Media Encoder estándar](media-services-advanced-encoding-with-mes.md#trim_video).</span><span class="sxs-lookup"><span data-stu-id="9c5da-134">For information, see [How tootrim videos using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).</span></span>

### <a name="create-overlays"></a><span data-ttu-id="9c5da-135">Creación de superposiciones</span><span class="sxs-lookup"><span data-stu-id="9c5da-135">Create overlays</span></span>
<span data-ttu-id="9c5da-136">Para obtener información, consulte [cómo toocreate se superpone con Media Encoder estándar](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="9c5da-136">For information, see [How toocreate overlays using Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

### <a name="see-also"></a><span data-ttu-id="9c5da-137">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="9c5da-137">See also</span></span>
[<span data-ttu-id="9c5da-138">blog de servicios multimedia de Hola</span><span class="sxs-lookup"><span data-stu-id="9c5da-138">hello Media Services blog</span></span>](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a><span data-ttu-id="9c5da-139">Flujo de trabajo del Codificador multimedia</span><span class="sxs-lookup"><span data-stu-id="9c5da-139">Media Encoder Premium Workflow</span></span>
### <a name="overview"></a><span data-ttu-id="9c5da-140">Información general</span><span class="sxs-lookup"><span data-stu-id="9c5da-140">Overview</span></span>
[<span data-ttu-id="9c5da-141">Introducción de la codificación Premium en Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="9c5da-141">Introducing Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a><span data-ttu-id="9c5da-142">Cómo toouse</span><span class="sxs-lookup"><span data-stu-id="9c5da-142">How toouse</span></span>
<span data-ttu-id="9c5da-143">El flujo de trabajo del Codificador multimedia Premium se configura mediante flujos de trabajo complejos.</span><span class="sxs-lookup"><span data-stu-id="9c5da-143">Media Encoder Premium Workflow is configured using complex workflows.</span></span> <span data-ttu-id="9c5da-144">Archivos de flujo de trabajo se pudo crear y actualizar con hello [Workflow Designer](media-services-workflow-designer.md) herramienta.</span><span class="sxs-lookup"><span data-stu-id="9c5da-144">Workflow files could be created and updated using hello [Workflow Designer](media-services-workflow-designer.md) tool.</span></span>

[<span data-ttu-id="9c5da-145">¿Cómo tooUse Premium de codificación en servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="9c5da-145">How tooUse Premium Encoding in Azure Media Services</span></span>](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a><span data-ttu-id="9c5da-146">Problemas conocidos</span><span class="sxs-lookup"><span data-stu-id="9c5da-146">Known issues</span></span>
<span data-ttu-id="9c5da-147">Si el vídeo de entrada no contiene subtítulos, Hola salida que activos todavía contendrá un archivo TTML vacío.</span><span class="sxs-lookup"><span data-stu-id="9c5da-147">If your input video does not contain closed captioning, hello output Asset will still contain an empty TTML file.</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="9c5da-148">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="9c5da-148">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9c5da-149">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="9c5da-149">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="9c5da-150">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="9c5da-150">Related articles</span></span>
* [<span data-ttu-id="9c5da-151">Realización de tareas de codificación avanzadas mediante la personalización de valores preestablecidos de Media Encoder Estándar</span><span class="sxs-lookup"><span data-stu-id="9c5da-151">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="9c5da-152">Cuotas y limitaciones</span><span class="sxs-lookup"><span data-stu-id="9c5da-152">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
