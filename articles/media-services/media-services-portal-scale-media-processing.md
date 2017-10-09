---
title: media de aaaScale procesamiento mediante Hola portal de Azure | Documentos de Microsoft
description: "Este tutorial le guiará por los pasos de Hola de escalado medios procesamiento mediante Hola portal de Azure."
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
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a><span data-ttu-id="f6ac7-103">Tipo de unidad de cambio Hola reservado</span><span class="sxs-lookup"><span data-stu-id="f6ac7-103">Change hello reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6ac7-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f6ac7-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="f6ac7-105">Portal</span><span class="sxs-lookup"><span data-stu-id="f6ac7-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="f6ac7-106">REST</span><span class="sxs-lookup"><span data-stu-id="f6ac7-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="f6ac7-107">Java</span><span class="sxs-lookup"><span data-stu-id="f6ac7-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="f6ac7-108">PHP</span><span class="sxs-lookup"><span data-stu-id="f6ac7-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="f6ac7-109">Información general</span><span class="sxs-lookup"><span data-stu-id="f6ac7-109">Overview</span></span>

<span data-ttu-id="f6ac7-110">Una cuenta de servicios multimedia está asociada a un tipo de unidad reservada, que determina la velocidad de hello con la que se procesan los medios de las tareas de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-110">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="f6ac7-111">Puede elegir entre como consecuencia de hello reservado los tipos de unidad: **S1**, **S2**, o **S3**.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-111">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="f6ac7-112">Por ejemplo, hello mismo trabajo de codificación se ejecuta con mayor rapidez cuando se usa hello **S2** tipo de unidad reservada comparar toohello **S1** tipo.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-112">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

<span data-ttu-id="f6ac7-113">Además toospecifying Hola reservado del tipo de unidad, puede especificar su cuenta con tooprovision **unidades reservadas** (RUs).</span><span class="sxs-lookup"><span data-stu-id="f6ac7-113">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="f6ac7-114">número de Hola de RUs aprovisionados determina número Hola de tareas multimedia que se pueden procesar simultáneamente en una cuenta determinada.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-114">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="f6ac7-115">Las unidades reservadas sirven para establecer paralelismos en todo el procesamiento multimedia, incluida la indexación de trabajos mediante Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="f6ac7-116">Sin embargo, a diferencia de la codificación, la indexación de los trabajos no se procesará más rápido con unidades reservadas de mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6ac7-117">Que seguro Hola tooreview [Introducción](media-services-scale-media-processing-overview.md) tooget de tema para obtener más información acerca de cómo ampliar el medio de procesamiento de tema.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-117">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="f6ac7-118">Escalar el procesamiento multimedia</span><span class="sxs-lookup"><span data-stu-id="f6ac7-118">Scale media processing</span></span>
<span data-ttu-id="f6ac7-119">toochange Hola reservado hello y tipo de número de unidad de unidades reservadas, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f6ac7-119">toochange hello reserved unit type and hello number of reserved units, do hello following:</span></span>

1. <span data-ttu-id="f6ac7-120">Hola [portal de Azure](https://portal.azure.com/), seleccione su cuenta de servicios multimedia de Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="f6ac7-121">Hola **configuración** ventana, seleccione **unidades reservadas de multimedia**.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-121">In hello **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="f6ac7-122">número de hello toochange de unidades reservadas para hello seleccionado el tipo de unidad reservada, use hello **unidades de medios servida** control deslizante.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-122">toochange hello number of reserved units for hello selected reserved unit type, use hello **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="f6ac7-123">Hola toochange **tipo de unidad reservada**, presione S1, S2 o S3.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-123">toochange hello **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Página de procesadores](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="f6ac7-125">Hola presione Guardar botón toosave los cambios.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-125">Press hello SAVE button toosave your changes.</span></span>
   
    <span data-ttu-id="f6ac7-126">unidades reservadas de Hola se asignan cuando se presiona guardar.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-126">hello new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6ac7-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f6ac7-127">Next steps</span></span>
<span data-ttu-id="f6ac7-128">Consulte las rutas de aprendizaje de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="f6ac7-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f6ac7-129">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="f6ac7-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

