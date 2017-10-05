---
title: Recomendaciones sobre seguridad de Azure Advisor | Microsoft Docs
description: Utilice Azure Advisor para mejorar la seguridad de las implementaciones de Azure.
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
ms.openlocfilehash: 53be05593c3733ccb27979a3a026414013125779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="f25a1-103">Recomendaciones sobre seguridad de Advisor</span><span class="sxs-lookup"><span data-stu-id="f25a1-103">Advisor Security recommendations</span></span>

<span data-ttu-id="f25a1-104">Azure Advisor proporciona una vista coherente y consolidada de recomendaciones para todos los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f25a1-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="f25a1-105">Se integra con Azure Security Center para proporcionarle recomendaciones sobre seguridad.</span><span class="sxs-lookup"><span data-stu-id="f25a1-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="f25a1-106">Puede obtener recomendaciones sobre seguridad en la pestaña **Seguridad** del panel de Advisor.</span><span class="sxs-lookup"><span data-stu-id="f25a1-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![El botón de seguridad de Advisor](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="f25a1-108">El Centro de seguridad ayuda a evitar, detectar y responder a amenazas con más visibilidad y control de la seguridad en los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f25a1-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="f25a1-109">Analiza periódicamente el estado de seguridad de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f25a1-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="f25a1-110">Cuando el Centro de seguridad identifica vulnerabilidades de seguridad potenciales, crea recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="f25a1-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="f25a1-111">Las recomendaciones lo guían en el proceso de configuración de los controles necesarios.</span><span class="sxs-lookup"><span data-stu-id="f25a1-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![Pestaña Seguridad de Advisor](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="f25a1-113">Para obtener más información sobre las recomendaciones de seguridad, consulte [Administración de recomendaciones de seguridad en Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="f25a1-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="f25a1-114">Obtención de acceso a las recomendaciones sobre seguridad en Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="f25a1-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="f25a1-115">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f25a1-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="f25a1-116">En el panel izquierdo, haga clic en **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="f25a1-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="f25a1-117">En el panel de menú de servicio, en **Supervisión y administración**, haga clic en **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="f25a1-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="f25a1-118">Se muestra el panel de Advisor.</span><span class="sxs-lookup"><span data-stu-id="f25a1-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="f25a1-119">En el panel de Advisor, haga clic en la pestaña **Seguridad**.</span><span class="sxs-lookup"><span data-stu-id="f25a1-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="f25a1-120">Seleccione la suscripción para la que desea recibir las recomendaciones y haga clic en **Obtener recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="f25a1-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="f25a1-121">Para acceder a las recomendaciones de Advisor, primero debe *registrar su suscripción* en dicha solución.</span><span class="sxs-lookup"><span data-stu-id="f25a1-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="f25a1-122">Una suscripción se registra cuando el *propietario de esta* inicia el panel de Advisor y hace clic en el botón **Obtener recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="f25a1-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="f25a1-123">Esta operación *solo se realiza una vez*.</span><span class="sxs-lookup"><span data-stu-id="f25a1-123">This is a *one-time operation*.</span></span> <span data-ttu-id="f25a1-124">Una vez registrada la suscripción, puede acceder a las recomendaciones de Advisor como *Propietario*, *Contribuidor* o *Lector* para una suscripción, un grupo de recursos o un recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="f25a1-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f25a1-125">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f25a1-125">Next steps</span></span>

<span data-ttu-id="f25a1-126">Para aprender más sobre las recomendaciones de Advisor, consulte:</span><span class="sxs-lookup"><span data-stu-id="f25a1-126">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="f25a1-127">Introducción a Advisor</span><span class="sxs-lookup"><span data-stu-id="f25a1-127">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="f25a1-128">Introducción a Advisor</span><span class="sxs-lookup"><span data-stu-id="f25a1-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="f25a1-129">Recomendaciones sobre el costo de Advisor</span><span class="sxs-lookup"><span data-stu-id="f25a1-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="f25a1-130">Recomendaciones sobre rendimiento de Advisor</span><span class="sxs-lookup"><span data-stu-id="f25a1-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="f25a1-131">Recomendaciones sobre alta disponibilidad de Advisor</span><span class="sxs-lookup"><span data-stu-id="f25a1-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
