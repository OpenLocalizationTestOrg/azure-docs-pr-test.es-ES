---
title: "Información general sobre los patrones comunes de escalado automático | Microsoft Docs"
description: "Obtenga información sobre algunos de los patrones comunes de escalado automático de recursos en Azure."
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
ms.openlocfilehash: fce51546e041c8989d813c3935e058c52b38ba77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="39b29-103">Información general sobre los patrones comunes de escalado automático</span><span class="sxs-lookup"><span data-stu-id="39b29-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="39b29-104">En este artículo se describen algunos de los patrones comunes para escalar recursos en Azure.</span><span class="sxs-lookup"><span data-stu-id="39b29-104">This article describes some of the common patterns to scale your resource in Azure.</span></span>

<span data-ttu-id="39b29-105">El escalado automático de Azure Monitor solo se aplica a Conjuntos de escalado de máquinas virtuales, Cloud Services, planes de App Service y App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="39b29-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="39b29-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="39b29-106">Lets get started</span></span>

<span data-ttu-id="39b29-107">En este artículo se asume que está familiarizado con el escalado automático.</span><span class="sxs-lookup"><span data-stu-id="39b29-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="39b29-108">Puede [comenzar aquí a escalar los recursos][1].</span><span class="sxs-lookup"><span data-stu-id="39b29-108">You can [get started here to scale your resource][1].</span></span> <span data-ttu-id="39b29-109">A continuación, se indican algunos de los patrones comunes de escalado.</span><span class="sxs-lookup"><span data-stu-id="39b29-109">The following are some of the common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="39b29-110">Escala en función de la CPU</span><span class="sxs-lookup"><span data-stu-id="39b29-110">Scale based on CPU</span></span>

<span data-ttu-id="39b29-111">Tiene una aplicación web (rol de VMSS o de servicio en la nube) y:</span><span class="sxs-lookup"><span data-stu-id="39b29-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="39b29-112">Desea escalar o reducir horizontalmente en función de la CPU.</span><span class="sxs-lookup"><span data-stu-id="39b29-112">You want to scale out/scale in based on CPU.</span></span>
- <span data-ttu-id="39b29-113">Además, desea asegurarse de que hay un número mínimo de instancias.</span><span class="sxs-lookup"><span data-stu-id="39b29-113">Additionally, you want to ensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="39b29-114">También quiere asegurarse de que establece un límite máximo del número de instancias al que puede escalar.</span><span class="sxs-lookup"><span data-stu-id="39b29-114">Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.</span></span>

![Escala en función de la CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="39b29-116">Escalado distinto entre los días de la semana y los fines de semana</span><span class="sxs-lookup"><span data-stu-id="39b29-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="39b29-117">Tiene una aplicación web (rol de VMSS o de servicio en la nube) y:</span><span class="sxs-lookup"><span data-stu-id="39b29-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="39b29-118">Desea 3 instancias de forma predeterminada (en días de la semana).</span><span class="sxs-lookup"><span data-stu-id="39b29-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="39b29-119">No espera que haya tráfico durante los fines de semana y, por tanto, desea reducir verticalmente a 1 instancia para los fines de semana.</span><span class="sxs-lookup"><span data-stu-id="39b29-119">You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.</span></span>

![Escalado distinto entre los días de la semana y los fines de semana][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="39b29-121">Escalado distinto durante festividades</span><span class="sxs-lookup"><span data-stu-id="39b29-121">Scale differently during holidays</span></span>

<span data-ttu-id="39b29-122">Tiene una aplicación web (rol de VMSS o de servicio en la nube) y:</span><span class="sxs-lookup"><span data-stu-id="39b29-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="39b29-123">Desea escalar o reducir verticalmente en función del uso de CPU de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="39b29-123">You want to scale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="39b29-124">Sin embargo, durante Navidad u otros días específicos importantes para su negocio, desea reemplazar los valores predeterminados y disponer de más capacidad.</span><span class="sxs-lookup"><span data-stu-id="39b29-124">However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.</span></span>

![Escalado distinto durante festividades][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="39b29-126">Escalado en función de métricas personalizadas</span><span class="sxs-lookup"><span data-stu-id="39b29-126">Scale based on custom metric</span></span>

<span data-ttu-id="39b29-127">Tiene un front-end web y un nivel de API que se comunica con el back-end.</span><span class="sxs-lookup"><span data-stu-id="39b29-127">You have a web front end and a API tier that communicates with the backend.</span></span> 

- <span data-ttu-id="39b29-128">Desea escalar el nivel de API en función de eventos personalizados en el front-end; por ejemplo, desea escalar el proceso de compra en función del número de artículos que hay en el carro de la compra.</span><span class="sxs-lookup"><span data-stu-id="39b29-128">You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)</span></span>

![Escalado en función de métricas personalizadas][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png