---
title: "Ejemplo de secuencia de comandos de CLI - aaaAzure crear una máquina virtual si se adjunta un disco como disco del sistema operativo administrado | Documentos de Microsoft"
description: "Script de CLI de Azure de ejemplo: creación de una máquina virtual conectando un disco administrado como disco del SO"
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="2d004-103">Creación de una máquina virtual con un disco del SO administrado mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="2d004-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="2d004-104">Este script crea una máquina virtual conectando un disco administrado como disco del SO.</span><span class="sxs-lookup"><span data-stu-id="2d004-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="2d004-105">Use este script en los anteriores escenarios:</span><span class="sxs-lookup"><span data-stu-id="2d004-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="2d004-106">Creación de una máquina virtual desde un disco del SO administrado que se copió desde un disco administrado de otra suscripción</span><span class="sxs-lookup"><span data-stu-id="2d004-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="2d004-107">Creación de una máquina virtual desde un disco administrado que se creó a partir de un archivo de disco duro virtual especializado</span><span class="sxs-lookup"><span data-stu-id="2d004-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="2d004-108">Creación de una máquina virtual desde un disco del SO administrado que se creó a partir de una instantánea</span><span class="sxs-lookup"><span data-stu-id="2d004-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2d004-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2d004-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2d004-110">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="2d004-110">Clean up deployment</span></span> 

<span data-ttu-id="2d004-111">Ejecute hello después el grupo de recursos de comando tooremove hello, la VM y todos ellos relacionados con recursos.</span><span class="sxs-lookup"><span data-stu-id="2d004-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2d004-112">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="2d004-112">Script explanation</span></span>

<span data-ttu-id="2d004-113">Este script utiliza Hola comandos tooget administrado disco propiedades siguientes, adjuntar un disco administrado tooa nueva máquina virtual y cree una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2d004-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="2d004-114">Cada elemento de la documentación específica de hello tabla vínculos toocommand.</span><span class="sxs-lookup"><span data-stu-id="2d004-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2d004-115">Comando</span><span class="sxs-lookup"><span data-stu-id="2d004-115">Command</span></span> | <span data-ttu-id="2d004-116">Notas</span><span class="sxs-lookup"><span data-stu-id="2d004-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2d004-117">az disk show</span><span class="sxs-lookup"><span data-stu-id="2d004-117">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="2d004-118">Obtiene propiedades del disco administrado mediante el nombre del disco y el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d004-118">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="2d004-119">Propiedad ID es tooattach usa un disco administrado tooa nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2d004-119">Id property is used tooattach a managed disk tooa new VM</span></span> |
| [<span data-ttu-id="2d004-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="2d004-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2d004-121">Crea una máquina virtual con un disco del SO administrado.</span><span class="sxs-lookup"><span data-stu-id="2d004-121">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="2d004-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2d004-122">Next steps</span></span>

<span data-ttu-id="2d004-123">Para obtener más información sobre Hola CLI de Azure, consulte [documentación de Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2d004-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2d004-124">Ejemplos de secuencias de comandos CLI de máquina virtual adicional pueden encontrarse en hello [documentación de Azure VM de Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2d004-124">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
