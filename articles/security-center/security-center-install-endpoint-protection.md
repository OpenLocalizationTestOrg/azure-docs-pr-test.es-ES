---
title: aaaInstall Endpoint Protection en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** instalar Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="8c50c-103">Instalación de Endpoint Protection en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8c50c-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="8c50c-104">Azure Security Center recomienda instalar Endpoint Protection en las máquinas virtuales de Azure si aún no se ha habilitado esta solución.</span><span class="sxs-lookup"><span data-stu-id="8c50c-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="8c50c-105">Esta recomendación aplica tooWindows máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8c50c-105">This recommendation applies tooWindows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="8c50c-106">En esta implementación de ejemplo se utiliza Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="8c50c-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="8c50c-107">Consulte [Integración de asociados en Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) para ver una lista de asociados integrados con Security Center.</span><span class="sxs-lookup"><span data-stu-id="8c50c-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="8c50c-108">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="8c50c-108">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="8c50c-109">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8c50c-109">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="8c50c-110">Este documento no es una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="8c50c-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="8c50c-111">Hola **recomendaciones** hoja, seleccione **instalar Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="8c50c-111">In hello **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="8c50c-112">![Selección de instalar Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="8c50c-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="8c50c-113">Hola **instalar Endpoint Protection** hoja abrirá mostrando una lista de las máquinas virtuales sin protección de extremo.</span><span class="sxs-lookup"><span data-stu-id="8c50c-113">hello **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="8c50c-114">Seleccione uno de Hola Hola de lista máquinas virtuales que desea que tooinstall endpoint protection en y haga clic en **instalar en máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="8c50c-114">Select from hello list hello VMs that you want tooinstall endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="8c50c-115">![Seleccione las máquinas virtuales tooinstall Endpoint Protection en][2]</span><span class="sxs-lookup"><span data-stu-id="8c50c-115">![Select VMs tooinstall Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="8c50c-116">Hola **seleccione Endpoint Protection** hoja abre tooallow se tooselect Hola extremo solución de protección que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="8c50c-116">hello **Select Endpoint Protection** blade opens tooallow you tooselect hello endpoint protection solution you want toouse.</span></span> <span data-ttu-id="8c50c-117">En este ejemplo, vamos a seleccionar **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="8c50c-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="8c50c-118">![Select Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="8c50c-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="8c50c-119">Se muestra información adicional sobre solución de protección de extremo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c50c-119">Additional information about hello endpoint protection solution is displayed.</span></span> <span data-ttu-id="8c50c-120">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8c50c-120">Select **Create**.</span></span>
   <span data-ttu-id="8c50c-121">![Creación de solución antimalware][4]</span><span class="sxs-lookup"><span data-stu-id="8c50c-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="8c50c-122">Escriba valores de configuración de hello necesario en hello **Agregar extensión** hoja y, a continuación, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8c50c-122">Enter hello required configuration settings on hello **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="8c50c-123">toolearn más información acerca de los valores de configuración de hello, consulte [predeterminadas y configuración de Antimalware personalizada](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="8c50c-123">toolearn more about hello configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="8c50c-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) está activo en hello selecciona las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8c50c-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="8c50c-125">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="8c50c-125">See also</span></span>
<span data-ttu-id="8c50c-126">En este artículo se ha explicado cómo tooimplement Hola recomendación de centro de seguridad "Instalar Endpoint Protection".</span><span class="sxs-lookup"><span data-stu-id="8c50c-126">This article showed you how tooimplement hello Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="8c50c-127">toolearn más acerca de cómo habilitar Microsoft Antimalware en Azure, vea Hola siguiente documento:</span><span class="sxs-lookup"><span data-stu-id="8c50c-127">toolearn more about enabling Microsoft Antimalware in Azure, see hello following document:</span></span>

* <span data-ttu-id="8c50c-128">[Microsoft Antimalware para servicios en la nube y máquinas virtuales](../security/azure-security-antimalware.md) : Obtenga información acerca de cómo toodeploy Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="8c50c-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how toodeploy Microsoft Antimalware.</span></span>

<span data-ttu-id="8c50c-129">toolearn más información acerca del centro de seguridad, vea Hola siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="8c50c-129">toolearn more about Security Center, see hello following documents:</span></span>

* <span data-ttu-id="8c50c-130">[Configuración de directivas de seguridad en el centro de seguridad de Azure](security-center-policies.md) : Obtenga información acerca de cómo las directivas de seguridad de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="8c50c-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="8c50c-131">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c50c-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="8c50c-132">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c50c-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="8c50c-133">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="8c50c-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="8c50c-134">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="8c50c-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="8c50c-135">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8c50c-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="8c50c-136">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="8c50c-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
