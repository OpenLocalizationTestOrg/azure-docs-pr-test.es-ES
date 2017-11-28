---
title: "Ejemplo de script de Azure PowerShell: filtrar el tráfico de red de VM | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: filtrar el tráfico de red de VM entrante y saliente."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: e871ba2f370157936c2aaabc804dc9f5aea6d7ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="1f85c-103">Filtrar el tráfico de red de VM entrante y saliente</span><span class="sxs-lookup"><span data-stu-id="1f85c-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="1f85c-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="1f85c-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="1f85c-105">El tráfico de red entrante hacia la subred de front-end se limita a HTTP y HTTPS, mientras que el tráfico saliente hacia Internet desde la subred back-end no está permitido.</span><span class="sxs-lookup"><span data-stu-id="1f85c-105">Inbound network traffic to the front-end subnet is limited to HTTP, and HTTPS, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="1f85c-106">Después de ejecutar el script, tendrá una máquina virtual con dos NIC.</span><span class="sxs-lookup"><span data-stu-id="1f85c-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="1f85c-107">Cada NIC se conecta a una subred diferente.</span><span class="sxs-lookup"><span data-stu-id="1f85c-107">Each NIC is connected to a different subnet.</span></span>

<span data-ttu-id="1f85c-108">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="1f85c-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1f85c-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="1f85c-109">Sample script</span></span>


<span data-ttu-id="1f85c-110">[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filtrar el tráfico de red de VM")]</span><span class="sxs-lookup"><span data-stu-id="1f85c-110">[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1f85c-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="1f85c-111">Clean up deployment</span></span> 

<span data-ttu-id="1f85c-112">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="1f85c-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="1f85c-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="1f85c-113">Script explanation</span></span>

<span data-ttu-id="1f85c-114">Este script usa los siguientes comandos para crear un grupo de recursos, una red virtual y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="1f85c-114">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="1f85c-115">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="1f85c-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="1f85c-116">Comando</span><span class="sxs-lookup"><span data-stu-id="1f85c-116">Command</span></span> | <span data-ttu-id="1f85c-117">Notas</span><span class="sxs-lookup"><span data-stu-id="1f85c-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1f85c-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1f85c-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1f85c-119">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="1f85c-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1f85c-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="1f85c-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="1f85c-121">Crea un objeto de configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="1f85c-121">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="1f85c-122">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="1f85c-122">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="1f85c-123">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="1f85c-123">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="1f85c-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="1f85c-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="1f85c-125">Crea reglas de seguridad que se asignarán a un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="1f85c-125">Creates security rules to be assigned to a network security group.</span></span> |
| [<span data-ttu-id="1f85c-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="1f85c-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="1f85c-127">Crea reglas NSG que permiten o bloquean puertos específicos para subredes concretas.</span><span class="sxs-lookup"><span data-stu-id="1f85c-127">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="1f85c-128">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="1f85c-128">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="1f85c-129">Asocia NSG a subredes.</span><span class="sxs-lookup"><span data-stu-id="1f85c-129">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="1f85c-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="1f85c-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="1f85c-131">Crea una dirección IP pública para acceder a la VM desde Internet.</span><span class="sxs-lookup"><span data-stu-id="1f85c-131">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="1f85c-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="1f85c-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="1f85c-133">Crea interfaces de red virtual y las asocia a subredes de front-end y back-end de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="1f85c-133">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="1f85c-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="1f85c-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="1f85c-135">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1f85c-135">Creates a VM configuration.</span></span> <span data-ttu-id="1f85c-136">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="1f85c-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="1f85c-137">La configuración se utiliza durante la creación de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1f85c-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="1f85c-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="1f85c-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="1f85c-139">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="1f85c-139">Create a virtual machine.</span></span> |
|[<span data-ttu-id="1f85c-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1f85c-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1f85c-141">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="1f85c-141">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1f85c-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1f85c-142">Next steps</span></span>

<span data-ttu-id="1f85c-143">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1f85c-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="1f85c-144">En la [documentación de la información general de redes de Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json) puede encontrar ejemplos adicionales de script de PowerShell de redes.</span><span class="sxs-lookup"><span data-stu-id="1f85c-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>