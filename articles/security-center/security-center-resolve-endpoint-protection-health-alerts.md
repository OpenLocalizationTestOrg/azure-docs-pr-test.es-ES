---
title: aaaResolve de alertas de estado de endpoint protection en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** alertas de estado de resolver Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="780c4-103">Resolución de alertas de estado de Endpoint Protection en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="780c4-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="780c4-104">Azure Security Center recomendará resolver las alertas de estado detectadas de Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="780c4-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="780c4-105">Centro de seguridad le permite toosee qué máquinas virtuales (VM) tiene errores de protección de extremo y de cuántos.</span><span class="sxs-lookup"><span data-stu-id="780c4-105">Security Center enables you toosee which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="780c4-106">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="780c4-106">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="780c4-107">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="780c4-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="780c4-108">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="780c4-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="780c4-109">Hola **hoja de recomendaciones**, seleccione **las alertas de estado de Endpoint Protection de resolver**.</span><span class="sxs-lookup"><span data-stu-id="780c4-109">In hello **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="780c4-110">![Resolver alertas de estado de Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="780c4-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="780c4-111">Esto abre una hoja de hello **error de Endpoint Protection** que enumera las máquinas virtuales con errores y el número de Hola de errores para cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="780c4-111">This opens hello blade **Endpoint Protection failure** which lists VMs with failures and hello number of failures for each VM.</span></span> <span data-ttu-id="780c4-112">Seleccione una máquina virtual de hello lista.</span><span class="sxs-lookup"><span data-stu-id="780c4-112">Select a VM from hello list.</span></span>
   <span data-ttu-id="780c4-113">![Endpoint protection failure][2]</span><span class="sxs-lookup"><span data-stu-id="780c4-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="780c4-114">A **lista de errores de** hoja se abre para saludo seleccionado VM, mostrando una lista de errores.</span><span class="sxs-lookup"><span data-stu-id="780c4-114">A **Failures List** blade opens for hello selected VM, displaying a list of failures.</span></span> <span data-ttu-id="780c4-115">Seleccione un error de hello lista toolearn más.</span><span class="sxs-lookup"><span data-stu-id="780c4-115">Select a failure from hello list toolearn more.</span></span> <span data-ttu-id="780c4-116">Se abrirá una hoja con información sobre el error de hello seleccionado.</span><span class="sxs-lookup"><span data-stu-id="780c4-116">This opens a blade with information about hello selected failure.</span></span>
   <span data-ttu-id="780c4-117">![Lista de errores][3]
   ![Evento de error][4]</span><span class="sxs-lookup"><span data-stu-id="780c4-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="780c4-118">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="780c4-118">See also</span></span>
<span data-ttu-id="780c4-119">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="780c4-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="780c4-120">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md): Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="780c4-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="780c4-121">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que lo ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="780c4-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="780c4-122">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md): Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="780c4-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="780c4-123">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md): Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="780c4-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="780c4-124">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="780c4-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="780c4-125">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md)--buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="780c4-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="780c4-126">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtener información y noticias de seguridad de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="780c4-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
