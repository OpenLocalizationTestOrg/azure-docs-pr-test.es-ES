---
title: "Script de Azure PowerShell de ejemplo: crear un disco administrado desde un archivo VHD en una cuenta de almacenamiento en la misma o distinta suscripción | Microsoft Docs"
description: "Script de Azure PowerShell de ejemplo: crear un disco administrado desde un archivo VHD en una cuenta de almacenamiento en la misma o distinta suscripción"
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
ms.openlocfilehash: b9c3d2e8dbf5caa525f82955aceb615cb1c28e93
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="80e17-103">Creación de un disco administrado desde un archivo VHD en una cuenta de almacenamiento en la misma o distinta suscripción con PowerShell</span><span class="sxs-lookup"><span data-stu-id="80e17-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="80e17-104">Este script crea un disco administrado desde un archivo VHD en una cuenta de almacenamiento en la misma o distinta suscripción.</span><span class="sxs-lookup"><span data-stu-id="80e17-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="80e17-105">Utilice este script para importar un archivo VHD especializado (no generalizado o preparado con sysprep) a un disco de sistema operativo administrado para crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80e17-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="80e17-106">También puede utilizarlo para importar datos de un archivo VHD a un disco de datos administrado.</span><span class="sxs-lookup"><span data-stu-id="80e17-106">Also, use it to import a data VHD to managed data disk.</span></span> 

<span data-ttu-id="80e17-107">No debe crear varios discos administrados idénticos desde un archivo VHD en un período de tiempo corto.</span><span class="sxs-lookup"><span data-stu-id="80e17-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="80e17-108">Para crear discos administrados desde un archivo VHD, se crear una instantánea de blob del archivo VHD y, a continuación, se utiliza para crear discos administrados.</span><span class="sxs-lookup"><span data-stu-id="80e17-108">To create managed disks from a vhd file, blob snapshot of the vhd file is created and then it is used to create managed disks.</span></span> <span data-ttu-id="80e17-109">Solo se puede crear una instantánea de blob en un minuto, lo que provoca errores de creación de disco debido a la limitación.</span><span class="sxs-lookup"><span data-stu-id="80e17-109">Only one blob snapshot can be created in a minute that causes disk creation failures due to throttling.</span></span> <span data-ttu-id="80e17-110">Para evitar esta limitación, cree una [instantánea administrada desde el archivo VHD](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) y, a continuación, use la instantánea administrada para crear varios discos administrados en un corto período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="80e17-110">To avoid this throttling, create a [managed snapshot from the vhd file](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use the managed snapshot to create multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="80e17-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="80e17-111">Sample script</span></span>

<span data-ttu-id="80e17-112">[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Creación de un disco administrado desde un archivo VHD")]</span><span class="sxs-lookup"><span data-stu-id="80e17-112">[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="80e17-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="80e17-113">Script explanation</span></span>

<span data-ttu-id="80e17-114">Este script utiliza los comandos siguientes para crear un disco administrado desde un archivo VHD en una suscripción distinta.</span><span class="sxs-lookup"><span data-stu-id="80e17-114">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="80e17-115">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="80e17-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="80e17-116">Comando</span><span class="sxs-lookup"><span data-stu-id="80e17-116">Command</span></span> | <span data-ttu-id="80e17-117">Notas</span><span class="sxs-lookup"><span data-stu-id="80e17-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="80e17-118">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="80e17-118">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="80e17-119">Crea la configuración de disco que se usa para la creación del disco.</span><span class="sxs-lookup"><span data-stu-id="80e17-119">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="80e17-120">Incluye el tipo de almacenamiento, ubicación, identificador de recurso de la cuenta de almacenamiento donde se almacena el archivo VHD primario, identificador URI del archivo VHD primario.</span><span class="sxs-lookup"><span data-stu-id="80e17-120">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="80e17-121">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="80e17-121">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="80e17-122">Crea un disco mediante la configuración de disco, el nombre del disco y el nombre del grupo de recursos que se pasan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="80e17-122">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80e17-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="80e17-123">Next steps</span></span>

[<span data-ttu-id="80e17-124">Creación de una máquina virtual conectando un disco administrado como disco del SO</span><span class="sxs-lookup"><span data-stu-id="80e17-124">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="80e17-125">Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80e17-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="80e17-126">Encontrará más ejemplos de scripts de Azure PowerShell de máquina virtual en la [documentación sobre máquinas virtuales Windows de Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80e17-126">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>