---
title: "Ejemplo de script de Azure PowerShell: creación de un disco administrado a partir de una instantánea | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: creación de un disco administrado a partir de una instantánea"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: b475516694d120b7ea05d0892b6789710eec171e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="a89e0-103">Creación de un disco administrado a partir de una instantánea con PowerShell</span><span class="sxs-lookup"><span data-stu-id="a89e0-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="a89e0-104">Este script crea un disco administrado a partir de una instantánea.</span><span class="sxs-lookup"><span data-stu-id="a89e0-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="a89e0-105">Úselo para restaurar una máquina virtual a partir de las instantáneas de discos de sistema operativo y datos.</span><span class="sxs-lookup"><span data-stu-id="a89e0-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="a89e0-106">Cree los discos de sistema operativo y datos a partir de las instantáneas correspondientes y, luego, cree una nueva máquina virtual conectando los discos administrados.</span><span class="sxs-lookup"><span data-stu-id="a89e0-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="a89e0-107">También puede restaurar los discos de datos de una máquina virtual existente conectando los discos de datos creados a partir de las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="a89e0-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a89e0-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a89e0-108">Sample script</span></span>

<span data-ttu-id="a89e0-109">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Crear un disco administrado a partir de una instantánea")]</span><span class="sxs-lookup"><span data-stu-id="a89e0-109">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="a89e0-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="a89e0-110">Script explanation</span></span>

<span data-ttu-id="a89e0-111">Este script usa los siguientes comandos para crear un disco administrado a partir de una instantánea.</span><span class="sxs-lookup"><span data-stu-id="a89e0-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="a89e0-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="a89e0-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a89e0-113">Comando</span><span class="sxs-lookup"><span data-stu-id="a89e0-113">Command</span></span> | <span data-ttu-id="a89e0-114">Notas</span><span class="sxs-lookup"><span data-stu-id="a89e0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a89e0-115">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="a89e0-115">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="a89e0-116">Obtiene las propiedades de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="a89e0-116">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="a89e0-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="a89e0-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="a89e0-118">Crea la configuración de disco que se usa para la creación del disco.</span><span class="sxs-lookup"><span data-stu-id="a89e0-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="a89e0-119">Incluye el identificador de recurso de la instantánea principal y una ubicación igual a la de la instantánea principal y el tipo de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a89e0-119">It includes the resource Id of the parent snapshot, location that is same as the location of parent snapshot and the storage type.</span></span>  |
| [<span data-ttu-id="a89e0-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="a89e0-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="a89e0-121">Crea un disco mediante la configuración de disco, el nombre del disco y el nombre del grupo de recursos que se pasan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="a89e0-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="a89e0-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a89e0-122">Next steps</span></span>

[<span data-ttu-id="a89e0-123">Crear una máquina virtual a partir de un disco administrado</span><span class="sxs-lookup"><span data-stu-id="a89e0-123">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="a89e0-124">Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a89e0-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a89e0-125">Encontrará más ejemplos de scripts de Azure PowerShell de máquina virtual en la [documentación sobre máquinas virtuales Windows de Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a89e0-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>