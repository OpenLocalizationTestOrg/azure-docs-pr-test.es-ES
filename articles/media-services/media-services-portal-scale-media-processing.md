---
title: Escalado del procesamiento de medios mediante Azure Portal | Microsoft Docs
description: "Este tutorial lo guiará a través de los pasos de escalado de procesamiento de medios con Azure Portal."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 46ca29d3e66701f2abcb185791089e94761984e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="change-the-reserved-unit-type"></a><span data-ttu-id="b8f8a-103">Cambio del tipo de unidad reservada</span><span class="sxs-lookup"><span data-stu-id="b8f8a-103">Change the reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8f8a-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b8f8a-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="b8f8a-105">Portal</span><span class="sxs-lookup"><span data-stu-id="b8f8a-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="b8f8a-106">REST</span><span class="sxs-lookup"><span data-stu-id="b8f8a-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="b8f8a-107">Java</span><span class="sxs-lookup"><span data-stu-id="b8f8a-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="b8f8a-108">PHP</span><span class="sxs-lookup"><span data-stu-id="b8f8a-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="b8f8a-109">Información general</span><span class="sxs-lookup"><span data-stu-id="b8f8a-109">Overview</span></span>

<span data-ttu-id="b8f8a-110">Una cuenta de Servicios multimedia está asociada con un tipo de unidad reservada que determina la rapidez con la que se procesan las tareas de procesamiento multimedia.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-110">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="b8f8a-111">Puede elegir uno de los siguientes tipos de unidad reservada: **S1**, **S2** o **S3**.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-111">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="b8f8a-112">Por ejemplo, el mismo trabajo de codificación se ejecuta más rápido cuando se usa el tipo de unidad reservada **S2** en comparación con el tipo**S1**.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-112">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span>

<span data-ttu-id="b8f8a-113">Además de especificar el tipo de unidad reservada, puede especificar el aprovisionamiento de su cuenta con **unidades reservadas**.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-113">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="b8f8a-114">El número de unidades reservadas aprovisionadas determina el número de tareas de medios que se pueden procesar de forma simultánea en una cuenta determinada.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-114">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="b8f8a-115">Las unidades reservadas sirven para establecer paralelismos en todo el procesamiento multimedia, incluida la indexación de trabajos mediante Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="b8f8a-116">Sin embargo, a diferencia de la codificación, la indexación de los trabajos no se procesará más rápido con unidades reservadas de mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8f8a-117">Para más información sobre cómo escalar el procesamiento de medios, consulte este tema de [introducción](media-services-scale-media-processing-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="b8f8a-117">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="b8f8a-118">Escalar el procesamiento multimedia</span><span class="sxs-lookup"><span data-stu-id="b8f8a-118">Scale media processing</span></span>
<span data-ttu-id="b8f8a-119">Para cambiar el tipo de unidad reservada y el número de unidades reservadas, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="b8f8a-119">To change the reserved unit type and the number of reserved units, do the following:</span></span>

1. <span data-ttu-id="b8f8a-120">En [Azure Portal](https://portal.azure.com/), seleccione la cuenta de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="b8f8a-121">En la ventana **Configuración**, seleccione **Unidades reservadas de medios**.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-121">In the **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="b8f8a-122">Para cambiar el número de unidades reservadas para el tipo de unidad reservada seleccionada, use el control deslizante **Unidades reservadas de medios** .</span><span class="sxs-lookup"><span data-stu-id="b8f8a-122">To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="b8f8a-123">Para cambiar el **TIPO DE UNIDAD RESERVADA**, haga clic en S1, S2 o S3.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-123">To change the **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Página de procesadores](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="b8f8a-125">Presione el botón GUARDAR para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-125">Press the SAVE button to save your changes.</span></span>
   
    <span data-ttu-id="b8f8a-126">Las nuevas unidades reservadas se asignan en cuanto presiona GUARDAR.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-126">The new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8f8a-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b8f8a-127">Next steps</span></span>
<span data-ttu-id="b8f8a-128">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="b8f8a-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b8f8a-129">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="b8f8a-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

