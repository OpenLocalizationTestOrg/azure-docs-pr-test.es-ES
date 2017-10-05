---
title: Uso de reproductores existentes para reproducir el contenido - Azure | Microsoft Docs
description: En este tema se enumeran los reproductores existentes que puede usar para reproducir el contenido.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7e9fcf89-0fb6-4fa4-96cb-666320684d69
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako
ms.openlocfilehash: 48f373b013b1192c353352b801876d706d91dd28
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="playing-your-content-with-existing-players"></a><span data-ttu-id="94c9d-103">Reproducción de contenido con existentes</span><span class="sxs-lookup"><span data-stu-id="94c9d-103">Playing your content with existing players</span></span>
<span data-ttu-id="94c9d-104">Servicios multimedia de Azure admite muchos formatos de streaming populares como Smooth Streaming, HTTP Live Streaming y MPEG-Dash.</span><span class="sxs-lookup"><span data-stu-id="94c9d-104">Azure Media Services supports many popular streaming formats, such as Smooth Streaming, HTTP Live Streaming, and MPEG-Dash.</span></span> <span data-ttu-id="94c9d-105">Este tema remite a reproductores existentes que puede usar para probar sus transmisiones.</span><span class="sxs-lookup"><span data-stu-id="94c9d-105">This topic points you to existing players that you can use to test your streams.</span></span>

### <a name="the-azure-portal-media-services-content-player"></a><span data-ttu-id="94c9d-106">Reproductor del contenido de Media Services de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="94c9d-106">The Azure portal Media Services content player</span></span>
<span data-ttu-id="94c9d-107">**Azure Portal** proporciona un reproductor de contenido que puede usar para probar el vídeo.</span><span class="sxs-lookup"><span data-stu-id="94c9d-107">The **Azure** portal provides a content player that you can use to test your video.</span></span>

<span data-ttu-id="94c9d-108">Haga clic en el vídeo deseado (asegúrese de que se ha [publicado](media-services-portal-publish.md)) y haga clic en el botón **Reproducir** situado en la parte inferior del portal.</span><span class="sxs-lookup"><span data-stu-id="94c9d-108">Click on the desired video (make sure it was [published](media-services-portal-publish.md)) and click the **Play** button at the bottom of the portal.</span></span>

<span data-ttu-id="94c9d-109">Se aplican algunas consideraciones:</span><span class="sxs-lookup"><span data-stu-id="94c9d-109">Some considerations apply:</span></span>

