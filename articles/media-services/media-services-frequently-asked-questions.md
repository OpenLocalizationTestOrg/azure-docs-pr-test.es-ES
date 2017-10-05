---
title: "Azure Media Services: Preguntas más frecuentes (P+F) | Microsoft Docs"
description: "Preguntas más frecuentes (P+F)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 48f3924d44a084d61c1d38002cd5098094001acb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="24be1-103">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="24be1-103">Frequently asked questions</span></span>

<span data-ttu-id="24be1-104">En este artículo tratan las preguntas más frecuentes planteadas por la comunidad de usuarios de Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="24be1-104">This article addresses frequently asked questions raised by the Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="24be1-105">Preguntas más frecuentes generales sobre AMS</span><span class="sxs-lookup"><span data-stu-id="24be1-105">General AMS FAQs</span></span>
<span data-ttu-id="24be1-106">P: ¿Cómo se escala la indización?</span><span class="sxs-lookup"><span data-stu-id="24be1-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="24be1-107">R: las unidades reservadas son las mismas para las tareas de codificación y de indización.</span><span class="sxs-lookup"><span data-stu-id="24be1-107">A: The reserved units are the same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="24be1-108">Siga las instrucciones de [Escalado de unidades reservadas de codificación](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="24be1-108">Follow instructions on [How to Scale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="24be1-109">**Tenga en cuenta** que el rendimiento del indexador no se ve afectado por el tipo de unidad reservada.</span><span class="sxs-lookup"><span data-stu-id="24be1-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="24be1-110">P: He cargado, codificado y publicado un vídeo.</span><span class="sxs-lookup"><span data-stu-id="24be1-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="24be1-111">¿Cuál es el motivo por el que el vídeo no se reproduce cuando intento transmitirlo?</span><span class="sxs-lookup"><span data-stu-id="24be1-111">What would be the reason the video does not play when I try to stream it?</span></span>

<span data-ttu-id="24be1-112">R: Uno de los motivos más habituales es que no tiene el punto de conexión de streaming desde el que está intentando reproducir en estado **Running** (en ejecución).</span><span class="sxs-lookup"><span data-stu-id="24be1-112">A: One of the most common reasons is you do not have the streaming endpoint from which you are trying to playback in the **Running** state.</span></span>  

<span data-ttu-id="24be1-113">P: ¿Puedo realizar una composición en una secuencia en directo?</span><span class="sxs-lookup"><span data-stu-id="24be1-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="24be1-114">R: no se ofrece actualmente la composición en secuencias en vivo en Servicios multimedia de Azure, por lo que tendrá que realizar una composición previa en el equipo.</span><span class="sxs-lookup"><span data-stu-id="24be1-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need to pre-compose on your computer.</span></span>

