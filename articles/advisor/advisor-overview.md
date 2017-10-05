---
title: "Introducción a Azure Advisor | Microsoft Docs"
description: Utilice Azure Advisor para optimizar las implementaciones de Azure.
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
ms.openlocfilehash: 35678142550f9f887562f311a5e7d9516495cf53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-azure-advisor"></a><span data-ttu-id="7b168-103">Introducción a Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="7b168-103">Introduction to Azure Advisor</span></span>

<span data-ttu-id="7b168-104">Obtenga información sobre Azure Advisor y sus funcionalidades clave, y obtenga respuesta a las preguntas más frecuentes.</span><span class="sxs-lookup"><span data-stu-id="7b168-104">Learn about Azure Advisor and its key capabilities, and get answers to frequently asked questions.</span></span>

## <a name="what-is-advisor"></a><span data-ttu-id="7b168-105">¿Qué es Advisor?</span><span class="sxs-lookup"><span data-stu-id="7b168-105">What is Advisor?</span></span>
<span data-ttu-id="7b168-106">Advisor es un consultor personalizado en la nube que lo ayuda a seguir procedimientos recomendados para optimizar las implementaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b168-106">Advisor is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments.</span></span> <span data-ttu-id="7b168-107">Analiza la configuración de recursos y la telemetría de uso, y recomienda soluciones que pueden ayudar a mejoran la rentabilidad, el rendimiento, la alta disponibilidad y la seguridad de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b168-107">It analyzes your resource configuration and usage telemetry and then recommends solutions that can help you improve the cost effectiveness, performance, high availability, and security of your Azure resources.</span></span>

<span data-ttu-id="7b168-108">Con Advisor, puede:</span><span class="sxs-lookup"><span data-stu-id="7b168-108">With Advisor, you can:</span></span>
* <span data-ttu-id="7b168-109">Obtener sugerencias de procedimientos recomendados proactivas, prácticas y personalizadas,</span><span class="sxs-lookup"><span data-stu-id="7b168-109">Get proactive, actionable, and personalized best practices recommendations.</span></span> 
* <span data-ttu-id="7b168-110">Mejorar el rendimiento, la seguridad y la alta disponibilidad de los recursos, al mismo tiempo que identifica oportunidades para reducir el gasto general de Azure, y</span><span class="sxs-lookup"><span data-stu-id="7b168-110">Improve the performance, security, and high availability of your resources, as you identify opportunities to reduce your overall Azure spend.</span></span>
* <span data-ttu-id="7b168-111">Obtener recomendaciones con acciones propuestas en línea.</span><span class="sxs-lookup"><span data-stu-id="7b168-111">Get recommendations with proposed actions inline.</span></span>

