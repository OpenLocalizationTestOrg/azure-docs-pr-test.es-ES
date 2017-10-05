---
title: "Ejemplo de script de Azure PowerShell: redirigir el tráfico a través de una aplicación virtual de red | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: redirigir el tráfico a través de una aplicación virtual de red de firewall."
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
ms.openlocfilehash: 883d28dac72a66c2186d222f72b04d68e532cead
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="7aced-103">Redirigir el tráfico a través de una aplicación virtual de red</span><span class="sxs-lookup"><span data-stu-id="7aced-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="7aced-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="7aced-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="7aced-105">También crea una VM con el reenvío IP habilitado para redirigir el tráfico entre las dos subredes.</span><span class="sxs-lookup"><span data-stu-id="7aced-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="7aced-106">Después de ejecutar el script puede implementar software de red, como una aplicación de firewall, en la VM.</span><span class="sxs-lookup"><span data-stu-id="7aced-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

<span data-ttu-id="7aced-107">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) y, luego, ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="7aced-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7aced-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7aced-108">Sample script</span></span>


<span data-ttu-id="7aced-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Redirigir el tráfico a través de una aplicación virtual de red")]</span><span class="sxs-lookup"><span data-stu-id="7aced-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7aced-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="7aced-110">Clean up deployment</span></span> 

<span data-ttu-id="7aced-111">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="7aced-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="7aced-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="7aced-112">Script explanation</span></span>

<span data-ttu-id="7aced-113">Este script usa los siguientes comandos para crear un grupo de recursos, una red virtual y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="7aced-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="7aced-114">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="7aced-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="7aced-115">Comando</span><span class="sxs-lookup"><span data-stu-id="7aced-115">Command</span></span> | <span data-ttu-id="7aced-116">Notas</span><span class="sxs-lookup"><span data-stu-id="7aced-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7aced-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7aced-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="7aced-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="7aced-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7aced-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="7aced-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="7aced-120">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="7aced-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="7aced-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="7aced-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="7aced-122">Crea subredes de back-end y de red perimetral.</span><span class="sxs-lookup"><span data-stu-id="7aced-122">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="7aced-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="7aced-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="7aced-124">Crea una dirección IP pública para acceder a la VM desde Internet.</span><span class="sxs-lookup"><span data-stu-id="7aced-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="7aced-125">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="7aced-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="7aced-126">Crea una interfaz de red virtual y habilita el reenvío IP para ella.</span><span class="sxs-lookup"><span data-stu-id="7aced-126">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="7aced-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="7aced-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="7aced-128">Crea un grupo de seguridad de red (NSG).</span><span class="sxs-lookup"><span data-stu-id="7aced-128">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="7aced-129">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="7aced-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="7aced-130">Crea reglas NSG que permiten puertos HTTP y HTTPS entrantes en la VM.</span><span class="sxs-lookup"><span data-stu-id="7aced-130">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="7aced-131">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="7aced-131">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="7aced-132">Asocia los NSG y tablas de rutas a las subredes.</span><span class="sxs-lookup"><span data-stu-id="7aced-132">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="7aced-133">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="7aced-133">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="7aced-134">Crea una tabla de rutas para todas las rutas.</span><span class="sxs-lookup"><span data-stu-id="7aced-134">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="7aced-135">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="7aced-135">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="7aced-136">Crea rutas para redirigir el tráfico entre subredes e Internet a través de la VM.</span><span class="sxs-lookup"><span data-stu-id="7aced-136">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="7aced-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="7aced-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="7aced-138">Crea una máquina virtual y conecta la NIC a ella.</span><span class="sxs-lookup"><span data-stu-id="7aced-138">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="7aced-139">Este comando también especifica la imagen de máquina virtual que se usará y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="7aced-139">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="7aced-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7aced-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="7aced-141">Elimina un grupo de recursos y todos los recursos que contiene.</span><span class="sxs-lookup"><span data-stu-id="7aced-141">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7aced-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7aced-142">Next steps</span></span>

<span data-ttu-id="7aced-143">Para más información sobre Azure PowerShell, consulte la [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7aced-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="7aced-144">En la [documentación de la información general de redes de Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json) puede encontrar ejemplos adicionales de script de PowerShell de redes.</span><span class="sxs-lookup"><span data-stu-id="7aced-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>