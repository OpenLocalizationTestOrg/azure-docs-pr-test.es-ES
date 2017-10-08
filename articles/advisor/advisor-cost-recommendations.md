---
title: recomendaciones de Advisor costo aaaAzure | Documentos de Microsoft
description: Utilice el Asistente de Azure toooptimize Hola coste de las implementaciones de Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="3c9f7-103">Recomendaciones sobre el costo de Advisor</span><span class="sxs-lookup"><span data-stu-id="3c9f7-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="3c9f7-104">Advisor lo ayuda a optimizar y reducir el gasto global de Azure mediante la identificación de recursos inactivos e infrautilizados.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="3c9f7-105">Puede obtener costo recomendaciones de hello **costo** pestaña Panel de Asistente de Hola.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Pestaña Cost (Costo) de Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="3c9f7-107">Optimización del gasto en máquinas virtuales mediante la adecuación del tamaño en instancias infrautilizadas</span><span class="sxs-lookup"><span data-stu-id="3c9f7-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="3c9f7-108">Aunque pueden dar lugar a determinados escenarios de aplicación en un uso escaso por diseño, a menudo puede ahorrar dinero mediante la administración del tamaño de Hola y el número de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="3c9f7-109">Advisor supervisa la utilización de las máquinas virtuales durante 14 días e identifica aquellas con una utilización escasa.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="3c9f7-110">Se considera que una máquina virtual tiene una utilización escasa si su utilización de la CPU es del 5 % o menos y el de la red es de 7 MB o menos durante cuatro o más días.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="3c9f7-111">El asistente muestra de Hola costo estimado de continuar toorun la máquina virtual, para que pueda elegir tooshut abajo o cambiar su tamaño.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![Recomendaciones sobre el costo de Advisor para cambiar el tamaño de máquinas virtuales](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="3c9f7-113">Usar un objetivos de rendimiento de la solución más rentable toomanage de varias bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="3c9f7-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="3c9f7-114">Advisor identifica las instancias de SQL Server que pueden beneficiarse de la creación de grupos de bases de datos elásticas.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="3c9f7-115">Los grupos de bases de datos elásticas proporcionan una solución simple y rentable toomanage objetivos de rendimiento de Hola de varias bases de datos que tienen diferentes patrones de uso.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="3c9f7-116">Para más información sobre los grupos de bases de datos elásticas de Azure, consulte [¿Qué es un grupo elástico de Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/)</span><span class="sxs-lookup"><span data-stu-id="3c9f7-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Recomendaciones sobre el costo de Advisor para grupos de bases de datos elásticas](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="3c9f7-118">¿Cómo tooaccess costo recomendaciones en el Asistente de Azure</span><span class="sxs-lookup"><span data-stu-id="3c9f7-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="3c9f7-119">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3c9f7-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="3c9f7-120">En el panel izquierdo de hello, haga clic en **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="3c9f7-121">Hola servicio panel de menú, en **supervisión y administración**, haga clic en **Asistente de Azure**.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="3c9f7-122">Hola Advisor panel se abre.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="3c9f7-123">En el panel del Asistente de hello, haga clic en hello **costo** ficha.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="3c9f7-124">Seleccione la suscripción de hello para el que desea tooreceive recomendaciones y, a continuación, haga clic en **obtener recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="3c9f7-125">tooaccess las recomendaciones del asistente, primero debe *registrar su suscripción* con el asistente.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="3c9f7-126">Una suscripción se registra cuando un *suscripción propietario* inicia Hola Hola de panel y hace clic en el asistente **obtener recomendaciones** botón.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="3c9f7-127">Esta operación *solo se realiza una vez*.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-127">This is a *one-time operation*.</span></span> <span data-ttu-id="3c9f7-128">Después de registra la suscripción de hello, puede tener acceso a las recomendaciones del asistente como *propietario*, *colaborador*, o *lector* para una suscripción de un grupo de recursos, o recurso específico.</span><span class="sxs-lookup"><span data-stu-id="3c9f7-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c9f7-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3c9f7-129">Next steps</span></span>

<span data-ttu-id="3c9f7-130">toolearn más información acerca de las recomendaciones del asistente, vea:</span><span class="sxs-lookup"><span data-stu-id="3c9f7-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="3c9f7-131">Introducción tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="3c9f7-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="3c9f7-132">Introducción</span><span class="sxs-lookup"><span data-stu-id="3c9f7-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="3c9f7-133">Recomendaciones sobre rendimiento de Advisor</span><span class="sxs-lookup"><span data-stu-id="3c9f7-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="3c9f7-134">Recomendaciones sobre alta disponibilidad de Advisor</span><span class="sxs-lookup"><span data-stu-id="3c9f7-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="3c9f7-135">Recomendaciones sobre seguridad de Advisor</span><span class="sxs-lookup"><span data-stu-id="3c9f7-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