<span data-ttu-id="7b168-112">Puede acceder a Advisor mediante [Azure Portal](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="7b168-112">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="7b168-113">Inicie sesión en [Azure Portal](https://portal.azure.com), seleccione **Examinar** y desplácese a **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="7b168-113">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="7b168-114">El panel de Advisor muestra recomendaciones personalizadas de la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="7b168-114">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="7b168-115">Las recomendaciones se dividen en cuatro categorías:</span><span class="sxs-lookup"><span data-stu-id="7b168-115">The recommendations are divided into four categories:</span></span> 

* <span data-ttu-id="7b168-116">**Alta disponibilidad**: lo ayuda a garantizar y mejorar la continuidad de las aplicaciones empresariales críticas.</span><span class="sxs-lookup"><span data-stu-id="7b168-116">**High Availability**: To ensure and improve the continuity of your business-critical applications.</span></span> <span data-ttu-id="7b168-117">Para obtener más información, consulte las [recomendaciones sobre alta disponibilidad de Advisor](advisor-high-availability-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="7b168-117">For more information, see [Advisor High Availability recommendations](advisor-high-availability-recommendations.md).</span></span>

* <span data-ttu-id="7b168-118">**Seguridad**: lo ayuda a detectar amenazas y vulnerabilidades que podrían dar lugar a infracciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7b168-118">**Security**: To detect threats and vulnerabilities that might lead to security breaches.</span></span> <span data-ttu-id="7b168-119">Para obtener más información, consulte las [recomendaciones sobre seguridad de Advisor](advisor-security-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="7b168-119">For more information, see [Advisor Security recommendations](advisor-security-recommendations.md).</span></span>

* <span data-ttu-id="7b168-120">**Rendimiento**: lo ayuda a mejorar la velocidad de las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7b168-120">**Performance**: To improve the speed of your applications.</span></span> <span data-ttu-id="7b168-121">Para obtener más información, consulte las [recomendaciones sobre rendimiento de Advisor](advisor-performance-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="7b168-121">For more information, see [Advisor Performance recommendations](advisor-performance-recommendations.md).</span></span>

* <span data-ttu-id="7b168-122">**Costo**: lo ayuda a optimizar y reducir el gasto general de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b168-122">**Cost**: To optimize and reduce your overall Azure spend.</span></span> <span data-ttu-id="7b168-123">Para obtener más información, consulte las [recomendaciones sobre el costo de Advisor](advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="7b168-123">For more information, see [Advisor Cost recommendations](advisor-cost-recommendations.md).</span></span>

  ![Tipos de recomendaciones de Advisor](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> <span data-ttu-id="7b168-125">Para acceder a las recomendaciones de Advisor, primero debe *registrar su suscripción* en dicha solución.</span><span class="sxs-lookup"><span data-stu-id="7b168-125">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="7b168-126">Una suscripción se registra cuando el *propietario de esta* inicia el panel de Advisor y hace clic en el botón **Obtener recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="7b168-126">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="7b168-127">Esta operación *solo se realiza una vez*.</span><span class="sxs-lookup"><span data-stu-id="7b168-127">This is a *one-time operation*.</span></span> <span data-ttu-id="7b168-128">Una vez registrada la suscripción, puede acceder a las recomendaciones de Advisor como *Propietario*, *Contribuidor* o *Lector* para una suscripción, un grupo de recursos o un recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="7b168-128">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

<span data-ttu-id="7b168-129">Puede hacer clic en una recomendación para saber más sobre ella.</span><span class="sxs-lookup"><span data-stu-id="7b168-129">You can click a recommendation to learn more about it.</span></span> <span data-ttu-id="7b168-130">También puede aprender más sobre las acciones que puede llevar a cabo para aprovechar las ventajas de una oportunidad o resolver un problema.</span><span class="sxs-lookup"><span data-stu-id="7b168-130">You can also learn about actions that you can perform to take advantage of an opportunity or resolve an issue.</span></span> 

<span data-ttu-id="7b168-131">Advisor ofrece recomendaciones con acciones insertadas o vínculos de documentación.</span><span class="sxs-lookup"><span data-stu-id="7b168-131">Advisor offers recommendations with inline actions or documentation links.</span></span> <span data-ttu-id="7b168-132">Al hacer clic en una acción insertada, se inicia un "viaje de usuario guiado" para implementarla.</span><span class="sxs-lookup"><span data-stu-id="7b168-132">Clicking an inline action takes you through a “guided user journey” to implement it.</span></span> <span data-ttu-id="7b168-133">Al hacer clic en un vínculo de documentación, se le remite a documentación que describe cómo llevar a cabo la acción de forma manual.</span><span class="sxs-lookup"><span data-stu-id="7b168-133">Clicking a documentation link points you to documentation that describes how to manually implement the action.</span></span> 

<span data-ttu-id="7b168-134">Advisor actualiza las recomendaciones cada hora.</span><span class="sxs-lookup"><span data-stu-id="7b168-134">Advisor updates recommendations hourly.</span></span> <span data-ttu-id="7b168-135">Si no desea realizar de inmediato una acción basada en una recomendación, puede posponerla durante un período de tiempo o descartarla.</span><span class="sxs-lookup"><span data-stu-id="7b168-135">If you don’t intend to take immediate action on a recommendation, you can snooze it for a specified time period or dismiss it.</span></span> 

## <a name="frequently-asked-questions"></a><span data-ttu-id="7b168-136">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="7b168-136">Frequently asked questions</span></span>

### <a name="how-do-i-access-advisor"></a><span data-ttu-id="7b168-137">¿Cómo se accede a Advisor?</span><span class="sxs-lookup"><span data-stu-id="7b168-137">How do I access Advisor?</span></span>
<span data-ttu-id="7b168-138">Puede acceder a Advisor mediante [Azure Portal](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="7b168-138">You can access Advisor through the [Azure portal](https://aka.ms/azureadvisordashboard).</span></span> <span data-ttu-id="7b168-139">Inicie sesión en [Azure Portal](https://portal.azure.com), seleccione **Examinar** y desplácese a **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="7b168-139">Sign in to the [portal](https://portal.azure.com), select **Browse**, and then scroll to **Azure Advisor**.</span></span> <span data-ttu-id="7b168-140">El panel de Advisor muestra recomendaciones personalizadas de la suscripción seleccionada.</span><span class="sxs-lookup"><span data-stu-id="7b168-140">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

<span data-ttu-id="7b168-141">También puede ver las recomendaciones de Advisor a través de la hoja de recursos de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7b168-141">You can also view Advisor recommendations through the virtual machine resource blade.</span></span> <span data-ttu-id="7b168-142">Seleccione una máquina virtual y después desplácese a las recomendaciones de Advisor en el menú.</span><span class="sxs-lookup"><span data-stu-id="7b168-142">Choose a virtual machine, and then scroll to Advisor recommendations in the menu.</span></span> 

### <a name="what-permissions-do-i-need-to-access-advisor"></a><span data-ttu-id="7b168-143">¿Qué permisos son necesarios para acceder a Advisor?</span><span class="sxs-lookup"><span data-stu-id="7b168-143">What permissions do I need to access Advisor?</span></span>

<span data-ttu-id="7b168-144">Para acceder a las recomendaciones de Advisor, primero debe *registrar su suscripción* en dicha solución.</span><span class="sxs-lookup"><span data-stu-id="7b168-144">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="7b168-145">Una suscripción se registra cuando el *propietario de esta* inicia el panel de Advisor y hace clic en el botón **Obtener recomendaciones**.</span><span class="sxs-lookup"><span data-stu-id="7b168-145">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="7b168-146">Esta operación *solo se realiza una vez*.</span><span class="sxs-lookup"><span data-stu-id="7b168-146">This is a *one-time operation*.</span></span> <span data-ttu-id="7b168-147">Una vez registrada la suscripción, puede acceder a las recomendaciones de Advisor como *Propietario*, *Contribuidor* o *Lector* para una suscripción, un grupo de recursos o un recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="7b168-147">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

### <a name="how-often-are-advisor-recommendations-updated"></a><span data-ttu-id="7b168-148">¿Con qué frecuencia se actualizan las recomendaciones de Advisor?</span><span class="sxs-lookup"><span data-stu-id="7b168-148">How often are Advisor recommendations updated?</span></span>

<span data-ttu-id="7b168-149">Las recomendaciones de Advisor se actualizan cada hora.</span><span class="sxs-lookup"><span data-stu-id="7b168-149">Advisor recommendations are updated hourly.</span></span>

### <a name="what-resources-does-advisor-provide-recommendations-for"></a><span data-ttu-id="7b168-150">¿Para qué recursos Advisor ofrece recomendaciones?</span><span class="sxs-lookup"><span data-stu-id="7b168-150">What resources does Advisor provide recommendations for?</span></span>

<span data-ttu-id="7b168-151">Advisor proporciona recomendaciones para máquinas virtuales, conjuntos de disponibilidad, puertas de enlace de aplicaciones, App Services, servidores SQL Server, bases de datos SQL y Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="7b168-151">Advisor provides recommendations for virtual machines, availability sets, application gateways, App Services, SQL servers, SQL databases, and Redis Cache.</span></span>

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a><span data-ttu-id="7b168-152">¿Se puede posponer o descartar una recomendación?</span><span class="sxs-lookup"><span data-stu-id="7b168-152">Can I snooze or dismiss a recommendation?</span></span>

<span data-ttu-id="7b168-153">Para posponer o descartar una recomendación, haga clic en el botón o vínculo **Snooze** (Posponer).</span><span class="sxs-lookup"><span data-stu-id="7b168-153">To snooze or dismiss a recommendation, click the **Snooze** button or link.</span></span> <span data-ttu-id="7b168-154">Puede especificar un tiempo de posposición o seleccionar **Never** (Nunca) para descartar la recomendación.</span><span class="sxs-lookup"><span data-stu-id="7b168-154">You can specify a snooze time period or select **Never** to dismiss the recommendation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b168-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7b168-155">Next steps</span></span>

<span data-ttu-id="7b168-156">Para aprender más sobre las recomendaciones de Advisor, consulte:</span><span class="sxs-lookup"><span data-stu-id="7b168-156">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="7b168-157">Introducción a Advisor</span><span class="sxs-lookup"><span data-stu-id="7b168-157">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="7b168-158">Recomendaciones sobre alta disponibilidad de Advisor</span><span class="sxs-lookup"><span data-stu-id="7b168-158">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="7b168-159">Recomendaciones sobre seguridad de Advisor</span><span class="sxs-lookup"><span data-stu-id="7b168-159">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
* [<span data-ttu-id="7b168-160">Recomendaciones sobre rendimiento de Advisor</span><span class="sxs-lookup"><span data-stu-id="7b168-160">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="7b168-161">Recomendaciones sobre el costo de Advisor</span><span class="sxs-lookup"><span data-stu-id="7b168-161">Advisor Cost recommendations</span></span>](advisor-cost-recommendations.md)
