---
title: "Ejemplo de Script de PowerShell: instantánea de copia (movimiento) de un disco administrado toosame o de otra suscripción aaaAzure | Documentos de Microsoft"
description: "Ejemplo de Script de PowerShell Azure - instantánea de copia (movimiento) de un disco administrado toosame o de otra suscripción"
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 7a3565356f13cb93759dec7ef9d0357e04c3410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="63c24-103">Copiar instantánea de un disco administrado en la misma suscripción o en otra con PowerShell</span><span class="sxs-lookup"><span data-stu-id="63c24-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="63c24-104">Este script crea una copia de una instantánea en hello mismo misma suscripción u otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="63c24-104">This script creates a copy of a snapshot in hello same same subscription or different subscription.</span></span> <span data-ttu-id="63c24-105">Utilice este toomove una suscripción de instantánea toodifferent de secuencia de comandos para la retención de datos.</span><span class="sxs-lookup"><span data-stu-id="63c24-105">Use this script toomove a snapshot toodifferent subscription for data retention.</span></span> <span data-ttu-id="63c24-106">El almacenamiento de instantáneas en otra suscripción es una medida de protección frente a la eliminación accidental de las instantáneas de la suscripción principal.</span><span class="sxs-lookup"><span data-stu-id="63c24-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="63c24-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="63c24-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="63c24-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="63c24-108">Script explanation</span></span>

<span data-ttu-id="63c24-109">Este script utiliza después comandos toocreate una instantánea en la suscripción de destino de hello con Hola Id. de instantánea de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="63c24-109">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="63c24-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="63c24-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="63c24-111">Comando</span><span class="sxs-lookup"><span data-stu-id="63c24-111">Command</span></span> | <span data-ttu-id="63c24-112">Notas</span><span class="sxs-lookup"><span data-stu-id="63c24-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="63c24-113">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="63c24-113">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="63c24-114">Crea la configuración de instantánea que se usa para la creación de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="63c24-114">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="63c24-115">Incluye recursos de hello Id. de instantánea de hello primaria y la ubicación que sea igual a la instantánea primaria de Hola.</span><span class="sxs-lookup"><span data-stu-id="63c24-115">It includes hello resource Id of hello parent snapshot and location that is same as hello parent snapshot.</span></span>  |
| [<span data-ttu-id="63c24-116">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="63c24-116">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="63c24-117">Crea una instantánea mediante la configuración de instantánea, el nombre de instantánea y el nombre de grupo de recursos pasados como parámetros.</span><span class="sxs-lookup"><span data-stu-id="63c24-117">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="63c24-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="63c24-118">Next steps</span></span>

[<span data-ttu-id="63c24-119">Crear una máquina virtual a partir de una instantánea</span><span class="sxs-lookup"><span data-stu-id="63c24-119">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="63c24-120">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="63c24-120">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="63c24-121">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="63c24-121">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
