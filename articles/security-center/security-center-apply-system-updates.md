---
title: actualizaciones del sistema aaaApply en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendaciones de Azure Security Center ** aplicar las actualizaciones de sistema ** y ** reiniciar después de las actualizaciones de sistema **."
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
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="b7a96-103">Aplicar actualizaciones del sistema en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="b7a96-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="b7a96-104">Azure Security Center supervisa diariamente las máquinas virtuales Windows y Linux por si faltan actualizaciones de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="b7a96-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="b7a96-105">Security Center recupera una lista de actualizaciones críticas y de seguridad disponibles desde Windows Update o Windows Server Update Services (WSUS), dependiendo de qué servicio está configurado en una máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="b7a96-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="b7a96-106">Centro de seguridad también comprueba las actualizaciones más recientes de hello en sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="b7a96-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="b7a96-107">Si falta una actualización del sistema en la máquina virtual, Security Center le recomendará que aplique las actualizaciones del sistema</span><span class="sxs-lookup"><span data-stu-id="b7a96-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="b7a96-108">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b7a96-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="b7a96-109">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="b7a96-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="b7a96-110">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="b7a96-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="b7a96-111">Hola **recomendaciones** hoja, seleccione **aplicar actualizaciones del sistema**.</span><span class="sxs-lookup"><span data-stu-id="b7a96-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Aplicar actualizaciones del sistema][1]
2. <span data-ttu-id="b7a96-113">Hola **aplicar actualizaciones del sistema** hoja abrirá mostrando una lista de las máquinas virtuales que les faltan actualizaciones de sistema.</span><span class="sxs-lookup"><span data-stu-id="b7a96-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="b7a96-114">Seleccione una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b7a96-114">Select a VM.</span></span>

   ![Seleccionar una máquina virtual][2]
3. <span data-ttu-id="b7a96-116">Se abre una hoja que muestra una lista de las actualizaciones que faltan en esa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b7a96-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="b7a96-117">Seleccione una actualización del sistema.</span><span class="sxs-lookup"><span data-stu-id="b7a96-117">Select a system update.</span></span> <span data-ttu-id="b7a96-118">En este ejemplo, vamos a seleccionar KB3156016.</span><span class="sxs-lookup"><span data-stu-id="b7a96-118">In this example, let’s select KB3156016.</span></span>

   ![Actualizaciones de seguridad que faltan][3]

4. <span data-ttu-id="b7a96-120">Siga los pasos de Hola Hola **de actualizaciones de seguridad** tooapply hoja Hola actualización que falta.</span><span class="sxs-lookup"><span data-stu-id="b7a96-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![Actualización de seguridad][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="b7a96-122">Reiniciar tras actualizar el sistema</span><span class="sxs-lookup"><span data-stu-id="b7a96-122">Reboot after system updates</span></span>
1. <span data-ttu-id="b7a96-123">Devolver toohello **recomendaciones** hoja.</span><span class="sxs-lookup"><span data-stu-id="b7a96-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="b7a96-124">Se genera una nueva entrada después de aplicar las actualizaciones del sistema, denominada **Reiniciar tras actualizar el sistema**.</span><span class="sxs-lookup"><span data-stu-id="b7a96-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="b7a96-125">Esta entrada le permite saber que necesita proceso tooreboot Hola VM toocomplete Hola de aplicar las actualizaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="b7a96-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![Reiniciar tras actualizar el sistema][5]
2. <span data-ttu-id="b7a96-127">Seleccione **Reiniciar tras actualizar el sistema**.</span><span class="sxs-lookup"><span data-stu-id="b7a96-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="b7a96-128">Se abrirá **es reiniciar el equipo las actualizaciones del sistema pendiente toocomplete** hoja muestra una lista de las máquinas virtuales que necesite toorestart toocomplete Hola aplica proceso actualizaciones del sistema.</span><span class="sxs-lookup"><span data-stu-id="b7a96-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![Reinicio pendiente][6]

<span data-ttu-id="b7a96-130">Reinicie Hola VM desde el proceso de Azure toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="b7a96-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="b7a96-131">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="b7a96-131">See also</span></span>
<span data-ttu-id="b7a96-132">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b7a96-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="b7a96-133">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7a96-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="b7a96-134">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7a96-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="b7a96-135">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7a96-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="b7a96-136">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="b7a96-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="b7a96-137">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="b7a96-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="b7a96-138">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="b7a96-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="b7a96-139">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="b7a96-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
