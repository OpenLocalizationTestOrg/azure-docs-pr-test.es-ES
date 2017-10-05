---
title: "Ejemplo de script de Azure PowerShell: copiar (mover) instantánea de un disco administrado en la misma suscripción o en otra | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: copiar (mover) instantánea de un disco administrado en la misma suscripción o en otra"
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
ms.openlocfilehash: f7b4869669a2c5e840f9bd384dcd6d6096ba58e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="2ae1a-103">Copiar instantánea de un disco administrado en la misma suscripción o en otra con PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ae1a-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="2ae1a-104">Este script crea una copia de una instantánea en la misma suscripción o en otra.</span><span class="sxs-lookup"><span data-stu-id="2ae1a-104">This script creates a copy of a snapshot in the same same subscription or different subscription.</span></span> <span data-ttu-id="2ae1a-105">Use este script para mover una instantánea a otra suscripción para la retención de datos.</span><span class="sxs-lookup"><span data-stu-id="2ae1a-105">Use this script to move a snapshot to different subscription for data retention.</span></span> <span data-ttu-id="2ae1a-106">El almacenamiento de instantáneas en otra suscripción es una medida de protección frente a la eliminación accidental de las instantáneas de la suscripción principal.</span><span class="sxs-lookup"><span data-stu-id="2ae1a-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2ae1a-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2ae1a-107">Sample script</span></span>

<span data-ttu-id="2ae1a-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copiar instantánea")]</span><span class="sxs-lookup"><span data-stu-id="2ae1a-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="2ae1a-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="2ae1a-109">Script explanation</span></span>

<span data-ttu-id="2ae1a-110">Este script usa los siguientes comandos para crear una instantánea en la suscripción de destino mediante el identificador de la instantánea de origen.</span><span class="sxs-lookup"><span data-stu-id="2ae1a-110">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="2ae1a-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="2ae1a-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2ae1a-112">Comando</span><span class="sxs-lookup"><span data-stu-id="2ae1a-112">Command</span></span> | <span data-ttu-id="2ae1a-113">Notas</span><span class="sxs-lookup"><span data-stu-id="2ae1a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2ae1a-114">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="2ae1a-114">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="2ae1a-115">Crea la configuración de instantánea que se usa para la creación de instantáneas.</span><span class="sxs-lookup"><span data-stu-id="2ae1a-115">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="2ae1a-116">Incluye el identificador de recurso de la instantánea principal y una ubicación igual a la de la instantánea principal.</span><span class="sxs-lookup"><span data-stu-id="2ae1a-116">It includes the resource Id of the parent snapshot and location that is same as the parent snapshot.</span></span>  |
| [<span data-ttu-id="2ae1a-117">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="2ae1a-117">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="2ae1a-118">Crea una instantánea mediante la configuración de instantánea, el nombre de instantánea y el nombre de grupo de recursos pasados como parámetros.</span><span class="sxs-lookup"><span data-stu-id="2ae1a-118">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="2ae1a-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2ae1a-119">Next steps</span></span>

[<span data-ttu-id="2ae1a-120">Crear una máquina virtual a partir de una instantánea</span><span class="sxs-lookup"><span data-stu-id="2ae1a-120">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="2ae1a-121">Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2ae1a-121">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2ae1a-122">Encontrará más ejemplos de scripts de Azure PowerShell de máquina virtual en la [documentación sobre máquinas virtuales Windows de Azure](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2ae1a-122">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>