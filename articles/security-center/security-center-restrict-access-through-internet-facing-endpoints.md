---
title: "Restricción del acceso a través de puntos de conexión accesibles desde Internet en Azure Security Center | Microsoft Docs"
description: "En este documento se muestra cómo implementar la recomendación de Azure Security Center de restringir el acceso a través de puntos de conexión accesibles desde Internet."
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
ms.openlocfilehash: f7309c617f1705205e2c9f1b1b48d141391d45da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="734d7-103">Restricción del acceso a través de puntos de conexión accesibles desde Internet en Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="734d7-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="734d7-104">Azure Security Center recomendará restringir el acceso a través de puntos de conexión accesibles desde Internet si alguno de los grupos de seguridad de red (NSG) tiene una o varias reglas de entrada que permitan el acceso desde cualquier dirección IP de origen.</span><span class="sxs-lookup"><span data-stu-id="734d7-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="734d7-105">Al abrir el acceso a cualquier IP, los atacantes pueden lograr acceder a los recursos.</span><span class="sxs-lookup"><span data-stu-id="734d7-105">Opening access to “any” may enable attackers to access your resources.</span></span> <span data-ttu-id="734d7-106">Azure Security Center recomienda editar estas reglas de entrada para restringir el acceso a las direcciones IP de origen que realmente necesiten acceder.</span><span class="sxs-lookup"><span data-stu-id="734d7-106">Security Center will recommend that you edit these inbound rules to restrict access to source IP addresses that actually need access.</span></span>

<span data-ttu-id="734d7-107">Esta recomendación se genera para cualquier puerto no web que tenga la opción Cualquiera como origen.</span><span class="sxs-lookup"><span data-stu-id="734d7-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="734d7-108">En este documento se presenta el servicio mediante una implementación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="734d7-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="734d7-109">No se trata de una guía paso a paso.</span><span class="sxs-lookup"><span data-stu-id="734d7-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="734d7-110">Implementación de la recomendación</span><span class="sxs-lookup"><span data-stu-id="734d7-110">Implement the recommendation</span></span>
1. <span data-ttu-id="734d7-111">En la hoja **Recomendaciones**, seleccione **Restringir el acceso a través de un punto de conexión accesible desde Internet**.</span><span class="sxs-lookup"><span data-stu-id="734d7-111">In the **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Restricción del acceso a través de puntos de conexión accesibles desde Internet][1]
2. <span data-ttu-id="734d7-113">Se abrirá la hoja **Restrict access through Internet facing endpoint**(Restringir el acceso a través de puntos de conexión accesibles desde Internet).</span><span class="sxs-lookup"><span data-stu-id="734d7-113">This opens the blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="734d7-114">Esta hoja enumera las máquinas virtuales (VM) con reglas de entrada que generan un posible problema de seguridad.</span><span class="sxs-lookup"><span data-stu-id="734d7-114">This blade lists the virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="734d7-115">Seleccione una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="734d7-115">Select a VM.</span></span>

   ![Seleccionar una máquina virtual][2]
3. <span data-ttu-id="734d7-117">La hoja **NSG** muestra la información de los grupos de seguridad de red, las reglas de entrada relacionadas y la máquina virtual asociada.</span><span class="sxs-lookup"><span data-stu-id="734d7-117">The **NSG** blade displays Network Security Group information, related inbound rules, and the associated VM.</span></span> <span data-ttu-id="734d7-118">Seleccione **Editar reglas de entrada** para continuar con la edición de una regla de entrada.</span><span class="sxs-lookup"><span data-stu-id="734d7-118">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span>

   ![Hoja Grupo de seguridad de red][3]
4. <span data-ttu-id="734d7-120">En la hoja **Reglas de seguridad de entrada** , seleccione la regla de entrada que va a editar.</span><span class="sxs-lookup"><span data-stu-id="734d7-120">On the **Inbound security rules** blade select the inbound rule to edit.</span></span> <span data-ttu-id="734d7-121">En este ejemplo, vamos a seleccionar **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="734d7-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Reglas de seguridad de entrada][4]

   <span data-ttu-id="734d7-123">Tenga en cuenta que también puede seleccionar **Reglas predeterminadas** para ver el conjunto de reglas predeterminadas que contiene todos los NSG.</span><span class="sxs-lookup"><span data-stu-id="734d7-123">Note, you can also select **Default rules** to see the set of default rules contained by all NSGs.</span></span> <span data-ttu-id="734d7-124">No se pueden eliminar las reglas predeterminadas, pero como que tienen asignada la prioridad mínima, pueden reemplazarse por las reglas que cree.</span><span class="sxs-lookup"><span data-stu-id="734d7-124">The default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by the rules that you create.</span></span> <span data-ttu-id="734d7-125">Obtenga más información sobre [reglas predeterminadas](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="734d7-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Reglas predeterminadas][5]
5. <span data-ttu-id="734d7-127">En la hoja **AllowWeb**, edite las propiedades de la regla de entrada para que el **origen** sea una dirección IP o un bloque de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="734d7-127">On the **AllowWeb** blade, edit the properties of the inbound rule so that the **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="734d7-128">Para obtener más información sobre las propiedades de la regla de entrada, consulte [Reglas de grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="734d7-128">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Editar regla de entrada][6]

## <a name="see-also"></a><span data-ttu-id="734d7-130">Consulte también</span><span class="sxs-lookup"><span data-stu-id="734d7-130">See also</span></span>
<span data-ttu-id="734d7-131">En este artículo se muestra cómo implementar la recomendación de Azure Security Center de restringir el acceso a través de puntos de conexión accesibles desde Internet.</span><span class="sxs-lookup"><span data-stu-id="734d7-131">This article showed you how to implement the Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="734d7-132">Para obtener más información sobre cómo habilitar NSG y reglas, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="734d7-132">To learn more about enabling NSGs and rules, see the following:</span></span>

* [<span data-ttu-id="734d7-133">¿Qué es un grupo de seguridad de red?</span><span class="sxs-lookup"><span data-stu-id="734d7-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="734d7-134">Cómo administrar grupos de seguridad de red con el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="734d7-134">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="734d7-135">Para más información sobre el Centro de seguridad, consulte los siguientes recursos:</span><span class="sxs-lookup"><span data-stu-id="734d7-135">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="734d7-136">[Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): aprenda a configurar directivas de seguridad para las suscripciones y los grupos de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="734d7-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="734d7-137">[Administración de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md): recomendaciones que lo ayudan a proteger los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="734d7-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="734d7-138">[Supervisión del estado de seguridad en Centro de seguridad de Azure](security-center-monitoring.md): obtenga información sobre cómo supervisar el estado de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="734d7-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="734d7-139">[Administración y respuesta a las alertas de seguridad en el Centro de seguridad de Azure](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="734d7-139">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="734d7-140">[Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md) : aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.</span><span class="sxs-lookup"><span data-stu-id="734d7-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="734d7-141">[Preguntas más frecuentes acerca del Centro de seguridad de Azure](security-center-faq.md): busque las preguntas más frecuentes sobre cómo usar el servicio.</span><span class="sxs-lookup"><span data-stu-id="734d7-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="734d7-142">[Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): obtenga las últimas noticias e información sobre la seguridad en Azure.</span><span class="sxs-lookup"><span data-stu-id="734d7-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
