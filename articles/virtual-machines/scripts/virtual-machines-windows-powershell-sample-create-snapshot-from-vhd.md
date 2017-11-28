---
title: "aaaAzure ejemplo de Script de PowerShell: crear una instantánea de un disco duro virtual toocreate varios discos administrados idénticos en pequeña cantidad de tiempo | Documentos de Microsoft"
description: "Script de Azure PowerShell de ejemplo: crear una instantánea de un disco duro virtual toocreate varios discos administrados idénticos en pequeña cantidad de tiempo"
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
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="834ac-103">Crear una instantánea de un disco duro virtual toocreate varios discos administrados idénticos en pequeña cantidad de tiempo con PowerShell</span><span class="sxs-lookup"><span data-stu-id="834ac-103">Create a snapshot from a VHD toocreate multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="834ac-104">Este script crea una instantánea desde un archivo VHD en una cuenta de almacenamiento en una misma suscripción o en una suscripción distinta.</span><span class="sxs-lookup"><span data-stu-id="834ac-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="834ac-105">Use este tooimport una instantánea de tooa de disco duro virtual (no generalizado/preparada con Sysprep) especializada de script y use después Hola instantánea toocreate varios discos administrados idénticos en poco tiempo.</span><span class="sxs-lookup"><span data-stu-id="834ac-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD tooa snapshot and then use hello snapshot toocreate multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="834ac-106">Además, usarlo tooimport una instantánea de tooa de disco duro virtual de datos y, a continuación, Hola instantánea toocreate varios discos administrados en poco tiempo.</span><span class="sxs-lookup"><span data-stu-id="834ac-106">Also, use it tooimport a data VHD tooa snapshot and then use hello snapshot toocreate multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="834ac-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="834ac-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="834ac-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="834ac-108">Script explanation</span></span>

<span data-ttu-id="834ac-109">Este script usará los siguientes comandos toocreate un disco administrado desde un disco duro virtual en otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="834ac-109">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="834ac-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="834ac-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="834ac-111">Comando</span><span class="sxs-lookup"><span data-stu-id="834ac-111">Command</span></span> | <span data-ttu-id="834ac-112">Notas</span><span class="sxs-lookup"><span data-stu-id="834ac-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="834ac-113">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="834ac-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="834ac-114">Crea la configuración de disco que se usa para la creación del disco.</span><span class="sxs-lookup"><span data-stu-id="834ac-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="834ac-115">Incluye el tipo de almacenamiento, la ubicación, Id. de cuenta de almacenamiento de Hola donde se almacena el VHD primario de Hola de recurso y URI de VHD de VHD primario de Hola.</span><span class="sxs-lookup"><span data-stu-id="834ac-115">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, and VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="834ac-116">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="834ac-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="834ac-117">Crea un disco mediante la configuración de disco, el nombre del disco y el nombre del grupo de recursos que se pasan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="834ac-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="834ac-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="834ac-118">Next steps</span></span>

[<span data-ttu-id="834ac-119">Creación de un disco administrado a partir de una instantánea</span><span class="sxs-lookup"><span data-stu-id="834ac-119">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="834ac-120">Creación de una máquina virtual conectando un disco administrado como disco del SO</span><span class="sxs-lookup"><span data-stu-id="834ac-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="834ac-121">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="834ac-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="834ac-122">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="834ac-122">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
