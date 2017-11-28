---
title: "media de aaaScale procesamiento mediante la adición de unidades de codificación - Azure |  Documentos de Microsoft"
description: "Obtenga información acerca de cómo toohow tooadd unidades de codificación con .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a><span data-ttu-id="f86d1-103">¿Cómo tooscale codificación con el SDK de .NET</span><span class="sxs-lookup"><span data-stu-id="f86d1-103">How tooscale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f86d1-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f86d1-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="f86d1-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f86d1-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="f86d1-106">REST</span><span class="sxs-lookup"><span data-stu-id="f86d1-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="f86d1-107">Java</span><span class="sxs-lookup"><span data-stu-id="f86d1-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="f86d1-108">PHP</span><span class="sxs-lookup"><span data-stu-id="f86d1-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="f86d1-109">Información general</span><span class="sxs-lookup"><span data-stu-id="f86d1-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f86d1-110">Que seguro Hola tooreview [Introducción](media-services-scale-media-processing-overview.md) tooget de tema para obtener más información acerca de cómo ampliar el medio de procesamiento de tema.</span><span class="sxs-lookup"><span data-stu-id="f86d1-110">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="f86d1-111">Hola toochange Hola reservado hello y tipo de número de unidad con .NET SDK, de unidades reservadas de codificación siguientes:</span><span class="sxs-lookup"><span data-stu-id="f86d1-111">toochange hello reserved unit type and hello number of encoding reserved units using .NET SDK, do hello following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="f86d1-112">Apertura de una incidencia de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="f86d1-112">Opening a Support Ticket</span></span>
<span data-ttu-id="f86d1-113">De forma predeterminada, cada cuenta de servicios multimedia puede escalar tooup too25 codificación y 5 petición unidades reservadas de Streaming.</span><span class="sxs-lookup"><span data-stu-id="f86d1-113">By default every Media Services account can scale tooup too25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="f86d1-114">Si desea solicitar un límite mayor, abra una incidencia de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="f86d1-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="f86d1-115">Abrir una incidencia de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="f86d1-115">Open a support ticket</span></span>
<span data-ttu-id="f86d1-116">tooopen una incidencia de soporte técnico Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f86d1-116">tooopen a support ticket do hello following:</span></span>

1. <span data-ttu-id="f86d1-117">Haga clic en [Obtener soporte técnico](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="f86d1-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="f86d1-118">Si no ha iniciado sesión, tendrá que ser solicitada tooenter sus credenciales.</span><span class="sxs-lookup"><span data-stu-id="f86d1-118">If you are not logged in, you will be prompted tooenter your credentials.</span></span>
2. <span data-ttu-id="f86d1-119">Seleccione su suscripción.</span><span class="sxs-lookup"><span data-stu-id="f86d1-119">Select your subscription.</span></span>
3. <span data-ttu-id="f86d1-120">En el tipo de soporte, seleccione "Técnico".</span><span class="sxs-lookup"><span data-stu-id="f86d1-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="f86d1-121">Haga clic en "Crear incidencia".</span><span class="sxs-lookup"><span data-stu-id="f86d1-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="f86d1-122">Seleccione "Servicios multimedia de Azure" en la lista de productos de hello presentados en la página siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="f86d1-122">Select "Azure Media Services" in hello product list presented on hello next page.</span></span>
6. <span data-ttu-id="f86d1-123">Seleccione un "Tipo de problema" que sea pertinente en relación con su problema.</span><span class="sxs-lookup"><span data-stu-id="f86d1-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="f86d1-124">Haga clic en Continue.</span><span class="sxs-lookup"><span data-stu-id="f86d1-124">Click Continue.</span></span>
8. <span data-ttu-id="f86d1-125">Siga las instrucciones que aparecen en la página siguiente y, a continuación, escriba los detalles de su problema.</span><span class="sxs-lookup"><span data-stu-id="f86d1-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="f86d1-126">Haga clic en enviar vale de hello tooopen.</span><span class="sxs-lookup"><span data-stu-id="f86d1-126">Click submit tooopen hello ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f86d1-127">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="f86d1-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f86d1-128">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="f86d1-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

