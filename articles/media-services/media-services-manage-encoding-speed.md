---
title: "velocidad de administrar aaa y la simultaneidad de la codificación con servicios multimedia de Azure | Documentos de Microsoft"
description: "En este artículo se proporciona una breve introducción sobre cómo puede administrar la velocidad y la simultaneidad de las trabajos y las tareas de codificación con Azure Media Services."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 676313f8-a158-4e3a-a99b-2c29a341ecc9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: da52a6278a3d3b084dbf5a594db37df8447bb944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="94e1a-103">Administración de la velocidad y la simultaneidad de la codificación</span><span class="sxs-lookup"><span data-stu-id="94e1a-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="94e1a-104">En este artículo se proporciona una breve introducción sobre cómo puede administrar la velocidad y la simultaneidad de las trabajos y las tareas de codificación.</span><span class="sxs-lookup"><span data-stu-id="94e1a-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="94e1a-105">Información general</span><span class="sxs-lookup"><span data-stu-id="94e1a-105">Overview</span></span>

<span data-ttu-id="94e1a-106">En los servicios multimedia, un **tipo de unidad reservada** determina la velocidad de hello con la que se procesan los medios de las tareas de procesamiento.</span><span class="sxs-lookup"><span data-stu-id="94e1a-106">In Media Services, a **Reserved Unit Type** determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="94e1a-107">Puede elegir entre como consecuencia de hello reservado los tipos de unidad: **S1**, **S2**, o **S3**.</span><span class="sxs-lookup"><span data-stu-id="94e1a-107">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="94e1a-108">Por ejemplo, hello mismo trabajo de codificación se ejecuta con mayor rapidez cuando se usa hello **S2** tipo de unidad reservada comparar toohello **S1** tipo.</span><span class="sxs-lookup"><span data-stu-id="94e1a-108">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span> <span data-ttu-id="94e1a-109">Hola [ajuste de escala en unidades de codificación](media-services-scale-media-processing-overview.md) tema muestra una tabla que le ayuda a tomar la decisión al elegir entre distintas velocidades de codificación.</span><span class="sxs-lookup"><span data-stu-id="94e1a-109">hello [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="94e1a-110">Además toospecifying Hola reservado del tipo de unidad, puede especificar su cuenta con tooprovision **unidades reservadas**.</span><span class="sxs-lookup"><span data-stu-id="94e1a-110">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units**.</span></span> <span data-ttu-id="94e1a-111">número de Hola de unidades reservadas aprovisionadas determina número Hola de tareas multimedia que se pueden procesar simultáneamente en una cuenta determinada.</span><span class="sxs-lookup"><span data-stu-id="94e1a-111">hello number of provisioned reserved units determines hello number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="94e1a-112">Por ejemplo, si su cuenta tiene cinco unidades reservadas, se ejecutarán simultáneamente siempre y tareas de cinco medios como hay toobe de tareas que se procesan.</span><span class="sxs-lookup"><span data-stu-id="94e1a-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks toobe processed.</span></span> <span data-ttu-id="94e1a-113">las tareas restantes de Hello esperarán en cola de Hola y se procesarán de manera secuencial cuando finaliza una tarea en ejecución.</span><span class="sxs-lookup"><span data-stu-id="94e1a-113">hello remaining tasks will wait in hello queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="94e1a-114">Si una cuenta no tiene ninguna unidad reservada aprovisionada, las tareas se elegirán de manera secuencial.</span><span class="sxs-lookup"><span data-stu-id="94e1a-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="94e1a-115">En este caso, Hola de tiempo entre la finalización de una tarea de espera y hello siguiente que empieza dependerá disponibilidad Hola de recursos de sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="94e1a-115">In this case, hello wait time between one task finishing and hello next one starting will depend on hello availability of resources in hello system.</span></span>

<span data-ttu-id="94e1a-116">Para obtener información detallada y ejemplos que muestran cómo tooscale unidades de codificación, vea [esto](media-services-scale-media-processing-overview.md) tema.</span><span class="sxs-lookup"><span data-stu-id="94e1a-116">For detailed information and examples that show how tooscale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="94e1a-117">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="94e1a-117">Next step</span></span>

[<span data-ttu-id="94e1a-118">Escalar unidades de codificación</span><span class="sxs-lookup"><span data-stu-id="94e1a-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="94e1a-119">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="94e1a-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="94e1a-120">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="94e1a-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

