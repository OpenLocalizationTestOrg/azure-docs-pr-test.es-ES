---
title: "aaaAzure servicios multimedia de preguntas más frecuentes | Documentos de Microsoft"
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
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a><span data-ttu-id="2634d-103">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="2634d-103">Frequently asked questions</span></span>

<span data-ttu-id="2634d-104">Este artículo tratan las preguntas más frecuentes generadas por la Comunidad de usuarios de servicios de multimedia de Azure (AMS) Hola.</span><span class="sxs-lookup"><span data-stu-id="2634d-104">This article addresses frequently asked questions raised by hello Azure Media Services (AMS) user community.</span></span>

## <a name="general-ams-faqs"></a><span data-ttu-id="2634d-105">Preguntas más frecuentes generales sobre AMS</span><span class="sxs-lookup"><span data-stu-id="2634d-105">General AMS FAQs</span></span>
<span data-ttu-id="2634d-106">P: ¿Cómo se escala la indización?</span><span class="sxs-lookup"><span data-stu-id="2634d-106">Q: How do you scale indexing?</span></span>

<span data-ttu-id="2634d-107">R: unidades de hello reservado se Hola mismo para la codificación y tareas de indización.</span><span class="sxs-lookup"><span data-stu-id="2634d-107">A: hello reserved units are hello same for Encoding and Indexing tasks.</span></span> <span data-ttu-id="2634d-108">Siga las instrucciones de [cómo unidades reservadas de codificación tooScale](media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2634d-108">Follow instructions on [How tooScale Encoding Reserved Units](media-services-scale-media-processing-overview.md).</span></span> <span data-ttu-id="2634d-109">**Tenga en cuenta** que el rendimiento del indexador no se ve afectado por el tipo de unidad reservada.</span><span class="sxs-lookup"><span data-stu-id="2634d-109">**Note** that Indexer performance is not affected by Reserved Unit Type.</span></span>

<span data-ttu-id="2634d-110">P: He cargado, codificado y publicado un vídeo.</span><span class="sxs-lookup"><span data-stu-id="2634d-110">Q: I uploaded, encoded, and published a video.</span></span> <span data-ttu-id="2634d-111">¿Lo que sería un vídeo de Hola de hello motivo no se reproduce cuando intento toostream él?</span><span class="sxs-lookup"><span data-stu-id="2634d-111">What would be hello reason hello video does not play when I try toostream it?</span></span>

<span data-ttu-id="2634d-112">R: uno de hello más comunes motivos por los que es no tener Hola origen desde el que está tratando de tooplayback Hola **ejecutando** estado.</span><span class="sxs-lookup"><span data-stu-id="2634d-112">A: One of hello most common reasons is you do not have hello streaming endpoint from which you are trying tooplayback in hello **Running** state.</span></span>  

<span data-ttu-id="2634d-113">P: ¿Puedo realizar una composición en una secuencia en directo?</span><span class="sxs-lookup"><span data-stu-id="2634d-113">Q: Can I do compositing on a live stream?</span></span>

<span data-ttu-id="2634d-114">R: la composición en secuencias en directo no proporciona actualmente en los servicios de multimedia de Azure, lo que deberá toopre-crear en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2634d-114">A: Compositing on live streams is currently not offered in Azure Media Services, so you would need toopre-compose on your computer.</span></span>

<span data-ttu-id="2634d-115">P: ¿Puedo usar CDN de Azure con secuencia en directo?</span><span class="sxs-lookup"><span data-stu-id="2634d-115">Q: Can I use Azure CDN with Live Streaming?</span></span>

<span data-ttu-id="2634d-116">R: servicios multimedia de admite la integración con la red CDN de Azure (para obtener más información, consulte [cómo tooManage los extremos de Streaming en una cuenta de servicios multimedia](media-services-portal-manage-streaming-endpoints.md)).</span><span class="sxs-lookup"><span data-stu-id="2634d-116">A: Media Services supports integration with Azure CDN (for more information, see [How tooManage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)).</span></span>  <span data-ttu-id="2634d-117">Puede usar el streaming en vivo con CDN.</span><span class="sxs-lookup"><span data-stu-id="2634d-117">You can use Live streaming with CDN.</span></span> <span data-ttu-id="2634d-118">Servicios multimedia de Azure proporciona salidas de Smooth Streaming, HLS y MPEG-DASH.</span><span class="sxs-lookup"><span data-stu-id="2634d-118">Azure Media Services provides Smooth Streaming, HLS and MPEG-DASH outputs.</span></span> <span data-ttu-id="2634d-119">Todos estos formatos usan HTTP para transferir datos y obtener beneficios del almacenamiento en caché de HTTP.</span><span class="sxs-lookup"><span data-stu-id="2634d-119">All these formats use HTTP for transferring data and get benefits of HTTP caching.</span></span> <span data-ttu-id="2634d-120">En directo de datos reales de audio/vídeo de transmisión por secuencias es toofragments dividido y se almacene en caché este fragmentos individuales en la red CDN.</span><span class="sxs-lookup"><span data-stu-id="2634d-120">In live streaming actual video/audio data is divided toofragments and this individual fragments get cached in CDN.</span></span> <span data-ttu-id="2634d-121">Solo los toobe de necesidades datos actualizados es datos de manifiesto de saludo.</span><span class="sxs-lookup"><span data-stu-id="2634d-121">Only data needs toobe refreshed is hello manifest data.</span></span> <span data-ttu-id="2634d-122">CDN actualiza periódicamente los datos de manifiesto.</span><span class="sxs-lookup"><span data-stu-id="2634d-122">CDN periodically refreshes manifest data.</span></span>

<span data-ttu-id="2634d-123">P: ¿Los servicios multimedia de Azure admiten el almacenamiento de imágenes?</span><span class="sxs-lookup"><span data-stu-id="2634d-123">Q: Does Azure Media services support storing images?</span></span>

<span data-ttu-id="2634d-124">R: si solo desea toostore JPEG o imágenes PNG, debe mantenerlos de almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="2634d-124">A: If you are just looking toostore JPEG or PNG images, you should keep those in Azure Blob Storage.</span></span> <span data-ttu-id="2634d-125">No hay ningún tooputting de beneficio en los servicios multimedia de la cuenta a menos que desee tookeep que ellos asociados con el vídeo o Audio activos.</span><span class="sxs-lookup"><span data-stu-id="2634d-125">There is no benefit tooputting them in your Media Services account unless you want tookeep them associated with your Video or Audio Assets.</span></span> <span data-ttu-id="2634d-126">O bien, si es posible que tenga una necesidad toouse hello las imágenes como superposiciones de codificador de vídeo de Hola. Media Encoder estándar es compatible con imágenes de capas en la parte superior vídeos, y que es lo que muestra JPEG y PNG como admiten formatos de entrada.</span><span class="sxs-lookup"><span data-stu-id="2634d-126">Or if you might have a need toouse hello images as overlays in hello video encoder.Media Encoder Standard supports overlaying images on top of videos, and that is what it lists JPEG and PNG as supported input formats.</span></span> <span data-ttu-id="2634d-127">Para obtener más información, consulte [Creación de superposiciones](media-services-advanced-encoding-with-mes.md#overlay).</span><span class="sxs-lookup"><span data-stu-id="2634d-127">For more information, see [Creating Overlays](media-services-advanced-encoding-with-mes.md#overlay).</span></span>

<span data-ttu-id="2634d-128">P: ¿Cómo puedo copiar activos de una tooanother de cuenta de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="2634d-128">Q: How can I copy assets from one Media Services account tooanother.</span></span>

<span data-ttu-id="2634d-129">R: toocopy activos de una tooanother de cuenta de servicios multimedia con. NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) método de extensión disponible en hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repositorio.</span><span class="sxs-lookup"><span data-stu-id="2634d-129">A: toocopy assets from one Media Services account tooanother using .NET, use [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) extension method available in hello [Azure Media Services .NET SDK Extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repository.</span></span> <span data-ttu-id="2634d-130">Para obtener más información, consulte [esta](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) conversación del foro.</span><span class="sxs-lookup"><span data-stu-id="2634d-130">For more information, see [this](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum thread.</span></span>

<span data-ttu-id="2634d-131">P: ¿Cuáles son Hola admite caracteres para asignar nombres a archivos cuando se trabaja con AMS?</span><span class="sxs-lookup"><span data-stu-id="2634d-131">Q: What are hello supported characters for naming files when working with AMS?</span></span>

<span data-ttu-id="2634d-132">R: servicios multimedia de usa el valor de Hola de hello IAssetFile.Name propiedad al generar direcciones URL para hello transmisión por secuencias contenido (por ejemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por esta razón, no se permite la codificación porcentual.</span><span class="sxs-lookup"><span data-stu-id="2634d-132">A: Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="2634d-133">Hola valo hello **nombre** propiedad no puede tener cualquiera de los siguientes hello [por ciento reservados a la codificación de caracteres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="2634d-133">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="2634d-134">Además, solo puede haber un "."</span><span class="sxs-lookup"><span data-stu-id="2634d-134">Also, there can only be one ‘.’</span></span> <span data-ttu-id="2634d-135">para la extensión de nombre de archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="2634d-135">for hello file name extension.</span></span>

<span data-ttu-id="2634d-136">P: ¿cómo uso tooconnect REST?</span><span class="sxs-lookup"><span data-stu-id="2634d-136">Q: How tooconnect using REST?</span></span>

<span data-ttu-id="2634d-137">R: para obtener información sobre cómo tooconnect toohello AMS API, consulte [Hola acceso API de servicios multimedia de Azure con autenticación de Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="2634d-137">A: For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> <span data-ttu-id="2634d-138">Después de conectarse correctamente toohttps://media.windows.net, recibirá una redirección 301 especificando otra URI de servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="2634d-138">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="2634d-139">Debe realizar las llamadas subsiguientes toohello nuevo URI.</span><span class="sxs-lookup"><span data-stu-id="2634d-139">You must make subsequent calls toohello new URI.</span></span> 

<span data-ttu-id="2634d-140">P: ¿¿Cómo puedo girar un vídeo durante el proceso de codificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="2634d-140">Q: How can I rotate a video during hello encoding process.</span></span>

<span data-ttu-id="2634d-141">R: Hola [Media Encoder estándar](media-services-dotnet-encode-with-media-encoder-standard.md) admite la rotación de ángulos de 90, 180 y 270.</span><span class="sxs-lookup"><span data-stu-id="2634d-141">A: hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 90/180/270.</span></span> <span data-ttu-id="2634d-142">comportamiento predeterminado de Hello es "Auto", donde intenta toodetect Hola rotación metadatos en el archivo MP4/.mov entrante de Hola y compensar para él.</span><span class="sxs-lookup"><span data-stu-id="2634d-142">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming MP4/MOV file and compensate for it.</span></span> <span data-ttu-id="2634d-143">Hola siguientes **orígenes** tooone de elemento de valores preestablecidos de json de hello definido [aquí](media-services-mes-presets-overview.md):</span><span class="sxs-lookup"><span data-stu-id="2634d-143">Include hello following **Sources** element tooone of hello json presets defined [here](media-services-mes-presets-overview.md):</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="2634d-144">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="2634d-144">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2634d-145">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="2634d-145">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
