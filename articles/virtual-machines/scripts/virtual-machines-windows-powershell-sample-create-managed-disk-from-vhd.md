---
title: "aaaAzure ejemplo de Script de PowerShell: crear un disco administrado desde un archivo de disco duro virtual en una cuenta de almacenamiento en la misma o distintas suscripción | Documentos de Microsoft"
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
ms.openlocfilehash: 47acff274cdf79d6fc3cd685cda01cad3d14ca8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="56ad2-103">Creación de un disco administrado desde un archivo VHD en una cuenta de almacenamiento en la misma o distinta suscripción con PowerShell</span><span class="sxs-lookup"><span data-stu-id="56ad2-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="56ad2-104">Este script crea un disco administrado desde un archivo VHD en una cuenta de almacenamiento en la misma o distinta suscripción.</span><span class="sxs-lookup"><span data-stu-id="56ad2-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="56ad2-105">Utilice este tooimport script un versión especializada del toocreate de (no generalizado/preparada con Sysprep) VHD toomanaged OS disco una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="56ad2-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="56ad2-106">Además, utilizarlo tooimport un disco de datos de toomanaged de disco duro virtual de datos.</span><span class="sxs-lookup"><span data-stu-id="56ad2-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="56ad2-107">No debe crear varios discos administrados idénticos desde un archivo VHD en un período de tiempo corto.</span><span class="sxs-lookup"><span data-stu-id="56ad2-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="56ad2-108">discos administrados por toocreate desde un archivo de disco duro virtual, se crea la instantánea de blob del archivo de disco duro virtual de hello y, a continuación, resulta discos utilizados toocreate administrado.</span><span class="sxs-lookup"><span data-stu-id="56ad2-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="56ad2-109">Instantánea de solo blob puede crearse en un minuto que provoca errores de creación de disco toothrottling due.</span><span class="sxs-lookup"><span data-stu-id="56ad2-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="56ad2-110">tooavoid esta limitación, cree un [administrado instantánea del archivo de disco duro virtual de hello](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) y, a continuación, use Hola administrados instantánea toocreate varios discos administrados en poco tiempo.</span><span class="sxs-lookup"><span data-stu-id="56ad2-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="56ad2-111">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="56ad2-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="56ad2-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="56ad2-112">Script explanation</span></span>

<span data-ttu-id="56ad2-113">Este script usará los siguientes comandos toocreate un disco administrado desde un disco duro virtual en otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="56ad2-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="56ad2-114">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="56ad2-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="56ad2-115">Comando</span><span class="sxs-lookup"><span data-stu-id="56ad2-115">Command</span></span> | <span data-ttu-id="56ad2-116">Notas</span><span class="sxs-lookup"><span data-stu-id="56ad2-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="56ad2-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="56ad2-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="56ad2-118">Crea la configuración de disco que se usa para la creación del disco.</span><span class="sxs-lookup"><span data-stu-id="56ad2-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="56ad2-119">Incluye el tipo de almacenamiento, ubicación, Id. de cuenta de almacenamiento de Hola donde se almacena el VHD primario de hello, URI de VHD de VHD primario de Hola de recurso.</span><span class="sxs-lookup"><span data-stu-id="56ad2-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="56ad2-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="56ad2-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="56ad2-121">Crea un disco mediante la configuración de disco, el nombre del disco y el nombre del grupo de recursos que se pasan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="56ad2-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="56ad2-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56ad2-122">Next steps</span></span>

[<span data-ttu-id="56ad2-123">Creación de una máquina virtual conectando un disco administrado como disco del SO</span><span class="sxs-lookup"><span data-stu-id="56ad2-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="56ad2-124">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="56ad2-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="56ad2-125">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56ad2-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>