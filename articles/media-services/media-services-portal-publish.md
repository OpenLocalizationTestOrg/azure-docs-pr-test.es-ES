---
title: "  Publicación de contenido con Azure Portal | Microsoft Docs"
description: "Este tutorial lo guiará a través de los pasos de publicación de contenidos con el Portal de Azure."
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
ms.openlocfilehash: 68a2fbdda0996cf4ba5ea3b09816bf845af756f4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="publish-content-with-the-azure-portal"></a><span data-ttu-id="657b6-103">Publicación de contenido con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="657b6-103">Publish content with the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="657b6-104">Portal</span><span class="sxs-lookup"><span data-stu-id="657b6-104">Portal</span></span>](media-services-portal-publish.md)
> * [<span data-ttu-id="657b6-105">.NET</span><span class="sxs-lookup"><span data-stu-id="657b6-105">.NET</span></span>](media-services-deliver-streaming-content.md)
> * [<span data-ttu-id="657b6-106">REST</span><span class="sxs-lookup"><span data-stu-id="657b6-106">REST</span></span>](media-services-rest-deliver-streaming-content.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="657b6-107">Información general</span><span class="sxs-lookup"><span data-stu-id="657b6-107">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="657b6-108">Para completar este tutorial, deberá tener una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="657b6-108">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="657b6-109">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="657b6-109">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="657b6-110">Para proporcionar al usuario una dirección URL que pueda utilizarse para transmitir o descargar su contenido, primero necesitará "publicar" su recurso mediante la creación de un localizador.</span><span class="sxs-lookup"><span data-stu-id="657b6-110">To provide your user with a  URL that can be used to stream or download your content, you first need to "publish" your asset by creating a locator.</span></span> <span data-ttu-id="657b6-111">Los localizadores proporcionan acceso a los archivos contenidos en el recurso.</span><span class="sxs-lookup"><span data-stu-id="657b6-111">Locators provide access to files contained in the asset.</span></span> <span data-ttu-id="657b6-112">Media Services admite dos tipos de localizadores:</span><span class="sxs-lookup"><span data-stu-id="657b6-112">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="657b6-113">Los localizadores de streaming (OnDemandOrigin), que se usan en el streaming adaptable (por ejemplo, para transmitir MPEG DASH, HLS o Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="657b6-113">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, to stream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="657b6-114">Para crear un localizador de streaming el recurso debe contener un archivo .ism.</span><span class="sxs-lookup"><span data-stu-id="657b6-114">To create a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="657b6-115">Localizadores (SAS) progresivos, utilizados para la entrega de vídeo mediante descarga progresiva.</span><span class="sxs-lookup"><span data-stu-id="657b6-115">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="657b6-116">Una dirección URL de streaming tiene el siguiente formato y se puede usar para reproducir los recursos de Smooth Streaming:</span><span class="sxs-lookup"><span data-stu-id="657b6-116">A streaming URL has the following format and you can use it to play Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="657b6-117">Para generar una dirección URL de streaming de HLS, anexe (format=m3u8-aapl) a la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="657b6-117">To build an HLS streaming URL, append (format=m3u8-aapl) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="657b6-118">Para generar una dirección URL de streaming de MPEG DASH, anexe (format=mpd-time-csf) a la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="657b6-118">To build an  MPEG DASH streaming URL, append (format=mpd-time-csf) to the URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

<span data-ttu-id="657b6-119">Una dirección URL de SAS tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="657b6-119">A SAS URL has the following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="657b6-120">Para obtener más información, consulte la [introducción a la entrega de contenidos](media-services-deliver-content-overview.md).</span><span class="sxs-lookup"><span data-stu-id="657b6-120">For more information, see [Delivering content overview](media-services-deliver-content-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="657b6-121">Si usó el portal para crear localizadores antes de marzo de 2015, se crearon localizadores con una fecha de caducidad de dos años.</span><span class="sxs-lookup"><span data-stu-id="657b6-121">If you used the portal to create locators before March 2015, locators with a two year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="657b6-122">Para actualizar la fecha de caducidad de un localizador, use las API de [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) o de [.NET](http://go.microsoft.com/fwlink/?LinkID=533259).</span><span class="sxs-lookup"><span data-stu-id="657b6-122">To update an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="657b6-123">Tenga en cuenta que, cuando se actualiza la fecha de caducidad de un localizador de SAS, cambia la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="657b6-123">Note that when you update the expiration date of a SAS locator, the URL changes.</span></span>

### <a name="to-use-the-portal-to-publish-an-asset"></a><span data-ttu-id="657b6-124">Uso del portal para publicar un recurso</span><span class="sxs-lookup"><span data-stu-id="657b6-124">To use the portal to publish an asset</span></span>
<span data-ttu-id="657b6-125">Para usar el portal para publicar un recurso, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="657b6-125">To use the portal to publish an asset, do the following:</span></span>

1. <span data-ttu-id="657b6-126">En [Azure Portal](https://portal.azure.com/), seleccione la cuenta de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="657b6-126">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="657b6-127">Seleccione **Configuración** > **Activos**.</span><span class="sxs-lookup"><span data-stu-id="657b6-127">Select **Settings** > **Assets**.</span></span>
3. <span data-ttu-id="657b6-128">Seleccione el recurso que desea publicar.</span><span class="sxs-lookup"><span data-stu-id="657b6-128">Select the asset that you want to publish.</span></span>
4. <span data-ttu-id="657b6-129">Haga clic en el botón **Publicar** .</span><span class="sxs-lookup"><span data-stu-id="657b6-129">Click the **Publish** button.</span></span>
5. <span data-ttu-id="657b6-130">Seleccione el tipo de localizador.</span><span class="sxs-lookup"><span data-stu-id="657b6-130">Select the locator type.</span></span>
6. <span data-ttu-id="657b6-131">Presione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="657b6-131">Press **Add**.</span></span>
   
    ![Publicar](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="657b6-133">La dirección URL se agregará a la lista de **direcciones URL publicadas**.</span><span class="sxs-lookup"><span data-stu-id="657b6-133">The URL will be added to the list of **Published URLs**.</span></span>

## <a name="play-content-from-the-portal"></a><span data-ttu-id="657b6-134">contenido desde el portal</span><span class="sxs-lookup"><span data-stu-id="657b6-134">Play content from the portal</span></span>
<span data-ttu-id="657b6-135">Azure Portal proporciona un reproductor de contenido que puede usar para probar el vídeo.</span><span class="sxs-lookup"><span data-stu-id="657b6-135">The Azure portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="657b6-136">Haga clic en el vídeo deseado y, luego, en el botón **Reproducir** .</span><span class="sxs-lookup"><span data-stu-id="657b6-136">Click the desired video and then click the **Play** button.</span></span>

![Publicar](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="657b6-138">Se aplican algunas consideraciones:</span><span class="sxs-lookup"><span data-stu-id="657b6-138">Some considerations apply:</span></span>

* <span data-ttu-id="657b6-139">Asegúrese de que se ha publicado el vídeo.</span><span class="sxs-lookup"><span data-stu-id="657b6-139">Make sure the video has been published.</span></span>
* <span data-ttu-id="657b6-140">**Media player** reproduce desde el punto de conexión de streaming predeterminado.</span><span class="sxs-lookup"><span data-stu-id="657b6-140">This **Media player** plays from the default streaming endpoint.</span></span> <span data-ttu-id="657b6-141">Si desea reproducir desde un punto de conexión de streaming que no esté predeterminado, haga clic para copiar la dirección URL y use otro reproductor.</span><span class="sxs-lookup"><span data-stu-id="657b6-141">If you want to play from a non-default streaming endpoint, click to copy the URL and use another player.</span></span> <span data-ttu-id="657b6-142">Por ejemplo, el [Reproductor de Servicios multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="657b6-142">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
* <span data-ttu-id="657b6-143">Debe estar ejecutándose el punto de conexión de streaming desde el que está realizando una operación de streaming.</span><span class="sxs-lookup"><span data-stu-id="657b6-143">The streaming endpoint from which you are streaming must be running.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="657b6-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="657b6-144">Next steps</span></span>
<span data-ttu-id="657b6-145">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="657b6-145">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="657b6-146">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="657b6-146">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

