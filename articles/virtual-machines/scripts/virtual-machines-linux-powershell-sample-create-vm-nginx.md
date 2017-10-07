---
title: aaaAzure ejemplo de Script de PowerShell - NGINX | Documentos de Microsoft
description: 'Ejemplo de script de Azure PowerShell: NGINX'
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
ms.openlocfilehash: 017a4853e400f8f544a3f92771adaf468b5dee76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-nginx-vm-with-powershell"></a><span data-ttu-id="ea9c8-103">Creación de una máquina virtual NGINX con PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea9c8-103">Create an NGINX VM with PowerShell</span></span>

<span data-ttu-id="ea9c8-104">Este script crea una máquina Virtual de Azure y, a continuación, usa Hola extensión de Script personalizado de Azure Virtual Machine tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-104">This script creates an Azure Virtual Machine and then uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="ea9c8-105">Después de ejecutar el script de Hola, puede tener acceso a un sitio Web de demostración de la dirección IP pública de Hola de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ea9c8-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="ea9c8-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.ps1 "Create VM NGINX")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ea9c8-107">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="ea9c8-107">Clean up deployment</span></span> 

<span data-ttu-id="ea9c8-108">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ea9c8-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="ea9c8-109">Script explanation</span></span>

<span data-ttu-id="ea9c8-110">Este script utiliza Hola después de la implementación de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="ea9c8-111">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ea9c8-112">Comando</span><span class="sxs-lookup"><span data-stu-id="ea9c8-112">Command</span></span> | <span data-ttu-id="ea9c8-113">Notas</span><span class="sxs-lookup"><span data-stu-id="ea9c8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ea9c8-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ea9c8-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ea9c8-115">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ea9c8-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ea9c8-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ea9c8-117">Crea una configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-117">Creates a subnet configuration.</span></span> <span data-ttu-id="ea9c8-118">Esta configuración se utiliza con el proceso de creación de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="ea9c8-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="ea9c8-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="ea9c8-120">Crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="ea9c8-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ea9c8-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ea9c8-122">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ea9c8-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ea9c8-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="ea9c8-124">Crea configuración de regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="ea9c8-125">Esta configuración es toocreate usa una regla de NSG cuando se crea hello NSG.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="ea9c8-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="ea9c8-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="ea9c8-127">Crea un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="ea9c8-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="ea9c8-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="ea9c8-129">Obtiene la información de subred.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-129">Gets subnet information.</span></span> <span data-ttu-id="ea9c8-130">Esta información se usa al crear una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="ea9c8-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ea9c8-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ea9c8-132">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="ea9c8-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ea9c8-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="ea9c8-134">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-134">Creates a VM configuration.</span></span> <span data-ttu-id="ea9c8-135">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ea9c8-136">configuración de Hola se utiliza durante la creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ea9c8-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ea9c8-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ea9c8-138">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="ea9c8-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="ea9c8-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="ea9c8-140">Agregar una máquina virtual VM extensión toohello.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="ea9c8-141">En este ejemplo, la extensión de script personalizado de hello es usado tooinstall NGINX.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-141">In this sample, hello custom script extension is used tooinstall NGINX.</span></span> |
|[<span data-ttu-id="ea9c8-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ea9c8-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ea9c8-143">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="ea9c8-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ea9c8-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ea9c8-144">Next steps</span></span>

<span data-ttu-id="ea9c8-145">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ea9c8-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ea9c8-146">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea9c8-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>