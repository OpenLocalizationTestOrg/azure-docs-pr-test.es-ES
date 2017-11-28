---
title: "aaaHow tooscale el entorno de visión de serie de tiempo de Azure | Documentos de Microsoft"
description: "Este tutorial trata cómo tooscale su entorno de visión de serie de tiempo de Azure"
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
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a><span data-ttu-id="e5eb5-103">Cómo tooscale su entorno de visión de la serie de tiempo</span><span class="sxs-lookup"><span data-stu-id="e5eb5-103">How tooscale your Time Series Insights environment</span></span>

<span data-ttu-id="e5eb5-104">Este tutorial trata cómo tooscale su entorno de visión de la serie de tiempo.</span><span class="sxs-lookup"><span data-stu-id="e5eb5-104">This tutorial covers how tooscale your Time Series Insights environment.</span></span>

> [!NOTE]
> <span data-ttu-id="e5eb5-105">No se permite el escalado vertical entre los tipos de SKU.</span><span class="sxs-lookup"><span data-stu-id="e5eb5-105">Scale up across sku types is not allowed.</span></span> <span data-ttu-id="e5eb5-106">Un entorno con una SKU S1 no se puede convertir en un entorno de S2.</span><span class="sxs-lookup"><span data-stu-id="e5eb5-106">An environment with a S1 Sku cannot be converted into an S2 environment.</span></span>

## <a name="s1-sku-ingress-rates-and-capacities"></a><span data-ttu-id="e5eb5-107">Capacidades y tasas de entrada de SKU de S1</span><span class="sxs-lookup"><span data-stu-id="e5eb5-107">S1 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="e5eb5-108">Capacidad de SKU de S1</span><span class="sxs-lookup"><span data-stu-id="e5eb5-108">S1 SKU Capacity</span></span> | <span data-ttu-id="e5eb5-109">Velocidad de entrada</span><span class="sxs-lookup"><span data-stu-id="e5eb5-109">Ingress Rate</span></span> | <span data-ttu-id="e5eb5-110">Capacidad máxima de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e5eb5-110">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="e5eb5-111">1</span><span class="sxs-lookup"><span data-stu-id="e5eb5-111">1</span></span> | <span data-ttu-id="e5eb5-112">1 GB (1 millones de eventos)</span><span class="sxs-lookup"><span data-stu-id="e5eb5-112">1 GB (1 million events)</span></span> | <span data-ttu-id="e5eb5-113">30 GB (30 millones de eventos) al mes</span><span class="sxs-lookup"><span data-stu-id="e5eb5-113">30 GB (30 million events) per month</span></span> |
| <span data-ttu-id="e5eb5-114">10</span><span class="sxs-lookup"><span data-stu-id="e5eb5-114">10</span></span> | <span data-ttu-id="e5eb5-115">10 GB (10 millones de eventos)</span><span class="sxs-lookup"><span data-stu-id="e5eb5-115">10 GB (10 million events)</span></span> | <span data-ttu-id="e5eb5-116">300 GB (300 millones de eventos) al mes</span><span class="sxs-lookup"><span data-stu-id="e5eb5-116">300 GB (300 million events) per month</span></span> |

## <a name="s2-sku-ingress-rates-and-capacities"></a><span data-ttu-id="e5eb5-117">Capacidades y tasas de entrada de SKU de S2</span><span class="sxs-lookup"><span data-stu-id="e5eb5-117">S2 SKU ingress rates and capacities</span></span>

| <span data-ttu-id="e5eb5-118">Capacidad de SKU de S2</span><span class="sxs-lookup"><span data-stu-id="e5eb5-118">S2 SKU Capacity</span></span> | <span data-ttu-id="e5eb5-119">Velocidad de entrada</span><span class="sxs-lookup"><span data-stu-id="e5eb5-119">Ingress Rate</span></span> | <span data-ttu-id="e5eb5-120">Capacidad máxima de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e5eb5-120">Maximum Storage Capacity</span></span>
| --- | --- | --- |
| <span data-ttu-id="e5eb5-121">1</span><span class="sxs-lookup"><span data-stu-id="e5eb5-121">1</span></span> | <span data-ttu-id="e5eb5-122">10 GB (10 millones de eventos)</span><span class="sxs-lookup"><span data-stu-id="e5eb5-122">10 GB (10 million events)</span></span> | <span data-ttu-id="e5eb5-123">300 GB (300 millones de eventos) al mes</span><span class="sxs-lookup"><span data-stu-id="e5eb5-123">300 GB (300 million events) per month</span></span> |
| <span data-ttu-id="e5eb5-124">10</span><span class="sxs-lookup"><span data-stu-id="e5eb5-124">10</span></span> | <span data-ttu-id="e5eb5-125">100 GB (100 millones de eventos)</span><span class="sxs-lookup"><span data-stu-id="e5eb5-125">100 GB (100 million events)</span></span> | <span data-ttu-id="e5eb5-126">3 TB (3 mil millones de eventos) al mes</span><span class="sxs-lookup"><span data-stu-id="e5eb5-126">3 TB (3 billion events) per month</span></span> |

<span data-ttu-id="e5eb5-127">Las capacidades se escalan linealmente, por lo que una SKU de S1 con capacidad 2 admite una tasa de entrada de 2 GB (2 millones) de eventos al día y 60 GB (60 millones de eventos) al mes.</span><span class="sxs-lookup"><span data-stu-id="e5eb5-127">Capacities scale linearly, so a S1 sku with capacity 2 supports 2 GB (2 million) events per day ingress rate and 60 GB (60 million events) per month.</span></span>

## <a name="changing-hello-capacity-of-your-environment"></a><span data-ttu-id="e5eb5-128">Cambiar la capacidad de Hola de su entorno</span><span class="sxs-lookup"><span data-stu-id="e5eb5-128">Changing hello capacity of your environment</span></span>

1. <span data-ttu-id="e5eb5-129">Hola portal de Azure, seleccione Hola entorno cuya capacidad desea toochange.</span><span class="sxs-lookup"><span data-stu-id="e5eb5-129">In hello Azure portal, select hello environment whose capacity you want toochange.</span></span>
1. <span data-ttu-id="e5eb5-130">En Configuración, haga clic en Configurar.</span><span class="sxs-lookup"><span data-stu-id="e5eb5-130">Under Settings, click Configure.</span></span>
1. <span data-ttu-id="e5eb5-131">Utilice Hola capacidad control deslizante tooselect Hola capacidad que cumpla los requisitos de Hola para las tarifas de entrada y almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e5eb5-131">Use hello Capacity slider tooselect hello capacity that meets hello requirements for your ingress rates and storage capacity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5eb5-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e5eb5-132">Next steps</span></span>

* <span data-ttu-id="e5eb5-133">Compruebe que la nueva capacidad de hello es suficiente tooprevent limitación.</span><span class="sxs-lookup"><span data-stu-id="e5eb5-133">Verify that hello new capacity is sufficient tooprevent throttling.</span></span> <span data-ttu-id="e5eb5-134">Para obtener más información, vea hello *el entorno podría obtener limitarán* sección [aquí](time-series-insights-diagnose-and-solve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="e5eb5-134">For more details, see hello *Your environment might be getting throttled* section [here](time-series-insights-diagnose-and-solve-problems.md).</span></span>
