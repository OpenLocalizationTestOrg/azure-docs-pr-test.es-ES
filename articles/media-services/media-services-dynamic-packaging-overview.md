---
title: "Introducción al empaquetado dinámico de Azure Media Services | Microsoft Docs"
description: "El tema proporciona información general sobre el empaquetado dinámico."
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
ms.openlocfilehash: 2d212599302fced3f60085ab30cdeaefc1ee2e6a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="dynamic-packaging"></a><span data-ttu-id="17689-103">Empaquetado dinámico</span><span class="sxs-lookup"><span data-stu-id="17689-103">Dynamic packaging</span></span>
## <a name="overview"></a><span data-ttu-id="17689-104">Información general</span><span class="sxs-lookup"><span data-stu-id="17689-104">Overview</span></span>
<span data-ttu-id="17689-105">Servicios multimedia de Microsoft Azure puede usarse para proporcionar varios formatos de archivo de origen multimedia, formatos de streaming multimedia y formatos de protección de contenido a diversas tecnologías cliente (por ejemplo, iOS, XBOX, Silverlight y Windows 8).</span><span class="sxs-lookup"><span data-stu-id="17689-105">Microsoft Azure Media Services can be used to deliver many media source file formats, media streaming formats, and content protection formats to a variety of client technologies (for example, iOS, XBOX, Silverlight, Windows 8).</span></span> <span data-ttu-id="17689-106">Estos clientes entienden distintos protocolos. Por ejemplo, iOS requiere un formato HTTP Live Streaming (HLS) V4, y Silverlight y Xbox requieren Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="17689-106">These clients understand different protocols, for example iOS requires an HTTP Live Streaming (HLS) V4 format and Silverlight and Xbox require Smooth Streaming.</span></span> <span data-ttu-id="17689-107">Si tiene un conjunto de archivos MP4 (ISO Base Media 14496-12) de velocidad de bits adaptable (varias velocidades de bits) o un conjunto de archivos Smooth Streaming de velocidad de bits adaptable que desea ofrecer a los clientes que entienden MPEG DASH, HLS o Smooth Streaming, puede aprovechar el empaquetado dinámico de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="17689-107">If you have a set of adaptive bitrate (multi-bitrate) MP4 (ISO Base Media 14496-12) files or a set of adaptive bitrate Smooth Streaming files that you want to serve to clients that understand MPEG DASH, HLS or Smooth Streaming, you should take advantage of Media Services dynamic packaging.</span></span>

<span data-ttu-id="17689-108">Con el empaquetado dinámico, lo único que debe hacer es crear un recurso que contenga un conjunto de archivos MP4 de velocidad de bits adaptable o archivos Smooth Streaming de velocidad de bits adaptable.</span><span class="sxs-lookup"><span data-stu-id="17689-108">With dynamic packaging all you need is to create an asset that contains a set of adaptive bitrate MP4 files or adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="17689-109">Luego, según el formato especificado en la solicitud de manifiesto o fragmento, el servidor de streaming a petición se asegurará de que reciba la secuencia en el protocolo elegido.</span><span class="sxs-lookup"><span data-stu-id="17689-109">Then, based on the specified format in the manifest or fragment request, the On-Demand Streaming server will ensure that you receive the stream in the protocol you have chosen.</span></span> <span data-ttu-id="17689-110">Como resultado, solo tendrá que almacenar y pagar los archivos en formato de almacenamiento único y Servicios multimedia creará y proporcionará la respuesta adecuada en función de las solicitudes de un cliente.</span><span class="sxs-lookup"><span data-stu-id="17689-110">As a result, you only need to store and pay for the files in single storage format and Media Services service will build and serve the appropriate response based on requests from a client.</span></span>

<span data-ttu-id="17689-111">El diagrama siguiente muestra el flujo de trabajo de codificación y empaquetado estático tradicionales.</span><span class="sxs-lookup"><span data-stu-id="17689-111">The following diagram shows the traditional encoding and static packaging workflow.</span></span>

