---
title: "aaaFind próximo salto con Monitor Azure red próximo salto - 1.0 de CLI de Azure | Documentos de Microsoft"
description: "En este artículo se describe cómo puede encontrar qué Hola siguiente tipo de salto es y uso de dirección ip del próximo salto de mediante la CLI de Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="97ea6-103">Averiguar qué tipo de hello próximo salto es con capacidad de próximo salto de hello en Monitor de red de Azure mediante Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="97ea6-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="97ea6-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="97ea6-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="97ea6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97ea6-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="97ea6-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="97ea6-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="97ea6-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="97ea6-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="97ea6-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="97ea6-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="97ea6-109">Próximo salto es una característica del Monitor de red que proporciona la capacidad de hello obtener tipo hello de próximo salto y la dirección IP basándose en una máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="97ea6-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="97ea6-110">Esta característica es útil para determinar si el tráfico que sale de una máquina virtual recorre una puerta de enlace, internet o redes virtuales tooget tooits destino.</span><span class="sxs-lookup"><span data-stu-id="97ea6-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="97ea6-111">En este artículo, se utiliza la multiplataforma Azure CLI 1.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="97ea6-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="97ea6-112">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="97ea6-112">Before you begin</span></span>

<span data-ttu-id="97ea6-113">En este escenario, utilizará Hola tipo de próximo salto de CLI de Azure toofind hello y la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="97ea6-113">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="97ea6-114">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="97ea6-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="97ea6-115">escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.</span><span class="sxs-lookup"><span data-stu-id="97ea6-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="97ea6-116">Escenario</span><span class="sxs-lookup"><span data-stu-id="97ea6-116">Scenario</span></span>

<span data-ttu-id="97ea6-117">escenario de Hello descrito en este artículo usa próximo salto, una característica de Monitor de red que se determina el tipo de próximo salto hello y dirección IP para un recurso.</span><span class="sxs-lookup"><span data-stu-id="97ea6-117">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="97ea6-118">toolearn más información acerca de próximo salto, visite [información general sobre salto siguiente](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97ea6-118">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="97ea6-119">Obtención del próximo salto</span><span class="sxs-lookup"><span data-stu-id="97ea6-119">Get Next Hop</span></span>

<span data-ttu-id="97ea6-120">llamamos a Hola de próximo salto tooget hello `azure netowrk watcher next-hop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="97ea6-120">tooget hello next hop we call hello `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="97ea6-121">Pasamos grupo de recursos de Monitor de red de hello cmdlet hello, hello NetworkWatcher, máquina virtual de Id., dirección IP de origen y dirección IP de destino.</span><span class="sxs-lookup"><span data-stu-id="97ea6-121">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="97ea6-122">En este ejemplo, la dirección IP de destino de Hola es tooa máquina virtual en otra red virtual.</span><span class="sxs-lookup"><span data-stu-id="97ea6-122">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="97ea6-123">Hay una puerta de enlace de red virtual entre las dos redes virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="97ea6-123">There is a virtual network gateway between hello two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="97ea6-124">Si Hola máquina virtual tiene varios NIC y reenvío IP está habilitado en ninguno de hello NIC, a continuación, Hola parámetro NIC (-Id. de nic) debe especificarse.</span><span class="sxs-lookup"><span data-stu-id="97ea6-124">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="97ea6-125">De lo contrario, es opcional.</span><span class="sxs-lookup"><span data-stu-id="97ea6-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="97ea6-126">Revisión de los resultados</span><span class="sxs-lookup"><span data-stu-id="97ea6-126">Review results</span></span>

<span data-ttu-id="97ea6-127">Cuando haya finalizado, se proporcionan los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="97ea6-127">When complete, hello results are provided.</span></span> <span data-ttu-id="97ea6-128">se devuelve la dirección IP del próximo salto Hello, así como de tipo hello del recurso es.</span><span class="sxs-lookup"><span data-stu-id="97ea6-128">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="97ea6-129">Hello lista siguiente muestra valores de hello disponibles actualmente NextHopType:</span><span class="sxs-lookup"><span data-stu-id="97ea6-129">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="97ea6-130">**Tipo de próximo salto**</span><span class="sxs-lookup"><span data-stu-id="97ea6-130">**Next Hop Type**</span></span>

* <span data-ttu-id="97ea6-131">Internet</span><span class="sxs-lookup"><span data-stu-id="97ea6-131">Internet</span></span>
* <span data-ttu-id="97ea6-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="97ea6-132">VirtualAppliance</span></span>
* <span data-ttu-id="97ea6-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="97ea6-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="97ea6-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="97ea6-134">VnetLocal</span></span>
* <span data-ttu-id="97ea6-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="97ea6-135">HyperNetGateway</span></span>
* <span data-ttu-id="97ea6-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="97ea6-136">VnetPeering</span></span>
* <span data-ttu-id="97ea6-137">None</span><span class="sxs-lookup"><span data-stu-id="97ea6-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="97ea6-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97ea6-138">Next steps</span></span>

<span data-ttu-id="97ea6-139">Obtenga información acerca de cómo tooreview la configuración del grupo de seguridad de red mediante programación si visita [NSG auditoría con Monitor de red](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="97ea6-139">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
