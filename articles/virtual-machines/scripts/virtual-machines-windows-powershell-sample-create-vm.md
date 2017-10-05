---
title: "Ejemplo de script de Azure PowerShell: creación de una máquina virtual Windows | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: creación de una máquina virtual Windows"
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
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: a9e46aded0cf3792558a7fba6f00e5662166cc0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="ccfe8-103">Creación una máquina virtual completamente configurada con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccfe8-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="ccfe8-104">Este script crea una máquina virtual de Azure donde se ejecuta Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="ccfe8-105">Después de ejecutar el script, puede acceder a la máquina virtual a través de RDP.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-105">After running the script, you can access the virtual machine over RDP.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ccfe8-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ccfe8-106">Sample script</span></span>

<span data-ttu-id="ccfe8-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.ps1 "Creación detallada de una máquina virtual")]</span><span class="sxs-lookup"><span data-stu-id="ccfe8-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.ps1 "Create VM detailed")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ccfe8-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="ccfe8-108">Clean up deployment</span></span> 

<span data-ttu-id="ccfe8-109">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ccfe8-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="ccfe8-110">Script explanation</span></span>

<span data-ttu-id="ccfe8-111">Este script usa los siguientes comandos para crear la implementación.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="ccfe8-112">Cada elemento de la tabla incluye vínculos a la documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ccfe8-113">Comando</span><span class="sxs-lookup"><span data-stu-id="ccfe8-113">Command</span></span> | <span data-ttu-id="ccfe8-114">Notas</span><span class="sxs-lookup"><span data-stu-id="ccfe8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ccfe8-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ccfe8-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ccfe8-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ccfe8-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ccfe8-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ccfe8-118">Crea una configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-118">Creates a subnet configuration.</span></span> <span data-ttu-id="ccfe8-119">Esta configuración se utiliza con el proceso de creación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="ccfe8-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ccfe8-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ccfe8-121">Crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="ccfe8-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ccfe8-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ccfe8-123">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ccfe8-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ccfe8-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="ccfe8-125">Crea configuración de regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="ccfe8-126">Esta configuración se utiliza para crear una regla NSG cuando se crea el NSG.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="ccfe8-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ccfe8-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="ccfe8-128">Crea un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="ccfe8-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ccfe8-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ccfe8-130">Obtiene la información de subred.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-130">Gets subnet information.</span></span> <span data-ttu-id="ccfe8-131">Esta información se usa al crear una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="ccfe8-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ccfe8-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ccfe8-133">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="ccfe8-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ccfe8-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="ccfe8-135">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-135">Creates a VM configuration.</span></span> <span data-ttu-id="ccfe8-136">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ccfe8-137">La configuración se utiliza durante la creación de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ccfe8-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ccfe8-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ccfe8-139">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-139">Create a virtual machine.</span></span> |
|[<span data-ttu-id="ccfe8-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ccfe8-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ccfe8-141">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="ccfe8-141">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ccfe8-142">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ccfe8-142">Next steps</span></span>

<span data-ttu-id="ccfe8-143">Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ccfe8-143">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ccfe8-144">Encontrará más ejemplos de scripts de Azure PowerShell de máquina virtual en la [documentación sobre máquinas virtuales Windows de Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ccfe8-144">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