![Codificación estática](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

<span data-ttu-id="17689-113">El diagrama siguiente muestra el flujo de trabajo de empaquetado dinámico.</span><span class="sxs-lookup"><span data-stu-id="17689-113">The following diagram shows the dynamic packaging workflow.</span></span>

![Codificación dinámica](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)


## <a name="common-scenario"></a><span data-ttu-id="17689-115">Escenario común</span><span class="sxs-lookup"><span data-stu-id="17689-115">Common scenario</span></span>
1. <span data-ttu-id="17689-116">Cargar un archivo de entrada (llamado archivo intermedio).</span><span class="sxs-lookup"><span data-stu-id="17689-116">Upload an input file (called a mezzanine file).</span></span> <span data-ttu-id="17689-117">Por ejemplo, H.264, MP4 o WMV (para obtener la lista de formatos compatibles, vea [Formatos de Media Encoder Standard](media-services-media-encoder-standard-formats.md)).</span><span class="sxs-lookup"><span data-stu-id="17689-117">For example, H.264, MP4, or WMV (for the list of supported formats see [Formats Supported by the Media Encoder Standard](media-services-media-encoder-standard-formats.md).</span></span>
2. <span data-ttu-id="17689-118">Codificar el archivo intermedio en conjuntos MP4 de velocidad de bits adaptable H.264.</span><span class="sxs-lookup"><span data-stu-id="17689-118">Encode your mezzanine file to H.264 MP4 adaptive bitrate sets.</span></span>
3. <span data-ttu-id="17689-119">Publicar el recurso que contiene el conjunto MP4 de velocidad de bits adaptable mediante la creación del localizador a petición.</span><span class="sxs-lookup"><span data-stu-id="17689-119">Publish the asset that contains the adaptive bitrate MP4 set by creating the On-Demand Locator.</span></span>
4. <span data-ttu-id="17689-120">Compilar las direcciones URL de streaming para obtener acceso al contenido y hacer streaming de este.</span><span class="sxs-lookup"><span data-stu-id="17689-120">Build the streaming URLs to access and stream your content.</span></span>

## <a name="preparing-assets-for-dynamic-streaming"></a><span data-ttu-id="17689-121">Preparación de recursos para el streaming dinámico</span><span class="sxs-lookup"><span data-stu-id="17689-121">Preparing assets for dynamic streaming</span></span>
<span data-ttu-id="17689-122">Si desea preparar el recurso para el streaming dinámico, tiene dos opciones:</span><span class="sxs-lookup"><span data-stu-id="17689-122">To prepare your asset for dynamic streaming you have two options:</span></span>

1. <span data-ttu-id="17689-123">[Cargar un archivo maestro](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="17689-123">[Upload a master file](media-services-dotnet-upload-files.md).</span></span>
2. <span data-ttu-id="17689-124">[Usar el codificador Media Encoder Standard para producir conjuntos MP4 de velocidad de bits adaptable H.264](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="17689-124">[Use the Media Encoder Standard encoder to produce H.264 MP4 adaptive bitrate sets](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>
3. <span data-ttu-id="17689-125">[Transmita el contenido](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="17689-125">[Stream your content](media-services-deliver-content-overview.md).</span></span>

## <span data-ttu-id="17689-126"><a id="unsupported_formats"></a>Formatos no compatibles con el empaquetado dinámico</span><span class="sxs-lookup"><span data-stu-id="17689-126"><a id="unsupported_formats"></a>Formats that are not supported by dynamic packaging</span></span>
<span data-ttu-id="17689-127">El empaquetado dinámico no admite los siguientes formatos de archivo de origen:</span><span class="sxs-lookup"><span data-stu-id="17689-127">The following source file formats are not supported by dynamic packaging.</span></span>

* <span data-ttu-id="17689-128">Archivos MP4 Dolby Digital.</span><span class="sxs-lookup"><span data-stu-id="17689-128">Dolby digital mp4 files.</span></span>
* <span data-ttu-id="17689-129">Archivos MP4 Dolby Digital Smooth.</span><span class="sxs-lookup"><span data-stu-id="17689-129">Dolby digital smooth files.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="17689-130">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="17689-130">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="17689-131">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="17689-131">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

