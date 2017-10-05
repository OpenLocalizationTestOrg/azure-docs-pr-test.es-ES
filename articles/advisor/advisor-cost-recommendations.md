---
title: Recomendaciones sobre el costo de Azure Advisor | Microsoft Docs
description: Utilice Azure Advisor para optimizar el costo de las implementaciones de Azure.
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
ms.openlocfilehash: 5eef2116f238b477fa8de46ce7b25728c393739c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="4652f-103">Recomendaciones sobre el costo de Advisor</span><span class="sxs-lookup"><span data-stu-id="4652f-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="4652f-104">Advisor lo ayuda a optimizar y reducir el gasto global de Azure mediante la identificación de recursos inactivos e infrautilizados.</span><span class="sxs-lookup"><span data-stu-id="4652f-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="4652f-105">Puede obtener recomendaciones sobre el costo en la pestaña **Cost** (Costo) del panel de Advisor.</span><span class="sxs-lookup"><span data-stu-id="4652f-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span></span>

![Pestaña Cost (Costo) de Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="4652f-107">Optimización del gasto en máquinas virtuales mediante la adecuación del tamaño en instancias infrautilizadas</span><span class="sxs-lookup"><span data-stu-id="4652f-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="4652f-108">Mientras que determinados escenarios de aplicaciones pueden dar lugar a un uso escaso debido al diseño, a menudo puede ahorrar dinero administrando el tamaño y número de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4652f-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span></span> <span data-ttu-id="4652f-109">Advisor supervisa la utilización de las máquinas virtuales durante 14 días e identifica aquellas con una utilización escasa.</span><span class="sxs-lookup"><span data-stu-id="4652f-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="4652f-110">Se considera que una máquina virtual tiene una utilización escasa si su utilización de la CPU es del 5 % o menos y el de la red es de 7 MB o menos durante cuatro o más días.</span><span class="sxs-lookup"><span data-stu-id="4652f-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="4652f-111">Advisor muestra el costo estimado de continuar ejecutando la máquina virtual, para que puede elegir entre apagarla o cambiar su tamaño.</span><span class="sxs-lookup"><span data-stu-id="4652f-111">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span></span>  

![Recomendaciones sobre el costo de Advisor para cambiar el tamaño de máquinas virtuales](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-to-manage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="4652f-113">Usar una solución rentable para administrar los objetivos de rendimiento de varias bases de datos SQL</span><span class="sxs-lookup"><span data-stu-id="4652f-113">Use a cost effective solution to manage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="4652f-114">Advisor identifica las instancias de SQL Server que pueden beneficiarse de la creación de grupos de bases de datos elásticas.</span><span class="sxs-lookup"><span data-stu-id="4652f-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="4652f-115">Los grupos de bases de datos elásticas proporcionan una solución sencilla y rentable para administrar los objetivos de rendimiento de varias bases de datos que tienen patrones de utilización diferentes.</span><span class="sxs-lookup"><span data-stu-id="4652f-115">Elastic database pools provide a simple, cost-effective solution to manage the performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="4652f-116">Para más información sobre los grupos de bases de datos elásticas de Azure, consulte [¿Qué es un grupo elástico de Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/)</span><span class="sxs-lookup"><span data-stu-id="4652f-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Recomendaciones sobre el costo de Advisor para grupos de bases de datos elásticas](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="4652f-118">Obtención de acceso a las recomendaciones sobre el costo en Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="4652f-118">How to access cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="4652f-119">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4652f-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4652f-120">En el panel izquierdo, haga clic en **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="4652f-120">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="4652f-121">En el panel de menú de servicio, en **Supervisión y administración**, haga clic en **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="4652f-121">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="4652f-122">Se muestra el panel de Advisor.</span><span class="sxs-lookup"><span data-stu-id="4652f-122">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="4652f-123">En el panel de Advisor, haga clic en la pestaña **Costo**.</span><span class="sxs-lookup"><span data-stu-id="4652f-123">On the Advisor dashboard, click the **Cost** tab.</span></span>

5. <span data-ttu-id="4652f-124">Seleccione la suscripción para la que desea recibir las recomendaciones y haga clic en **Obtener recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="4652f-124">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="4652f-125">Para acceder a las recomendaciones de Advisor, primero debe *registrar su suscripción* en dicha solución.</span><span class="sxs-lookup"><span data-stu-id="4652f-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="4652f-126">Una suscripción se registra cuando el *propietario de esta* inicia el panel de Advisor y hace clic en el botón **Obtener recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="4652f-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="4652f-127">Esta operación *solo se realiza una vez*.</span><span class="sxs-lookup"><span data-stu-id="4652f-127">This is a *one-time operation*.</span></span> <span data-ttu-id="4652f-128">Una vez registrada la suscripción, puede acceder a las recomendaciones de Advisor como *Propietario*, *Contribuidor* o *Lector* para una suscripción, un grupo de recursos o un recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="4652f-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4652f-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4652f-129">Next steps</span></span>

<span data-ttu-id="4652f-130">Para aprender más sobre las recomendaciones de Advisor, consulte:</span><span class="sxs-lookup"><span data-stu-id="4652f-130">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="4652f-131">Introducción a Advisor</span><span class="sxs-lookup"><span data-stu-id="4652f-131">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="4652f-132">Introducción</span><span class="sxs-lookup"><span data-stu-id="4652f-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="4652f-133">Recomendaciones sobre rendimiento de Advisor</span><span class="sxs-lookup"><span data-stu-id="4652f-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="4652f-134">Recomendaciones sobre alta disponibilidad de Advisor</span><span class="sxs-lookup"><span data-stu-id="4652f-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="4652f-135">Recomendaciones sobre seguridad de Advisor</span><span class="sxs-lookup"><span data-stu-id="4652f-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
