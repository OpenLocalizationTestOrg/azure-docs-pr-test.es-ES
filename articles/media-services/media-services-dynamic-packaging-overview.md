---
title: "información general sobre el empaquetado dinámico de servicios multimedia aaaAzure | Documentos de Microsoft"
description: "Hola tema proporciona y visión general de los paquetes dinámicos."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0d9e4f54-5daa-45c1-bfaa-cf09ca89b812
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 970e24eba800e098774172c87f56629430b227a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="d786e-103">Empaquetado dinámico</span><span class="sxs-lookup"><span data-stu-id="d786e-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="d786e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d786e-104">Overview</span></span>
<span data-ttu-id="d786e-105">Servicios de multimedia de Microsoft Azure puede ser usado toodeliver origen multimedia muchos formatos de archivo, formatos de transmisión por secuencias de multimedia y formatos de protección de contenido tooa gran variedad de tecnologías de cliente (por ejemplo, iOS, XBOX, Silverlight, Windows 8).</span><span class="sxs-lookup"><span data-stu-id="d786e-105">Microsoft Azure Media Services can be used toodeliver many media source file formats, media streaming formats, and content protection formats tooa variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="d786e-106">Estos clientes entienden distintos protocolos. Por ejemplo, iOS requiere un formato HTTP Live Streaming (HLS) V4, y Silverlight y Xbox requieren Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="d786e-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="d786e-107">Si tiene un conjunto de velocidad de bits adaptativa (velocidades de bits) MP4 archivos (ISO Base Media 14496-12) o un conjunto de archivos de Smooth Streaming de velocidad de bits adaptativa que desea tooclients tooserve que entienden MPEG DASH, HLS o Smooth Streaming, le conviene aprovechar de medios Servicios de empaquetado dinámico.</span><span class="sxs-lookup"><span data-stu-id="d786e-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want tooserve tooclients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="d786e-108">Con el empaquetado dinámico todo lo que necesita es toocreate un activo que contiene un conjunto de archivos MP4 de velocidad de bits adaptativa o archivos de Smooth Streaming de velocidad de bits adaptativa.</span><span class="sxs-lookup"><span data-stu-id="d786e-108">With dynamic packaging all you need is toocreate an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="d786e-109">A continuación, según Hola formato especificado en el manifiesto de Hola o fragmentar la solicitud, Hola servidor se asegurará de que recibe Hola transmisión por secuencias de protocolo de Hola que ha elegido el Streaming a petición.</span><span class="sxs-lookup"><span data-stu-id="d786e-109">Then, based on hello specified format in hello manifest or fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="d786e-110">Como resultado, solo tendrá toostore y pago para los archivos de hello en formato de almacenamiento único y el servicio de servicios multimedia creará y proporcionará la respuesta adecuada Hola según las solicitudes de un cliente.</span><span class="sxs-lookup"><span data-stu-id="d786e-110">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="d786e-111">Hello siguiente diagrama muestra la codificación tradicional de Hola y flujo de trabajo de empaquetado estático.</span><span class="sxs-lookup"><span data-stu-id="d786e-111">hello following diagram shows hello traditional encoding and static packaging workflow.</span></span>

![Codificación estática](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="d786e-113">Hello siguiente diagrama muestra el flujo de trabajo de hello empaquetado dinámico.</span><span class="sxs-lookup"><span data-stu-id="d786e-113">hello following diagram shows hello dynamic packaging workflow.</span></span>

![Codificación dinámica](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="d786e-115">Escenario común</span><span class="sxs-lookup"><span data-stu-id="d786e-115">Common scenario</span></span>
1. <span data-ttu-id="d786e-116">Cargar un archivo de entrada (llamado archivo intermedio).</span><span class="sxs-lookup"><span data-stu-id="d786e-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="d786e-117">Por ejemplo, H.264, MP4 o WMV (consulte lista de Hola de formatos admitidos [formatos compatibles con hello Media Encoder estándar](media-services-media-encoder-standard-formats.md).</span><span class="sxs-lookup"><span data-stu-id="d786e-117">For example, H.264, MP4, or WMV (for hello list of supported formats see [Formats Supported by hello Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="d786e-118">Codificar los conjuntos de velocidad de bits adaptativa mezzanine tooH.264 MP4 de archivo.</span><span class="sxs-lookup"><span data-stu-id="d786e-118">Encode your mezzanine file tooH.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="d786e-119">Publicar el recurso de Hola que contiene Hola velocidad de bits adaptativa MP4 establecido mediante la creación de hello localizador a petición.</span><span class="sxs-lookup"><span data-stu-id="d786e-119">Publish hello asset that contains hello adaptive bitrate MP4 set by creating hello On-Demand Locator.</span></span>
4. <span data-ttu-id="d786e-120">Compile hello tooaccess de direcciones URL de streaming y transmitir el contenido.</span><span class="sxs-lookup"><span data-stu-id="d786e-120">Build hello streaming URLs tooaccess and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="d786e-121">Preparación de recursos para el streaming dinámico</span><span class="sxs-lookup"><span data-stu-id="d786e-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="d786e-122">tooprepare su activo para dinámicas de transmisión por secuencias se tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="d786e-122">tooprepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="d786e-123">[Cargar un archivo maestro](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="d786e-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="d786e-124">[Usar conjuntos de velocidad de bits adaptativa de codificador Media Encoder estándar de hello tooproduce MP4 H.264](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="d786e-124">[Use hello Media Encoder Standard encoder tooproduce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="d786e-125">[Transmita el contenido](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d786e-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="d786e-126"><a id="unsupported_formats"></a>Formatos no compatibles con el empaquetado dinámico</span><span class="sxs-lookup"><span data-stu-id="d786e-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="d786e-127">Hello siguientes formatos de archivo de origen no se admiten con el empaquetado dinámico.</span><span class="sxs-lookup"><span data-stu-id="d786e-127">hello following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="d786e-128">Archivos MP4 Dolby Digital.</span><span class="sxs-lookup"><span data-stu-id="d786e-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="d786e-129">Archivos MP4 Dolby Digital Smooth.</span><span class="sxs-lookup"><span data-stu-id="d786e-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d786e-130">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="d786e-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d786e-131">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="d786e-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

