---
title: "Búsqueda del próximo salto con Next Hop de Azure Network Watcher: CLI de Azure 2.0 | Microsoft Docs"
description: "En este artículo se describe cómo encontrar el tipo del próximo salto y la dirección IP mediante la funcionalidad Next Hop con la CLI de Azure."
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
ms.openlocfilehash: d1ee6870ba0188ff2c473e4cca12a5bdc1f97d3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="71929-103">Obtenga más información sobre el tipo del próximo salto con la funcionalidad Next Hop de Azure Network Watcher mediante la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="71929-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="71929-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="71929-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="71929-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="71929-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="71929-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="71929-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="71929-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="71929-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="71929-108">API de REST de Azure</span><span class="sxs-lookup"><span data-stu-id="71929-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="71929-109">Próximo salto es una característica de Network Watcher que permite obtener el tipo del próximo salto y la dirección IP para una máquina virtual especificada.</span><span class="sxs-lookup"><span data-stu-id="71929-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="71929-110">Esta característica es útil para determinar si el tráfico que sale de una máquina virtual atraviesa una puerta de enlace, Internet o redes virtuales para llegar a su destino.</span><span class="sxs-lookup"><span data-stu-id="71929-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="71929-111">En este artículo se usa la CLI de próxima generación para el modelo de implementación de Resource Manager, la CLI de Azure 2.0, que está disponible para Windows, Mac y Linux.</span><span class="sxs-lookup"><span data-stu-id="71929-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="71929-112">Para seguir los pasos de este artículo, es preciso [instalar la interfaz de la línea de comandos de Azure para Mac, Linux y Windows (CLI de Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="71929-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="71929-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="71929-113">Before you begin</span></span>

<span data-ttu-id="71929-114">En este escenario, se usa la CLI de Azure para averiguar el tipo de próximo salto y la dirección IP.</span><span class="sxs-lookup"><span data-stu-id="71929-114">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="71929-115">En este escenario, se da por hecho que ya ha seguido los pasos descritos en [Creación de una instancia de Network Watcher](network-watcher-create.md) para crear un monitor de red.</span><span class="sxs-lookup"><span data-stu-id="71929-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="71929-116">En este escenario también se da por hecho que existe un grupo de recursos con una máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="71929-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="71929-117">Escenario</span><span class="sxs-lookup"><span data-stu-id="71929-117">Scenario</span></span>

<span data-ttu-id="71929-118">El escenario descrito en este artículo usa Next Hop, una característica de Network Watcher, para averiguar el tipo de próximo salto y la dirección IP de un recurso.</span><span class="sxs-lookup"><span data-stu-id="71929-118">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="71929-119">Para más información acerca de Next Hop, consulte la [introducción a Next Hop](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71929-119">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="71929-120">Obtención del próximo salto</span><span class="sxs-lookup"><span data-stu-id="71929-120">Get Next Hop</span></span>

<span data-ttu-id="71929-121">Para obtener el próximo salto, llamamos al cmdlet `az network watcher show-next-hop`.</span><span class="sxs-lookup"><span data-stu-id="71929-121">To get the next hop we call the `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="71929-122">Pasamos al cmdlet el grupo de recursos de Network Watcher, NetworkWatcher, el identificador de la máquina virtual, la dirección IP de origen y dirección IP de destino.</span><span class="sxs-lookup"><span data-stu-id="71929-122">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="71929-123">En este ejemplo, la dirección IP de destino es una máquina virtual en otra red virtual.</span><span class="sxs-lookup"><span data-stu-id="71929-123">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="71929-124">Hay una puerta de enlace de red virtual entre las dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="71929-124">There is a virtual network gateway between the two virtual networks.</span></span>

<span data-ttu-id="71929-125">Si todavía no lo ha hecho, instale y configure la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="71929-125">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="71929-126">Luego, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="71929-126">Then run the following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="71929-127">Si la máquina virtual tiene varias NIC y el reenvío de IP está habilitado en cualquiera de ellas, debe especificarse el parámetro de NIC (-i nic-id).</span><span class="sxs-lookup"><span data-stu-id="71929-127">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="71929-128">De lo contrario, es opcional.</span><span class="sxs-lookup"><span data-stu-id="71929-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="71929-129">Revisión de los resultados</span><span class="sxs-lookup"><span data-stu-id="71929-129">Review results</span></span>

<span data-ttu-id="71929-130">Una vez finalizado, se proporcionan los resultados.</span><span class="sxs-lookup"><span data-stu-id="71929-130">When complete, the results are provided.</span></span> <span data-ttu-id="71929-131">Se devuelve la dirección IP del próximo salto y el tipo de recurso que es.</span><span class="sxs-lookup"><span data-stu-id="71929-131">The next hop IP address is returned as well as the type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="71929-132">La lista siguiente muestra los valores de NextHopType disponibles actualmente:</span><span class="sxs-lookup"><span data-stu-id="71929-132">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="71929-133">**Tipo de próximo salto**</span><span class="sxs-lookup"><span data-stu-id="71929-133">**Next Hop Type**</span></span>

* <span data-ttu-id="71929-134">Internet</span><span class="sxs-lookup"><span data-stu-id="71929-134">Internet</span></span>
* <span data-ttu-id="71929-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="71929-135">VirtualAppliance</span></span>
* <span data-ttu-id="71929-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="71929-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="71929-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="71929-137">VnetLocal</span></span>
* <span data-ttu-id="71929-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="71929-138">HyperNetGateway</span></span>
* <span data-ttu-id="71929-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="71929-139">VnetPeering</span></span>
* <span data-ttu-id="71929-140">None</span><span class="sxs-lookup"><span data-stu-id="71929-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="71929-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="71929-141">Next steps</span></span>

<span data-ttu-id="71929-142">Aprenda cómo revisar la configuración del grupo de seguridad de red mediante programación en [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Auditoría de NSG con Network Watcher).</span><span class="sxs-lookup"><span data-stu-id="71929-142">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
