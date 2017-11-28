---
title: "aaaEnable agente de máquina virtual en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** agente ** de habilitar la máquina virtual."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="6faea-103">Habilitación del Agente de máquina virtual en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="6faea-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="6faea-104">Hello agente de máquina virtual debe instalarse en máquinas virtuales (VM) en orden demasiado[habilitar la recopilación de datos](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="6faea-104">hello VM Agent must be installed on virtual machines (VMs) in order too[enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="6faea-105">Habilita el centro de seguridad de Azure se toosee que las máquinas virtuales requieren Hola a agente de máquina virtual y se recomienda que habilite Hola a agente de máquina virtual en esas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="6faea-105">Azure Security Center enables you toosee which VMs require hello VM Agent and will recommend that you enable hello VM Agent on those VMs.</span></span>

<span data-ttu-id="6faea-106">Hola agente de máquina virtual está instalado de forma predeterminada para las máquinas virtuales que se implementan desde hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6faea-106">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="6faea-107">artículo de Hello [agente de máquina virtual y extensiones: parte 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) proporciona información acerca de cómo tooinstall Hola agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6faea-107">hello article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="6faea-108">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6faea-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="6faea-109">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="6faea-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="6faea-110">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="6faea-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="6faea-111">Hola **hoja de recomendaciones**, seleccione **habilitar agente de máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="6faea-111">In hello **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="6faea-112">![Habilitar el Agente de máquina virtual][1]</span><span class="sxs-lookup"><span data-stu-id="6faea-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="6faea-113">Esto abre una hoja de hello **VM agente falta o no responde**.</span><span class="sxs-lookup"><span data-stu-id="6faea-113">This opens hello blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="6faea-114">Esta hoja enumera las máquinas virtuales de Hola que requieren Hola agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6faea-114">This blade lists hello VMs that require hello VM Agent.</span></span> <span data-ttu-id="6faea-115">Siga las instrucciones de hello en el agente de máquina virtual de hello hoja tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="6faea-115">Follow hello instructions on hello blade tooinstall hello VM agent.</span></span>
   <span data-ttu-id="6faea-116">![Agente de máquina virtual ausente][2]</span><span class="sxs-lookup"><span data-stu-id="6faea-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="6faea-117">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="6faea-117">See also</span></span>
<span data-ttu-id="6faea-118">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="6faea-118">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="6faea-119">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md): Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="6faea-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="6faea-120">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que lo ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6faea-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="6faea-121">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md): Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6faea-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="6faea-122">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md): Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="6faea-122">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="6faea-123">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="6faea-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="6faea-124">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md)--buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6faea-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="6faea-125">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtener información y noticias de seguridad de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="6faea-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
