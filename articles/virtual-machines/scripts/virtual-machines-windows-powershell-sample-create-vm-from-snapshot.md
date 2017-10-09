---
title: "aaaAzure ejemplo de Script de PowerShell: crear una máquina virtual desde una instantánea | Documentos de Microsoft"
description: "Ejemplo de script de Azure PowerShell: creación de una máquina virtual a partir de una instantánea"
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
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="aff15-103">Creación de una máquina virtual a partir de una instantánea con PowerShell</span><span class="sxs-lookup"><span data-stu-id="aff15-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="aff15-104">Este script crea una máquina virtual a partir de una instantánea de un disco del SO.</span><span class="sxs-lookup"><span data-stu-id="aff15-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="aff15-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="aff15-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="aff15-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="aff15-106">Clean up deployment</span></span> 

<span data-ttu-id="aff15-107">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="aff15-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="aff15-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="aff15-108">Script explanation</span></span>

<span data-ttu-id="aff15-109">Este script utiliza Hola después comandos tooget propiedades de la instantánea, crear un disco administrado desde la instantánea y crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="aff15-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="aff15-110">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="aff15-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="aff15-111">Comando</span><span class="sxs-lookup"><span data-stu-id="aff15-111">Command</span></span> | <span data-ttu-id="aff15-112">Notas</span><span class="sxs-lookup"><span data-stu-id="aff15-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="aff15-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="aff15-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="aff15-114">Obtiene una instantánea con el nombre de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="aff15-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="aff15-115">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="aff15-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="aff15-116">Crea una configuración de disco.</span><span class="sxs-lookup"><span data-stu-id="aff15-116">Creates a disk configuration.</span></span> <span data-ttu-id="aff15-117">Esta configuración se utiliza con el proceso de creación del disco de Hola.</span><span class="sxs-lookup"><span data-stu-id="aff15-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="aff15-118">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="aff15-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="aff15-119">Crea un disco administrado.</span><span class="sxs-lookup"><span data-stu-id="aff15-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="aff15-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="aff15-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="aff15-121">Crea una configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="aff15-121">Creates a VM configuration.</span></span> <span data-ttu-id="aff15-122">Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas.</span><span class="sxs-lookup"><span data-stu-id="aff15-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="aff15-123">configuración de Hola se utiliza durante la creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="aff15-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="aff15-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="aff15-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="aff15-125">Disco administrado Hola se asocia como máquina virtual de sistema operativo disco toohello</span><span class="sxs-lookup"><span data-stu-id="aff15-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="aff15-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="aff15-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="aff15-127">Crea una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="aff15-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="aff15-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="aff15-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="aff15-129">Crea una interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="aff15-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="aff15-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="aff15-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="aff15-131">Crea una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="aff15-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="aff15-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="aff15-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="aff15-133">Quita un grupo de recursos y todos los recursos incluidos en él.</span><span class="sxs-lookup"><span data-stu-id="aff15-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="aff15-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="aff15-134">Next steps</span></span>

<span data-ttu-id="aff15-135">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aff15-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="aff15-136">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aff15-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
