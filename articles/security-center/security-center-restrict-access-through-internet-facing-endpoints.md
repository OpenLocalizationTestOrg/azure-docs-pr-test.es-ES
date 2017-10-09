---
title: "aaaRestrict acceso a través de extremos de conexión a Internet en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este documento muestra cómo tooimplement Hola recomendación de Azure Security Center ** restringir el acceso a través de Internet orientada hacia el extremo **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="c1c72-103">Restricción del acceso a través de puntos de conexión accesibles desde Internet en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="c1c72-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="c1c72-104">Azure Security Center recomendará restringir el acceso a través de puntos de conexión accesibles desde Internet si alguno de los grupos de seguridad de red (NSG) tiene una o varias reglas de entrada que permitan el acceso desde cualquier dirección IP de origen.</span><span class="sxs-lookup"><span data-stu-id="c1c72-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="c1c72-105">Abrir acceso demasiado "any" puede habilitar los atacantes tooaccess sus recursos.</span><span class="sxs-lookup"><span data-stu-id="c1c72-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="c1c72-106">Centro de seguridad se recomienda editar estas direcciones IP de las reglas de entrada toorestrict acceso toosource que realmente necesitan tener acceso.</span><span class="sxs-lookup"><span data-stu-id="c1c72-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="c1c72-107">Esta recomendación se genera para cualquier puerto no web que tenga la opción Cualquiera como origen.</span><span class="sxs-lookup"><span data-stu-id="c1c72-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="c1c72-108">Este documento presentan servicio hello mediante el uso de una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c1c72-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="c1c72-109">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="c1c72-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="c1c72-110">Implementar la recomendación de Hola</span><span class="sxs-lookup"><span data-stu-id="c1c72-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="c1c72-111">Hola **hoja de recomendaciones**, seleccione **restringir el acceso a través de Internet orientada hacia el extremo**.</span><span class="sxs-lookup"><span data-stu-id="c1c72-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Restricción del acceso a través de puntos de conexión accesibles desde Internet][1]
2. <span data-ttu-id="c1c72-113">Esto abre una hoja de hello **restringir el acceso a través de Internet orientada hacia el extremo**.</span><span class="sxs-lookup"><span data-stu-id="c1c72-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="c1c72-114">Esta hoja enumera hello las máquinas virtuales (VM) con las reglas de entrada que crean un posible riesgo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="c1c72-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="c1c72-115">Seleccione una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c1c72-115">Select a VM.</span></span>

   ![Seleccionar una máquina virtual][2]
3. <span data-ttu-id="c1c72-117">Hola **NSG** hoja muestra la información de grupo de seguridad de red, las reglas de entrada relacionadas, y Hola asociados máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c1c72-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="c1c72-118">Seleccione **editar reglas de entrada** tooproceed con la edición de una regla de entrada.</span><span class="sxs-lookup"><span data-stu-id="c1c72-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![Hoja Grupo de seguridad de red][3]
4. <span data-ttu-id="c1c72-120">En hello **reglas de seguridad de entrada** seleccione hoja Hola tooedit de regla de entrada.</span><span class="sxs-lookup"><span data-stu-id="c1c72-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="c1c72-121">En este ejemplo, vamos a seleccionar **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="c1c72-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Reglas de seguridad de entrada][4]

   <span data-ttu-id="c1c72-123">Tenga en cuenta que también puede seleccionar **reglas predeterminadas** toosee Hola formado por las reglas predeterminadas que contiene todos los NSG.</span><span class="sxs-lookup"><span data-stu-id="c1c72-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="c1c72-124">no se puede eliminar las reglas predeterminadas de Hello pero, dado que se asignan una prioridad más baja, puede reemplazarse por reglas de Hola que cree.</span><span class="sxs-lookup"><span data-stu-id="c1c72-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="c1c72-125">Obtenga más información sobre [reglas predeterminadas](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="c1c72-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Reglas predeterminadas][5]
5. <span data-ttu-id="c1c72-127">En hello **AllowWeb** hoja, modificar las propiedades de regla de entrada de Hola para que Hola Hola **origen** es una dirección IP o un bloque de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="c1c72-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="c1c72-128">toolearn más información sobre propiedades de Hola de regla de entrada de hello, consulte [reglas del NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="c1c72-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Editar regla de entrada][6]

## <a name="see-also"></a><span data-ttu-id="c1c72-130">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="c1c72-130">See also</span></span>
<span data-ttu-id="c1c72-131">En este artículo se ha mostrado cómo tooimplement Hola centro de seguridad recomendación "restringir el acceso a través de Internet orientada hacia el punto de conexión."</span><span class="sxs-lookup"><span data-stu-id="c1c72-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="c1c72-132">toolearn más acerca de cómo habilitar los NSG y reglas, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c1c72-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="c1c72-133">¿Qué es un grupo de seguridad de red?</span><span class="sxs-lookup"><span data-stu-id="c1c72-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="c1c72-134">Cómo NSG toomanage mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c1c72-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="c1c72-135">toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c1c72-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="c1c72-136">[Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md): Obtenga información acerca de cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1c72-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c1c72-137">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que lo ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1c72-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c1c72-138">[Supervisión de estado de seguridad de Azure Security Center](security-center-monitoring.md): Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1c72-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="c1c72-139">[Toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure](security-center-managing-and-responding-alerts.md): Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.</span><span class="sxs-lookup"><span data-stu-id="c1c72-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="c1c72-140">[Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="c1c72-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="c1c72-141">[Preguntas más frecuentes de Azure Security Center](security-center-faq.md)--buscar preguntas más frecuentes sobre el uso de servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1c72-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c1c72-142">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtener información y noticias de seguridad de Azure más recientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="c1c72-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
