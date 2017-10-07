---
title: aaa"publicar contenido con hello portal de Azure | Documentos de Microsoft"
description: "Este tutorial le guiará por los pasos de saludo de la publicación del contenido con hello portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 92c364eb-5a5f-4f4e-8816-b162c031bb40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: a7a3867a6939b4b9da883176c6cc20c99d6c54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="publish-content-with-hello-azure-portal"></a><span data-ttu-id="37491-103">Publicar contenido con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="37491-103">Publish content with hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37491-104">Portal</span><span class="sxs-lookup"><span data-stu-id="37491-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="37491-105">.NET</span><span class="sxs-lookup"><span data-stu-id="37491-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="37491-106">REST</span><span class="sxs-lookup"><span data-stu-id="37491-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="37491-107">Información general</span><span class="sxs-lookup"><span data-stu-id="37491-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="37491-108">toocomplete este tutorial, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="37491-108">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="37491-109">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37491-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="37491-110">tooprovide el usuario con una dirección URL que puede ser toostream usado o descargar el contenido, primero necesita demasiado "publicar" su activo mediante la creación de un localizador.</span><span class="sxs-lookup"><span data-stu-id="37491-110">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="37491-111">Los localizadores proporcionan toofiles de acceso que contiene el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="37491-111">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="37491-112">Media Services admite dos tipos de localizadores:</span><span class="sxs-lookup"><span data-stu-id="37491-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="37491-113">Transmisión por secuencias localizadores (OnDemandOrigin), que se usan para streaming adaptable (por ejemplo, toostream MPEG DASH, HLS o Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="37491-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="37491-114">toocreate un localizador de streaming el activo debe contener un archivo .ism.</span><span class="sxs-lookup"><span data-stu-id="37491-114">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="37491-115">Localizadores (SAS) progresivos, utilizados para la entrega de vídeo mediante descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="37491-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="37491-116">Una dirección URL de streaming tiene Hola siguiendo el formato y se pueden usar recursos de Smooth Streaming tooplay.</span><span class="sxs-lookup"><span data-stu-id="37491-116">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="37491-117">Anexar toobuild una transmisión por secuencias de dirección URL, de HLS (formato = m3u8-aapl) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="37491-117">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="37491-118">Anexar toobuild una dirección URL de streaming de MPEG DASH (formato = mpd: tiempo-csf) toohello URL.</span><span class="sxs-lookup"><span data-stu-id="37491-118">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="37491-119">Una dirección URL SAS tiene Hola siguiendo el formato.</span><span class="sxs-lookup"><span data-stu-id="37491-119">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="37491-120">Para obtener más información, consulte la [introducción a la entrega de contenidos](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="37491-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="37491-121">Si utiliza los localizadores de hello toocreate portal antes de marzo de 2015, se crearon localizadores con una fecha de expiración de dos años.</span><span class="sxs-lookup"><span data-stu-id="37491-121">If you used hello portal toocreate locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="37491-122">tooupdate una fecha de caducidad en un localizador, utilice [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API.</span><span class="sxs-lookup"><span data-stu-id="37491-122">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="37491-123">Tenga en cuenta que cuando se actualiza la fecha de expiración de Hola de un localizador SAS, dirección URL de hello cambia.</span><span class="sxs-lookup"><span data-stu-id="37491-123">Note that when you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="37491-124">toouse Hola portal toopublish un activo</span><span class="sxs-lookup"><span data-stu-id="37491-124">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="37491-125">toouse Hola portal toopublish un activo, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="37491-125">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="37491-126">Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="37491-126">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="37491-127">Seleccione **Configuración** > **Activos**.</span><span class="sxs-lookup"><span data-stu-id="37491-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="37491-128">Seleccione activo de Hola que desea toopublish.</span><span class="sxs-lookup"><span data-stu-id="37491-128">Select hello asset that you want toopublish.</span></span>
4. <span data-ttu-id="37491-129">Haga clic en hello **publicar** botón.</span><span class="sxs-lookup"><span data-stu-id="37491-129">Click hello **Publish** button.</span></span>
5. <span data-ttu-id="37491-130">Seleccione el tipo de localizador de Hola.</span><span class="sxs-lookup"><span data-stu-id="37491-130">Select hello locator type.</span></span>
6. <span data-ttu-id="37491-131">Presione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="37491-131">Press **Add**.</span></span>
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="37491-133">dirección URL de Hola se agregarán toohello lista de **publicado direcciones URL**.</span><span class="sxs-lookup"><span data-stu-id="37491-133">hello URL will be added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="37491-134">Reproducir contenido del portal de Hola</span><span class="sxs-lookup"><span data-stu-id="37491-134">Play content from hello portal</span></span>
<span data-ttu-id="37491-135">Hello portal de Azure proporciona un Reproductor de contenido que se puede usar tootest el vídeo.</span><span class="sxs-lookup"><span data-stu-id="37491-135">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="37491-136">Haga clic en vídeo de hello deseado y, a continuación, haga clic en hello **reproducir** botón.</span><span class="sxs-lookup"><span data-stu-id="37491-136">Click hello desired video and then click hello **Play** button.</span></span>

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="37491-138">Se aplican algunas consideraciones:</span><span class="sxs-lookup"><span data-stu-id="37491-138">Some considerations apply:</span></span>

* <span data-ttu-id="37491-139">Asegúrese de que se ha publicado Hola vídeo.</span><span class="sxs-lookup"><span data-stu-id="37491-139">Make sure hello video has been published.</span></span>
* <span data-ttu-id="37491-140">Esto **Reproductor** reproduce desde predeterminado Hola extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="37491-140">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="37491-141">Si desea que tooplay de un valor no predeterminado del origen, haga clic en la dirección URL de hello toocopy y utilice otro reproductor.</span><span class="sxs-lookup"><span data-stu-id="37491-141">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="37491-142">Por ejemplo, [Reproductor de Azure Media Services](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="37491-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="37491-143">Hola origen desde el que está transmitiendo por secuencias debe estar ejecutándose.</span><span class="sxs-lookup"><span data-stu-id="37491-143">hello streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="37491-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37491-144">Next steps</span></span>
<span data-ttu-id="37491-145">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="37491-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="37491-146">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="37491-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

