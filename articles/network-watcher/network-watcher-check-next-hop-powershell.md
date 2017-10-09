---
title: "aaaFind próximo salto con Monitor Azure red próximo salto - PowerShell | Documentos de Microsoft"
description: "En este artículo se describe cómo puede encontrar qué Hola siguiente tipo de salto es y uso de dirección ip del próximo salto de uso de PowerShell."
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
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="87069-103">Averiguar qué tipo de hello próximo salto es con capacidad de próximo salto de hello en Monitor de red de Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="87069-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="87069-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="87069-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="87069-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="87069-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="87069-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="87069-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="87069-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="87069-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="87069-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="87069-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="87069-109">Próximo salto es una característica del Monitor de red que proporciona la capacidad de hello obtener tipo hello de próximo salto y la dirección IP basándose en una máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="87069-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="87069-110">Esta característica es útil para determinar si el tráfico que sale de una máquina virtual recorre una puerta de enlace, internet o redes virtuales tooget tooits destino.</span><span class="sxs-lookup"><span data-stu-id="87069-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="87069-111">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="87069-111">Before you begin</span></span>

<span data-ttu-id="87069-112">En este escenario, utilizará Hola tipo toofind portal Azure Hola de próximo salto y la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="87069-112">In this scenario, you will use hello Azure portal toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="87069-113">Este escenario se supone que ya ha seguido los pasos de hello en [crear un monitor de red](network-watcher-create.md) toocreate un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="87069-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="87069-114">escenario de Hello también supone que un grupo de recursos con una máquina virtual válida existe toobe usa.</span><span class="sxs-lookup"><span data-stu-id="87069-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="87069-115">Escenario</span><span class="sxs-lookup"><span data-stu-id="87069-115">Scenario</span></span>

<span data-ttu-id="87069-116">escenario de Hello descrito en este artículo usa próximo salto, una característica de Monitor de red que se determina el tipo de próximo salto hello y dirección IP para un recurso.</span><span class="sxs-lookup"><span data-stu-id="87069-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="87069-117">toolearn más información acerca de próximo salto, visite [información general sobre salto siguiente](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="87069-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="87069-118">Recuperación de Network Watcher</span><span class="sxs-lookup"><span data-stu-id="87069-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="87069-119">Hola primer paso es instancia de Monitor de red de tooretrieve Hola.</span><span class="sxs-lookup"><span data-stu-id="87069-119">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="87069-120">Hola `$networkWatcher` pasa una variable toohello próximo salto comprobar cmdlet.</span><span class="sxs-lookup"><span data-stu-id="87069-120">hello `$networkWatcher` variable is passed toohello next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="87069-121">Obtención de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="87069-121">Get a virtual machine</span></span>

<span data-ttu-id="87069-122">Próximo salto devuelve próximo salto de Hola y la dirección IP de hello del próximo salto de Hola desde una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="87069-122">Next hop returns hello next hop and hello IP address of hello next hop from a virtual machine.</span></span> <span data-ttu-id="87069-123">Un identificador de una máquina virtual se requiere para hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="87069-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="87069-124">Si ya conoce el identificador de Hola de hello toouse de máquina virtual, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="87069-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="87069-125">Salto siguiente requiere que el recurso de máquina virtual de Hola se asigna toorun.</span><span class="sxs-lookup"><span data-stu-id="87069-125">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="get-hello-network-interfaces"></a><span data-ttu-id="87069-126">Obtener interfaces de red de Hola</span><span class="sxs-lookup"><span data-stu-id="87069-126">Get hello network interfaces</span></span>

<span data-ttu-id="87069-127">se necesita la dirección IP de Hola de una NIC en la máquina virtual de Hola, en este ejemplo recuperamos Hola NIC en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="87069-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="87069-128">Si ya sabe Hola IP de direcciones que desea tootest en la máquina virtual de hello, puede omitir este paso.</span><span class="sxs-lookup"><span data-stu-id="87069-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="87069-129">Obtención del próximo salto</span><span class="sxs-lookup"><span data-stu-id="87069-129">Get Next Hop</span></span>

<span data-ttu-id="87069-130">Ahora se denomina hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="87069-130">Now we call hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="87069-131">Se pasa Hola cmdlet Hola Monitor de red, máquina virtual de Id., dirección IP y dirección IP de destino de código fuente.</span><span class="sxs-lookup"><span data-stu-id="87069-131">We pass hello cmdlet hello Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="87069-132">En este ejemplo, la dirección IP de destino de Hola es tooa máquina virtual en otra red virtual.</span><span class="sxs-lookup"><span data-stu-id="87069-132">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="87069-133">Hay una puerta de enlace de red virtual entre las dos redes virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="87069-133">There is a virtual network gateway between hello two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="87069-134">Revisión de los resultados</span><span class="sxs-lookup"><span data-stu-id="87069-134">Review results</span></span>

<span data-ttu-id="87069-135">Cuando haya finalizado, se proporcionan los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="87069-135">When complete, hello results are provided.</span></span> <span data-ttu-id="87069-136">se devuelve la dirección IP del próximo salto Hello, así como de tipo hello del recurso es.</span><span class="sxs-lookup"><span data-stu-id="87069-136">hello next hop IP address is returned as well as hello type of resource it is.</span></span> <span data-ttu-id="87069-137">En este escenario, es la dirección IP pública de Hola de puerta de enlace de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="87069-137">In this scenario, it is hello public IP address of hello virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="87069-138">Hello lista siguiente muestra valores de hello disponibles actualmente NextHopType:</span><span class="sxs-lookup"><span data-stu-id="87069-138">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="87069-139">**Tipo de próximo salto**</span><span class="sxs-lookup"><span data-stu-id="87069-139">**Next Hop Type**</span></span>

* <span data-ttu-id="87069-140">Internet</span><span class="sxs-lookup"><span data-stu-id="87069-140">Internet</span></span>
* <span data-ttu-id="87069-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="87069-141">VirtualAppliance</span></span>
* <span data-ttu-id="87069-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="87069-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="87069-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="87069-143">VnetLocal</span></span>
* <span data-ttu-id="87069-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="87069-144">HyperNetGateway</span></span>
* <span data-ttu-id="87069-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="87069-145">VnetPeering</span></span>
* <span data-ttu-id="87069-146">None</span><span class="sxs-lookup"><span data-stu-id="87069-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="87069-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="87069-147">Next steps</span></span>

<span data-ttu-id="87069-148">Obtenga información acerca de cómo tooreview la configuración del grupo de seguridad de red mediante programación si visita [NSG auditoría con Monitor de red](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="87069-148">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















