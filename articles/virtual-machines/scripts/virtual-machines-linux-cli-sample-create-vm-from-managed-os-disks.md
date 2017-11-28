---
title: "Script de CLI de Azure de ejemplo: creación de una máquina virtual conectando un disco administrado como disco del SO | Microsoft Docs"
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
ms.openlocfilehash: 18eefee869b243b35d4426c226eff5f48cd490a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="01bd7-103">Creación de una máquina virtual con un disco del SO administrado mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="01bd7-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="01bd7-104">Este script crea una máquina virtual conectando un disco administrado como disco del SO.</span><span class="sxs-lookup"><span data-stu-id="01bd7-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="01bd7-105">Use este script en los anteriores escenarios:</span><span class="sxs-lookup"><span data-stu-id="01bd7-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="01bd7-106">Creación de una máquina virtual desde un disco del SO administrado que se copió desde un disco administrado de otra suscripción</span><span class="sxs-lookup"><span data-stu-id="01bd7-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="01bd7-107">Creación de una máquina virtual desde un disco administrado que se creó a partir de un archivo de disco duro virtual especializado</span><span class="sxs-lookup"><span data-stu-id="01bd7-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="01bd7-108">Creación de una máquina virtual desde un disco del SO administrado que se creó a partir de una instantánea</span><span class="sxs-lookup"><span data-stu-id="01bd7-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="01bd7-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="01bd7-109">Sample script</span></span>

<span data-ttu-id="01bd7-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Creación de una máquina virtual desde un disco administrado")]</span><span class="sxs-lookup"><span data-stu-id="01bd7-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="01bd7-111">Limpieza de la implementación</span><span class="sxs-lookup"><span data-stu-id="01bd7-111">Clean up deployment</span></span> 

<span data-ttu-id="01bd7-112">Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="01bd7-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="01bd7-113">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="01bd7-113">Script explanation</span></span>

<span data-ttu-id="01bd7-114">Este script usa los siguientes comandos para obtener las propiedades del disco administrado, conectar un disco administrado a una nueva máquina virtual y crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01bd7-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="01bd7-115">Cada elemento de la tabla incluye vínculos a la documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="01bd7-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="01bd7-116">Comando</span><span class="sxs-lookup"><span data-stu-id="01bd7-116">Command</span></span> | <span data-ttu-id="01bd7-117">Notas</span><span class="sxs-lookup"><span data-stu-id="01bd7-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01bd7-118">az disk show</span><span class="sxs-lookup"><span data-stu-id="01bd7-118">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="01bd7-119">Obtiene propiedades del disco administrado mediante el nombre del disco y el nombre del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="01bd7-119">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="01bd7-120">La propiedad de identificador se utiliza para conectar un disco administrado a una nueva máquina virtual</span><span class="sxs-lookup"><span data-stu-id="01bd7-120">Id property is used to attach a managed disk to a new VM</span></span> |
| [<span data-ttu-id="01bd7-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="01bd7-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="01bd7-122">Crea una máquina virtual con un disco del SO administrado.</span><span class="sxs-lookup"><span data-stu-id="01bd7-122">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="01bd7-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="01bd7-123">Next steps</span></span>

<span data-ttu-id="01bd7-124">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01bd7-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="01bd7-125">Encontrará más ejemplos de scripts de la CLI de máquina virtual en la [documentación sobre máquinas virtuales Linux de Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01bd7-125">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
