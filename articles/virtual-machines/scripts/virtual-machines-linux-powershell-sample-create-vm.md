---
title: 'aaaAzure ejemplo de Script de PowerShell: crear una VM de Linux | Documentos de Microsoft'
description: "Ejemplo de script de Azure PowerShell: creación de una máquina virtual Linux"
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
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8ee2ee42aa68ee135a859b7eaead25811cf54095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="9f6db-103">Creación una máquina virtual completamente configurada con PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f6db-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="9f6db-104">Este script crea una máquina virtual de Azure con un sistema operativo Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="9f6db-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="9f6db-105">Después de ejecutar el script de Hola, puede tener acceso a máquina virtual de hello mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="9f6db-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9f6db-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9f6db-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.ps1 "Create VM detailed")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9f6db-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="9f6db-107">Clean up deployment</span></span> 

<span data-ttu-id="9f6db-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="9f6db-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9f6db-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="9f6db-109">Script explanation</span></span>

<span data-ttu-id="9f6db-110">Este script utiliza Hola después de la implementación de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6db-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="9f6db-111">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="9f6db-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9f6db-112">Comando</span><span class="sxs-lookup"><span data-stu-id="9f6db-112">Command</span></span> | <span data-ttu-id="9f6db-113">Notas</span><span class="sxs-lookup"><span data-stu-id="9f6db-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9f6db-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9f6db-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9f6db-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="9f6db-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9f6db-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9f6db-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9f6db-117">Crea una configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="9f6db-117">Creates a subnet configuration.</span></span> <span data-ttu-id="9f6db-118">Esta configuración se utiliza con el proceso de creación de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="9f6db-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="9f6db-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9f6db-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="9f6db-120">Crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="9f6db-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="9f6db-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="9f6db-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="9f6db-122">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="9f6db-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="9f6db-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9f6db-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="9f6db-124">Crea configuración de regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="9f6db-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="9f6db-125">Esta configuración es toocreate usa una regla de NSG cuando se crea hello NSG.</span><span class="sxs-lookup"><span data-stu-id="9f6db-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="9f6db-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="9f6db-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="9f6db-127">Crea un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="9f6db-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="9f6db-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9f6db-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9f6db-129">Obtiene la información de subred.</span><span class="sxs-lookup"><span data-stu-id="9f6db-129">Gets subnet information.</span></span> <span data-ttu-id="9f6db-130">Esta información se usa al crear una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="9f6db-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="9f6db-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="9f6db-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="9f6db-132">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="9f6db-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="9f6db-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="9f6db-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="9f6db-134">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f6db-134">Creates a VM configuration.</span></span> <span data-ttu-id="9f6db-135">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="9f6db-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="9f6db-136">configuración de Hola se utiliza durante la creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9f6db-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="9f6db-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9f6db-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="9f6db-138">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f6db-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="9f6db-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9f6db-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9f6db-140">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="9f6db-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9f6db-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f6db-141">Next steps</span></span>

<span data-ttu-id="9f6db-142">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9f6db-142">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9f6db-143">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f6db-143">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
