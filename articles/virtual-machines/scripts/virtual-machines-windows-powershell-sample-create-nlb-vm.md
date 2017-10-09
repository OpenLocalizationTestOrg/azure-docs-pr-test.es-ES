---
title: "aaaAzure ejemplo de Script de PowerShell: crear una máquina virtual de Windows NLB | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: creación de un NLB de máquina virtual Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 60a48c5f243c8ff3ab886437ae45b21ce069ea4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="47175-103">Equilibrio de la carga de tráfico entre máquinas virtuales de alta disponibilidad</span><span class="sxs-lookup"><span data-stu-id="47175-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="47175-104">Este ejemplo de secuencia de comandos crea todo lo necesario toorun varias máquinas virtuales de Windows Server 2016 configurado en una alta disponibilidad y de carga equilibrada de configuración.</span><span class="sxs-lookup"><span data-stu-id="47175-104">This script sample creates everything needed toorun several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="47175-105">Después de ejecutar script de Hola, tendrá tres máquinas virtuales, tooan Unidos a un conjunto de disponibilidad de Azure y es accesible a través de un equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="47175-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="47175-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="47175-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="47175-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="47175-107">Clean up deployment</span></span> 

<span data-ttu-id="47175-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="47175-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="47175-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="47175-109">Script explanation</span></span>

<span data-ttu-id="47175-110">Este script utiliza Hola después de la implementación de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="47175-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="47175-111">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="47175-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="47175-112">Comando</span><span class="sxs-lookup"><span data-stu-id="47175-112">Command</span></span> | <span data-ttu-id="47175-113">Notas</span><span class="sxs-lookup"><span data-stu-id="47175-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="47175-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="47175-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="47175-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="47175-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="47175-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="47175-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="47175-117">Crea una configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="47175-117">Creates a subnet configuration.</span></span> <span data-ttu-id="47175-118">Esta configuración se utiliza con el proceso de creación de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="47175-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="47175-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="47175-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="47175-120">Crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="47175-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="47175-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="47175-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="47175-122">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="47175-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="47175-123">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="47175-123">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="47175-124">Crea una configuración de dirección IP de Front-End para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="47175-124">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="47175-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="47175-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="47175-126">Crea una configuración de grupo de direcciones de back-end para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="47175-126">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="47175-127">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="47175-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="47175-128">Crea una configuración de sondeo para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="47175-128">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="47175-129">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="47175-129">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="47175-130">Crea una configuración de regla para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="47175-130">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="47175-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="47175-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="47175-132">Crea una configuración de regla NAT entrante para un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="47175-132">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="47175-133">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="47175-133">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="47175-134">Crea un equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="47175-134">Creates a load balancer.</span></span> |
| [<span data-ttu-id="47175-135">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="47175-135">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="47175-136">Crea configuración de regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="47175-136">Creates a network security group rule configuration.</span></span> <span data-ttu-id="47175-137">Esta configuración es toocreate usa una regla de NSG cuando se crea hello NSG.</span><span class="sxs-lookup"><span data-stu-id="47175-137">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="47175-138">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="47175-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="47175-139">Crea un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="47175-139">Creates a network security group.</span></span> |
| [<span data-ttu-id="47175-140">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="47175-140">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="47175-141">Obtiene la información de subred.</span><span class="sxs-lookup"><span data-stu-id="47175-141">Gets subnet information.</span></span> <span data-ttu-id="47175-142">Esta información se usa al crear una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="47175-142">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="47175-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="47175-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="47175-144">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="47175-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="47175-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="47175-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="47175-146">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47175-146">Creates a VM configuration.</span></span> <span data-ttu-id="47175-147">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="47175-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="47175-148">configuración de Hola se utiliza durante la creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="47175-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="47175-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="47175-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="47175-150">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47175-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="47175-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="47175-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="47175-152">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="47175-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="47175-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="47175-153">Next steps</span></span>

<span data-ttu-id="47175-154">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="47175-154">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="47175-155">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="47175-155">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
