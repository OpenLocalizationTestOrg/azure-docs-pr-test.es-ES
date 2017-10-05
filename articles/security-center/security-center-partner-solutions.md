---
title: "Administración de soluciones de asociados en Azure Security Center | Microsoft Docs"
description: "En este documento se explica cómo Azure Security Center permite supervisar de un vistazo el estado de mantenimiento de las soluciones de asociados integradas con su suscripción de Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: 2ebb930e877c5027f4d7b0a316a7f5ebe84471b1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="30bc5-103">Supervisión de las soluciones de asociados con Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="30bc5-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="30bc5-104">En este documento se explica cómo supervisar el estado de mantenimiento de las soluciones de asociados en Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="30bc5-104">This document walks you through how to monitor the health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="30bc5-105">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="30bc5-105">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="30bc5-106">Este documento no es una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="30bc5-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="30bc5-107">Supervisión de soluciones de asociados</span><span class="sxs-lookup"><span data-stu-id="30bc5-107">Monitoring partner solutions</span></span>
<span data-ttu-id="30bc5-108">El icono de **Soluciones de asociados** de la hoja **Security Center** permite supervisar a simple vista el estado de mantenimiento de las soluciones de asociados que se integran con su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="30bc5-108">The **Partner solutions** tile on the **Security Center** blade lets you monitor at a glance the health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Icono Partner solutions (Soluciones de asociados)][1]

<span data-ttu-id="30bc5-110">El icono de **Soluciones de asociados** muestra el número de soluciones de asociados integradas en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="30bc5-110">The **Partner solutions** tile displays the number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="30bc5-111">Si no hay ninguna solución integrada, en el icono se muestra el número cero.</span><span class="sxs-lookup"><span data-stu-id="30bc5-111">If there are no solutions integrated, the tile displays the number zero.</span></span>

<span data-ttu-id="30bc5-112">Para ver el estado de sus soluciones de asociados:</span><span class="sxs-lookup"><span data-stu-id="30bc5-112">To view the health of your partner solutions:</span></span>

1. <span data-ttu-id="30bc5-113">Seleccione el icono **Soluciones de asociados** .</span><span class="sxs-lookup"><span data-stu-id="30bc5-113">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="30bc5-114">Se abre la hoja **Soluciones de asociados**, donde se muestra una lista de soluciones de asociados conectadas a Security Center.</span><span class="sxs-lookup"><span data-stu-id="30bc5-114">The **Partner solutions** blade opens displaying a list of your partner solutions connected to Security Center.</span></span>

   ![Soluciones de socios][3]

   <span data-ttu-id="30bc5-116">El estado de una solución de asociado puede ser:</span><span class="sxs-lookup"><span data-stu-id="30bc5-116">The status of a partner solution can be:</span></span>

   * <span data-ttu-id="30bc5-117">Protegido (verde): no hay ningún problema de estado.</span><span class="sxs-lookup"><span data-stu-id="30bc5-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="30bc5-118">Incorrecto (rojo): hay un problema de estado que requiere atención inmediata.</span><span class="sxs-lookup"><span data-stu-id="30bc5-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="30bc5-119">Información detenida (naranja): la solución ha dejado de informar sobre su estado.</span><span class="sxs-lookup"><span data-stu-id="30bc5-119">Stopped reporting (orange) - the solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="30bc5-120">Estado de protección desconocido (naranja): el estado de la solución se desconoce en este momento debido a un error en el proceso de agregación de un nuevo recurso a la solución existente.</span><span class="sxs-lookup"><span data-stu-id="30bc5-120">Unknown protection status (orange) - the health of the solution is unknown at this time due to a failed process of adding a new resource to the existing solution.</span></span>
   * <span data-ttu-id="30bc5-121">Sin información (gris): la solución no ha notificado nada todavía; es posible que el estado de una solución no se notifique si acaba de conectarse y todavía se está implementando.</span><span class="sxs-lookup"><span data-stu-id="30bc5-121">Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="30bc5-122">Seleccione una solución de asociado.</span><span class="sxs-lookup"><span data-stu-id="30bc5-122">Select a partner solution.</span></span> <span data-ttu-id="30bc5-123">En este ejemplo, se va a seleccionar la solución **Qualys**.</span><span class="sxs-lookup"><span data-stu-id="30bc5-123">In this example, lets select the **Qualys** solution.</span></span>  <span data-ttu-id="30bc5-124">Se abre una hoja que muestra que el estado de la solución de asociado y de sus recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="30bc5-124">A blade opens showing you the status of the partner solution and the solution's associated resources.</span></span> <span data-ttu-id="30bc5-125">Seleccione **Consola de soluciones** para abrir la experiencia de administración de asociados de esta solución.</span><span class="sxs-lookup"><span data-stu-id="30bc5-125">Select **Solution console** to open the partner management experience for this solution.</span></span>

   ![Detalle de solución de asociado][4]
3. <span data-ttu-id="30bc5-127">Vuelva a la hoja **Qualys** y seleccione **Vincular VM**.</span><span class="sxs-lookup"><span data-stu-id="30bc5-127">Go back to the **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="30bc5-128">Se abre la hoja **Link Applications** (Vincular aplicaciones).</span><span class="sxs-lookup"><span data-stu-id="30bc5-128">The **Link Applications** blade opens.</span></span> <span data-ttu-id="30bc5-129">Aquí puede conectar recursos a la solución de asociados.</span><span class="sxs-lookup"><span data-stu-id="30bc5-129">Here you can connect resources to the partner solution.</span></span>

   ![Vinculación de recursos a soluciones de asociados][5]

## <a name="next-steps"></a><span data-ttu-id="30bc5-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="30bc5-131">Next steps</span></span>
<span data-ttu-id="30bc5-132">En este documento, se ha presentado el icono **Partner Solutions** (Soluciones de asociados) de Security Center.</span><span class="sxs-lookup"><span data-stu-id="30bc5-132">In this document, you were introduced to the **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="30bc5-133">Para más información sobre Security Center, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="30bc5-133">To learn more about Security Center, see the following articles:</span></span>

* <span data-ttu-id="30bc5-134">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md) : aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="30bc5-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="30bc5-135">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que lo ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="30bc5-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="30bc5-136">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md) : obtenga información sobre cómo supervisar el estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="30bc5-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="30bc5-137">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md) : obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="30bc5-137">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="30bc5-138">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md) : encuentre las preguntas más frecuentes sobre el uso del servicio.</span><span class="sxs-lookup"><span data-stu-id="30bc5-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="30bc5-139">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenga las últimas noticias e información sobre la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="30bc5-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
