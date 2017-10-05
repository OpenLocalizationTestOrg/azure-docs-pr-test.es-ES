---
title: "Ejemplo de script de Azure PowerShell: creación de una instantánea desde un VHD para crear varios discos administrados idénticos en poco tiempo | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: creación de una instantánea desde un VHD para crear varios discos administrados idénticos en poco tiempo"
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
ms.openlocfilehash: 8588a33a1f0b4cce0059a40239301587cdc28920
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-snapshot-from-a-vhd-to-create-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="de066-103">Creación de una instantánea desde un VHD para crear varios discos administrados idénticos en poco tiempo con PowerShell</span><span class="sxs-lookup"><span data-stu-id="de066-103">Create a snapshot from a VHD to create multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="de066-104">Este script crea una instantánea desde un archivo VHD en una cuenta de almacenamiento en una misma suscripción o en una suscripción distinta.</span><span class="sxs-lookup"><span data-stu-id="de066-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="de066-105">Use este script para importar un VHD especializado (no generalizado ni preparado con SysPrep) a una instantánea y luego usar esta instantánea para crear varios discos administrados idénticos en poco tiempo.</span><span class="sxs-lookup"><span data-stu-id="de066-105">Use this script to import a specialized (not generalized/sysprepped) VHD to a snapshot and then use the snapshot to create multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="de066-106">Además, úsela para importar un VHD de datos a una instantánea y luego use esta instantánea para crear varios discos administrados en poco tiempo.</span><span class="sxs-lookup"><span data-stu-id="de066-106">Also, use it to import a data VHD to a snapshot and then use the snapshot to create multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="de066-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="de066-107">Sample script</span></span>

<span data-ttu-id="de066-108">[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Creación de instantánea desde VHD")]</span><span class="sxs-lookup"><span data-stu-id="de066-108">[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="de066-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="de066-109">Script explanation</span></span>

<span data-ttu-id="de066-110">Este script utiliza los comandos siguientes para crear un disco administrado desde un archivo VHD en una suscripción distinta.</span><span class="sxs-lookup"><span data-stu-id="de066-110">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="de066-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="de066-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="de066-112">Comando</span><span class="sxs-lookup"><span data-stu-id="de066-112">Command</span></span> | <span data-ttu-id="de066-113">Notas</span><span class="sxs-lookup"><span data-stu-id="de066-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="de066-114">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="de066-114">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="de066-115">Crea la configuración de disco que se usa para la creación del disco.</span><span class="sxs-lookup"><span data-stu-id="de066-115">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="de066-116">Incluye tipo de almacenamiento, ubicación, identificador de recurso de la cuenta de almacenamiento donde se almacena el VHD principal y el URI de VHD del VHD principal.</span><span class="sxs-lookup"><span data-stu-id="de066-116">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, and VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="de066-117">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="de066-117">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="de066-118">Crea un disco mediante la configuración de disco, el nombre del disco y el nombre del grupo de recursos que se pasan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="de066-118">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="de066-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="de066-119">Next steps</span></span>

[<span data-ttu-id="de066-120">Creación de un disco administrado a partir de una instantánea</span><span class="sxs-lookup"><span data-stu-id="de066-120">Create a managed disk from snapshot</span></span>](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="de066-121">Creación de una máquina virtual conectando un disco administrado como disco del SO</span><span class="sxs-lookup"><span data-stu-id="de066-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="de066-122">Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="de066-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="de066-123">Encontrará más ejemplos de scripts de Azure PowerShell de máquina virtual en la [documentación sobre máquinas virtuales Windows de Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="de066-123">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>