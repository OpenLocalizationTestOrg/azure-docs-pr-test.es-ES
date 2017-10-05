---
title: "Habilitación del Agente de máquina virtual en Azure Security Center | Microsoft Docs"
description: "En este documento se muestra cómo implementar la recomendación de Azure Security Center de habilitar el Agente de máquina virtual."
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
ms.openlocfilehash: 337a7adfd93c76882a749685702bea6d1524c96a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="ecbe9-103">Habilitación del Agente de máquina virtual en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="ecbe9-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="ecbe9-104">El agente de máquina virtual debe instalarse en máquinas virtuales para [habilitar la recopilación de datos](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="ecbe9-104">The VM Agent must be installed on virtual machines (VMs) in order to [enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="ecbe9-105">Azure Security Center permite ver qué máquinas virtuales requieren el Agente de máquina virtual y recomienda habilitarlo en esas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-105">Azure Security Center enables you to see which VMs require the VM Agent and will recommend that you enable the VM Agent on those VMs.</span></span>

<span data-ttu-id="ecbe9-106">De manera predeterminada, el agente de máquina virtual está instalado en las máquinas virtuales que se implementan desde Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-106">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="ecbe9-107">El artículo [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) (Agente de VM y extensiones, parte 2) proporciona información sobre cómo instalar el Agente de VM.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-107">The article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="ecbe9-108">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="ecbe9-109">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="ecbe9-110">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="ecbe9-110">Implement the recommendation</span></span>
1. <span data-ttu-id="ecbe9-111">En la hoja **Recomendaciones**, seleccione **Habilitar el agente de máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-111">In the **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="ecbe9-112">![Habilitar el Agente de máquina virtual][1]</span><span class="sxs-lookup"><span data-stu-id="ecbe9-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="ecbe9-113">Se abrirá la hoja **VM Agent Is Missing Or Not Responding**(Agente de máquina virtual ausente o no responde).</span><span class="sxs-lookup"><span data-stu-id="ecbe9-113">This opens the blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="ecbe9-114">Esta hoja enumera las máquinas virtuales que requieren el Agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-114">This blade lists the VMs that require the VM Agent.</span></span> <span data-ttu-id="ecbe9-115">Siga las instrucciones de la hoja para instalar el Agente de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-115">Follow the instructions on the blade to install the VM agent.</span></span>
   <span data-ttu-id="ecbe9-116">![Agente de máquina virtual ausente][2]</span><span class="sxs-lookup"><span data-stu-id="ecbe9-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="ecbe9-117">Consulte también</span><span class="sxs-lookup"><span data-stu-id="ecbe9-117">See also</span></span>
<span data-ttu-id="ecbe9-118">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="ecbe9-118">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="ecbe9-119">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ecbe9-120">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que lo ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="ecbe9-121">[Supervisión del estado de seguridad en Centro de seguridad de Azure](security-center-monitoring.md): obtenga información sobre cómo supervisar el estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="ecbe9-122">[Administración y respuesta a las alertas de seguridad en el Centro de seguridad de Azure](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-122">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="ecbe9-123">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md) : aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="ecbe9-124">[Preguntas más frecuentes acerca del Centro de seguridad de Azure](security-center-faq.md): busque las preguntas más frecuentes sobre cómo usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="ecbe9-125">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtenga las últimas noticias e información sobre la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="ecbe9-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
