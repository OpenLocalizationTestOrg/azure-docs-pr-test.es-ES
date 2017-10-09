---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una máquina virtual desde una instantánea | Documentos de Microsoft"
description: "Ejemplo de script de la CLI de Azure: creación de una máquina virtual a partir de una instantánea"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="19b4e-103">Creación de una máquina virtual a partir de una instantánea con la CLI</span><span class="sxs-lookup"><span data-stu-id="19b4e-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="19b4e-104">Este script crea una máquina virtual a partir de una instantánea de un disco del SO.</span><span class="sxs-lookup"><span data-stu-id="19b4e-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="19b4e-105">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="19b4e-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="19b4e-106">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="19b4e-106">Clean up deployment</span></span> 

<span data-ttu-id="19b4e-107">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="19b4e-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="19b4e-108">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="19b4e-108">Script explanation</span></span>

<span data-ttu-id="19b4e-109">Este script usa Hola después comandos toocreate un disco administrado, la máquina virtual, y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="19b4e-109">This script uses hello following commands toocreate a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="19b4e-110">Cada comando de documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="19b4e-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="19b4e-111">Comando</span><span class="sxs-lookup"><span data-stu-id="19b4e-111">Command</span></span> | <span data-ttu-id="19b4e-112">Notas</span><span class="sxs-lookup"><span data-stu-id="19b4e-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="19b4e-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="19b4e-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="19b4e-114">Obtiene instantáneas mediante el nombre de la instantánea y el del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="19b4e-114">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="19b4e-115">Propiedad de Id. de hello devuelve el objeto es toocreate usa un disco administrado.</span><span class="sxs-lookup"><span data-stu-id="19b4e-115">Id property of hello returned object is used toocreate a managed disk.</span></span>  |
| [<span data-ttu-id="19b4e-116">az disk create</span><span class="sxs-lookup"><span data-stu-id="19b4e-116">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="19b4e-117">Crea discos administrados a partir de una instantánea usando el identificador de las instantáneas, el nombre del disco, el tipo de almacenamiento y el tamaño.</span><span class="sxs-lookup"><span data-stu-id="19b4e-117">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="19b4e-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="19b4e-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="19b4e-119">Crea una máquina virtual con un disco del SO administrado.</span><span class="sxs-lookup"><span data-stu-id="19b4e-119">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="19b4e-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="19b4e-120">Next steps</span></span>

<span data-ttu-id="19b4e-121">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="19b4e-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="19b4e-122">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="19b4e-122">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
