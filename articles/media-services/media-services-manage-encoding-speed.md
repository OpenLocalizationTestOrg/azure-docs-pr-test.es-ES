---
title: "Administración de la velocidad y la simultaneidad de la codificación con Azure Media Services | Microsoft Docs"
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
ms.openlocfilehash: 0463904fd9bf1138587d0d214e572ddd38cc2184
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
#  <a name="manage-speed-and-concurrency-of-your-encoding"></a><span data-ttu-id="e1993-103">Administración de la velocidad y la simultaneidad de la codificación</span><span class="sxs-lookup"><span data-stu-id="e1993-103">Manage speed and concurrency of your encoding</span></span>

<span data-ttu-id="e1993-104">En este artículo se proporciona una breve introducción sobre cómo puede administrar la velocidad y la simultaneidad de las trabajos y las tareas de codificación.</span><span class="sxs-lookup"><span data-stu-id="e1993-104">This article gives a brief overview of how you can manage speed and concurrency of your encoding jobs/tasks.</span></span>

## <a name="overview"></a><span data-ttu-id="e1993-105">Información general</span><span class="sxs-lookup"><span data-stu-id="e1993-105">Overview</span></span>

<span data-ttu-id="e1993-106">En Media Services, el valor de **Tipo de unidad reservada** determina la velocidad con que se procesan las tareas de procesamiento multimedia.</span><span class="sxs-lookup"><span data-stu-id="e1993-106">In Media Services, a **Reserved Unit Type** determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="e1993-107">Puede elegir uno de los siguientes tipos de unidad reservada: **S1**, **S2** o **S3**.</span><span class="sxs-lookup"><span data-stu-id="e1993-107">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="e1993-108">Por ejemplo, el mismo trabajo de codificación se ejecuta más rápido cuando se usa el tipo de unidad reservada **S2** en comparación con el tipo**S1**.</span><span class="sxs-lookup"><span data-stu-id="e1993-108">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span> <span data-ttu-id="e1993-109">En el tema sobre el [escalado de unidades de codificación](media-services-scale-media-processing-overview.md), se muestra una tabla que ayuda a elegir entre distintas velocidades de codificación.</span><span class="sxs-lookup"><span data-stu-id="e1993-109">The [scaling encoding units](media-services-scale-media-processing-overview.md) topic shows a table that helps you make decision when choosing between different encoding speeds.</span></span>

<span data-ttu-id="e1993-110">Además de especificar el tipo de unidad reservada, puede especificar el aprovisionamiento de su cuenta con **Unidades reservadas**.</span><span class="sxs-lookup"><span data-stu-id="e1993-110">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units**.</span></span> <span data-ttu-id="e1993-111">El número de unidades reservadas de codificación aprovisionadas determina el número de tareas de medios que se pueden procesar de forma simultánea en una cuenta determinada.</span><span class="sxs-lookup"><span data-stu-id="e1993-111">The number of provisioned reserved units determines the number of media tasks that can be processed concurrently in a given account.</span></span> <span data-ttu-id="e1993-112">Por ejemplo, si la cuenta tiene cinco unidades reservadas, se ejecutarán simultáneamente cinco tareas multimedia siempre que haya tareas para procesar.</span><span class="sxs-lookup"><span data-stu-id="e1993-112">For example, if your account has five reserved units, then five media tasks will be running concurrently as long as there are tasks to be processed.</span></span> <span data-ttu-id="e1993-113">Las tareas restantes esperarán en la cola y se elegirán para el procesamiento secuencialmente cuando finalice la tarea en ejecución.</span><span class="sxs-lookup"><span data-stu-id="e1993-113">The remaining tasks will wait in the queue and will get picked up for processing sequentially when a running task finishes.</span></span> <span data-ttu-id="e1993-114">Si una cuenta no tiene ninguna unidad reservada aprovisionada, las tareas se elegirán de manera secuencial.</span><span class="sxs-lookup"><span data-stu-id="e1993-114">If an account does not have any reserved units provisioned, then tasks will be picked up sequentially.</span></span> <span data-ttu-id="e1993-115">En este caso, el tiempo de espera entre la finalización de una tarea y el inicio de la siguiente dependerá de la disponibilidad de los recursos del sistema.</span><span class="sxs-lookup"><span data-stu-id="e1993-115">In this case, the wait time between one task finishing and the next one starting will depend on the availability of resources in the system.</span></span>

<span data-ttu-id="e1993-116">Para ver información detallada y ejemplos que muestran cómo escalar unidades de codificación, consulte [este](media-services-scale-media-processing-overview.md) tema.</span><span class="sxs-lookup"><span data-stu-id="e1993-116">For detailed information and examples that show how to scale encoding units, see [this](media-services-scale-media-processing-overview.md) topic.</span></span>

## <a name="next-step"></a><span data-ttu-id="e1993-117">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="e1993-117">Next step</span></span>

[<span data-ttu-id="e1993-118">Escalar unidades de codificación</span><span class="sxs-lookup"><span data-stu-id="e1993-118">Scale encoding units</span></span>](media-services-scale-media-processing-overview.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="e1993-119">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="e1993-119">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e1993-120">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="e1993-120">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

