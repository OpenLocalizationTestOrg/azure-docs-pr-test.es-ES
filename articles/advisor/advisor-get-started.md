---
title: "Introducción a Azure Advisor | Microsoft Docs"
description: "Introducción a Azure Advisor."
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: a662841bebda460d4225e080f16705b3f16fdc46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="edf4e-103">Introducción a Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="edf4e-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="edf4e-104">Obtenga información acerca de cómo acceder a Advisor mediante Azure Portal y obtener, implementar y buscar las recomendaciones, así como actualizarlas.</span><span class="sxs-lookup"><span data-stu-id="edf4e-104">Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="edf4e-105">Obtención de recomendaciones de Advisor</span><span class="sxs-lookup"><span data-stu-id="edf4e-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="edf4e-106">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="edf4e-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="edf4e-107">En el panel izquierdo, haga clic en **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="edf4e-107">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="edf4e-108">En el panel de menú de servicio, en **Supervisión y administración**, haga clic en **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="edf4e-108">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="edf4e-109">Se muestra el panel de Advisor.</span><span class="sxs-lookup"><span data-stu-id="edf4e-109">The Advisor dashboard is displayed.</span></span>

   ![Acceso a Azure Advisor mediante Azure Portal](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="edf4e-111">En el panel de Advisor, seleccione la suscripción para la que le gustaría recibir las recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="edf4e-111">On the Advisor dashboard, select the subscription for which you want to receive recommendations.</span></span>  
<span data-ttu-id="edf4e-112">El panel de Advisor muestra recomendaciones personalizadas de la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="edf4e-112">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="edf4e-113">Para obtener recomendaciones para una categoría determinada, haga clic en una de las pestañas **High Availability** (Alta disponibilidad), **Security** (Seguridad), **Performance** (Rendimiento) o **Cost** (Costo).</span><span class="sxs-lookup"><span data-stu-id="edf4e-113">To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="edf4e-114">Para acceder a las recomendaciones de Advisor, primero debe *registrar su suscripción* en dicha solución.</span><span class="sxs-lookup"><span data-stu-id="edf4e-114">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="edf4e-115">Una suscripción se registra cuando el *propietario de esta* inicia el panel de Advisor y hace clic en el botón **Obtener recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="edf4e-115">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="edf4e-116">Esta operación *solo se realiza una vez*.</span><span class="sxs-lookup"><span data-stu-id="edf4e-116">This is a *one-time operation*.</span></span> <span data-ttu-id="edf4e-117">Una vez registrada la suscripción, puede acceder a las recomendaciones de Advisor como *Propietario*, *Contribuidor* o *Lector* para una suscripción, un grupo de recursos o un recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="edf4e-117">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Panel de Azure Advisor](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="edf4e-119">Obtener detalles de recomendaciones de Advisor e implementar una solución</span><span class="sxs-lookup"><span data-stu-id="edf4e-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="edf4e-120">La hoja **Recommendation** (Recomendación) en Advisor ofrece información adicional acerca de la recomendación de Advisor.</span><span class="sxs-lookup"><span data-stu-id="edf4e-120">The **Recommendation** blade in Advisor offers additional information about the recommendation.</span></span> 

1. <span data-ttu-id="edf4e-121">Inicie sesión en [Azure Portal](https://portal.azure.com) y después inicie [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="edf4e-121">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="edf4e-122">En el panel **Advisor recommendations** (Recomendaciones de Advisor), haga clic en **Obtener recomendación**.</span><span class="sxs-lookup"><span data-stu-id="edf4e-122">On the **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="edf4e-123">En la lista de recomendaciones, haga clic en una recomendación que desee revisar en detalle.</span><span class="sxs-lookup"><span data-stu-id="edf4e-123">In the list of recommendations, click a recommendation that you want to review in detail.</span></span>  
<span data-ttu-id="edf4e-124">Se abre la hoja **Recomendación**.</span><span class="sxs-lookup"><span data-stu-id="edf4e-124">The **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="edf4e-125">En la hoja **Recomendaciones**, revise la información sobre las acciones que puede llevar a cabo para resolver un problema potencial o aprovechar una oportunidad de ahorro de costos.</span><span class="sxs-lookup"><span data-stu-id="edf4e-125">On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![Hoja Recomendación de Advisor](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="edf4e-127">Búsqueda de recomendaciones de Advisor</span><span class="sxs-lookup"><span data-stu-id="edf4e-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="edf4e-128">Puede buscar recomendaciones para una suscripción específica o un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="edf4e-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="edf4e-129">También puede buscar recomendaciones por estado.</span><span class="sxs-lookup"><span data-stu-id="edf4e-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="edf4e-130">Inicie sesión en [Azure Portal](https://portal.azure.com) y después inicie [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="edf4e-130">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="edf4e-131">Busque las recomendaciones mediante el filtrado de las suscripciones, grupos de recursos y el estado de la recomendación (**Active** [Activa] o **Snoozed** [Pospuesta]).</span><span class="sxs-lookup"><span data-stu-id="edf4e-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="edf4e-132">Haga clic en **Obtener recomendaciones** para obtener una lista de las recomendaciones de Advisor en función de los filtros de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="edf4e-132">To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Criterios de filtro de búsqueda de Advisor](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="edf4e-134">Posponer o descartar recomendaciones de Advisor</span><span class="sxs-lookup"><span data-stu-id="edf4e-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="edf4e-135">Inicie sesión en [Azure Portal](https://portal.azure.com) y después inicie [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="edf4e-135">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="edf4e-136">Haga clic en **Obtener recomendaciones** y después haga clic en una recomendación de la lista de recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="edf4e-136">Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="edf4e-137">En la hoja **Recommendation** (Recomendación), haga clic en **Snooze** (Posponer).</span><span class="sxs-lookup"><span data-stu-id="edf4e-137">On the **Recommendation** blade, click **Snooze**.</span></span>  

   ![Ejemplo de acción de recomendación de Advisor](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="edf4e-139">Puede especificar el tiempo que se pospondrá o seleccionar **Never** (Nunca) para descartar la recomendación.</span><span class="sxs-lookup"><span data-stu-id="edf4e-139">Specify a snooze time period, or select **Never** to dismiss the recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="edf4e-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="edf4e-140">Next steps</span></span>

<span data-ttu-id="edf4e-141">Para más información sobre Advisor, consulte:</span><span class="sxs-lookup"><span data-stu-id="edf4e-141">To learn more about Advisor, see:</span></span>
* [<span data-ttu-id="edf4e-142">Introducción a Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="edf4e-142">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="edf4e-143">Recomendaciones sobre alta disponibilidad de Advisor</span><span class="sxs-lookup"><span data-stu-id="edf4e-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="edf4e-144">Recomendaciones sobre seguridad de Advisor</span><span class="sxs-lookup"><span data-stu-id="edf4e-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="edf4e-145">Recomendaciones sobre rendimiento de Advisor</span><span class="sxs-lookup"><span data-stu-id="edf4e-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="edf4e-146">Recomendaciones sobre el costo de Advisor</span><span class="sxs-lookup"><span data-stu-id="edf4e-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
