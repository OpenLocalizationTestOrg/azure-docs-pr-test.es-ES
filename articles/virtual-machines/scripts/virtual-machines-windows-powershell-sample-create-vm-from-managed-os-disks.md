---
title: "aaaAzure ejemplo de Script de PowerShell: crear una máquina virtual si se adjunta un disco como disco del sistema operativo administrado | Documentos de Microsoft"
description: "Script de Azure PowerShell de Azure de ejemplo: creación de una máquina virtual conectando un disco administrado como disco del SO"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="52ee3-103">Creación de una máquina virtual con un disco del SO administrado mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="52ee3-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="52ee3-104">Este script crea una máquina virtual conectando un disco administrado como disco del SO.</span><span class="sxs-lookup"><span data-stu-id="52ee3-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="52ee3-105">Use este script en los anteriores escenarios:</span><span class="sxs-lookup"><span data-stu-id="52ee3-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="52ee3-106">Creación de una máquina virtual desde un disco del SO administrado que se copió desde un disco administrado de otra suscripción</span><span class="sxs-lookup"><span data-stu-id="52ee3-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="52ee3-107">Creación de una máquina virtual desde un disco administrado que se creó a partir de un archivo de disco duro virtual especializado</span><span class="sxs-lookup"><span data-stu-id="52ee3-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="52ee3-108">Creación de una máquina virtual desde un disco del SO administrado que se creó a partir de una instantánea</span><span class="sxs-lookup"><span data-stu-id="52ee3-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="52ee3-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="52ee3-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="52ee3-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="52ee3-110">Clean up deployment</span></span> 

<span data-ttu-id="52ee3-111">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="52ee3-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="52ee3-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="52ee3-112">Script explanation</span></span>

<span data-ttu-id="52ee3-113">Este script utiliza Hola comandos tooget administrado disco propiedades siguientes, adjuntar un disco administrado tooa nueva máquina virtual y cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="52ee3-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="52ee3-114">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="52ee3-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="52ee3-115">Comando</span><span class="sxs-lookup"><span data-stu-id="52ee3-115">Command</span></span> | <span data-ttu-id="52ee3-116">Notas</span><span class="sxs-lookup"><span data-stu-id="52ee3-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="52ee3-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="52ee3-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="52ee3-118">Obtiene el objeto de disco basado en nombre de Hola y el grupo de recursos de Hola de un disco.</span><span class="sxs-lookup"><span data-stu-id="52ee3-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="52ee3-119">Propiedad de Id. de hello devuelto objeto de disco es tooattach usado Hola disco tooa nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="52ee3-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="52ee3-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="52ee3-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="52ee3-121">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="52ee3-121">Creates a VM configuration.</span></span> <span data-ttu-id="52ee3-122">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="52ee3-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="52ee3-123">configuración de Hola se utiliza durante la creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="52ee3-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="52ee3-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="52ee3-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="52ee3-125">Adjunta un disco administrado mediante la propiedad de Id. de hello del disco de hello como sistema operativo disco tooa nueva máquina virtual de</span><span class="sxs-lookup"><span data-stu-id="52ee3-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="52ee3-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="52ee3-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="52ee3-127">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="52ee3-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="52ee3-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="52ee3-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="52ee3-129">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="52ee3-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="52ee3-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="52ee3-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="52ee3-131">Cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="52ee3-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="52ee3-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="52ee3-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="52ee3-133">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="52ee3-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="52ee3-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52ee3-134">Next steps</span></span>

<span data-ttu-id="52ee3-135">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="52ee3-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="52ee3-136">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="52ee3-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
