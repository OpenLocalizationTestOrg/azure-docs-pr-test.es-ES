---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear un disco administrado desde una instantánea | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: creación de un disco administrado a partir de una instantánea"
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
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="534c4-103">Creación de un disco administrado a partir de una instantánea con CLI</span><span class="sxs-lookup"><span data-stu-id="534c4-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="534c4-104">Este script crea un disco administrado a partir de una instantánea.</span><span class="sxs-lookup"><span data-stu-id="534c4-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="534c4-105">Usar toorestore una máquina virtual de las instantáneas de discos de sistema operativo y los datos.</span><span class="sxs-lookup"><span data-stu-id="534c4-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="534c4-106">Cree los discos de sistema operativo y datos a partir de las instantáneas correspondientes y, luego, cree una nueva máquina virtual conectando los discos administrados.</span><span class="sxs-lookup"><span data-stu-id="534c4-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="534c4-107">También puede restaurar los discos de datos de una máquina virtual existente conectando los discos de datos creados a partir de las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="534c4-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="534c4-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="534c4-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="534c4-109">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="534c4-109">Script explanation</span></span>

<span data-ttu-id="534c4-110">Este script usará los siguientes comandos toocreate un disco administrado desde una instantánea.</span><span class="sxs-lookup"><span data-stu-id="534c4-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="534c4-111">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="534c4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="534c4-112">Comando</span><span class="sxs-lookup"><span data-stu-id="534c4-112">Command</span></span> | <span data-ttu-id="534c4-113">Notas</span><span class="sxs-lookup"><span data-stu-id="534c4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="534c4-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="534c4-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="534c4-115">Obtiene todas las propiedades de Hola de una instantánea mediante el nombre de Hola y propiedades de grupo de recursos de instantánea de Hola.</span><span class="sxs-lookup"><span data-stu-id="534c4-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="534c4-116">Propiedad ID es toocreate usado de disco administrado.</span><span class="sxs-lookup"><span data-stu-id="534c4-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="534c4-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="534c4-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="534c4-118">Crea un disco administrado usando un identificador de una instantánea administrada</span><span class="sxs-lookup"><span data-stu-id="534c4-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="534c4-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="534c4-119">Next steps</span></span>

[<span data-ttu-id="534c4-120">Creación de una máquina virtual conectando un disco administrado como disco del SO</span><span class="sxs-lookup"><span data-stu-id="534c4-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="534c4-121">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="534c4-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="534c4-122">Máquina virtual adicional y ejemplos de secuencias de comandos CLI de discos administrados pueden encontrarse en hello [documentación de Azure VM de Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="534c4-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
