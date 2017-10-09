---
title: "ejemplo de script de PowerShell aaaAzure - tráfico de red de VM de filtro | Documentos de Microsoft"
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
ms.openlocfilehash: 39eae6a43a8dc7f9fc616ef3ec50f95443fd3547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="caf9a-103">Filtrar el tráfico de red de VM entrante y saliente</span><span class="sxs-lookup"><span data-stu-id="caf9a-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="caf9a-104">Este ejemplo de script crea una red virtual con subredes de front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="caf9a-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="caf9a-105">El tráfico de red entrante toohello la subred front-end es tooHTTP limitado y tráfico HTTPS, mientras saliente, toohello Internet desde la subred de back-end de hello no está permitida.</span><span class="sxs-lookup"><span data-stu-id="caf9a-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, and HTTPS, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="caf9a-106">Después de ejecutar el script de Hola, tendrá una máquina virtual con dos NIC.</span><span class="sxs-lookup"><span data-stu-id="caf9a-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="caf9a-107">Cada NIC está conectado tooa otra subred.</span><span class="sxs-lookup"><span data-stu-id="caf9a-107">Each NIC is connected tooa different subnet.</span></span>

<span data-ttu-id="caf9a-108">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="caf9a-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="caf9a-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="caf9a-109">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="caf9a-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="caf9a-110">Clean up deployment</span></span> 

<span data-ttu-id="caf9a-111">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="caf9a-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="caf9a-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="caf9a-112">Script explanation</span></span>

<span data-ttu-id="caf9a-113">Este script utiliza Hola después comandos toocreate un grupo de recursos, redes virtuales y grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="caf9a-113">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="caf9a-114">Cada comando de la tabla de hello vincula documentación específica del toocommand.</span><span class="sxs-lookup"><span data-stu-id="caf9a-114">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="caf9a-115">Comando</span><span class="sxs-lookup"><span data-stu-id="caf9a-115">Command</span></span> | <span data-ttu-id="caf9a-116">Notas</span><span class="sxs-lookup"><span data-stu-id="caf9a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="caf9a-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="caf9a-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="caf9a-118">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="caf9a-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="caf9a-119">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="caf9a-119">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="caf9a-120">Crea un objeto de configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="caf9a-120">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="caf9a-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="caf9a-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="caf9a-122">Crea una subred de front-end y una red virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="caf9a-122">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="caf9a-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="caf9a-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="caf9a-124">Crea toobe de reglas de seguridad asignado a tooa grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="caf9a-124">Creates security rules toobe assigned tooa network security group.</span></span> |
| [<span data-ttu-id="caf9a-125">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="caf9a-125">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="caf9a-126">Crea reglas NSG que permiten o bloquear subredes toospecific de puertos específicos.</span><span class="sxs-lookup"><span data-stu-id="caf9a-126">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="caf9a-127">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="caf9a-127">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="caf9a-128">Asocia los NSG toosubnets.</span><span class="sxs-lookup"><span data-stu-id="caf9a-128">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="caf9a-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="caf9a-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="caf9a-130">Crea un Hola de tooaccess VM pública para la dirección IP de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="caf9a-130">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="caf9a-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="caf9a-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="caf9a-132">Crea las interfaces de red virtual y los asocia subredes de la red virtual toohello front-end y back-end.</span><span class="sxs-lookup"><span data-stu-id="caf9a-132">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="caf9a-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="caf9a-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="caf9a-134">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="caf9a-134">Creates a VM configuration.</span></span> <span data-ttu-id="caf9a-135">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="caf9a-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="caf9a-136">configuración de Hola se utiliza durante la creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="caf9a-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="caf9a-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="caf9a-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="caf9a-138">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="caf9a-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="caf9a-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="caf9a-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="caf9a-140">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="caf9a-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="caf9a-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="caf9a-141">Next steps</span></span>

<span data-ttu-id="caf9a-142">Para obtener más información sobre hello Azure PowerShell, consulte [documentación de Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="caf9a-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="caf9a-143">Encontrará ejemplos de script de PowerShell de red adicionales en hello [documentación de introducción a las redes Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="caf9a-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
