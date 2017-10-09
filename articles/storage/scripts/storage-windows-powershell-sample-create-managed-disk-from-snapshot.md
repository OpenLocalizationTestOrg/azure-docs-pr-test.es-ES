---
title: "aaaAzure ejemplo de Script de PowerShell: crear un disco administrado desde una instantánea | Documentos de Microsoft"
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
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="9d50f-103">Creación de un disco administrado a partir de una instantánea con PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d50f-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="9d50f-104">Este script crea un disco administrado a partir de una instantánea.</span><span class="sxs-lookup"><span data-stu-id="9d50f-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="9d50f-105">Usar toorestore una máquina virtual de las instantáneas de discos de sistema operativo y los datos.</span><span class="sxs-lookup"><span data-stu-id="9d50f-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="9d50f-106">Cree los discos de sistema operativo y datos a partir de las instantáneas correspondientes y, luego, cree una nueva máquina virtual conectando los discos administrados.</span><span class="sxs-lookup"><span data-stu-id="9d50f-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="9d50f-107">También puede restaurar los discos de datos de una máquina virtual existente conectando los discos de datos creados a partir de las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="9d50f-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9d50f-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9d50f-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="9d50f-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="9d50f-109">Script explanation</span></span>

<span data-ttu-id="9d50f-110">Este script usará los siguientes comandos toocreate un disco administrado desde una instantánea.</span><span class="sxs-lookup"><span data-stu-id="9d50f-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="9d50f-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="9d50f-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9d50f-112">Comando</span><span class="sxs-lookup"><span data-stu-id="9d50f-112">Command</span></span> | <span data-ttu-id="9d50f-113">Notas</span><span class="sxs-lookup"><span data-stu-id="9d50f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9d50f-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="9d50f-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="9d50f-115">Obtiene las propiedades de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="9d50f-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="9d50f-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="9d50f-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="9d50f-117">Crea la configuración de disco que se usa para la creación del disco.</span><span class="sxs-lookup"><span data-stu-id="9d50f-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="9d50f-118">Incluye recursos de hello identificador de instantánea primaria de hello, ubicación que sea igual a la ubicación de Hola de tipo de almacenamiento de instantáneas y Hola primario.</span><span class="sxs-lookup"><span data-stu-id="9d50f-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="9d50f-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="9d50f-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="9d50f-120">Crea un disco mediante la configuración de disco, el nombre del disco y el nombre del grupo de recursos que se pasan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="9d50f-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="9d50f-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d50f-121">Next steps</span></span>

[<span data-ttu-id="9d50f-122">Crear una máquina virtual a partir de un disco administrado</span><span class="sxs-lookup"><span data-stu-id="9d50f-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="9d50f-123">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9d50f-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9d50f-124">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d50f-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
