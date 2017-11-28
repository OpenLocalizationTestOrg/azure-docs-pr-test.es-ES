---
title: "Ejemplo de Script de PowerShell: instantánea de exportación/copiar como cuenta de almacenamiento de disco duro virtual tooa en otra región aaaAzure | Documentos de Microsoft"
description: "Ejemplo de Script de PowerShell Azure - instantánea de exportación/copiar como cuenta de almacenamiento de tooa de disco duro virtual en la misma región diferente"
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="bf7e2-103">Exportación o copia administrado instantáneas como cuenta de almacenamiento de tooa de disco duro virtual en una región distinta con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf7e2-103">Export/Copy managed snapshots as VHD tooa storage account in different region with PowerShell</span></span>

<span data-ttu-id="bf7e2-104">Este script exporta una cuenta de almacenamiento de instantáneas administrado tooa en otra región.</span><span class="sxs-lookup"><span data-stu-id="bf7e2-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="bf7e2-105">En primer lugar genera Hola URI de SAS de instantánea de hello y, a continuación, usa toocopy se tooa cuenta de almacenamiento en una región diferente.</span><span class="sxs-lookup"><span data-stu-id="bf7e2-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="bf7e2-106">Use esta copia de seguridad de secuencia de comandos toomaintain los discos administrados en una región diferente para la recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="bf7e2-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bf7e2-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="bf7e2-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="bf7e2-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="bf7e2-108">Script explanation</span></span>

<span data-ttu-id="bf7e2-109">Este script utiliza después toogenerate comandos URI de SAS para una administrado hello instantáneas ni copias instantáneas tooa cuenta de almacenamiento con el URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="bf7e2-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="bf7e2-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="bf7e2-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bf7e2-111">Comando</span><span class="sxs-lookup"><span data-stu-id="bf7e2-111">Command</span></span> | <span data-ttu-id="bf7e2-112">Notas</span><span class="sxs-lookup"><span data-stu-id="bf7e2-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bf7e2-113">Grant-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="bf7e2-113">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="bf7e2-114">URI de SAS se genera para una instantánea que sea utilizado toocopy se tooa cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="bf7e2-114">Generates SAS URI for a snapshot that is used toocopy it tooa storage account.</span></span> |
| [<span data-ttu-id="bf7e2-115">New-AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="bf7e2-115">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="bf7e2-116">Crea un contexto de la cuenta de almacenamiento mediante la clave y el nombre de la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="bf7e2-116">Creates a storage account context using hello account name and key.</span></span> <span data-ttu-id="bf7e2-117">Este contexto puede ser operaciones de lectura/escritura tooperform usado en la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="bf7e2-117">This context can be used tooperform read/write operations on hello storage account.</span></span> |
| [<span data-ttu-id="bf7e2-118">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="bf7e2-118">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="bf7e2-119">Copias Hola VHD subyacente de una cuenta de almacenamiento de instantáneas tooa</span><span class="sxs-lookup"><span data-stu-id="bf7e2-119">Copies hello underlying VHD of a snapshot tooa storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bf7e2-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bf7e2-120">Next steps</span></span>

[<span data-ttu-id="bf7e2-121">Crear un disco administrado a partir de un VHD</span><span class="sxs-lookup"><span data-stu-id="bf7e2-121">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="bf7e2-122">Crear una máquina virtual a partir de un disco administrado</span><span class="sxs-lookup"><span data-stu-id="bf7e2-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="bf7e2-123">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bf7e2-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="bf7e2-124">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf7e2-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
