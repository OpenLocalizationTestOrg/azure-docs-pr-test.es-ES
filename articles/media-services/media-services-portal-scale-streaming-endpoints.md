---
title: "Escalado de puntos de conexión de streaming con Azure Portal | Microsoft Docs"
description: "Este tutorial lo guiará a través de los pasos de escalado de puntos de conexión de streaming con el Portal de Azure."
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
ms.openlocfilehash: 4bb891371e3fc802fa667688a88878db18e32422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="scale-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="6c0a4-103">Escalado de puntos de conexión de streaming con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6c0a4-103">Scale streaming endpoints with the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="6c0a4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="6c0a4-104">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="6c0a4-105">Para completar este tutorial, deberá tener una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-105">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="6c0a4-106">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c0a4-106">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

<span data-ttu-id="6c0a4-107">Los puntos de conexión de streaming **Premium** son adecuados para cargas de trabajo avanzadas y proporcionan una capacidad de ancho de banda dedicada y escalable.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-107">**Premium** streaming endpoints are suitable for advanced workloads, providing dedicated and scalable bandwidth capacity.</span></span> <span data-ttu-id="6c0a4-108">Los clientes que tienen un punto de conexión de streaming **Premium**, de forma predeterminada, obtienen una unidad de streaming (SU).</span><span class="sxs-lookup"><span data-stu-id="6c0a4-108">Customers that have a **Premium** streaming endpoint, by default get one streaming unit (SU).</span></span> <span data-ttu-id="6c0a4-109">El punto de conexión de streaming puede ampliarse agregando unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-109">The streaming endpoint can be scaled by adding SUs.</span></span> <span data-ttu-id="6c0a4-110">Cada unidad de streaming proporciona capacidad de ancho de banda adicional a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-110">Each SU provides additional bandwidth capacity to the application.</span></span> <span data-ttu-id="6c0a4-111">Para obtener más información acerca de los puntos de conexión de streaming y la configuración de la red CDN, vea el tema [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) (Información general de puntos de conexión de streaming).</span><span class="sxs-lookup"><span data-stu-id="6c0a4-111">For more information about streaming endpoint types and CDN configuration, see the [Streaming Endpoint overview](media-services-portal-manage-streaming-endpoints.md) topic.</span></span>
 
<span data-ttu-id="6c0a4-112">Este tema muestra cómo escalar un punto de conexión de streaming.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-112">This topic shows how to scale a streaming endpoint.</span></span>

<span data-ttu-id="6c0a4-113">Para obtener más información acerca del precio, consulte la página sobre [información del precio de Servicios multimedia](http://go.microsoft.com/fwlink/?LinkId=275107).</span><span class="sxs-lookup"><span data-stu-id="6c0a4-113">For information about pricing details, see [Media Services Pricing Details](http://go.microsoft.com/fwlink/?LinkId=275107).</span></span>

## <a name="scale-streaming-endpoints"></a><span data-ttu-id="6c0a4-114">Escalar puntos de conexión de streaming</span><span class="sxs-lookup"><span data-stu-id="6c0a4-114">Scale streaming endpoints</span></span>

<span data-ttu-id="6c0a4-115">Para crear y cambiar el número de unidades de streaming, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="6c0a4-115">To change the number of streaming units, do the following:</span></span>

1. <span data-ttu-id="6c0a4-116">En [Azure Portal](https://portal.azure.com/), seleccione la cuenta de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-116">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="6c0a4-117">En la ventana **Configuración**, haga clic en **Extremos de streaming**.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-117">In the **Settings** window, select **Streaming endpoints**.</span></span>
3. <span data-ttu-id="6c0a4-118">Haga clic en el punto de conexión de streaming que desea modificar.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-118">Click on the streaming endpoint that you want to scale.</span></span> 

    [!NOTE] <span data-ttu-id="6c0a4-119">Solo puede escalar puntos de conexión de streaming **Premium**.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-119">You can only scale **Premium** streaming endpoints.</span></span>

4. <span data-ttu-id="6c0a4-120">Mueva el control deslizante para especificar el número de unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-120">Move the slider to specify the number of streaming units.</span></span>

    ![punto de conexión de streaming](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints3.png)

## <a name="next-steps"></a><span data-ttu-id="6c0a4-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6c0a4-122">Next steps</span></span>
<span data-ttu-id="6c0a4-123">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="6c0a4-123">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6c0a4-124">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="6c0a4-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

