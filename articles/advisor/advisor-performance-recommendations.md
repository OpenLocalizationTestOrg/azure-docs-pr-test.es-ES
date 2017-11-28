---
title: Recomendaciones sobre rendimiento de Azure Advisor | Microsoft Docs
description: Utilice Advisor para optimizar el rendimiento de las implementaciones de Azure.
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
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="4a5e1-103">Recomendaciones sobre rendimiento de Advisor</span><span class="sxs-lookup"><span data-stu-id="4a5e1-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="4a5e1-104">Las recomendaciones sobre rendimiento de Azure Advisor ayudan a mejorar la velocidad y la capacidad de respuesta de las aplicaciones empresariales críticas.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="4a5e1-105">Puede obtener las recomendaciones sobre rendimiento de Advisor en la pestaña **Rendimiento** del panel de Advisor.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![Pestaña Advisor Performance (Rendimiento de Advisor)](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="4a5e1-107">Mejora del rendimiento de la base de datos con SQL DB Advisor</span><span class="sxs-lookup"><span data-stu-id="4a5e1-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="4a5e1-108">Advisor proporciona una vista coherente y consolidada de recomendaciones para todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="4a5e1-109">Se integra con SQL Database Advisor para ofrecer recomendaciones y mejorar el rendimiento de la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="4a5e1-110">SQL Database Advisor evalúa el rendimiento de las bases de datos SQL Azure mediante el análisis del historial de utilización.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="4a5e1-111">Después, ofrece las recomendaciones más adecuadas para ejecutar la carga de trabajo habitual de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="4a5e1-112">Para obtener recomendaciones, es preciso que una base de datos lleve usándose aproximadamente una semana y que, dentro de esa semana, muestre alguna actividad coherente.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="4a5e1-113">SQL Database Advisor puede optimizar los patrones de consultas coherentes con más facilidad que en el caso de ráfagas aleatorias de actividad.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="4a5e1-114">Para más información acerca de SQL Database Advisor, consulte [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="4a5e1-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![Recomendaciones de SQL Database](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="4a5e1-116">Mejora de la confiabilidad y el rendimiento de Redis Cache</span><span class="sxs-lookup"><span data-stu-id="4a5e1-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="4a5e1-117">Advisor identifica las instancias de Redis Cache donde el rendimiento puede verse afectado negativamente por la utilización intensa de la memoria, la carga del servidor, el ancho de banda de red o un número elevado de conexiones de cliente.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="4a5e1-118">Advisor también sugiere procedimientos recomendados para evitar posibles problemas.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="4a5e1-119">Para obtener más información acerca de las recomendaciones de Redis Cache, vea [Advisor de Redis Cache](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="4a5e1-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="4a5e1-120">Mejora de la confiabilidad y el rendimiento de App Service</span><span class="sxs-lookup"><span data-stu-id="4a5e1-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="4a5e1-121">Azure Advisor integra las sugerencias de los procedimientos recomendados para mejorar su experiencia de App Services y para descubrir las funciones de la plataforma adecuada.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="4a5e1-122">Ejemplos de recomendaciones de App Services:</span><span class="sxs-lookup"><span data-stu-id="4a5e1-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="4a5e1-123">Detección de instancias en las que los tiempos de ejecución de las aplicaciones con opciones de mitigación agotan los recursos de la memoria o la CPU.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="4a5e1-124">Detección de instancias donde la colocación de recursos como aplicaciones web y bases de datos puede mejorar el rendimiento y reducir el costo.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="4a5e1-125">Para obtener más información acerca de las recomendaciones de App Services, consulte los [procedimientos recomendados para Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="4a5e1-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="4a5e1-126">![Recomendaciones de App Services](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="4a5e1-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="4a5e1-127">Obtención de acceso a las recomendaciones sobre rendimiento en Advisor</span><span class="sxs-lookup"><span data-stu-id="4a5e1-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="4a5e1-128">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4a5e1-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4a5e1-129">En el panel izquierdo, haga clic en **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="4a5e1-130">En el panel de menú de servicio, en **Supervisión y administración**, haga clic en **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="4a5e1-131">Se muestra el panel de Advisor.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="4a5e1-132">En el panel de Advisor, haga clic en la pestaña **Rendimiento**.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="4a5e1-133">Seleccione la suscripción para la que desea recibir las recomendaciones y haga clic en **Obtener recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="4a5e1-134">Para acceder a las recomendaciones de Advisor, primero debe *registrar su suscripción* en dicha solución.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="4a5e1-135">Una suscripción se registra cuando el *propietario de esta* inicia el panel de Advisor y hace clic en el botón **Obtener recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="4a5e1-136">Esta operación *solo se realiza una vez*.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-136">This is a *one-time operation*.</span></span> <span data-ttu-id="4a5e1-137">Una vez registrada la suscripción, puede acceder a las recomendaciones de Advisor como *Propietario*, *Contribuidor* o *Lector* para una suscripción, un grupo de recursos o un recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="4a5e1-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a5e1-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a5e1-138">Next steps</span></span>

<span data-ttu-id="4a5e1-139">Para aprender más sobre las recomendaciones de Advisor, consulte:</span><span class="sxs-lookup"><span data-stu-id="4a5e1-139">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="4a5e1-140">Introducción a Advisor</span><span class="sxs-lookup"><span data-stu-id="4a5e1-140">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="4a5e1-141">Introducción a Advisor</span><span class="sxs-lookup"><span data-stu-id="4a5e1-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="4a5e1-142">Recomendaciones sobre el costo de Advisor</span><span class="sxs-lookup"><span data-stu-id="4a5e1-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="4a5e1-143">Recomendaciones sobre alta disponibilidad de Advisor</span><span class="sxs-lookup"><span data-stu-id="4a5e1-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="4a5e1-144">Recomendaciones sobre seguridad de Advisor</span><span class="sxs-lookup"><span data-stu-id="4a5e1-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

