---
title: Uso de asociados para proporcionar licencias de Widevine a Azure Media Services | Microsoft Docs
description: "En este artículo se describe cómo puede usar Servicios multimedia de Azure (AMS) para entregar una secuencia que se cifra dinámicamente por AMS con DRM tanto de PlayReady como Widevine. La licencia de PlayReady procede del servidor de licencias PlayReady de Servicios multimedia y la licencia de Widevine se entrega al servidor de licencias de castLabs."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5bcad5a4-c0bb-4871-9cce-808a913c53e6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 6867e4f910970121df3858516c6bab3114c3c6f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="using-partners-to-deliver-widevine-licenses-to-azure-media-services"></a><span data-ttu-id="98daf-104">Uso de partners para entregar licencias de Widevine a Servicios multimedia de Azure</span><span class="sxs-lookup"><span data-stu-id="98daf-104">Using partners to deliver Widevine licenses to Azure Media Services</span></span>
## <a name="overview"></a><span data-ttu-id="98daf-105">Información general</span><span class="sxs-lookup"><span data-stu-id="98daf-105">Overview</span></span>
<span data-ttu-id="98daf-106">Servicios multimedia de Microsoft Azure le permite entregar MPEG-DASH protegido con DRM de Widevine, que se cifra según la especificación de cifrado común (CENC).</span><span class="sxs-lookup"><span data-stu-id="98daf-106">Microsoft Azure Media Services enables you to deliver MPEG-DASH protected with Widevine DRM, which is encrypted per the Common Encryption (CENC) specification.</span></span>

<span data-ttu-id="98daf-107">A partir del SDK de Servicios multimedia para .NET versión 3.5.2, Servicios multimedia permite configurar la plantilla de licencia Widevine y obtener licencias de Widevine.</span><span class="sxs-lookup"><span data-stu-id="98daf-107">Starting with the Media Services .NET SDK version 3.5.2, Media Services enables you to configure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="98daf-108">También puede usar los siguientes asociados de AMS para ayudarle a entregar licencias de Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/) y [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="98daf-108">You can also use the following AMS partners to help you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

## <a name="castlabs"></a><span data-ttu-id="98daf-109">castLabs</span><span class="sxs-lookup"><span data-stu-id="98daf-109">castLabs</span></span>
<span data-ttu-id="98daf-110">Puede usar [castLabs](http://castlabs.com/company/partners/azure/) para entregar licencias Widevine.</span><span class="sxs-lookup"><span data-stu-id="98daf-110">You can use [castLabs](http://castlabs.com/company/partners/azure/) to deliver Widevine licenses.</span></span> <span data-ttu-id="98daf-111">Para obtener más información, consulte [Uso de castLabs para entregar licencias de DRM a Servicios multimedia de Azure](media-services-castlabs-integration.md)</span><span class="sxs-lookup"><span data-stu-id="98daf-111">For more information, see [Using castLabs to deliver DRM licenses to Azure Media Services](media-services-castlabs-integration.md)</span></span>

## <a name="axinom"></a><span data-ttu-id="98daf-112">Axinom</span><span class="sxs-lookup"><span data-stu-id="98daf-112">Axinom</span></span>
<span data-ttu-id="98daf-113">Puede usar [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) para entregar licencias Widevine.</span><span class="sxs-lookup"><span data-stu-id="98daf-113">You can use [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/) to deliver Widevine licenses.</span></span> <span data-ttu-id="98daf-114">Para obtener más información, consulte [Uso de Axinom para entregar licencias de DRM a Servicios multimedia de Azure](media-services-axinom-integration.md)</span><span class="sxs-lookup"><span data-stu-id="98daf-114">For more information, see [Using Axinom to deliver DRM licenses to Azure Media Services](media-services-axinom-integration.md)</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="98daf-115">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="98daf-115">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="98daf-116">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="98daf-116">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="98daf-117">Consulte también</span><span class="sxs-lookup"><span data-stu-id="98daf-117">See also</span></span>
[<span data-ttu-id="98daf-118">Uso de cifrado dinámico común de PlayReady o Widevine.</span><span class="sxs-lookup"><span data-stu-id="98daf-118">Using PlayReady and/or Widevine dynamic common encryption</span></span>](media-services-protect-with-drm.md)

[<span data-ttu-id="98daf-119">Blog de Mingfei</span><span class="sxs-lookup"><span data-stu-id="98daf-119">Mingfei’s blog</span></span>](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/)

