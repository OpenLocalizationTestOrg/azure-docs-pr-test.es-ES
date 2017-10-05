---
title: Escalado del entorno de Azure Time Series Insights | Microsoft Docs
description: "Este tutorial describe cómo escalar el entorno de Azure Time Series Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 8f6c66ea2173c98179ec899d6626c2ab6f7ec4b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-your-time-series-insights-environment"></a><span data-ttu-id="286e4-103">Escalado de su entorno de Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="286e4-103">How to scale your Time Series Insights environment</span></span>

<span data-ttu-id="286e4-104">Este tutorial describe cómo escalar el entorno de Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="286e4-104">This tutorial covers how to scale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="286e4-105">No se permite el escalado vertical entre los tipos de SKU.</span><span class="sxs-lookup"><span data-stu-id="286e4-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="286e4-106">Un entorno con una SKU S1 no se puede convertir en un entorno de S2.</span><span class="sxs-lookup"><span data-stu-id="286e4-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="286e4-107">Capacidades y tasas de entrada de SKU de S1</span><span class="sxs-lookup"><span data-stu-id="286e4-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="286e4-108">Capacidad de SKU de S1</span><span class="sxs-lookup"><span data-stu-id="286e4-108">S1 SKU Capacity</span></span> | <span data-ttu-id="286e4-109">Velocidad de entrada</span><span class="sxs-lookup"><span data-stu-id="286e4-109">Ingress Rate</span></span> | <span data-ttu-id="286e4-110">Capacidad máxima de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="286e4-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="286e4-111">1</span><span class="sxs-lookup"><span data-stu-id="286e4-111">1</span></span> | <span data-ttu-id="286e4-112">1 GB (1 millones de eventos)</span><span class="sxs-lookup"><span data-stu-id="286e4-112">1 GB (1 million events)</span></span> | <span data-ttu-id="286e4-113">30 GB (30 millones de eventos) al mes</span><span class="sxs-lookup"><span data-stu-id="286e4-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="286e4-114">10</span><span class="sxs-lookup"><span data-stu-id="286e4-114">10</span></span> | <span data-ttu-id="286e4-115">10 GB (10 millones de eventos)</span><span class="sxs-lookup"><span data-stu-id="286e4-115">10 GB (10 million events)</span></span> | <span data-ttu-id="286e4-116">300 GB (300 millones de eventos) al mes</span><span class="sxs-lookup"><span data-stu-id="286e4-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="286e4-117">Capacidades y tasas de entrada de SKU de S2</span><span class="sxs-lookup"><span data-stu-id="286e4-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="286e4-118">Capacidad de SKU de S2</span><span class="sxs-lookup"><span data-stu-id="286e4-118">S2 SKU Capacity</span></span> | <span data-ttu-id="286e4-119">Velocidad de entrada</span><span class="sxs-lookup"><span data-stu-id="286e4-119">Ingress Rate</span></span> | <span data-ttu-id="286e4-120">Capacidad máxima de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="286e4-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="286e4-121">1</span><span class="sxs-lookup"><span data-stu-id="286e4-121">1</span></span> | <span data-ttu-id="286e4-122">10 GB (10 millones de eventos)</span><span class="sxs-lookup"><span data-stu-id="286e4-122">10 GB (10 million events)</span></span> | <span data-ttu-id="286e4-123">300 GB (300 millones de eventos) al mes</span><span class="sxs-lookup"><span data-stu-id="286e4-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="286e4-124">10</span><span class="sxs-lookup"><span data-stu-id="286e4-124">10</span></span> | <span data-ttu-id="286e4-125">100 GB (100 millones de eventos)</span><span class="sxs-lookup"><span data-stu-id="286e4-125">100 GB (100 million events)</span></span> | <span data-ttu-id="286e4-126">3 TB (3 mil millones de eventos) al mes</span><span class="sxs-lookup"><span data-stu-id="286e4-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="286e4-127">Las capacidades se escalan linealmente, por lo que una SKU de S1 con capacidad 2 admite una tasa de entrada de 2 GB (2 millones) de eventos al día y 60 GB (60 millones de eventos) al mes.</span><span class="sxs-lookup"><span data-stu-id="286e4-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-the-capacity-of-your-environment"></a><span data-ttu-id="286e4-128">Cambio de la capacidad del entorno</span><span class="sxs-lookup"><span data-stu-id="286e4-128">Changing the capacity of your environment</span></span>

1. <span data-ttu-id="286e4-129">En Azure Portal, seleccione el entorno cuya capacidad desee cambiar.</span><span class="sxs-lookup"><span data-stu-id="286e4-129">In the Azure portal, select the environment whose capacity you want to change.</span></span>
1. <span data-ttu-id="286e4-130">En Configuración, haga clic en Configurar.</span><span class="sxs-lookup"><span data-stu-id="286e4-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="286e4-131">Utilice el control deslizante de la capacidad para seleccionar la capacidad que cumple los requisitos para las tarifas de entrada y la capacidad de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="286e4-131">Use the Capacity slider to select the capacity that meets the requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="286e4-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="286e4-132">Next steps</span></span>

* <span data-ttu-id="286e4-133">Compruebe que la nueva capacidad sea suficiente para evitar la limitación.</span><span class="sxs-lookup"><span data-stu-id="286e4-133">Verify that the new capacity is sufficient to prevent throttling.</span></span> <span data-ttu-id="286e4-134">Para más información, vea la sección *Puede que se esté limitando el entorno* [aquí](time-series-insights-diagnose-and-solve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="286e4-134">For more details, see the *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>