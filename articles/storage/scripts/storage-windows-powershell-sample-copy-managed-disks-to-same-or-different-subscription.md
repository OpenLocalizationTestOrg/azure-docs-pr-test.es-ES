---
title: "aaaAzure ejemplo de Script de PowerShell - copia (movimiento) administrado toosame de discos u otra suscripción | Documentos de Microsoft"
description: "Ejemplo de Script de PowerShell Azure - toosame de discos de copia (movimiento) administrado o de otra suscripción"
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
ms.openlocfilehash: 5a92118e10a14615e5b1713f1b90188b37b05305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="97ced-103">Copia administrada discos Hola mismo suscripción u otra suscripción con PowerShell</span><span class="sxs-lookup"><span data-stu-id="97ced-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="97ced-104">Este script crea una copia de un disco administrado existente en hello misma suscripción u otra suscripción.</span><span class="sxs-lookup"><span data-stu-id="97ced-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="97ced-105">Hello nuevo disco se crea en Hola misma región como elemento primario de hello administrados disco.</span><span class="sxs-lookup"><span data-stu-id="97ced-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="97ced-106">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="97ced-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="97ced-107">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="97ced-107">Script explanation</span></span>

<span data-ttu-id="97ced-108">Esta secuencia de comandos que se utiliza después de comandos toocreate un nuevo disco administrado en la suscripción de destino de hello con Hola Id. de origen de hello administra el disco.</span><span class="sxs-lookup"><span data-stu-id="97ced-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="97ced-109">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="97ced-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="97ced-110">Comando</span><span class="sxs-lookup"><span data-stu-id="97ced-110">Command</span></span> | <span data-ttu-id="97ced-111">Notas</span><span class="sxs-lookup"><span data-stu-id="97ced-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="97ced-112">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="97ced-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="97ced-113">Crea la configuración de disco que se usa para la creación del disco.</span><span class="sxs-lookup"><span data-stu-id="97ced-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="97ced-114">Incluye recursos de hello Id. de disco primario con hello y la ubicación que sea igual a la ubicación de Hola de disco primario.</span><span class="sxs-lookup"><span data-stu-id="97ced-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="97ced-115">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="97ced-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="97ced-116">Crea un disco mediante la configuración de disco, el nombre del disco y el nombre del grupo de recursos que se pasan como parámetros.</span><span class="sxs-lookup"><span data-stu-id="97ced-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="97ced-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97ced-117">Next steps</span></span>

[<span data-ttu-id="97ced-118">Crear una máquina virtual a partir de un disco administrado</span><span class="sxs-lookup"><span data-stu-id="97ced-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="97ced-119">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="97ced-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="97ced-120">Ejemplos de secuencias de comandos de PowerShell de máquina virtual adicional pueden encontrarse en hello [documentación de la máquina virtual de Windows Azure](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97ced-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
