---
title: soluciones de socios de aaaManaging en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento le guía a través de cómo Azure Security Center permite a supervisar en un estado de mantenimiento de Hola de vista de las soluciones de socios comerciales integrado con su suscripción de Azure."
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
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="50cc2-103">Supervisión de las soluciones de asociados con Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="50cc2-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="50cc2-104">Este documento le guía a través de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales en el centro de seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="50cc2-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="50cc2-105">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="50cc2-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="50cc2-106">Este documento no es una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="50cc2-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="50cc2-107">Supervisión de soluciones de asociados</span><span class="sxs-lookup"><span data-stu-id="50cc2-107">Monitoring partner solutions</span></span>
<span data-ttu-id="50cc2-108">Hola **soluciones de asociados** icono hello **centro de seguridad** permite hoja supervisar en un estado de mantenimiento de Hola de vista de las soluciones de socios comerciales que se integran con la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="50cc2-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Icono Partner solutions (Soluciones de asociados)][1]

<span data-ttu-id="50cc2-110">Hola **soluciones de asociados** mosaico muestra el número de Hola de soluciones de socios integrado con su suscripción.</span><span class="sxs-lookup"><span data-stu-id="50cc2-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="50cc2-111">Si no hay ningún soluciones integradas, icono hello muestra hello número cero.</span><span class="sxs-lookup"><span data-stu-id="50cc2-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="50cc2-112">estado de hello tooview de las soluciones de socios comerciales:</span><span class="sxs-lookup"><span data-stu-id="50cc2-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="50cc2-113">Seleccione hello **soluciones de asociados** icono.</span><span class="sxs-lookup"><span data-stu-id="50cc2-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="50cc2-114">Hola **soluciones de asociados** abre hoja muestra una lista de las soluciones de socios comerciales conectado tooSecurity Center.</span><span class="sxs-lookup"><span data-stu-id="50cc2-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![Soluciones de socios][3]

   <span data-ttu-id="50cc2-116">estado de Hola de una solución de socio comercial puede ser:</span><span class="sxs-lookup"><span data-stu-id="50cc2-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="50cc2-117">Protegido (verde): no hay ningún problema de estado.</span><span class="sxs-lookup"><span data-stu-id="50cc2-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="50cc2-118">Incorrecto (rojo): hay un problema de estado que requiere atención inmediata.</span><span class="sxs-lookup"><span data-stu-id="50cc2-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="50cc2-119">Detenido informes (naranja) - solución Hola dejó de informar sobre su estado.</span><span class="sxs-lookup"><span data-stu-id="50cc2-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="50cc2-120">Estado de protección desconocido (naranja) - estado de Hola de solución de hello es desconocido en este momento debido proceso tooa no se pudo agregar una nueva solución existente de toohello de recursos.</span><span class="sxs-lookup"><span data-stu-id="50cc2-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="50cc2-121">No se notifica (gris) - solución hello no ha notificado nada todavía, el estado de la solución puede ser no notificado si recientemente ha conectado y todavía se está implementando.</span><span class="sxs-lookup"><span data-stu-id="50cc2-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="50cc2-122">Seleccione una solución de asociado.</span><span class="sxs-lookup"><span data-stu-id="50cc2-122">Select a partner solution.</span></span> <span data-ttu-id="50cc2-123">En este ejemplo, permite seleccionar hello **Qualys** solución.</span><span class="sxs-lookup"><span data-stu-id="50cc2-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="50cc2-124">Una hoja se abre con estado de Hola de solución de socios de Hola y de la solución de Hola los recursos asociados.</span><span class="sxs-lookup"><span data-stu-id="50cc2-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="50cc2-125">Seleccione **consola de solución** la experiencia de administración de socios comerciales de hello tooopen de esta solución.</span><span class="sxs-lookup"><span data-stu-id="50cc2-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![Detalle de solución de asociado][4]
3. <span data-ttu-id="50cc2-127">Volver atrás toohello **Qualys** hoja y seleccione **vínculo VM**.</span><span class="sxs-lookup"><span data-stu-id="50cc2-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="50cc2-128">Hola **aplicaciones de vínculo** abre la hoja.</span><span class="sxs-lookup"><span data-stu-id="50cc2-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="50cc2-129">Aquí puede conectarse solución de socios de recursos toohello.</span><span class="sxs-lookup"><span data-stu-id="50cc2-129">Here you can connect resources toohello partner solution.</span></span>

   ![Solución de toopartner de recursos de vínculo][5]

## <a name="next-steps"></a><span data-ttu-id="50cc2-131">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="50cc2-131">Next steps</span></span>
<span data-ttu-id="50cc2-132">En este documento, eran toohello se ha introducido **soluciones de socios** el icono Centro de seguridad.</span><span class="sxs-lookup"><span data-stu-id="50cc2-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="50cc2-133">toolearn más información acerca del centro de seguridad, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="50cc2-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="50cc2-134">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : más información cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="50cc2-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="50cc2-135">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que lo ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="50cc2-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="50cc2-136">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="50cc2-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="50cc2-137">[Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md) : más información cómo toomanage y que responden las alertas de toosecurity.</span><span class="sxs-lookup"><span data-stu-id="50cc2-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="50cc2-138">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="50cc2-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="50cc2-139">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="50cc2-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
