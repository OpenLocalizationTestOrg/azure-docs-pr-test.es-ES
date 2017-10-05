---
title: "Aplicación de actualizaciones del sistema en Azure Security Center | Microsoft Docs"
description: "En este documento se muestra cómo implementar las recomendaciones de **Aplicar actualizaciones del sistema** y **Reiniciar tras actualizar el sistema** de Azure Security Center."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="c3ac8-103">Aplicar actualizaciones del sistema en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="c3ac8-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="c3ac8-104">Azure Security Center supervisa diariamente las máquinas virtuales Windows y Linux por si faltan actualizaciones de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="c3ac8-105">Security Center recupera una lista de actualizaciones críticas y de seguridad disponibles desde Windows Update o Windows Server Update Services (WSUS), dependiendo de qué servicio está configurado en una máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="c3ac8-106">Security Center comprueba también las últimas actualizaciones de los sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="c3ac8-107">Si falta una actualización del sistema en la máquina virtual, Security Center le recomendará que aplique las actualizaciones del sistema</span><span class="sxs-lookup"><span data-stu-id="c3ac8-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="c3ac8-108">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="c3ac8-109">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="c3ac8-110">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="c3ac8-110">Implement the recommendation</span></span>
1. <span data-ttu-id="c3ac8-111">En la hoja **Recomendaciones**, seleccione **Aplicar actualizaciones del sistema**.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Aplicar actualizaciones del sistema][1]
2. <span data-ttu-id="c3ac8-113">Se abre la hoja **Aplicar actualizaciones del sistema** con una lista de las máquinas virtuales en las que faltan actualizaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="c3ac8-114">Seleccione una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-114">Select a VM.</span></span>

   ![Seleccionar una máquina virtual][2]
3. <span data-ttu-id="c3ac8-116">Se abre una hoja que muestra una lista de las actualizaciones que faltan en esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="c3ac8-117">Seleccione una actualización del sistema.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-117">Select a system update.</span></span> <span data-ttu-id="c3ac8-118">En este ejemplo, vamos a seleccionar KB3156016.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-118">In this example, let’s select KB3156016.</span></span>

   ![Actualizaciones de seguridad que faltan][3]

4. <span data-ttu-id="c3ac8-120">Siga los pasos de la hoja **Actualización de seguridad** para aplicar la actualización que falta.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![Actualización de seguridad][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="c3ac8-122">Reiniciar tras actualizar el sistema</span><span class="sxs-lookup"><span data-stu-id="c3ac8-122">Reboot after system updates</span></span>
1. <span data-ttu-id="c3ac8-123">Vuelva a la hoja **Recomendaciones** .</span><span class="sxs-lookup"><span data-stu-id="c3ac8-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="c3ac8-124">Se genera una nueva entrada después de aplicar las actualizaciones del sistema, denominada **Reiniciar tras actualizar el sistema**.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="c3ac8-125">Esta entrada permite saber que tiene que reiniciar la máquina virtual para completar el proceso de aplicación de las actualizaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![Reiniciar tras actualizar el sistema][5]
2. <span data-ttu-id="c3ac8-127">Seleccione **Reiniciar tras actualizar el sistema**.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="c3ac8-128">Se abre la hoja **Hay un reinicio pendiente para completar las actualizaciones del sistema** que muestra una lista de máquinas virtuales que deben reiniciarse para completar el proceso de aplicación de actualizaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![Reinicio pendiente][6]

<span data-ttu-id="c3ac8-130">Reinicie la máquina virtual de Azure para completar el proceso.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="c3ac8-131">Consulte también</span><span class="sxs-lookup"><span data-stu-id="c3ac8-131">See also</span></span>
<span data-ttu-id="c3ac8-132">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="c3ac8-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="c3ac8-133">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c3ac8-134">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c3ac8-135">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="c3ac8-136">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="c3ac8-137">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="c3ac8-138">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md) : busque las preguntas más frecuentes sobre cómo usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="c3ac8-139">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="c3ac8-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
