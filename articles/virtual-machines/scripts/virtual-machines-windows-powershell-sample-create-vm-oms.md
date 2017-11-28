---
title: Ejemplo de Script de PowerShell - aaaAzure OMS | Documentos de Microsoft
description: 'Ejemplo de script de Azure PowerShell: OMS'
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
ms.date: 03/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eeafbe743013e97bf3fcefb5ce87f72cb503a4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="119ec-103">Creación de una máquina virtual supervisada de Operations Management Suite con PowerShell</span><span class="sxs-lookup"><span data-stu-id="119ec-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="119ec-104">Este script crea una máquina Virtual de Azure, instala al agente de Operations Management Suite (OMS) hello e inscribe sistema Hola con un área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="119ec-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="119ec-105">Una vez que se ejecutó la secuencia de comandos de hello, máquina virtual de hello serán visible en la consola de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="119ec-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span> <span data-ttu-id="119ec-106">Además, se necesita tooupdate Hola OMS área de trabajo área de trabajo y el identificador de clave.</span><span class="sxs-lookup"><span data-stu-id="119ec-106">Also, you need tooupdate hello OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="119ec-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="119ec-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="119ec-108">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="119ec-108">Clean up deployment</span></span> 

<span data-ttu-id="119ec-109">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="119ec-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="119ec-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="119ec-110">Script explanation</span></span>

<span data-ttu-id="119ec-111">Este script utiliza Hola después de la implementación de comandos toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="119ec-111">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="119ec-112">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="119ec-112">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="119ec-113">Comando</span><span class="sxs-lookup"><span data-stu-id="119ec-113">Command</span></span> | <span data-ttu-id="119ec-114">Notas</span><span class="sxs-lookup"><span data-stu-id="119ec-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="119ec-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="119ec-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="119ec-116">Crea un grupo de recursos en el que se almacenan todos los recursos.</span><span class="sxs-lookup"><span data-stu-id="119ec-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="119ec-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="119ec-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="119ec-118">Crea una configuración de subred.</span><span class="sxs-lookup"><span data-stu-id="119ec-118">Creates a subnet configuration.</span></span> <span data-ttu-id="119ec-119">Esta configuración se utiliza con el proceso de creación de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="119ec-119">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="119ec-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="119ec-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="119ec-121">Crea una red virtual.</span><span class="sxs-lookup"><span data-stu-id="119ec-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="119ec-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="119ec-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="119ec-123">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="119ec-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="119ec-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="119ec-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="119ec-125">Crea configuración de regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="119ec-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="119ec-126">Esta configuración es toocreate usa una regla de NSG cuando se crea hello NSG.</span><span class="sxs-lookup"><span data-stu-id="119ec-126">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="119ec-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="119ec-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="119ec-128">Crea un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="119ec-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="119ec-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="119ec-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="119ec-130">Obtiene la información de subred.</span><span class="sxs-lookup"><span data-stu-id="119ec-130">Gets subnet information.</span></span> <span data-ttu-id="119ec-131">Esta información se usa al crear una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="119ec-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="119ec-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="119ec-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="119ec-133">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="119ec-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="119ec-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="119ec-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="119ec-135">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="119ec-135">Creates a VM configuration.</span></span> <span data-ttu-id="119ec-136">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="119ec-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="119ec-137">configuración de Hola se utiliza durante la creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="119ec-137">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="119ec-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="119ec-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="119ec-139">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="119ec-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="119ec-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="119ec-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="119ec-141">Agregar una máquina virtual VM extensión toohello.</span><span class="sxs-lookup"><span data-stu-id="119ec-141">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="119ec-142">En este caso, Hola extensión del agente Operations Management Suite tooinstall usado Hola OMS agente e inscribir Hola máquina virtual en un área de trabajo OMS.</span><span class="sxs-lookup"><span data-stu-id="119ec-142">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="119ec-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="119ec-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="119ec-144">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="119ec-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="119ec-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="119ec-145">Next steps</span></span>

<span data-ttu-id="119ec-146">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="119ec-146">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="119ec-147">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="119ec-147">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
