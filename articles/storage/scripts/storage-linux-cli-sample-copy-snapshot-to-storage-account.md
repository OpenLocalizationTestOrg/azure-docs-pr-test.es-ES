---
title: "Ejemplo de script de CLI de Azure: exportación o copia de instantánea como un VHD a una cuenta de almacenamiento en otra región | Microsoft Docs"
description: "Ejemplo de script de CLI de Azure: exportación o copia de instantánea como un VHD a una cuenta de almacenamiento en misma suscripción o en una diferente"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: fafb74af5f02f74036c770934c5e33f1b8a5593e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-cli"></a><span data-ttu-id="8ee71-103">Exportación o copia de una instantánea administrada como un VHD a una cuenta de almacenamiento en una región diferente con CLI</span><span class="sxs-lookup"><span data-stu-id="8ee71-103">Export/Copy managed snapshots as VHD to a storage account in different region with CLI</span></span>

<span data-ttu-id="8ee71-104">Este script exporta una instantánea administrada a una cuenta de almacenamiento en una región diferente.</span><span class="sxs-lookup"><span data-stu-id="8ee71-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="8ee71-105">En primer lugar, genera el identificador URI de SAS de la instantánea y, luego, lo usa para copiarlo en una cuenta de almacenamiento en una región diferente.</span><span class="sxs-lookup"><span data-stu-id="8ee71-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="8ee71-106">Use este script para mantener una copia de seguridad de los discos administrados en una región distinta para la recuperación ante desastres.</span><span class="sxs-lookup"><span data-stu-id="8ee71-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8ee71-107">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8ee71-107">Sample script</span></span>

<span data-ttu-id="8ee71-108">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copiar instantánea")]</span><span class="sxs-lookup"><span data-stu-id="8ee71-108">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="8ee71-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="8ee71-109">Script explanation</span></span>

<span data-ttu-id="8ee71-110">Este script usa los siguientes comandos para generar el identificador URI de SAS para una instantánea administrada y copia la instantánea en una cuenta de almacenamiento usando el URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="8ee71-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="8ee71-111">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="8ee71-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8ee71-112">Comando</span><span class="sxs-lookup"><span data-stu-id="8ee71-112">Command</span></span> | <span data-ttu-id="8ee71-113">Notas</span><span class="sxs-lookup"><span data-stu-id="8ee71-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8ee71-114">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="8ee71-114">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="8ee71-115">Genera la SAS de solo lectura que se usa para copiar el archivo de VHD subyacente a una cuenta de almacenamiento o descargarlo localmente.</span><span class="sxs-lookup"><span data-stu-id="8ee71-115">Generates read-only SAS that is used to copy underlying VHD file to a storage account or download it to on-premises</span></span>  |
| [<span data-ttu-id="8ee71-116">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="8ee71-116">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="8ee71-117">Copia un blob de forma asincrónica desde una cuenta de almacenamiento a otra.</span><span class="sxs-lookup"><span data-stu-id="8ee71-117">Copies a blob asynchronously from one storage account to another</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8ee71-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8ee71-118">Next steps</span></span>

[<span data-ttu-id="8ee71-119">Crear un disco administrado a partir de un VHD</span><span class="sxs-lookup"><span data-stu-id="8ee71-119">Create a managed disk from a VHD</span></span>](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="8ee71-120">Crear una máquina virtual desde un disco administrado</span><span class="sxs-lookup"><span data-stu-id="8ee71-120">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="8ee71-121">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8ee71-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8ee71-122">Encontrará más ejemplos de scripts de la CLI de máquina virtual y discos administrados en la [documentación de Azure sobre máquinas virtuales Linux](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ee71-122">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
