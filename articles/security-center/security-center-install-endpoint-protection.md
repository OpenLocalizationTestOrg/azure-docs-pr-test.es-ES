---
title: "Instalación de Endpoint Protection en Azure Security Center | Microsoft Docs"
description: "En este documento, mostramos cómo implementar la recomendación de instalar Endpoint Protection de Azure Security Center."
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
ms.openlocfilehash: efb86a0ae362c30a6772c391a499154b7ae2a697
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="fc516-103">Instalación de Endpoint Protection en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="fc516-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="fc516-104">Azure Security Center recomienda instalar Endpoint Protection en las máquinas virtuales de Azure si aún no se ha habilitado esta solución.</span><span class="sxs-lookup"><span data-stu-id="fc516-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="fc516-105">Esta recomendación se aplica únicamente a las máquinas virtuales de Windows.</span><span class="sxs-lookup"><span data-stu-id="fc516-105">This recommendation applies to Windows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="fc516-106">En esta implementación de ejemplo se utiliza Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="fc516-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="fc516-107">Consulte [Integración de asociados en Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) para ver una lista de asociados integrados con Security Center.</span><span class="sxs-lookup"><span data-stu-id="fc516-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="fc516-108">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="fc516-108">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="fc516-109">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="fc516-109">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="fc516-110">Este documento no es una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="fc516-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="fc516-111">En la hoja **Recomendaciones**, seleccione **Instalar Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="fc516-111">In the **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="fc516-112">![Selección de instalar Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="fc516-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="fc516-113">Se abre la hoja **Instalar Endpoint Protection** con una lista de máquinas virtuales sin Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="fc516-113">The **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="fc516-114">Seleccione en la lista las máquinas virtuales en las que quiere instalar Endpoint Protection y haga clic en **Install on VMs** (Instalar en máquinas virtuales).</span><span class="sxs-lookup"><span data-stu-id="fc516-114">Select from the list the VMs that you want to install endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="fc516-115">![Selección de máquinas virtuales en las que instalar Endpoint Protection][2]</span><span class="sxs-lookup"><span data-stu-id="fc516-115">![Select VMs to install Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="fc516-116">Se abre la hoja **Seleccionar Endpoint Protection**, que permite seleccionar la solución Endpoint Protection que quiere usar.</span><span class="sxs-lookup"><span data-stu-id="fc516-116">The **Select Endpoint Protection** blade opens to allow you to select the endpoint protection solution you want to use.</span></span> <span data-ttu-id="fc516-117">En este ejemplo, vamos a seleccionar **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="fc516-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="fc516-118">![Select Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="fc516-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="fc516-119">Aparece información adicional sobre la solución Endpoint Protection.</span><span class="sxs-lookup"><span data-stu-id="fc516-119">Additional information about the endpoint protection solution is displayed.</span></span> <span data-ttu-id="fc516-120">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fc516-120">Select **Create**.</span></span>
   <span data-ttu-id="fc516-121">![Creación de solución antimalware][4]</span><span class="sxs-lookup"><span data-stu-id="fc516-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="fc516-122">Escriba las opciones de configuración requeridas en la hoja **Agregar extensión** y seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fc516-122">Enter the required configuration settings on the **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="fc516-123">Para obtener más información acerca de las opciones de configuración, consulte [Configuración predeterminada y personalizada de Antimalware](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="fc516-123">To learn more about the configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="fc516-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) ahora está activo en las máquinas virtuales seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="fc516-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="fc516-125">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="fc516-125">See also</span></span>
<span data-ttu-id="fc516-126">En este documento, mostramos cómo implementar la recomendación "Instalar Endpoint Protection" de Security Center.</span><span class="sxs-lookup"><span data-stu-id="fc516-126">This article showed you how to implement the Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="fc516-127">Para obtener más información sobre cómo habilitar Microsoft Antimalware en Azure, consulte el siguiente documento:</span><span class="sxs-lookup"><span data-stu-id="fc516-127">To learn more about enabling Microsoft Antimalware in Azure, see the following document:</span></span>

* <span data-ttu-id="fc516-128">[Microsoft Antimalware para Azure Cloud Services y Virtual Machines](../security/azure-security-antimalware.md): aprenda a implementar Microsoft Antimalware.</span><span class="sxs-lookup"><span data-stu-id="fc516-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how to deploy Microsoft Antimalware.</span></span>

<span data-ttu-id="fc516-129">Para obtener más información sobre Security Center, consulte los siguientes documentos:</span><span class="sxs-lookup"><span data-stu-id="fc516-129">To learn more about Security Center, see the following documents:</span></span>

* <span data-ttu-id="fc516-130">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md) : aprenda a configurar directivas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fc516-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="fc516-131">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc516-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="fc516-132">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc516-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="fc516-133">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="fc516-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="fc516-134">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="fc516-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="fc516-135">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md) : busque las preguntas más frecuentes sobre cómo usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="fc516-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="fc516-136">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : encuentre publicaciones de blog sobre el cumplimiento y la seguridad de Azure.</span><span class="sxs-lookup"><span data-stu-id="fc516-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