<span data-ttu-id="24be1-115">P: ¿Puedo usar CDN de Azure con secuencia en directo?</span><span class="sxs-lookup"><span data-stu-id="24be1-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="24be1-116">R: servicios multimedia admite la integración con CDN de Azure (para obtener más información, consulte [Administración de extremos de streaming en una cuenta de Servicios multimedia](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="24be1-116">A: Media Services supports integration with Azure CDN (for more information, see [How to Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="24be1-117">Puede usar el streaming en vivo con CDN.</span><span class="sxs-lookup"><span data-stu-id="24be1-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="24be1-118">Servicios multimedia de Azure proporciona salidas de Smooth Streaming, HLS y MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="24be1-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="24be1-119">Todos estos formatos usan HTTP para transferir datos y obtener beneficios del almacenamiento en caché de HTTP.</span><span class="sxs-lookup"><span data-stu-id="24be1-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="24be1-120">En la transmisión en vivo, los datos de audio/vídeo reales se dividen en fragmentos y los fragmentos individuales se almacenan en caché en CDN.</span><span class="sxs-lookup"><span data-stu-id="24be1-120">In live streaming actual video/audio data is divided to fragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="24be1-121">Solo tienen que actualizarse los datos de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="24be1-121">Only data needs to be refreshed is the manifest data.</span></span> <span data-ttu-id="24be1-122">CDN actualiza periódicamente los datos de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="24be1-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="24be1-123">P: ¿Los servicios multimedia de Azure admiten el almacenamiento de imágenes?</span><span class="sxs-lookup"><span data-stu-id="24be1-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="24be1-124">R: si solo busca almacenar las imágenes JPEG o PNG, debe mantenerlas en Almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="24be1-124">A: If you are just looking to store JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="24be1-125">No supone una ventaja si se colocan en la cuenta de Servicios multimedia a menos que desee mantenerlas asociadas a los recursos de vídeo o audio.</span><span class="sxs-lookup"><span data-stu-id="24be1-125">There is no benefit to putting them in your Media Services account unless you want to keep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="24be1-126">O bien, si puede tener la necesidad de usar las imágenes como superposiciones en el codificador de vídeo, el Estándar de codificador multimedia admite la superposición de las imágenes encima de los vídeos, por eso muestra JPEG y PNG como formatos de entrada admitidos.</span><span class="sxs-lookup"><span data-stu-id="24be1-126">Or if you might have a need to use the images as overlays in the video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="24be1-127">Para obtener más información, consulte [Creación de superposiciones](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="24be1-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="24be1-128">P: ¿Cómo puedo copiar recursos de una cuenta de Servicios multimedia a otra?</span><span class="sxs-lookup"><span data-stu-id="24be1-128">Q: How can I copy assets from one Media Services account to another.</span></span>

<span data-ttu-id="24be1-129">R: Para copiar recursos de una cuenta de Media Services a otra mediante .NET, use el método de extensión [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) disponible en el repositorio de [extensiones del SDK de .NET para Azure Media Services](https://github.com/Azure/azure-sdk-for-media-services-extensions/).</span><span class="sxs-lookup"><span data-stu-id="24be1-129">A: To copy assets from one Media Services account to another using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in the [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="24be1-130">Para obtener más información, consulte [esta](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) conversación del foro.</span><span class="sxs-lookup"><span data-stu-id="24be1-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="24be1-131">P: ¿Cuáles son los caracteres admitidos para nombrar los archivos cuando se trabaja con AMS?</span><span class="sxs-lookup"><span data-stu-id="24be1-131">Q: What are the supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="24be1-132">R: Media Services usa el valor de la propiedad IAssetFile.Name al generar direcciones URL para el contenido de streaming (por ejemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters). Por esta razón, no se permite la codificación porcentual.</span><span class="sxs-lookup"><span data-stu-id="24be1-132">A: Media Services uses the value of the IAssetFile.Name property when building URLs for the streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="24be1-133">El valor de la propiedad **Name**no puede tener ninguno de los siguientes [caracteres reservados para la codificación porcentual](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):!*'();:@&=+$,/?%#[]" </span><span class="sxs-lookup"><span data-stu-id="24be1-133">The value of the **Name** property cannot have any of the following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="24be1-134">Además, solo puede haber un "."</span><span class="sxs-lookup"><span data-stu-id="24be1-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="24be1-135">Además, solo puede haber un '.' para la extensión del nombre de archivo.</span><span class="sxs-lookup"><span data-stu-id="24be1-135">for the file name extension.</span></span>

<span data-ttu-id="24be1-136">P: ¿Cómo se realiza la conexión con REST?</span><span class="sxs-lookup"><span data-stu-id="24be1-136">Q: How to connect using REST?</span></span>

<span data-ttu-id="24be1-137">R: Para más información sobre cómo conectarse a la API de Azure Media Services, vea [Acceso a Azure Media Services API con la autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="24be1-137">A: For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="24be1-138">Después de conectarse correctamente a https://media.windows.net, recibirá una redirección 301 que especifica otro URI de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="24be1-138">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="24be1-139">Debe realizar las llamadas posteriores al nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="24be1-139">You must make subsequent calls to the new URI.</span></span> 

<span data-ttu-id="24be1-140">P: ¿Cómo puedo girar un vídeo durante el proceso de codificación?</span><span class="sxs-lookup"><span data-stu-id="24be1-140">Q: How can I rotate a video during the encoding process.</span></span>

<span data-ttu-id="24be1-141">R: [Media Encoder Estándar](media-services-dotnet-encode-with-media-encoder-standard.md) admite ángulos de rotación de 90, 180 o 270.</span><span class="sxs-lookup"><span data-stu-id="24be1-141">A: The [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="24be1-142">El comportamiento predeterminado es "Auto", en el que se intentan detectar los metadatos de rotación del archivo MP4 o MOV entrante y la compensación.</span><span class="sxs-lookup"><span data-stu-id="24be1-142">The default behavior is "Auto", where it tries to detect the rotation metadata in the incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="24be1-143">Incluya el siguiente elemento **Sources** en uno de los valores preestablecidos JSON definidos [aquí](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="24be1-143">Include the following **Sources** element to one of the json presets defined [here](media-services-mes-presets-overview.md):</span></span>

    "Version": 1.0,
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


## <a name="media-services-learning-paths"></a><span data-ttu-id="24be1-144">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="24be1-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="24be1-145">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="24be1-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
