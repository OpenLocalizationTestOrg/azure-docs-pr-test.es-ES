---
title: "Actualización de la versión del sistema operativo en Azure Security Center | Microsoft Docs"
description: "En este artículo, mostramos cómo implementar la recomendación **Actualizar versión del sistema operativo** de Security Center."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: aa372492-ecdb-4368-8fdd-d8ed31e216ee
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: ce0d178914907750e5da59f223a4b1e04b9bb6fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="update-os-version-in-azure-security-center"></a><span data-ttu-id="444b8-103">Actualización de la versión del sistema operativo en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="444b8-103">Update OS version in Azure Security Center</span></span>
<span data-ttu-id="444b8-104">Para las máquinas virtuales de los servicios en la nube, Azure Security Center recomienda que se actualice el sistema operativo si hay disponible una versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="444b8-104">For virtual machines (VMs) in cloud services, Azure Security Center will recommend that the operating system (OS) be updated if there is a more recent version available.</span></span>  <span data-ttu-id="444b8-105">Se supervisan los roles de web y de trabajo de servicios en la nube que se ejecutan en espacios de producción.</span><span class="sxs-lookup"><span data-stu-id="444b8-105">Only cloud services web and worker roles running in production slots are monitored.</span></span>

> [!NOTE]
> <span data-ttu-id="444b8-106">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="444b8-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="444b8-107">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="444b8-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="444b8-108">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="444b8-108">Implement the recommendation</span></span>
1. <span data-ttu-id="444b8-109">En la hoja **Recomendaciones**, seleccione **Actualizar la versión del SO**.</span><span class="sxs-lookup"><span data-stu-id="444b8-109">In the **Recommendations** blade, select **Update OS version**.</span></span>
   <span data-ttu-id="444b8-110">![Actualizar versión del sistema operativo][1]</span><span class="sxs-lookup"><span data-stu-id="444b8-110">![Update OS version][1]</span></span>
2. <span data-ttu-id="444b8-111">Se abrirá la hoja **Actualizar versión del sistema operativo**.</span><span class="sxs-lookup"><span data-stu-id="444b8-111">This opens the blade **Update OS version**.</span></span> <span data-ttu-id="444b8-112">Siga los pasos de esta hoja para actualizar la versión del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="444b8-112">Follow the steps in this blade to update the OS version.</span></span>

## <a name="see-also"></a><span data-ttu-id="444b8-113">Consulte también</span><span class="sxs-lookup"><span data-stu-id="444b8-113">See also</span></span>
<span data-ttu-id="444b8-114">En este artículo, mostramos cómo implementar la recomendación "Actualizar versión del sistema operativo" de Security Center.</span><span class="sxs-lookup"><span data-stu-id="444b8-114">This article showed you how to implement the Security Center recommendation "Update OS version."</span></span> <span data-ttu-id="444b8-115">Para más información acerca de los servicios en la nube y la actualización de la versión de sistema operativo para un servicio en la nube, consulte:</span><span class="sxs-lookup"><span data-stu-id="444b8-115">To learn more about cloud services and updating the OS version for a cloud service, see:</span></span>

* [<span data-ttu-id="444b8-116">Información general de Servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="444b8-116">Cloud Services overview</span></span>](../cloud-services/cloud-services-choose-me.md)
* [<span data-ttu-id="444b8-117">Actualización de un servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="444b8-117">How to update a cloud service</span></span>](../cloud-services/cloud-services-update-azure-service.md)
* [<span data-ttu-id="444b8-118">Configuración de servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="444b8-118">How to Configure Cloud Services</span></span>](../cloud-services/cloud-services-how-to-configure-portal.md)

<span data-ttu-id="444b8-119">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="444b8-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="444b8-120">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="444b8-120">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="444b8-121">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="444b8-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="444b8-122">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="444b8-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="444b8-123">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="444b8-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="444b8-124">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="444b8-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="444b8-125">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md): busque las preguntas más frecuentes sobre cómo usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="444b8-125">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="444b8-126">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtenga las últimas noticias e información sobre la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="444b8-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-update-os-version/update-os-version.png
