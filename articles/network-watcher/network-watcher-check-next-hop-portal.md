---
title: "aaaFind próximo salto con Monitor Azure red próximo salto: portal de Azure | Documentos de Microsoft"
description: "En este artículo se describe cómo puede ver qué Hola siguiente tipo de salto es y dirección ip mediante el uso de salto siguiente Hola portal de Azure"
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
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="3de65-103">Averiguar qué tipo de hello próximo salto es con capacidad de próximo salto de hello en Monitor de red de Azure mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="3de65-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="3de65-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3de65-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="3de65-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3de65-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="3de65-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3de65-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="3de65-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3de65-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="3de65-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="3de65-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="3de65-109">Próximo salto es una característica del Monitor de red que proporciona la capacidad de hello obtener tipo hello de próximo salto y la dirección IP basándose en una máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="3de65-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="3de65-110">Esta característica es útil para determinar si el tráfico que sale de una máquina virtual recorre una puerta de enlace, internet o redes virtuales tooget tooits destino.</span><span class="sxs-lookup"><span data-stu-id="3de65-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3de65-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="3de65-111">Before you begin</span></span>

<span data-ttu-id="3de65-112">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="3de65-112">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="3de65-113">escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.</span><span class="sxs-lookup"><span data-stu-id="3de65-113">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="3de65-114">Escenario</span><span class="sxs-lookup"><span data-stu-id="3de65-114">Scenario</span></span>

<span data-ttu-id="3de65-115">escenario de Hello descrito en este artículo usa toofind de salto siguiente tipo hello de próximo salto y la dirección IP para un recurso.</span><span class="sxs-lookup"><span data-stu-id="3de65-115">hello scenario covered in this article uses Next hop toofind out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="3de65-116">toolearn más información acerca de próximo salto, visite [información general sobre salto siguiente](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3de65-116">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="3de65-117">En este escenario va a:</span><span class="sxs-lookup"><span data-stu-id="3de65-117">In this scenario, you will:</span></span>

* <span data-ttu-id="3de65-118">Recuperar de próximo salto Hola desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3de65-118">Retrieve hello next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="3de65-119">Obtención del próximo salto</span><span class="sxs-lookup"><span data-stu-id="3de65-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="3de65-120">Paso 1</span><span class="sxs-lookup"><span data-stu-id="3de65-120">Step 1</span></span>

<span data-ttu-id="3de65-121">Navegar tooyour recurso de Monitor de red en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3de65-121">Navigate tooyour Network Watcher resource in hello Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="3de65-122">Paso 2</span><span class="sxs-lookup"><span data-stu-id="3de65-122">Step 2</span></span>

<span data-ttu-id="3de65-123">Haga clic en **del próximo salto** en el panel de navegación de hello, máquina virtual de hello select e interfaz de red, rellenar Hola IP de origen y de destino y haga clic en hello **del próximo salto** botón.</span><span class="sxs-lookup"><span data-stu-id="3de65-123">Click **Next hop** in hello navigation pane, select hello virtual machine and network interface, fill out hello source and destination IP, and click hello **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="3de65-124">Salto siguiente requiere que el recurso de máquina virtual de Hola se asigna toorun.</span><span class="sxs-lookup"><span data-stu-id="3de65-124">Next hop requires that hello VM resource is allocated toorun.</span></span>

![información general sobre obtención del próximo salto][1]

### <a name="step-3"></a><span data-ttu-id="3de65-126">Paso 3</span><span class="sxs-lookup"><span data-stu-id="3de65-126">Step 3</span></span>

<span data-ttu-id="3de65-127">Una vez completada la tarea hello, se proporcionan los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="3de65-127">Once hello task is complete, hello results are provided.</span></span> <span data-ttu-id="3de65-128">Hola dirección IP y el tipo de dispositivo Hola de próximo salto es, se muestra.</span><span class="sxs-lookup"><span data-stu-id="3de65-128">hello IP address and type of device hello next hop is, is displayed.</span></span> <span data-ttu-id="3de65-129">Hello tabla siguiente muestran los valores devueltos disponibles hello en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="3de65-129">hello following table shows hello available returned values in hello portal.</span></span>

<span data-ttu-id="3de65-130">**Tipo de próximo salto**</span><span class="sxs-lookup"><span data-stu-id="3de65-130">**Next Hop Type**</span></span>

* <span data-ttu-id="3de65-131">Internet</span><span class="sxs-lookup"><span data-stu-id="3de65-131">Internet</span></span>
* <span data-ttu-id="3de65-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="3de65-132">VirtualAppliance</span></span>
* <span data-ttu-id="3de65-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="3de65-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="3de65-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="3de65-134">VnetLocal</span></span>
* <span data-ttu-id="3de65-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="3de65-135">HyperNetGateway</span></span>
* <span data-ttu-id="3de65-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="3de65-136">VnetPeering</span></span>
* <span data-ttu-id="3de65-137">None</span><span class="sxs-lookup"><span data-stu-id="3de65-137">None</span></span>

<span data-ttu-id="3de65-138">Si una ruta personalizada se ha usado tooroute este tráfico, la ruta definida por el usuario de hello (UDR) se muestra también con los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="3de65-138">If a custom route was used tooroute this traffic, hello User-defined route (UDR) is shown as well with hello results.</span></span>

![resultados de obtención del próximo salto][2]

## <a name="next-steps"></a><span data-ttu-id="3de65-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3de65-140">Next steps</span></span>

<span data-ttu-id="3de65-141">Obtenga información acerca de cómo tooreview la configuración del grupo de seguridad de red mediante programación si visita [NSG auditoría con Monitor de red](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="3de65-141">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














