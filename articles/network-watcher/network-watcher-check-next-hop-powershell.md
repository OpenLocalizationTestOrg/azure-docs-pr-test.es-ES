---
title: "Búsqueda del próximo salto con Próximo salto de Azure Network Watcher (PowerShell) | Microsoft Docs"
description: "En este artículo se describe cómo encontrar el tipo del próximo salto y la dirección IP mediante la funcionalidad Próximo salto con PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 00161e7c6fb4becdb7d8eab266fa27128e50f8ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="9f711-103">Obtenga más información sobre el tipo del próximo salto con la funcionalidad Próximo salto de Azure Network Watcher mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f711-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9f711-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="9f711-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="9f711-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f711-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="9f711-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9f711-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="9f711-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9f711-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="9f711-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="9f711-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="9f711-109">Próximo salto es una característica de Network Watcher que permite obtener el tipo del próximo salto y la dirección IP para una máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="9f711-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="9f711-110">Esta característica es útil para determinar si el tráfico que sale de una máquina virtual atraviesa una puerta de enlace, Internet o redes virtuales para llegar a su destino.</span><span class="sxs-lookup"><span data-stu-id="9f711-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9f711-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="9f711-111">Before you begin</span></span>

<span data-ttu-id="9f711-112">En este escenario, se usa Azure Portal para averiguar el tipo de próximo salto y la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="9f711-112">In this scenario, you will use the Azure portal to find the next hop type and IP address.</span></span>

<span data-ttu-id="9f711-113">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Create an Azure Network Watcher instance](network-watcher-create.md) (Creación de una instancia de Azure Network Watcher) para crear una instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="9f711-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="9f711-114">En este escenario también se da por hecho que existe un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="9f711-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="9f711-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="9f711-115">Scenario</span></span>

<span data-ttu-id="9f711-116">El escenario descrito en este artículo usa Next Hop, una característica de Network Watcher, para averiguar el tipo de próximo salto y la dirección IP de un recurso.</span><span class="sxs-lookup"><span data-stu-id="9f711-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="9f711-117">Para más información sobre Próximo salto, vea [introducción a Próximo salto](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9f711-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="9f711-118">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="9f711-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="9f711-119">El primer paso consiste en recuperar la instancia de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="9f711-119">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="9f711-120">La variable `$networkWatcher` pasa al cmdlet de verificación del próximo salto.</span><span class="sxs-lookup"><span data-stu-id="9f711-120">The `$networkWatcher` variable is passed to the next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="9f711-121">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="9f711-121">Get a virtual machine</span></span>

<span data-ttu-id="9f711-122">Próximo salto devuelve el próximo salto y la dirección IP del próximo salto de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f711-122">Next hop returns the next hop and the IP address of the next hop from a virtual machine.</span></span> <span data-ttu-id="9f711-123">Se necesita el identificador de una máquina virtual para ejecutar el cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9f711-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="9f711-124">Si ya conoce el identificador de la máquina virtual que se va a usar, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="9f711-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="9f711-125">Un requisito del próximo salto es que el recurso de máquina virtual esté asignado para ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="9f711-125">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="get-the-network-interfaces"></a><span data-ttu-id="9f711-126">Obtención de las interfaces de red</span><span class="sxs-lookup"><span data-stu-id="9f711-126">Get the network interfaces</span></span>

<span data-ttu-id="9f711-127">Se necesita la dirección IP de una NIC en la máquina virtual; en este ejemplo, se recuperan las NIC de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f711-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="9f711-128">Si ya conoce la dirección IP que desea probar en la máquina virtual, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="9f711-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="9f711-129">Obtención del próximo salto</span><span class="sxs-lookup"><span data-stu-id="9f711-129">Get Next Hop</span></span>

<span data-ttu-id="9f711-130">Ahora se llama al cmdlet `Get-AzureRmNetworkWatcherNextHop`.</span><span class="sxs-lookup"><span data-stu-id="9f711-130">Now we call the `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="9f711-131">Se pasa al cmdlet la instancia de Network Watcher, el identificador de la máquina virtual, la dirección IP de origen y la dirección IP de destino.</span><span class="sxs-lookup"><span data-stu-id="9f711-131">We pass the cmdlet the Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="9f711-132">En este ejemplo, la dirección IP de destino es una máquina virtual en otra red virtual.</span><span class="sxs-lookup"><span data-stu-id="9f711-132">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="9f711-133">Hay una puerta de enlace de red virtual entre las dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="9f711-133">There is a virtual network gateway between the two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="9f711-134">Revisión de los resultados</span><span class="sxs-lookup"><span data-stu-id="9f711-134">Review results</span></span>

<span data-ttu-id="9f711-135">Una vez finalizado, se proporcionan los resultados.</span><span class="sxs-lookup"><span data-stu-id="9f711-135">When complete, the results are provided.</span></span> <span data-ttu-id="9f711-136">Se devuelve la dirección IP del próximo salto y el tipo de recurso que es.</span><span class="sxs-lookup"><span data-stu-id="9f711-136">The next hop IP address is returned as well as the type of resource it is.</span></span> <span data-ttu-id="9f711-137">En este escenario, es la dirección IP pública de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="9f711-137">In this scenario, it is the public IP address of the virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="9f711-138">En la lista siguiente se muestran los valores de NextHopType disponibles actualmente:</span><span class="sxs-lookup"><span data-stu-id="9f711-138">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="9f711-139">**Tipo de próximo salto**</span><span class="sxs-lookup"><span data-stu-id="9f711-139">**Next Hop Type**</span></span>

* <span data-ttu-id="9f711-140">Internet</span><span class="sxs-lookup"><span data-stu-id="9f711-140">Internet</span></span>
* <span data-ttu-id="9f711-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="9f711-141">VirtualAppliance</span></span>
* <span data-ttu-id="9f711-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="9f711-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="9f711-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="9f711-143">VnetLocal</span></span>
* <span data-ttu-id="9f711-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="9f711-144">HyperNetGateway</span></span>
* <span data-ttu-id="9f711-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="9f711-145">VnetPeering</span></span>
* <span data-ttu-id="9f711-146">None</span><span class="sxs-lookup"><span data-stu-id="9f711-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f711-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f711-147">Next steps</span></span>

<span data-ttu-id="9f711-148">Aprenda cómo revisar la configuración del grupo de seguridad de red mediante programación en [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Auditoría de NSG con Network Watcher).</span><span class="sxs-lookup"><span data-stu-id="9f711-148">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















