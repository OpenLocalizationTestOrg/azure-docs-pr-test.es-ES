---
title: "Ejemplo de script de la CLI de Azure: creación de un disco administrado a partir de una instantánea | Microsoft Docs"
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
ms.openlocfilehash: 68e17ae9e5d82da7f9be9d36e3e2324a2aeadbc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="11f68-103">Creación de un disco administrado a partir de una instantánea con CLI</span><span class="sxs-lookup"><span data-stu-id="11f68-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="11f68-104">Este script crea un disco administrado a partir de una instantánea.</span><span class="sxs-lookup"><span data-stu-id="11f68-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="11f68-105">Úselo para restaurar una máquina virtual a partir de las instantáneas de discos de sistema operativo y datos.</span><span class="sxs-lookup"><span data-stu-id="11f68-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="11f68-106">Cree los discos de sistema operativo y datos a partir de las instantáneas correspondientes y, luego, cree una nueva máquina virtual conectando los discos administrados.</span><span class="sxs-lookup"><span data-stu-id="11f68-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="11f68-107">También puede restaurar los discos de datos de una máquina virtual existente conectando los discos de datos creados a partir de las instantáneas.</span><span class="sxs-lookup"><span data-stu-id="11f68-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="11f68-108">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="11f68-108">Sample script</span></span>

<span data-ttu-id="11f68-109">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Crear un disco administrado a partir de una instantánea")]</span><span class="sxs-lookup"><span data-stu-id="11f68-109">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="11f68-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="11f68-110">Script explanation</span></span>

<span data-ttu-id="11f68-111">Este script usa los siguientes comandos para crear un disco administrado a partir de una instantánea.</span><span class="sxs-lookup"><span data-stu-id="11f68-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="11f68-112">Cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="11f68-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="11f68-113">Comando</span><span class="sxs-lookup"><span data-stu-id="11f68-113">Command</span></span> | <span data-ttu-id="11f68-114">Notas</span><span class="sxs-lookup"><span data-stu-id="11f68-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="11f68-115">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="11f68-115">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="11f68-116">Obtiene todas las propiedades de una instantánea usando las propiedades de nombre y grupo de recursos de la instantánea.</span><span class="sxs-lookup"><span data-stu-id="11f68-116">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="11f68-117">La propiedad de identificador se utiliza para crear disco administrado.</span><span class="sxs-lookup"><span data-stu-id="11f68-117">Id property is used to create managed disk.</span></span>  |
| [<span data-ttu-id="11f68-118">az disk create</span><span class="sxs-lookup"><span data-stu-id="11f68-118">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="11f68-119">Crea un disco administrado usando un identificador de una instantánea administrada</span><span class="sxs-lookup"><span data-stu-id="11f68-119">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="11f68-120">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="11f68-120">Next steps</span></span>

[<span data-ttu-id="11f68-121">Crear una máquina virtual conectando un disco administrado como disco del SO</span><span class="sxs-lookup"><span data-stu-id="11f68-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="11f68-122">Para más información sobre la CLI de Azure, consulte la [documentación de la CLI de Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="11f68-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="11f68-123">Encontrará más ejemplos de scripts de la CLI de máquina virtual y discos administrados en la [documentación de Azure sobre máquinas virtuales Linux](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="11f68-123">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