* <span data-ttu-id="94c9d-110">El **REPRODUCTOR DE CONTENIDO DE SERVICIOS MULTIMEDIA** reproduce desde el extremo de streaming predeterminado.</span><span class="sxs-lookup"><span data-stu-id="94c9d-110">The **MEDIA SERVICES CONTENT PLAYER** plays from the default streaming endpoint.</span></span> <span data-ttu-id="94c9d-111">Si desea reproducir desde un extremo de streaming que no esté predeterminado, use otro reproductor.</span><span class="sxs-lookup"><span data-stu-id="94c9d-111">If you want to play from a non-default streaming endpoint, use another player.</span></span> <span data-ttu-id="94c9d-112">Por ejemplo, [Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="94c9d-112">For example, [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

![AMSPlayer][AMSPlayer]

### <a name="azure-media-player"></a><span data-ttu-id="94c9d-114">Reproductor multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="94c9d-114">Azure Media Player</span></span>
<span data-ttu-id="94c9d-115">Use el [Reproductor multimedia de Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html) para reproducir el contenido (libre o protegido) en cualquiera de los siguientes formatos:</span><span class="sxs-lookup"><span data-stu-id="94c9d-115">Use [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) to playback your content (clear or protected) in any of the following formats:</span></span>

* <span data-ttu-id="94c9d-116">Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="94c9d-116">Smooth Streaming</span></span>
* <span data-ttu-id="94c9d-117">MPEG DASH</span><span class="sxs-lookup"><span data-stu-id="94c9d-117">MPEG DASH</span></span>
* <span data-ttu-id="94c9d-118">HLS</span><span class="sxs-lookup"><span data-stu-id="94c9d-118">HLS</span></span>
* <span data-ttu-id="94c9d-119">MP4 progresivo</span><span class="sxs-lookup"><span data-stu-id="94c9d-119">Progressive MP4</span></span>

### <a name="flash-player"></a><span data-ttu-id="94c9d-120">Flash Player</span><span class="sxs-lookup"><span data-stu-id="94c9d-120">Flash Player</span></span>
#### <a name="aes-encrypted-with-token"></a><span data-ttu-id="94c9d-121">Cifrado de AES con token</span><span class="sxs-lookup"><span data-stu-id="94c9d-121">AES-encrypted with Token</span></span>
[<span data-ttu-id="94c9d-122">http://aestoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="94c9d-122">http://aestoken.azurewebsites.net</span></span>](http://aestoken.azurewebsites.net)

### <a name="silverlight-players"></a><span data-ttu-id="94c9d-123">Reproductores de Silverlight</span><span class="sxs-lookup"><span data-stu-id="94c9d-123">Silverlight Players</span></span>
#### <a name="monitoring"></a><span data-ttu-id="94c9d-124">Supervisión</span><span class="sxs-lookup"><span data-stu-id="94c9d-124">Monitoring</span></span>
[<span data-ttu-id="94c9d-125">http://smf.cloudapp.net/healthmonitor</span><span class="sxs-lookup"><span data-stu-id="94c9d-125">http://smf.cloudapp.net/healthmonitor</span></span>](http://smf.cloudapp.net/healthmonitor)

#### <a name="playready-with-token"></a><span data-ttu-id="94c9d-126">PlayReady con token</span><span class="sxs-lookup"><span data-stu-id="94c9d-126">PlayReady with Token</span></span>
[<span data-ttu-id="94c9d-127">http://sltoken.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="94c9d-127">http://sltoken.azurewebsites.net</span></span>](http://sltoken.azurewebsites.net)

### <a name="dash-players"></a><span data-ttu-id="94c9d-128">Reproductores DASH</span><span class="sxs-lookup"><span data-stu-id="94c9d-128">DASH Players</span></span>
[<span data-ttu-id="94c9d-129">http://dashplayer.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="94c9d-129">http://dashplayer.azurewebsites.net</span></span>](http://dashplayer.azurewebsites.net)

[<span data-ttu-id="94c9d-130">http://dashif.org</span><span class="sxs-lookup"><span data-stu-id="94c9d-130">http://dashif.org</span></span>](http://dashif.org)

### <a name="other"></a><span data-ttu-id="94c9d-131">Otros</span><span class="sxs-lookup"><span data-stu-id="94c9d-131">Other</span></span>
<span data-ttu-id="94c9d-132">Para probar las direcciones URL de HLS también puede utilizar:</span><span class="sxs-lookup"><span data-stu-id="94c9d-132">To test HLS URLs you can also use:</span></span>

* <span data-ttu-id="94c9d-133">**Safari** en un dispositivo iOS o</span><span class="sxs-lookup"><span data-stu-id="94c9d-133">**Safari** on an iOS device or</span></span>
* <span data-ttu-id="94c9d-134">**3ivx HLS Player** en Windows.</span><span class="sxs-lookup"><span data-stu-id="94c9d-134">**3ivx HLS Player** on Windows.</span></span>

## <a name="developing-video-players"></a><span data-ttu-id="94c9d-135">Desarrollo de reproductores de vídeo</span><span class="sxs-lookup"><span data-stu-id="94c9d-135">Developing video players</span></span>
<span data-ttu-id="94c9d-136">Para obtener información sobre cómo desarrollar sus propios reproductores, consulte [Desarrollo de reproductores de vídeo](media-services-develop-video-players.md)</span><span class="sxs-lookup"><span data-stu-id="94c9d-136">For information about how to develop your own players, see [Developing video players](media-services-develop-video-players.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="94c9d-137">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="94c9d-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="94c9d-138">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="94c9d-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[AMSPlayer]: ./media/media-services-playback-content-with-existing-players/media-services-portal-player.png
