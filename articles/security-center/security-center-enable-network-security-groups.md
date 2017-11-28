---
title: "Habilitación de grupos de seguridad de red en Azure Security Center | Microsoft Docs"
description: "En este documento, mostramos cómo implementar la recomendación de Azure Security Center **Habilitar los grupos de seguridad de red**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 1e034d59d8847f237fa0d4c772344d45cd618576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="f2550-103">Habilitación de los grupos de seguridad de red en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f2550-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="f2550-104">Azure Security Center recomienda habilitar un grupo de seguridad de red (NSG) si no hay ninguno habilitado.</span><span class="sxs-lookup"><span data-stu-id="f2550-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="f2550-105">Los NSG contienen una lista de reglas de la lista de control de acceso (ACL) que permiten o deniegan el tráfico de red a sus instancias de máquina virtual en una red virtual.</span><span class="sxs-lookup"><span data-stu-id="f2550-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="f2550-106">Los NSG se pueden asociar con las subredes o las instancias individuales de máquina virtual dentro de esa subred.</span><span class="sxs-lookup"><span data-stu-id="f2550-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="f2550-107">Cuando un NSG está asociado a una subred, las reglas de la ACL se aplican a todas las instancias de la máquina virtual de esa subred.</span><span class="sxs-lookup"><span data-stu-id="f2550-107">When an NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span> <span data-ttu-id="f2550-108">Además, el tráfico que se llega a una máquina virtual se puede restringir aún más, para lo que se debe asociar un NSG directamente a dicha máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f2550-108">In addition, traffic to an individual VM can be restricted further by associating an NSG directly to that VM.</span></span> <span data-ttu-id="f2550-109">Para más información, consulte [¿Qué es un grupo de seguridad de red?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="f2550-109">To learn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="f2550-110">Si no tiene habilitados los NSG, Security Center presenta dos recomendaciones: habilitar grupos de seguridad de red en subredes y habilitar grupos de seguridad de red en máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f2550-110">If you do not have NSGs enabled, Security Center presents two recommendations to you: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="f2550-111">Elija el nivel, subred o máquina virtual donde aplicar el NSG.</span><span class="sxs-lookup"><span data-stu-id="f2550-111">You choose which level, subnet or VM, to apply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="f2550-112">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f2550-112">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="f2550-113">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="f2550-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="f2550-114">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="f2550-114">Implement the recommendation</span></span>
1. <span data-ttu-id="f2550-115">En la hoja **Recomendaciones**, seleccione **Habilitar los grupos de seguridad de red** en subredes o en máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f2550-115">In the **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="f2550-116">![Habilitar los grupos de seguridad de red][1]</span><span class="sxs-lookup"><span data-stu-id="f2550-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="f2550-117">Se abrirá la hoja **Configurar los grupos de seguridad de red que faltan** para las subredes o para las máquinas virtuales, según la recomendación que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="f2550-117">This opens the blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on the recommendation that you selected.</span></span> <span data-ttu-id="f2550-118">Seleccione una subred o una máquina virtual en la que configurar un NSG.</span><span class="sxs-lookup"><span data-stu-id="f2550-118">Select a subnet or a virtual machine to configure an NSG on.</span></span>

   ![Configurar NSG para subred][2]

   ![Configurar NSG para máquina virtual][3]
3. <span data-ttu-id="f2550-121">En la hoja **Elegir grupo de seguridad de red** seleccione un NSG existente o seleccione la opción **Crear nuevo** para crear un NSG.</span><span class="sxs-lookup"><span data-stu-id="f2550-121">On the **Choose network security group** blade, select an existing NSG or select **Create new** to create an NSG.</span></span>

   ![Elegir grupo de seguridad de red][4]

<span data-ttu-id="f2550-123">Si crea un nuevo NSG, siga los pasos de [Cómo administrar grupos de seguridad de red con Azure Portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) para crear un NSG y establecer las reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f2550-123">If you create an NSG, follow the steps in [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) to create an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="f2550-124">Consulte también</span><span class="sxs-lookup"><span data-stu-id="f2550-124">See also</span></span>
<span data-ttu-id="f2550-125">En este artículo se ha mostrado cómo implementar la recomendación de Security Center "Habilitar los grupos de seguridad de red" para las subredes o las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f2550-125">This article showed you how to implement the Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="f2550-126">Para más información sobre la habilitación de NSG, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="f2550-126">To learn more about enabling NSGs, see the following:</span></span>

* [<span data-ttu-id="f2550-127">¿Qué es un grupo de seguridad de red?</span><span class="sxs-lookup"><span data-stu-id="f2550-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="f2550-128">Cómo administrar grupos de seguridad de red con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f2550-128">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="f2550-129">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="f2550-129">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="f2550-130">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2550-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f2550-131">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2550-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f2550-132">[Supervisión del estado de seguridad en Azure Security Center](security-center-monitoring.md): obtenga información sobre cómo supervisar el mantenimiento de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="f2550-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="f2550-133">[Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="f2550-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="f2550-134">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="f2550-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="f2550-135">[Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md): busque las preguntas más frecuentes sobre cómo usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="f2550-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="f2550-136">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtenga las últimas noticias e información sobre la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="f2550-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
