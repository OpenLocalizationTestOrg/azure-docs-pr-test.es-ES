---
title: "ejemplo de script de PowerShell aaaAzure - enrutar el tráfico a través de un dispositivo virtual de red | Documentos de Microsoft"
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="9c657-103">Redirigir el tráfico a través de una aplicación virtual de red</span><span class="sxs-lookup"><span data-stu-id="9c657-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="9c657-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="9c657-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="9c657-105">También se crea una máquina virtual con la dirección IP que reenvía el tráfico de tooroute habilitado entre dos subredes de Hola.</span><span class="sxs-lookup"><span data-stu-id="9c657-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="9c657-106">Después de ejecutar el script de Hola puede implementar software de red, como una aplicación de firewall, toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9c657-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

<span data-ttu-id="9c657-107">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="9c657-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9c657-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9c657-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9c657-109">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="9c657-109">Clean up deployment</span></span> 

<span data-ttu-id="9c657-110">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="9c657-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="9c657-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="9c657-111">Script explanation</span></span>

<span data-ttu-id="9c657-112">Este script utiliza Hola después comandos toocreate un grupo de recursos, redes virtuales y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="9c657-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="9c657-113">Cada comando de la tabla de hello vincula documentación específica del toocommand.</span><span class="sxs-lookup"><span data-stu-id="9c657-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="9c657-114">Comando</span><span class="sxs-lookup"><span data-stu-id="9c657-114">Command</span></span> | <span data-ttu-id="9c657-115">Notas</span><span class="sxs-lookup"><span data-stu-id="9c657-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9c657-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9c657-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="9c657-117">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="9c657-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9c657-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9c657-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="9c657-119">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="9c657-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="9c657-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9c657-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9c657-121">Crea subredes de back-end y de red perimetral.</span><span class="sxs-lookup"><span data-stu-id="9c657-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="9c657-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="9c657-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="9c657-123">Crea un Hola de tooaccess VM pública para la dirección IP de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="9c657-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="9c657-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="9c657-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="9c657-125">Crea una interfaz de red virtual y habilita el reenvío IP para ella.</span><span class="sxs-lookup"><span data-stu-id="9c657-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="9c657-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="9c657-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="9c657-127">Crea un grupo de seguridad de red (NSG).</span><span class="sxs-lookup"><span data-stu-id="9c657-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="9c657-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9c657-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="9c657-129">Crea reglas NSG que permiten a los puertos HTTP y HTTPS entrantes toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9c657-129">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="9c657-130">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9c657-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="9c657-131">Asocia Hola NSG y toosubnets de tablas de ruta.</span><span class="sxs-lookup"><span data-stu-id="9c657-131">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="9c657-132">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="9c657-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="9c657-133">Crea una tabla de rutas para todas las rutas.</span><span class="sxs-lookup"><span data-stu-id="9c657-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="9c657-134">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="9c657-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="9c657-135">Crea rutas tooroute tráfico entre subredes y Hola Internet a través de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9c657-135">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="9c657-136">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9c657-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="9c657-137">Crea una máquina virtual y conecta Hola NIC tooit.</span><span class="sxs-lookup"><span data-stu-id="9c657-137">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="9c657-138">Este comando también especifica toouse de imagen de máquina virtual de Hola y credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="9c657-138">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="9c657-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9c657-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="9c657-140">Elimina un grupo de recursos y todos los recursos que contiene.</span><span class="sxs-lookup"><span data-stu-id="9c657-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9c657-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9c657-141">Next steps</span></span>

<span data-ttu-id="9c657-142">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9c657-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="9c657-143">Encontrará ejemplos de script de PowerShell de red adicionales en hello [documentación de introducción a las redes Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9c657-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
