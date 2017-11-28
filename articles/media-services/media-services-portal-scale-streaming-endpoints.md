---
title: aaaScale streaming extremos con hello portal de Azure | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de ajuste de escala en los extremos de streaming con hello portal de Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1008b3a3-2fa1-4146-85bd-2cf43cd1e00e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: e466edf9232558b9e270f54ee2849cd9b22ad121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="scale-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="b2e47-103">Escalar los extremos de streaming con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b2e47-103">Scale streaming endpoints with hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="b2e47-104">Información general</span><span class="sxs-lookup"><span data-stu-id="b2e47-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="b2e47-105">toocomplete este tutorial, necesita una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="b2e47-105">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="b2e47-106">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b2e47-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="b2e47-107">Los puntos de conexión de streaming **Premium** son adecuados para cargas de trabajo avanzadas y proporcionan una capacidad de ancho de banda dedicada y escalable.</span><span class="sxs-lookup"><span data-stu-id="b2e47-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="b2e47-108">Los clientes que tienen un punto de conexión de streaming **Premium**, de forma predeterminada, obtienen una unidad de streaming (SU).</span><span class="sxs-lookup"><span data-stu-id="b2e47-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="b2e47-109">Hola extremo de streaming puede ampliarse mediante la adición de SUs.</span><span class="sxs-lookup"><span data-stu-id="b2e47-109">hello streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="b2e47-110">Cada SU proporciona aplicaciones de toohello de capacidad de ancho de banda adicional.</span><span class="sxs-lookup"><span data-stu-id="b2e47-110">Each SU provides additional bandwidth capacity toohello application.</span></span> <span data-ttu-id="b2e47-111">Para obtener más información acerca de los tipos de punto de conexión y la configuración de red CDN de transmisión por secuencias, vea hello [información general de transmisión por secuencias Endpoint](media-services-portal-manage-streaming-endpoints.md) tema.</span><span class="sxs-lookup"><span data-stu-id="b2e47-111">For more information about streaming endpoint types and CDN configuration, see hello [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="b2e47-112">Este tema se muestra cómo tooscale un extremo de streaming.</span><span class="sxs-lookup"><span data-stu-id="b2e47-112">This topic shows how tooscale a streaming endpoint.</span></span>

<span data-ttu-id="b2e47-113">Para obtener más información acerca del precio, consulte la página sobre [información del precio de Servicios multimedia](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="b2e47-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="b2e47-114">Escalar puntos de conexión de streaming</span><span class="sxs-lookup"><span data-stu-id="b2e47-114">Scale streaming endpoints</span></span>

<span data-ttu-id="b2e47-115">número de hello toochange de unidades de streaming, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b2e47-115">toochange hello number of streaming units, do hello following:</span></span>

1. <span data-ttu-id="b2e47-116">Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="b2e47-116">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="b2e47-117">Hola **configuración** ventana, seleccione **los extremos de Streaming**.</span><span class="sxs-lookup"><span data-stu-id="b2e47-117">In hello **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="b2e47-118">Haga clic en extremo de streaming de Hola que desea tooscale.</span><span class="sxs-lookup"><span data-stu-id="b2e47-118">Click on hello streaming endpoint that you want tooscale.</span></span> 

    [!NOTE] <span data-ttu-id="b2e47-119">Solo puede escalar puntos de conexión de streaming **Premium**.</span><span class="sxs-lookup"><span data-stu-id="b2e47-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="b2e47-120">Mover el número de Hola de hello control deslizante toospecify de unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="b2e47-120">Move hello slider toospecify hello number of streaming units.</span></span>

    ![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="b2e47-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b2e47-122">Next steps</span></span>
<span data-ttu-id="b2e47-123">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="b2e47-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b2e47-124">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="b2e47-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

