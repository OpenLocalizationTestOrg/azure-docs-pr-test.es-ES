---
title: 'Ejemplo de script de Azure PowerShell: IIS | Microsoft Docs'
description: 'Ejemplo de script de Azure PowerShell: IIS'
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
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1f2f6301267c43919efc298573b6239cacf39239
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="97028-103">Creación de una máquina virtual IIS con PowerShell</span><span class="sxs-lookup"><span data-stu-id="97028-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="97028-104">Este script crea una máquina virtual de Azure con Windows Server 2016 y, a continuación, usa la extensión de scripts personalizados para máquinas virtuales de Azure para instalar IIS.</span><span class="sxs-lookup"><span data-stu-id="97028-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine Custom Script Extension to install IIS.</span></span> <span data-ttu-id="97028-105">Una vez ejecutado el script, puedo acceder al sitio web IIS predeterminado en la dirección IP pública de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="97028-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="97028-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="97028-106">Sample script</span></span>

<span data-ttu-id="97028-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Creación de una máquina virtual IIS")]</span><span class="sxs-lookup"><span data-stu-id="97028-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="97028-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="97028-108">Clean up deployment</span></span> 

<span data-ttu-id="97028-109">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="97028-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="97028-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="97028-110">Script explanation</span></span>

<span data-ttu-id="97028-111">Este script usa los siguientes comandos para crear la implementación.</span><span class="sxs-lookup"><span data-stu-id="97028-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="97028-112">Cada elemento de la tabla incluye vínculos a la documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="97028-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="97028-113">Comando</span><span class="sxs-lookup"><span data-stu-id="97028-113">Command</span></span> | <span data-ttu-id="97028-114">Notas</span><span class="sxs-lookup"><span data-stu-id="97028-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="97028-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="97028-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="97028-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="97028-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="97028-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="97028-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="97028-118">Crea una configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="97028-118">Creates a subnet configuration.</span></span> <span data-ttu-id="97028-119">Esta configuración se utiliza con el proceso de creación de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="97028-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="97028-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="97028-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="97028-121">Crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="97028-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="97028-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="97028-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="97028-123">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="97028-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="97028-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="97028-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="97028-125">Crea configuración de regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="97028-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="97028-126">Esta configuración se utiliza para crear una regla NSG cuando se crea el NSG.</span><span class="sxs-lookup"><span data-stu-id="97028-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="97028-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="97028-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="97028-128">Crea un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="97028-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="97028-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="97028-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="97028-130">Obtiene la información de subred.</span><span class="sxs-lookup"><span data-stu-id="97028-130">Gets subnet information.</span></span> <span data-ttu-id="97028-131">Esta información se usa al crear una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="97028-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="97028-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="97028-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="97028-133">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="97028-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="97028-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="97028-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="97028-135">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="97028-135">Creates a VM configuration.</span></span> <span data-ttu-id="97028-136">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="97028-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="97028-137">La configuración se utiliza durante la creación de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="97028-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="97028-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="97028-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="97028-139">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="97028-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="97028-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="97028-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="97028-141">Agregue una extensión de máquina virtual a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="97028-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="97028-142">En este ejemplo, se utiliza la extensión de scripts personalizados para instalar IIS.</span><span class="sxs-lookup"><span data-stu-id="97028-142">In this sample, the custom script extension is used to install IIS.</span></span> |
|[<span data-ttu-id="97028-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="97028-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="97028-144">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="97028-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="97028-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97028-145">Next steps</span></span>

<span data-ttu-id="97028-146">Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="97028-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="97028-147">Encontrará más ejemplos de scripts de Azure PowerShell de máquina virtual en la [documentación sobre máquinas virtuales Windows de Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97028-147">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
