---
title: "Búsqueda del próximo salto con Próximo salto de Azure Network Watcher (Azure Portal) | Microsoft Docs"
description: "En este artículo se describe cómo encontrar el tipo del próximo salto y la dirección IP mediante la funcionalidad Próximo salto en Azure Portal."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5434b7972346821985c459fc4620805adb88676b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a><span data-ttu-id="0007f-103">Obtenga más información sobre el tipo del próximo salto con la funcionalidad Próximo salto de Azure Network Watcher mediante el portal.</span><span class="sxs-lookup"><span data-stu-id="0007f-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="0007f-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0007f-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="0007f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0007f-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="0007f-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0007f-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="0007f-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0007f-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="0007f-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="0007f-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="0007f-109">Próximo salto es una característica de Network Watcher que permite obtener el tipo del próximo salto y la dirección IP para una máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="0007f-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="0007f-110">Esta característica es útil para determinar si el tráfico que sale de una máquina virtual atraviesa una puerta de enlace, Internet o redes virtuales para llegar a su destino.</span><span class="sxs-lookup"><span data-stu-id="0007f-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0007f-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="0007f-111">Before you begin</span></span>

<span data-ttu-id="0007f-112">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="0007f-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="0007f-113">En este escenario también se da por hecho que existe un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="0007f-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="0007f-114">Escenario</span><span class="sxs-lookup"><span data-stu-id="0007f-114">Scenario</span></span>

<span data-ttu-id="0007f-115">El escenario descrito en este artículo usa Próximo salto para averiguar el tipo de próximo salto y la dirección IP de un recurso.</span><span class="sxs-lookup"><span data-stu-id="0007f-115">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="0007f-116">Para más información sobre Próximo salto, vea [introducción a Próximo salto](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0007f-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="0007f-117">En este escenario:</span><span class="sxs-lookup"><span data-stu-id="0007f-117">In this scenario, you will:</span></span>

* <span data-ttu-id="0007f-118">Recuperará el próximo salto de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0007f-118">Retrieve the next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="0007f-119">Obtención del próximo salto</span><span class="sxs-lookup"><span data-stu-id="0007f-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="0007f-120">Paso 1</span><span class="sxs-lookup"><span data-stu-id="0007f-120">Step 1</span></span>

<span data-ttu-id="0007f-121">Vaya al recurso de Network Watcher en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="0007f-121">Navigate to your Network Watcher resource in the Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="0007f-122">Paso 2</span><span class="sxs-lookup"><span data-stu-id="0007f-122">Step 2</span></span>

<span data-ttu-id="0007f-123">Haga clic en **Próximo salto** en el panel de navegación, seleccione la máquina virtual y la interfaz de red, rellene la IP de origen y de destino y haga clic en el botón **Próximo salto**.</span><span class="sxs-lookup"><span data-stu-id="0007f-123">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="0007f-124">Un requisito del próximo salto es que el recurso de máquina virtual esté asignado para ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="0007f-124">Next hop requires that the VM resource is allocated to run.</span></span>

![información general sobre obtención del próximo salto][1]

### <a name="step-3"></a><span data-ttu-id="0007f-126">Paso 3</span><span class="sxs-lookup"><span data-stu-id="0007f-126">Step 3</span></span>

<span data-ttu-id="0007f-127">Después de completar la tarea, se muestran los resultados.</span><span class="sxs-lookup"><span data-stu-id="0007f-127">Once the task is complete, the results are provided.</span></span> <span data-ttu-id="0007f-128">Se muestran la dirección IP y el tipo de dispositivo del próximo salto.</span><span class="sxs-lookup"><span data-stu-id="0007f-128">The IP address and type of device the next hop is, is displayed.</span></span> <span data-ttu-id="0007f-129">En la siguiente tabla se muestran los valores devueltos disponibles en el portal.</span><span class="sxs-lookup"><span data-stu-id="0007f-129">The following table shows the available returned values in the portal.</span></span>

<span data-ttu-id="0007f-130">**Tipo de próximo salto**</span><span class="sxs-lookup"><span data-stu-id="0007f-130">**Next Hop Type**</span></span>

* <span data-ttu-id="0007f-131">Internet</span><span class="sxs-lookup"><span data-stu-id="0007f-131">Internet</span></span>
* <span data-ttu-id="0007f-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="0007f-132">VirtualAppliance</span></span>
* <span data-ttu-id="0007f-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="0007f-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="0007f-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="0007f-134">VnetLocal</span></span>
* <span data-ttu-id="0007f-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="0007f-135">HyperNetGateway</span></span>
* <span data-ttu-id="0007f-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="0007f-136">VnetPeering</span></span>
* <span data-ttu-id="0007f-137">None</span><span class="sxs-lookup"><span data-stu-id="0007f-137">None</span></span>

<span data-ttu-id="0007f-138">Si se utilizó una ruta personalizada para enrutar este tráfico, se muestra también la ruta definida por el usuario (UDR) con los resultados.</span><span class="sxs-lookup"><span data-stu-id="0007f-138">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span></span>

![resultados de obtención del próximo salto][2]

## <a name="next-steps"></a><span data-ttu-id="0007f-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0007f-140">Next steps</span></span>

<span data-ttu-id="0007f-141">Aprenda cómo revisar la configuración del grupo de seguridad de red mediante programación en [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Auditoría de NSG con Network Watcher).</span><span class="sxs-lookup"><span data-stu-id="0007f-141">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














