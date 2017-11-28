---
title: "aaaOverview de patrones comunes de escalado automático | Documentos de Microsoft"
description: "Obtenga información acerca de que algunas tooauto patrones comunes de hello escalan el recurso de Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="e8275-103">Información general sobre los patrones comunes de escalado automático</span><span class="sxs-lookup"><span data-stu-id="e8275-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="e8275-104">Este artículo describen algunos tooscale patrones comunes de hello el recurso de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8275-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="e8275-105">Azure Autoescala de Monitor aplica solo tooVirtual conjuntos de escala de máquina (VMSS), servicios en la nube, planes de servicio de aplicaciones y entornos del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="e8275-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="e8275-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="e8275-106">Lets get started</span></span>

<span data-ttu-id="e8275-107">En este artículo se asume que está familiarizado con el escalado automático.</span><span class="sxs-lookup"><span data-stu-id="e8275-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="e8275-108">También puede [obtener iniciada tooscale aquí el recurso][1].</span><span class="sxs-lookup"><span data-stu-id="e8275-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="e8275-109">siguiente Hola es algunos de los patrones comunes de escala de Hola.</span><span class="sxs-lookup"><span data-stu-id="e8275-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="e8275-110">Escala en función de la CPU</span><span class="sxs-lookup"><span data-stu-id="e8275-110">Scale based on CPU</span></span>

<span data-ttu-id="e8275-111">Tiene una aplicación web (rol de VMSS o de servicio en la nube) y:</span><span class="sxs-lookup"><span data-stu-id="e8275-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="e8275-112">Desea tooscale fuera y de CPU en función de la escala.</span><span class="sxs-lookup"><span data-stu-id="e8275-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="e8275-113">Además, desea tooensure hay un número mínimo de instancias.</span><span class="sxs-lookup"><span data-stu-id="e8275-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="e8275-114">Además, le interesará tooensure que establece un número de toohello de límite máximo de instancias que se pueda adaptar a.</span><span class="sxs-lookup"><span data-stu-id="e8275-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![Escala en función de la CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="e8275-116">Escalado distinto entre los días de la semana y los fines de semana</span><span class="sxs-lookup"><span data-stu-id="e8275-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="e8275-117">Tiene una aplicación web (rol de VMSS o de servicio en la nube) y:</span><span class="sxs-lookup"><span data-stu-id="e8275-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="e8275-118">Desea 3 instancias de forma predeterminada (en días de la semana).</span><span class="sxs-lookup"><span data-stu-id="e8275-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="e8275-119">No esperar un tráfico de los fines de semana y, por tanto, desea tooscale too1 instancia los fines de semana.</span><span class="sxs-lookup"><span data-stu-id="e8275-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![Escalado distinto entre los días de la semana y los fines de semana][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="e8275-121">Escalado distinto durante festividades</span><span class="sxs-lookup"><span data-stu-id="e8275-121">Scale differently during holidays</span></span>

<span data-ttu-id="e8275-122">Tiene una aplicación web (rol de VMSS o de servicio en la nube) y:</span><span class="sxs-lookup"><span data-stu-id="e8275-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="e8275-123">Desea tooscale arriba/abajo según el uso de CPU de forma predeterminada</span><span class="sxs-lookup"><span data-stu-id="e8275-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="e8275-124">Sin embargo, durante la temporada de vacaciones (o los días específicos que son importantes para su empresa) desea que los valores predeterminados de toooverride hello y tiene más capacidad a su disposición.</span><span class="sxs-lookup"><span data-stu-id="e8275-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![Escalado distinto durante festividades][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="e8275-126">Escalado en función de métricas personalizadas</span><span class="sxs-lookup"><span data-stu-id="e8275-126">Scale based on custom metric</span></span>

<span data-ttu-id="e8275-127">Tiene un front-end web y un nivel de API que se comunica con hello back-end.</span><span class="sxs-lookup"><span data-stu-id="e8275-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="e8275-128">Desea capa de hello API tooscale basado en eventos personalizados de front-end de hello (ejemplo: desea tooscale el proceso de pago según el número de Hola de elementos de hello carro de la compra)</span><span class="sxs-lookup"><span data-stu-id="e8275-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![Escalado en función de métricas personalizadas][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png