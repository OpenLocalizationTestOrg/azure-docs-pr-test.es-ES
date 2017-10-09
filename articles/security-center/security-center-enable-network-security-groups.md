---
title: aaaEnable grupos de seguridad de red en el centro de seguridad de Azure | Documentos de Microsoft
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** Habilitar red seguridad grupos **."
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
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="8784c-103">Habilitación de los grupos de seguridad de red en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8784c-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="8784c-104">Azure Security Center recomienda habilitar un grupo de seguridad de red (NSG) si no hay ninguno habilitado.</span><span class="sxs-lookup"><span data-stu-id="8784c-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="8784c-105">Los NSG contienen una lista de reglas de lista de Control de acceso (ACL) que permiten o deniegan el tráfico de red tooyour instancias de máquina virtual en una red Virtual.</span><span class="sxs-lookup"><span data-stu-id="8784c-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="8784c-106">Los NSG se pueden asociar con las subredes o las instancias individuales de máquina virtual dentro de esa subred.</span><span class="sxs-lookup"><span data-stu-id="8784c-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="8784c-107">Cuando un NSG está asociado a una subred, las reglas de ACL de hello aplican tooall instancias de máquina virtual de hello en esa subred.</span><span class="sxs-lookup"><span data-stu-id="8784c-107">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="8784c-108">Además, el tráfico tooan máquina virtual individual se puede restringir aún más mediante asociar un NSG directamente toothat máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8784c-108">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span> <span data-ttu-id="8784c-109">toolearn más vea [¿qué es un grupo de seguridad de red (NSG)?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="8784c-109">toolearn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="8784c-110">Si no tiene habilitado el NSG, centro de seguridad presenta dos tooyou recomendaciones: habilitar grupos de seguridad de red en subredes y habilitar a los grupos de seguridad de red en máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8784c-110">If you do not have NSGs enabled, Security Center presents two recommendations tooyou: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="8784c-111">Elija qué nivel, la subred o la máquina virtual, tooapply NSG.</span><span class="sxs-lookup"><span data-stu-id="8784c-111">You choose which level, subnet or VM, tooapply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="8784c-112">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8784c-112">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="8784c-113">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="8784c-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="8784c-114">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="8784c-114">Implement hello recommendation</span></span>
1. <span data-ttu-id="8784c-115">Hola **recomendaciones** hoja, seleccione **habilitar grupos de seguridad de red** en subredes o en máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8784c-115">In hello **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="8784c-116">![Habilitar los grupos de seguridad de red][1]</span><span class="sxs-lookup"><span data-stu-id="8784c-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="8784c-117">Esto abre una hoja de hello **configurar grupos de seguridad de red falta** para subredes o para las máquinas virtuales, según la recomendación de Hola que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="8784c-117">This opens hello blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on hello recommendation that you selected.</span></span> <span data-ttu-id="8784c-118">En, seleccione una subred o un tooconfigure un NSG de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8784c-118">Select a subnet or a virtual machine tooconfigure an NSG on.</span></span>

   ![Configurar NSG para subred][2]

   ![Configurar NSG para máquina virtual][3]
3. <span data-ttu-id="8784c-121">En hello **elegir grupo de seguridad de red** hoja, seleccione un NSG existente o **crear nuevo** toocreate un NSG.</span><span class="sxs-lookup"><span data-stu-id="8784c-121">On hello **Choose network security group** blade, select an existing NSG or select **Create new** toocreate an NSG.</span></span>

   ![Elegir grupo de seguridad de red][4]

<span data-ttu-id="8784c-123">Si crea un NSG, siga los pasos de hello en [cómo NSG toomanage mediante Hola portal de Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate un NSG y establecer las reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8784c-123">If you create an NSG, follow hello steps in [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="8784c-124">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="8784c-124">See also</span></span>
<span data-ttu-id="8784c-125">En este artículo se ha explicado cómo tooimplement Hola centro de seguridad recomendación "habilitar grupos de seguridad red" para subredes o máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="8784c-125">This article showed you how tooimplement hello Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="8784c-126">toolearn más acerca de cómo habilitar los NSG, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8784c-126">toolearn more about enabling NSGs, see hello following:</span></span>

* [<span data-ttu-id="8784c-127">¿Qué es un grupo de seguridad de red?</span><span class="sxs-lookup"><span data-stu-id="8784c-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="8784c-128">Cómo NSG toomanage mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8784c-128">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="8784c-129">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="8784c-129">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="8784c-130">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md) : Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="8784c-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="8784c-131">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) : recomendaciones que le ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8784c-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="8784c-132">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="8784c-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="8784c-133">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md) : Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="8784c-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="8784c-134">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="8784c-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="8784c-135">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md) --buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="8784c-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="8784c-136">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/) : obtener información y noticias de seguridad de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="8784c-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
