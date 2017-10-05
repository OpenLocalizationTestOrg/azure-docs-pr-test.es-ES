---
title: 'Ejemplo de script de Azure PowerShell: WordPress | Microsoft Docs'
description: 'Ejemplo de script de Azure PowerShell: WordPress'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 778a6d5cfc63f80aa66654d682fedb178cfd67a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="102ce-103">Creación de una máquina virtual WordPress con PowerShell</span><span class="sxs-lookup"><span data-stu-id="102ce-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="102ce-104">Este script crea una máquina virtual y, a continuación, usa la extensión de scripts personalizados para máquinas virtuales de Azure para instalar WordPress.</span><span class="sxs-lookup"><span data-stu-id="102ce-104">This script creates a virtual machine and uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="102ce-105">Después de ejecutar el script, puede acceder al sitio de configuración de WordPress en `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="102ce-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="102ce-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="102ce-106">Sample script</span></span>

<span data-ttu-id="102ce-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Creación de una máquina virtual WordPress")]</span><span class="sxs-lookup"><span data-stu-id="102ce-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="102ce-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="102ce-108">Clean up deployment</span></span> 

<span data-ttu-id="102ce-109">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="102ce-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="102ce-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="102ce-110">Script explanation</span></span>

<span data-ttu-id="102ce-111">Este script usa los siguientes comandos para crear la implementación.</span><span class="sxs-lookup"><span data-stu-id="102ce-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="102ce-112">Cada elemento de la tabla incluye vínculos a la documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="102ce-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="102ce-113">Comando</span><span class="sxs-lookup"><span data-stu-id="102ce-113">Command</span></span> | <span data-ttu-id="102ce-114">Notas</span><span class="sxs-lookup"><span data-stu-id="102ce-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="102ce-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="102ce-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="102ce-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="102ce-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="102ce-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="102ce-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="102ce-118">Crea una configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="102ce-118">Creates a subnet configuration.</span></span> <span data-ttu-id="102ce-119">Esta configuración se utiliza con el proceso de creación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="102ce-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="102ce-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="102ce-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="102ce-121">Crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="102ce-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="102ce-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="102ce-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="102ce-123">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="102ce-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="102ce-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="102ce-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="102ce-125">Crea configuración de regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="102ce-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="102ce-126">Esta configuración se utiliza para crear una regla NSG cuando se crea el NSG.</span><span class="sxs-lookup"><span data-stu-id="102ce-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="102ce-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="102ce-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="102ce-128">Crea un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="102ce-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="102ce-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="102ce-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="102ce-130">Obtiene la información de subred.</span><span class="sxs-lookup"><span data-stu-id="102ce-130">Gets subnet information.</span></span> <span data-ttu-id="102ce-131">Esta información se usa al crear una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="102ce-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="102ce-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="102ce-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="102ce-133">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="102ce-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="102ce-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="102ce-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="102ce-135">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="102ce-135">Creates a VM configuration.</span></span> <span data-ttu-id="102ce-136">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="102ce-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="102ce-137">La configuración se utiliza durante la creación de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="102ce-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="102ce-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="102ce-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="102ce-139">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="102ce-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="102ce-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="102ce-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="102ce-141">Agregue la extensión de scripts personalizados a la máquina virtual que invoca un script para instalar WordPress.</span><span class="sxs-lookup"><span data-stu-id="102ce-141">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
|[<span data-ttu-id="102ce-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="102ce-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="102ce-143">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="102ce-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="102ce-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="102ce-144">Next steps</span></span>

<span data-ttu-id="102ce-145">Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="102ce-145">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="102ce-146">Encontrará más ejemplos de scripts de PowerShell de máquina virtual en la [documentación sobre máquinas virtuales Linux de Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="102ce-146">Additional virtual machine PowerShell script samples can be found in the [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
